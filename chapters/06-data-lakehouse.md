# 6. Data Lakehouse

Anta att referensmyndigheten har etablerat flexibel lagring för dokument, händelser och tabulära utdrag, men att rapporteringen fortfarande kräver överföring till ett separat Data Warehouse. Skulle samma lagringsgrund kunna användas för både återkommande rapporter och mer experimentell analys, utan att ge avkall på konsistens och förvaltningsbarhet? Det är den fråga som Lakehouse-arkitekturen försöker besvara.

## Från filer till förvaltade tabeller

Armbrust med flera presenterade 2021 Lakehouse som ett arkitekturmönster där öppna dataformat, avancerad analys och datalagerfunktionalitet förenas [K001]. Ambitionen är att minska behovet av parallella analytiska lagringsmiljöer. Det är ett arkitekturförslag, inte ett belägg för att alla Data Warehouse kan ersättas med bättre resultat.

En viktig skillnad mot en enklare Data Lake är möjligheten att med ett tabellformat behandla en samling filer som en sammanhängande, versionshanterad tabell. En analys ska inte behöva avgöra vilka filer som råkar finnas i en katalog vid lästillfället. Den ska kunna utgå från ett definierat tabelltillstånd, även när andra processer uppdaterar informationen.

Tre nivåer behöver hållas isär:

| Nivå | Uppgift | Exempel |
|---|---|---|
| Lagringsmedium | Beständig lagring av filer och objekt | Objektlagring, distribuerat filsystem |
| Filformat | Representation av information i en enskild fil | Parquet, ORC |
| Tabellformat | Samordning av filer, tabellmetadata och versioner | Iceberg, Delta Lake, Hudi |

![Logisk Lakehouse-arkitektur där kompatibla motorer använder förvaltade tabeller med metadata och versioner över gemensam lagring. Inläsningens pil avser skrivning via kompatibla motorer, inte direkt skrivning förbi tabellprotokollet. Dokument kan också bevaras som filer utan att bli tabeller. Dubbelriktade pilar visar logisk åtkomst och resultat eller läsning och skrivning där det stöds.](../assets/generated/IMG-06-01.svg)

Apache Parquet är ett kolumnorienterat filformat med stöd för komprimering och kodning [K048]. När en fråga bara behöver ett fåtal kolumner kan en lämplig läsmotor begränsa mängden information som läses. Parquet definierar däremot inte på egen hand en transaktion som omfattar flera filer. Det är tabellformatet tillsammans med kompatibla läs- och skrivmotorer som hanterar den uppgiften.

## Transaktioner och tabelltillstånd

Tänk dig en tabell över avslutade ärenden som behöver korrigeras efter att ett fel i ett källsystem har upptäckts. En uppdatering kan beröra flera datafiler. Om en rapport läser några gamla och några nya filer samtidigt kan resultatet bli inkonsekvent.

En transaktionell tabellmekanism kan i stället publicera ändringen som ett nytt konsistent tabelltillstånd. En läsare kan då arbeta mot en tidigare version medan skrivningen slutförs. Vilken isolering som faktiskt erhålls beror på format, protokoll, motor och lagringssystem.

Begreppet ACID avser atomicitet, konsistens, isolering och beständighet. I Lakehouse-sammanhang måste arkitekten undersöka vilken omfattning garantierna har. En atomär ändring av en tabell innebär inte automatiskt att ändringar av flera tabeller genomförs som en gemensam transaktion. Inte heller innebär teknisk konsistens att informationen är verksamhetsmässigt korrekt.

Versionshanteringen kan göra det möjligt att läsa ett äldre tabelltillstånd, ofta kallat time travel, så länge nödvändig metadata och datafiler finns kvar. För reproducerbarhet behöver även bearbetningskod, konfiguration och relevanta källdata kunna återskapas. Historiska tabellversioner måste dessutom hanteras utifrån informationens bevarandevillkor; versionshantering får inte bli ett sätt att kringgå gallring.

## Tre tabellformat

Apache Iceberg, Delta Lake och Apache Hudi har överlappande ambitioner men olika tekniska mekanismer. Valet påverkar både vilka motorer som kan användas och hur tabellerna behöver förvaltas.

### Apache Iceberg

Iceberg beskriver tabellens tillstånd med metadata och snapshots. En snapshot refererar via en manifestlista till manifest som beskriver tabellens filer och deras metadata. Det kan hjälpa frågemotorn att undvika läsning av irrelevanta filer [K049]. En tabell kan därmed förändras utan att läsaren behöver använda kataloglistning som källa till sanningen.

Formatet har mekanismer för att förändra schema och partitionering över tid utan att alla äldre filer måste skrivas om för varje sådan förändring [K049]. För en stor organisation är det särskilt intressant när olika bearbetningsmotorer behöver använda samma tabeller. Arkitekten måste dock verifiera att motorerna stöder just de funktioner och formatversioner som ska användas, inklusive ändringar och borttagning av rader.

### Delta Lake

Delta Lake använder en transaktionslogg för att beskriva tabellens förändringar [K053]. Kompatibla läsare kan utgå från ett konsistent tillstånd medan skrivare genomför förändringar. Dokumentationen beskriver optimistisk samtidighetskontroll där en skrivning valideras före publicering och kan avvisas om den står i konflikt med en annan skrivning [K050].

Bearbetningsflöden behöver därför hantera konflikter och vid behov försöka igen efter förnyad validering, utan att skapa dubbla verksamhetshändelser. För en organisation som använder flera motorer är det viktigt att kontrollera kompatibilitet med de protokollfunktioner som aktiveras i tabellen. Stöd för att läsa grundläggande tabeller är inte samma sak som stöd för alla skrivoperationer.

### Apache Hudi

Hudi skiljer mellan två tabelltyper som illustrerar en viktig avvägning mellan kostnaden för läsning och kostnaden för förändring. Med Copy-on-Write skrivs berörda basfiler om vid uppdateringar. Med Merge-on-Read kan förändringar läggas i loggfiler och senare sammanföras med basfilerna genom sammanfogning och omskrivning, så kallad compaction [K051].

Det senare mönstret kan göra täta uppdateringar enklare att hantera, men läsning av det aktuella tillståndet kan kräva ytterligare bearbetning. Hudi erbjuder också inkrementella frågemönster. För Merge-on-Read kan en läsoptimerad fråga som enbart läser basfiler ge ett äldre resultat än en snapshot-fråga som också beaktar loggade förändringar [K051]. För referensmyndigheten är det relevant om stora informationsmängder regelbundet kompletteras med ändrade ärendeuppgifter. Nyttan måste vägas mot kraven på underhåll och stöd i valda motorer.

### Valet av tabellformat

Det finns inte tillräcklig grund för att rangordna formaten oberoende av arbetslast. LHBench jämförde de tre alternativen med bland annat inläsning, uppdateringar, analytiska frågor och ett stort antal filer. Testerna från december 2022 genomfördes med Spark i AWS EMR, S3 och specifika dåtida programversioner [K002]. De illustrerar betydelsen av arbetslast och realisering, men utgör inte ett aktuellt produktfacit för en lokalt driftad myndighet.

En egen utvärdering bör därför omfatta läsning, skrivning, uppdatering, borttagning, samtidighet, schemaändringar, återställning och löpande tabellunderhåll. Det är hela kombinationen av format, motorer och lagring som ska utvärderas.

## Frågemotorer och kataloger

Ett tabellformat beskriver tabellens filer och metadata; det är inte i sig en frågemotor. En motor som Apache Spark kan användas för distribuerad bearbetning [K054], medan en SQL-frågemotor som Trino kan vara ett alternativ för interaktiv analys [K055]. Andra motorer kan vara lämpliga för mindre arbetslaster eller specialiserade uppgifter. Exemplen är teknikroller, inte en rekommendation om en viss produktkombination.

Separat skalning av beräkningsresurser gör det möjligt att dimensionera olika arbetslaster oberoende av lagringsvolymen. Det innebär dock inte fullständig resursisolering. Gemensam objektlagring, nätverk och katalogtjänster kan fortfarande bli flaskhalsar. För rapportering med höga krav på förutsägbara svarstider kan särskild kapacitet, optimerade tabeller eller kompletterande serving-lager behövas.

En teknisk tabellkatalog hjälper motorerna att hitta tabeller och deras metadata. I vissa realiseringar deltar katalogen också i samordningen av uppdateringar. En verksamhetsorienterad datakatalog har ett annat syfte: att beskriva vad informationen betyder, vem som ansvarar för den och vilka användningsvillkor som gäller. Dessa funktioner kan finnas i samma produkt men behöver bedömas var för sig.

En öppen fil- och tabellrepresentation minskar vissa beroenden, men friheten att byta motor förutsätter fungerande kompatibilitet, åtkomstkontroll och tillgång till metadata. Om en ny motor bara kan läsa datafilerna och inte tolka tabellens ändringar eller säkerhetsregler är portabiliteten begränsad.

## Medallion Architecture

Medallion är ett namn på en zonbaserad bearbetningsmodell där information förädlas stegvis. Databricks dokumentation beskriver tre nivåer: Bronze för källnära data, Silver för kvalitetssäkrad och bearbetad information och Gold för konsumtionsanpassade representationer [K052].

För referensmyndigheten skulle Bronze kunna innehålla mottagna ärendehändelser, Silver kvalitetssäkrade och sammanställda ärendeposter och Gold underlag för verksamhetsuppföljning. Ett rapporteringslager kan fortfarande använda dimensionsmodellering enligt kapitel 4. Lakehouse gör alltså inte behovet av informationsmodellering mindre i de delar där gemensamma begrepp och mått är avgörande.

Medallion är varken en förutsättning för Lakehouse eller en garanti för kvalitet. Organisationen behöver inte skapa tre fysiska kopior av varje dataset. En zon kan i vissa fall representeras genom vyer eller andra logiska avgränsningar. Antalet bearbetningssteg ska motiveras av återanvändning, kvalitetskrav, åtkomst och driftbehov.

## Vad en fungerande Lakehouse-miljö kräver

Vid lokal drift behöver referensmyndigheten själv eller genom en tjänsteleverantör säkerställa de förmågor som annars kan ingå i en integrerad molntjänst. Följande är en arkitekturmässig miniminivå för en fleranvändarmiljö med förvaltade analytiska tabeller, inte en universell produktlista.

| Förmåga | Praktiskt krav |
|---|---|
| Lagring | Beständig och återställningsbar lagring med verifierade egenskaper för valda skrivprotokoll |
| Tabellhantering | Kompatibla skrivare och läsare, versionshantering och kontrollerade förändringar |
| Bearbetning | Motorer för relevanta arbetslaster och styrning av resursutnyttjande |
| Katalog | Tillförlitlig registrering och åtkomst till tabellmetadata |
| Säkerhet | Identiteter, åtkomstkontroller och revisionsspår även vid direkt filåtkomst |
| Drift | Övervakning, uppgraderingar, återställningsprov och automatiserat tabellunderhåll |
| Informationsförsörjning | Kontrollerade flöden för inläsning, kvalitetskontroll och publicering |

Särskilt viktigt är att inte underskatta arbetet med tabellunderhåll. Många små skrivningar kan skapa ett stort antal filer och omfattande metadata. Beroende på format och användning behöver filer samlas om, metadata optimeras och äldre versioner tas bort under kontrollerade former. Icebergs underhållsdokumentation beskriver exempelvis omskrivning av datafiler och utfasning av snapshots [K056]. Underhållsarbetet förbrukar beräkningsresurser och måste samordnas med läsning, skrivning och bevarandekrav.

Ett annat kritiskt område är direktåtkomst till lagringen. Om behörigheter endast kontrolleras i SQL-motorn men användare kan läsa underliggande objekt direkt, riskerar de att kunna kringgå tabellens åtkomstregler. Säkerhetsarkitekturen måste därför täcka samtliga tillåtna åtkomstvägar.

## När Lakehouse är ett motiverat alternativ

Lakehouse är särskilt intressant när organisationen behöver kombinera stora tabulära informationsmängder med avancerad analys och vill undvika vissa överföringar mellan olika analytiska miljöer. Det kan också vara motiverat när samma förvaltade tabeller behöver användas av flera motorer och organisationen vill ha större teknisk handlingsfrihet.

Om behovet framför allt är stabil rapportering baserad på väletablerade informationsmodeller kan ett modernt Data Warehouse vara enklare att förvalta. Om behovet främst är flexibel dokument- och fillagring kan en enklare Data Lake vara tillräcklig. Lakehouse innebär inte heller att alla dokument eller bilder måste representeras som tabeller.

Ett lämpligt första steg för referensmyndigheten är att välja en avgränsad arbetslast där dagens separata lagringsmiljöer skapar ett konkret problem. Utvärdera sedan om den nya lösningen kan uppfylla samma krav på rapportkvalitet, aktualitet, återställning och säkerhet med rimlig total förvaltningsinsats. Först när detta har visats finns ett tillräckligt beslutsunderlag för en bredare etablering. Kapitel 8 återkommer till jämförelsen mellan lagringsarkitekturerna.
