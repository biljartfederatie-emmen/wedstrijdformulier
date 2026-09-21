# Wedstrijdformulier Generator (biljart)

Open `wedstrijdformulier.html` in Edge, Chrome, Safari of Firefox. Er is geen installatie of server nodig.
Werkt op pc, tablet en mobiel. Alles wordt automatisch in de browser opgeslagen (localStorage).

## Werkwijze
1. **Spelers**: de app heeft een ingebouwde lijst van biljartpoint.nl (Klasse A en B) met teamnummers,
   bijvoorbeeld De Schalm 1 t/m 4. De teamindeling komt uit de gespeelde partijen: vaste speler = speelde daar
   de meeste partijen, reserve = viel daar in. Wie nog niet gespeeld heeft, staat onder "<club> (geen team)" en is
   alleen als invaller te vinden.
   **Online (GitHub Pages):** elke nacht worden de moyennes gecontroleerd. Zijn ze gewijzigd, dan verschijnt bovenaan
   de app een gele balk *Nieuwe moyennes* met de knop **Bijwerken** (en *Bekijk wijzigingen*). Tcar van nog niet
   gespeelde partijen op het open formulier wordt dan ook bijgewerkt. Een link met `?bijwerken` erachter werkt meteen bij.
   **Lokaal bestand:** `python spelers_ophalen.py` → Spelers → *Importeer .xlsx / .csv* → `Spelers_biljartpoint.xlsx`.
   Importeren kan ook met een eigen .xlsx of .csv met de kolommen `Teamnaam, Bondsnr, Naam, Temaken, Moy` (optioneel `Reserve`).
2. **Formulier**: kies het thuis- en uitteam. Typ daarna in het naamvak een deel van de naam of het bondsnummer
   (bijv. `jan v`, `hols` of `10019`). Kies de speler met een klik, of met ↑/↓ en Enter.
   Bondsnummer en Tcar (te maken caramboles) worden dan automatisch ingevuld.
   De lijst toont alleen spelers van het gekozen team (eerst vaste spelers, dan reserves).
   **Invaller uit een ander team?** Klik onderaan de lijst op *➕ Invaller uit ander team zoeken* (of druk op Enter
   als er niets gevonden is). Dan wordt in alle teams gezocht, met de teamnaam erbij.
   Een naam die helemaal niet in de lijst staat, blijft staan als invaller; Bondsnr en Tcar vul je dan zelf in.
3. **Live scoreblad**: per partij voer je de serie per beurt in. Gcar, beurten en hoogste serie
   komen daarna automatisch op het formulier.
4. **Handtekeningen**: de aanvoerders tekenen in het vak met hun vinger, een pen of de muis.
5. **Afdrukken / export**:
   - 2 exemplaren op 1 A4 (thuisteam + federatie/uitteam, met knipstreep)
   - of 2 exemplaren op aparte A4's
   - scoreblad (8 partijen, 2 pagina's)
   - PDF (formulier + scoreblad)
   - Excel (.xlsx) in dezelfde opmaak als het originele Wedstrijdformulier.xlsx:
     tabblad *Formulier* (2 exemplaren op 1 A4, punten als formules) en *Scoreblad* (4 partijen per A4),
     plus *Beurten* (alle series) en *Spelers*. De afdrukinstellingen staan al goed.
6. **Opslaan** zet de wedstrijd in het *Archief*. Van daaruit kun je hem later openen of als back-up (.json) exporteren.

## Puntentelling (overgenomen uit MpPlayer1/MpPlayer2)
Thuisspeler rij *n* speelt tegen uitspeler rij *n*. Verschil = Gcar − Tcar.

| Situatie | Punten |
|---|---|
| Groter verschil én doel gehaald | 3 |
| Gelijk verschil én doel gehaald | 2 |
| Groter verschil, doel niet gehaald | 2 |
| Gelijk verschil, doel niet gehaald | 1 |
| Kleiner verschil, wel doel gehaald | 1 |
| Anders | 0 |

De punten worden pas berekend als bij beide spelers Gcar is ingevuld (0 telt ook als ingevuld).

## Online zetten met dagelijkse moyenne-controle (GitHub Pages)
Eenmalig, ongeveer 10 minuten. Daarna draait alles vanzelf en gratis.

1. Maak een gratis account op <https://github.com> (als je dat nog niet hebt).
2. Klik rechtsboven op **+ → New repository**. Naam bijv. `wedstrijdformulier`, kies **Public**, klik **Create repository**.
3. Klik op **uploading an existing file** en sleep deze bestanden/mappen uit de map erin:
   `wedstrijdformulier.html`, `index.html`, `spelers.json`, `spelers_ophalen.py`, `LEESMIJ.md`, `.gitignore`
   en de map **`.github`** (met daarin `workflows/moyennes.yml`). Klik **Commit changes**.
   *Niet* uploaden: `Wedstrijdformulier.xlsx` en `Spelers_biljartpoint.xlsx`.
4. Ga naar **Settings → Pages** en kies bij *Source*: **GitHub Actions**.
5. Ga naar het tabblad **Actions** → *Moyennes bijwerken en publiceren* → **Run workflow**.
   Na ± 2 minuten staat de app op `https://<jouw-gebruikersnaam>.github.io/wedstrijdformulier/`.
6. Deel die link met de aanvoerders (bijv. in de app-groep). Tip: op telefoon/tablet via *Toevoegen aan beginscherm*.

Elke nacht om ± 06:00 haalt GitHub de moyennes op. Alleen als er iets veranderd is, wordt `spelers.json`
vernieuwd en zien gebruikers de melding. Handmatig controleren kan in de app via Spelers → *Moyennes controleren*,
of op GitHub via Actions → *Run workflow*. Andere competities toevoegen: pas in `moyennes.yml` de regel
`python spelers_ophalen.py --alleen-json` aan, bijv. `python spelers_ophalen.py 9830 9831 9900 --alleen-json`.
