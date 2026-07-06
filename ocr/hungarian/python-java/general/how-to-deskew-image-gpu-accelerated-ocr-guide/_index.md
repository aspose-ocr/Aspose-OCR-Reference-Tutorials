---
category: general
date: 2026-01-02
description: Tanulja meg, hogyan korrigálja a kép ferdeségét és növelje a kép kontrasztját,
  hogy gyorsan nyers szöveget kapjon. Tartalmaz lépésről‑lépésre Python kódot és tippeket
  a szöveg kinyeréséhez.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: hu
og_description: Hogyan korrigáljuk a kép ferdeségét és növeljük a kontrasztot a tiszta
  szöveg eléréséhez. Teljes Python példa táblázatkinyeréssel és GPU gyorsítással.
og_title: Hogyan kiegyenesítsünk képet – Teljes GPU OCR útmutató
tags:
- OCR
- Python
- Image Processing
title: Képek kiegyenesítése – GPU-gyorsított OCR útmutató
url: /hu/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését – GPU‑gyorsított OCR útmutató

Valaha is elgondolkodtál **how to deskew image**-en, amikor a nyugtáid furcsa szögben érkeznek? Nem vagy egyedül; egy ferde fénykép tökéletesen olvasható nyugtát is összegabalyodott káossá változtathat. A jó hír, hogy néhány Python sorral automatikusan korrigálhatod a dőlést, növelheted a kontrasztot, és tiszta egyszerű szöveget nyerhetsz ki – manuális Photoshop nélkül.  

Ebben a tutorialban egy teljes, futtatható példán keresztül mutatjuk be, hogy nem csak **how to deskew image**, hanem **how to boost contrast**, **how to get plain text**, és még **how to extract text** is működik a táblázatokból, amelyeket az OCR motor felismer. A végére egy önálló szkriptet kapsz, amelyet bármelyik projektbe beilleszthetsz.

## Amire szükséged lesz

- Python 3.9+ telepítve (a kód típusjelöléseket használ, így egy friss interpreter segít)
- Az `ocr` könyvtár, amely biztosítja az `OcrEngine`, `EngineMode`, `ImageProcessingOptions` és `OcrResult` osztályokat (telepítsd a `pip install ocr‑sdk` paranccsal – cseréld le a tényleges csomagnévre)
- GPU kompatibilis illesztőprogramokkal, ha a sebességjavulást szeretnéd (opcionális, de ajánlott)
- Egy kép, amely enyhén el van forgatva vagy alacsony kontrasztú, pl. `receipt_skewed.jpg`

> **Pro tipp:** Ha nincs GPU-d, egyszerűen cseréld le a `EngineMode.GPU`-t `EngineMode.CPU`-ra, és a szkript továbbra is működik – csak egy kicsit lassabban.

## Lépésről‑lépésre megvalósítás

Alább a megoldást logikai egységekre bontjuk. Minden egységnek van egy leíró **H2** címe, amely vagy a fő kulcsszót *how to deskew image*, vagy valamelyik másodlagos kulcsszót tartalmazza. A kód teljes, kommentált és futtatható.

### Hogyan korrigáljuk a kép dőlését GPU‑gyorsított OCR-rel

Az első lépésben azt mondjuk az OCR motornak, hogy a GPU-n fusson, és engedélyezzük az automatikus dőléskorrekciót. Az auto‑deskew elemzi a kép geometriáját, és visszaforgatja függőleges állapotba.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Miért fontos:** A GPU gyorsítás csökkentheti a feldolgozási időt másodpercek helyett ezrekre, ami kulcsfontosságú, ha percenként tucatnyi nyugtát kell kezelni.

### Növeld a kép kontrasztját a jobb felismerésért

Az alacsony kontrasztú nyugta rémálom minden OCR rendszer számára. A kontraszt növelésével tisztább éleket biztosítunk a motor számára.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Hogyan növeld a kontrasztot:** A `set_contrast_boost` metódus százalékot vár; a 30 % egy biztonságos alapértelmezés, amely a legtöbb beolvasott nyugtán működik. Ha a képeid nagyon sötétek, emeld 50 %-ra vagy kísérletezz.

### Szerezz egyszerű szöveget a feldolgozott képből

Most, hogy a kép egyenes és világos, betápláljuk a motorba, és kérjük az egyszerű szöveg eredményt.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Várható kimenet** (rövidítve):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Hogyan szerezz egyszerű szöveget:** A `get_text()` metódus eltávolít minden elrendezési információt, és tiszta karakterláncot ad vissza, amelyet aztán adatbázisba menthetsz, API‑nak küldhetsz, vagy downstream elemzésekhez használhatsz.

### Hogyan nyerjünk ki szöveget a felismert táblákból

Gyakran a nyugták táblázatos adatokat tartalmaznak (tételek, mennyiségek, árak). Az OCR SDK képes táblázatokat felismerni, és lehetővé teszi a sorok és cellák iterálását.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Minta táblázat kimenet**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Miért érdemes táblákat kinyerni:** A strukturált adatok egyszerűvé teszik az összegek kiszámítását, jelentések generálását, vagy könyvelő szoftverbe való betáplálást.

### Teljes működő szkript

Mindent összevonva, itt a szkript, amelyet beilleszthetsz a `deskew_and_ocr.py` fájlba:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Futtasd a következővel:

```bash
python deskew_and_ocr.py
```

A konzolon meg kell jelennie a megtisztított szövegnek és az esetlegesen felismert tábláknak.

## Gyakori szélhelyzetek és megoldások

| Szituáció | Mit tegyünk |
|-----------|------------|
| **A kép fejjel lefelé van** | Növeld a `set_auto_deskew(True)` biztonságát azzal, hogy hívod a `set_rotation_correction(True)`-t, ha az SDK ezt támogatja. |
| **A kontraszt növelése túl fényessé teszi a képet** | Csökkentsd a `set_contrast_boost`-nak átadott százalékot (pl. 15 %). |
| **GPU nem elérhető** | Cseréld le a `EngineMode.GPU`-t `EngineMode.CPU`-ra; a pipeline többi része változatlan marad. |
| **A táblázatok kimaradnak** | Próbálj nagyobb felbontású beolvasást, vagy engedélyezd a `set_table_detection(True)`-t, ha a könyvtár ezt biztosítja. |

## Következő lépések: Az egyszerű szövegből strukturált adatok

Most, hogy tudod **how to deskew image**, **how to boost contrast**, és **how to get plain text**, érdemes lehet:

- Az egyszerű szöveget reguláris kifejezésekkel feldolgozni, hogy kulcs‑érték párokat nyerj ki (pl. `total`, `date`).
- Az eredményeket SQLite vagy PostgreSQL adatbázisban tárolni későbbi jelentéskészítéshez.
- A szkriptet serverless funkcióba (AWS Lambda, Azure Functions) integrálni, hogy a feltöltéseket automatikusan feldolgozza.

Mindezek a kiterjesztések ugyanazon az alapon nyugszanak, amelyet itt bemutattunk.

## Következtetés

Áttekintettük, hogyan kell **how to deskew image** egy GPU‑gyorsított OCR motorral, bemutattuk, **how to boost contrast** a jobb felismerésért, megmutattuk pontosan, **how to get plain text**, és még **how to extract text** táblázatokból is. A teljes, futtatható szkript mindent összekapcsol, így beillesztheted bármelyik Python projektbe, és azonnal tiszta adatokat nyerhetsz ki ferde, alacsony kontrasztú fényképekből.

Próbáld ki néhány saját nyugtáddal, állítsd be a kontrasztot, és hagyd, hogy az OCR végezze a nehéz munkát. Ha valami furcsaságot észlelsz, nézd meg a fenti szélhelyzet‑táblázatot – a legtöbb probléma csak egy apró beállítással orvosolható.

Boldog kódolást, és legyenek a képeid mindig egyenesek és fényesek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}