---
category: general
date: 2026-03-18
description: Szöveg kinyerése PNG-ből Python és az Aspose OCR használatával. Tanulja
  meg, hogyan töltsön be képet OCR-hez, hogyan futtasson OCR-t több fájlon, és hogyan
  valósítson meg kötegelt OCR-t párhuzamos képfelismeréssel.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: hu
og_description: Szöveg kinyerése PNG-ből az Aspose OCR-rel Pythonban. Ez az útmutató
  bemutatja, hogyan töltsünk be képet OCR-hez, hogyan dolgozzunk fel több fájlt OCR-rel,
  és hogyan futtassunk kötegelt OCR képeket párhuzamos képfelismeréssel.
og_title: Szöveg kinyerése PNG-ből – Párhuzamos OCR útmutató
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Szöveg kinyerése PNG-ből – Párhuzamos OCR útmutató kötegelt képfelismeréshez
url: /hu/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése PNG‑ből – Párhuzamos OCR útmutató kötegelt képfelismeréshez

Valaha szükséged volt **szöveg kinyerésére PNG** fájlokból, de elakadtál azon a ponton, amikor egyetlen kép feldolgozása örökké tart? Nem vagy egyedül. Sok valós projektben – gondolj csak a számlaskannerekre, nyugtadigitalizálókra vagy archiváló eszközökre – a sebesség számít, és a PNG‑k egyesével történő feldolgozása egyszerűen nem elegendő.

Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható megoldáson, amely **betölti a képet OCR‑hez**, **ocr több fájlt** **kötegelt OCR képek** módon futtat, és **párhuzamos képfelismerést** használ a Python `threading` moduljával. A végére egy olyan szkriptet kapsz, amely másodpercek alatt, nem percek alatt nyeri ki a szöveget tetszőleges számú PNG‑ből.

## Amire szükséged lesz

- Python 3.8 vagy újabb (a bemutatott szintaxis 3.10‑en is működik).  
- Az Aspose OCR for Java/Python csomag (`aspose-ocr`). Telepítheted `pip`‑en keresztül.  
- Egy mappa néhány, a feldolgozandó PNG fájllal.  
- Mérsékelt mennyiségű RAM – minden szál egy kis OCR‑motor példányt tart, így még egy laptop is több tucat munkavállalót képes indítani.

Nincs külső szolgáltatás, nincs felhőkulcs, és nincs rejtélyes konfigurációs fájl. Csak tiszta Python kód, amelyet másolhatsz‑beilleszthetsz és futtathatsz.

## Miért kell szöveget kinyerni PNG‑ből párhuzamosan?

Egy PNG feldolgozása CPU‑intenzív: az OCR‑motor egy sor képelemző algoritmust futtat, amelyek átvágják a pixel adatokat. Ha tíz, húsz vagy akár száz képed van, a teljes futási idő lényegében az egyes futások összegével egyezik.

Minden fájlhoz egy szál indításával lehetővé tesszük, hogy az operációs rendszer párhuzamosan ütemezze ezeket a CPU‑igényes feladatokat. Többmagos gépen ez gyakran felére – vagy akár negyedére – csökkenti a valós időt. Az árnyékoldal egy kissé nagyobb memóriahasználat, de a legtöbb kötegelt feladat esetén a sebességnyereség ezt bőven ellensúlyozza.

> **Pro tipp:** Ha több száz megabájt képpel dolgozol, fontold meg a `concurrent.futures.ProcessPoolExecutor` használatát a `threading` helyett. A folyamatok valódi párhuzamosságot biztosítanak a GIL‑korlátozott CPython értelmezőben, egy kicsit nagyobb overhead ára mellett.

## 1. lépés: Aspose OCR telepítése Pythonhoz

Először is—szerezzük be az OCR könyvtárat a rendszeredre.

```bash
pip install aspose-ocr
```

Ez az egyetlen sor letölti a legújabb Aspose OCR binárisokat és a Python kötéseket. Ha jogosultsági hibát kapsz, próbáld meg a `--user` kapcsolót, vagy használj virtuális környezetet.

## 2. lépés: Kép betöltése OCR‑hez – a munkavállaló függvény

Most definiáljuk a magrutint, amely minden szálban végrehajtásra kerül. **Betölti a képet OCR‑hez**, futtatja a felismerést, és előnézetet nyomtat a kinyert szövegből.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Néhány fontos megjegyzés:

- **Miért új `OcrEngine` minden szálhoz?** A motor belső puffereket tart; egy példány megosztása versenyhelyzeteket és torz kimenetet okozna.  
- **Miért távolítjuk el a sortöréseket?** Amikor a konzolra naplózunk, így a sor rendezett marad.  
- **Hibakezelés?** Éles környezetben a testet `try/except`‑be tennéd, és esetleg fájlba naplóznád – erről később lesz szó.

## 3. lépés: Listázd a feldolgozandó PNG fájlokat

Hard‑kódolhatnád a listát, de egy rugalmasabb megközelítés a könyvtár beolvasása. Lent három fájlt sorolunk fel kézzel a tisztaság kedvéért; cseréld ki az útvonalakat a saját mappádra.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Ha inkább automatikus felfedezést szeretnél:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Ez a kis módosítás lehetővé teszi, hogy **szöveget nyerj ki PNG** fájlokból tömegesen anélkül, hogy minden alkalommal a forráskódot módosítanád.

## 4. lépés: Állítsd be az ocr több fájlt kötegelt OCR képekkel

Most minden képhez létrehozunk egy szálat. Ez a **kötegelt OCR képek** minta szíve.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

A listakomprehenciót használva a kód tömör marad, és minden `Thread` objektum tárolja a célfüggvényt és annak argumentumát (`image_path`).  

> **Megjegyzés:** A Python `threading` modul natív OS szálakat használ, így egy 4‑magos laptopon általában legfeljebb négy szál fut egyszerre; a többit a magok szabadulásakor ütemezi be a rendszer.

## 5. lépés: Párhuzamos képfelismerés indítása

A munkavállalók indítása egyszerű: iterálj a listán és hívd meg a `start()`‑ot. Ezután a `join()`‑nal várunk, amíg minden szál befejeződik.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Amikor a szkript befejeződik, olyan sorokat látsz majd, mint:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Ez a kimenet megerősíti, hogy minden PNG feldolgozásra került, és a kinyert szöveg további felhasználásra (pl. adatbázisba mentés vagy NLP csővezetékbe való betáplálás) elérhető.

## 6. lépés: Ellenőrizd az eredményeket és kezeld a szélsőséges eseteket

### Üres eredmények ellenőrzése

Néha egy kép túl zajos, vagy az OCR‑motor nem talál karaktert. Egy gyors ellenőrzés megakadályozhatja a későbbi hibákat.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### A párhuzamos szálak számának korlátozása

Ha ezt egy szerény VM‑en futtatod, a több száz szál indítása túlterhelheti az ütemezőt. A párhuzamosságot szemináriummal (semaphore) korlátozhatod:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Eredmények mentése fájlba

A nyomtatás helyett lehet, hogy egy CSV‑t szeretnél, amely a fájlnevet és a kinyert szöveget tartalmazza:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Győződj meg róla, hogy a CSV‑t **egyszer** nyitod meg a szálfüggvényen kívül, hogy elkerüld a versenyhelyzeteket; a `csv` modul írója egyszerű írások esetén szálbiztos.

## Teljes működő példa

Mindent összevonva, itt egy egyetlen szkript, amelyet elhelyezhetsz egy `batch_ocr.py` nevű fájlba és futtathatsz:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}