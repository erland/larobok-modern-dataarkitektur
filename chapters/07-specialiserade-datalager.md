# 7. Specialiserade och kompletterande datalager

Ett gemensamt analytiskt datalager kan vara en god grund för myndighetens informationsförsörjning utan att vara den bästa tekniska lösningen för varje användningsområde. Att hitta ett dokument, följa en kedja av relationer mellan företag och beräkna antalet inkommande ärenden under de senaste minuterna är tre olika arbetslaster. De kan använda samma underliggande information men behöver inte använda samma lagrings- eller frågeteknik.

Stonebraker och Çetintemel argumenterade redan 2005 för att olika arbetslaster motiverar olika databasmotorer [K064]. Deras tes innebär inte att varje modernt användningsfall kräver en separat produkt. Specialisering är motiverad när en konkret egenskap inte kan uppnås tillräckligt väl i den befintliga miljön. Det kan handla om svarstid, aktualitet, informationsmodell eller isolering av belastning. Valet bör däremot inte utgå från att varje ny användning kräver en ny databasprodukt.

## Aktuella verksamhetsbilder och realtidsanalys

### Operational Data Store

Ett Operational Data Store (ODS) används här som beteckning för ett integrerat lager med relativt aktuell operativ information. Oracle beskriver ODS som ett lager för den dagliga verksamheten med begränsat historiskt djup [K065]. Till skillnad från ett historiskt analyslager är dess huvudsakliga uppgift att tillhandahålla en samlad bild av verksamhetens aktuella tillstånd. Det kan exempelvis sammanföra uppgifter om ett ärendes status, tillhörande dokument och pågående handläggningsaktiviteter från flera IT-stöd.

Ett ODS behöver inte vara en separat produktkategori. En relationsdatabas med en ändamålsenlig modell och kontrollerad uppdatering kan räcka. Det avgörande är att definiera vilken aktualitet och konsistens konsumenterna behöver. Uppgifter som överförs från olika system kan representera olika tidpunkter. Ett samlat lager innebär därför inte automatiskt en gemensam transaktionell ögonblicksbild.

Om en handläggare behöver ändra en uppgift måste arkitekturen dessutom klargöra vilket system som ansvarar för ändringen. En läsmodell bör inte utan ett uttryckligt beslut bli en alternativ källa för verksamhetens registreringar. Ett ODS kan vara lämpligt för att avlasta källsystemen och förenkla tvärgående uppslag, men bör inte införas om samma behov kan tillgodoses genom en befintlig tjänst.

### Realtidsanalys

Ett lager för realtidsanalys kan behöva hantera ett kontinuerligt inflöde av händelser samtidigt som många användare ställer aggregerande frågor. Exempel är att följa köbildning, förändringar i arbetsbelastning eller tekniska avvikelser. Här är kravet inte bara att en enskild fråga ska vara snabb, utan att informationen ska vara tillräckligt aktuell när svaret levereras.

Kolumnorienterade analysmotorer kan vara en relevant lösning för denna arbetslast. ClickHouse är ett exempel på en sådan databasmotor [K057]. En streamingmotor kan komplettera lagret genom att beräkna tidsfönster eller sammanställningar före lagring. Streamingbearbetning är dock inte detsamma som ett beständigt analyslager: behovet av att kunna fråga historiska resultat måste bedömas separat.

Organisationen bör prova kontinuerliga skrivningar och samtidiga frågor tillsammans. En lösning som är snabb vid en isolerad läsning kan fungera sämre när den samtidigt behöver ta emot förändringar, hantera sena händelser och återhämta sig efter avbrott. Begreppet realtid behöver därför konkretiseras som en tolererad fördröjning från källhändelse till användbart resultat.

HTAP, som introducerades i kapitel 2, är ett alternativ när analysen behöver ligga nära transaktionerna. Ett separat analyslager kan i stället vara motiverat när belastningen eller informationsmodellen behöver vara självständig. Dessa alternativ löser delvis samma behov, men med olika beroenden till den operativa miljön.

## Dokument och sökbar information

En dokumentdatabas representerar information i dokumentliknande strukturer, exempelvis JSON-liknande objekt med inbäddade fält och samlingar. Det kan vara lämpligt för informationsobjekt vars struktur varierar och där konsumenterna ofta behöver läsa objektet som en helhet. MongoDB:s modelleringsdokumentation illustrerar hur inbäddning kan användas för relaterade uppgifter [K058].

En dokumentdatabas ska skiljas från objektlagring av dokumentfiler och från ett sökindex. Ett PDF-dokument kan exempelvis bevaras i objektlagring, dess strukturerade metadata i en databas och den extraherade texten i ett sökindex. Dessa tre representationer fyller olika funktioner.

Ett sökindex organiserar information för återfinning. Vid fulltextsökning används ofta ett inverterat index, där termer kopplas till de dokument där de förekommer [K059]. Det möjliggör sökning som tar hänsyn till språklig bearbetning och relevans, inte bara exakt likhet mellan databasfält.

För referensmyndigheten kan ett index göra det möjligt att söka bland ärendehandlingar från flera IT-stöd. Indexet bör då betraktas som en härledd representation med definierad källa och uppdateringsprocess. En rättelse eller förändrad behörighet i källsystemet måste få genomslag även i sökningen. Organisationen behöver kunna kontrollera att träfflistor, textutdrag och aggregeringar inte röjer uppgifter som användaren saknar åtkomst till.

Det är ofta värdefullt att kunna återskapa indexet från dess källor. Det förutsätter att källinformationen finns kvar och att regler för textutvinning, indexering och behörighet kan reproduceras. Ett index som i praktiken innehåller den enda kopian av viss information får en annan roll och andra återställningskrav.

## Relationer som förstklassig information

I en grafdatabas representeras objekt och deras relationer direkt. En egenskapsgraf kan exempelvis innehålla noder för företag och ärenden, relationer mellan dessa samt egenskaper på noder och relationer [K060]. Detta kan vara användbart när frågorna handlar om vägar genom nätverk eller samband över flera led.

En graf är inte automatiskt bättre än en relationsmodell. Ett fåtal kända kopplingar kan ofta hanteras väl med SQL. Grafteknik blir särskilt intressant när relationernas struktur är central för analysen och frågornas djup eller mönster varierar. Även en graf som byggs tillfälligt för en analys kan vara tillräcklig; ett permanent graflager är ett separat beslut.

En kunskapsgraf tillför en mer uttrycklig beskrivning av betydelsen hos objekt och relationer. Begreppet är inte synonymt med grafdatabas: semantiken kan representeras med olika modeller och tekniker. För myndigheten är en viktig fråga hur identifierare, relationernas giltighetstid och uppgifternas ursprung hanteras. En härledd koppling får inte presenteras som en verifierad sakuppgift utan stöd.

## Vektorsökning och Feature Stores

En vektorrepresentation kan beskriva egenskaper hos exempelvis en text eller bild som en numerisk följd. Vid semantisk sökning jämförs sådana representationer för att hitta innehåll med liknande egenskaper. Likhet är dock inte en garanti för att innehållet är korrekt, relevant eller tillåtet att lämna ut.

Vektorsökning kan realiseras både i specialiserade databaser och genom tillägg till befintliga databasmotorer. PostgreSQL-tillägget pgvector illustrerar att en separat vektordatabas inte är en nödvändig förutsättning; det stöder både exakt och approximativ närmaste-granne-sökning [K061]. Approximativa index kan ge kortare svarstid på bekostnad av att vissa av de närmaste vektorerna missas [K061]. Mät därför både svarstid och återfinningsgrad (recall) mot exakt sökning med samma avståndsmått och filter. Semantisk relevans behöver dessutom bedömas separat.

Vid användning för generativ AI behöver vektorerna knytas till källdokument, dokumentversion, modellversion och åtkomstvillkor. Om modellen byts kan representationerna behöva räknas om. Vektorer och textsegment är härledda informationsmängder som omfattas av organisationens säkerhets- och livscykelbedömning. Vektorsökningens roll i AI-lösningar fördjupas i kapitel 19.

En Feature Store fyller ett annat behov: att tillhandahålla modellvariabler, så kallade features, för maskininlärning. En sådan förmåga kan stödja både historiska träningsunderlag och uppslag av aktuella värden vid modellkörning. Feast illustrerar denna uppdelning genom historiska datakällor och en online store [K062]. Vid träning måste informationen väljas så att den representerar vad som kunde vara känt vid den relevanta tidpunkten; annars kan framtida information läcka in i träningsunderlaget. Feast beskriver tidskorrekta kopplingar till historiska modellvariabler [K066]. För att även hantera sent registrerade uppgifter eller retroaktiva rättelser behöver organisationen säkerställa att uppgifternas faktiska tillgänglighetstid beaktas, inte enbart händelsetiden.

En Feature Store behöver inte innebära en ny permanent lagringsmotor. Befintliga analytiska lager och en snabb uppslagstjänst kan tillsammans realisera förmågan. Den är främst motiverad när återanvändning av modellvariabler, tidskorrekt historik och återkommande modellkörningar skapar ett verkligt samordningsbehov.

## Masterdata och referensinformation

Masterdata beskriver centrala verksamhetsobjekt, exempelvis organisationer och verksamhetsställen. Referensdata används för att klassificera eller tolka andra uppgifter, exempelvis landkoder och kodlistor [K063]. Båda kan behöva tillhandahållas gemensamt, men de är inte i första hand en viss databasteknik.

En gemensam masterdatatjänst kan vara motiverad när flera IT-stöd behöver samordnade identifierare, ansvar för rättelser och en gemensam publicering. En enkel förvaltad kodlista kan däremot räcka för vissa referensdata. Det viktiga är att fastställa vilken källa som har mandat att ändra informationen, hur versioner hanteras och hur konsumenter får del av ändringar. Ett analytiskt lager kan använda masterdata utan att därmed vara ansvarigt för deras operativa förvaltning.

## Erfarenheter av flera lagringstekniker

Vid HEPiX-workshopen i november 2025 beskrev CERN sina befintliga datatjänster, där bland annat Hadoop och OpenSearch ingick. Organisationen rapporterade samtidigt en pågående utvärdering av ClickHouse för analytiska arbetslaster med högt frågetryck och behov av nära realtid [K030]. Det är ett exempel på att en större organisation kan utvärdera kompletterande teknik för ett specifikt behov i stället för att förutsätta att alla arbetslaster ska flyttas till samma motor. Redogörelsen visar en utvärdering, inte att ClickHouse redan införts eller att en viss nytta har uppnåtts. CERN:s forskningsmiljö skiljer sig också från en svensk myndighets informationsmiljö.

## När är en ytterligare lagringslösning motiverad?

| Behov | Förmåga att pröva | Viktig verifiering |
|---|---|---|
| Samlad aktuell verksamhetsbild | ODS eller läsmodell | Aktualitet och ansvar |
| Täta analytiska frågor mot nya händelser | Realtidsanalyslager | Skriv- och frågebelastning tillsammans |
| Varierande objektstruktur | Dokumentmodell | Förändringar och konsistens |
| Sökning i text | Fulltextindex | Träffkvalitet och behörighet |
| Analys av komplexa samband | Grafbearbetning | Relationernas kvalitet och frågemönster |
| Semantisk likhetssökning | Vektorindex | Träffgrad, modellversion och åtkomst |
| Återanvändbara ML-variabler | Feature Store | Tidskorrekthet och aktualitet |
| Gemensamma identifierare och koder | Master- och referensdatatjänst | Ägarskap och giltighetstid |

Pröva först om en befintlig, förvaltad teknik kan realisera förmågan med tillräcklig kvalitet. Om den inte kan det bör en representativ arbetslast användas för att verifiera nyttan av en kompletterande lösning. Räkna då även med informationsöverföring, uppgraderingar, kompetens, återställning och kontroll av kopior. För en reglerad myndighet kan möjligheten att avveckla eller återskapa ett härlett lager vara lika viktig som dess prestanda.

Det är behovet av förmågan som behöver motiveras, inte en viss databasprodukt. En gemensam dataplattform kan erbjuda flera tekniker, men varje ytterligare teknik innebär ett långsiktigt åtagande. Kapitel 8 sammanför de viktigaste avvägningarna mellan de lagringsarkitekturer som nu har beskrivits.
