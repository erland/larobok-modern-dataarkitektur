# 11. Datadelning, federerad åtkomst och semantiska lager

När information redan finns i ett förvaltat datalager är det inte självklart att varje ny konsument behöver en egen kopia. En analys kan genomföras där informationen finns, genom en gemensam frågemotor eller på en kopia som skapats för ett specifikt ändamål. Valet påverkar prestanda, beroenden, informationssäkerhet och möjligheten att återskapa tidigare resultat.

## Kopiera eller läsa på plats?

En fysisk kopia ger konsumenten möjlighet att styra bearbetning, kapacitet och i viss mån historik oberoende av producentens miljö. Priset är ytterligare lagring, överföring och ansvar för att kopian hålls aktuell och hanteras enligt gällande bevarandevillkor. Direkt åtkomst minskar behovet av sådana kopior, men gör konsumenten beroende av den tillgänglighet och de egenskaper som producentens tjänst erbjuder.

| Mönster | Styrka | Viktig begränsning |
|---|---|---|
| Fysisk replikering | Isolerad arbetslast och möjlighet till lokal historik | Synkronisering och livscykel för kopior |
| Datavirtualisering | Gemensam logisk åtkomst utan krav på förhandskopiering | Beroende av underliggande källor |
| Federerade frågor | Kombination av information från flera källor | Varierande frågeprestanda och konsistens |
| Direkt datadelning | Återanvändning av redan publicerade dataset | Beroende av producentens åtkomstvillkor och kapacitet |

Mönstren är inte ömsesidigt uteslutande. En virtualiserad vy kan bygga på replikerad information, och en federerad fråga kan kombinera ett Data Warehouse med tabeller i ett Lakehouse.

## Datavirtualisering och federerade frågor

Datavirtualisering innebär att konsumenten får en logisk representation av information som inte nödvändigtvis finns samlad i ett fysiskt lager. Federerad frågebearbetning är en mekanism för att utföra frågor över flera datakällor. En gemensam SQL-vy kan exempelvis kombinera två analyslager utan att först skapa en permanent sammanfogad tabell.

Gu med flera undersökte 51 federationssystem, varav 33 industriella och 18 akademiska, i en forskningsöversikt publicerad 2024. Deras kvalitativa utvärderingsramverk omfattar federationsförmågor, informationssäkerhet, användargränssnitt och utvecklings- och supportförutsättningar. Studien bygger på dokumentation och publikationer; effektivitet mättes inte i utvärderingen. Den ger därför kriterier för urval snarare än en rangordning av prestanda [K073].

En distribuerad frågemotor som Trino kan genom anslutningar till olika datakällor delegera delar av frågebearbetningen till respektive källa, så kallad pushdown. Vilka operationer som kan delegeras beror på anslutningen och källans egenskaper [K074]. Om filtrering eller aggregering kan göras nära lagringen behöver mindre information föras över till frågemotorn. Om en stor sammanfogning i stället måste utföras i frågemotorn kan nätverk och beräkningskapacitet bli dimensionerande.

Arkitekten behöver därför bedöma faktiska frågeplaner, samtidiga arbetslaster och felbeteende. En gemensam fråga innebär inte automatiskt att samtliga källor läses vid samma logiska tidpunkt. För en rapport som ska kunna återskapas kan en dokumenterad uppsättning versionsbundna dataset eller en särskilt framställd kopia vara lämpligare.

Direkt federering mot kritiska operativa databaser bör inte vara ett generellt standardmönster. Även läsande frågor kan belasta källsystemen. En förvaltad analysreplik eller ett publicerat analysdataset kan ge bättre isolering utan att den logiska åtkomstmodellen behöver förändras.

## Direkt datadelning och zero-copy

Direkt datadelning innebär här att en producent erbjuder åtkomst till en publicerad informationsmängd utan att konsumenten först måste etablera ett eget permanent datalager. Begreppet zero-copy används ofta för sådana lösningar, men bör tolkas med försiktighet: data kan fortfarande överföras över nätverket, buffras och bearbetas hos konsumenten.

Delta Sharing är ett exempel på ett öppet protokoll för läsning av delade dataset. Dokumentationen beskriver hur en producent ger mottagaren åtkomst till data och hur kompatibla klienter kan läsa den delade tabellen [K075]. Det är ett exempel på en teknisk åtkomstmekanism, inte en komplett styrningsmodell eller en garanti för kompatibilitet med alla analysverktyg.

För en myndighet kan direkt datadelning förenkla återanvändning mellan analysmiljöer. Den förutsätter dock att åtkomst kan begränsas till rätt informationsmängd och att producentens tjänst klarar konsumenternas belastning. Återkallad åtkomst ska begränsa framtida läsningar, men när återkallelsen får genomslag beror bland annat på hur tjänsten hanterar redan utfärdade åtkomstuppgifter och pågående sessioner. Den kan inte i sig radera information som redan sparats hos mottagaren. Exporter, cache och härledda dataset behöver därför omfattas av en egen livscykelhantering.

## Semantiska lager

Att två analytiker kan läsa samma tabell betyder inte att de beräknar samma verksamhetsmått. Ett semantiskt lager tillhandahåller gemensamma definitioner av exempelvis mått, dimensioner och relationer, så att användare inte behöver implementera all verksamhetslogik på nytt i varje rapport.

Ett konkret exempel är dbt Semantic Layer, där mått definieras ovanpå befintliga modeller och kan konsumeras genom olika gränssnitt [K076]. Detta illustrerar en möjlig teknisk realisering av principen. Den dokumenterade tjänsten kräver ett dbt-plattformskonto; lokal drift och stöd i önskade klienter måste bedömas separat. Den organisatoriska uppgiften att komma överens om definitionerna kvarstår.

I referensmyndigheten kan måttet antal avslutade ärenden betyda antalet ärenden som fått ett slutligt beslut under perioden eller antalet ärenden som vid periodens slut har status avslutat. Återöppnade ärenden kan dessutom behandlas olika. Ett gemensamt mått behöver specificera händelse, tidsdimension, urval och hantering av rättelser. Olika legitima definitioner kan finnas parallellt om de namnges och dokumenteras tydligt.

Ett semantiskt lager ersätter alltså varken källornas datakontrakt eller den underliggande informationsmodelleringen. Det kan också medföra beroenden till en viss frågemotor eller ett visst rapportverktyg. Vid val av lösning bör myndigheten undersöka vilka konsumenter som faktiskt kan återanvända definitionerna och hur versioner av beräkningslogiken hanteras. Om en gemensam måttdefinition uppdateras för alla konsumenter behöver tidigare rapporter ändå kunna härledas till den definition och de dataversioner som användes när de framställdes, inom tillåtna bevarandetider.

## Datakataloger, marknadsplatser och Data Spaces

En datakatalog hjälper konsumenter att hitta och förstå tillgänglig information. En datamarknadsplats kan komplettera katalogen med funktioner för att begära åtkomst och etablera en relation till producenten. Begreppet innebär inte nödvändigtvis ekonomiska transaktioner. En intern marknadsplats är inte ett nytt datalager och behöver inte vara en separat produkt om befintliga katalog- och behörighetstjänster täcker behoven.

Data Spaces utvidgar samverkansperspektivet till självständiga organisationer. EU-kommissionens beskrivning av gemensamma europeiska dataområden betonar delade infrastrukturer och styrningsramverk för åtkomst och informationsutbyte [K077]. Ett dataområde kan kombinera olika tekniska åtkomstformer. Det är alltså inte synonymt med en federerad SQL-motor eller en central databas.

Vid informationsutbyte över organisationsgränser behöver deltagarna kunna identifiera varandra, förstå informationens betydelse och komma överens om villkoren för användningen. Teknisk interoperabilitet innebär inte att utlämnande eller vidareanvändning är tillåten. Sådana bedömningar behöver göras separat för det aktuella utbytet.

## Att välja åtkomstmönster

För referensmyndigheten är det rimligt att börja med att pröva direkt åtkomst till redan publicerade analysdataset. Återkommande tunga sammanfogningar, krav på oberoende tillgänglighet eller reproducerbara historiska resultat kan däremot motivera materialisering i ett förvaltat analyslager. En tillfällig analys över två befintliga lager kan använda federerade frågor utan att skapa ett nytt permanent lager.

Före etablering bör arkitekten verifiera följande för den konkreta arbetslasten:

- Att producentens och konsumentens tillgänglighetskrav är förenliga, även vid underhåll och fel.
- Att åtkomstkontrollen fungerar hela vägen genom frågemotorer, anslutningar och eventuella kopior, inklusive loggning och härledda resultat. Kontrollera även om kombinationer av uppgifter från olika källor kan avslöja skyddad information.
- Att nätverksbelastning, samtidighet och frågeplaner är acceptabla under realistiska förhållanden.
- Att resultatets tidsmässiga konsistens och reproducerbarhet motsvarar verksamhetens behov.
- Att gemensamma informationsdefinitioner kan användas i de verktyg som konsumenterna faktiskt behöver.

Dessa kriterier är en arkitektursyntes, inte en rangordning av produkter. Målet är att minimera onödiga kopior utan att skapa ohanterliga tillgänglighets- eller styrningsberoenden. En väl vald kombination av fysisk lagring, logisk åtkomst och gemensam semantik är ofta mer ändamålsenlig än att tillämpa samma åtkomstmönster på all information. Hur sådana gemensamma förmågor kan erbjudas som återanvändbara plattformstjänster behandlas i nästa kapitel.
