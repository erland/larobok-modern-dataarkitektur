# 18. Driftsmiljöer, portabilitet och teknisk handlingsfrihet

En myndighet kan behöva byta driftplats därför att säkerhetsförutsättningarna förändras, en leverantör upphör med en tjänst eller en ny driftsmiljö erbjuder bättre kapacitet. Att kunna fatta ett sådant beslut utan att först bygga om hela informationsförsörjningen är en strategisk förmåga. Portabilitet är därför inte enbart en egenskap hos programvara, utan hos den samlade arkitekturen och organisationens sätt att förvalta den.

## Val av driftsmiljö

Lokal drift ger organisationen möjlighet att själv kontrollera fysisk infrastruktur, nätverksgränser och driftprocesser. Det förutsätter samtidigt tillgång till kompetens, tillräcklig kapacitet och fungerande förmågor för uppgradering, återställning och säkerhetsövervakning. En lokal installation av en kommersiell produkt kan dessutom innebära betydande beroenden till leverantören.

Publika molntjänster kan erbjuda snabb kapacitetstilldelning och färdigförvaltade tjänster för exempelvis lagring, distribuerad bearbetning och analys. Organisationen behöver väga denna nytta mot beroendet av tjänstespecifika gränssnitt, externa driftprocesser, prismodeller och avtalsvillkor. Kostnaden för en arbetslast bör inkludera lagring, bearbetning, dataöverföring och den egna förvaltningen, inte bara tjänstens pris [K036].

En hybridarkitektur kan innebära att känsliga informationsmängder bearbetas lokalt medan andra arbetslaster använder externa tjänster. Den kräver emellertid samordning av identiteter, nätverk, övervakning, informationsklassning och livscykelhantering över flera miljöer. Om stora datamängder kontinuerligt behöver överföras mellan miljöerna kan såväl kostnader som fördröjningar bli betydande. Hybriddrift är därför ett medvetet val av placering för olika arbetslaster, inte ett självändamål.

## Informationssuveränitet och kontroll

Informationssuveränitet används här som ett samlingsbegrepp för faktisk kontroll över informationens behandling, åtkomst och tillgänglighet. Begreppet ersätter inte den rättsliga bedömningen i kapitel 17. Geografisk placering är en viktig faktor, men organisationen behöver även kartlägga administratörsåtkomst, underleverantörer, support, telemetri, nyckelhantering och vilka jurisdiktioner som berörs.

Vid behandling som omfattas av GDPR kan tredjelandsöverföring enligt IMY innebära att personuppgifter görs tillgängliga för en mottagare utanför EU/EES, inte bara att filer flyttas dit [K090]. Bedömningen behöver bland annat identifiera exportören och den separata mottagaren i tredjeland. En europeisk lagringsregion är därför inte i sig tillräckligt underlag för bedömningen av en molntjänst. IMY:s undersökning av sju svenska myndigheters molnanvändning från 2022 illustrerar också att förutsättningarna för sådana överföringar behöver klarläggas [K091]. Undersökningen är avgränsad och säger inte hur samtliga myndigheter arbetar i dag.

## Cloud native och alternativa driftplatser

Cloud native är inte liktydigt med publik molndrift. CNCF:s definition omfattar bland annat privata, publika och hybrida miljöer och betonar löst kopplade system och automation [K092]. För en organisation som i första hand driver sina IT-stöd lokalt kan sådana principer göra det lättare att etablera motsvarande funktionalitet på en annan driftplats.

Containerpaketering, deklarativ konfiguration och automatiserade installationer är viktiga byggstenar. De räcker dock inte om bearbetningsjobben förutsätter en viss leverantörs identitetstjänst, lagringsgränssnitt eller katalog. Organisationen behöver skilja mellan den funktion som ska vara flyttbar och de plattformstjänster som får ersättas med alternativa realiseringar. Målet är att kunna återetablera den nödvändiga funktionaliteten inom godtagbar tid, inte att alla tekniska komponenter måste vara identiska.

## Portabilitet genom hela arkitekturen

Interoperabilitet innebär här att komponenter kan samverka över definierade gränssnitt, medan portabilitet avser möjligheten att överföra data och funktionalitet. Återetableringsförmåga omfattar dessutom de praktiska resurser och processer som krävs för att återuppta verksamheten på en annan driftplats. Ett kompatibelt gränssnitt är inte i sig ett bevis på att hela flytten fungerar.

| Nivå | Vad behöver kunna återskapas eller flyttas? | Exempel på kvarstående beroende |
|---|---|---|
| Informationslagring | Data, tabellstruktur, versioner och historik | Lagringssökvägar och specifika datatyper |
| Bearbetning | Transformationer, körmiljö och schemaläggning | Proprietära SQL-funktioner och orkestrering |
| Datastyrning | Metadata, kontrakt, behörigheter och lineage | Katalogens gränssnitt och policysemantik |
| Konsumtion | Rapporter, semantiska modeller och åtkomstgränssnitt | Verktygsspecifika modeller och anslutningar |
| Infrastruktur | Nätverk, identiteter, konfiguration och drifttjänster | Leverantörsspecifika infrastrukturtjänster |

Öppna fil- och tabellformat minskar vissa beroenden. Apache Iceberg specificerar exempelvis hur tabellmetadata beskriver bland annat snapshots och datafiler [K049]. Ett öppet format är dock inte detsamma som en fullständigt flyttbar dataplattform. Katalogen måste kunna lokalisera tabellens aktuella metadata, och den alternativa frågemotorn måste stödja de funktioner och formatversioner som faktiskt används. Icebergs REST-baserade kataloggränssnitt kan minska ett sådant integrationsberoende, men standardiserar inte alla omgivande säkerhets- och driftfunktioner [K093].

Motsvarande bedömning behövs för ett Data Warehouse: export av tabeller i ett öppet format löser inte automatiskt portabiliteten för lagrade procedurer, åtkomstregler eller rapportdefinitioner. En specialiserad databas kan vara ändamålsenlig även om ett framtida byte kräver ombyggnad. Då bör beroendet vara ett dokumenterat och accepterat arkitekturval.

## Avtal och teknisk handlingsfrihet

EU:s dataförordning (Data Act), kapitel VI, innehåller regler om byte mellan databehandlingstjänster och övergång till egen ICT-infrastruktur. Artikel 23 behandlar hinder för byte och artikel 25 avtalsvillkor [K037]. Reglernas tillämplighet och eventuella undantag måste bedömas för den aktuella tjänsten. Artikel 30.1 ställer krav på rimliga åtgärder för att underlätta funktionell likvärdighet vid byte mellan infrastrukturtjänster av samma typ. För andra tjänster behandlar artikel 30 bland annat öppna gränssnitt och export i maskinläsbart format. Artikel 31 innehåller särskilda undantag. Rätten till export och stöd vid byte är inte en generell garanti för identisk funktionalitet [K037]. Bedömningen avser regelverket i november 2026.

Vid anskaffning bör organisationen därför begära en konkret beskrivning av exporterbara data och digitala tillgångar, gränssnitt, dokumentation, övergångsstöd och kostnader. Även återstående informationskopior och avslut av åtkomst måste hanteras i enlighet med tillämpliga krav. Kostnaden för att upprätthålla ett alternativ bör vägas mot konsekvenserna av ett framtida byte; fullständig parallell drift är sällan ett nödvändigt krav för alla arbetslaster.

## Verifiera flyttbarheten i praktiken

Referensmyndigheten har ett lokalt Data Warehouse och överväger att etablera en ny dataplattform med möjlighet till alternativ driftplats. Ett lämpligt första test är att välja en representativ dataprodukt med historik, schemalagda transformationer, metadata och olika åtkomstnivåer. Den alternativa miljön ska vara tillräckligt oberoende för att exponera de beroenden som testet avser att pröva. Använd syntetiska eller godkända testdata.

Testet bör omfatta följande moment:

- Etablera målmiljön från versionshanterad konfiguration och dokumenterade förutsättningar.
- Överför information och nödvändig metadata samt kontrollera fullständighet, historik och semantik.
- Kör bearbetningsflöden och jämför resultaten mot dokumenterade toleranser.
- Återskapa identiteter och åtkomstregler och verifiera både tillåten och nekad åtkomst. Flytta inte hemligheter okontrollerat.
- Anslut representativa konsumenter och pröva driftövervakning, återställning och fortsatt informationsförsörjning.
- Verifiera att bevarandevillkor, gallringsregler, revisionsspår och åtkomstbegränsningar fungerar även efter flytten och att kvarvarande kopior hanteras kontrollerat.
- Mät övergångstid, databortfall, kostnad och manuella arbetsmoment. Dokumentera kvarstående beroenden och hur en avbruten flytt återställs.

Ett lyckat test av en dataprodukt bevisar inte att hela plattformen är flyttbar. Testets omfattning behöver utökas efter risk, datavolym och variation i arbetslaster. Vid större förändringar bör relevanta tester upprepas. För en kritisk tjänst behöver även kontinuitetskrav och tillåten dataförlust ingå i acceptanskriterierna.

## Prioritera handlingsfrihet där den gör skillnad

Kritiska förmågor är kontrollerad export, dokumenterad återetablering, informationsintegritet, fungerande säkerhetskontroller och tillgång till kompetens för ett byte. Gemensamma gränssnitt, automatiserade installationer och återkommande flyttprov kan minska arbetsinsatsen. Samtidig drift hos flera leverantörer och helt utbytbara bearbetningsmotorer är kompletterande förmågor vars värde behöver motiveras av konkreta behov.

En myndighet bör inte välja en tekniskt sämre lösning enbart för att maximera generell portabilitet. Det avgörande är att förstå vilka beroenden som accepteras, kunna verifiera de alternativa driftvägar som är strategiskt viktiga och ha en realistisk plan för att hantera övriga beroenden. Nästa del återvänder till informationsanvändningen och visar hur analys och AI kan stödjas utan att varje behov leder till ett nytt centralt datalager.
