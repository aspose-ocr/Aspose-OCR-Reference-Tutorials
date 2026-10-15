---
category: general
date: 2026-01-12
description: Python OCR oktatóanyag, amely bemutatja, hogyan lehet táblázatszöveget
  kinyerni egy képből. Tanulja meg, hogyan olvassa be a táblázatot a képről, és hogyan
  nyerjen ki kiválasztott szöveget az Aspose OCR‑rel.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: hu
og_description: Python OCR oktatóanyag, amely megtanítja, hogyan lehet táblázatszöveget
  kinyerni egy képből, táblázatot olvasni a képből, és kiválasztott szöveget kinyerni
  az Aspose OCR segítségével.
og_title: 'Python OCR oktató: Táblázat szövegének kinyerése képekből'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python OCR útmutató: Táblázatszöveg kinyerése képekből'
url: /hu/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Bemutató: Táblázatszöveg Kinyerése Képekből

Valaha is szükséged volt egy **python ocr tutorial**-ra, amely valóban megmutatja, hogyan lehet egy táblázatot kihúzni egy beolvasott űrlapról? Nem vagy egyedül. A legtöbb bemutató csak az általános szövegkinyerésnél áll meg, és arra hagy, hogy kitaláld, hogyan izoláld azt a rendezett adatrácsot, amelyre szükséged van.  

Ebben az útmutatóban egy valós példán keresztül vezetünk végig: egy táblázat olvasása egy képről, csak a szükséges szöveg kinyerése, majd a végeredmény kiírása. Útközben tippeket adunk a **how to extract table** adatok megbízható kinyeréséhez, így nem kell minden alkalommal újra feltalálni a kereket.

## Mit Tanulhatsz

- Hogyan állítsd be az Aspose OCR-t Pythonhoz.
- Hogyan definiálj egy téglalap alakú régiót, amely táblázatot tartalmaz.
- A pontos lépések a **extract table text** és **read table from image**.
- Tippek többnyelvű vagy szabálytalan táblázat elrendezések kezeléséhez.
- Egy teljes, futtatható szkript, amelyet azonnal beilleszthetsz a projektedbe.

**Előfeltételek**  
- Python 3.8 vagy újabb.  
- Alapvető ismeretek az OCR koncepciókról (mély szakértelem nem szükséges).  
- Egy PNG vagy JPEG kép, amely egyértelmű táblázatot tartalmaz (ezt `form_with_table.png`-nek hívjuk).

Ha megvannak ezek, merüljünk el—nincs felesleges részlet, csak gyakorlati kód.

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr tutorial példa a táblázat régió megjelenítésére"}

## 1. lépés: Aspose OCR telepítése és importálása

Először is: szükséged van az Aspose OCR könyvtárra. A csomag a PyPI-n elérhető, így egyetlen `pip` parancs elég.

```bash
pip install aspose-ocr
```

Most importáld a modult és a szükséges segédfüggvényeket.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tipp:* Tartsd a függőségeket egy `requirements.txt` fájlban. Ez könnyűvé teszi a környezet reprodukálását.

## 2. lépés: OCR motor inicializálása (Python OCR Bemutató Core)

A motor létrehozása bármely **python ocr tutorial** szíve. Itt beállítjuk az alapértelmezett nyelvet angolra—később nyugodtan cserélheted.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Miért állítod be a nyelvet? Az OCR pontossága drámaian javulhat, ha a motor tudja, milyen karakterekre számíthat. Ha többnyelvű űrlapokkal dolgozol, beállíthatsz egy nyelvlistát, vagy régiónként felülírhatod (lásd később).

## 3. lépés: Kép betöltése

Az Aspose OCR a legtöbb általános képformátummal működik. Csak add meg a fájl elérési útját, és kapsz egy `Image` objektumot, amely készen áll a feldolgozásra.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Különleges eset:* Nagy képek (5 MB felett) lelassíthatják a feldolgozást. Fontold meg a méretezést vagy tömörítést OCR előtt, ha a teljesítmény problémát jelent.

## 4. lépés: A táblázat régió meghatározása (Read Table from Image)

Most jön a szórakoztató rész: megmondani a motornak, *hol* található a táblázat. Egy `OcrRegion`-t adsz meg egy `Rectangle`-lel (x, y, szélesség, magasság). A koordináták pixel‑alapúak, így egy kicsit kísérletezni kell.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Miért használj régiót? Az OCR korlátozásával a táblázat területére **extract selected text** gyorsabban történik, és elkerülhető a környező címkék vagy grafikák zajja. Emellett javítja a pontosságot, mivel a motor egy egységes elrendezésre tud fókuszálni.

## 5. lépés: OCR futtatása a meghatározott régióban

A régió beállítása után meghívjuk a `process_region`-t. A metódus egy `OcrResult` objektumot ad vissza, amely a nyers szöveget, a megbízhatósági pontszámokat és akár a keretmezőket is tartalmazza, ha később szükséged van rájuk.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Ha több táblázatot kell kinyerni, egyszerűen ismételd meg a 4‑5. lépéseket különböző téglalapokkal.

## 6. lépés: Kinyert táblázatszöveg kiírása

Végül írd ki—vagy tárold— a táblázat szöveges ábrázolását. Az Aspose OCR egyszerű szöveget ad vissza sortörésekkel, amelyek általában a sorokhoz igazodnak, így az utófeldolgozás egyszerű.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Várható kimenet** (példa):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Most ezt a karakterláncot átadhatod `csv` elemzőknek, pandas DataFrame-eknek vagy bármely további analitikai folyamatnak.

## Teljes Működő Példa

Mindent összevonva, itt a teljes szkript, amelyet azonnal futtathatsz. Cseréld le a `YOUR_DIRECTORY/form_with_table.png`-t a kép tényleges elérési útjára.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Futtasd a szkriptet a `python extract_table.py` paranccsal. Ha minden rendben van, a táblázat megjelenik a konzolon.

## Gyakori Kérdések és Különleges Esetek Kezelése

**Mi van, ha a táblázat nem tökéletesen téglalap alakú?**  
Feloszthatod a táblázatot több átfedő régióra, vagy használhatsz egy nagyobb téglalapot, amely az egész területet lefedi, majd utófeldolgozod a szöveget (pl. sorokra bontás).

**Kinyerhetek csak bizonyos oszlopokat?**  
A teljes táblázatszöveg után használhatod a Python `csv` vagy `pandas` modulját, hogy kivágd a kívánt oszlopokat. Az OCR lépés maga minden adatot visszaad a téglalapon belül.

**Hogyan dolgozhatok nem angol táblázatokkal?**  
Állítsd be az `ocr_engine.language`-t (vagy a `region.language`-t) a megfelelő enumra, például `ocr.Language.FRENCH`, vagy kombinálj több nyelvet az `ocr.Language.ENGLISH | ocr.Language.SPANISH` használatával.

**Van mód arra, hogy minden cellához kapjak határoló keretet?**  
Az Aspose OCR vissza tud adni `region_result.words`-t, ahol minden szó tartalmaz egy határoló keretet. Ezeket a kereteket vissza kell térképezni egy rácshoz—hasznos fejlett elrendezés-elemzéshez.

## Tippek a Pontosság Javításához

- **Tisztítsd meg a képet**: Binarizáld vagy növeld a kontrasztot, mielőtt OCR-nek adnád. Olyan könyvtárak, mint a Pillow segíthetnek.
- **Kerüld a tömörítési hibákat**: Amikor csak lehetséges, mentsd a beolvasásokat PNG formátumban.
- **Figyelj a DPI-re**: 300 dpi az ideális; alacsonyabb értékek elmaradt karaktereket eredményezhetnek.
- **Tesztelj különböző téglalap méreteket**: Kissé nagyobb téglalapok gyakran elkapják a táblázathoz tartozó elszórt karaktereket.

## Következő Lépések

Miután elsajátítottad a **how to extract table** adatokat az Aspose OCR-rel, érdemes lehet felfedezni:

- A kinyert szöveg CSV fájlba konvertálása a Python `csv` moduljával.
- Az adatok betáplálása egy **pandas** DataFrame-be elemzéshez.
- OCR használata kézírásos űrlapok olvasásához (másik motor vagy további tréning szükséges).
- Több tucat beolvasott űrlap kötegelt feldolgozásának automatizálása egy egyszerű `for` ciklussal.

Ezek a kiterjesztések mind az ebben a **python ocr tutorial**-ban lefedett alapvető koncepciókra épülnek, így jól fel vagy készülve a skálázásra.

---

*Boldog kódolást! Ha bármilyen problémába ütközöl, írj egy megjegyzést alább—szívesen segítek a kinyerés finomhangolásában.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}