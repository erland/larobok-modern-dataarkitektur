# 10. Dataprodukter, dataägande och datakontrakt

En informationsleverans kan vara tekniskt stabil och ändå svår att använda. Konsumenten behöver inte bara veta vilka fält som finns, utan vad uppgifterna betyder, vilka begränsningar de har och vem som ansvarar när något förändras. Dataprodukten gör dessa frågor till en del av leveransens utformning, inte till ett problem som varje konsument måste lösa på nytt.

## Från dataset till dataprodukt

Ett dataset är en avgränsad mängd data. En dataprodukt är i bokens mening ett förvaltat erbjudande där ett eller flera dataset görs användbara för identifierade konsumentbehov. Produkten omfattar informationen, dess åtkomstgränssnitt, dokumentation, ansvar och livscykel. Goedegebuure m.fl. sammanställer 114 publikationer från industrin och identifierar produktperspektivet och domänbaserat dataägande som två av fyra centrala Data Mesh-principer [K006]. Översikten beskriver praktikernas perspektiv, inte uppmätta effekter av att införa dataprodukter. Principen kan emellertid användas även i en centraliserad organisation.

En produkt kan exponeras som en tabell, en filbaserad leverans, ett API eller en händelseström. Det avgörande är inte gränssnittets teknik utan vad konsumenten kan förvänta sig av det. En dokumenterad mottagningszon kan därför utvecklas till en dataprodukt utan att byta lagringsteknik.

| Egenskap | Teknisk informationsleverans | Förvaltad dataprodukt |
|---|---|---|
| Struktur | Fält och typer dokumenterade | Stabilt, versionerat gränssnitt |
| Semantik | Kan kräva kännedom om källsystemet | Betydelse, urval och begränsningar förklarade |
| Kvalitet | Kontroller kan finnas | Mätbara kvalitetsmål och kända avvikelser |
| Ansvar | Förvaltning av flödet | Utpekat ansvar för hela erbjudandet |
| Förändring | Samordning från fall till fall | Planerade kompatibilitetsregler och avveckling |
| Åtkomst | Teknisk anslutning | Beskrivna villkor och behörighetsprocess |

Tabellen är en idealtypisk jämförelse, inte en klassificering av tekniker. Ett väldokumenterat API med motsvarande åtaganden kan redan vara en dataprodukt. Omvänt är en tabell i en produktkatalog inte automatiskt en dataprodukt.

## Produktgränser och ansvar

Källorienterade dataprodukter återger information nära den verksamhet som skapar den. De bör erbjuda stabila verksamhetsbegrepp utan att i onödan exponera interna databastabeller eller applikationens implementation. Konsumentorienterade dataprodukter kombinerar eller bearbetar information för ett visst behov, exempelvis en uppföljning av handläggningstider. Mellan dessa kan det finnas gemensamma produkter som harmoniserar identifierare eller kodverk.

I den fiktiva referensmyndigheten kan ett ärendehanteringsstöd tillhandahålla en produkt för registrerade ärenden. En annan produkt kan kombinera ärenden med kontrollresultat för analys av ledtider. Den senare behöver eget förvaltningsansvar för kopplingsregler, urval och härledda mått; ansvaret kan inte enbart hänvisas tillbaka till källsystemen. Produkterna behöver inte ha samma lagringsplats eller utvecklingsteam.

En rimlig ansvarsfördelning skiljer mellan verksamhetens mandat att definiera informationens betydelse och användningsvillkor, produktförvaltarens ansvar för leveransen och plattformsteamets ansvar för de gemensamma tekniska tjänsterna. Begreppet dataägare innebär här ett organisatoriskt ansvar, inte äganderätt eller en förändring av myndighetens rättsliga ansvar. Konsumenten ansvarar också för att bedöma om uppgifterna är lämpliga för sitt ändamål.

Produktgränsen bör följa ett begripligt informationsområde och en hanterbar förändringstakt. Att skapa en produkt för varje tabell ger ofta för många beroenden. Att göra hela myndighetens information till en enda produkt gör i stället ansvar och förändringar svåra att avgränsa. Utgå från sammanhängande konsumentbehov och ett team med faktiskt mandat och resurser att upprätthålla åtagandena.

## Datakontrakt som gränssnitt

Ett datakontrakt beskriver vad producent och konsument kan förvänta sig av informationsleveransen. Kontraktet är ett tekniskt och organisatoriskt åtagande; det behöver inte vara ett juridiskt avtal. Open Data Contract Standard (ODCS), exempelvis version 3.0.0, visar hur bland annat schema, kvalitetsregler, ansvar och servicenivåer kan representeras maskinläsbart [K072]. En standardiserad representation kan användas för olika leveranstekniker. Kontraktsfilen verkställer dock inga kontroller av sig själv: reglerna måste kopplas till publicering, övervakning och hantering av avvikelser.

Ett praktiskt kontrakt bör åtminstone täcka följande delar:

- Struktur: fält, datatyper, identifierare, obligatoriska värden och relationer.
- Semantik: definitioner, måttenheter, tidsbegrepp, kodverk, urval och vad en post representerar.
- Kvalitet: exempelvis fullständighet, dubbletter och tillåtna värden, inklusive hur avvikelser rapporteras.
- Servicenivå: aktualitet, tillgänglighet, återställning och kontaktvägar, anpassade till konsumenternas behov.
- Användningsvillkor: informationsklassning, tillåtna ändamål, åtkomstvillkor och bevarandevillkor.
- Förändring: versioner, kompatibilitetsregler, kommunikation och avvecklingsvillkor.

Ett kvalitetsmål behöver vara mätbart och ha en definierad mätpunkt. Att lova daglig uppdatering säger exempelvis inte om dagens leverans ska vara färdig före arbetsdagens början eller om uppgifterna omfattar alla händelser fram till föregående dygns slut. Ett illustrativt mål är att 99 procent av arbetsdagarnas leveranser under ett kvartal ska vara tillgängliga före kl. 07.00 och omfatta föregående dygns registrerade ärenden. Aktualitet och fullständighet måste då mätas separat, med regler för sena registreringar och rättelser. Skilj mellan ett uppföljningsbart servicenivåmål och ett formellt åtagande, ofta benämnda SLO respektive SLA. Kraven bör stå i proportion till konsekvenserna av en utebliven eller felaktig leverans.

### Strukturell och semantisk kompatibilitet

Ett schemaregister kan automatisera vissa kompatibilitetskontroller. Bakåtkompatibilitet innebär i Confluents terminologi att en konsument med det nya schemat kan läsa äldre data. Framåtkompatibilitet innebär att en konsument med det äldre schemat kan läsa data enligt det nya. Full kompatibilitet kombinerar båda. Transitiv kontroll omfattar alla tidigare registrerade versioner inom samma schemaämne (subject), inte enbart den närmast föregående. Vilka förändringar som accepteras beror på schemaformat och konfiguration [K038].

Detta är inte samma sak som att en förändring är säker för verksamheten. Anta att fältet `avslutsdatum` tidigare angav när ett ärende avgjordes, men efter en systemändring anger när beslutet expedierades. Datatypen är oförändrad och en schemakontroll kan därför passera, samtidigt som statistiken över handläggningstid förändras. Om den ursprungliga betydelsen ingår i kontraktet är detta en brytande förändring. Producenten kan exempelvis bevara den ursprungliga definitionen och exponera expedieringsdatum som ett nytt fält. Om den ursprungliga betydelsen inte längre kan levereras behöver förändringen hanteras genom en ny kontraktsversion eller en uttryckligen överenskommen migrering.

Automatiserade kontroller kan verifiera exempeldata, kodvärden, kvalitetsregler och vissa kontraktsvillkor. De kan inte på egen hand avgöra om en ny verksamhetsdefinition är korrekt eller om ett nytt användningsändamål är tillåtet. Det kräver ansvariga personer och dokumenterade beslut.

## Förändring och livscykel

En produktversion bör identifiera det kontrakt konsumenten förlitar sig på, oberoende av vilken applikationsversion som producerar uppgifterna. En intern databasändring kan då hanteras genom att producenten bibehåller den publicerade representationen. En ny uppgift kan publiceras efter kontroll av både kontrakt och berörda konsumenters faktiska beteende, medan en brytande förändring kan kräva en parallell version under en övergångsperiod.

Parallella versioner har en kostnad: dubbla kontroller, ytterligare drift och risk för otydlighet. De bör därför ha ett uttalat slutdatum, kommunicerade migrationsvillkor och en verifierad väg för konsumenterna att byta. För historiska rapporter kan den gamla definitionen behöva dokumenteras även när den gamla leveransversionen inte längre körs. Detta innebär inte att data alltid får bevaras; informationslivscykeln måste följa tillämpliga villkor.

Produktförvaltning omfattar också introduktion och avveckling. Registrera produkten i en sökbar katalog, ange kontaktväg och användningsbegränsningar och följ upp faktiska behov. En oanvänd produkt kan avvecklas efter kontroll av beroenden, inklusive periodiska rapporter och sällan körda analyser. En katalogpost utan aktiv förvaltning kan annars skapa en falsk bild av tillgänglighet och kvalitet.

## Inför dataprodukter där de gör skillnad

Referensmyndigheten behöver inte omvandla alla befintliga mottagningszoner samtidigt. Börja med leveranser där flera konsumenter återkommande behöver samma information eller där förändringar idag medför omfattande samordning. Bevara fungerande tekniska flöden, etablera ansvar och definiera kontrakt vid leveransgränsen. Automatisera därefter de kontroller som återkommer och följ upp både producentens arbetsbelastning och konsumentens förmåga att använda informationen.

Ett dataproduktperspektiv är motiverat när kostnaden för ett gemensamt åtagande är lägre än kostnaden för återkommande individuella tolkningar och integrationer. För ett tillfälligt engångsuttag kan en enklare dokumenterad leverans räcka. För kritisk återanvändbar information är stabil betydelse, tydligt ansvar och kontrollerad förändring viktigare än att alla leveranser använder samma teknik. Dataprodukten definierar vad som erbjuds; nästa kapitel behandlar hur konsumenter kan få tillgång till det.
