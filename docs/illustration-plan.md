# Illustrationsplan

Användaren har godkänt den balanserade varianten (nio inre SVG-illustrationer). Designsystem: [illustration-design.md](illustration-design.md). Integrerade i kapitel i steg 8.7. Bildtexten används även som beskrivande alt-text av befintlig exportpipeline; de utförligare alt-texterna nedan bevaras som redaktionellt underlag.

| Bild-ID | Kapitel | Syfte | Metod | Källa | Renderad fil | Status |
|---|---|---|---|---|---|---|
| IMG-02-01 | 2 | Operativ och analytisk datahantering | SVG | assets/diagrams/IMG-02-01.svg | assets/generated/IMG-02-01.svg | integrerad, intern granskning |
| IMG-03-01 | 3 | Dataarkitekturens fem dimensioner | SVG | assets/diagrams/IMG-03-01.svg | assets/generated/IMG-03-01.svg | integrerad, intern granskning |
| IMG-04-01 | 4 | Logisk Data Warehouse-arkitektur | SVG | assets/diagrams/IMG-04-01.svg | assets/generated/IMG-04-01.svg | integrerad, intern granskning |
| IMG-05-01 | 5 | Logisk Data Lake-arkitektur | SVG | assets/diagrams/IMG-05-01.svg | assets/generated/IMG-05-01.svg | integrerad, intern granskning |
| IMG-06-01 | 6 | Logisk Lakehouse-arkitektur | SVG | assets/diagrams/IMG-06-01.svg | assets/generated/IMG-06-01.svg | integrerad, intern granskning |
| IMG-09-01 | 9 | Tre alternativa leveranskedjor | SVG | assets/diagrams/IMG-09-01.svg | assets/generated/IMG-09-01.svg | integrerad, intern granskning |
| IMG-12-01 | 12 | Dataplattformens tjänsteerbjudande | SVG | assets/diagrams/IMG-12-01.svg | assets/generated/IMG-12-01.svg | integrerad, intern granskning |
| IMG-19-01 | 19 | Informationsförsörjning till analys och AI | SVG | assets/diagrams/IMG-19-01.svg | assets/generated/IMG-19-01.svg | integrerad, intern granskning |
| IMG-20-01 | 20 | Kombinerad referensarkitektur | SVG | assets/diagrams/IMG-20-01.svg | assets/generated/IMG-20-01.svg | integrerad, intern granskning |

## Bildtexter och alt-texter

### IMG-04-01

Bildtext: Logisk Data Warehouse-arkitektur där källinformation integreras och historiseras för återanvändning i konsumtionsanpassade modeller. Nivåerna behöver inte vara separata produkter.

Alt-text: Ärende- och ekonomisystem levererar till mottagning och transformation. Information förs vidare till integrerat datalager, Data Marts och analytisk bearbetning för rapportering och analys. Styrning omfattar alla nivåer.

Placering: efter tabellen under Datalagrets logiska struktur.

### IMG-05-01

Bildtext: Logisk Data Lake-arkitektur med gemensam fil- eller objektlagring, exempel på informationszoner och separat bearbetning. Zonindelningen är inte obligatorisk; motorer kan nyttja olika zoner och material beroende på behörighet och behov.

Alt-text: Operativa IT-stöd, dokument och filer tas emot och kontrolleras. Gemensam lagring rymmer källnära, förädlade och konsumtionsanpassade zoner; bearbetnings- och frågemotorer använder zonerna för analys och maskininlärning. Styrning omfattar alla nivåer.

Placering: efter tabellen under Informationszoner.

### IMG-06-01

Bildtext: Logisk Lakehouse-arkitektur där kompatibla motorer använder förvaltade tabeller med metadata och versioner över gemensam lagring. Inläsningens pil avser skrivning via kompatibla motorer, inte direkt skrivning förbi tabellprotokollet. Dokument kan också bevaras som filer utan att bli tabeller. Dubbelriktade pilar visar logisk åtkomst och resultat eller läsning och skrivning där det stöds.

Alt-text: Operativa källor och filer förs via kontrollerad inläsning till gemensam lagring. Tabellformat och katalog möjliggör versionshanterade tabeller som kompatibla fråge- och bearbetningsmotorer använder för BI och avancerad analys. Styrning omfattar alla nivåer.

Placering: efter tabellen under Från filer till förvaltade tabeller.

### IMG-02-01

Bildtext: Exempel på separerad operativ och analytisk datahantering. Parallella motriktade pilar visar transaktioner och svar respektive frågor och resultat. Den analytiska miljön försörjs med information från den operativa miljön. Graden av isolering väljs efter verksamhetskraven; läsrepliker och HTAP kan vara alternativa lösningar.

Alt-text: Ett operativt IT-stöd använder ett operativt datalager. Information förs via informationsförsörjning till ett analytiskt datalager som används för analys och rapportering. Isolering bedöms utifrån resurskonkurrens, felpåverkan, behörighet, aktualitet och historik.

Placering: efter avsnittet Varför arbetslaster behöver isoleras, före CERN-exemplet.

### IMG-03-01

Bildtext: Fem samverkande arkitekturdimensioner enligt bokens analysramverk. Plattformar samt organisation och ansvar berör de övriga dimensionerna. Grupperingen visar inte en obligatorisk teknisk lagerarkitektur eller sekvens.

Alt-text: Informationsförsörjning, lagring och bearbetning samt tillgängliggörande och konsumtion visas som tre jämställda områden. Gemensamma plattformsförmågor samt organisation och ansvar visas som två tvärgående områden.

Placering: efter avsnittet Fem dimensioner av dataarkitekturen, före Centralisering är inte ett enda vägval.

### IMG-09-01

Bildtext: Tre alternativa leveranskedjor till samma typ av mottagningszon, med exempel på ansvar vid en förändring. Självbetjäning förutsätter en godkänd källa, stödd anslutning och uppfyllda publiceringsvillkor. Batch eller händelser avgör inte i sig förändringsledtiden; dataprodukter kan byggas ovanpå alla tre alternativen. Analytisk bearbetning efter mottagning ingår inte i bilden.

Alt-text: Tre parallella kedjor visar specialistutvecklad ETL, individuell händelseintegration via outbox och meddelandeplattform samt deklarativ självbetjäning genom konfigurerad anslutning och gemensam exekvering. Alla når en mottagningszon. Under varje kedja anges vilket team som ändrar leveransen.

Placering: efter tabellen under Jämför hela leveranskedjan.

### IMG-12-01

Bildtext: Ett logiskt dataplattformserbjudande med självbetjänade gränssnitt, dataspecifika funktioner och återanvändning av gemensamma IT-tjänster. Streckade pilar visar tjänstenyttjande, inte informationsflöden. Gränsdragningen är ett exempel; AI-plattformens tjänster nyttjas vid behov. Erbjudandet behöver inte motsvara en enda produkt eller driftplats.

Alt-text: Systemteam, analysteam och informationskonsumenter använder självbetjänade gränssnitt för publicering, förädling och konsumtion. Dataplattformen samlar informationsförsörjning, lagring, bearbetning och åtkomst med tvärgående kontroll och drift. Den återanvänder utvecklings-, integrations-, infrastruktur-, säkerhets- och AI-tjänster.

Placering: efter avsnittet Ett sammanhängande tjänsteerbjudande, före Orkestrering och gemensam exekvering.

### IMG-19-01

Bildtext: Fyra exempel på informationsflöden till analys och AI. Historisk analys använder en historisk dataprodukt; assistenten kombinerar sökindex och behörighetskontrollerat aktuellt uppslag. Agenten skiljer läsning från åtgärder via operativt funktionsgränssnitt; de motriktade pilarna avser åtgärdsanrop och resultat/status. Vid osäkert utfall behövs statuskontroll och kontrollerad felhantering. Den specialiserade AI-tjänsten får avgränsad indata och lämnar resultat till IT-stödets granskningsflöde. Pilar visar logisk informationsriktning, inte fullständiga protokoll. Behörighetskontroller gäller även sökindexets innehåll före återvinning till modellen.

Alt-text: Fyra parallella exempel. A: operativt IT-stöd via historisk dataprodukt och analysmodell till rapport. B: styrdokument via sökindex och aktuellt ärende via kontrollerat uppslag till AI-assistent och källhänvisat svar. C: kontrollerad läsning till agent och separat åtgärdsväg genom mandatkontroll och operativt funktionsgränssnitt. D: vald handling till dokumenttolkning och resultat till ärendets granskningsflöde.

Placering: efter tabellen under Informationsflöden i fyra verksamhetsnära tillämpningar.

### IMG-20-01

Bildtext: Exempel på en kombinerad målarkitektur för referensmyndigheten. Heldragna uppåtriktade pilar visar logiska informationsflöden. Lakehouse är en möjlig avgränsad prövning, inte ett krav; streckad kontur markerar denna avgränsning. Direktåtkomst visar förfrågan och svar utan obligatorisk mellanlagring. Gemensamma tjänster och styrning visas som tvärgående band, inte som ytterligare steg i informationsflödet. Källor och konsumenter kan återanvändas mellan kedjorna; placeringen anger inte separata driftplatser.

Alt-text: Fyra parallella informationskedjor från källor via leveranser till Data Warehouse för BI, specialiserad läsmodell för riskanalys, dokumentindex för AI-assistent och ett möjligt Lakehouse för utforskande analys och modellträning. En separat dubbelriktad väg ger konsumenten aktuell ärendestatus via ett kontrollerat gränssnitt. Gemensamma tjänster och styrning omfattar arkitekturen.

Placering: efter stycket om Lakehouse-prövning under Informationsflöden och nödvändiga plattformstjänster, före resonemanget om avbrott.

## Omslag

- ID: COVER-01
- Fil: `assets/cover/cover.png` (1024 × 1536 px, original-PNG).
- Metod: AI-genererat omslag, valt och uttryckligen godkänt av användaren.
- Motiv: mörk teal, isometriska sammankopplade block på diskret rutnät. Titel, undertitel och författare.
- Status: godkänt, konfigurerat i `book.yaml`; faktisk PDF-/EPUB-inbäddning och proportioner återstår att kontrollera.
