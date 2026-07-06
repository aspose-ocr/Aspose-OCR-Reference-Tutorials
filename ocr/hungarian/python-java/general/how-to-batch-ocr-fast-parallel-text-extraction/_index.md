---
category: general
date: 2026-03-26
description: Hogyan lehet hatékonyan kötegelt OCR-t végezni Pythonban — tanulj meg
  szöveget kinyerni képekből és PDF-ekből OCR-konverzióval párhuzamos feldolgozás
  segítségével.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: hu
og_description: hogyan lehet hatékonyan tömeges OCR-t végezni—lépésről‑lépésre útmutató
  a képek szövegének kinyeréséhez, PDF OCR konverzióhoz és a Python használatával
  történő tömeges OCR feldolgozáshoz.
og_title: 'Hogyan végezzünk kötegelt OCR-t: gyors párhuzamos szövegkinyerés'
tags:
- OCR
- Python
- Parallel Computing
title: 'Hogyan végezzünk kötegelt OCR-t: gyors párhuzamos szövegkivonás'
url: /hu/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kötegelt OCR: gyors párhuzamos szövegkinyerés

Gondolkodtál már **hogyan kötegelt OCR**-t végezni, amikor tucatnyi beolvasott oldal, képernyőfelvétel és PDF hever a gépen? Nem vagy egyedül – a legtöbb fejlesztő ugyanazzal a problémával szembesül: az egyes fájlok egyesével történő feldolgozása fájdalmas szűk keresztmetszetté válik.  

A jó hír, hogy elindíthatsz néhány munkás szálat, betáplálhatod nekik az összes fájlt, és nézheted, ahogy az OCR motor párhuzamosan dolgozza fel a köteget. Ebben a tutorialban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **extract text from images**, hogyan végezz **pdf ocr conversion**‑t, és hogyan használd a **parallel ocr processing**‑t a sebesség növeléséhez.

> **Mit fogsz megtanulni**  
> * Egy teljesen működő Python szkript, amely egy lépésben dolgozza fel a PNG, TIFF, PDF és JPG fájlok vegyes listáját.  
> * Megértés, hogy miért gyorsít fel egy szálkészlet az I/O‑központú OCR feladatokat.  
> * Tippek hibakezeléshez, nagy PDF-ekhez és egyedi szál számok beállításához.  

## Prerequisites

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel a következőkkel:

| Követelmény | Indok |
|-------------|-------|
| Python 3.8+ | Modern szintaxis és `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | `OcrBatchProcessor` és eredményobjektumok biztosítása |
| A handful of sample files (PNG, TIFF, PDF, JPG) | A **extract text from images** működésének megtekintéséhez |
| Basic familiarity with threads (optional) | Hasznos, de nem kötelező |

Ha még nem telepítetted az `ocr` csomagot, futtasd:

```bash
pip install ocr-lib   # replace with the actual package name
```

Most, hogy a környezet készen áll, bontsuk le a feladatot.

## 1. lépés: Segédfüggvények importálása és a kötegelt feldolgozó példányosítása

Az első dolog, amire szükségünk van, egy hely, ahol az összes OCR feladatot összegyűjthetjük. Az `OcrBatchProcessor` osztály pontosan ezt teszi – sorba állítja a munkákat, és egy `Future` objektumok listáját adja vissza.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Miért fontos*: Az `as_completed` importálása lehetővé teszi, hogy azonnal reagáljunk minden befejezett feladatra, a leglassabb fájlra való várakozás nélkül. Ez a **batch ocr processing** lényege.

## 2. lépés: A munkavállaló pool finomhangolása párhuzamos végrehajtáshoz

Alapértelmezés szerint a processzor egyetlen szálat használhat, ami aláássa a kötegelt feldolgozás célját. Kifejezetten négy munkást kérünk – nyugodtan növeld ezt a számot a CPU magjaid számához.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tipp*: I/O‑központú feladatoknál, mint az OCR, gyakran `CPU cores * 2` után csökken a hozam. Próbálj ki néhány értéket, és válaszd ki az optimálisat.

## 3. lépés: Minden OCR‑elni kívánt fájl sorba állítása

Itt egy vegyes csomagot adunk hozzá képekből és PDF‑ekből. Az `add` metódus egyszerűen rögzíti az útvonalat; a tényleges munka csak a köteg benyújtása után kezdődik.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Ha egy teljes mappát szeretnél feldolgozni, egy gyors `glob` ciklus megoldja a feladatot:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## 4. lépés: A feladatok indítása és a future‑ok gyűjtése

A `submit_all` hívás zöld lámpát ad a processzornak. Egy `Future` objektumok listáját adja vissza – tekintsd őket olyan helyőrzőnek, amely a később megjelenő eredményeket tárolja.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Ekkor már az OCR motor a háttérben dolgozik, minden szál egy fájlon "rágcsál".

## 5. lépés: Az eredmények lekérése, amint elkészülnek

Az `as_completed` használatával a future‑okon a befejezésük sorrendjében iterálunk, nem pedig a benyújtásuk sorrendjében. Ez a szkriptet reszponzívvá teszi, különösen akkor, ha egyes PDF‑ek hosszabbak, mint a egyszerű PNG‑k.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Minden blokk az eredeti fájl egyszerű szöveges reprezentációjának felel meg. Ha **pdf ocr conversion**‑t végzel, a szöveg tartalmazni fogja mindazt, amit az OCR motor minden oldalról ki tudott fejteni.

## Szélhelyzetek és gyakori buktatók kezelése

| Helyzet | Mit figyeljünk | Gyors megoldás |
|---------|----------------|----------------|
| Sérült kép | a `future.result()` `OSError`-t dob | Csomagold try/except-be (lásd a fenti kód) |
| Nagyon nagy PDF-ek ( > 100 MB ) | Memória nyomás, lassabb szálak | Növeld mérsékelten a `thread_count` értékét, vagy oszd fel a PDF-et fejezetekre |
| Vegyes nyelvű dokumentumok | Az alapértelmezett OCR modell hibásan ismerhet fel | Adj nyelvi tippeket az `OcrBatchProcessor`-nek, ha a könyvtár támogatja |
| Elrendezés megőrzése szükséges | A sima `get_text()` elveszíti az oszlopokat | Használd az `ocr_result.get_hocr()` vagy hasonló elrendezés‑tudatos metódust |

### Pro tipp: Egyedi szál szám fájltípus alapján

Ha tudod, hogy a munkaterhed túlnyomórészt PDF‑ekből áll, több szálat oszthatsz azokhoz, kevesebbet pedig a kis PNG‑khez. Néhány könyvtár enged per‑job `priority`‑t megadni; ellenkező esetben létrehozhatsz két külön köteget – egyet képeknek, egyet PDF‑eknek – és egyszerre futtathatod őket.

## Vizuális áttekintés (opcionális)

![hogyan kötegelt OCR munkafolyamat diagram](https://example.com/ocr-workflow.png "hogyan kötegelt OCR munkafolyamat")

*A diagram illusztrálja a folyamatot a fájlok felfedezésétől → köteg létrehozásáig → párhuzamos végrehajtásig → eredmény aggregálásig.*

## Teljes szkript, amit másolhatsz‑beilleszthetsz

Az alábbiakban megtalálod a teljes programot, amely készen áll egy `.py` fájlba másolni. Tartalmazza a fenti összes kódrészletet, valamint egy apró segédfüggvényt, amely automatikusan felfedezi a támogatott fájlokat egy könyvtárban.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Mentsd el `batch_ocr.py` néven, mutasd meg egy olyan mappára, amely a beolvasott anyagokat tartalmazza, és nézd, ahogy a konzol megtelik a kinyert szöveggel.  

### Miért működik ez

* **Thread pool** – Az OCR főként lemez‑I/O-ra és külső motorhívásokra vár, így a több szál a CPU-t foglaltan tartja.  
* **`as_completed`** – Az eredményeket azonnal megkapod, amint készen állnak, ami ideális UI‑visszajelzéshez vagy streaming csővezetékekhez.  
* **Error isolation** – Egy rossz fájl nem fogja leállítani az egész köteget; a `try/except` blokk elszigeteli a hibákat.  

## Összegzés

Röviden, most már tudod, **hogyan kötegelt OCR**-t végezni a Python `concurrent.futures`‑ével és egy olyan OCR könyvtárral, amely támogatja a kötegelt feldolgozást. Egy mérsékelt szálkészlet konfigurálásával, minden támogatott fájl sorba állításával és az eredmények befejezés szerinti lekérésével gyors **parallel ocr processing**-et érhetsz el megbízhatóság feláldozása nélkül.  

Innen tovább:

* Az eredményt csatlakoztathatod egy keresőindexhez a gyors dokumentum‑visszakereséshez.  
* Kiterjesztheted a szkriptet, hogy minden eredményt egy `.txt` fájlba írjon az eredeti mellé.  
* Cseréld le a beépített thread pool‑t `asyncio`-ra, ha az OCR könyvtárad async API‑kat kínál.  

Folytasd a kísérletezést – cseréld le Tesseract‑ra, Azure Cognitive Services‑re vagy Google Vision‑ra, és ugyanazt a mintát fogod látni. Boldog OCR‑zést!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}