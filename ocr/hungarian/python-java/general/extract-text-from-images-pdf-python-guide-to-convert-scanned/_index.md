---
category: general
date: 2026-06-06
description: Szöveg kinyerése képekből és PDF-ből Python OCR-rel. Tanulja meg, hogyan
  konvertálhatja a beolvasott dokumentumokat szöveggé gyorsan aszinkron kötegelt felismeréssel.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: hu
og_description: Szöveg kinyerése képekből és PDF‑ből Python segítségével. Ez a lépésről‑lépésre
  útmutató bemutatja, hogyan lehet a beolvasott dokumentumokat szöveggé konvertálni
  aszinkron OCR használatával.
og_title: Szöveg kinyerése képekből PDF-ben – Python OCR oktató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Szöveg kinyerése képek PDF-ből – Python útmutató a beolvasott dokumentumok
  szöveggé konvertálásához
url: /hu/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek PDF-ből szöveg kinyerése – Python útmutató a beolvasott dokumentumok szöveggé konvertálásához

Valaha is szükséged volt **szöveg kinyerésére képek PDF-ből** anélkül, hogy órákat töltenél a gépeléssel? Ebben az útmutatóban megmutatjuk, hogyan **konvertálhatod a beolvasott dokumentumokat szöveggé** egy egyszerű aszinkron OCR munkafolyamat segítségével Pythonban.  

Ha már valaha is egy csomó beolvasott PDF-et néztél, és azt gondoltad: „Biztos van gyorsabb módja”, akkor jó helyen vagy. Át fogjuk nézni a kód minden sorát, elmagyarázzuk, miért fontos minden részlet, és még néhány edge case‑et is bemutatunk, amivel előfordulhat, hogy találkozol.

## Mit fogsz megtanulni

- Hogyan indítsunk el egy OCR motort és állítsuk be a felismerési nyelvet.  
- A vegyes PNG‑ és PDF‑lista betáplálásának mechanikája egy kötegelt felismerőbe.  
- Az OCR feladat aszinkron futtatása, hogy az alkalmazásod reagálóképes maradjon.  
- Az eredmények visszakeresése, párosítása a forrásfájlokkal, és tiszta kimenet nyomtatása.  

**Előfeltételek**: Python 3.8+, alapvető ismeretek az `asyncio`‑ról vagy a `concurrent.futures`‑ről, valamint egy OCR könyvtár, amely egy példához hasonló `OcrEngine` osztályt biztosít (pl. Aspose.OCR, Tesseract wrapper, vagy egy egyedi wrapper). Nehéz beállításra nincs szükség – csak telepítsd a könyvtárat, és már indulhatsz.

![szöveg kinyerése képek PDF-ből](https://example.com/placeholder.png "OCR kimenet képernyőképe – szöveg kinyerése képek PDF-ből")

## Képek PDF-ből szöveg kinyerése – OCR motor beállítása

Az első dolog, amire szükséged van, egy OCR motor példány, amely a dokumentumaid nyelvére van konfigurálva. A példában franciát használunk, de bármely támogatott nyelvre cserélheted.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Miért fontos ez**: A nyelv előzetes beállítása drámaian javítja a pontosságot. A motor nyelvspecifikus szótárakat és karaktermodelleket használ; a rossz nyelv megadása gyakori oka a torz kimenetnek.

## Fájllista előkészítése – Képek és PDF-ek együtt

A kötegelt felismerő képes kezelni mind a raszteres képeket (`.png`, `.jpg`), mind a PDF konténereket. Csak adj át egy egyszerű Python listát a fájlutakból.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tipp**: Tartsd a listát lapos struktúrában; a motor belsőleg minden PDF‑oldalt képekké bont, mielőtt a felismerés megtörténik. Ha több ezer fájlod van, fontold meg a lista kisebb adagokra bontását, hogy elkerüld a memóriahullámokat.

## Aszinkron kötegelt felismerés indítása

A fő szál blokkolása helyett a OCR feladatot a háttérben indítjuk el. A metódus egy `Future`‑t ad vissza, amely végül egy `OcrResult` objektumok listáját fogja tartalmazni.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Hogyan működik**: A motor a háttérben egy szálcsoportot (vagy aszinkron feladatot, a megvalósítástól függően) hoz létre. Ez lehetővé teszi, hogy más munkákat is végezz – például UI frissítést, további fájlok betöltését vagy a folyamat állapotának naplózását – miközben a nehéz feldolgozás máshol zajlik.

## Hasznos feladat végrehajtása OCR futása közben

Gyakori hiba, hogy üresjáratban várakozol és szoros ciklusban lekérdezed a future‑t. Ehelyett végezhetsz bármilyen más, nem kapcsolódó feladatot. Demonstrációként csak egy státuszsor kiírását mutatjuk.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Eredmények összegyűjtése a Future befejezése után

Amikor készen állsz az OCR kimenet begyűjtésére, használd a `as_completed`‑t a `concurrent.futures`‑ből. Ez a minta akkor is működik, ha egy vagy több future‑d van.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Mit fogsz látni**: Minden fájlút után a kinyert egyszerű szöveg jelenik meg. PDF-ek esetén a `result.text` tartalmazza az összes oldal összefűzött szövegét.

### Várható kimenet (példa)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Ha hiányzó karaktereket észlelsz, ellenőrizd, hogy a beállított nyelv megegyezik‑e a dokumentum nyelvével, és fontold meg a képek előfeldolgozását (kiegyenesítés, kontraszt növelés) a motorba való betáplálás előtt.

## Széljegyek és gyakori buktatók kezelése

| Helyzet | Mit kell tenni |
|-----------|------------|
| **Vegyes nyelvek** | Először futtass nyelvfelismerő lépést, majd hozz létre külön motorokat nyelvenként. |
| **Óriási PDF-ek (> 100 MB)** | Oszd fel a PDF-et egyes oldalakra a lemezen (pl. a `PyPDF2`‑vel), és tápláld be őket külön bejegyzésként. |
| **Nem latin írásrendszerek** | Győződj meg róla, hogy az OCR könyvtár tartalmazza a szükséges nyelvi csomagot; egyes könyvtárakhoz további adatfájlok letöltése szükséges. |
| **Teljesítménybottleneck** | Növeld a szálcsoport méretét (`engine.set_thread_pool_size(8)`) vagy válts GPU‑gyorsított backendre, ha elérhető. |
| **Hiányzó szöveg alacsony felbontású képeken** | Előfeldolgozás OpenCV‑vel: `cv2.resize`, `cv2.threshold`, és `cv2.medianBlur` a olvashatóság javításához. |

## Teljes működő példa (másolás-beillesztés kész)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Mentsd el `extract_text_async.py` néven, cseréld le a `YOUR_DIRECTORY`‑t a fájljaid elérési útjára, telepítsd az OCR csomagot (`pip install your-ocr-lib`), és futtasd a `python extract_text_async.py` parancsot. A konzolon a korábban illusztrált kimenetet kell látnod.

## Következő lépések – Alapvető kinyerésen túl

- **Utófeldolgozás**: Távolítsd el a felesleges szóközöket, normalizáld a Unicode‑t (`unicodedata.normalize`), vagy futtass helyesírás-ellenőrzőt az OCR zaj csökkentéséhez.  
- **Strukturált kimenet**: Exportáld az eredményeket CSV‑be, JSON‑ba, vagy közvetlenül egy adatbázisba a további kereséshez.  
- **Párhuzamos kötegek**: Ha több száz fájlod van, indíts több future‑t, és használj egy sort, hogy a CPU folyamatosan dolgozzon anélkül, hogy a memória túlterhelődne.  
- **Integráció webes keretrendszerekkel**: Kapcsold ezt a szkriptet egy Flask vagy FastAPI végponthoz, hogy igény szerint OCR‑szolgáltatást nyújts.

---

### TL;DR

Most már tudod, hogyan **szöveget nyerhetsz ki képek PDF‑ből** egy minimális Python szkripttel, amely aszinkron módon futtatja az OCR‑t, így **beolvasott dokumentumokat szöveggé konvertálhatsz**, miközben a programod reagálóképes marad. Kísérletezz a nyelvi beállításokkal, kötegméretekkel és előfeldolgozási trükkökkel, hogy a lehető legmagasabb karakter‑pontosságot érjed el.

Van egy saját ötleted – például OCR kézírásos jegyzeteken vagy felhőalapú szolgáltatáson? Írj egy megjegyzést, és jó kódolást!

## Mit érdemes még tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR-rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Szöveg kinyerése képekből OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Szöveg kinyerése képekből Aspose.OCR-rel – Engedélyezett karakterek](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}