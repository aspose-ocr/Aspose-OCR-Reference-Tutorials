---
category: general
date: 2026-04-26
description: Hogyan végezz kötegelt OCR-t a dokumentumaidon és nyerj ki szöveget a
  beolvasott képekből Pythonban. Tanulj meg lépésről‑lépésre kötegelt feldolgozást
  az OcrEngine segítségével JSON kimenethez.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: hu
og_description: Hogyan végezzünk kötegelt OCR‑t a beolvasott fájlokon, és egyetlen
  szkriptben nyerjünk ki szöveget a beolvasott anyagokból. Teljes kód, tippek és szélsőséges
  esetek kezelése.
og_title: Hogyan végezzünk tömeges OCR-t – Gyors Python útmutató
tags:
- OCR
- Python
- Automation
title: Hogyan végezzünk kötegelt OCR-t – Hatékony szövegkinyerés szkennelésekből
url: /hu/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t – Szöveg kinyerése a beolvasott dokumentumokból hatékonyan

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR-t** egy hegy óriási beolvasott PDF-en anélkül, hogy elveszítenéd a józan eszed? Nem vagy egyedül – a fejlesztők állandóan kérdezik, *„Hogyan tudok szöveget kinyerni a beolvasott dokumentumokból egyetlen lépésben?”* A jó hír, hogy néhány Python sor átalakíthatja ezt a fáradságos feladatot egy sima, automatizált folyamatba.  

Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható megoldáson, amely **kinyeri a szöveget a beolvasott dokumentumokból**, JSON‑ként menti az eredményeket, és a végén egy gyors ellenőrzést biztosít. Nincs külső szolgáltatás, nincs varázslat – csak tiszta Python, az `OcrEngine` osztály, és egy kis mappakezelés.

## Mit fogsz megtanulni

- Egy teljesen működő szkript, amely **kötegelt OCR‑t** végez bármely képmappán.  
- Világos magyarázatok arra, *miért* létezik az egyes sor, nem csak arra, *mit* csinál.  
- Tippek üres mappák, nem‑képfájlok és nagy kötegek kezelésére.  
- Egy módszer annak ellenőrzésére, hogy a JSON‑kimenet valóban tartalmazza-e a kinyert szöveget.

### Előfeltételek (a legszükségesebb)

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.8+ | Modern szintaxis és típusjelölések |
| `OcrEngine` library (or a compatible wrapper) | Az OCR alapfunkcionalitása |
| A directory with scanned image files (PNG, JPG, TIFF) | Bemeneti adatok |
| Write permissions for the output folder | JSON eredmények mentése |

Ha már megvannak ezek, nagyszerű – merüljünk el.

![hogyan kötegelt OCR munkafolyamat](image-placeholder.png){alt="hogyan kötegelt OCR munkafolyamat"}

## 1. lépés – Az OCR motor inicializálása (hogyan kötegelt OCR)

Mielőtt bármit feldolgoznánk, szükségünk van egy OCR motor példányra. Gondolj rá úgy, mint egy „agyra”, amely minden képet beolvas és szöveget ad vissza. Egyszeri inicializálása és a teljes köteg során újra‑használata a leghatékonyabb mintázat.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Miért használjuk újra ugyanazt a példányt?**  
> Új motor létrehozása minden egyes fájlhoz újra és újra betöltené a nehéz modelleket a memóriába, ami drámaian lelassítaná a köteget. Egyetlen példány a modellt a RAM‑ban tartja, és lehetővé teszi, hogy több ezer képet dolgozz fel anélkül, hogy jelentős lassulást észlelnél.

## 2. lépés – A beolvasott fájlok mappájának megadása (szöveg kinyerése a beolvasott dokumentumokból)

A beolvasott fájlok valahol a lemezen vannak. Mondjuk meg a szkriptnek, hol találja meg őket. Az abszolút útvonalak használata elkerüli a „fájl nem található” meglepetéseket, ha a szkriptet más munkakönyvtárból indítják.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro tipp:**  
> Ha Windows‑on vagy, a perjel (`/`) tökéletesen működik az `os.path.abspath`‑szal, így nem kell a visszaperjeleket (`\`) escape‑elned.

## 3. lépés – Válaszd ki, hová kerüljenek a JSON eredmények

Valószínűleg szeretnél egy rendezett mappát az OCR eredményeknek. A kimenet elkülönítése a forrástól megkönnyíti a későbbi takarítást vagy a JSON egy másik folyamatba való betáplálását.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Miért hozd létre a mappát programozottan?**  
> Ez garantálja, hogy a szkript nem omlik össze, ha a könyvtár hiányzik, és az `exist_ok=True` idempotens műveletet biztosít – a szkriptet többször is futtathatod hibák nélkül.

## 4. lépés – A kötegelt folyamat futtatása (hogyan kötegelt OCR)

Most jön a lényeg: a `ocr_engine` megmondása, hogy járja be az `input_dir` minden fájlját, futtassa az OCR‑t, és a JSON‑t az `output_dir`‑be írja. A `format="json"` jelző azt mondja a motornak, hogy a eredményt egy strukturált módon sorosítsa, amit a downstream eszközök szeretnek.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Mi történik a háttérben?

1. **Fájl felfedezés** – A motor rekurzívan bejárja az `input_folder`‑t, figyelmen kívül hagyva a rejtett fájlokat.  
2. **Fájl validáció** – Csak a támogatott képkiterjesztések (`.png`, `.jpg`, `.tif`, stb.) kerülnek az OCR modellhez.  
3. **OCR végrehajtás** – Minden képet elküld a OCR motor, a szöveg, a megbízhatósági pontszámok és az elrendezési adatok rögzítésre kerülnek.  
4. **JSON sorosítás** – Az eredmény egy azonos alappal, de `.json` kiterjesztéssel rendelkező fájlba íródik az `output_folder`‑ben.

> **Szélsőséges esetek kezelése:**  
> - **Üres mappa:** A motor naplózza a „No files found” üzenetet, és elegánsan visszatér.  
> - **Sérült kép:** Kihagyja a fájlt, egy `batch_errors.log` bejegyzésben rögzíti a hibát, és folytatja.  
> - **Nagy köteg (10 000+ fájl):** A memóriahasználat alacsony marad, mivel minden képet önállóan dolgoz fel.

## 5. lépés – A konverzió befejezésének megerősítése

Egy egyszerű `print` utasítás azonnali visszajelzést ad a konzolon. Gyártási folyamatoknál ezt helyettesítheted egy naplózási hívással vagy e‑mail értesítéssel.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Amikor látod ezt a sort, nyugodtan ellenőrizheted a `json_output` mappát. Minden JSON fájl nagyjából így fog kinézni:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Most már betáplálhatod ezeket a JSON fájlokat egy adatbázisba, keresőindexbe vagy bármilyen downstream analitikai eszközbe.

## Gyakran Ismételt Kérdések (és gyors válaszok)

**Q: Mi van, ha PDF‑eket kell feldolgozni képek helyett?**  
A: Először minden PDF oldalt konvertálj képpé (pl. a `pdf2image` használatával), majd helyezd a keletkezett PNG/JPG fájlokat az `input_dir`‑be. A kötegelt OCR logika változatlan marad.

**Q: Át tudom-e állítani a kimeneti formátumot egyszerű szövegre?**  
A: Természetesen. Cseréld le a `format="json"`‑t `format="txt"`‑re, és a motor egy `.txt` fájlt ír, amely csak a kinyert szöveget tartalmazza.

**Q: A beolvasott fájlok több alkönyvtárban vannak – a szkript rekurzívan bejárja őket?**  
A: Igen. A `batch_process` alapértelmezés szerint bejárja a könyvtárfát. Ha lapos kimenetet szeretnél, állítsd `flatten=True`‑ra (ha a könyvtár támogatja), vagy utólag dolgozd fel a JSON fájlneveket.

**Q: Hogyan kezeljem a nem latin írásrendszereket?**  
A: Inicializáld az `OcrEngine`‑t egy nyelvi paraméterrel, pl. `OcrEngine(lang="spa+eng")`. Maga a kötegelt ciklusnak nincs szüksége változtatásra.

## Pro tippek és gyakori buktatók

- **A köteg mérete számít:** Ha CPU‑csúcsokat észlelsz, lassítsd le a folyamatot egy egyszerű `time.sleep(0.1)` hívással a fájlok között.  
- **Naplózás:** Cseréld le a `print` hívást a Python `logging` moduljára, hogy időbélyegeket és hibaszinteket rögzíts.  
- **Fájlnév-ütközések:** Ha két beolvasott fájl ugyanazzal az alappal rendelkezik, de külön alkönyvtárban van, a JSON fájlok felülírják egymást. Adj egy hash‑t a relatív útvonalhoz a kimeneti névhez, hogy elkerüld ezt.  
- **Memóriaszivárgások:** Egyes OCR backendek natív erőforrásokat tartanak fenn. Hívd meg a `ocr_engine.close()`‑t a szkript végén, ha a könyvtár biztosít takarítási metódust.

## Teljes szkript – Kész a másoláshoz és beillesztéshez

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Várt konzol kimenet**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Ellenőrizheted a JSON‑t, ha megnyitsz bármelyik fájlt a `json_output`‑ban egy szövegszerkesztővel, vagy betöltöd Pythonban:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

A nyers OCR‑kivont szöveget kell látnod a konzolon.

## Összegzés

Már lefedtük, **hogyan végezzünk kötegelt OCR‑t** egy teljes könyvtár beolvasott képeken, és **kinyerjük a szöveget a beolvasott dokumentumokból** tiszta, gép‑olvasható JSON fájlokba. A megközelítés szándékosan egyszerű: egyszer állítsd be a motort, mutasd rá egy mappára, és hagyd, hogy a könyvtár elvégezze a nehéz munkát. Innen tovább:

- Plug the JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}