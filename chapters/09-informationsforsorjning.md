# 9. Informationsförsörjning från operativa IT-stöd

En myndighet kan ha en modern analysplattform och ändå behöva vänta månader på att få tillgång till ett nytt informationsfält. Om varje förändring förutsätter samordnade beställningar till flera specialistteam ligger begränsningen i informationsförsörjningen, inte nödvändigtvis i datalagret. Arkitekturvalet behöver därför omfatta hela vägen från att informationen uppstår i det operativa IT-stödet till att analysmiljön kan använda en förvaltad leverans.

## Skilj mellan överföring, bearbetning och publicering

Tre beslut som ofta blandas samman är hur information hämtas från källan, var den bearbetas och vad som erbjuds konsumenten. ETL (Extract, Transform, Load) innebär att informationen bearbetas före inläsning i det avsedda målet. ELT (Extract, Load, Transform) innebär att den först läses in och därefter bearbetas där eller med motorer kopplade till målet. Den avgörande skillnaden är ordningsföljden [K069]. Samma organisation kan använda båda mönstren i olika delar av ett flöde.

ETL kan vara lämpligt när information måste filtreras eller skyddas innan den lämnar källmiljön. ELT kan underlätta ombearbetning när ursprungliga leveranser får bevaras och nya analysbehov tillkommer. Inget av mönstren säger i sig om överföringen sker via filer, API:er eller förändringsloggar, vem som äger flödet eller hur snabbt en ändring kan införas. Inte heller innebär ELT att all källdata bör kopieras till analysmiljön.

## Mönster för överföring

| Mönster | Lämpligt när | Viktig begränsning |
|---|---|---|
| Periodisk fullständig leverans | Datamängden är hanterbar och aktualitetskravet måttligt | Upprepad överföring; historiska ändringar mellan uttag kan förloras |
| Inkrementellt batchuttag | Ändringar kan identifieras med en tillförlitlig markör | Raderingar, samtidiga ändringar och felaktiga tidsmarkörer måste hanteras |
| API-baserad hämtning | Källan erbjuder avgränsad, stabil åtkomst | Sidindelning, uttagsgränser och konsekventa uttag behöver hanteras |
| Loggbaserad CDC | Täta förändringar ska fångas utan återkommande fullständiga uttag | Beroende av källans loggar, behörigheter och tekniska schema |
| Verksamhetshändelser | Betydelsefulla verksamhetsförändringar ska kommuniceras | Kräver uttrycklig modellering och en tillförlitlig publiceringsmekanism |

Batch är ett sätt att gruppera överföring i avgränsade körningar, inte en särskild transportteknik. Ett API kan användas för både batchuttag och tätare hämtning. Streaming innebär fortlöpande behandling av inkommande data, ofta med buffring och små bearbetningsintervall. Det garanterar inte att konsumentens information är aktuell i realtid. Aktualiteten måste mätas hela vägen från källhändelse till användbart resultat.

### Change Data Capture

CDC (Change Data Capture) identifierar förändringar i källinformation. En loggbaserad variant läser databasmotorns förändringslogg. Debeziums PostgreSQL-anslutning är ett exempel där initiala eller inkrementella ögonblicksbilder kan kombineras med fortlöpande förändringshändelser [K067]. Det kan minska behovet av särskilda exportfunktioner i varje applikation, men anslutningen behöver hantera bland annat loggbevarande, återstart och förändrade databasscheman. Om ändringsloggen inte längre täcker ett avbrott kan en ny ögonblicksbild och avstämning behövas. Loggläsning eliminerar inte heller belastningen från initiala uttag.

Databasens förändringslogg beskriver inte automatiskt verksamhetens avsikt. En ändrad statuskolumn kan exempelvis representera en rättelse, ett beslut eller en teknisk migrering. Flera ändringar kan dessutom tillsammans utgöra en enda verksamhetshändelse. Om konsumenterna binds direkt till interna tabeller kan en refaktorering av källsystemet kräva förändringar i flera analysflöden. CDC är därför ofta en bra intern överföringsmekanism, men behöver inte vara det gränssnitt som erbjuds analyskonsumenterna.

### Händelser och API:er

En verksamhetshändelse uttrycker att något av betydelse har inträffat, exempelvis att ett ärende har avgjorts. Den kan ge konsumenten ett stabilare semantiskt gränssnitt än en följd av ändrade databasrader. Händelsen kan innehålla de uppgifter som behövs för ett analysändamål eller en identifierare som används för kompletterande hämtning. I det senare fallet måste det vara klart om hämtningen ger informationens aktuella eller historiska tillstånd.

Om applikationen både uppdaterar en databas och publicerar ett meddelande kan ett av stegen misslyckas. Ett sätt att minska denna risk är en transaktionell outbox: verksamhetsändringen och en publiceringspost skrivs i samma lokala transaktion, varefter en separat mekanism levererar posten. Publiceringsposten blir därmed atomärt lagrad med verksamhetsändringen, men själva meddelandeleveransen sker separat och kan fördröjas eller upprepas. Konsumenten måste ändå kunna hantera omleveranser [K070]. En kö eller händelseplattform ersätter inte heller behovet av en initial leverans av befintlig information och en strategi för att bygga upp ett analyslager på nytt.

Ett operativt API som hämtar enskilda ärenden är inte nödvändigtvis lämpligt för ett analysuttag av miljontals poster. Ett separat exportgränssnitt kan erbjuda större uttag, stabila markörer och tydliga regler för historik. Att tillgängliggöra information innebär därmed inte att alla konsumenter måste använda samma tekniska gränssnitt. Diggs vägledning om tillgängliggörande av information ger ett offentligt perspektiv på val av format och öppna specifikationer [K068]; den ska inte tolkas som att skyddad intern information måste publiceras externt.

## Tillförlitlig leverans är mer än lyckad transport

En överföring kan vara tekniskt framgångsrik men ändå lämna ett ofullständigt eller missvisande analysunderlag. Foidl med flera undersöker faktorer som påverkar kvalitet i datapipelines genom litteratur, åtta expertintervjuer och analys av GitHub-projekt och Stack Overflow-inlägg [K004]. En arkitekturmässig slutsats av studien är att kvalitet behandlas som en egenskap hos hela flödet, inte enbart som en kontroll av slutresultatet.

För en förvaltad leverans behöver följande frågor besvaras:

- Hur upptäcks saknade, dubblerade eller försenade leveranser? Använd exempelvis sekvensmarkörer, kontrollsummor, antal poster och verksamhetsmässiga avstämningar där de är meningsfulla.
- Hur hanteras felaktiga poster? En isolerad felmängd kan möjliggöra fortsatt bearbetning, men konsumenten måste veta när resultatet är ofullständigt. Ett stopp kan vara nödvändigt för vissa kritiska leveranser.
- Hur återställs flödet? Bevara bearbetningspositioner och stöd omläsning inom tillåtna bevarandetider. Gör mottagarens uppdateringar idempotenta där det går, så att samma leverans inte ger dubbla effekter.
- Hur hanteras rättelser och raderingar? Skilj verksamhetstid från registrerings- och mottagningstid. En sen rättelse kan behöva påverka tidigare analysperioder utan att äldre rapporter skrivs om i tysthet.
- Hur upptäcks schemaändringar? Automatiska strukturkontroller behöver kompletteras med bedömning av ändrad verksamhetsbetydelse.

Mät aktualitet, fullständighet och återställningsförmåga tillsammans. En låg fördröjning är av begränsat värde om felaktig information snabbt sprids. Leveransgarantier för en meddelandebuss säger inte automatiskt något om exakt en effekt i ett separat målsystem; detta måste säkerställas i hela bearbetningskedjan. Kafka skiljer exempelvis mellan transaktionell bearbetning mellan egna ämnen (topics) och leverans till externa målsystem, där mottagaren också behöver medverka [K071]. En praktisk lösning kan vara att atomärt registrera bearbetad händelseidentitet tillsammans med uppdateringen i målet.

## Från specialistberoende till självbetjänad informationsförsörjning

I den fiktiva referensmyndigheten finns två etablerade vägar till en systemspecifik mottagningszon (stage area): ett centralt ETL-flöde eller applikationsutvecklade händelser som bearbetas och skrivs till zonen. Strukturen är dokumenterad i båda fallen. Det är en användbar grund för att skilja operativ från analytisk bearbetning, men säger ännu inte hur självständigt systemteamet kan förändra sin leverans.

Anta att ett nytt fält behöver göras tillgängligt. I ETL-alternativet kan systemteamet behöva anlita en specialist för att ändra en mappning, testa överföringen och beställa driftsättning. I händelsealternativet kan motsvarande förändring kräva kodändringar i applikationen och i en separat mottagare, samordnade releaser och specialistkompetens i meddelandeplattformen. Att den ena lösningen använder batch och den andra händelser avgör inte i sig vilken som har kortast ledtid.

Ett mer självbetjänat alternativ är att erbjuda standardiserade anslutningar och ett deklarativt sätt att beskriva leveransen: godkänd källa, utvalda fält, transformationsregler, leveransfrekvens, kvalitetskontroller och ansvarig. Plattformen tillhandahåller körning, övervakning, säkerhetskontroller och återställning. Ett nytt fält får dock inte publiceras automatiskt bara för att det finns i källan: informationsklassning och behörighetsvillkor måste vara uppfyllda. Systemteamet ska inom dessa ramar kunna testa och publicera en kompatibel förändring utan att beställa en unik teknisk lösning. Avancerade transformationer och ovanliga källsystem kan fortfarande kräva specialiststöd.

Netflix beskriver Data Bridge som ett gemensamt styrskikt för dataförflyttning som återanvänder befintliga exekveringsmotorer. Användaren kan bland annat ange sin leverans genom konfiguration, medan styrskiktet väljer underliggande implementation. Stöd för både batch och streaming anges som ett designkrav [K010]. Det är ett exempel på organisationens egen dokumentation av hur tekniska variationer kan döljas bakom ett standardiserat erbjudande. Det visar ett möjligt mönster, inte att motsvarande ledtidsvinster är säkerställda i en myndighetsmiljö.

### Jämför hela leveranskedjan

Anta att referensmyndigheten behöver tillgängliggöra en redan registrerad uppgift om ärendets avgörandegrund som hittills inte har varit tillgänglig för analys. Uppgiften får användas för det aktuella ändamålet, men dess värdemängd behöver dokumenteras. Följande tre realiseringar är tänkbara; samtliga kan leverera till samma mottagningszon.

| Realisering | Kedja från källa till mottagningszon | Förändring av leveransen |
|---|---|---|
| Specialistutvecklad ETL | Källuttag → centralt ETL-jobb → mottagningszon | Systemteamet beskriver uppgiften; ETL-teamet ansvarar i detta exempel för ändrat uttag, mappning, test och driftsättning. |
| Individuell händelseintegration | Applikation → outbox → meddelandeplattform → mottagare → mottagningszon | Producenten ändrar händelsens innehåll; mottagaren anpassar bearbetning och målstruktur där det behövs. |
| Deklarativ självbetjäning | Godkänd källa → konfigurerad anslutning → gemensam exekvering → mottagningszon | Systemteamet ändrar leveransbeskrivningen, testar och publicerar inom fastställda villkor. |

![Tre alternativa leveranskedjor till samma typ av mottagningszon, med exempel på ansvar vid en förändring. Självbetjäning förutsätter en godkänd källa, stödd anslutning och uppfyllda publiceringsvillkor. Batch eller händelser avgör inte i sig förändringsledtiden; dataprodukter kan byggas ovanpå alla tre alternativen. Analytisk bearbetning efter mottagning ingår inte i bilden.](../assets/generated/IMG-09-01.svg)

I det första alternativet kan en förändring vara tekniskt enkel men ändå behöva vänta i en annan grupps arbetskö. I det andra kan samma team äga både producent och mottagare, vilket minskar organisatoriska överlämningar men inte eliminerar kodarbete. Om mottagaren stöder kompatibla schemautökningar behöver den inte alltid ändras. I det tredje alternativet kan en standardiserad anslutning hantera uttag och mottagning utan ny flödesspecifik kod. Förutsättningen är att fältet redan exponeras av en godkänd källa och att plattformen stöder förändringen. Annars krävs fortfarande ändringar i källan eller i plattformens anslutning.

En förvaltad dataprodukt kan byggas ovanpå alla tre alternativen. Den tillför ett uttryckligt informationsåtagande: betydelse, struktur, aktualitet, ansvar och förändringsvillkor. Produkten kan erbjuda mottagningszonens dataset som gränssnitt, eller exponera det genom exempelvis ett API eller en frågetjänst. Ett tillagt fält blir inte automatiskt tillgängligt för alla konsumenter; produktens kontrakt och åtkomstvillkor avgör detta. Kapitel 10 fördjupar denna skillnad mellan leverans och produkt.

Förändringsarbetet slutar inte vid mottagningszonen. Om ett gemensamt mått eller en rapport ska använda avgörandegrunden behöver även den analytiska bearbetningen och konsumtionen anpassas. Självbetjäning i leveransledet eliminerar inte detta arbete. Vid jämförelsen bör därför både tiden fram till publicerat källdataset och tiden fram till användbart analysresultat följas upp separat.

Standardisering flyttar en del av komplexiteten från enskilda leveranser till plattformens utveckling och förvaltning. Det är motiverat när många team har återkommande likartade behov. Om varje system kräver en unik anslutning, transformation och säkerhetsmodell kan ett gemensamt verktyg i stället bli ytterligare ett beroende. Plattformens framgång bör därför bedömas genom exempelvis ledtid från beslutad ändring till användbar data, andel rutinändringar som team klarar själva och antal manuella överlämningar. Mät även kvalitet och återställning så att snabbare publicering inte sker på bekostnad av tillförlitligheten.

## Välj mönster utifrån behov, inte teknikpreferens

I en reglerad organisation bör valet börja med informationsbehovet, tillåten behandling, krav på historik och högsta acceptabla fördröjning. Ett dagligt stabilt batchuttag kan vara tillräckligt för återkommande statistik, medan operativ riskanalys kan motivera tätare förändringsleveranser. Båda kan stödjas av en gemensam plattform utan att använda samma överföringsmekanism. För inköpta system bör exportmöjligheter, dokumentation och förändringshantering beaktas redan i kravställningen; annars riskerar informationsförsörjningen att bli beroende av leverantörens individuella anpassningar.

En dokumenterad mottagningszon är ett möjligt leveransgränssnitt, men dess existens bevisar varken självbetjäning, stabil semantik eller förvaltat dataägande. Nästa steg i arkitekturen är att definiera vad konsumenterna kan förvänta sig av leveransen, vem som ansvarar för den och hur förändringar hanteras. Det är kärnan i dataprodukter och datakontrakt, som behandlas i nästa kapitel.
