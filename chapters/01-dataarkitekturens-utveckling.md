# 1. Dataarkitekturens utveckling och drivkrafter

En dataarkitektur formas av vilka frågor verksamheten behöver kunna besvara och av hur informationen uppstår. När en myndighet behöver sammanställa föregående års verksamhetsresultat ser kraven annorlunda ut än när den vill prioritera dagens kontrollinsatser eller utveckla ett AI-stöd som kan hitta relevanta uppgifter i dokument. De tre behoven kan existera samtidigt, även om de har uppstått vid olika tidpunkter.

Dataarkitekturens utveckling kan därför förstås som en successiv breddning av vad organisationer vill kunna göra med sin information. Nya arkitekturmönster har vuxit fram för att hantera begränsningar i tidigare lösningar. Samtidigt har de ursprungliga behoven inte försvunnit.

## Från samlad rapportering till bredare dataanvändning

### Den gemensamma bilden av verksamheten

När verksamhetsprocesser digitaliseras uppstår information i de system som stödjer dem. Ett ärendehanteringssystem registrerar exempelvis beslut och handläggningstider, medan ett ekonomisystem registrerar betalningar. Att följa upp verksamheten över systemgränser kräver att uppgifterna kan sammanställas och jämföras.

Data Warehouse blev ett etablerat sätt att tillgodose sådana behov: information från olika källor integreras för analys och rapportering [K033]. Den gemensamma informationsmodellen har ett värde som går utöver själva lagringen. Om två avdelningar definierar ett avslutat ärende på olika sätt behöver skillnaden hanteras innan deras resultat kan jämföras på ett meningsfullt sätt.

En väl fungerande rapporteringslösning kan alltså vara en betydande tillgång. Det är viktigt att skilja detta värde från eventuella begränsningar i den teknik eller de arbetssätt som används för att upprätthålla lösningen.

### Fler former av information och nya frågor

Behovet av att analysera exempelvis loggar, dokument, bilder och stora mängder händelsedata breddade kraven på analytisk lagring. För vissa användningar är det inte heller möjligt att på förhand bestämma vilka delar av informationen som kommer att behövas. Data Lake växte fram som ett sätt att hantera större variation i data och ge utrymme för utforskande bearbetning. En litteraturöversikt av Azzabi, Alfughi och Ouda från 2024 beskriver hur flera olika arkitekturer för Data Lake har utvecklats och hur deras utformning har förändrats över tid [K033].

För en myndighet kan den nya möjligheten vara att analysera texten i inkomna dokument tillsammans med strukturerade ärendeuppgifter. Att lagra dokumenten på ett sätt som möjliggör analys är dock bara en del av uppgiften. Det behöver också vara möjligt att förstå dokumentens sammanhang, identifiera vilken version som är relevant och avgöra om informationen får användas för ändamålet.

### Ambitionen att förena arbetslaster

När ett Data Lake och ett Data Warehouse används parallellt kan en organisation behöva underhålla flera representationer av samma information. I den artikel som presenterades vid CIDR 2021 argumenterar Armbrust med flera för Lakehouse som ett alternativ till en sådan tvådelad arkitektur. Ambitionen är att förena traditionell analys med maskininlärning och annan avancerad bearbetning på en gemensam lagringsgrund [K001].

Artikeln är ett viktigt bidrag till förståelsen av konceptet, men dess författare har koppling till Databricks och argumenterar för en viss teknisk inriktning. Deras förutsägelse om att den dåvarande Data Warehouse-arkitekturen skulle ersättas bör inte förväxlas med en oberoende jämförande utvärdering av alla moderna alternativ.

Arkitekturfrågan är om en gemensam lagringsgrund verkligen förenklar organisationens samlade lösning. Färre fysiska kopior kan vara värdefullt, men behovet av olika informationsmodeller, kvalitetskontroller och åtkomstvillkor kvarstår. Att flera arbetslaster kan hanteras med samma teknik innebär inte att de alltid bör använda samma tekniska instans.

## Drivkrafter som förändrar arkitekturkraven

Utvecklingen kan inte förklaras enbart med ökande datavolymer. Även en organisation med relativt begränsade datamängder kan behöva förändra sin arkitektur. Följande drivkrafter är särskilt användbara för att analysera behovet av en förflyttning.

| Drivkraft | Exempel på förändrat behov | Arkitekturfråga |
|---|---|---|
| Aktualitet | Riskbedömning under pågående ärende | Hur snabbt måste förändringar bli tillgängliga? |
| Informationsvariation | Analys av dokument och strukturerade uppgifter tillsammans | Vilka datatyper och bearbetningsformer behövs? |
| Skalbarhet | Fler samtidiga analyser och periodvis hög belastning | Hur kan kapaciteten anpassas utan att övriga arbetslaster störs? |
| Förändringstakt | Nya informationsbehov vid förändrade verksamhetsprocesser | Hur lång tid tar det att publicera användbar data? |
| AI och avancerad analys | Träning av modeller eller informationshämtning till AI-stöd | Vilka informationsrepresentationer och kvalitetskrav tillkommer? |
| Återanvändning | Samma informationsunderlag behövs av flera verksamhetsområden | Hur undviks onödigt dubbelarbete utan att kontrollen går förlorad? |

Tabellen är ett analysverktyg, inte en prognos om att alla behov kommer att öka i alla organisationer. Aktualitet är exempelvis inte ett självändamål. En månadsrapport kan ha större nytta av en stabil, kvalitetssäkrad periodavgränsning än av kontinuerliga uppdateringar.

### Förändringsförmåga och självbetjäning

Anta att referensmyndighetens systemteam inför ett nytt attribut. Även en liten ändring kan kräva samordning mellan källsystem, överföringsflöde, mottagningszon (stage area) och analytisk modell. Om denna samordning orsakar lång väntan är det förändringsförmågan snarare än lagringskapaciteten som begränsar verksamheten. Kapitel 9 följer detta exempel genom informationskedjan och kapitel 12 behandlar självbetjäning.

Gieß och Hutterer jämför moderna datahanteringskoncept utifrån bland annat styrning och decentralisering [K008]. Översikten ger en begreppslig grund för sådana vägval, inte belägg för att en viss ansvarsfördelning alltid förkortar ledtiderna.

### AI som ytterligare användningsområde

Ett AI-stöd kan behöva andra data än en rapport. Ett stöd som hämtar information ur myndighetens styrande dokument behöver exempelvis tillgång till relevanta textavsnitt och uppgifter om dokumentens giltighet. En modell som ska hjälpa till att prioritera kontroller kan i stället behöva historiska observationer och tillförlitliga uppgifter om utfall.

Båda exemplen ställer krav på dataarkitekturen, men på olika sätt. Det finns därför ingen grund för att enbart utifrån ett allmänt AI-behov besluta att organisationens datalager måste ersättas. Börja med den tänkta användningen och identifiera vilken information, kvalitet, aktualitet och bearbetning som behövs. Kapitel 19 fördjupar dessa skillnader.

## Varför teknik inte räcker

Den brittiska revisionsmyndigheten National Audit Office (NAO) publicerade 2019 en granskning av förutsättningarna för att använda data inom statsförvaltningen. Granskningen uppmärksammade bland annat bristande långsiktigt strategiskt ledarskap och att myndigheter inte prioriterat arbetet med att förbättra sina data tillräckligt [K014]. Det är en dokumenterad erfarenhet från en viss offentlig förvaltning, inte en aktuell mätning av svenska myndigheters förmåga.

För en IT-arkitekt är lärdomen att förbättrad teknisk kapacitet inte automatiskt medför bättre information. Om ett källsystem registrerar uppgifter på ett sätt som inte stödjer den avsedda analysen kan en snabbare frågemotor leverera ett otillräckligt underlag snabbare. Om ansvaret för att rätta problemet är oklart kan ytterligare integrationsflöden i stället göra det svårare att identifiera var bristen uppstår.

En reglerad organisation behöver dessutom kunna skilja mellan vad som är tekniskt möjligt och vad som är tillåtet och lämpligt. Att information kan sammanföras betyder inte att den får användas för varje tänkbart ändamål. Krav på skydd, spårbarhet och informationslivscykel är därmed förutsättningar för arkitekturen, inte frågor som kan skjutas upp tills tekniken är vald.

## Samexistens och behovsdriven modernisering

Nya arkitekturmönster behöver inte ersätta äldre enligt en given ordning. Kapitel 8 jämför lagringsalternativen och kapitel 20 visar hur de kan kombineras.

En behovsdriven förflyttning börjar därför med ett observerbart problem och en önskad effekt. Teknikvalet är en följd av den analysen. För att avgöra vilka tekniska egenskaper som faktiskt behövs är nästa steg att förstå skillnaden mellan den datahantering som stödjer den operativa verksamheten och den som stödjer analys.
