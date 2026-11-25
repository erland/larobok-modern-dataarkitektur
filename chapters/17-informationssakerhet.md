# 17. Informationssäkerhet, regulatoriska krav och informationslivscykel

När information från flera operativa IT-stöd samlas för analys uppstår nya möjligheter men också nya risker. Uppgifter som var för sig innebär begränsad risk kan tillsammans avslöja exempelvis en persons rörelsemönster eller en myndighets kontrollmetoder. En säker dataarkitektur måste därför utgå från både informationen och den behandling som möjliggörs.

## Från rättsliga krav till arkitekturbeslut

För en svensk myndighet behöver rättsliga förutsättningar bedömas för varje behandling och informationsutbyte. Dataskyddsförordningen (GDPR) ställer bland annat krav på rättslig grund, ändamålsbegränsning, uppgiftsminimering, lagringsminimering och säkerhet vid behandling av personuppgifter. Artiklarna 5, 6, 25 och 32 är särskilt relevanta för arkitekturen [K020]. En teknisk möjlighet att kombinera data innebär inte att kombinationen är tillåten. Vid behandling som omfattas av GDPR och sannolikt medför hög risk för enskildas rättigheter och friheter krävs som huvudregel en konsekvensbedömning före behandlingen enligt artikel 35. För behöriga myndigheters behandling för brottsbekämpande ändamål kan i stället brottsdatalagen och kompletterande registerförfattningar vara tillämpliga [K088]. Det är behandlingens ändamål och tillämpligt regelverk, inte valet av dataplattform, som avgör vilka krav som gäller.

Offentlighets- och sekretesslagen reglerar bland annat utlämnande av sekretessbelagda uppgifter mellan myndigheter och mellan självständiga verksamhetsgrenar inom en myndighet (8 kap. 1–2 §§) [K085]. En gemensam dataplattform upphäver inte dessa gränser. Samtidigt behöver myndigheten kunna hantera rätten att ta del av allmänna handlingar. Intern åtkomststyrning och prövning av utlämnande är olika processer. En elektronisk sammanställning kan omfattas av handlingsoffentligheten om den kan tas fram med rutinbetonade åtgärder, med de begränsningar som följer av 2 kap. 6–7 §§ tryckfrihetsförordningen [K089].

Arkivlagen och tillämpliga föreskrifter reglerar arkivvård, bevarande och gallring [K086] [K021]. Särskilda registerförfattningar och andra verksamhetsspecifika regler kan påverka vilka uppgifter som får behandlas och hur länge de får finnas kvar. Vilket regelverk som gäller måste bedömas i sitt sammanhang. Kapitlets rättsliga utgångspunkter avser november 2026; exemplen är arkitekturbedömningar, inte rättsliga ställningstaganden i enskilda ärenden.

## Informationsklassning och skyddsgränser

Informationsklassning behöver omfatta konfidentialitet, riktighet och tillgänglighet. En informationsmängds skyddsbehov kan förändras när den bearbetas, kombineras eller görs tillgänglig för en ny grupp användare. Klassningen bör därför omprövas vid publicering av förädlade dataprodukter och vid förändrade användningsändamål.

En gemensam fysisk lagringsmiljö kan innehålla flera logiskt separerade informationsområden, förutsatt att isoleringen motsvarar kraven. För vissa uppgifter kan starkare separation behövas, exempelvis egna exekveringsmiljöer, administrativa behörighetsgränser eller separat nyckelhantering. Beslutet bör utgå från konsekvensen av ett fel eller en komprometterad komponent, inte enbart från vilket lagringsformat som används.

## Åtkomst, maskering och kryptering

Åtkomst bör ges till den informationsmängd och den behandling som mottagaren behöver. Rollbaserad åtkomststyrning kan kompletteras med attributbaserade regler som beaktar exempelvis informationsklass, organisatorisk tillhörighet och beslutat användningsändamål. Ett angivet ändamål i en teknisk förfrågan är dock inte i sig ett bevis på att behandlingen är tillåten.

| Kontroll | Arkitekturmässig tillämpning |
|---|---|
| Identitet och behörighet | Individuella identiteter för användare och arbetslaster, minsta nödvändiga behörighet och regelbunden omprövning. |
| Rad- och kolumnbegränsning | Begränsa vilka poster och attribut som får läsas genom kontrollerade åtkomstvägar. |
| Maskering och pseudonymisering | Minska exponeringen av direkt identifierande uppgifter där analysbehovet tillåter det. |
| Kryptering | Skydda data under överföring och lagring, med kontrollerad nyckelhantering. |
| Exportkontroll | Hantera nedladdningar, vidarepublicering och åtkomst från externa verktyg. |

Pseudonymiserade personuppgifter omfattas fortfarande av GDPR när de kan hänföras till en person med hjälp av ytterligare information. Anonymisering kräver en bedömning av identifieringsmöjligheterna, även vid kombination med andra uppgifter [K020]. Kryptering skyddar inte heller mot alla risker: en behörig eller komprometterad frågemotor kan fortfarande läsa klartext.

En central åtkomstpolicy är bara verksam om samtliga relevanta åtkomstvägar omfattas. Om en användare kan läsa underliggande filer direkt kan säkerhetsregler i frågemotorn kringgås. Det behöver verifieras även för administrativa verktyg, tjänsteidentiteter, säkerhetskopior och integrationsflöden.

## Säkerhetsloggning och revisionsspår

Som arkitekturmål bör myndigheten kunna utreda vem eller vilken arbetslast som har läst, förändrat eller lämnat ut information, när det skedde och vilket åtkomstbeslut som tillämpades. Vilka händelser som måste loggas, hur detaljerade de ska vara och hur länge de ska sparas behöver bestämmas utifrån risk och tillämpliga regler.

Ett revisionsspår bör kunna koppla samman identitet, informationsobjekt, operation och tidpunkt. För distribuerade flöden kan gemensamma korrelationsidentifierare underlätta utredning. Lineage från kapitel 16 kompletterar säkerhetsloggar men ersätter dem inte: en registrerad bearbetningsrelation visar inte nödvändigtvis vem som tog del av resultatet.

Loggar behöver själva skyddas. Frågetexter, felmeddelanden och sökparametrar kan innehålla personuppgifter eller sekretessbelagd information. Begränsa därför loggarnas informationsinnehåll, åtkomst och lagringstid och skydda dem mot obehörig förändring.

## Bevarande, gallring och informationskopior

Arkivlagens utgångspunkt är bevarande av myndigheternas arkiv för bland annat offentlighetsprincipen, förvaltningens och rättskipningens informationsbehov och forskning. Gallring regleras bland annat i 10 § [K086]. GDPR:s lagringsminimering behöver bedömas tillsammans med tillämpliga bevarandekrav och undantag, bland annat för arkivändamål av allmänt intresse. Rätten till radering är inte ovillkorlig (artiklarna 5, 17 och 89) [K020].

Riksarkivets RA-FS 2009:1 omfattar bland annat planering, dokumentation och skydd av elektroniska handlingar; ändringsföreskriften RA-FS 2024:3 ändrar bland annat 6 kap. 1 och 7 §§ [K021] [K087]. Föreskrifternas tillämpningsområde och eventuella undantag behöver beaktas. En långsiktigt läsbar handling kräver mer än att dess bitar finns kvar. Struktur, definitioner, samband och relevant dokumentation behöver bevaras så att informationen kan förstås och användas.

Alla tekniska kopior har inte samma rättsliga status. En handling som förvaras enbart för att kunna återskapa förlorad information i myndighetens ordinarie system är enligt 2 kap. 13 § tryckfrihetsförordningen inte en allmän handling [K089]. Den tekniska livscykeln behöver ändå omfatta även mottagningszoner, härledda tabeller, index, snapshots, temporära filer och säkerhetskopior. Att ta bort en rad ur en aktuell Lakehouse-tabell behöver exempelvis inte innebära att uppgiften försvinner ur äldre snapshots. En gallringsprocess måste därför ha kontroll över kvarvarande versioner och de regler som styr deras bevarande. Efter återställning från en säkerhetskopia behöver tidigare genomförda gallrings- och rättelseåtgärder kunna tillämpas på nytt när tillämpliga regler kräver det.

## Konsekvenser för lagrings- och åtkomstarkitekturer

| Arkitekturmönster | Särskilt kontrollbehov |
|---|---|
| Data Warehouse | Behörighet till integrerade informationsmängder och härledda rapporter samt historiska versioner. |
| Data Lake | Klassning och åtkomst även för råfiler, ostrukturerad information och direkta lagringsgränssnitt. |
| Lakehouse | Samordnad behörighet mellan frågemotorer, kataloger och objektlagring samt kontroll över snapshots och metadata. |
| Federerad åtkomst | Enhetliga åtkomstbeslut över källor, hantering av kombinerade resultat och återkallande av behörighet. |
| Specialiserade datalager | Kontroll över härledda sökindex, vektorer, cachar och modellvariabler samt deras uppdatering och avveckling. |

Ingen av arkitekturerna är i sig förenlig eller oförenlig med regelverket. Bedömningen behöver göras av den konkreta realiseringen och informationsbehandlingen.

## Gemensamma kontrollförmågor i praktiken

I den fiktiva referensmyndigheten kan systemteam publicera informationsleveranser inom förutbestämda ramar. Plattformen kan kräva klassning, utsedd ansvarig, dokumenterade bevarandevillkor och godkända åtkomstvägar innan en leverans aktiveras. Kontrollerna bör vara automatiserade där reglerna är entydiga. En ny kombination av sekretesskänsliga data eller ett nytt behandlingsändamål kan däremot kräva en särskild bedömning före aktivering av leveransen.

Kritiska förmågor är att identifiera och begränsa åtkomst, skydda information, följa upp säkerhetshändelser, hantera livscykeln och återställa information under kontrollerade former. Mer avancerade funktioner som automatiserad klassningsassistans och dynamisk maskering kan vara värdefulla när behovet motiverar dem. Det avgörande är kontrollernas faktiska täckning, inte antalet säkerhetsprodukter.

Uppföljningen bör exempelvis omfatta andelen publicerade informationsmängder med dokumenterade skydds- och livscykelvillkor, tiden för att återkalla behörighet, täckningen hos revisionsspåren och resultat av återställnings- och gallringstester. Därmed blir säkerhetsförmågan en verifierbar del av dataplattformens tjänsteerbjudande.
