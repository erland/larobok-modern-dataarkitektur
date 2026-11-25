# 8. Jämförande analys av lagringsarkitekturer

En myndighet med ett etablerat Data Warehouse behöver inte börja sin modernisering med att välja ett nytt datalager. Den behöver först avgöra vilka begränsningar som faktiskt finns, vad de beror på och vilka som kan undanröjas utan en förändring av lagringsarkitekturen. Om nya analysbehov kräver andra informationsformat eller bearbetningsmönster kan en kompletterande lagringsmiljö däremot vara motiverad.

## Jämför likvärdiga alternativ

Data Warehouse, Data Lake och Lakehouse har olika tyngdpunkter. Gränserna mellan tekniska realiseringar är emellertid inte absoluta. Ett modernt Data Warehouse kan stödja semistrukturerad information och separera beräkning från lagring, medan en Lakehouse-miljö kan erbjuda välstrukturerade tabeller för stabil rapportering. En jämförelse som ställer ett äldre datalager mot en ny Lakehouse-produkt riskerar därför att tillskriva själva arkitekturmönstret fördelar som egentligen följer av modernare teknik.

Följande jämförelse är en arkitektursyntes av föregående kapitel, inte en uppmätt rangordning av produkter.

| Behov | Data Warehouse | Data Lake | Lakehouse |
|---|---|---|---|
| Återkommande, kvalitetssäkrad rapportering | Naturlig tyngdpunkt | Kräver ytterligare bearbetning och struktur | Lämpligt med förvaltade tabeller och modeller |
| Dokument, bilder och rådata | Kan kräva kompletterande lagring | Naturlig tyngdpunkt | Flexibel underliggande lagring; tabellformat för tabulära data |
| Flera bearbetningsmotorer över samma data | Varierar med produkt och gränssnitt | Möjligt över gemensamma filer | Central ambition; kompatibilitet måste verifieras |
| Kontrollerade tabelluppdateringar | Vanligen integrerat | Kräver kompletterande mekanismer | Stöd via tabellformat och kompatibla motorer |
| Förvaltningsinsats | Beror på integration, produkt och driftmodell | Risk för omfattande eget struktur- och metadataarbete | Beror bland annat på integration och tabellunderhåll |

Ingen av lösningarna garanterar gemensamma verksamhetsdefinitioner, korrekt information eller snabb informationsförsörjning. Dessa egenskaper behöver realiseras oberoende av lagringsvalet.

## Vad jämförande forskning kan visa

Harby och Zulkernines studie av Data Lakehouse, publicerad i Information Systems 2025, innehåller både en forskningsöversikt och ett experiment med HDFS, Hive och Delta Lake [K009]. Studien är relevant för att förstå skillnader mellan konkreta tekniska realiseringar. Den omfattar däremot inte alla moderna datalagermotorer. Resultat för Hive kan inte utan vidare överföras till ett modernt kommersiellt Data Warehouse eller en annan SQL-motor.

Oliveira e Sá, Gonçalves och Kaldeich beskriver 2024 en jämförande utvärdering av molnbaserade datalager [K032]. Den illustrerar att även inom en och samma produktkategori behöver alternativen utvärderas separat. En jämförelse av molntjänster kan inte direkt användas som kostnads- eller prestandaprognos för egen drift.

LHBench från 2022 är i stället utformat för att undersöka skillnader mellan Lakehouse-lagringssystem, bland annat vid många filer och återkommande förändringar [K002]. I testmiljön med Spark på AWS EMR och S3 visade exempelvis Merge-on-Read för Hudi kortare uppdateringstid men längre efterföljande frågetid än Copy-on-Write. Det illustrerar varför skriv- och läsprestanda måste bedömas tillsammans. Resultatet gäller de testade versionerna från 2022, inte dagens produkter generellt. Sådana tester kompletterar traditionella analytiska frågetester, men de utgör inte en heltäckande jämförelse av färdiga dataplattformar [K002].

För arkitekten är studiernas viktigaste bidrag att identifiera relevanta arbetslaster och möjliga flaskhalsar. Det saknas här underlag för en allmängiltig rangordning av arkitekturerna efter prestanda eller kostnad. En lokal utvärdering bör därför dokumentera motorversioner, datafördelning, hårdvara, samtidighet, cacheförhållanden, skrivmönster och underhållsarbete. Resultaten behöver också omfatta fel och återhämtning, inte enbart lyckade frågor.

## Utgå från användningsmönster

Referensmyndigheten kan ha tre olika behov: stabil statistisk rapportering, utforskande analys av stora historiska informationsmängder och verksamhetsnära riskanalys med kort aktualitetskrav. De behöver inte tillgodoses med samma tekniska lösning.

För den statistiska rapporteringen är det avgörande att rapporternas definitioner och historiska underlag är kontrollerade. Om det befintliga datalagret redan uppfyller dessa krav kan förbättrad informationsförsörjning och resursisolering vara mer värdefulla investeringar än ett byte av lagringsteknik.

Utforskande analys kan behöva tillgång till information som inte passar i befintliga rapportmodeller. En Data Lake kan då ge en separat yta för tillåten lagring och bearbetning av sådana underlag. Om utforskande analys och återkommande rapportering i hög grad använder samma tabulära data kan Lakehouse vara ett alternativ för att minska behovet av vissa kopior och överföringar. Nyttan behöver verifieras mot kostnaden för att samordna motorer och förvalta tabeller.

Vid verksamhetsnära riskanalys bör aktualitetskravet delas upp i fördröjning från källsystem, bearbetningstid och svarstid vid konsumtion. En snabbare frågemotor löser inte ett problem som beror på att informationen bara överförs en gång per dygn. Om analysen måste leverera resultat inom en operativ process kan ett särskilt realtidsanalyslager vara motiverat, enligt resonemanget i kapitel 7.

## Förvaltning och ekonomi

En ekonomisk jämförelse behöver omfatta hela den tjänst som organisationen ska leverera. Licensfri programvara är inte liktydig med kostnadsfri drift. En integrerad produkt kan reducera integrationsarbete, men kan också medföra begränsningar eller kostnader för kapacitet och framtida byte. En sammansatt lösning kan erbjuda större valfrihet, samtidigt som organisationen får ansvar för fler gränssnitt och uppgraderingar.

FinOps Foundations vägledning för dataplattformar betonar samverkan mellan ekonomiska och tekniska roller för att förstå kostnader och användning [K036]. För lokal drift behöver motsvarande resonemang anpassas till investeringar, kapacitetsplanering och intern resursfördelning snarare än enbart molnfakturor.

En jämförelse över samma tidshorisont bör omfatta:

- Teknik: licenser, support, beräkning, lagring, nätverk, redundans och reservkapacitet.
- Utveckling: integrationsarbete, modellering, automatisering och förändringar i anslutna IT-stöd.
- Förvaltning: övervakning, incidenthantering, uppgraderingar, återställningsprov och specialistkompetens.
- Organisation: samordning, väntetid, utbildning och beroenden mellan team.
- Förflyttning: migrering, parallell drift, verifiering, avveckling och framtida utträde.

Beräkna kostnader för ett basscenario och alternativa belastnings- och tillväxtscenarier. Skilj mellan redan nedlagda kostnader, framtida undvikbara kostnader och sådana gemensamma kostnader som kvarstår även efter ett teknikbyte. Redovisa nyttor separat så att exempelvis en kortare utvecklingsledtid inte dubbelräknas som både besparing och verksamhetsnytta.

### Ett illustrativt femårsexempel

Anta att referensmyndigheten jämför vidareutveckling av sitt Data Warehouse (A) med en kompletterande Lakehouse-miljö (B). Båda alternativen antas kunna uppfylla samma krav för de arbetslaster som jämförs. Siffrorna nedan är illustrativa räkneantaganden, inte marknadspriser eller prognoser. Beloppen anges i miljoner kronor, i fast prisnivå, utan diskontering.

| Kostnadspost | A | B |
|---|---:|---:|
| Etablering och ombyggnad av leveranser, engångsbelopp | 3 | 7 |
| Övergång, extra parallell drift och verifiering, engångsbelopp | 1 | 3 |
| Teknik och support per år | 3 | 4 |
| Löpande teknisk förvaltning per år | 2 | 3 |
| Förändringsarbete per år | 2,4 | 1,2 |
| Total kostnad över fem år | 41 | 51 |

Förändringsarbetet motsvarar i exemplet 60 leveransändringar per år med 40 respektive 20 aktiva arbetstimmar per ändring, till en kalkylkostnad på 1 000 kronor per timme. Specialistarbete ingår i dessa timmar; det räknas inte en gång till som en separat kostnad. Den löpande tekniska förvaltningen avser i stället exempelvis uppgraderingar, incidenter och driftunderhåll. B:s årliga teknik- och förvaltningskostnader omfattar båda kvarvarande miljöerna. Övergångsposten omfattar endast tillfälliga merkostnader utöver den löpande driften.

B är tio miljoner kronor dyrare över fem år trots det antagna lägre förändringsarbetet. Om antalet ändringar ökar till 160 per år, medan timåtgång och övriga kostnader är oförändrade, blir femårskostnaden 61 miljoner för båda alternativen. Denna brytpunkt är endast en känslighetsanalys: kapacitetsbehov och kostnader kan i verkligheten förändras med volymen. Vid teknikvalet behöver myndigheten även undersöka om samma minskning av timåtgång kan uppnås i A genom bättre självbetjäning. Om B dessutom möjliggör ett nytt verksamhetsbehov bör den nyttan bedömas separat, inte antas ingå i kostnadsjämförelsen.

Frigjorda arbetstimmar innebär inte automatiskt en budgetbesparing. De kan i stället ge kapacitet för fler förändringar. Väntetid mellan team bör mätas separat från aktiv arbetstid. Vid en verklig investering bör även tidpunkten för utgifter, riskintervall och eventuella restvärden ingå i kalkylen.

## Säkerhet och handlingsfrihet som urvalsvillkor

I en reglerad organisation bör vissa krav fungera som urvalsvillkor snarare än som poäng i en sammanvägd jämförelse. Om ett alternativ inte kan uppfylla nödvändiga krav på åtkomstkontroll, återställning eller informationslivscykel är bättre frågeprestanda inte tillräckligt för att kompensera bristen.

Verifiera även vad en alternativ driftplats faktiskt kräver. Ett öppet fil- eller tabellformat kan underlätta en förflyttning men garanterar inte att bearbetningslogik, katalog, behörigheter eller driftförfaranden kan flyttas utan omfattande arbete. Dessa frågor fördjupas i kapitel 17 och 18.

## Behålla, komplettera eller ersätta

| Handlingsalternativ | När det är motiverat | Viktig kontroll |
|---|---|---|
| Vidareutveckla | Befintlig lösning klarar centrala arbetslaster; problemen ligger främst i anslutning, kapacitet eller arbetssätt | Att grundtekniken har rimlig återstående livslängd och stödjer nya krav |
| Komplettera | Nya arbetslaster har väsentligt andra krav, medan befintliga tjänster fortfarande fungerar väl | Att nyttan överstiger kostnaden för dubbla miljöer och samordning |
| Ersätta | Strukturella begränsningar kan inte åtgärdas rimligt, eller fortsatt drift innebär oacceptabel risk eller kostnad | Att ersättaren uppfyller befintliga och framtida krav och har en realistisk migreringsväg |

För referensmyndigheten är en viktig hypotes att långsam tillgång till nya data kan bero på specialistberoenden i informationsförsörjningen snarare än på datalagret. Om hypotesen stämmer kan en ny lagringsplattform lämna det ursprungliga problemet olöst. Om det befintliga datalagret däremot inte klarar nya arbetslaster bör komplettering eller ersättning prövas.

## Verifiera innan ett större vägval

Använd ett representativt urval av verkliga, tillåtna informationsmängder och arbetslaster. Jämför en rimligt moderniserad befintlig lösning med kandidaterna under likvärdiga villkor. Följ upp rapportkorrekthet, svarstid vid normal och hög samtidighet, tid från källändring till tillgänglig information, resursförbrukning, återställningstid och utvecklingsinsats för en ny informationsleverans. Testa även behörigheter och borttagning av data enligt de villkor som gäller för informationen.

Fastställ acceptansgränser innan testerna genomförs. För en verksamhetskritisk rapport kan reproducerbarhet vara ett absolut krav medan en experimentell analys kan tillåta större variation i svarstid. Jämför alternativ som levererar samma informationskvalitet och servicenivå, inte enbart samma datavolym. Mät också den återkommande arbetsinsatsen efter att pilotmiljön etablerats: en lyckad demonstration är inte detsamma som en förvaltningsbar tjänst.

Det mest motiverade lagringsvalet är det som uppfyller de faktiska kraven med rimlig långsiktig insats. Nästa del av boken behandlar hur informationen kan föras till och göras användbar i dessa miljöer, oberoende av vilken lagringsarkitektur organisationen väljer.
