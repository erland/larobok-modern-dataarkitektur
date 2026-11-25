# 19. Dataarkitektur för verksamhetsutveckling, analys och AI

En myndighet som vill använda AI i sin verksamhet behöver inte nödvändigtvis ersätta sin analytiska arkitektur. Informationen behöver däremot kunna användas på fler sätt än i återkommande rapporter. En handläggare kan behöva en aktuell sammanställning i sitt operativa IT-stöd, en analytiker ett historiskt träningsunderlag och en AI-assistent tillgång till gällande styrdokument. Dessa behov ställer olika krav på informationsförsörjningen.

## Från analysmiljö till verksamhetsnära konsumtion

Traditionell BI bygger ofta på gemensamma definitioner, kvalitetssäkrade historiska uppgifter och återkommande beräkningar. Ett centralt Data Warehouse kan vara fullt ändamålsenligt för detta. Verksamhetsnära analys innebär däremot att resultatet används där en verksamhetsuppgift utförs, exempelvis när en handläggare behöver bedöma ett ärende. Den analytiska beräkningen kan fortfarande ske separat från det operativa IT-stödet, men resultatet behöver tillhandahållas genom ett lämpligt gränssnitt och med tillräcklig aktualitet.

Det är användningsändamålet som avgör hur aktuella uppgifterna måste vara. En månatlig resursuppföljning, en sammanställning av dagens arbetskö och en kontroll av om en uppgift fortfarande gäller vid ett beslut behöver inte använda samma leveransmekanism. För den sista situationen kan ett direkt uppslag i en auktoritativ källa vara nödvändigt. En snabbare analytisk kopia eliminerar inte risken för att informationen har ändrats sedan kopian skapades.

## Maskininlärning som återkommande informationsprocess

Vid prediktiv analys tillkommer behov av att kunna skapa, utvärdera och återanvända träningsunderlag. Det räcker inte att veta vilken tabell som användes. Även urval, tidpunkter, rättelser, transformationer, modellvariabler och eventuella etiketter behöver dokumenteras. Tränings- och testdata ska utformas så att utvärderingen återspeglar den avsedda användningen och inte utnyttjar information som saknas vid en verklig modellkörning.

Vid användning av modellen behöver informationsförsörjningen upprätthålla de antaganden som gjordes under träningen. Ett ändrat registreringsförfarande kan exempelvis förändra innebörden av en modellvariabel utan att dess tekniska datatyp ändras. En modell som tidigare fungerat väl kan då ge sämre resultat. Sculley m.fl. beskriver databeroenden, återkopplingsslingor och förändringar i omvärlden som källor till teknisk skuld i maskininlärningssystem [K023].

Myndigheten bör därför följa både kvaliteten på indata och modellens faktiska resultat. Skilj mellan den tidpunkt då en händelse inträffade och den tidpunkt då uppgiften blev tillgänglig. Vid träning får en senare rättelse inte oavsiktligt ge modellen kunskap som saknades vid det historiska beslutstillfället. Ett gemensamt stöd för versionshantering av träningsunderlag och modellvariabler kan vara motiverat. En särskild Feature Store, beskriven i kapitel 7, är däremot inte en förutsättning för varje modell.

## Generativ AI och informationsåtervinning

En språkmodell kan kompletteras med information som hämtas vid användningstillfället. Retrieval-Augmented Generation (RAG) kombinerar informationsåtervinning med generering. Lewis m.fl. utvärderade 2020 en sådan modell med ett tätt vektorindex över Wikipedia på kunskapsintensiva språkbehandlingsuppgifter [K094]. Resultaten gäller de undersökta uppgifterna och innebär inte att en RAG-lösning alltid ger korrekta svar.

En myndighets RAG-lösning behöver en förvaltad kedja från källdokument till sökbart innehåll. Dokument kan delas upp i segment och förses med metadata om källa, giltighetstid, version och åtkomstvillkor. Sökningen kan kombinera fulltext, semantisk likhet och strukturerade filter. Vektorindex är ett möjligt hjälpmedel, inte ett obligatoriskt separat datalager.

Om ett styrdokument ersätts behöver förändringen nå även sökindex och eventuella cachar. Vid hämtning måste behörighet kontrolleras innan innehållet lämnas till modellen; en instruktion till modellen att inte avslöja viss information är inte en tillräcklig skyddsmekanism. Hämtat innehåll bör betraktas som data, inte som betrodda instruktioner. Även härledda segment, index, loggar och cachar behöver omfattas av informationsklassning och livscykelhantering enligt principerna i kapitel 17. För att underlätta granskning bör svaret kunna hänvisa till de dokumentversioner som faktiskt användes.

Utvärdering behöver skilja mellan återvinningens kvalitet och genereringens kvalitet. Ett felaktigt svar kan bero på att relevant information saknas, att sökningen väljer fel källa eller att modellen misstolkar ett korrekt underlag. Testfall bör därför omfatta gällande och upphävda dokument, motstridiga uppgifter, otillräckligt underlag och användare med olika behörighet.

## AI-assistenter, AI-agenter och specialiserade AI-tjänster

En AI-assistent som hjälper en handläggare att sammanfatta ett ärende kan använda både dokument och strukturerade uppgifter. En agent som dessutom får utföra åtgärder behöver tillgång till kontrollerade verksamhetsfunktioner, inte bara till ett analytiskt datalager. Läsning av information och ändring av verksamhetstillstånd bör vara separata befogenheter. Ändringar ska gå genom ansvariga operativa IT-stöds gränssnitt och deras valideringsregler. Mandat, godkännandepunkter och spårbarhet bör anpassas efter åtgärdens konsekvenser. Det operativa IT-stödet behöver själv kontrollera behörighet och aktuellt tillstånd vid varje åtgärd; en tidigare behörighetskontrollerad läsning är inte ett tillräckligt underlag för en senare ändring.

Specialiserade AI-tjänster, såsom transkribering, klassificering eller dokumenttolkning, behöver inte vara assistenter eller agenter. De kan anropas från befintliga IT-stöd som en avgränsad funktion. Resultatet behöver då kopplas till rätt informationsobjekt och vid behov till modellversion, källmaterial och granskningsstatus. AI-genererade uppgifter behöver kontrolleras innan de behandlas som verifierade sakuppgifter. Exempelvis kan ett automatiskt extraherat belopp behöva kontrolleras mot originalhandlingen innan det används i ett beslut.

## Informationsflöden i fyra verksamhetsnära tillämpningar

Anta att referensmyndigheten vill förbättra handläggningen av ett ärende. Samma operativa information kan behöva tillgängliggöras på olika sätt. Följande exempel beskriver möjliga ansvarsfördelningar, inte en obligatorisk teknisk struktur.

| Tillämpning | Informationsväg | Resultatets väg tillbaka |
|---|---|---|
| Analys av handläggningstider | Operativt IT-stöd → historisk dataprodukt → analysmodell | Rapport eller uppföljningsvy |
| AI-assistent | Förvaltade styrdokument → sökindex; aktuellt ärende → behörighetskontrollerat uppslag | Sammanställning med källhänvisningar till handläggaren |
| AI-agent | Dokument och aktuella ärendeuppgifter → agentens kontext; verksamhetsfunktioner via kontrollerade gränssnitt | Föreslagen eller godkänd åtgärd via operativt IT-stöd |
| AI-integrerat IT-stöd | Vald handling → dokumenttolkningstjänst | Strukturerat tolkningsresultat till ärendets granskningsflöde |

![Fyra exempel på informationsflöden till analys och AI. Historisk analys använder en historisk dataprodukt; assistenten kombinerar sökindex och behörighetskontrollerat aktuellt uppslag. Agenten skiljer läsning från åtgärder via operativt funktionsgränssnitt; de motriktade pilarna avser åtgärdsanrop och resultat/status. Vid osäkert utfall behövs statuskontroll och kontrollerad felhantering. Den specialiserade AI-tjänsten får avgränsad indata och lämnar resultat till IT-stödets granskningsflöde. Pilar visar logisk informationsriktning, inte fullständiga protokoll. Behörighetskontroller gäller även sökindexets innehåll före återvinning till modellen.](../assets/generated/IMG-19-01.svg)

I analysfallet är en historisk kopia värdefull eftersom den möjliggör jämförelser över tid. Assistenten behöver däremot kunna skilja mellan historisk information och uppgifter som gäller vid frågetillfället. Sökindexet kan försörjas asynkront, medan en aktuell ärendestatus vid behov hämtas direkt genom källsystemets gränssnitt. Om underlaget inte är tillgängligt eller har passerat sin giltighetstid bör assistenten kunna avstå från att ge ett bestämt svar.

Agenten använder motsvarande läsvägar men behöver dessutom en separat väg för åtgärder. Ett förslag att ändra en ärendestatus kan exempelvis först visas för en behörig handläggare. Efter godkännande prövar det operativa IT-stödet att statusen fortfarande är aktuell, att åtgärden är tillåten och att ett upprepat anrop inte orsakar en oavsiktlig dubbel ändring. Vid osäkert utfall behöver agenten kontrollera åtgärdens status innan ett nytt försök görs. Om utfallet inte kan fastställas bör åtgärden överlämnas till kontrollerad felhantering i stället för att upprepas blint. Den analytiska kopian är inte en skrivväg tillbaka till verksamheten.

Vid dokumenttolkning behöver AI-tjänsten bara det underlag som krävs för den avgränsade funktionen. IT-stödet ansvarar för att koppla svaret till rätt handling, hantera fel och avgöra när mänsklig kontroll behövs. Tjänsten behöver inte ges generell åtkomst till myndighetens dataplattform. Om verifierade tolkningsresultat senare behövs för analys kan de publiceras genom IT-stödets ordinarie informationsförsörjning.

Dataplattformens uppgift är i dessa exempel att erbjuda förvaltade informationsunderlag och lämpliga åtkomstvägar. AI-plattformen kan erbjuda inferens, informationsåtervinning och utvärdering, medan utvecklings- och integrationsplattformarna bidrar med gemensamma tekniska tjänster enligt kapitel 12. Informationsansvar, åtkomstbeslut och verksamhetsregler behöver bevaras oavsett var komponenterna körs. Det är därför inte nödvändigt att föra all information genom ett centralt analytiskt lager innan AI kan användas.

## Informationslämplighet och gemensamma förmågor

Sambasivan m.fl. undersökte genom intervjuer med 53 AI-praktiker hur problem i dataarbetet kan fortplanta sig i AI-system inom områden med stora konsekvenser [K022]. Den kvalitativa studien ger stöd för att uppmärksamma informationsarbetet tidigt, men fastställer varken problemens förekomst i svenska myndigheter eller vilken dataplattform en sådan myndighet bör välja.

Information som är tillräcklig för statistik är inte automatiskt lämplig för individnära prediktion eller automatiserade åtgärder. Representativitet, registreringspraxis, aktualitet, rättsligt tillåten användning och konsekvenser av fel behöver bedömas för varje användningsfall. Följande prioritering är ett arkitekturunderlag, inte en universell produktlista.

| Användningsfall | Kritiska informationsförmågor | Kompletterande förmågor vid behov |
|---|---|---|
| BI och rapportering | Gemensamma mått, historik, kvalitetssäkrade leveranser | Semantiskt lager för bred självbetjäning |
| Operativ analys | Aktualitet, definierad källa, tillgängligt gränssnitt | Strömmande bearbetning, särskild läsmodell |
| Maskininlärning | Tidskorrekta träningsdata, versioner, utvärdering och uppföljning | Feature Store, dedikerad träningsinfrastruktur |
| RAG | Förvaltade källor, behörighetskontrollerad återvinning, aktualitet och testdata | Vektorindex, avancerad rangordning |
| Agent med åtgärdsmandat | Kontrollerade funktionsgränssnitt, identitet, mandat och revisionsspår | Orkestrering för flerledade arbetsflöden |
| Specialiserad AI-tjänst | Definierade in- och utdata, resultatkontroll, koppling till källa | Gemensam modellserver och batchbearbetning |

För referensmyndigheten är ett rimligt första steg att återanvända befintliga kvalitetssäkrade dataprodukter för BI och prediktiv analys, samt etablera kontrollerad åtkomst till dokument och aktuella verksamhetsuppgifter för ett avgränsat assistentfall. Förmågor för modellträning och inferens kan etableras i anslutning till dataplattformen utan att nödvändigtvis ingå i samma tekniska produkt. Nya lagringsmotorer eller en separat AI-dataplattform bör motiveras av verifierade behov, inklusive driftkostnad och informationsskydd.

Uppföljningen bör utgå från verksamhetsresultat, exempelvis tidsåtgång, rättelsebehov och fel med betydelse för handläggningen, tillsammans med tekniska mått som informationsaktualitet, återvinningskvalitet och modellprestanda. Jämför med ett dokumenterat nuläge och kontrollera att förbättrad hastighet inte sker på bekostnad av tillförlitlighet. Kapitel 20 sammanför dessa behov med tidigare arkitekturval till kombinerbara referensarkitekturer.
