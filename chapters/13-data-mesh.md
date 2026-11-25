# 13. Data Mesh

När varje ny informationsleverans behöver beställas från en central dataorganisation kan tillgången till specialistkompetens begränsa utvecklingstakten. Men att flytta uppgifterna till verksamhetsnära team utan att ge dem förutsättningar att utföra dem riskerar att skapa många mindre flaskhalsar. Data Mesh adresserar denna organisatoriska skalningsfråga snarare än enbart växande datavolymer.

## Fyra samverkande principer

Zhamak Dehghani formulerade 2020 fyra principer för Data Mesh [K080]. De beskriver tillsammans en socioteknisk arkitektur för analytisk information.

| Princip | Praktisk innebörd |
|---|---|
| Domänorienterat dataägande | Verksamhetsnära domäner ansvarar för sina analytiska informationsleveranser. |
| Data som produkt | Informationen erbjuds med definierad betydelse, kvalitet och livscykel. |
| Självbetjänad dataplattform | Domänerna får återanvändbara tekniska tjänster för att fullgöra ansvaret. |
| Federerad, automatiserbar datastyrning | Gemensamma spelregler beslutas samordnat och tillämpas där det är möjligt genom tekniska kontroller. |

Principerna förutsätter inte varsin teknikprodukt. Flera domäner kan använda samma Data Warehouse eller Lakehouse med logiskt separerade ansvarsområden. Omvänt innebär ett antal separata datalager inte att Data Mesh har etablerats. Det avgörande är hur ansvar, mandat och tekniskt stöd samverkar.

## Domänansvar är mer än systemansvar

En domän bör avgränsas utifrån en sammanhängande verksamhetsförmåga och dess informationsbegrepp, inte mekaniskt utifrån dagens systemkarta. Ett system kan stödja flera domäner och en domän kan behöva samordna information från flera system. Därför behöver domänens mandat över informationsdefinitioner och prioriteringar skiljas från systemteamets ansvar för den tekniska leveransen.

I den fiktiva referensmyndigheten kan exempelvis deklarationshantering och kontrollverksamhet utgöra olika domäner. Deklarationsdomänen ansvarar för hur deklarationsuppgifter ska förstås, medan kontrolldomänen ansvarar för information om genomförda kontroller. Ett tvärgående analysteam kan kombinera dessa uppgifter till underlag för resursplanering och ansvara för de härledda måtten. Det övertar inte därmed ansvaret för källuppgifternas betydelse.

Dataägande används här i organisatorisk mening: ett utpekat ansvar att förvalta information och fatta beslut inom delegerat mandat. Det innebär inte äganderätt till uppgifterna eller ett självständigt mandat att frångå myndighetens regler för behandling och utlämnande.

Domänansvaret förutsätter ett mandat att prioritera även leveranser vars nytta uppstår utanför domänen. Kapitel 15 analyserar hur mandat, kapacitet och finansiering kan fördelas.

## Federerad styrning utan fragmentering

Federerad styrning samordnar gemensamma regler med domänspecifika beslut. För Data Mesh är det särskilt viktigt att domänerna deltar i utformningen av regler som deras dataprodukter omfattas av. Kapitel 15 behandlar den mer generella fördelningen av beslutsmandat.

Automatiserbar styrning innebär exempelvis att publicering förutsätter en ansvarig, informationsklassning och godkända kontraktskontroller. Plattformen kan hindra tekniskt otillåtna publiceringar men inte själv avgöra om ett nytt användningsändamål är tillåtet. Vissa bedömningar behöver även fortsättningsvis göras av människor med rätt mandat. Målet är att återkommande, entydiga regler inte ska kräva en ny manuell prövning varje gång.

## Vad erfarenheterna visar

Goedegebuure med flera sammanställde i en systematisk översikt 114 industripublikationer om Data Mesh. Översikten beskriver principer, förmågor och organisatoriska roller, men dess underlag utgör inte en kontrollerad jämförelse av införandenas resultat [K006]. Det är viktigt att skilja mellan en utförlig beskrivning av en målmodell och empiriska belägg för dess nytta.

Bode med flera (2024) genomförde 15 semistrukturerade expertintervjuer mellan november 2022 och januari 2023. Studien belyser svårigheter med att förstå konceptet, flytta förvaltningsansvar och övergå till federerad styrning. Författarna föreslår bland annat samordning över domängränser, uppföljning av produktanvändning och tidiga avgränsade resultat [K007]. Underlaget är kvalitativt och ger vägledning om införanderisker snarare än ett mått på förväntade besparingar. Författarna uppmärksammar också risken att de intervjuade framställer sina egna införanden som mer framgångsrika än de faktiskt är.

Uber beskriver hur en gemensam tjänst för resurshantering etablerades inför migrering av batchdata till molnet. Tjänsten kopplar informationsresurser till organisationens ansvarshierarki och använder metadata för att automatisera tillämpningen av resurs- och livscykelregler. Förändrat ägande kan medföra att resurser behöver märkas om eller information flyttas [K011]. Exemplet visar hur vissa Mesh-principer kan understödjas tekniskt. Det är en självrapporterad erfarenhet från en specifik molnmigrering, inte en utvärdering av ett fullständigt organisatoriskt införande.

En lärdom för referensmyndigheten är att organisationsförändringar måste kunna hanteras utan att konsumenter behöver ändra sina anslutningar varje gång ett förvaltningsansvar flyttas. Uber beskriver också ett logiskt filsystem som döljer de fysiska lagringsvägarna [K011]. Stabila produktidentifierare och en uppdateringsbar koppling till ansvariga team är därför lämpligare än att exponera organisationsnamn och fysiska lagringsvägar som permanenta kontrakt.

## Organisatoriska förutsättningar

En särskild införanderisk är att domänernas nya ansvar inte motsvaras av kompetens, finansiering och användbara plattformstjänster. Om många domäner måste bygga samma leveransfunktion eller rekrytera samma specialistkompetens bör plattformens erbjudande och ansvarsfördelningen omprövas. De generella finansierings- och kompetensmodellerna behandlas i kapitel 15.

## Partiellt införande i en reglerad myndighet

Referensmyndigheten kan börja med att utveckla två befintliga systemspecifika mottagningszoner till förvaltade dataprodukter med verksamhetsnära ansvar, stabila gränssnitt och gemensamma publiceringskontroller. Det centrala Data Warehouse kan fortsätta att förvalta tvärgående rapporteringsmodeller. Plattformsteamet utvecklar de återkommande tekniska arbetsvägar som pilotdomänerna behöver, medan specialiststöd behålls för avvikande leveranser.

Vid uppföljningen är det särskilt viktigt att undersöka om producenternas ökade självständighet leder till faktisk återanvändning utan ökat tolkningsarbete hos konsumenterna. Kapitel 15 behandlar jämförelse av organisatoriska modeller och kapitel 21 verifiering före breddinförande.

En sådan tillämpning av utvalda principer är inte nödvändigtvis ett fullständigt Data Mesh enligt den ursprungliga målmodellen. Det är heller inte ett problem om syftet är att lösa konkreta hinder. Där informationsansvaret är svårt att avgränsa, kompetensen är mycket knapp eller samordningsbehovet dominerar kan en gemensam funktion vara mer ändamålsenlig. Utvidga domänansvaret där nyttan kan visas och där mandat, resurser och gemensamma kontroller fungerar tillsammans. Data Mesh är ett sätt att organisera informationsförsörjningen, inte ett krav på att byta lagringsarkitektur.
