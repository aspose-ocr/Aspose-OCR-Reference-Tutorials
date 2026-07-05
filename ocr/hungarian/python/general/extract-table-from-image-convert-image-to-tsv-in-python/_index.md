---
category: general
date: 2026-07-05
description: Táblázat kinyerése képből Python OCR segítségével. Tanulja meg, hogyan
  nyerjen ki táblázatot, konvertálja a képet TSV formátumba, és sajátítsa el az OCR
  táblázat képek Python technikáit.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: hu
og_description: Táblázat kinyerése képből Python OCR-rel. Ez az útmutató bemutatja,
  hogyan lehet kinyerni a táblázatot, képet TSV formátumba konvertálni, és OCR táblázat
  képekhez Python eszközöket használni.
og_title: Képből táblázat kinyerése – Kép TSV-re konvertálása Pythonban
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Táblázat kinyerése képből – Kép konvertálása TSV formátumba Pythonban
url: /hu/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képből táblázat kinyerése – Kép konvertálása TSV-re Pythonban

Gondolkodtál már azon, hogyan lehet táblázatot kinyerni egy képből anélkül, hogy a hajadba ragadnál? Ebben az útmutatóban végigvezetünk **a táblázat** adatainak kinyerésén egy képről a `aocr` könyvtár segítségével, majd azt egy rendezett TSV fájlba mentjük. Nincs varázslat, csak néhány Python sor és egy kis AI‑alapú utófeldolgozás.

Ha valaha is megpróbáltál egy beolvasott számláról vagy képernyőképről táblázatot másolni‑beilleszteni, és csak egy összezavaró kusza lett belőle, akkor értékelni fogod, miért érdemes elsajátítani egy OCR‑alapú megközelítést. A végére képes leszel bármilyen táblázatot tartalmazó képet Pythonba betáplálni, és tiszta, tabulátorral elválasztott értékeket kapni, készen a táblázatkezelőkhöz vagy adatbázisokhoz.

---

## Amire szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

| Követelmény | Miért fontos |
|-------------|---------------|
| Python 3.9+ | Az `aocr` csomag a modern Python futtatókörnyezetekre céloz. |
| `aocr` könyvtár (`pip install aocr`) | Biztosítja az OCR motorját és az AI utófeldolgozót, amelyet használni fogunk. |
| Egy táblázatot tartalmazó képfájl (PNG, JPG, stb.) | A forrásadat, amelyből kinyerjük a táblázatot. |
| Opcionálisan: virtuális környezet | Elkülöníti a függőségeket – erősen ajánlott. |

Ezek előkészítése megakadályozza, hogy a útmutató közepén megszakadjon a munka.

---

## A függőségek telepítése

Először telepítsük az OCR eszközöket. Nyiss egy terminált és futtasd:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Ha jogosultsági hibákat kapsz, add hozzá a `--user` kapcsolót a `pip install` parancshoz, vagy használd a `pipx`‑et a globális telepítéshez.

---

## 1. lépés – Az OCR motor inicializálása

A motor a folyamat szíve. Gondolj rá úgy, mint a “agyra”, amely minden pixelt megvizsgál, és eldönti, melyik karakter hova tartozik.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Miért hozunk létre egy motor objektumot egyetlen függvényhívás helyett? Az engine objektum lehetővé teszi, hogy később egyedi utófeldolgozókat csatoljunk, így finomhangolhatjuk a kimenetet – ez elengedhetetlen, ha **ocr table image python** pontosságra van szükséged.

---

## 2. lépés – AI utófeldolgozó csatolása

Az `aocr` egy könnyű AI utófeldolgozót tartalmaz, amely megtisztítja a nyers OCR eredményeket, miközben megőrzi a cellahatárokat. Nincs szükség extra argumentumokra, így a kód tiszta marad.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Ha kihagyod ezt a lépést, még mindig kapsz nyers szöveget, de a táblázat szerkezete zajos lesz – mintha egy táblázat minden cellája egy rejtély lenne. Az utófeldolgozó végzi a nehéz munkát, hogy a szöveget az eredeti rácshoz igazítsa.

---

## 3. lépés – Töltsd be a táblázat képet

Bármilyen útvonalról betölthetsz képet, de a tisztaság kedvéért egy helyőrző könyvtárat használunk. Cseréld le a `"YOUR_DIRECTORY/invoice_table.png"`‑t a saját fájlod tényleges útvonalára.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Megjegyzés:** Az `aocr.Image` automatikusan felismeri a képformátumot és normalizálja a színcsatornákat, így nem kell előfeldolgozni a fájlt, hacsak nem súlyosan sérült.

---

## 4. lépés – Strukturált OCR végrehajtása

Most a motor beolvassa a képet, és egy nyers táblázat objektumot ad vissza. Ez az objektum sorokat, oszlopokat és minden cellához tartozó nyers szöveget tartalmaz.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Miért használjuk a `recognize_structured`‑t egy általános `recognize` hívás helyett? A strukturált változat megpróbálja meghatározni a sor/oszlop határokat, így egy mátrix‑szerű eredményt kapunk, amely sokkal könnyebben konvertálható TSV‑re később.

---

## 5. lépés – Az adatok tisztítása az AI utófeldolgozóval

Az utófeldolgozó futtatása finomítja a nyers kimenetet: eltávolítja a felesleges karaktereket, egyesíti a szétválasztott darabokat, és biztosítja, hogy minden cella szövege helyesen legyen igazítva.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Ha megnézed a `processed_table.table`‑t, egy sorlistát látsz, ahol minden sor egy `Cell` objektumok listája. Minden `Cell` rendelkezik egy `.text` attribútummal, amely a megtisztított karakterláncot tartalmazza.

---

## 6. lépés – A táblázat exportálása TSV‑ként

Az utolsó lépés a feldolgozott adat TSV (tab‑separated values) fájlba konvertálása – pontosan amire szükséged van, ha **convert image to TSV** szeretnél Excelhez vagy Google Sheets‑hez.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

A script futtatása minden sort kiír a konzolra (ha úgy szeretnéd), és egy tiszta TSV fájlt hoz létre, amelyet bármely táblázatkezelő program megnyithat.

### Gyors ellenőrzés

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

A kimenetnek így kell kinéznie:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Ha a kimenet összekuszáltnak tűnik, ellenőrizd a kép minőségét (élesség, kontraszt), és fontold meg az OCR motor beállításainak finomhangolását – a `engine.set_config(...)` segítségével módosíthatod a nyelvi modelleket és a megbízhatósági küszöböket.

---

## Gyakori edge case‑ek kezelése

| Helyzet | Javasolt megoldás |
|-----------|-------------------|
| **Ferde kép** | Előre forgasd a képet a `Pillow` (`Image.rotate`) segítségével, mielőtt az `aocr`‑nek adnád. |
| **Alacsony kontraszt** | Alkalmazz hisztogram kiegyenlítést (`cv2.equalizeHist`) a olvashatóság növeléséhez. |
| **Egyesített cellák** | Utófeldolgozd a TSV‑t, hogy a cellákat ismert határolók alapján szétválaszd, vagy használd a `merge_cells=False` flag‑et, ha elérhető. |
| **Többoldalas PDF‑ek** | Először minden oldalt konvertálj képpé (`pdf2image`), majd futtasd a pipeline‑t egy ciklusban. |

Ezekkel a finomításokkal a **ocr table image python** munkafolyamatod robusztus marad a különféle forrásanyagok esetén.

---

## Teljes script – Egy‑állomásos megoldás

Az alábbiakban a teljes, azonnal futtatható script található, amely összegyűjti a fent tárgyalt lépéseket. Mentsd `extract_table.py` néven, és futtasd `python extract_table.py`‑vel.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Kép szövegének kinyerése Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Táblázat kinyerése képből Aspose.OCR‑rel .NET‑hez](/ocr/english/net/text-recognition/recognize-table/)
- [Szöveg kinyerése képből téglalapok előkészítésével OCR‑ban](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}