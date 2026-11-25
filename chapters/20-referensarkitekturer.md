# 20. Referensarkitekturer och val av teknikplattformar

Referensmyndigheten har ett etablerat Data Warehouse, systemspecifika mottagningszoner och ett växande behov av verksamhetsnära analys och AI. Vilken framtida arkitektur bör den välja? Ett användbart beslutsunderlag behöver beskriva mer än lagringsprodukten: hur information försörjs och konsumeras, vilka gemensamma tjänster som erbjuds och hur ansvar fördelas.

De fem referensarkitekturerna nedan är bokens egen syntes av tidigare kapitel. De beskriver olika tyngdpunkter i en målarkitektur, inte fem konkurrerande produkter. De tre första rör främst lagring och bearbetning, den fjärde ansvar och den femte åtkomst och placering.

## Fem kombinerbara referensarkitekturer

### Moderniserat Data Warehouse

Operativa IT-stöd publicerar information via standardiserade leveransgränssnitt till förvaltade mottagningszoner. Bearbetningar förädlar informationen till gemensamma analysmodeller och dataprodukter. Rapporter, analysverktyg och andra konsumenter använder definierade åtkomstgränssnitt. Gemensamma tjänster för leveransövervakning, testning och metadata kompletterar lagret. Dokumenterade mottagningsstrukturer kan behållas där de fungerar; förändringen behöver inte innebära att alla leveranser byggs om.

Alternativet är särskilt relevant när stabil rapportering och integrerad historik dominerar och det befintliga datalagret har tillräcklig teknisk livslängd. En viktig förändring kan vara att låta systemteam själva utveckla och underhålla standardiserade leveranser. Därmed kan specialistberoenden minska utan att den centrala analysmodellen ersätts. Begränsningen är att nya informationsformat eller bearbetningsmönster kan kräva kompletteringar. Ett moderniserat Data Warehouse ska inte bedömas som om det vore en oförändrad äldre installation.

### Data Lakehouse

Information tas emot i en gemensam lagringsmiljö där förvaltade tabeller kan bearbetas av kompatibla motorer. En katalog samordnar tabellmetadata. Behörighetsregler måste dessutom kunna upprätthållas av samtliga motorer och åtkomstvägar. Bearbetningsflöden producerar kvalitetssäkrade dataprodukter, som kan exponeras för SQL-analys, rapportering och modellträning. Dokument och andra icke-tabellära underlag hanteras med lämpliga representationer vid sidan av tabellerna.

Alternativet är relevant när flera arbetslaster återanvänder stora informationsmängder och när behovet av flera motorer är konkret. Kritiska förutsättningar är fungerande tabellhantering, samtidiga läsningar och skrivningar, säkerhet och ansvar för underhåll. Öppna format kan underlätta samverkan men eliminerar inte behovet av kompatibilitetstester. Om varje arbetslast ändå kräver en separat kopia eller egen förädlingskedja behöver nyttan av den gemensamma lagringen omprövas.

### Arkitektur med flera specialiserade datalager

Ett gemensamt analytiskt lager kompletteras med exempelvis en realtidsorienterad läsmodell och ett dokumentindex. Varje lager har en definierad uppgift och försörjs från ansvariga källor eller dataprodukter. En gemensam katalog beskriver härledning och åtkomst, medan respektive motor optimeras för sin arbetslast.

Alternativet är motiverat när ett konkret behov inte kan uppfyllas rimligt i huvudlagret. Exempelvis kan verksamhetsnära riskanalys ha andra aktualitets- och svarstidskrav än statistik. Ett sökindex för dokument behöver inte bli organisationens primära informationslager. Arkitekturen förutsätter att kopior kan uppdateras, återskapas och omfattas av livscykelregler. Annars riskerar specialiseringen att skapa okontrollerade parallella informationsbestånd.

### Domänorienterad dataarkitektur

Verksamhetsdomäner eller ansvariga systemteam publicerar och förvaltar dataprodukter enligt gemensamma kontrakt. Ett plattformsteam erbjuder självbetjänade tjänster för mottagning, bearbetning, kvalitet och åtkomst. Gemensamma verksamhetsmått och tvärgående modeller får uttryckligt ansvar och finansiering.

Alternativet är särskilt relevant när förändringar fördröjs av överlämningar och central specialistkapacitet. Fysisk lagring kan fortsatt vara gemensam, exempelvis i ett Data Warehouse eller Lakehouse. Förutsättningen är att domänerna har kompetens och mandat även för konsumenters behov. Om de enbart får ett nytt administrativt ansvar utan tekniska arbetsvägar förblir det centrala beroendet. Ett fullständigt Data Mesh-införande är inte ett krav.

### Federerad och hybrid dataarkitektur

Vissa informationsmängder tillgängliggörs där de förvaltas, medan andra överförs till gemensamma analysmiljöer. Kontrollerade frågegränssnitt, tjänster och vid behov materialiserade dataprodukter ger konsumenter tillgång över flera miljöer. Placering avgörs av bland annat skyddsbehov, arbetslast, aktualitet och möjligheten att driva tjänsten.

Alternativet är relevant när informationsmängder inte lämpligen samlas fysiskt eller när flera driftplatser behöver samverka. Federerad åtkomst ska inte förväxlas med hybrid drift: den ena gäller åtkomst över källgränser, den andra placering i olika typer av driftsmiljöer. De kan kombineras men behöver inte införas tillsammans. Kritiska kontroller gäller bland annat belastning på källor, åtkomstbeslut, tillgänglighet och informationsbetydelse. En federerad fråga kan behöva ersättas med en kontrollerad leverans när reproducerbar historik eller oberoende av källans tillgänglighet är avgörande.

## Informationsflöden och nödvändiga plattformstjänster

Följande översikt konkretiserar alternativen som logiska tjänstekedjor. Gemensam identitet, åtkomstkontroll, metadata, kvalitet, övervakning och informationslivscykel förutsätts i samtliga fall. Tjänsterna kan återanvändas från andra plattformar enligt kapitel 12; tabellen är inte en inköpslista.

| Alternativ | Typiskt informationsflöde | Särskilda tjänstebehov | Kritiskt beroende |
|---|---|---|---|
| Moderniserat Data Warehouse | Källa → mottagningszon → förädlad analysmodell → BI | Leveransmallar, transformation, avstämning, SQL-åtkomst | Samordnade definitioner och kontrollerad historik |
| Lakehouse | Källa → gemensam lagring → förvaltade tabeller → flera motorer | Tabellkatalog, kompatibla motorer, tabellunderhåll | Enhetliga transaktions- och åtkomstregler |
| Specialiserade lager | Källa eller dataprodukt → huvudlager och härledda läsmodeller → olika konsumenter | Synkronisering, indexering, återuppbyggnad | Kontrollerad härledning och aktualitet |
| Domänorienterad arkitektur | Ansvarig domän → kontrakt och publicering → dataprodukt → konsument | Självbetjäning, kontraktstest, katalog, leveransövervakning | Mandat och ägarskap genom hela leveransen |
| Federerad och hybrid arkitektur | Konsument ↔ kontrollerat gränssnitt ↔ förvaltad källa; vid behov materialisering | Frågeförmedling, identitetskoppling, nätverk och eventuell replikering | Källans tillgänglighet, skyddsgränser och belastning |

En sammanhängande målarkitektur för referensmyndigheten kan kombinera dessa kedjor. Operativa systemteam publicerar exempelvis kontraktsstyrda leveranser till befintliga mottagningszoner. Det centrala Data Warehouse förädlar dem till gemensamma statistiska modeller. En särskild läsmodell får aktuella uppgifter från ansvarig källa för verksamhetsnära riskanalys, medan ett dokumentindex försörjer en assistent enligt kapitel 19. Katalogen behöver visa vilken källa respektive representation härrör från och vem som ansvarar för den. Aktuell ärendestatus kan vid behov hämtas direkt från det operativa IT-stödet i stället för från analyslagret.

En ny Lakehouse-miljö kan prövas för en avgränsad arbetslast med gemensamma tabeller för exempelvis modellträning och utforskande analys. Den behöver inte ersätta rapportmiljön under försöket. Om båda miljöerna behålls måste det framgå vilken som förvaltar respektive informationsåtagande, hur avvikelser hanteras och vilka kopior som är avsiktliga. Gemensam kataloginformation betyder inte att samma fysiska lagring eller samma behörighet måste användas överallt.

![Exempel på en kombinerad målarkitektur för referensmyndigheten. Heldragna uppåtriktade pilar visar logiska informationsflöden. Lakehouse är en möjlig avgränsad prövning, inte ett krav; streckad kontur markerar denna avgränsning. Direktåtkomst visar förfrågan och svar utan obligatorisk mellanlagring. Gemensamma tjänster och styrning visas som tvärgående band, inte som ytterligare steg i informationsflödet. Källor och konsumenter kan återanvändas mellan kedjorna; placeringen anger inte separata driftplatser.](../assets/generated/IMG-20-01.svg)

Vid ett avbrott i källsystemets leverans ska rapporter kunna markera senaste verifierade uppdatering, en läsmodell signalera inaktuell information och en direkt fråga hantera att källan inte svarar. Vid återhämtning behöver kedjorna kunna stämmas av mot respektive källas leveransåtagande. Dessa beteenden bör ingå i arkitekturbeslutet, eftersom en gemensam plattform annars riskerar att ge olika konsumenter en felaktig bild av informationens aktualitet.

## Välj kombination utifrån det problem som ska lösas

| Observerad begränsning | Första alternativ att pröva | Vad kan motivera ett annat val? |
|---|---|---|
| Långsam anslutning av nya informationsfält | Moderniserad försörjning och domänansvar | Lagringsmotorn kan inte hantera nödvändiga förändringar |
| Dubblerade stora tabulära analysunderlag | Lakehouse med gemensam tabellåtkomst | Motorernas kompatibilitet eller skyddsbehov kräver separata miljöer |
| För lång svarstid i operativ analys | Specialiserad läsmodell | Fördröjningen ligger egentligen i källans leverans |
| Information måste förvaltas i skilda miljöer | Federerad åtkomst eller kontrollerade leveranser | Källbelastning, historik eller tillgänglighet kräver materialisering |
| Bristande samordning av definitioner och kvalitet | Gemensamma styrningsförmågor och tydligt informationsansvar | Inget lagringsbyte löser i sig detta problem |

För referensmyndigheten är en rimlig målhypotes att behålla den etablerade analysmiljön, utveckla domänorienterad informationsförsörjning och komplettera med specialiserade förmågor där mätbara behov finns. Lakehouse bör prövas om gemensam lagring för flera motorer kan minska ett faktiskt problem med kopior eller bearbetningskostnader. Federerad åtkomst bör väljas selektivt. Detta är en villkorad rekommendation för det fiktiva scenariot, inte ett beslut om en verklig myndighets teknik.

## Från referensarkitektur till teknikplattform

Beskriv först ett minsta sammanhängande tjänsteerbjudande: kontrollerad mottagning, bearbetning, lagring, publicering, åtkomst, metadata, kvalitet och driftövervakning. Säkerhet och informationslivscykel måste fungera genom hela kedjan. Ytterligare motorer, avancerade katalogfunktioner och automatiserad semantisk integration motiveras av användningsfall, inte av en önskan att fylla en produktkatalog.

Vid utvärdering av en integrerad produktfamilj respektive en sammansatt lösning bör organisationen dokumentera vilka funktioner som redan finns och vilka som måste byggas eller köpas. Bedöm även vilka komponenter som behöver kunna ersättas oberoende. I sin egen fallbeskrivning redogör Meta för en satsning på återanvändbara komponenter och gemensamma gränssnitt [K003]. Erfarenheten illustrerar ett sätt att hantera fragmentering, men utgör inte ett oberoende belägg för motsvarande nytta hos myndigheten.

## Beslutsunderlag och verifiering

Jämför kandidaterna med de sex bedömningsdimensionerna från kapitel 3. Bindande skydds- och livscykelkrav är urvalsvillkor. För övriga kriterier ska prioriteringar och avvägningar dokumenteras innan utvärderingen börjar. Undvik en totalsumma som döljer en avgörande svaghet.

| Bedömningsdimension | Konkret verifiering |
|---|---|
| Verksamhetsnytta | Genomför ett verklighetsnära analysfall och en förändring i källsystemet |
| Teknik | Mät aktualitet, svarstid, samtidighet och återhämtning vid fel |
| Utveckling och förvaltning | Låt ordinarie team etablera och ändra en leverans utan leverantörens hjälp |
| Organisation och ansvar | Hantera en kvalitetsavvikelse över två ansvarsgränser |
| Säkerhet och handlingsfrihet | Prova nekad åtkomst, livscykelåtgärd och återetablering i alternativ miljö |
| Ekonomi | Beräkna total ägandekostnad för samma servicenivå och tidshorisont |

Benchmarkstudierna i kapitel 8 [K002] [K009] [K032] ger exempel på avgränsade tekniska utvärderingar, inte färdiga beslutsresultat för en myndighet. Använd jämförbara datamängder, belastningsprofiler, resursramar och säkerhetskrav. Dokumentera konfigurationer, versioner, uppvärmning och variation mellan upprepade körningar. Ta med den befintliga miljön som referens. Komplettera prestandaprov med ett genomgående förändringsfall: en ny uppgift ska registreras i ett operativt IT-stöd, publiceras, kvalitetssäkras, behörighetskontrolleras och användas i en rapport. Mät både aktiv arbetstid och väntetid. Upprepa efter att pilotens etableringsstöd har upphört. Fastställ i förväg vilka resultat som innebär godkänt, underkänt eller behov av ytterligare prov.

Beräkna total ägandekostnad enligt kostnadsposterna i kapitel 8. FinOps-vägledningen [K036] kan användas som inspiration för att hänföra gemensam resursförbrukning till tjänster och arbetslaster även i lokal drift. Gör separata scenarier för normal belastning, tillväxt och alternativ driftplats. Skilj engångskostnader för övergång från återkommande drift- och förvaltningskostnader, och redovisa osäkra antaganden med intervall. För en sammansatt lösning måste integrations- och kompatibilitetsarbete räknas med; för en integrerad lösning även kostnader för export, övergång och eventuell ersättning av leverantörsspecifika funktioner. Räkna inte en minskad väntetid som en budgetbesparing utan att visa hur resurser faktiskt frigörs eller omfördelas.

Beslutet bör ange valda arkitekturmönster per arbetslast, gemensamma tjänster, ansvariga team, avvisade alternativ, kvarstående risker och verifierade respektive ännu oprövade antaganden. Därmed blir referensarkitekturen ett styrande underlag för investeringar snarare än en bild av en önskad teknisk slutpunkt. Nästa kapitel behandlar hur förändringen kan genomföras stegvis utan att äventyra fungerande informationsleveranser.
