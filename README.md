# Mányai Zoltán — bemutatkozó oldal

Egyoldalas, statikus bemutatkozó weboldal: szakmai pálya, szakterületek,
tanulmányok és a saját kisebb webes produktumok (keresztrejtvény,
időjárás-ügyelet, névnapnaptár) egy helyen.

Nincs build-lépés, nincs függőség: sima HTML + CSS, a fotó külön fájlként
mellékelve.

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

- `index.html` — az oldal teljes tartalma és stílusa
- `photo.jpg` — profilfotó

## Produktumok

Az oldal a "Produktumok" szekcióban a szerző saját projektjeire linkel,
amelyek külön repóban élnek és GitHub Pages-en futnak:

- [Angol szókincs keresztrejtvény](https://github.com/Menyuswin/angol-keresztrejtveny)
- [Menyusweather](https://github.com/Menyuswin/Menyusweather)
- [Névnapnaptár](https://github.com/Menyuswin/nevnapnaptar)
