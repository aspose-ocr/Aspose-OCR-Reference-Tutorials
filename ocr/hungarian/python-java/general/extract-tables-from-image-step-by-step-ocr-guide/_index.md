---
category: general
date: 2026-03-26
description: Képből táblázatok kinyerése és a kép táblázatfájllá konvertálása Python
  OCR használatával. Tanulja meg, hogyan töltsön be képet OCR-hez, olvassa be a táblázatokat
  és nyerje ki a táblázat adatait.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: hu
og_description: Képeken lévő táblázatok kinyerése Python OCR-rel. Ez az útmutató bemutatja,
  hogyan töltsd be a képet OCR-hez, olvasd ki a táblázatokat, és konvertáld őket egy
  elektronikus táblázatba.
og_title: Táblázatok kinyerése képből – Teljes OCR útmutató
tags:
- OCR
- Python
- Data Extraction
title: Táblázatok kinyerése képből – Lépésről‑lépésre OCR útmutató
url: /hu/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Táblázatok kinyerése képből – Teljes OCR útmutató

Valaha is szükséged volt **táblázatok kinyerése képből**, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok fejlesztő elakad, amikor egy PDF vagy képernyőfotó táblázatos adatokat tartalmaz, amelyeket szerkeszthető sorokká és oszlopokká kell alakítani. A jó hír? Néhány Python sor, egy megbízható OCR motorral párosítva, másodpercek alatt átalakíthatja a képet egy használható táblázattá.

Ebben az útmutatóban végigvezetünk a kép betöltésén, az OCR motor futtatásán és a táblázatok soronkénti kinyerésén. A végére **kép konvertálása táblázatba**, valamint a **ocr read tables** és **ocr extract table data** használatát is megmutatjuk a további feldolgozáshoz. Nincs rejtett varázslat, csak tiszta, futtatható kód, amit ma beilleszthetsz a projektedbe.

---

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következőkkel rendelkezel:

- **Python 3.9+** – a legújabb stabil kiadás a legjobb.
- Az **`ocr`** könyvtár (vagy bármely kompatibilis OCR SDK, amely elérhetővé teszi az `OcrEngine`, `Image` és a táblázatokhoz kapcsolódó metódusokat). Telepítsd a `pip install ocr‑sdk` paranccsal (cseréld ki a tényleges csomagnévre).
- Egy kép fájl (`.png`, `.jpg`, stb.), amely egy jól nyomtatható táblázatot tartalmaz.  
- Opcionális: **pandas**, ha a kinyert adatot közvetlenül CSV vagy Excel fájlba szeretnéd írni (`pip install pandas`).

Minden megvan? Remek – kezdjünk is bele.

---

## 1. lépés: Importáld az OCR SDK‑t és állítsd be a környezetet

Először is be kell hoznunk az OCR osztályokat a szkriptünkbe, és létrehozni egy kis segédfüggvényt, amely később a nyers táblázat adatot DataFrame‑mé alakítja.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Miért fontos:** Az `ocr` importálása hozzáférést biztosít az `OcrEngine`, `Imaging.Image` és a táblázat objektumokhoz, amelyeken iterálni fogunk. A `pandas` nem kötelező a kinyeréshez, de a **kép konvertálása táblázatba** részt jelentősen leegyszerűsíti.

---

## 2. lépés: Töltsd be a feldolgozni kívánt képet

Most már **betöltjük a képet az OCR‑hez**. Az SDK egy `Image` objektumot vár, ezért a fájl útvonalat a `Image.load()` segédfüggvénnyel fogjuk becsomagolni.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tipp:** Tartsd a képfájlokat egy dedikált mappában (`assets/` vagy `data/`) és használj relatív útvonalakat. Így a szkript könnyen hordozható marad különböző gépek között.

---

## 3. lépés: Futtasd a felismerési folyamatot

Miután a kép csatolva van, végre is mondhatjuk az motornak, hogy **ocr read tables**. A `recognize()` hívás egy eredményobjektust ad vissza, amely mindent tartalmaz, amit a motor felfedezett – szövegdobozok, sorok és, ami a legfontosabb számunkra, a táblázatok.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Miért ellenőrzünk:** Egyes képek zajosak lehetnek, vagy a táblázat szegélyei halványak, ami miatt a motor kimaradhatja őket. Egy figyelmeztetés naplózása korai visszajelzést ad anélkül, hogy a szkript összeomlana.

---

## 4. lépés: Kinyerés minden táblázat sorait és celláit

Itt kezdődik a valódi varázslat. Végigiterálunk minden észlelt táblázaton, kinyerjük minden sorát, majd minden cellájának szövegét. A belső listakomprehenszió rövid kódot eredményez, de mégis részletesen elmagyarázzuk a folyamatot.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Mi történik?**  

- `enumerate(..., start=1)` barátságos táblázatszámot ad a naplózáshoz.  
- `row_obj.get_cells()` visszaadja az egyes cellaobjektumokat; `cell.get_text()` lekéri az OCR‑dekódolt karakterláncot.  
- A sorokat a `rows_data`‑ba tároljuk, majd átadjuk a `pandas.DataFrame`‑nek, amely automatikusan igazítja az oszlopokat.  
- A `print` blokk tükrözi az **essential output**‑ot az eredeti kódrészletből, így azonnal ellenőrizheted az eredményt.

**Szélsőséges eset kezelése:** Ha egy sor celláinak száma eltér a többitől, a `pandas` a hiányzó helyeket `NaN`‑nel tölti fel. Később a DataFrame‑t megtisztíthatod `df.fillna('')`‑vel, ha üres karakterláncokat szeretnél.

---

## 5. lépés: Mentsd el a kinyert táblázatokat egy táblázatfájlba

Most, hogy van egy listánk DataFrame‑ekkel, az Excel munkafüzet (vagy CSV fájlok) létrehozása egy sétagalopp. Ezzel teljesül a **kép konvertálása táblázatba** cél.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Miért Excel?** A legtöbb üzleti felhasználó kedveli a `.xlsx` formátumot. Ha inkább CSV‑t szeretnél, cseréld le a ciklust `df.to_csv(f"table_{idx}.csv", index=False)`‑re.

---

## Teljes, futtatható szkript

Mindent összegezve, itt a komplett program, amelyet egyszerűen másolj be és futtass.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Várt konzolkimenet** (egy egyszerű 2×3-as táblázat esetén):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

A szkript mappájában megtalálod az `extracted_tables.xlsx` fájlt, minden táblázat egy saját munkalapon.

---

## Gyakran Ismételt Kérdések és Tippek

| Kérdés | Válasz |
|----------|--------|
| **Használhatok másik OCR könyvtárat?** | Természetesen. A minta ugyanaz marad: betöltés → felismerés → iterálás a `get_tables()` felett. Csak cseréld le az importot és az objektumneveket. |
| **Mi van, ha a képem zajos?** | Előfeldolgozd OpenCV‑vel (küszöbölés, kiegyenesítés) mielőtt az OCR motorhoz adnád. A zajcsökkentés gyakran javítja a **ocr extract table data** pontosságát. |
| **Telepítenem kell az `openpyxl`‑t?** | Igen, a `pandas` ezt a háttérben használja az Excel kimenethez. Telepítsd a `pip install openpyxl` paranccsal. |
| **Hogyan kezelem az egyesített cellákat?** | Néhány SDK kínál `cell.is_merged()` metódust; detektálhatod, és manuálisan terjesztheted az értéket a megadott tartományra. |
| **Kiválasztható, hogy csak bizonyos táblázatokat nyerjek ki?** | Szűrhetsz `table_obj.get_confidence()` alapján vagy a fejléc kulcsszavak ellenőrzésével a feldolgozás előtt. |

---

## Összegzés

Most már rendelkezel egy teljes, vég‑től‑végig megoldással a **táblázatok kinyerése képből**, az eredmény rendezett táblázatba konvertálásához, és akár több táblázat egyetlen képen való kezeléséhez. A szkript bemutatja, hogyan **load image for OCR**, **ocr read tables**, és **ocr extract table data**, miközben elég rugalmas marad a valós világ változásaihoz.

Mi a következő lépés? Próbáld ki az OCR motort egy PDF oldal képként renderelt változatával, vagy kísérletezz különböző nyelvekkel és betűtípusokkal. A DataFrame‑eket közvetlenül adatbázisba vagy jelentéskészítő eszközbe is továbbíthatod – a képzeleted szab határt.

Ha hasznosnak találtad ezt az útmutatót, oszd meg, csillagozd meg a SDK‑t tartalmazó repót, vagy írj kommentet a saját trükkjeiddel. Boldog kódolást, és legyenek a táblázataid mindig tökéletesen feldolgozva!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}