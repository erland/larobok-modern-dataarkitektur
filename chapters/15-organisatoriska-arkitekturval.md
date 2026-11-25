# 15. Jämförande analys av centraliserad, decentraliserad och federerad datahantering

En myndighet kan samla all analytisk lagring i en gemensam teknisk miljö och samtidigt fördela informationsansvaret mellan verksamhetsområden. Den kan också ha många separata datalager men en central organisation som beslutar om varje förändring. Valet av organisatorisk modell är därför inte detsamma som valet av lagringsarkitektur.

Den avgörande frågan är var beslut, kompetens och genomförandekapacitet behöver finnas för att informationen ska kunna utvecklas i takt med verksamheten, samtidigt som gemensamma krav uppfylls.

## Tre modeller för ansvarsfördelning

| Modell | Styrka | Risk | Lämpliga förutsättningar |
|---|---|---|---|
| Centraliserad | Samlad specialistkompetens och enhetlig modellering | Beställningsköer och avstånd till källans verksamhetskontext | Få kompetenta specialistteam, stort samordningsbehov |
| Decentraliserad | Lokal prioritering och korta beslutsvägar inom domänen | Dubblerade lösningar och svårigheter att kombinera information | Tydligt avgränsade domäner med egna resurser och begränsade tvärgående beroenden |
| Federerad | Lokal autonomi inom gemensamma ramar | Oklara mandat och kostsam samordning | Gemensam plattform, fungerande beslutsordning och finansierat lokalt ansvar |

Tabellen beskriver idealtyper. En praktisk arkitektur kan kombinera dem: central drift, federerat informationsansvar och decentraliserad utveckling av vissa analysprodukter. En federerad organisation behöver kunna fatta bindande gemensamma beslut; ett forum utan mandat att lösa konflikter räcker inte. Beslutsordningen bör ange vem som avgör tvister om gemensamma definitioner, hur undantag från standarder prövas och vem som finansierar åtgärder som berör flera domäner.

Centralisering kan fungera väl när samma specialistgrupp kan hantera behoven utan långa väntetider. Det är inte antalet team som avgör om modellen behöver förändras, utan var arbetet fastnar. Om flaskhalsen i själva verket är otydliga informationsdefinitioner hjälper det inte nödvändigtvis att fördela fler utvecklingsuppgifter till systemteamen.

## Fördela besluten efter deras räckvidd

En utgångspunkt är att beslut bör fattas så nära den berörda verksamheten som möjligt, men på en nivå som kan hantera konsekvenserna för andra. Det är särskilt viktigt att skilja den som definierar informationen från den som realiserar och driver leveransen.

| Beslut eller uppgift | Föreslagen huvudansvarig i en federerad modell |
|---|---|
| Betydelse och kvalitet hos källuppgifter | Verksamhetsdomän med stöd av systemteam |
| Teknisk publicering och förändring av källprodukt | System- eller dataproduktteam |
| Gemensamma identifierare och tvärgående definitioner | Utsedd beslutsfunktion efter beredning med berörda domäner |
| Härledda mått för ett specifikt analysbehov | Ansvarig analysprodukt eller verksamhetsfunktion |
| Myndighetsgemensamma rapporteringsmått | Utsedd ansvarig för rapporteringen, med mandat att samordna definitionerna |
| Tekniska standarder och återanvändbara tjänster | Gemensamt plattformsansvar inom beslutad arkitekturram |
| Tillåtna behandlingsmiljöer och säkerhetskrav | Behöriga beslutsfunktioner enligt myndighetens styrning |

Det behövs inte en gemensam informationsmodell för varje detalj i varje system. Däremot behöver gemensamma begrepp som ska jämföras eller kombineras ha överenskomna definitioner. Om två domäner räknar ett avslutat ärende på olika sätt kan båda definitionerna vara relevanta lokalt, medan myndighetens officiella statistik kräver ett särskilt fastställt mått. En gemensam teknisk databas löser inte denna skillnad.

Ett centralt analysteam kan förvalta en myndighetsgemensam modell utan att ta över källornas verksamhetsansvar. Det lokala ansvaret måste samtidigt innefatta skyldighet att utreda fel i källinformation som upptäcks av andra team. På så sätt hamnar rättelser där de kan få effekt för flera konsumenter.

## Kompetens och finansiering som arkitekturvillkor

Att delegera arbete utan att delegera kapacitet och mandat skapar ett nominellt ansvar. Om varje systemteam fortfarande behöver köa till samma ETL-specialist har organisationen ändrat ansvarsbeskrivningen men inte genomförandeförmågan. Om varje team i stället tvingas bygga egna överföringskomponenter har beroendet ersatts med duplicerat arbete.

En gemensam specialistfunktion kan ha två uppdrag: att utföra särskilt svåra uppgifter och att omsätta återkommande specialistkunskap i återanvändbara tjänster, mallar och kontroller. Den senare uppgiften minskar behovet av individuell handpåläggning. Team med små informationsvolymer eller sällsynta förändringar kan fortfarande använda ett gemensamt leveransteam; autonomi behöver inte betyda att alla utför alla uppgifter själva.

Finansieringen behöver följa ansvaret. En möjlig modell är att finansiera plattformens basförmågor gemensamt, låta domäner bära ordinarie produktförvaltning och använda gemensam portföljprioritering för större behov som korsar domängränser. Synliggör kostnaden för både producenten och konsumenten. Annars kan en besparing i ett team innebära att flera analysteam måste göra samma komplettering var för sig. FinOps Foundations vägledning för molnbaserade dataplattformar beskriver kostnadsfördelning per arbetslast [K036]. Även i lokal drift kan sådan uppföljning vara användbar, men kostnadsfördelning är inte i sig en modell för prioritering av myndighetsnytta.

## Erfarenheter från reglerade och stora organisationer

En fallstudie av Joshi, Pratik och Rao (2021) beskriver ett pilotarbete vid Saxo Bank där tekniska och kulturella förändringar kombinerades. Författarna lyfter katalog, kvalitet och ägande tillsammans med förändringsledning och incitament [K026]. Eftersom författarna var involverade i arbetet och det rör sig om en pilot är studien främst ett exempel på genomförandefrågor, inte ett oberoende mått på effekter.

Christensen och Ramstad (2023) undersökte Data Mesh-införanden hos Lego, Zalando och Saxo Bank i en masteruppsats. De identifierar bland annat utmaningar kring att lämna central kontroll, kompetensbrist och informationskvalitet [K027]. Resultaten ger kompletterande kvalitativa perspektiv men bör inte ges samma evidensvikt som bredare oberoende forskning. De överensstämmer i stora drag med de införanderisker som behandlades i kapitel 13 [K007].

Baselkommitténs uppföljning 2023 omfattade 31 globalt systemviktiga banker och visade varierande grad av anpassning till principerna för riskdataaggregering och rapportering [K024]. I ett nyhetsbrev den 6 januari 2026 sammanfattar Baselkommittén erfarenheter från dialog med tillsynsmyndigheter och branschaktörer, bland annat fragmenterat ansvar, otillräckligt ledningsengagemang och svårigheter med koncernövergripande aggregering. Nyhetsbrevet är inte en ny tillsynsvägledning eller en ny kvantitativ uppföljning av de 31 bankerna [K025]. Bankernas regelverk gäller inte automatiskt en myndighet. Den relevanta arkitekturlärdomen är att lokalt ansvar behöver förenas med en förmåga att på ledningsnivå säkerställa tillförlitlig tvärgående rapportering. Ingen av dessa källor fastställer att en viss organisatorisk modell generellt är bäst.

## Tillämpning i referensmyndigheten

Anta att den fiktiva referensmyndigheten vill lägga till en uppgift från ett operativt IT-stöd i en gemensam analys. I nuläget krävs en ändring i källsystemet, en specialistbeställning för överföringen och en ändring i det centrala Data Warehouse.

En centraliserad förbättring kan vara att standardisera överföringarna och ge den centrala gruppen ett tydligt leveransåtagande. En decentraliserad förbättring kan vara att låta systemteamet publicera uppgiften och analysteamet själv modellera den. Den federerade varianten kombinerar lokal publicering genom gemensamma plattformstjänster med ett utpekat ansvar för den gemensamma analysmodellen. Om uppgiften kräver en ny myndighetsgemensam definition behöver de berörda verksamhetsfunktionerna samordna den oavsett vilken modell som väljs.

Den federerade varianten är en rimlig hypotes när det finns många återkommande leveransbehov och en gemensam plattform kan undanröja rutinmässiga specialistberoenden. Den förutsätter dock finansierad kapacitet i systemteamen och en fungerande ordning för gemensamma definitioner. Om detta saknas kan en förbättrad central leveransfunktion vara ett bättre första steg.

## Bedöm resultatet före breddinförande

Utvärdera samma typ av förändring från behov till användbar information, inte endast tiden fram till publicering. Jämför med en dokumenterad utgångsnivå och välj förändringar med jämförbara krav på kvalitet, säkerhet och aktualitet. Följ upp väntetid respektive aktiv arbetstid, antal överlämningar, totala förvaltningstimmar, återanvändning och kvalitetsbrister. Kontrollera också att gemensamma rapporter kan återskapas och att beslut om åtkomst är spårbara. Om lokal utveckling blir snabbare men arbetet med att harmonisera data ökar i motsvarande grad har nyttan förskjutits snarare än realiserats.

Det är möjligt att börja med en begränsad förändring av ansvarsfördelningen utan att flytta lagringen. Bredda det lokala mandatet där det minskar den sammanlagda förändringskostnaden och där gemensamma kontrollkrav fortfarande uppfylls. Behåll centrala tjänster och modeller där skalfördelar, kompetenskoncentration eller gemensamma behov väger tyngre. Den organisatoriska arkitekturen bör utvecklas utifrån uppmätta hinder och resultat, inte utifrån ambitionen att maximera graden av decentralisering.
