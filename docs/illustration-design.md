# Grafiskt designsystem – steg 8.2

Godkänd inriktning: nio professionella, vektorbaserade arkitekturbilder. Logiska arkitekturer, informell notation, inga produktlogotyper, skuggor, gradienter eller 3D-effekter. Vitt bildfält; bildrubrik och bildtext utanför SVG i bokflödet.

| Roll | Kontur/textaccent | Fyllning |
|---|---|---|
| Operativa IT-stöd och källor | #334155 | #F1F5F9 |
| Informationsförsörjning | #0E7490 | #ECFEFF |
| Lagring och bearbetning | #2563EB | #EFF6FF |
| Konsumtion | #7C3AED | #F5F3FF |
| Plattformstjänster | #0F766E | #F0FDFA |
| Styrning och kontroll | #B45309 | #FFFBEB |

Normal bildyta 1200 × 800, marginal ca 40 enheter, riktvärde för layoutgrid 8 enheter, hörnradie 8, konturer och flödeslinjer 2. Noto Sans med DejaVu Sans/sans-serif som reserv. Rubriker 26–30, sekundär text minst 22. Anpassa exakt placering efter etiketter och pilarnas fria utrymme. Funktion ska framgå även utan färg genom etiketter och gruppering. Inga externa beroenden eller skript.

## Notation

Avrundad rektangel för logisk funktion, tjänst eller system; cylinder när en särskild lagringsinstans behöver markeras; gränssnitt med portmarkering; streckad inramning för logisk gruppering. Plattformstjänster kan visas som gemensamt band. Heldragen enkel pil för informationsflöde; två motriktade pilar eller dubbelriktad pil för läsning/skrivning respektive förfrågan/svar (förklara i bildtext). Streckad pil för tjänsteberoende, prickad linje för styrning. Styrningsfält utan pilar betyder tvärgående krav, inte ett separat informationsflöde.

## Layoutmönster

A: horisontella logiska nivåer med källor nederst och konsumtion överst. B: informationsflöde från vänster till höger. C: jämförande alternativ med gemensam nivåindelning. Kapitel 4–6 använder A med samma fem nivåer och styrningsfält. Nivåer är pedagogiska avgränsningar och behöver inte motsvara separata produkter. Exempel är inte uttömmande; faktiska möjligheter överlappar.

## Kvalitetsgrind

Sakgranska mot kapitlet, kontrollera SVG via projektets render_diagrams.py, rendera för visuell kontroll, kontrollera läsbarhet vid sidbredd och i gråskala. Bevara kanonisk SVG i assets/diagrams och verifierad kopia i assets/generated. Bildtext och alt-text i registret. Kapitelintegration och verkliga PDF-/EPUB-kontroller genomförs i senare steg; inga exportresultat påstås före dessa.
