# 2. Operativ och analytisk datahantering

När en handläggare registrerar ett beslut måste IT-stödet kunna bekräfta att beslutet har sparats korrekt. När en analytiker undersöker hur besluten fördelat sig under de senaste fem åren behöver samma information kunna bearbetas tillsammans med ett stort antal andra uppgifter. Båda arbetsuppgifterna är viktiga, men de ställer olika krav på datahanteringen.

Att skilja på dessa krav är en förutsättning för att kunna avgöra vilka delar av en dataarkitektur som bör vara gemensamma och vilka som behöver separeras. Skillnaden handlar inte om vilka personer som använder informationen, utan om hur den bearbetas och vilka konsekvenser bearbetningen får.

## Två typer av arbetslaster

OLTP (Online Transaction Processing) avser transaktionsbearbetning där enskilda operationer läser eller förändrar ett avgränsat informationsinnehåll. Ett ärende kan exempelvis uppdateras genom en transaktion som ändrar dess status och registrerar ett beslut. Om flera förändringar ingår i samma atomära transaktion ska de antingen genomföras tillsammans eller inte alls.

OLAP (Online Analytical Processing) avser analytisk bearbetning, exempelvis summeringar, jämförelser och undersökningar av samband i större datamängder. En fråga kan behöva läsa många miljoner poster men bara ett fåtal attribut i varje post. Avancerad analys omfattar även andra arbetslaster än klassisk OLAP, exempelvis modellträning och bearbetning av dokument.

| Egenskap | Typisk OLTP | Typisk OLAP |
|---|---|---|
| Bearbetning | Många avgränsade operationer | Läsning och beräkning över stora urval |
| Svarstidskrav | Kort och förutsägbar svarstid per operation | Rimlig tid för hela analysen |
| Informationsbild | Ofta aktuellt verksamhetstillstånd | Ofta historik och sammanställda uppgifter |
| Samtidighet | Många samtidiga transaktioner | Varierande antal, ibland resurskrävande frågor |
| Optimering | Effektiva uppslag och ändringar | Effektiv skanning, filtrering och aggregering |

Egenskaperna är typiska, inte absoluta. Ett operativt IT-stöd kan behöva utföra aggregeringar, och en analytisk miljö måste också kunna hantera uppdateringar. En databasprodukt kan stödja båda arbetslasterna utan att vara lika lämplig för varje kombination av dem.

### Hur lagring påverkar bearbetningen

I radbaserad lagring ligger attributen för en post typiskt nära varandra, vilket passar många operationer som hämtar eller ändrar en hel post. Kolumnbaserad lagring samlar i stället värden för samma attribut. Vid en summering av exempelvis beslutsbelopp per månad kan frågemotorn därmed undvika att läsa många av de övriga attributen.

Stonebraker med flera beskrev 2005 C-Store, en relationsdatabas utformad för läsintensiva arbetslaster med bland annat kolumnlagring och komprimering [K031]. Artikeln redovisade preliminära prestandatester, inte ett allmängiltigt mått på skillnaden mellan rad- och kolumnbaserade databaser. Den illustrerar framför allt hur arbetslasten påverkar databasens fysiska utformning.

## Varför arbetslaster behöver isoleras

En omfattande analysfråga kan konkurrera med operativa transaktioner om processor, minne och lagringens I/O-kapacitet. Även när en databas kan hantera samtidiga läsningar och skrivningar utan att de direkt blockerar varandra kan konkurrensen om resurser påverka svarstiderna.

För referensmyndigheten är detta en verksamhetsrisk. Ett analysarbete som tillfälligt behöver mer kapacitet får inte göra ett kritiskt IT-stöd otillgängligt eller försämra handläggningen utöver accepterade gränser. Arkitekten behöver därför bedöma isoleringen ur flera perspektiv: resurskonkurrens, felpåverkan, behörigheter och oberoende förändring av informationsmodeller.

Isolering kan åstadkommas på olika nivåer. En avgränsad fråga i källsystemet kan vara tillräcklig om belastningen är liten och förutsägbar. En separat läsreplik kan avlasta den primära databasen, men har fortfarande beroenden till källsystemets struktur och replikeringsmekanism. En asynkron replik kan dessutom ligga efter källan. Ett självständigt analytiskt datalager ger större möjligheter att anpassa kapacitet, historik och modellering, men tillför kostnader och ansvar för informationsförsörjningen.

![Exempel på separerad operativ och analytisk datahantering. Parallella motriktade pilar visar transaktioner och svar respektive frågor och resultat. Den analytiska miljön försörjs med information från den operativa miljön. Graden av isolering väljs efter verksamhetskraven; läsrepliker och HTAP kan vara alternativa lösningar.](../assets/generated/IMG-02-01.svg)

### Ett dokumenterat exempel från CERN

CERN beskriver hur övervakningsdata från ATLAS-experimentets Detector Control System används för både drift och historiska analyser. Den operativa Oracle-miljön kompletterades med en analytisk miljö baserad på Hadoop, Parquet och Spark. En skrivskyddad replik användes som källa för datauttag till analysmiljön, som uppdaterades dagligen. Analysen kunde utföras i Jupyter-notebooks. Bakgrunden var bland annat att omfattande historiska frågor kunde belasta produktionsdatabaserna [K029].

Detta är organisationens egen beskrivning av en lösning i en forskningsmiljö. Den visar hur en operativ lagringslösning kan behållas samtidigt som ett kompletterande analyslager införs. Den visar däremot inte att samma teknik är det ekonomiskt bästa alternativet för en myndighet. Den överförbara lärdomen är att utgå från arbetslast och skyddsbehov, inte från en förutsättning om att den operativa databasen måste ersättas.

## Historik och informationsmodeller

En kopia av ett operativt system är inte nödvändigtvis ett tillräckligt analysunderlag. Anta att ett ärendes ansvariga organisatoriska enhet ändras när en omorganisation genomförs. Om källsystemet endast behåller den senaste tilldelningen går det inte att i efterhand avgöra vilken enhet som ansvarade för ärendet vid en tidigare tidpunkt utan kompletterande historik.

För analys behöver organisationen bestämma vilken tidsbild som ska representeras. Det kan finnas en skillnad mellan när en förändring faktiskt gällde i verksamheten och när den registrerades i systemet. En retroaktiv rättelse kan därför påverka historiska resultat. En rapport som ska kunna återskapas kan behöva bevara även information om vilken dataversion och vilka beräkningsregler som användes.

Informationsmodellen behöver också anpassas till frågan. En analys av genomloppstider kan exempelvis kräva att flera händelser kopplas till samma ärende och att start- och sluttid definieras entydigt. Detta är en annan uppgift än att registrera varje händelse korrekt. Därför finns det ett självständigt värde i analytiska modeller även om operativ och analytisk bearbetning kan ske i samma tekniska miljö. Modellering av datalager behandlas närmare i kapitel 4.

## När analys behöver vara verksamhetsnära

Operativ analys innebär att analysresultat används för att stödja den pågående verksamheten. En riskindikator kan exempelvis behöva beräknas i samband med att ett nytt ärende tas emot. Det betyder inte att all bearbetning måste utföras i det operativa IT-stödets databas.

Skilj mellan informationens aktualitet, tiden för själva beräkningen och tiden för att leverera resultatet till användaren. En riskindikator kan kombinera aktuella ärendeuppgifter med historiska mönster som beräknats i förväg. Då kan en relativt omfattande analys ligga utanför det kritiska transaktionsflödet, medan beslutstillfället endast kräver en avgränsad beräkning eller ett uppslag.

Om analysresultatet hämtas synkront från en separat tjänst blir tjänsten ett tillgänglighetsberoende för det operativa IT-stödet. Arkitekturen behöver då definiera vad som händer vid timeout, föråldrade data eller uteblivet svar. Ett reservförfarande måste vara förenligt med verksamhetskraven; det är inte alltid möjligt eller lämpligt att fortsätta utan riskbedömning.

### Kan OLTP och OLAP kombineras?

HTAP (Hybrid Transactional/Analytical Processing) är en inriktning där transaktions- och analysbearbetning kan stödjas i en gemensam databasmiljö. Kemper och Neumann presenterade 2011 forskningssystemet HyPer, där analytiska frågor kördes mot konsistenta ögonblicksbilder av transaktionsdata. Syftet var att möjliggöra samtidiga arbetslaster och minska aktualitetsproblemen vid överföring mellan separata system [K040]. Det är ett dokumenterat exempel på en teknisk möjlighet, inte en garanti för att alla moderna hybridlösningar klarar en organisations krav.

Gemensam bearbetning är särskilt intressant när analysen måste ligga nära transaktionernas aktuella tillstånd. Även här behöver resursisolering och påverkan vid fel verifieras; en konsistent ögonblicksbild innebär inte i sig garanterad svarstid. Den undanröjer dock inte behovet av informationsintegration över systemgränser, historik eller ändamålsenliga modeller. En hybrid databas kan därför komplettera ett gemensamt analyslager snarare än ersätta det.

## Arkitekturval utifrån arbetslasten

| Behov | Alternativ att pröva | Viktig kontroll |
|---|---|---|
| Enkel uppföljning av aktuella ärenden | Avgränsad fråga i operativ miljö | Belastning och åtkomst |
| Läsintensiv analys nära källsystemet | Läsreplik eller hybrid bearbetning | Fördröjning, isolering och felpåverkan |
| Historisk analys över flera IT-stöd | Separat analytisk miljö | Historik, semantik och datakvalitet |
| Riskindikator vid beslutstillfället | Förberäknat underlag och avgränsad aktuell beräkning | Aktualitet och beteende vid fel |

Tabellen är ett beslutsstöd, inte en uppsättning obligatoriska mönster. Före ett arkitekturbeslut bör organisationen fastställa accepterad påverkan på operativa svarstider, högsta tolererade informationsfördröjning, behov av historik och krav på återställning. Verifiera sedan lösningen med representativa samtidiga arbetslaster, inklusive belastningstoppar och återhämtning efter avbrott. Genomsnittliga svarstider räcker inte om verksamheten är känslig för enstaka långa väntetider.

Det centrala vägvalet är därmed vilken grad av självständighet den analytiska bearbetningen behöver, inte om den måste ligga i en viss produktkategori. Hur informationen förs mellan miljöerna är ett separat arkitekturbeslut som behandlas i kapitel 9.
