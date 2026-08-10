---
category: general
date: 2026-06-28
description: Hogyan végezzünk kötegelt OCR-t Pythonban. Tanulj meg több képet OCR-ozni,
  szöveget kinyerni PNG-ből, és képet szöveggé konvertálni egy teljes Python OCR útmutatóval.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: hu
og_description: A Pythonban történő tömeges OCR módja az első mondatban magyarázva.
  Kövesd ezt a Python OCR útmutatót, hogy hatékonyan szöveget nyerj ki PNG fájlokból.
og_title: Hogyan végezzünk kötegelt OCR-t Pythonban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk kötegelt OCR-t Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t Pythonban – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, **hogyan lehet kötegelt OCR‑t** végrehajtani egy halom beolvasott oldalon anélkül, hogy egy UI‑t blokkoló ciklust írnál? Nem vagy egyedül. Tüzököt PNG‑fájlok feldolgozása egy‑esével olyan, mintha a festék száradását néznéd, különösen, ha minden kép dekódolása egy‑két másodpercet vesz igénybe.  

Ebben az útmutatóban bemutatunk egy tiszta, nem blokkoló módot **több kép OCR‑elésére** egyszerre, **szöveg kinyerésére PNG‑fájlokból**, és **kép‑szöveggé konvertálásra** egy modern Python OCR‑motor segítségével. A végére egy azonnal futtatható szkriptet kapsz, amelyet bármely projektbe beilleszthetsz – tökéletes egy gyors *python ocr tutorial* vagy egy termelés‑szintű kötegelt feladathoz.

## Amit építeni fogsz

- Inicializálsz egy OCR‑motort és beállítod a nyelvet latinra (vagy bármely más nyelvre, amire szükséged van).  
- Betáplálsz egy listát képfájl‑útvonalakkal (példánkban PNG) a motorba.  
- Elindítasz egy kötegelt műveletet, amely egy Future‑szerű objektumot ad vissza.  
- Az összes eredményt párhuzamosan egy szálkészlettel húzod le, miközben a fő szál szabad marad.  
- Kiírod az egyes oldalak felismert szövegét, szépen elválasztva.

Nincs rejtett varázslat, csak tiszta Python és egy harmadik‑fél OCR‑könyvtár (az illusztrációhoz a fiktív `pyocr` csomagot használjuk).  

**Előfeltételek**  
- Python 3.8+ telepítve.  
- Alapvető ismeretek a Python függvényekről és a `concurrent.futures`‑ról.  
- Hozzáférés egy OCR‑könyvtárhoz, amely egy `OcrEngine` osztályt biztosít (pl. `pip install pyocr`).  

Ha valamelyik hiányzik, szerezd be most – könnyebb, mint gondolnád.

---

## Hogyan végezzünk kötegelt OCR‑t Pythonban – Alapfogalmak

Mielőtt a kódba merülnénk, válaszoljunk a „miért” kérdésekre minden lépés mögött.

1. **Miért állítjuk be a nyelvet?**  
   Az OCR‑pontosság óriási ugrást tesz, ha a motor tudja, milyen karakterekre számíthat. A latin az angol, francia, spanyol stb. nyelvekhez megfelelő. Válts `Language.Japanese` vagy `Language.Arabic`‑ra, ha szükséges.

2. **Miért használunk kötegelt műveletet?**  
   Egy kötegelt hívás lehetővé teszi, hogy a motor belsőleg ütemezze a munkát, gyakran natív szálakat vagy GPU‑gyorsítást használva. Egy kezelőobjektát ad vissza, amelyet később lekérdezhetsz, így nem blokkolsz minden egyes kép feldolgozása közben.

3. **Miért ThreadPoolExecutor?**  
   A visszakapott Future objektum *lusta* – csak akkor kezd el eredményeket húzni, amikor kérjük. Ha egy szálkészletet adunk a `getAll`‑nak, a Python párhuzamosan kérdezi le minden oldal szövegét, drámai módon csökkentve a teljes futási időt.

4. **Miért enumeráljuk az eredményeket?**  
   Az eredmények sorrendje megegyezik a bemeneti útvonalak sorrendjével, így biztonságosan címkézhetjük az egyes oldalszámokat.

Ezeknek a „miért” kérdéseknek a megértése segít a mintát más könyvtárakra vagy nagyobb adathalmazokra adaptálni.

---

## 1. lépés: Szükséges csomagok telepítése és importálása

Először győződj meg róla, hogy az OCR‑könyvtár telepítve van. A példában egy általános `pyocr` csomagot használunk; cseréld le a ténylegesen preferált könyvtárra (pl. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Most importáljuk a szükséges elemeket.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tipp:** A `Path` a `pathlib`‑ből használata teszi a szkriptet operációs‑rendszer‑függetlenné és könnyebben olvashatóvá.

---

## 2. lépés: OCR‑motor létrehozása és nyelv beállítása

A motor létrehozása egyszerű. A bemutatóhoz latinra rögzítjük.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

A `setLanguage` hívás opcionális néhány motor esetén, de jó szokás. Elmondja az OCR‑modellnek, hogy a kívánt karakterkészletre fókuszáljon, ezáltal növelve a sebességet és a pontosságot.

---

## 3. lépés: A feldolgozandó képfájlok listázása (Szöveg kinyerése PNG‑ból)

Gyűjtsd össze az összes PNG‑fájlt, amelyet konvertálni szeretnél. A `Path.glob` használatával egy egész mappát be tudsz dobni anélkül, hogy a szkriptet módosítanád.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Miért fontos:** A lista rendezésével determinisztikus sorrendet biztosítunk, ami később minden eredményt a megfelelő oldalszámhoz rendel.

---

## 4. lépés: Kötegelt OCR‑művelet indítása (Kép‑szöveggé konvertálás)

Most átadjuk a listát a motornak. A metódus egy Future‑szerű tárolót ad vissza, amelyet később lekérdezünk.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

A háttérben a motor saját munkaszálakat vagy akár GPU‑csővezetékeket indíthat. Nekünk csak az a fontos, hogy van egy kezelőnk (`batch_future`), amely tudja, hogyan kell lekérni az egyes eredményeket.

---

## 5. lépés: Az összes eredmény egyidejű lekérése (OCR több kép egyszerre)

Itt történik a valódi *köteg* feldolgozás. Ha egy `ThreadPoolExecutor`‑t adunk a `getAll`‑nak, minden oldal szövege saját szálban kerül lekérdezésre.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

A `max_workers` értékét a CPU‑magok számához vagy az OCR‑könyvtár ajánlásaihoz igazíthatod. Több munkás ≠ mindig gyorsabb – figyeld a CPU‑használatot.

---

## 6. lépés: Felismert szöveg kiírása (Python OCR Tutorial befejezése)

Végül nyomtatjuk ki minden oldal szövegét. A `Result` objektum a `getText()`‑t biztosítja – módosítsd, ha a könyvtárad más metódusnevet használ.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Várható kimenet (példa)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Ha egy kép hibát jelez, a legtöbb motor üres karakterláncot ad vissza vagy kivételt dob – a ciklust `try/except`‑el körülveheted, hogy az élszituációkat elegánsan kezeld.

---

## Teljes szkript – Kész a futtatásra

Az alábbiakban a komplett, önálló szkriptet találod. Másold be egy `batch_ocr.py` nevű fájlba, állítsd be a `YOUR_DIRECTORY`‑t, majd futtasd `python batch_ocr.py`‑val.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Mentsd, futtasd, és nézd, ahogy a konzol megtelik a kinyert szöveggel. Egyszerű, gyors és teljesen aszinkron.

---

## Gyakori hibák és elkerülésük módjai

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Nincs kimenet** – üres karakterláncok | Az OCR‑motor nem talált szöveget (túl zajos kép) | Előfeldolgozás: binarizálás, kiegyenesítés, vagy DPI növelése |
| **`FileNotFoundError`** | Hibás könyvtárútvonal vagy hiányzó PNG‑fájlok | Ellenőrizd a `YOUR_DIRECTORY`‑t, és győződj meg róla, hogy a fájlok `.png`‑vel végződnek |
| **Magas CPU‑használat** | `max_workers` túl magas a gépedhez képest | Csökkentsd a `max_workers` értékét, vagy engedélyezd a GPU‑gyorsítást, ha támogatott |
| **Unicode‑göröngy** | A motor alapértelmezett nyelve eltérő | Hívd meg `engine.setLanguage(Language.Latin)`‑t (vagy a megfelelő nyelvet) a kötegelt OCR előtt |

Ezek korai kezelése órákat spórolhat a hibakeresésben.

---

## A tutorial bővítése – Következő lépések

- **OCR több kép** más formátumokban (JPEG, TIFF) – csak a glob mintát módosítsd.  
- **Szöveg kinyerése PNG‑ból** és betáplálása egy keresőindexbe (pl. Elasticsearch).  
- **Kép‑szöveggé konvertálás** PDF‑generáláshoz a `reportlab` vagy `PyPDF2` segítségével.  
- **Párhuzamosítás gépek között** `multiprocessing`‑al vagy egy feladatkészlettel, mint a Celery, nagy adathalmazokhoz.  

Ezek a témák természetesen épülnek a **python ocr tutorial**-ra, amit most befejeztél.

---

## Összegzés

Áttekintettük, **hogyan végezzünk kötegelt OCR‑t** egy PNG‑gyűjteményen, bemutattuk egy kötegelt API erejét, és megmutattuk, hogyan **nyerjünk szöveget PNG‑ból** szálkészlet‑alapú megközelítéssel. A fenti komplett szkript már production‑kész, és most már szilárd alapod van bármely OCR‑intenzív Python‑projekthez.

Próbáld ki, finomítsd a nyelvi beállításokat, vagy cseréld le a `pyocr`‑t `pytesseract`‑ra – a minta változatlan marad. Van kérdésed vagy szeretnél egy menő felhasználási esetet megosztani? Írj kommentet, és folytassuk a beszélgetést.

*Boldog kódolást!*


## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}