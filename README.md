# Hvervningsbarometeret

Live-side der viser, hvor stor en del af sit eget hvervningsmål hver SFU-lokalafdeling har nået.

**Kun FU kan ændre stillingen.** Afdelingerne kan kun se siden.

---

## Sådan lægger du det på GitHub

### 1. Opret et repository

1. Log ind på [github.com](https://github.com) (opret en gratis konto, hvis du ikke har en)
2. Klik **+** øverst til højre → **New repository**
3. **Repository name:** `hvervningsbarometer`
4. Vælg **Public** — GitHub Pages kræver et offentligt repo på en gratis konto
5. Sæt ikke flueben i noget andet. Klik **Create repository**

### 2. Læg filerne op

1. På repositoriets forside: **Add file → Upload files**
2. Træk `index.html`, `data.csv` og `README.md` ind
3. Klik **Commit changes**

### 3. Slå GitHub Pages til

1. **Settings** (øverst i repoet) → **Pages** (i menuen til venstre)
2. Under **Source** vælg **Deploy from a branch**
3. **Branch:** `main` · **Folder:** `/ (root)` → **Save**
4. Vent 1–2 minutter, opdatér siden. Linket står øverst:

```
https://DIT-BRUGERNAVN.github.io/hvervningsbarometer/
```

Det link sender du til afdelingerne.

---

## Sådan opdaterer du stillingen

### Den enkle måde: ret `data.csv` i GitHub

1. Åbn `data.csv` i repoet
2. Klik blyantsikonet (**Edit this file**) oppe til højre
3. Ret tallene
4. **Commit changes** nederst

Siden er opdateret efter ca. et minut. Det er alt.

Filen ser sådan her ud — tre kolonner, én linje pr. afdeling:

```csv
Afdeling,Mål,Nye
København,39,12
Aarhus,27,0
Viborg,6,0
```

- **Afdeling** — navnet, som det skal stå på siden
- **Mål** — afdelingens egen ambition: antal nye medlemmer inden 1. april
- **Nye** — hvor mange de har hvervet indtil nu

Rækkefølgen er ligegyldig; siden sorterer selv efter målopfyldelse.

### Alternativet: styr tallene fra et Google Sheet

Hvis du hellere vil rette i et regneark end i GitHub:

1. Lav et **nyt, separat** Google Sheet med de samme tre kolonner
2. **Filer → Del → Udgiv på nettet** → vælg fanen → format **Kommasepareret værdi (.csv)** → **Udgiv**
3. Kopiér linket. Det ender på `output=csv`
4. Åbn `index.html`, find linjen nær toppen af scriptet og sæt linket ind:

```js
var SHEET_CSV_URL = "";      // ← her
```

Siden henter så nye tal automatisk hvert 5. minut, og der er en **Hent nye tal**-knap.

---

## Sikkerhed — læs den her

**Repoet er offentligt.** Alt hvad du lægger i det, kan alle læse. Læg derfor aldrig
medlemslister, telefonnumre, mailadresser, restancelister eller ringearket i dette repo.
Kun de tre kolonner: afdelingsnavn, mål, antal nye.

**Siden er offentlig for alle med linket.** Der er ingen adgangskode. Det er i orden,
fordi indholdet kun er afdelingsnavne og procenter — men det er værd at vide, før I
deler linket bredt.

**Bruger du Google Sheets: lav et separat regneark.** Det udgivne CSV-link står i
sidens kildekode og kan læses af alle. Udgiver du en fane fra det samme dokument, hvor
ringearket eller medlemslisten ligger, kan andre faner i det dokument blive læsbare.
Hold barometeret i sit eget dokument.

**"Udgiv på nettet" er ikke det samme som at dele arket.** Det gør kun en
skrivebeskyttet kopi af tallene læsbar. Redigeringsadgang har kun dem, du selv
deler dokumentet med — så lad være med at give andre redigeringsret.

**Kun du kan ændre stillingen**, fordi kun du har skriveadgang til repoet
(og eventuelt til regnearket). Vil du give en anden fra FU adgang:
**Settings → Collaborators → Add people**. Giv aldrig adgang til hele LL.

**Der er ingen hemmeligheder i koden.** Ingen adgangskoder, ingen nøgler, ingen
sporing af brugere. Siden henter kun én CSV-fil og tegner den.

---

## Tilpasninger

Alt ligger i `index.html`.

- **Præmietrappen** — variablen `LADDER` nær toppen af scriptet. Ret procenter og tekster.
- **Opdateringsfrekvens** — `OPDATER_HVERT_MINUT`. Sæt til `0` for at slå automatisk hentning fra.
- **Reservetal** — `FALLBACK`. Vises kun, hvis `data.csv` ikke kan hentes, så siden aldrig står tom foran en afdeling.
- **Farver** — samlet i `:root` øverst i stylesheetet.

---

## Hvis noget ikke virker

**Siden er tom, eller der står "Kunne ikke hente tallene"** — tjek at `data.csv`
ligger i samme mappe som `index.html`, og at den første linje hedder
`Afdeling,Mål,Nye`. Åbn browserens konsol (F12) for at se den præcise fejl.

**Ændringer slår ikke igennem** — GitHub Pages er cirka et minut om at bygge.
Bruger du Google Sheets, cacher Google det udgivne CSV i op til fem minutter.
Prøv en hård genindlæsning (Ctrl+Shift+R / Cmd+Shift+R).

**404 på linket** — tjek under Settings → Pages at branch er `main` og mappe er
`/ (root)`, og at filen hedder præcis `index.html` med småt.

**Forkerte tal** — tjek at der ikke er tomme linjer eller ekstra kommaer i `data.csv`.
Afdelingsnavne med komma i skal stå i anførselstegn: `"Roskilde, Lejre",9,0`
