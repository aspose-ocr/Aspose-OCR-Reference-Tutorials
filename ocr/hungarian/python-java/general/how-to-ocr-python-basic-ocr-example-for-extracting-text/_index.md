---
category: general
date: 2026-04-26
description: 'hogyan OCR Python: Tanulja meg a szöveg kinyerését képből és a TIFF
  fájl olvasását Pythonban egy egyszerű OCR példával. Gyors, futtatható kód mellékelve.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: hu
og_description: 'hogyan OCR Python: Lépésről‑lépésre útmutató, amely megmutatja, hogyan
  lehet szöveget kinyerni képből, TIFF‑fájlt olvasni Pythonban, és beolvasott képszöveget
  átalakítani egy egyszerű, futtatható szkripttel.'
og_title: hogyan OCR Pythonban – Alap OCR példa a szöveg kinyeréséhez
tags:
- OCR
- Python
- Image Processing
title: hogyan OCR Python – Alap OCR példa a szöveg kinyeréséhez
url: /hu/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Alap OCR példa szöveg kinyeréséhez

Valaha is elgondolkodtál **how to ocr python**-on, amikor egy beolvasott TIFF-ot találsz az asztalodon? Nem vagy egyedül, aki egy csomó képfájlra bámul és azt kérdezi: „Hogyan tudom kinyerni a szavakat ebből?” A jó hír, hogy egy képet egyszerű szöveggé alakítani egy könnyű feladat a megfelelő könyvtárral és néhány egyszerű lépéssel.

Ebben a bemutatóban egy **basic OCR example**-et fogunk végigjárni, amely beolvassa a TIFF fájlt, kinyeri a szöveget, és kiírja a konzolra. A végére pontosan tudni fogod, hogyan **extract text from image** fájlokból, hogyan kezeld a TIFF formátum sajátosságait, és mit kell finomhangolni, ha **convert scanned image text**-et szeretnél hasznosabb formába hozni. Nincs rejtett varázslat – csak egyszerű Python, amit ma másolhatsz‑beilleszthetsz és futtathatsz.

## Amire szükséged lesz

- Python 3.9+ telepítve (a legújabb stabil kiadás a legjobb).
- Egy pip‑installálható OCR könyvtár. Ebben az útmutatóban egy fiktív `aocr` csomagot használunk, amely a népszerű eszközökhöz, mint a Tesseract, hasonlít; később helyettesítheted `pytesseract`‑tal vagy `easyocr`‑ral.
- Egy TIFF kép, amelyet feldolgozni szeretnél – nevezd el `input.tiff`‑nek, és helyezd egy mappába, amelyre a kódban hivatkozol.
- Alapvető ismeretek a parancssorról (csak a csomag telepítéséhez).

Ennyi. Nincs nehéz függőség, nincs Docker konténer, csak néhány sor kód.

## 1. lépés – Függőségek telepítése és importálása (how to ocr python)

Először szerezd be az OCR csomagot. Nyiss egy terminált és futtasd:

```bash
pip install aocr
```

Ha egy valós könyvtárat szeretnél, cseréld le a `aocr`‑t `pytesseract`‑ra, és telepítsd külön a Tesseract motorját.

Most importáljuk, amire szükségünk van. A `Path` osztály a `pathlib`‑ből tiszta módot ad a fájlutak kezelésére különböző operációs rendszerek között.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Miért használjuk a `Path`‑t?* Mert elrejti a perjeleket (`/` vs `\`), és lehetővé teszi a könyvtárak összekapcsolását anélkül, hogy az alatta lévő OS‑től függnénk. Ez a kis részlet gyakran fejfájást spórol, amikor később a szkriptet CI szerverre helyezed.

## 2. lépés – OCR motor példány létrehozása (basic ocr example)

Most indítsuk el az OCR motort. Gondolj a `OcrEngine`‑re, mint az agyra, amely elolvassa a képet és karaktereket ad ki.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

A legtöbb OCR könyvtár lehetővé teszi a nyelv, DPI vagy a megbízhatósági küszöbök finomhangolását itt. Ehhez a **basic OCR example**‑hez az alapértelmezéseket használjuk, de később felfedezheted az `ocr_engine.config`‑ot, ha többnyelvű dokumentumokat kell kezelned.

## 3. lépés – TIFF kép betöltése (read tiff file python)

Itt jön a **read tiff file python** rész. A TIFF-ek lehetnek többoldalasak, de az `Image.load` alapértelmezés szerint az első oldalt tölti be – tökéletes egyoldalas beolvasáshoz.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Cseréld le a `"YOUR_DIRECTORY"`‑t arra a tényleges mappára, amelyik a `input.tiff`‑t tartalmazza. Ha nem vagy biztos benne, hogy a szkript hol fut, a `Path.cwd()` kiírja az aktuális munkakönyvtárat – hasznos a útvonalak hibakereséséhez.

## 4. lépés – OCR folyamat futtatása (extract text from image)

Most jön a varázslat. A `process()` meghívása átküldi a képet az OCR csővezetékén, és egy eredményobjektumot ad vissza.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

A háttérben a motor esetleg a képet szürkeárnyalatossá alakítja, küszöbölést alkalmaz, és egy neurális hálózatba táplálja. Nem kell ezeket a lépéseket kezelned; a könyvtár elrejti őket.

## 5. lépés – Felismert szöveg kiírása (convert scanned image text)

Végül, írd ki a szöveget. Valódi projektekben valószínűleg fájlba vagy adatbázisba írnád, de a kiírás tisztán tartja a példát.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

A szkript futtatásakor valami ilyesmit kell látnod:

```
Hello, world!
This is a sample scanned document.
```

Ha a kimenet összezavarodott, ellenőrizd, hogy a forráskép tiszta‑e, és hogy az OCR nyelv egyezik‑e a szöveggel.

## Teljes működő szkript

Összeállítva itt a teljes, azonnal futtatható program:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Várható kimenet

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Ha **convert scanned image text**‑et kereshető PDF‑be szeretnél átalakítani, a `ocr_result.text`‑et átirányíthatod egy PDF generátorba, például a `reportlab`‑ba – de ez egy önálló teljes tutorial.

## Gyakori buktatók és profi tippek

- **Alacsony felbontású beolvasások**: Az OCR nehezen működik 150 DPI alatt. Ha a TIFF elmosódott, először up‑sample‑eld a Pillow‑lal (`Image.open(...).resize(...)`).
- **Több oldal**: Többoldalas TIFF‑ek esetén iterálj a `Image.load_multi_page()`‑en (ha a könyvtárad támogatja) és fűzd össze az eredményeket.
- **Nyelvi támogatás**: Sok motor alapértelmezés szerint angolt használ. Állítsd be például `ocr_engine.language = "spa"` a spanyolhoz.
- **Üreshelyek kezelése**: Az OCR gyakran felesleges sortöréseket ad hozzá. Használd a `str.splitlines()`‑t vagy reguláris kifejezéseket a kimenet tisztításához.
- **Teljesítmény**: Tömeges feldolgozásnál használd újra ugyanazt az `OcrEngine` példányt, ahelyett, hogy minden fájlhoz újat hoznál létre.

## A példa kiterjesztése

Most, hogy elsajátítottad a **how to ocr python**‑t egyetlen képhez, fontold meg a következő lépéseket:

1. **Kötegelt feldolgozás** – Iterálj egy TIFF‑ek könyvtárán, és írd minden eredményt egy `.txt` fájlba.
2. **Integráció Pandas‑szal** – Tárold a kinyert szöveget metaadatokkal együtt a gyors elemzéshez.
3. **Hibrid megközelítés** – Kombináld az OCR‑t NLP könyvtárakkal, például `spaCy`‑val, hogy entitásokat (neveket, dátumokat, összegeket) nyerj ki beolvasott számlákból.
4. **Alternatív fájlformátumok** – Cseréld le az `Image.load`‑t `Image.from_bytes`‑re, hogy API‑ból vagy adatbázisból érkező képeket kezelj.

Mindez a **extract text from image** és a **convert scanned image text** alapötletére épül, hogy a gépek megértsék a beolvasott tartalmat.

## Következtetés

Áttekintettünk egy világos, vég‑ponttól‑végig **basic OCR example**‑et, amely megmutatja, hogyan **how to ocr python**, hogyan **read tiff file python**, és hogyan **extract text from image** fájlokból csak néhány sor kóddal. A szkript önálló, tartalmaz hibakezelést, és közvetlenül kiírja az eredményt, így szilárd alapot nyújt bármely projekthez, amely beolvasott dokumentumokat szerkeszthető szöveggé akar alakítani.

Nyugodtan kísérletezz – cseréld le az OCR backendet, finomítsd az előfeldolgozást, vagy csatlakoztasd a kimenetet egy downstream munkafolyamathoz. A lehetőségek határtalanok, ha megbízhatóan **convert scanned image text**‑et tudsz kereshető, kereshető adatokba alakítani.

Van kérdésed a szélsőséges esetekről, nyelvi csomagokról vagy a teljesítményhangolásról? Hagyj egy megjegyzést alább, és jó kódolást!

![hogyan OCR Python példája](/images/ocr-python-example.png "Képernyőkép a how to ocr python szkript kimenetéről")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}