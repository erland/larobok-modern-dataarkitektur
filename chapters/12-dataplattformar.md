# 12. Dataplattformar och självbetjänade plattformstjänster

En organisation kan ha ett modernt Lakehouse och ändå behöva beställa varje ny informationsleverans från en central specialistgrupp. Den kan också ha flera olika datalager och erbjuda systemteam och analytiker ett enhetligt, självbetjänat arbetssätt. Skillnaden ligger i plattformens tjänsteerbjudande, inte enbart i lagringstekniken.

En dataplattform är här en förvaltad helhet av tekniska förmågor, tjänstegränssnitt och gemensamma arbetssätt för att tillgängliggöra, bearbeta och använda information. Den kan omfatta ett eller flera datalager och återanvända tjänster från organisationens utvecklingsplattform, integrationsplattform och säkerhetsinfrastruktur. Den behöver inte vara en enda produkt eller en enda driftsmiljö.

## Från tekniska komponenter till plattformstjänster

En installerad frågemotor är en teknisk komponent. En förvaltad analystjänst erbjuder dessutom ett definierat sätt att ansluta, få behörighet, tilldela resurser, övervaka användning och hantera fel. Det är tjänstens samlade egenskaper som avgör hur mycket av den tekniska komplexiteten användaren behöver hantera själv.

CNCF:s vägledning om interna plattformar betonar självbetjänade gränssnitt, dokumentation och standardiserade arbetsvägar, liksom att plattformen behöver förvaltas utifrån användarnas behov [K078]. Vägledningen avser främst utvecklingsplattformar, men principerna är också relevanta för dataplattformar. En plattformstjänst för data kan exempelvis tillhandahålla ett versionshanterat gränssnitt för att etablera ett dataset med godkänd lagring, åtkomstpolicy och övervakning. Teamet behöver då inte veta vilken fysisk lagringsnod som används. Gränssnittet behöver däremot synliggöra vilka garantier tjänsten erbjuder, exempelvis tillgänglighet, återställning och tillåtna informationsklasser.

Självbetjäning innebär inte att alla beslut delegeras. En analytiker kan få möjlighet att skapa en arbetsyta inom ett tillåtet informationsområde utan att själv besluta om åtkomst till sekretesskyddade uppgifter. Automatiserad etablering bör bygga på godkända villkor, medan undantag hanteras genom en tydlig beslutsväg.

## Vilka förmågor behöver plattformen erbjuda?

Följande indelning är en arkitektursyntes. Kritisk innebär här att förmågan behöver finnas för ett tillförlitligt, återanvändbart erbjudande i den aktuella miljön, inte att varje förmåga behöver realiseras med en egen produkt. Vissa funktioner kan tillhandahållas av befintliga gemensamma tjänster.

| Kritisk förmåga | Vad tjänsteerbjudandet behöver säkerställa |
|---|---|
| Informationsförsörjning | Godkända anslutningar, överföring, felhantering och återläsning |
| Lagring och livscykel | Tilldelning av lagringsutrymme, skydd, bevarande och avveckling |
| Bearbetning | Kontrollerad exekvering av frågor och transformationer med resursisolering |
| Orkestrering | Hantering av beroenden, körningar, fel och omkörningar |
| Metadata och upptäckbarhet | Identifiering av dataset, ansvariga, strukturer och användningsvillkor |
| Kvalitetskontroll | Validering, mätning och hantering av avvikelser |
| Säkerhet och åtkomst | Identiteter, behörigheter, policytillämpning och revisionsspår |
| Drift och återställning | Övervakning, incidenthantering och verifierad återställningsförmåga |
| Självbetjänade gränssnitt | Dokumenterade och automatiserade sätt att använda godkända tjänster |

Åtkomst till publicerade dataset och dokumenterade konsumtionsgränssnitt ingår i det grundläggande erbjudandet; ett särskilt semantiskt lager är däremot behovsberoende. Förmågan till kostnadsuppföljning ingår också i ett uthålligt erbjudande. I lokal drift kan den börja med mätning av lagringsvolym, beräkningsresurser och belastning per team eller arbetslast. Det behövs inte intern fakturering för att kunna identifiera kostnadsdrivare och planera kapacitet. FinOps Foundations vägledning avser molnbaserade dataplattformar och betonar koppling mellan resursanvändning, arbetslaster och ansvariga team. Tillämpningen i lokal drift är en anpassning av dessa principer [K036].

Kompletterande förmågor kan vara kontinuerlig strömbearbetning, federerade frågor, semantiska lager, avancerad lineage, vektorsökning, Feature Stores och datamarknadsplatser. De blir kritiska när ett konkret verksamhetsbehov eller kontrollkrav förutsätter dem. En organisation som enbart behöver stabil daglig rapportering behöver exempelvis inte börja med en generell strömbearbetningsplattform. Däremot kan grundläggande spårbarhet och kontrollerad åtkomst inte skjutas upp med hänvisning till att avancerade metadatafunktioner planeras senare.

## Gränsdragning mot organisationens övriga plattformar

Dataplattformen är ett logiskt tjänsteerbjudande. Den behöver inte äga varje teknisk komponent som används i en informationskedja. Följande ansvarsfördelning är ett möjligt arkitekturval för en organisation med etablerade gemensamma IT-plattformar.

| Plattform | Gemensamt ansvar | Dataplattformens komplettering |
|---|---|---|
| Utvecklingsplattform | Versionshantering, bygg, test, distribution och artefakter | Mallar för informationsleveranser, kontraktskontroller och publicering av dataset |
| Integrationsplattform | API-hantering, meddelanden och säker transport | Uttagsbeskrivning, initial laddning, förändringsfångst, avstämning och återläsning av dataset |
| Infrastrukturplattform | Beräkningskraft, nätverk, grundläggande lagring och återställning | Tabell- och datasetförvaltning, arbetslastisolering samt informationsspecifik livscykel |
| Säkerhetstjänster | Identitet, autentisering, nycklar, hemligheter och logginsamling | Behörigheter till dataset, rader och kolumner där det behövs, samt informationsrelaterade revisionsspår |
| AI-plattform | Modellträning, modellversioner, inferens och AI-specifik exekvering | Förvaltade tränings- och referensdataset, kontrollerad informationsåtkomst och dokumenterade beroenden |

Gränserna är inte absoluta. En integrationsplattform kan exempelvis redan erbjuda CDC och deklarativa överföringar, och en AI-plattform kan tillhandahålla vektorindex. Då bör dataplattformens tjänsteerbjudande integrera dessa förmågor i stället för att automatiskt anskaffa motsvarande komponenter. Det avgörande är att hela informationskedjans krav uppfylls och att ansvaret för tjänstens kvalitet är tydligt.

### Ett sammanhängande tjänsteerbjudande

När ett systemteam i referensmyndigheten publicerar en ny informationsleverans kan konfigurationen versionshanteras och testas med utvecklingsplattformens befintliga tjänster. En godkänd anslutning använder integrationsplattformens transport. Dataplattformen tillhandahåller mottagning, kvalitetskontroll, metadata och publicering. Identiteter och hemligheter hanteras av gemensamma säkerhetstjänster, medan beräkning och fysisk lagring tillhandahålls av infrastrukturen. Konsumenten får ett dokumenterat dataset, inte en uppgift att själv samordna alla dessa funktioner.

För att detta ska fungera behöver plattformsteamen avtala om tjänstegränssnitt, ansvar vid fel, resursgränser, förändringshantering och support. Dataplattformens tjänsteansvariga behöver kunna följa upp hela leveransen även när en underliggande tjänst förvaltas av någon annan. Om en rutinändring fortfarande kräver separata beställningar till varje plattform har den tekniska återanvändningen inte blivit självbetjäning.

Dataspecifika förmågor som katalogisering av dataset, datakontrakt, kvalitetsregler och lineage bör bedömas utifrån om befintliga tjänster kan representera informationens betydelse och beroenden. En generell komponentkatalog eller teknisk driftövervakning är inte nödvändigtvis tillräcklig. Samtidigt behöver inte dataplattformen bygga egen autentisering, egen kodförvaltning eller egen meddelandebuss när de gemensamma tjänsterna uppfyller kraven. Gemensamma beroenden ska verifieras med avseende på skyddsnivå, kapacitet och alternativ driftplats innan de görs till obligatoriska standardvägar.

![Ett logiskt dataplattformserbjudande med självbetjänade gränssnitt, dataspecifika funktioner och återanvändning av gemensamma IT-tjänster. Streckade pilar visar tjänstenyttjande, inte informationsflöden. Gränsdragningen är ett exempel; AI-plattformens tjänster nyttjas vid behov. Erbjudandet behöver inte motsvara en enda produkt eller driftplats.](../assets/generated/IMG-12-01.svg)

## Orkestrering och gemensam exekvering

En orkestreringstjänst håller reda på vilka arbetsmoment som ska utföras, deras beroenden och resultat. Den är inte nödvändigtvis den motor som utför bearbetningen. Ett arbetsflöde kan exempelvis kontrollera att ett uttag är färdigt, starta en SQL-transformation, köra kvalitetskontroller och först därefter publicera en ny version av ett dataset. Den underliggande bearbetningen kan utföras i en databas eller en distribuerad motor.

Det gemensamma styrskiktet behöver kunna skilja mellan ett tekniskt lyckat jobb och en godkänd informationsleverans. Om alla steg avslutas utan tekniska fel men ett kvalitetsvillkor inte uppfylls ska konsumenterna inte automatiskt få den nya versionen. För varje körning bör det gå att identifiera ingångsdata, konfiguration, kodversion, resultat och felstatus i den omfattning som krävs för felsökning och återställning. Omkörning behöver vara utformad så att tidigare lyckade steg inte orsakar oavsiktliga dubbla effekter.

Gemensam orkestrering behöver inte innebära att alla jobb delar samma exekveringsresurser. Kritiska rapporter, experimentella analyser och resurskrävande modellträning kan behöva olika prioritet, kvoter och isolering. Fel i en arbetslast bör isoleras så att de inte slår ut styrskiktet eller andra arbetslaster. Ett centralt styrskikt utan återställningsplan kan annars bli en gemensam felpunkt.

## Självbetjäning i praktiken

Utgå från några återkommande användarresor, inte från en lista över verktyg. För den fiktiva referensmyndigheten kan tre tjänsteerbjudanden vara tillräckliga för en första förflyttning:

- Publicera en informationsleverans: systemteamet väljer en godkänd anslutning, beskriver leveransen och får ett testbart flöde med kontrollpunkter och övervakning.
- Förädla en dataprodukt: ett analysteam etablerar en versionshanterad transformation, deklarerar beroenden och kvalitetsvillkor och publicerar resultatet efter godkända kontroller.
- Konsumera information: en behörig användare hittar en produkt, begär vid behov åtkomst och ansluter ett godkänt analysverktyg inom tilldelade resursgränser.

För varje arbetsväg behöver det vara tydligt vad som kan göras direkt, vad som kräver beslut och vem som hjälper till när standardvägen inte räcker. Ett webbgränssnitt kan underlätta upptäckt och introduktion, medan API:er och versionshanterad konfiguration kan göra samma tjänster möjliga att använda i automatiserade arbetsflöden. En portal som bara skapar ärenden till plattformsteamet är inte i sig självbetjäning.

Ett exempel på ett avgränsat plattformserbjudande är Uber DataCentral, som organisationen beskriver som ett gemensamt stöd för insyn i datajobb och kostnadsfördelning. Uber beskriver hur motorernas metadata samlas in och hur felregler används för att ge användare begripliga felmeddelanden och åtgärdsförslag [K079]. För en myndighet behöver motsvarande felsökningsuppgifter omfattas av behörighetskontroll eftersom exempelvis frågetext och loggar kan innehålla skyddsvärd information. Erfarenheten illustrerar att självbetjäning även omfattar förvaltning efter publicering, inte bara etablering av nya resurser. Den är självrapporterad och visar inte att samma effekter uppstår i andra organisationer.

## Integrerad eller sammansatt plattform

En integrerad plattform kan erbjuda lagring, bearbetning, katalog och administration i en sammanhängande produktfamilj. En sammansatt plattform kombinerar flera komponenter bakom ett gemensamt tjänsteerbjudande. Det finns också mellanformer där vissa delar köps som en integrerad helhet medan andra återanvänds från organisationens befintliga miljö.

| Perspektiv | Integrerad realisering | Sammansatt realisering |
|---|---|---|
| Införande | Färdiga integrationer kan minska startarbetet | Integration och kompatibilitet behöver etableras |
| Förvaltning | Färre produktgränser, men beroende av leverantörens livscykel | Fler gränser att testa och förvalta |
| Anpassning | Beroende av produktens utbyggnadsmöjligheter | Komponenter kan väljas efter avgränsade behov |
| Handlingsfrihet | Export, API:er och ersättningsmöjligheter måste verifieras | Öppna gränssnitt hjälper, men egen integration kan skapa nya låsningar |
| Säkerhet | Sammanhållen policy är möjlig inom produktens gränser | Gemensam policy måste tillämpas konsekvent över komponentgränser |

Meta beskriver i sammanfattningen till konferensbidraget Shared Foundations hur självständigt framvuxna datasystem hade lett till fragmentering. Programmet inriktades på återanvändbara komponenter, minskad dubblering och gemensamma API:er [K003]. Det illustrerar att en gemensam teknisk grund kan kräva samordning över många organisatoriska gränser. Metas skala och egenutvecklade miljö skiljer sig väsentligt från referensmyndighetens; erfarenheten motiverar inte att en myndighet bygger motsvarande teknik själv.

Det centrala beslutet är vilka gränssnitt organisationen behöver kontrollera långsiktigt. En sammansatt lösning utan gemensamt ansvar för kompatibilitet kan ge högre förvaltningskostnad än en integrerad produkt. Omvänt kan en integrerad produkt med otillräckliga export- och åtkomstmöjligheter göra framtida förändringar dyra. Pröva därför en avgränsad export och återinläsning av dataset med metadata samt hur kontroller kan återskapas i en alternativ miljö. För komponenter som behöver kunna ersättas bör även gränssnitt och kompatibilitet provas.

## Plattformen som en förvaltad intern produkt

Plattformsteamets uppgift är att utveckla och driva återanvändbara tjänster, inte att genomföra alla verksamhetsspecifika förändringar. Det behöver ha mandat och resurser att förbättra de arbetsvägar som används av många team. Systemteam och informationsansvariga behåller däremot ansvaret för den information de publicerar enligt överenskommen ansvarsfördelning. Plattformen kan kontrollera att ett kontrakt finns och att definierade regler körs; den kan inte ensam garantera att verksamhetsdefinitionerna är riktiga.

Följ upp tjänsteerbjudandet genom ledtid för etablering, andel standardärenden utan manuell handläggning, kvalitet och återställning, resursförbrukning samt användarnas återkommande problem. Mät även plattformsteamets köer och kostnaden för undantag. Om ett nytt gemensamt verktyg ökar antalet manuella överlämningar har det inte nödvändigtvis förbättrat tjänsten, även om antalet tekniska komponenter minskar.

För referensmyndigheten är en lämplig start att låta befintligt Data Warehouse vara kvar och etablera ett gemensamt erbjudande kring ett fåtal återkommande informationsleveranser. Utöka först när arbetsvägarna fungerar i praktiken. En dataplattform är således inte ett alternativ till Data Warehouse eller Lakehouse, och självbetjäning kräver inte att allt dataägande decentraliseras. Hur ansvar kan fördelas mellan verksamhetsdomäner och gemensamma funktioner är nästa arkitekturfråga.
