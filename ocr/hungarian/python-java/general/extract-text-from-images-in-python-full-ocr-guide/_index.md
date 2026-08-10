---
category: general
date: 2026-06-19
description: Képek szövegének kinyerése Python OCR segítségével. Ismerje meg az automatikus
  nyelvfelismerést, a párhuzamos feldolgozást és a kötegelt felismerést egy tömör
  útmutatóban.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: hu
og_description: Képekből szöveg kinyerése Python OCR-rel. Ez az útmutató bemutatja
  az automatikus nyelvfelismerést, a párhuzamos feldolgozást és a kötegelt felismerést
  egyetlen oktatóanyagban.
og_title: Képekből szöveg kinyerése Pythonban – Teljes OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Szöveg kinyerése képekből Pythonban – Teljes OCR útmutató
url: /hu/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg kinyerése képekből Pythonban – Teljes OCR útmutató

Valaha is elgondolkodtál, hogyan **szöveget nyerhetsz ki képekből** anélkül, hogy kézzel be kellene gépelned minden szót? Nem vagy egyedül. Akár régi nyugtákat digitalizálsz, kereshető dokumentumarchívumot építesz, vagy csak menő AI trükkökkel játszol, a képekből szöveg kinyerésének képessége ma már elengedhetetlen készség minden Python fejlesztő számára.

Ebben a tutorialban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **szöveget nyerhetsz ki képekből** egy népszerű OCR motor segítségével. Kitérünk az automatikus nyelvfelismerésre, a párhuzamos feldolgozásra a sebesség növelése érdekében, valamint a csoportos képfelismerésre, hogy tucatnyi fájlt másodpercek alatt tudj kezelni. Pontosan erre van szükséged? Merüljünk el benne.

## Mit fogsz megtanulni

- Hogyan hozhatsz létre OCR motor példányt a `ocr.OcrEngine` segítségével.
- Az **automatikus nyelvfelismerés** engedélyezése, hogy a motor önmagától kiválassza a megfelelő nyelvet.
- A **párhuzamos feldolgozású OCR** beállítása egy egyedi szálkészlettel.
- A **csoportos képfelismerés** futtatása fájlok listáján.
- A felismert szöveg kiírása minden képre, készen áll a mentésre vagy indexelésre.

Nincs szükség külső dokumentációra – minden, amire szükséged van, itt van, és a kód azonnal működik az `ocr` csomaggal (telepítsd a `pip install ocr` paranccsal).

## Előfeltételek

1. Python 3.8 vagy újabb telepítve.  
2. `ocr` csomag (`pip install ocr`).  
3. Egy mappa PNG (vagy JPG) képekkel, amelyeket feldolgozni szeretnél.  
4. Alapvető ismeretek a Python függvényekkel és ciklusokkal kapcsolatban.

Ennyi – nincsenek nehéz függőségek, nincs GPU varázslat, csak tiszta Python.

![szöveg kinyerése képekből példa](https://example.com/ocr-demo.png "Képernyőkép, amely a képekből kinyert szöveg kimenetét mutatja")

*Alt szöveg: képekből szöveg kinyerése demó képernyőkép*

## 1. lépés – Az OCR motor beállítása (Elsődleges kulcsszó akcióban)

Először is: hozz létre egy OCR motor példányt. Tekintsd a `ocr.OcrEngine()`-t a művelet agyának; ismeri a karakterek, sorok és bekezdések olvasását.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Miért van szükségünk egy explicit motorra? Mert a **ocr.OcrEngine használata** finomhangolt vezérlést biztosít a nyelvi beállítások, a szálkezelés és egyéb funkciók felett. Ez a legflexibilisebb mód a **szöveg kinyerésére képekből**, összehasonlítva az egyvonalas segédeszközökkel.

## 2. lépés – Engedjük, hogy a motor automatikusan felismerje a nyelveket

A legtöbb OCR könyvtár megköveteli, hogy megadd, melyik nyelvet keresse. Ez egynyelvű projektnél rendben van, de egy vegyes nyelvű batch esetén nehézkes. Szerencsére az `ocr` csomag támogatja az **automatikus nyelvfelismerést**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Az `engine.language` beállítása `ocr.Language.Auto`-ra azt mondja a motornak, hogy minden képet átvizsgáljon, és a megfelelő nyelvi modellt válassza. Ez az apró sor órákat takarít meg a manuális konfigurációból, ha nemzetközi dokumentumokkal dolgozol.

## 3. lépés – Gyorsítsuk fel a párhuzamos feldolgozású OCR-rel

Ha négy vagy több CPU magod van, miért ne használnád őket? A motor képes szálkészletet indítani, így egyszerre több képet is feldolgozhatsz. Itt jön képbe a **párhuzamos feldolgozású OCR**.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Nyugodtan állítsd be a `4` számot a gépednek megfelelően. Több szál → gyorsabb batch futtatás, de ne feledd, hogy minden szál memóriát fogyaszt, ezért találd meg a megfelelő egyensúlyt a környezetedben.

## 4. lépés – Gyűjtsd össze a feldolgozni kívánt képeket

Most egy fájlútvonalak listájára van szükségünk. Kézzel is összeállíthatod, beolvashatod CSV‑ből, vagy használhatod a `glob`‑ot. Átláthatóság kedvéért egy rövid listát kódolunk be:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Cseréld le a `YOUR_DIRECTORY`‑t a rendszereden lévő tényleges útvonalra. Ha tucatnyi fájlod van, egy gyors `glob.glob("*.png")` elvégzi a nehéz munkát.

## 5. lépés – Csoportos képfelismerés futtatása

Itt van a tutorial szíve: egyetlen hívás, amely minden képet a `files` listában feldolgoz, és egy eredményobjektumok listáját adja vissza. Ez a **csoportos képfelismerés** funkció teszi a nagy léptékű OCR‑t gyakorlati szintre.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

A háttérben a motor minden fájlt eloszt a korábban beállított négy munkás szál között, miközben automatikusan felismeri az egyes képek nyelvét. A metódus egy listát ad vissza, ahol minden elem a felismert szöveget és a metaadatokat tartalmazza.

## 6. lépés – A kinyert szöveg kiírása (vagy tárolása)

Végül végigiterálunk az eredményeken, és kiírjuk a szöveget. Egy valódi projektben valószínűleg adatbázisba vagy CSV‑fájlba írnád, de a kiírás egyszerűvé teszi a példát.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Minden blokk a fájlnevet mutatja, majd az OCR‑ből származó karakterláncot. Ha egy kép több nyelvet tartalmaz, a megfelelő karakterek megjelennek az előző **automatikus nyelvfelismerés** lépésnek köszönhetően.

## Profi tippek és gyakori buktatók

- **A kép minősége számít** – a homályos vagy alacsony kontrasztú képek szemét eredményt adnak. Szükség esetén előfeldolgozd OpenCV‑vel (`cv2.threshold`, `cv2.resize`).
- **Szálak száma vs. I/O** – ha a képek lassú hálózati meghajtón vannak, a több szál nem segíthet. Figyeld a CPU használatot `top` vagy `Task Manager`‑rel.
- **Unicode kezelés** – a `result.text` egy Unicode karakterlánc. Fájlok írásakor nyisd meg őket `encoding="utf-8"` beállítással, hogy elkerüld a `UnicodeEncodeError`‑eket.
- **Memóriahasználat** – nagy PDF‑ek sok RAM‑ot fogyaszthatnak. Ha `MemoryError`-t kapsz, csökkentsd a szálkészlet méretét vagy dolgozd fel a képeket kisebb darabokban.

## Teljes működő szkript

Az alábbiakban megtalálod a teljes, másolás‑beillesztésre kész szkriptet, amely tartalmazza a megbeszélt összes lépést. Mentsd el `batch_ocr.py` néven, majd futtasd `python batch_ocr.py` paranccsal.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Futtasd így:

```bash
python batch_ocr.py ./my_images 4
```

Minden képre egy szépen formázott szövegrészletet látsz, ami bizonyítja, hogy **szöveget nyerhetsz ki képekből** nagy léptékben.

## Mi következik?

Most, hogy elsajátítottad a **szöveg kinyerését képekből** Pythonban, érdemes tovább mélyedni:

- **Utófeldolgozás**: tisztítsd meg az OCR kimenetet regex‑szel vagy természetes nyelvi könyvtárakkal.
- **PDF konverzió**: a kinyert szövegeket egy PDF generátorba táplálva kereshető PDF‑eket hozhatsz létre.
- **Felhő OCR szolgáltatások**: hasonlítsd össze az on‑prem `ocr` eredményeket a Google Vision vagy Azure OCR megoldásaival a szélsőséges pontosság érdekében.
- **GUI front‑end**: építs egy kis Flask vagy FastAPI alkalmazást, amely lehetővé teszi a felhasználók számára a képek feltöltését és a kinyert szöveg azonnali megtekintését.

Mindezek a témák a **Python OCR könyvtár** alapjára épülnek, és mindegyik profitál a **párhuzamos feldolgozású OCR** trükkökből, amelyeket itt bemutattunk.

---

*Boldog kódolást! Ha elakadsz, írj egy megjegyzést lent – mindig szívesen segítek az OCR‑buktatók megoldásában.*

## Mit tanulj meg legközelebb?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépés‑ről‑lépésre magyarázatokkal, hogy további API funkciókat saját projektjeidben is könnyedén alkalmazhass.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Szöveg kinyerése képekből OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Szöveg kinyerése képből – OCR optimalizálás Aspose.OCR‑rel .NET‑hez](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}