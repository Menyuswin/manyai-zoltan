# Mányai Zoltán — bemutatkozó oldal

Egyoldalas, statikus bemutatkozó weboldal: szakmai pálya, szakterületek,
tanulmányok és a saját kisebb webes produktumok (keresztrejtvény,
időjárás-ügyelet, névnapnaptár) egy helyen.

Nincs build-lépés, nincs függőség: sima HTML + CSS, a fotó külön fájlként
mellékelve.

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
