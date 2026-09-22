# Mányai Zoltán — bemutatkozó oldal

Statikus bemutatkozó weboldal: a főoldal (szakmai pálya röviden, szakterületek,
tanulmányok és a saját kisebb webes produktumok — keresztrejtvény,
időjárás-ügyelet, Kalendárium), plusz egy önálló, saját kanonikus URL-lel
rendelkező aloldal a teljes pályafutás-idővonalnak.

Nincs build-lépés, nincs függőség: sima HTML + megosztott CSS, a fotó külön
fájlként mellékelve.

A jobb oldali sávban futó "Sajtófigyelés" widget kliensoldali JavaScripttel,
oldalbetöltéskor kérdezi le 6 hírportál (Index, Telex, HVG, 444, 24.hu,
Portfolio) RSS-csatornáját a rss2json.com ingyenes, kulcs nélküli
proxyján keresztül (a böngészők CORS-korlátozása miatt közvetlenül nem
olvashatók), és 30 percig gyorsítótárazza az eredményt a böngésző
localStorage-ában.

## Megnyitás

```bash
python3 -m http.server 8000
```

Ezután: <http://localhost:8000>

A `file://` megnyitás is működik.

## Szerkezet

- `index.html` — a főoldal tartalma
- `style.css` — a két oldal (főoldal + Pályafutás) közös stíluslapja
- `palyafutas/index.html` — a Pályafutás önálló, saját canonical taggel
  ellátott aloldala (a teljes idővonal)
- `photo.jpg` — profilfotó
- `header.jpg` — teljes szélességű fejléc-banner ("Dialogus aperit portas")

## Produktumok

Az oldal a "Produktumok" szekcióban a szerző saját projektjeire linkel,
amelyek külön repóban élnek és GitHub Pages-en futnak:

- [Angol szókincs keresztrejtvény](https://github.com/Menyuswin/angol-keresztrejtveny)
- [Menyusweather](https://github.com/Menyuswin/Menyusweather)
- [Kalendárium](https://github.com/Menyuswin/nevnapnaptar)
