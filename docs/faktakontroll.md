# Faktakontroll

Aktuell sammanställning: 86 publicerade källposter av 94 inventerade kandidater. Historiska antal i kapitlens arbetsnoteringar avser respektive produktionstillfälle. Kontrollerna gäller avgränsade påståenden och innebär inte att alla originalpublikationer har fulltextgranskats eller att resultat har replikerats. Se slutkontrollen i steg 7.3a.

| ID | Kapitel | Påstående | Status | Källa och avsnitt | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F001 | 1 | Lakehouse föreslås för att förena analytiska arbetslaster | Verifierad för påståendet | K001, abstract och introduktion, figur 1 | 2026-11-25 | Författarnas argument och prognos, inte bevis för generell överlägsenhet |
| F002 | 1 | Moderna koncept skiljer sig i ansvar och styrning | Verifierad för påståendet | K008, avsnitt 4–5 | 2026-11-25 | Litteraturöversikt, inte kausal effektstudie |
| F003 | 1 | NAO uppmärksammade ledarskap, kvalitetsinvesteringar och hantering av brister | Verifierad för påståendet | K014, förord och sammanfattning, särskilt tryckt s. 5–6 | 2026-11-25 | Brittisk förvaltning 2019; inte svensk nulägesbedömning |
| F004 | 1 | Data Lake-arkitekturer har utvecklats över tid | Verifierad för påståendet | K033, abstract, avsnitt 2–3 | 2026-11-25 | Litteraturöversikt, inte jämförande kostnadsbevis |

Övriga resonemang i kapitel 1 är analytiska bedömningar och uttryckligen hypotetiska exempel. Källkontrollen avser relevanta avsnitt i originalpublikationerna, inte en fullständig systematisk granskning av alla deras referenser. Kapitel 1 omgranskat 2026-11-25 mot de fyra originalpublikationernas tillgängliga abstracts, förlagstext och NAO:s officiella rapportsammanfattning. NAO-formuleringen avgränsades till sammanfattningens belagda slutsatser; K008 preciserades till jämförelse av styrning och decentralisering. Historisk DWH-beskrivning hänvisar nu till K033. Ingen ny fulltextgranskning av PDF genomfördes.

## Kapitel 2

| ID | Kapitel | Påstående | Status | Källa och avsnitt | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F005 | 2 | C-Store utformades för läsintensiva arbetslaster med kolumnlagring och komprimering | Verifierad för påståendet | K031, abstract och introduktion, s. 553–554 | 2026-11-25 | Historisk forskningsprototyp; inga generella prestandasiffror används |
| F006 | 2 | CERN kompletterade Oracle med läsreplik och Hadoop/Parquet/Spark för analys | Verifierad för påståendet | K029, Data Storage in Oracle Databases och Leveraging CERN’s Hadoop Service | 2026-11-25 | Organisationens egen tekniska redogörelse, ingen oberoende effektutvärdering |
| F007 | 2 | HyPer stödde samtidig OLTP och OLAP genom konsistenta ögonblicksbilder | Verifierad för påståendet | K040, författarnas abstract i TUM:s publikationsregister | 2026-11-25 | Endast abstract granskat; ingen generalisering av testresultat |

K009 identifierades men används inte i detta kapitel eftersom jämförelsen av analytiska lagringsarkitekturer hör hemma i kapitel 8. K040 tillagd som mer direkt relevant forskningskälla. Övriga exempel är fiktiva och rekommendationerna är arkitekturanalys. Totalt sju källposter har använts; 33 av de nu 40 kandidaterna återstår att verifiera.

Omgranskning kapitel 2: CERN:s originalblogg bekräftar läsreplik, dagliga uppdateringar och Spark/Parquet/Hadoop/SWAN; C-Store originalartikel s. 553 (text och sidbild) bekräftar läsoptimering och preliminära resultat; HyPer kontrollerad mot författarnas abstract i TUM:s publikationsregister. Ingen ny fulltextgranskning av HyPer. Förtydligat replikfördröjning och att snapshot-konsistens inte garanterar svarstid.

## Kapitel 3

| ID | Kapitel | Påstående | Status | Källa och avsnitt | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F008 | 3 | Jämförelse av koncept utifrån styrning och tillämpningsområde, kombinationer möjliga, brist på empiriska jämförelser | Verifierad för påståendet | K008, avsnitt 5–6, https://link.springer.com/article/10.1007/s10257-025-00707-4 | 2026-11-25 | Begreppslig litteraturöversikt |
| F009 | 3 | Genomgång av 114 branschpublikationer, fyra Mesh-principer | Verifierad för påståendet | K006, författarnas abstract i TU Eindhoven forskningsportal, https://research.tue.nl/en/publications/data-mesh-a-systematic-gray-literature-review/ | 2026-11-25 | Abstract, inte fulltext; grå litteratur |
| F010 | 3 | Uppföljning av 31 systemviktiga banker, betydande arbete återstår hos flertalet | Verifierad för påståendet | K024, BIS officiella rapportsammanfattning, https://www.bis.org/publications/202311-implementation-reports-progress-adopting-principles-effective-risk-data-aggregation-and-risk-reporting | 2026-11-25 | Historisk tillsynsuppföljning, inte svensk myndighetsreglering; rapportens PDF ej granskad |

Fem arkitekturdimensioner och sex bedömningsdimensioner är bokens egen syntes. Exempel är fiktiva. Nio av 40 källkandidater har nu använts; 31 återstår att verifiera.

Omgranskning kapitel 3 (2026-11-25): K008 kontrollerad mot originalartikelns abstract, introduktion och avsnitt 5–6 (kombinationer och begränsad empirisk evidens); K006 mot författarnas abstract i TU/e:s forskningsportal (114 artiklar och fyra principer); K024 mot BIS officiella rapportsammanfattning (31 banker klassade som globalt systemviktiga 2011–2021; betydande arbete återstod hos flertalet). Fulltext av K006 och rapport-PDF för K024 har inte granskats. Inga nya externa sakpåståenden. Bokens egna exempel och beslutsramverk hålls åtskilda från forskningsresultat. Del I har jämförts med inledningen och kapitelplanen: kapitel 1 beskriver drivkrafter, kapitel 2 arbetslaster och kapitel 3 beslutsramverket. Återkommande myndighetsexempel har olika funktioner; inga tidigare kapitel behöver ändras.


## Kapitel 4

| ID | Kapitel | Påstående | Status | Källa | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F011 | 4 | Stage, marts, normalisering | Verifierad för påståendet | K041, Data Warehouse Architectures; K043, Modeling Approaches | 2026-11-25 | Metod- och produktdokumentation |
| F012 | 4 | Dimensionsmodellering och SCD | Verifierad för påståendet | K042, Grain, Conformed Dimensions, Type 1 och Type 2 | 2026-11-25 | Metodbeskrivning |
| F013 | 4 | Data Vault, hubbar, länkar, satelliter | Verifierad för påståendet | K043, Components of the Data; K045, Raw Vault och Business Vault | 2026-11-25 | Metod- och produktdokumentation |
| F014 | 4 | Separat beräkning, gemensam lagring, JSON | Verifierad för påståendet | K044, Data platform as a self-managed service, Database storage, Compute | 2026-11-25 | Produktdokumentation, ingen oberoende effektstudie |

K032 och K009 sparas till jämförelse i kapitel 8. K031 behandlas i kapitel 2. K041–K044 är nya källor för kapitel 4; relevanta avsnitt kontrollerade vid omgranskningen. Tabeller och myndighetsexempel är egen arkitekturanalys respektive fiktiva exempel.

Omgranskning kapitel 4 (2026-11-25): samtliga fyra ursprungliga webbkällors relevanta avsnitt öppnade och jämförda med texten. K045 tillagd för Raw/Business Vault. Snowflakes molnbegränsning uttryckligen angiven. Ingen oberoende prestanda- eller kostnadsjämförelse görs; sådana jämförelser hör till kapitel 8. Förtydligat reproducerbarhet och villkor för fortsatt förvaltning. 14 av 45 källkandidater har använts; 31 återstår.

## Kapitel 5

| ID | Kapitel | Påstående | Status | Källa | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F015 | 5 | Flexibla format, schematolkning och zonbaserade arkitekturer | Verifierad för påståendet | K033, avsnitt 3, 5.2, 6 | 2026-11-25 | Forskningsöversikt, inga generella kostnads- eller prestandapåståenden; tabell 1 har omkastade schemaetiketter jämfört med löptexten och används inte |
| F016 | 5 | Metadatahantering och Data Swamp | Verifierad mot abstract | K034, https://cris.unibo.it/handle/11585/997624 | 2026-11-25 | Förlagets fulltext gav 403; bibliografi och abstract tillgängliga i universitetets register |
| F017 | 5 | Tidig och senare bearbetning under datalivscykeln | Ej relevant efter korrigering | K035 | 2026-11-25 | Fulltext ej tillgänglig; specifik attribution borttagen, rekommendationen är egen arkitekturbedömning |
| F018 | 5 | HDFS och skillnader mot objektlagring | Verifierad för påståendet | K046, Data Replication och Persistence of File System Metadata; K047, avsnitt om objektlagring och rename | 2026-11-25 | Versionsbunden dokumentation; inga universella garantier |

Zonindelningen, beslutskriterierna och myndighetsexemplen är bokens egen syntes. Källregistret omfattar 17 poster av 47 kandidater.

Omgranskning kapitel 5: K033 kontrollerad mot löptext om schema och zoner; tabellens omkastade schemaetiketter används inte. K034 kontrollerad mot universitetets abstract, tillräckligt för det avgränsade påståendet om metadata och Data Swamp. K046 och K047 öppnade och kontrollerade mot relevanta dokumentationsavsnitt. K035 kunde inte fulltextkontrolleras; hänvisning och publicerad källpost borttagna, kandidaten kvar i arbetsinventeringen. Förtydligat objektlagringens varierande garantier, små objekt och reproducerbarhet.

## Kapitel 6

| ID | Kapitel | Påstående | Status | Källa och avsnitt | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F019 | 6 | Lakehouse som förenande arkitekturförslag | Verifierad mot abstract | K001, CIDR proceedings | 2026-11-25 | Författarnas tes, ej utfallsbevis |
| F020 | 6 | Parquet är kolumnorienterat filformat | Verifierad för påståendet | K048, Overview | 2026-11-25 | Teknisk dokumentation |
| F021 | 6 | Iceberg snapshots, manifest och schema/partitionering | Verifierad för påståendet | K049, Overview, Schema Evolution, Partition Evolution och Table Metadata | 2026-11-25 | Formatversioner och motorstöd varierar |
| F022 | 6 | Delta logg och optimistisk samtidighetskontroll | Verifierad för påståendet | K050, Overview och Optimistic concurrency control; K053, Transaction Log Protocol | 2026-11-25 | Lagringsberoende garantier |
| F023 | 6 | Hudi CoW och MoR samt inkrementella frågor | Verifierad för påståendet | K051, Table & Query Types | 2026-11-25 | Dokumenterade mekanismer, inte jämförande prestandabevis |
| F024 | 6 | LHBench arbetslaster och testmiljö | Verifierad för påståendet | K002, Workload och Results December 2022 | 2026-11-25 | Historiska versioner, ej generell rangordning; full artikel ej granskad |
| F025 | 6 | Bronze, Silver, Gold | Verifierad för påståendet | K052, beskrivningar av respektive lager | 2026-11-25 | Leverantörens arkitekturmönster |

Minimiförmågor, myndighetsscenario och beslutskriterier är bokens egen arkitektursyntes. Omgranskning: transaktionsomfattning, motorroller, Icebergs schema- och partitionsutveckling samt Delta-protokollet kontrollerade. K054 och K055 styrker motorroller; K056 styrker underhållsexemplen. Hudi-dokumentationen skiljer snapshot från läsoptimerad fråga. LHBench-resultatsidan verifierar Spark, EMR, S3 och versioner från 2022. K001 kontrollerad mot CIDR:s bibliografiska post och tillgänglig sammanfattning; ingen ny fulltextgranskning av artikeln. Inga generella prestandavinster hävdas. K009 sparas till kapitel 8. Ingen fullständig granskning av LHBench-artikeln gjordes.

## Kapitel 7

| ID | Kapitel | Påstående | Status | Källa | Kontrollerad | Begränsning |
|---|---|---|---|---|---|---|
| F026 | 7 | CERN:s befintliga tekniker och ClickHouse-utvärdering | Verifierad för påståendet | K030 | 2026-11-25 | Officiellt konferensabstract via workshopens tidtabell; direktlänk 403; ej presentationsmaterial eller utfall |
| F027 | 7 | Kolumnorienterad analysmotor | Verifierad för påståendet | K057 | 2026-11-25 | Leverantörens beskrivning |
| F028 | 7 | Inbäddade dokument och inverterat index | Verifierad för påståendet | K058, K059 | 2026-11-25 | Relevanta originalavsnitt |
| F029 | 7 | Egenskapsgraf, vektorsökning och feature store | Verifierad för påståendet | K060–K062 | 2026-11-25 | Relevanta originalavsnitt |
| F030 | 7 | Masterdata och referensdata | Verifierad för påståendet | K063 | 2026-11-25 | Leverantörens begreppsbeskrivning |

K064: författarnas abstract via ResearchGate, historisk tes om specialisering, ej fulltext. K065: Oracle 21, ODS-begreppet verifierat. K066: Feast v0.43, tidskorrekta kopplingar verifierade; tillgänglighetstid är egen arkitekturrekommendation. K061: recall mot exakt sökning verifierat. K029 och K040 behandlas redan i kapitel 2. Myndighetsexempel och beslutskriterier är egen arkitektursyntes. Inga generella prestandavinster hävdas.


## Kapitel 8

K009: bibliografiska data verifierade via DBLP och förlagets indexerade abstract; originalsidans direktåtkomst gav 403. Tillgängliga avsnitt av artikeln via ResearchGate stödjer experimentets avgränsning. K032: förlagets indexerade abstract och bibliografiska data verifierade; direktåtkomst gav 403. Exakt produktlista borttagen då den inte kunde verifieras i tillgängligt abstract. Inga påståenden om relativa prestanda eller kostnader från K009/K032. K002: originalets testbeskrivning och resultat verifierade (Spark på AWS EMR 6.9.0, S3, Hudi 0.12.0); avvägningen mellan uppdatering och efterföljande frågor avser TPC-DS Refresh. K036: originalavsnitt om kostnadsfördelning, samarbete och prognoser verifierade; anpassningen till lokal drift är egen syntes. Jämförelsetabeller, scenarier och kriterier är egen arkitektursyntes. Ingen fullständig granskning av K009 eller K032. Kontrollerat 2026-11-25.

## Kapitel 9

Kontrollerat 2026-11-25. K004: DLR:s publikationsregister och abstract verifierar bibliografi, litteraturöversikt, åtta intervjuer samt analys av GitHub och Stack Overflow; förlagets DOI-länk gav 403. Ingen fulltextgranskning; påståendet begränsat till metoden, slutsatsen markerad som arkitektursyntes. K010: originalartikel 31 januari 2026, avsnitten Background, Overview och Implementation, verifierar styrskikt och konfigurationsbaserad abstraktion; stöd för batch och streaming anges som designkrav, inte bevis på fullständig realisering. K067: originalavsnitt om inkrementella snapshots och samtidig loggläsning verifierat. K068: originalvägledning om öppna och delade data samt specifikationer verifierad; ingen rättslig slutsats. K069: IBM:s ETL/ELT-definitioner verifierade. K070: AWS:s outbox-mönster, lokal transaktion och dubbelleveranser verifierade; ej produktrekommendation. K071: Kafka 2.2, Message Delivery Semantics, verifierar skillnaden mellan transaktioner inom Kafka och externa mål; används för principen, inte aktuell versionsjämförelse. Tabeller, fiktivt myndighetsexempel, mätetal och rekommendationer är egen arkitektursyntes. K018 och K019 sparas till senare kapitel.

## Kapitel 10

Kontrollerat 2026-11-25. K006: universitetets publikationsregister och abstract (https://research.tue.nl/en/publications/data-mesh-a-systematic-gray-literature-review/) verifierar 114 industripublikationer, de fyra principerna, DOI och publicering januari 2025 (online oktober 2024). Ingen fulltextgranskning; slutsatsen avser praktikernas perspektiv, inte kausala effekter. K038: originaldokumentationens Schema evolution, Compatibility types och Transitive property verifierar riktning, omfattning och formatberoende. K072: originalspecifikationen version 3.0.0, Executive Summary, Fundamentals och Schema verifierar kontraktets maskinläsbara representation samt avsnitt för kvalitet, team och servicenivå. Versionen används som exempel, inte senaste version. Illustrativt servicenivåmål, ansvarsfördelning, semantisk kompatibilitet, produktgränser och beslutskriterier är egen arkitektursyntes. Ingen rättslig slutsats eller effektivitetsgaranti hävdas. K007, K018 och K019 kvarstår för senare kapitel.

## Kapitel 11

Kontrollerat 2026-11-25. K073: förlagets HTML-original (https://journals.sagepub.com/doi/full/10.3233/SW-223201), inledning, ramverk och slutsats samt författarens bibliografiska sida verifierar 51 system (33 industriella, 18 akademiska), fyra dimensioner och avsaknad av effektivitetsmätning. DOI-omdirigering fungerade inte, men direktlänken till artikeln fungerade. Ingen fullständig genomgång av alla system i studien. K074: Trino Pushdown, verifierat anslutningsberoende och möjliga nätverksvinster. K075: Delta Sharing, Read Delta Sharing Tables, verifierat öppet protokoll och läsåtkomst. K076: dbt Semantic Layer, originaldokumentation om gemensamma mått och krav på plattformskonto verifierad. K077: EU-kommissionens Concept verifierar infrastrukturer och styrningsramverk; inga rättsliga slutsatser. Återkallelsetid, härledda resultat, historisk reproducerbarhet, fiktivt scenario och beslutskriterier är egen arkitektursyntes; inga produktspecifika garantier hävdas.

## Kapitel 12

Kontrollerat 2026-11-25. K003: officiell CIDR-post med abstract verifierar författare, fragmentering, återanvändning och gemensamma API:er; ingen fulltextgranskning eller oberoende effektmätning. K078: originalets What is a platform, Platform maturity och Attributes of platforms verifierar tjänstegränssnitt, dokumentation, självbetjäning och produktperspektiv; avser interna cloud-native-plattformar. K079: originalartikeln 1 februari 2024, avsnitten Contactless, Architecture och Chargeback verifierar felregler, insamling av metadata och kostnadsattribuering; självrapporterad erfarenhet. K036: originalets Summary och Allocation verifierar arbetslastbaserad kostnadsfördelning i molnmiljö; lokal tillämpning är egen syntes. Förmågeindelning, säkerhetskontroller, orkestrering, mätetal och myndighetsscenario är egna arkitekturrekommendationer. Inga kvantifierade effektivitetsvinster hävdas.

## Kapitel 13

Kontrollerat 2026-11-25. K080: originalartikelns fyra principer verifierade. K006: universitetsregistrets abstract verifierar 114 industripublikationer och översiktens syfte; ej fulltextgranskad. K007: publicerad IEEE Access-version 2024, tillgänglig som HTML-text via ResearchGate, abstract, metod, införandestrategier och begränsningar verifierade; bibliografi kontrollerad mot DBLP. 15 intervjuer november 2022–januari 2023, kvalitativ metod och urvalsbias. Referensen uppdaterad från arXiv till slutversion med fyra författare. K011: originalartikelns introduktion och Ownership changes samt logiskt filsystem verifierade; självrapporterad erfarenhet, inte oberoende effektmätning. Ansvarstabell, finansiering, mätetal och fiktivt myndighetsscenario är egen arkitektursyntes. K026 och K027 sparas till kapitel 15.

## Kapitel 14

Kontrollerat 2026-11-25. K005: publicerad HTML-artikel hos Sage (https://journals.sagepub.com/doi/full/10.3233/SW-233347), avsnitt 3 och 7, samt Aalborgs publikationsregister verifierar metod, NextiaDI, användarstudie, skalbarhetsexperiment och bibliografi. DOI-omdirigeringen gav timeout men direktlänken fungerade. Inga kvantitativa effektpåståenden. K008: originalets abstract, metod och jämförelse verifierar 189 bidrag, styrningsdimensioner och kombinationer; begreppslig analys, inte effektstudie. K012: LinkedIns originalartikel 14 augusti 2019 verifierar metadataöversikt och författare; självrapporterad erfarenhet. K081: Gartners publika original om aktiv metadata och integration verifierat, analytikerperspektiv. K082: originaldokumentationens Stream-based Real-time Metadata Management Platform och Federated Metadata Serving verifierar händelsebaserad metadata och gemensamt sökindex/graf. Kontrollflöden, mandat, säkerhetsåtgärder, mätetal och fiktivt scenario är egen arkitektursyntes. Ingen generell effektivitetsvinst eller fullständig automation hävdas. Ingen fullständig reproduktion av forskningsstudierna.

## Kapitel 15

Kontrollerat 2026-11-25. K024: BIS officiella sammanfattning verifierar datum, 31 G-SIB och varierande anpassning; full rapport ej granskad. K025: originalnyhetsbrev nr 36, 6 januari 2026, avsnitten Governance and data och Cross-border implementation verifierar fragmenterat ansvar, ledningsengagemang och aggregeringsproblem. Dokumentet sammanfattar dialoger och utgör inte ny tillsynsvägledning eller ny kvantitativ uppföljning. K026: konferensregistrets abstract och affilieringar verifierar pilot, medverkande författare och tekniska/kulturella insatser. K027: CBS originalregister och abstract verifierar författare, uppsatsnivå, tre organisationer och identifierade hinder. Ingen fulltextgranskning av K026/K027; påståenden avgränsade till abstract. K007: publiceringsregister verifierat, tidigare dokumenterad originalgranskning återanvänds. K036: originalvägledning om molnbaserade dataplattformar, lokal tillämpning egen syntes. Ansvarsmatris, finansieringsmodell, beslutsordning, jämförelsekriterier och fiktivt scenario är egen arkitektursyntes. Bankernas regelverk överförs inte till myndigheten. Inga generella effektivitetsvinster hävdas. Del IV helhetsgranskad.

## Kapitel 16

Kontrollerat 2026-11-25. K014: NAO:s officiella pressmeddelande och rapportsida stöder brister i kvalitet, standarder och samordning; ingen ny fulltextgranskning. K015: officiell vägledningssida och NAO:s ämnesregister verifierar omfattning och publiceringsdatum 21 juli 2022. K083: originalets avsnitt Data quality dimensions och User needs and trade-offs verifierar sex DAMA UK-dimensioner, ändamålsberoende och avvägningar. K084: originalets Object Model verifierar JobEvent, DatasetEvent och RunEvent samt deklarerade respektive observerade beroenden; täckning är integrationsberoende. K004, K012 och K034: tidigare dokumenterade kontroller återanvänds (K004 och K034 avgränsade till abstract). Kontrolltabeller, rollfördelning, rättelseprocess, mätetal och fiktivt scenario är egen arkitektursyntes. Brittisk vägledning är jämförelseunderlag, inte svenska rättsliga krav. Ingen oberoende effektmätning.


## Kapitel 17

Kontrollerat 2026-11-25. K020: EUR-Lex indexerade originalutdrag och IMY:s vägledning (https://www.imy.se/verksamhet/dataskydd/det-har-galler-enligt-gdpr/grundlaggande-principer/ och https://www.imy.se/verksamhet/dataskydd/det-har-galler-enligt-gdpr/konsekvensbedomning/nar-ska-en-konsekvensbedomning-genomforas/) kontrollerade; direktåtkomst till EUR-Lex blockerades. K085: 8 kap. 1–2 §§ i riksdagens lagtext. K086: arkivlagens 3–6 §§ och bevarandeprincip; 10 § avser gallring. K021/K087: Riksarkivets konsoliderade version genom 2024:3, https://riksarkivet.se/files/2024/09/rafs_konsoliderad-ra-fs-2009-1.pdf, relevanta avsnitt om tillämpning, bevarande, dokumentation och säkerhet granskade; grund- och ändringsförfattningarnas direktlänkar gav timeout, officiella sökutdrag och konsoliderad text användes. Tryckt författning är rättsligt avgörande. K088: riksdagens lagtext, 1 kap. 2 §, och IMY:s vägledning om brottsbekämpning. K089: riksdagens lagtextutdrag om rutinbetonade sammanställningar och säkerhetskopior. Tekniska åtgärder och mätetal är arkitektursyntes, inte uttömmande rättskrav. Ingen juridisk expertgranskning.

## Kapitel 18

Kontrollerat 2026-11-25. K037: indexerade originalutdrag från EUR-Lex, artiklarna 23, 25, 30 och 31 samt skäl 86; direktåtkomst till svensk HTML gav endast tre rader. EU-kommissionens Data Act explained (https://digital-strategy.ec.europa.eu/en/factpages/data-act-explained) kompletterar kontrollen. K090: IMY:s originalvägledning, inklusive de tre kriterierna för tredjelandsöverföring. K091: officiell rapportsammanfattning, 16 november 2022, sju svarande; ingen fulltextgranskning. K092: CNCF:s officiella definitionssida (https://www.cncf.io/about/who-we-are/) bekräftar privata, publika och hybrida miljöer, lösa kopplingar och automation. K049/K093: officiella tabell- och REST-katalogspecifikationer kontrollerade; inga kompatibilitetstester genomförda. K036: tidigare dokumenterad vägledning återanvänds. Flyttprov och prioriteringar är egen arkitektursyntes, inga faktiska migreringar genomförda. Ingen juridisk expertgranskning. Rättskällor bör kontrolleras inför publicering. Del V helhetsgranskad.

## Kapitel 19

Kontrollerat 2026-11-25. K022: Google Research och ACM:s publikationsregister bekräftar 53 intervjuer och kvalitativt fokus på dataarbete inom AI med stora konsekvenser. K023: NeurIPS 2015 originalabstract verifierar databeroenden, återkopplingsslingor och förändringar i omvärlden. K094: NeurIPS 2020 originalabstract verifierar kombinationen av parametriskt minne och externt vektorindex över Wikipedia samt utvärdering på kunskapsintensiva uppgifter. Sakpåståenden avgränsade till publikationsregister och abstract; ingen fulltextgranskning eller reproduktion av experiment. Tidskorrekta träningsdata, behörighetskontroller, livscykel, agentmandat, prioriteringar och mätetal är egen arkitektursyntes. Ingen generell effektivitetsvinst hävdas.

## Kapitel 20

Kontrollerat 2026-11-25. K002: originalets testbeskrivning och december 2022-resultat verifierade; resultaten gäller specifika versioner och AWS EMR/Spark/S3. K003: CIDR:s originalabstract verifierar Metas egen beskrivning av återanvändbara komponenter och gemensamma API:er, inte oberoende effektmätning. K009 och K032: förlagets indexerade abstract verifierar studiernas ämne och avgränsning; ingen ny fulltextgranskning. K036: originalets sammanfattning verifierar kostnadsfördelning per arbetslast och gemensamma resurser i molnmiljö; lokal tillämpning egen syntes. Fem referensarkitekturer, kombinationer, urvalskriterier, TCO-scenarier och verifieringsfall är egen arkitektursyntes. Inga faktiska plattformstester eller nya generella effektpåståenden. Kapiteltext korrigerad och återläst.

## Kapitel 21

Kontrollerat 2026-11-25. K007: KIT:s publikationsregister och indexerat originalabstract bekräftar tidiga avgränsade införanden och tvärgående samordning; ingen ny fulltextgranskning. K015: NAO:s officiella sammanfattning bekräftar målgruppen ledande befattningshavare och organisatoriska hinder, resursfrågor och datakvalitet. K036: FinOps Foundations originalvägledning avser molnbaserade dataplattformar; lokal tillämpning är en anpassning. Tidigare dokumenterad källkontroll återanvänds. Etapper, pilot, migrering, återgång, finansiering, indikatorer och stoppkriterier är egen arkitektursyntes, inte empiriskt verifierade resultat. Inga faktiska migreringar genomförda. Kapitel korrigerat och återläst. Del VI helhetsgranskad.

## Steg 7.1b

Kapitel 9 och 12: nya exempel och ansvarsmatriser är illustrativ arkitektursyntes, inte empiriska resultat. Tidigare källhänvisningar bevarade; ingen ny extern källkontroll. Förnyad redaktionell granskning återstår.

## Steg 7.1c

Kapitel 8, 19 och 20: hypotetiska kalkylantaganden och arkitekturexempel; inga nya externa faktapåståenden. Femårskalkylen och brytpunkten kontrollerade aritmetiskt. Tidigare källhänvisningar bevarade. Ingen ny extern källkontroll. Förnyad granskning återstår.

## Steg 7.3a – Samlad källregisterkontroll

2026-11-25. Samtliga 86 publicerade ID har jämförts med kapiteltext, inventering och respektive kapitels dokumenterade faktakontroll. Alla 86 har en unik HTTPS-adress med giltig URL-syntax; detta är inte en kontroll av svarskod eller tillgänglighet. K006:s tidskriftsvolym, nummer, artikelnummer och DOI har stickprovskontrollerats mot TU/e:s publikationsregister. K085:s sekretessgränser har stickprovskontrollerats mot riksdagens aktuella lagtext och K037:s funktionella likvärdighet mot indexerade originalutdrag från EUR-Lex. Tidigare begränsningar kvarstår, inklusive abstractkontroller, blockerad direktåtkomst, historiska produktversioner, självrapporterade erfarenheter och avsaknad av juridisk expertgranskning. Inga kapiteltexter eller kapitelgodkännanden ändras. Se docs/reviews/kallkontroll-7.3a.md för fullständig ID-matris och öppna kontroller.

## Förnyad granskning 7.3b – revision 51

Kapitel 1, 3, 4, 5, 8, 9 och 10 jämförda med tidigare godkänd revision 45 och lästa mot den dokumenterade faktakontrollen samt källmatrisen i 7.3a. Samtliga källhänvisningar och deras antal bevarade. Ingen ny extern källgranskning genomförd. Korrigeringarna i kapitel 1 och 9 preciserar fiktiva scenarier, inte externa sakpåståenden. Kapitel 8 kontrollberäknat med heltal i kronor: 41 respektive 51 mnkr vid 60 ändringar per år, båda 61 mnkr vid 160. Se docs/reviews/fornyad-granskning-7.3b.md. Tidigare källbegränsningar kvarstår.

## Förnyad granskning 7.3c – revision 52

Åtta kapitel granskade mot revision 45 och tidigare dokumentation. Förnyade stickprov av TF, OSL och IMY:s vägledning; preciseringar i kapitel 17, 19 och 20. Tidigare källbegränsningar kvarstår. Se docs/reviews/fornyad-granskning-7.3c.md.
