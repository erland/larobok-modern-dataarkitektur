# 16. Datastyrning, informationskvalitet och metadata

När en myndighet har gjort information tekniskt tillgänglig återstår en avgörande fråga: kan verksamheten lita på den? En rapport kan vara korrekt beräknad utifrån lagrade data men ändå ge en missvisande bild av verkligheten. Orsaken kan ligga i registreringen, urvalet, överföringen eller tolkningen av uppgifterna. Datastyrning behöver därför omfatta hela informationskedjan och inte enbart den miljö där analysen utförs.

Den brittiska revisionsmyndigheten National Audit Office har i sin granskning av offentlig sektors dataanvändning 2019 uppmärksammat problem med kvalitet, standarder och samordning [K014]. Dess vägledning till ledande befattningshavare tar även upp resurser, tillgång till rådata och informationsutbyte mellan offentliga organisationer [K015]. Erfarenheterna är relevanta som jämförelseunderlag, men säger inte hur en enskild svensk myndighet bör organisera sin verksamhet.

## Datastyrning som en del av utvecklingsarbetet

Datastyrning (data governance) handlar om att etablera beslutanderätt, ansvar, gemensamma regler och uppföljning för informationens användning och förvaltning. En policy behöver omsättas i kontroller som faktiskt fungerar när information skapas, förändras och konsumeras. Att endast kräva dokumentation vid ett projekts slut innebär att många kostsamma vägval redan har gjorts.

I en självbetjänad miljö kan gemensamma krav på ägarskap, metadata, kvalitetskontroller och godkända åtkomstvägar byggas in i publiceringsflödet. Rutinmässiga leveranser kan då genomföras utan separat manuell granskning, förutsatt att de håller sig inom beslutade mandat och uppfyller kontrollerna. Nya användningsändamål, informationsdefinitioner eller avvikelser som kräver en riskbedömning behöver däremot hanteras av behöriga funktioner.

En data steward är i detta sammanhang en funktion som arbetar praktiskt med definitioner, kvalitetsregler, avvikelser och samordning. Funktionen behöver inte vara en särskild befattning för varje dataset. Informationsansvarig behöver kunna prioritera åtgärder, medan tekniska team realiserar och övervakar kontroller. Plattformsteamet ansvarar för de gemensamma kontrollmekanismernas funktion, inte för att tolka verksamhetens uppgifter.

## Informationskvalitet är beroende av användningen

Den brittiska förvaltningens Government Data Quality Framework beskriver sex kvalitetsdimensioner med utgångspunkt i DAMA UK och betonar användningsändamålets betydelse [K083]. Tabellen omsätter dimensionerna i exempel från en myndighet. Målvärden behöver fastställas för respektive användning.

| Dimension | Exempel på kontroll |
|---|---|
| Fullständighet | Andel förväntade ärenden som levererats och andel obligatoriska uppgifter som är ifyllda |
| Unikhet | Antal otillåtna dubbletter av en ärendeidentifierare |
| Konsistens | Motstridiga statusuppgifter för samma ärende och tidpunkt |
| Aktualitet | Fördröjning från registrering till tillgänglig uppgift |
| Validitet | Uppgifter följer tillåtna kodvärden och format |
| Korrekthet | Uppgiftens överensstämmelse med verifierat underlag |

En validerad kod kan ändå avse fel händelse. Korrekthet kan därför kräva avstämning mot en tillförlitlig källa eller manuell verksamhetskontroll. En hög andel ifyllda fält är inte heller ett bevis på att uppgifterna är korrekta. För analys av exempelvis handläggningstider kan en mindre fördröjning vara acceptabel, medan en aktuell operativ riskbedömning kan kräva betydligt färskare information.

Kvalitetsmått bör alltid ha en definierad population, mätperiod och beräkningsregel. En kontroll av fullständighet som utesluter avvisade poster riskerar annars att visa ett förbättrat resultat när leveransen i själva verket försämras. Aktualitet och fullständighet kan också stå i konflikt: en preliminär leverans kan vara användbar innan alla uppgifter inkommit, om konsumenten får tydlig information om täckningen.

## Kontroller genom hela informationskedjan

Foidl m.fl. behandlar kvalitetsproblem, bakomliggande orsaker och problemområden i datapipelines [K004]. För en arkitekt innebär det att kvalitetsarbetet inte bör reduceras till kontroller av slutliga tabeller. En ändamålsenlig kontrollkedja kan se ut så här:

| Kontrollpunkt | Vad behöver upptäckas? |
|---|---|
| Registrering i källsystem | Ogiltiga värden och saknade uppgifter |
| Publicering | Avvikelse från kontrakt, uteblivna leveranser |
| Överföring | Förlorade eller dubblerade poster |
| Bearbetning | Felaktiga kopplingar, omvandlingar och urval |
| Konsumtion | Olämplig användning, felaktig tolkning eller inaktuell information |

Tekniska kontroller kan bland annat jämföra antal poster mellan källa och mottagare, upptäcka oväntade förändringar av värdefördelningar och kontrollera referensintegritet. En statistisk avvikelse är en signal att utreda, inte automatiskt ett fel. En förändring i verksamhetens ärendemängd kan vara helt korrekt.

Kontroller bör ha olika konsekvenser beroende på risken. Ett brott mot en kritisk kontraktsregel kan stoppa publiceringen, medan en mindre kvalitetsavvikelse kan medföra en varning. Vid stopp behöver konsumenterna få veta att leveransen uteblivit eller att föregående version fortfarande visas. Avvisade poster måste kunna utredas på ett kontrollerat sätt. Att tyst utesluta dem kan ge sken av en felfri leverans.

Rättelser bör göras där felet uppstår när detta är möjligt och tillåtet. Fel som introduceras i en analysmodell ska däremot rättas där. När en rättelse kräver ombearbetning behöver det framgå vilka härledda dataset och rapporter som påverkas. Ansvar för att initiera, genomföra och verifiera rättelsen bör vara tydligt.

## Informationskatalogen som gemensam ingång

En informationskatalog hjälper användare att hitta och bedöma tillgängliga informationsresurser. Den behöver kombinera verksamhetsmetadata, såsom begrepp, ändamål och ansvar, med tekniska metadata om schema, leveransgränssnitt och bearbetning samt operativa metadata om aktualitet, kvalitetsstatus och fel. Erfarenheterna från LinkedIns DataHub visar ett exempel på gemensam metadatahantering [K012]. En forskningsöversikt om metadata i Data Lake-miljöer behandlar också metadatahanteringens betydelse [K034].

För prioriterade dataprodukter bör katalogen åtminstone visa beskrivning, ansvarig funktion, informationsdefinitioner, åtkomstväg, gällande kontraktsversion, aktualitetsmål och kända begränsningar. Tekniska uppgifter bör hämtas automatiskt från de miljöer där de uppstår, medan verksamhetsdefinitioner behöver förvaltas av ansvariga funktioner. En katalog som enbart speglar databastabeller riskerar att bli en teknisk inventering snarare än ett stöd för informationsanvändning.

Katalogens synlighet behöver skiljas från åtkomst till själva informationen. Även metadata kan vara skyddsvärda, exempelvis beskrivningar av känsliga källor eller urval. En gemensam katalog förutsätter därför inte att alla kan se alla katalogposter.

## Data lineage och reproducerbarhet

Data lineage beskriver informationens ursprung och härledning. På datasetnivå kan den visa vilka leveranser och bearbetningar som ligger bakom en rapport. På fältnivå kan den visa vilka indatafält som används för att beräkna ett visst resultat. OpenLineage är ett exempel på en specifikation där dataset, bearbetningsjobb och enskilda körningar beskrivs och kan kopplas samman [K084].

Det finns en viktig skillnad mellan deklarerade beroenden och observerade körningar. En modell kan ange att en rapport använder två tabeller, medan körningsmetadata kan visa vilka bearbetningar som faktiskt genomfördes. OpenLineage skiljer exempelvis mellan JobEvent för metadata om ett jobb och RunEvent för observationer av en körning. Vilka uppgifter som faktiskt samlas in beror på integrationernas täckning [K084]. Båda perspektiven behövs för olika ändamål. Deklarerade beroenden hjälper vid planerade förändringar; körningsinformation kan underlätta felsökning och utredning av inträffade fel.

Lineage är inte i sig ett bevis för att ett resultat kan återskapas. För det krävs även tillgång till relevanta dataversioner, beräkningsregler, kod, konfiguration och eventuella externa referensuppgifter, i den utsträckning informationen får bevaras. Täckningen behöver också vara känd: manuella uttag och bearbetningar utanför instrumenterade miljöer kan skapa luckor i spårbarheten.

## Prioritering och uppföljning

För en fiktiv referensmyndighet med ett centralt Data Warehouse och systemspecifika mottagningszoner är ett lämpligt första steg att välja ett fåtal informationsleveranser som används för viktiga gemensamma rapporter. Utse ansvarig för respektive leverans, dokumentera dess betydelse och kvalitetsmål, etablera kontroller av överföring och bearbetning samt registrera de viktigaste beroendena till rapporterna. Detta kan genomföras utan att ersätta det befintliga datalagret.

Kritiska förmågor är tydligt ansvar, åtkomliga och förvaltade metadata, riskanpassade kvalitetskontroller, avvikelsehantering och spårbarhet för viktiga resultat. Avancerad automatisk fältlineage, kunskapsgrafer och statistisk anomalidetektion kan tillföras när enklare kontroller inte räcker. För ett särskilt kritiskt användningsfall kan någon av dessa kompletterande förmågor behöva betraktas som nödvändig.

Följ upp andelen prioriterade leveranser med definierade kvalitetsmål, andelen uppfyllda mål (redovisa uteblivna mätningar separat), tid till upptäckt och rättelse av kvalitetsbrister samt täckningen av kritiska informationsberoenden. Mät också hur lång tid det tar för ett team att publicera en ändring som uppfyller styrningskraven. Antalet katalogposter eller automatiska kontroller är inte ensamt ett mått på datastyrningens nytta.

Målet är att göra tillförlitlig information enklare att använda och fel enklare att upptäcka och åtgärda. Gemensamma kontrollmekanismer ska göra det lättare att agera inom beslutade ramar, inte ersätta verksamhetens ansvar för informationens betydelse och kvalitet. Nästa kapitel fördjupar hur rättsliga krav, informationsskydd och livscykelvillkor måste upprätthållas i arkitekturen.
