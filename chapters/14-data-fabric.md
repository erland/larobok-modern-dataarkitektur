# 14. Data Fabric

En organisation kan ha väl förvaltade datalager och ändå ha svårt att förstå hur informationen hänger samman. En förändring i ett operativt IT-stöd påverkar kanske flera analysflöden, rapporter och AI-tillämpningar utan att beroendena är synliga för systemteamet. Data Fabric adresserar denna typ av problem genom att knyta samman information, metadata och automatisering över tekniska och organisatoriska gränser.

## Ett metadataorienterat arkitekturmönster

Data Fabric är inte ett särskilt lagringsformat eller en entydigt avgränsad produktkategori. Gartner beskriver en arkitekturinriktning där metadata används aktivt för att stödja automatisering av informationsintegration [K081]. En forskningsöversikt av Gieß och Hutterer behandlar Data Fabric som ett av flera moderna datahanteringsparadigm, med betoning på integrerad åtkomst och automatisering [K008].

En praktisk tolkning är att etablera ett sammanhängande styr- och kunskapsskikt över befintliga datatjänster. Skiktet behöver kunna samverka med de tekniska miljöer där information faktiskt lagras, bearbetas och konsumeras. Det behöver däremot inte själv utföra all bearbetning.

| Förmåga | Konkret användning |
|---|---|
| Insamling av metadata | Hämta scheman, beroenden, ägare och körningsresultat från anslutna tjänster. |
| Sammanhängande metadata | Koppla informationsobjekt till leveranser, transformationer, begrepp och konsumenter. |
| Aktiv metadata | Använda förändringar och observationer som underlag för kontroller och åtgärder. |
| Automatiserad integration | Föreslå mappningar eller generera delar av informationsflöden. |
| Tvärgående styrning | Omsätta gemensamma regler i kontroller hos berörda tekniska tjänster. |

Indelningen beskriver en möjlig arkitektursyntes, inte en obligatorisk uppsättning komponenter.

## Från passiv till aktiv metadata

En katalog som visar dataset och deras beskrivningar har ett självständigt värde. Men om katalogens innehåll inte följer förändringarna i den tekniska miljön kan den successivt förlora sin tillförlitlighet. Aktiv metadata innebär här att observationer används som indata till processer och beslut, inte bara presenteras för läsning.

Anta att en producent förbereder en schemaändring i en dataprodukt. En ansluten tjänst registrerar den föreslagna ändringen före publicering. Genom kända beroenden kan plattformen identifiera berörda konsumenter, kontrollera ändringen mot datakontraktet och underrätta ansvariga team. Vid en otillåten förändring kan en publiceringsprocess stoppas innan nya data görs tillgängliga. Detta är ett möjligt arbetsflöde, inte en garanti som följer av att en metadatakatalog installerats.

Automatiseringen kräver att metadata är aktuella, att identifierare är stabila och att de tekniska kontrollpunkterna faktiskt kan påverka publiceringen. Om ett flöde saknar registrerade beroenden kan en konsekvensanalys ge falsk trygghet. Täckningsgrad och aktualitet är därför viktiga kvalitetsmått för metadata i sig.

## Kunskapsgrafer och semantiska samband

En metadatagraf kan representera exempelvis relationer mellan en tabell, ett bearbetningsjobb, ett verksamhetsbegrepp och en rapport. En kunskapsgraf kan dessutom uttrycka formaliserade betydelser och samband som stödjer mer avancerade frågor. Gränsen mellan dessa representationer är inte alltid skarp. Det avgörande är vilken semantik som uttrycks och hur den underhålls, inte att informationen lagras i en grafdatabas.

LinkedIn beskriver DataHub som en gemensam miljö för att hitta och förstå metadata från flera olika tekniska system [K012]. DataHubs arkitekturdokumentation beskriver även hur federerade metadatatjänster förmedlar metadataändringar via Kafka till gemensamma sök- och graffunktioner [K082]. Detta illustrerar hur gemensam överblick kan kombineras med distribuerat ansvar, utan att all verksamhetsinformation behöver flyttas till samma lagringsmiljö.

Flores m.fl. (2024) presenterar en semiautomatisk metod för inkrementell schemaintegration med kunskapsgrafer, realiserad i forskningsverktyget NextiaDI. Metoden utvärderades genom en användarstudie och skalbarhetsexperiment [K005]. En sådan metod kan underlätta delar av integrationsarbetet, men den löser inte automatiskt frågor om verksamhetsbetydelse. Två fält med namnet status kan avse helt olika tillstånd, och två olika koder kan representera samma verksamhetsbegrepp endast under vissa villkor.

## Automatisering med kontrollerat mandat

Data Fabric förknippas ofta med ambitionen att använda maskininlärning och AI för att identifiera samband, föreslå transformationer och underlätta styrning. Det är viktigt att skilja mellan att upptäcka en möjlig relation och att fastställa att relationen är korrekt.

En rimlig progression är att börja med automatiserad insamling och validering, fortsätta med rekommendationer och därefter tillåta automatiska åtgärder när reglerna är tillräckligt entydiga. Ett förslag till semantisk mappning kan granskas av informationsansvarig, medan en deterministisk kontroll av ett obligatoriskt fält kan köras utan manuell handläggning. Beslut om behörighet behöver däremot bygga på uttryckligt fastställda regler och mandat. Ett AI-genererat förslag är inte ett åtkomstbeslut. Automatiska åtgärder bör vara spårbara, ha avgränsade behörigheter och kunna stoppas eller återställas när det är möjligt.

Metadata kan själva innehålla skyddsvärda uppgifter, exempelvis namn på känsliga dataset, beroenden mellan system eller uppgifter om användare. En gemensam katalog måste därför ha en egen säkerhetsmodell. Det räcker inte att skydda de underliggande datalagren.

## Förhållandet till Data Mesh och dataplattformar

Data Mesh behandlar främst hur ansvar, mandat och informationsprodukter organiseras. Data Fabric betonar hur metadata, integration och styrning kan samverka tekniskt. De kan därför kombineras: ett domänteam kan ansvara för en dataprodukt medan gemensamma metadatatjänster möjliggör tvärgående sökning och konsekvensanalys.

En befintlig dataplattform kan redan ha flera av de förmågor som förknippas med Data Fabric. Det är inte nödvändigt att skapa ett nytt parallellt plattformslager. Däremot kan en sammanhållen modell för identifierare, händelser och metadata behövas för att tjänsterna ska kunna samverka. Integrationskostnaden och beroendet till anslutningar måste vägas mot den nytta som uppstår.

## Forskningsläge och införande

Gieß och Hutterer analyserade 189 artiklar om dataplattformar, Data Spaces, Data Mesh och Data Fabric. Översikten skiljer bland annat mellan former för styrning och mellan intern och organisationsöverskridande datadelning. Den beskriver även kombinationer av Data Fabric och Data Mesh [K008]. Den är inte ett jämförande test av totalkostnad eller verksamhetsnytta vid fullskaliga Data Fabric-införanden. LinkedIns erfarenheter och forskningen om schemaintegration stödjer mer avgränsade tekniska förmågor; de ska inte tolkas som belägg för att hela arkitekturvisionen kan automatiseras.

För den fiktiva referensmyndigheten kan en lämplig första tillämpning vara att synliggöra beroenden mellan systemspecifika mottagningszoner, efterföljande transformationer och prioriterade rapporter. Nästa steg kan vara automatiserade kontraktskontroller vid publicering och förslag till berörda konsumenter vid schemaförändringar. Först när metadata och ansvar är tillräckligt tillförlitliga är det motiverat att utöka automatiseringen till mer komplexa semantiska samband.

Följ upp andelen prioriterade leveranser med aktuell metadata, hur stor andel av kända verkliga beroenden som konsekvensanalysen hittar, hur ofta den ger felaktiga träffar, tiden för att utreda förändringar och hur ofta automatiska kontroller behöver korrigeras. Om metadatainsamlingen kräver omfattande manuell specialisthantering eller om rekommendationerna ofta är felaktiga behöver grundförmågan förbättras innan fler funktioner införs.

Data Fabrics värde ligger därmed inte i att etablera en ny teknisk etikett, utan i att göra distribuerad information begriplig och styrbar med mindre manuellt samordningsarbete. Hur ansvaret bör fördelas för att uppnå detta behandlas i nästa kapitel.
