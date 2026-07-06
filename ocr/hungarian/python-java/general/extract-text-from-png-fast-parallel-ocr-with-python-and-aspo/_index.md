---
category: general
date: 2026-03-28
description: Gyorsan nyerjen ki szöveget PNG‑ből az Aspose OCR Python használatával.
  Tanulja meg, hogyan konvertálja a beolvasott oldalak szövegét párhuzamos képfelismeréssel
  Pythonban a nagy teljesítményű eredményekért.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: hu
og_description: Szöveg gyors kinyerése PNG-ből az Aspose OCR Pythonban. Ez az útmutató
  bemutatja, hogyan konvertálhatók a beolvasott oldalak szövegei párhuzamos képfelismeréssel
  Pythonban, magas sebességű eredményeket biztosítva.
og_title: Szöveg kinyerése PNG-ből – Gyors párhuzamos OCR Pythonban
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Szöveg kinyerése PNG-ből – Gyors párhuzamos OCR Python és Aspose segítségével
url: /hu/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG‑ből szöveg kinyerése – Gyors párhuzamos OCR Pythonban

Valaha is **szöveget kellett kinyerni PNG** fájlokból, de a egy‑szálas OCR fájdalmasan lassú volt? Nem vagy egyedül. Akár egy csomó beolvasott nyugtát digitalizálsz, akár előadási diákból kereshető PDF‑et szeretnél készíteni, a szűk keresztmetszet általában maga az OCR lépés.  

Ebben a bemutatóban egy teljes, azonnal futtatható megoldást mutatunk be, amely **párhuzamosan konvertálja a beolvasott oldalak szövegét**, az Aspose OCR aszinkron kötegelt módját kombinálva a Python `ThreadPoolExecutor`‑jével. A végére **image text python**‑stílusban fogod tudni felismerni a képek szövegét, tizedekben kevesebb idő alatt, mint egy naív ciklus.

> **Mit fogsz megtanulni**  
> * Egy teljesen működő szkriptet, amely PNG képekből szöveget nyer ki egyszerre.  
> * Megértést arról, hogy miért gyorsít fel az async batch mód.  
> * Tippeket a megoldás nagyobb munkaterhelésekre való skálázásához.

## Szükséges előkészületek

| Előfeltétel | Indoklás |
|--------------|----------|
| Python 3.9+ | Modern szintaxis és típusjelölések. |
| `aspose-ocr` és `aspose-storage` csomagok | Az OCR motor és a képbetöltő biztosítása. |
| Egy PNG fájlokból álló mappa (pl. beolvasott oldalak) | A feldolgozni kívánt forrásanyag. |
| Alapvető ismeretek a Python párhuzamosságról | Hasznos, de nem kötelező; mindent elmagyarázunk. |

Az Aspose könyvtárak telepítéséhez használd:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tipp:** Tartsd naprakészen a csomagjaidat (`pip list --outdated`), hogy a legújabb teljesítményjavulásokat élvezd.

## 1. lépés: Az Aspose OCR motor inicializálása async batch módban

Az első lépés egy `OcrEngine` példány létrehozása, majd **asynchronous batch mode**‑ra állítása. Ez a mód belső sorba állítja a felismerési kéréseket, lehetővé téve a motor számára, hogy több képet dolgozzon fel anélkül, hogy a Python szálad blokkolódna.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Miért async?*  
Szinkron módban a `recognize` hívás addig blokkol, amíg a kép teljesen feldolgozásra nem kerül. Async módban a motor már a következő képre is tud dolgozni, míg az előző még dekódolódik, így az I/O és a CPU munka átfedésben zajlik.

## 2. lépés: A feldolgozni kívánt PNG fájlok listázása

Itt definiáljuk a képek gyűjteményét. Egy valódi projektben ezt dinamikusan generálhatod (pl. `glob.glob("*.png")`), de az explicit lista könnyebben követhetővé teszi a példát.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Megjegyzés:** Cseréld le a `YOUR_DIRECTORY`‑t arra az útvonalra, ahol a PNG beolvasásaid találhatók. Ha több száz fájlod van, fontold meg az `os.listdir` használatát és a `.png` szűrést.

## 3. lépés: Segédfüggvény írása, amely betölti a képet és visszaadja a szöveget

A segédfüggvény elrejti a **Aspose Storage**‑on keresztül történő fájlbetöltés és az OCR motorhoz való átadás kétlépéses folyamatát. Egy rövid docstring hozzáadása önmagát dokumentálóvá teszi a függvényt – hasznos a jövőbeni karbantartáshoz.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Miért külön függvény?*  
Tisztábbá teszi a thread‑pool kódot, és lehetővé teszi a logika újrahasználatát (pl. egy Flask végponton). Emellett az I/O elkülönítése könnyebbé teszi a hibakeresést – ha egy adott fájl hibát okoz, a kivétel nyomkövetésében megjelenik a fájlnév.

## 4. lépés: Párhuzamos képfelismerés Pythonban Thread Pool használatával

Most jön a `ThreadPoolExecutor`. Alapértelmezés szerint négy munkavállalót indítunk, de a `max_workers` értéket a CPU magok száma és a képkészlet mérete alapján finomhangolhatod.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Hogyan biztosít ez párhuzamos képfelismerést Pythonban

* **ThreadPoolExecutor** egy munkavállaló szálakból álló medencét hoz létre, amelyek mindegyike meghívja a `recognize_image`‑t.  
* Mivel az OCR motor async batch módban van, minden szál át tudja adni a munkát a motor számára, miközben továbbra is reagál.  
* Az `as_completed` a jövőket a befejezésük sorrendjében adja vissza, így az eredményeket azonnal megkapod – tökéletes nagy kötegek streameléséhez.

> **Gyakori hibaforrás:** `max_workers=1` használata semmisíti meg a párhuzamosság előnyét. Egy 8‑magos gépen a `max_workers=8` gyakran a legjobb áteresztőképességet adja, de érdemes néhány értéket kipróbálni a hardveredhez leginkább illő beállítás megtalálásához.

## 5. lépés: Az eredmény ellenőrzése és a szélsőséges esetek kezelése

A szkript futtatásakor minden PNG-hez egy szövegrészletet kell látnod, amelynek elején a fájlnév szerepel:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Ha bármelyik kép hibát okoz (sérült fájl, nem támogatott formátum), az `except` ág egy hasznos hibaüzenetet ír ki ahelyett, hogy az egész köteg összeomlana.

### A megoldás bővítése

| Szenárió | Javasolt módosítás |
|----------|--------------------|
| **Több ezer oldal** | Válts `ProcessPoolExecutor`‑ra a több CPU folyamat kihasználásához, vagy darabold fel a listát és kötegelt módon dolgozd fel sorozatosan. |
| **Eltérő képformátumok (JPG, TIFF)** | A `storage.Image.load` metódus automatikusan felismeri a formátumot, így csak add hozzá a fájlokat az `input_images` listához. |
| **Eredmények tárolása** | Írd a `text`‑et egy `.txt` fájlba vagy illeszd be egy adatbázisba az `else` ágon belül. |
| **Teljesítményfigyelés** | Csomagold be a `recognize_image`‑t egy időmérővel (`time.perf_counter`) és naplózd a fájlonkénti időt. |

## Teljes, működő példa (másolás‑beillesztésre kész)

Az alábbiakban a teljes szkript látható, amelyet egyszerűen elhelyezhetsz egy `parallel_ocr.py` nevű fájlban. Semmi nem hiányzik – minden szükséges rész itt van.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Mentsd el a fájlt, állítsd be a `YOUR_DIRECTORY` helyőrzőt, majd futtasd:

```bash
python parallel_ocr.py
```

A konzolon minden PNG-hez megjelenik a kinyert szöveg, ahogy korábban is láttuk.

## Összegzés

Megmutattuk, hogyan **nyerhetünk szöveget PNG** fájlokból hatékonyan, az Aspose OCR async batch módját a Python `ThreadPoolExecutor`‑jével kombinálva. A szkript párhuzamosan konvertálja a beolvasott oldalak szövegét, skálázható módot biztosítva a **recognize image text python**‑stílusú OCR-hoz anélkül, hogy saját szálkezelőt kellene írnod.  

Ha tovább szeretnéd fejleszteni, próbáld ki:

* Az eredmények tárolását egy kereshető SQLite adatbázisban.  
* Képelőfeldolgozás (kiegyenesítés, zajcsökkentés) hozzáadását OpenCV‑vel az OCR előtt.  
* A szkript telepítését egy Flask vagy FastAPI végpont mögötti mikroszolgáltatásként.

Ne feledd, a magas teljesítményű OCR kulcsa nem csak egy gyorsabb motor – hanem az is, hogy a munkát úgy adod át a motorhoz, hogy a párhuzamosságot maximálisan kihasználd. Ezzel a mintával tucatnyi, vagy akár több száz PNG beolvasást is kezelhetsz minimális kómmódosítással.

Jó kódolást, és legyenek a PDF‑eid mindig kereshetők!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}