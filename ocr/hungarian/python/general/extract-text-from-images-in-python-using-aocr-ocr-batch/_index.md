---
category: general
date: 2026-06-25
description: Szöveg kinyerése képekből a Python aocr könyvtárral – tanulj meg kötegelt
  OCR-t, állítsd be a nyomtatott felismerési módot, és adj hozzá egy AI utófeldolgozót.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: hu
og_description: Szöveg kinyerése képekből a Python aocr könyvtár segítségével. Ez
  az útmutató bemutatja a kötegelt OCR-t, a nyomtatott felismerési módot, valamint
  az opcionális AI utófeldolgozót.
og_title: Szöveg kinyerése képekből Pythonban – Teljes aocr kötegelt útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Szöveg kinyerése képekből Pythonban aocr OCR köteg segítségével
url: /hu/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek szövegének kinyerése Pythonban aocr OCR köteg használatával

Valaha is szükséged volt **képek szövegének kinyerésére**, de elborította a tucatnyi apró lépés? Nem vagy egyedül. Akár beolvasott űrlapokat digitalizálsz, számlákról nyersz adatot, vagy kereshető archívumot építesz, a megbízható OCR eredmények skálázása úgy érezheted, mintha egy meredek hegyet másznál.

A jó hír? A **aocr library** segítségével egy teljes **Python OCR batch**-et indíthatsz el néhány sor kóddal. Ebben az útmutatóban végigvezetünk az OCR köteg létrehozásán, egy mappából az összes támogatott kép betöltésén, a megfelelő **recognition mode printed** kiválasztásán, és még egy **AI postprocessor** csatolásán a pontosság további növeléséhez. A végére egy azonnal futtatható szkriptet kapsz, amely kinyeri a szöveget a képekből, és megmutatja, mennyit sikerült minden fájlban rögzíteni.

## Amit meg fogsz tanulni

- Hogyan telepítsd és importáld az `aocr` csomagot.
- Az `OcrBatch` beállítása, hogy automatikusan kezelje a több ezer fájlt.
- A nyomtatott dokumentumokhoz optimális felismerési mód kiválasztása.
- (Opcionális) AI post‑processzor csatolása a zajos eredmények tisztításához.
- Minden fájlútvonal megjelenítése a kinyert szöveg hossza mellett.
- Tippek a szélsőséges esetek kezelésére, mint a nem támogatott formátumok vagy üres oldalak.

### Előfeltételek

- Python 3.8 vagy újabb telepítve a gépeden.  
- Alapvető ismeretek a Python szkriptekhez (ciklusok, importok, stb.).  
- Hozzáférés egy beolvasott képek mappájához (PNG, JPG, TIFF, stb.).  

Ha ezek megvannak, merüljünk el—külső szolgáltatások nélkül.

## 1. lépés: Az aocr könyvtár telepítése

Először is. Az `aocr` csomag nem része a standard könyvtárnak, ezért a PyPI‑ról kell letölteni.

```bash
pip install aocr
```

> **Pro tipp:** Használj virtuális környezetet (`python -m venv .venv`), hogy a függőségek izoláltak legyenek.  

A telepítés után importálhatod a fő osztályokat.

```python
# core imports
import aocr
```

## 2. lépés: OCR köteg példány létrehozása

Az `OcrBatch` a munkagépe, amely bejárja a könyvtáradat és nyilvántartja az összes képfájlt. Gondolj rá úgy, mint egy szállítószalagra, amely a képeket az OCR motorba juttatja.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Ezen a ponton a köteg üres, de a következő lépésben feltöltjük.

## 3. lépés: Minden támogatott kép hozzáadása egy mappából (rekurzívan)

Valószínűleg egy hierarchikus mappastruktúrával dolgozol—esetleg egy almappa ügyfelenként vagy hónaponként. Az `add_folder` metódus bejárja a fát helyetted, és betölti az összes olyan képet, amelyet képes olvasni.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Cseréld le a `"YOUR_DIRECTORY/scanned_forms/"`‑t a rendszereden lévő valós útvonalra. Ez a hívás után az `ocr_batch.file_paths` egy abszolút fájlnevekből álló listát tartalmaz, és a köteg pontosan tudni fogja, hány elemet kell feldolgoznia.

## 4. lépés: A nyomtatott szöveg felismerési módjának kiválasztása

Az `aocr` motor több módot támogat (kézírás, nyomtatott, vegyes). Mivel tiszta, nyomtatott űrlapokkal dolgozunk, állítsd be a módot ennek megfelelően. Ez a kis jelző drámai módon javíthatja a pontosságot, mivel a motor kihagyja a kézírásra jellemző nehéz heurisztikákat.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Miért fontos:** A nyomtatott szövegnek állandó alapvonalai és karakterformái vannak, ami lehetővé teszi az OCR modell számára, hogy szigorúbb karakterszótárakat alkalmazzon. Ha a módot “auto” állítod, alacsony felbontású beolvasásoknál extra zajt kaphatsz.

## 5. lépés: (Opcionális) AI post‑processzor csatolása

Ha a beolvasásaid elmosódottak, alacsony kontrasztúak vagy szokatlan betűtípusúak, egy AI post‑processzor megtisztíthatja a nyers OCR kimenetet, mielőtt továbbadnád a downstream rendszereknek. A `set_ai_postprocessor` metódus egy olyan objektumot vár, amely implementálja a `process(text: str) -> str` interfészt.

Alább egy minimális példa egy fiktív `SimpleCleaner` osztály használatával. Gyakorlatban beilleszthetsz egy HuggingFace transzformert, egy egyedi nyelvi modellt vagy akár szabály‑alapú helyesírás-ellenőrzőt.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Ha kihagyod ezt a lépést, a köteg egyszerűen a nyers OCR sztringeket adja vissza.

## 6. lépés: OCR futtatása az egész kötegen és az eredmények összegyűjtése

Most kezdődik a nehéz munka. A `run` metódus minden fájlon végigiterál, futtatja az OCR motort, átirányítja a kimenetet az opcionális AI post‑processzoron, és egy sztringlistát ad vissza—egy képenként.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Mivel a metódus egy egyszerű Python listát ad vissza, úgy kezelheted, mint bármely más gyűjteményt—tárolhatod, CSV‑be írhatod, vagy adatbázisba betáplálhatod.

## 7. lépés: Minden fájlútvonal megjelenítése a kinyert szöveg hosszával

Egy gyors ellenőrzésként írd ki, hány karakter került kinyerésre minden fájlból. Ha egy oldal üres vagy az OCR hibázik, a hossz `0` lesz.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

A tipikus kimenet így néz ki:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Egy `0` jelzés azonnal megmutatja, mely fájlok igényelnek második átnézést (lehet, hogy sérültek vagy egyáltalán nem képek).

## Gyakori szélsőséges esetek kezelése

### 1. Nem támogatott fájltípusok

Az `aocr` csendben kihagyja azokat a fájlokat, amelyeket nem tud dekódolni. Ha gyanítod, hogy PDF‑ek vagy BMP‑k is vannak keverve, szűrd ki őket előre:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Nagy kötegek és memóriahasználat

Több ezer nagy felbontású beolvasás futtatása felrobbanthatja a memóriahasználatot. Ennek mérséklésére dolgozz chunk‑okban:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Üres vagy alacsony kontrasztú oldalak

Ha egy oldal kevesebb, mint 10 karaktert ad vissza, érdemes lehet manuális felülvizsgálatra jelölni:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Teljes működő példa

Mindent egy helyre téve, itt egy szkript, amelyet másolj‑beilleszthetsz és azonnal futtathatsz. Mentsd el `batch_ocr.py`‑ként.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Futtasd a következővel:

```bash
python batch_ocr.py
```

Ha minden helyesen van beállítva, minden képhez egy sort látsz, amely a kinyert szöveg karakter számát jelzi.

## Gyakran Ismételt Kérdések

**Q: Működik ez PDF‑eken?**  
A: Nem „out‑of‑the‑box”. Az `aocr` csak raszteres képeket kezel. A PDF‑eket előbb konvertáld PNG/TIFF formátumba (pl. a `pdf2image` használatával).

**Q: Át tudom állítani a felismerési módot kézírásra?**  
A: Természetesen—csak cseréld le az `aocr.RecognitionMode.PRINTED`‑t `aocr.RecognitionMode.HANDWRITTEN`‑re. Lassabb lesz a futás, de jobb eredményt kapsz a kézírásos jegyzeteknél.

**Q: Mi van, ha többnyelvű támogatásra van szükségem?**  
A: A könyvtár nyelvi csomagokkal érkezik. Telepítsd a kívánt nyelvi modult (`pip install aocr-lang-fr` a francia nyelvhez, stb.) és állítsd be `ocr_batch.language = "fr"`‑t a futtatás előtt.

## Következő lépések és kapcsolódó témák

- **Párhuzamos feldolgozás:** Csomagold be a köteg végrehajtását egy `concurrent.futures.ThreadPoolExecutor`‑be, hogy több CPU magot használj.  
- **Eredmények tárolása:** Írd az `ocr_results`‑t CSV‑be vagy SQLite adatbázisba a további elemzésekhez.  
- **Felhő AI integráció:** Cseréld le a `SimpleCleaner`‑t egy HuggingFace transzformer modellre a csúcstechnológiás helyesírási javításhoz.  
- **aocr finomhangolása:** Ha egyedi betűkészleted van, nézd meg az `aocr.Trainer`‑t a nyomtatott mód pontosságának javításához.

---

Ennyi—most már egy szilárd

## Mit érdemes következőként tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Kép szövegének kinyerése Aspose OCR-rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Kép szövegének kinyerése OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Hogyan kötegeld az OCR képeket listával az Aspose.OCR .NET-ben](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}