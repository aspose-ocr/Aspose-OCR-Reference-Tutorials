---
category: general
date: 2026-06-19
description: Képek szövegének kinyerése Pythonban egy egyszerű OCR motorral. Tanulja
  meg, hogyan konvertálja a beolvasott képeket szöveggé, hogyan ismerje fel a képeken
  lévő szöveget, és hogyan listázza hatékonyan a képfájlokat Pythonban.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: hu
og_description: Szöveg kinyerése képekből Pythonban egy könnyű OCR motorral. Ez az
  útmutató megmutatja, hogyan konvertálhatod a beolvasott képeket szöveggé, hogyan
  ismerheted fel a szöveget a képekről, és hogyan listázhatod a képfájlokat Pythonban
  néhány lépésben.
og_title: Szöveg kinyerése képekből Pythonban – Teljes kötegelt OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Képek szövegének kinyerése Pythonban – Teljes kötegelt OCR útmutató
url: /hu/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képek szövegének kinyerése Pythonban – Teljes kötegelt OCR útmutató

Valaha is szükséged volt **képek szövegének kinyerésére**, de nem tudtad, hol kezdjed? Nem vagy egyedül – a fejlesztők folyamatosan szembesülnek a beolvasott PDF‑ek, fényképezett számlák vagy képernyőképek kereshető szöveggé alakításának kihívásával. Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **konvertálhatod a beolvasott képeket szöveggé**, hogyan ismerheted fel a szöveget a képekről, és még **list image files python**‑stílusban is felsorolhatod a képfájlokat. A végére egy újrahasználható szkriptet kapsz, amely egy egész mappát egy lépésben feldolgoz.

Mindent lefedünk, amire szükséged lehet: a szükséges könyvtárakat, hogy miért fontos minden egyes lépés, a szélsőséges esetek kezelését, és egy kis hibakeresést. Nincs szükség külső dokumentációk keresgélésére; az alábbi kód önmagában áll, és a magyarázatok a “hogyan” *és* a “miért” kérdésekre válaszolnak. Vedd elő a kedvenc IDE‑det, és kezdjünk bele.

---

## Mit fogsz építeni

- Inicializálod az OCR‑motort (az illusztrációhoz a `ocr` csomagot használjuk).
- Beolvasod egy könyvtár tartalmát és **list image files python**‑stílusban felsorolod a képfájlokat, szűrve a PNG, JPG és TIFF formátumokat.
- **Kötegelt OCR** műveletet futtatsz az összes megtalált képen.
- Kiírod az egyes fájlokhoz kinyert szöveget, egyértelműen címkézve.

> **Pro tipp:** Ha nincs telepítve a `ocr` könyvtár, helyettesítheted `pytesseract`‑tel néhány kisebb módosítással – a fő logika változatlan marad.

---

## Előfeltételek

- Python 3.8+ (a szkript f‑stringeket és típusjelöléseket használ).
- Egy OCR könyvtár, amely egy `OcrEngine`‑t biztosít a `recognize_batch` metódussal. Ebben az útmutatóban egy fiktív `ocr` csomagot feltételezünk, de a minta valódi könyvtárakkal is működik.
- Egy mappa, amely a feldolgozni kívánt képfájlokat tartalmazza (`.png`, `.jpg`, `.tif`).

---

## 1. lépés – A szükséges modulok telepítése és importálása

Először győződj meg róla, hogy az OCR csomag elérhető. Ha valós könyvtárat, például `pytesseract`‑et használsz, cseréld le az importot ennek megfelelően.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Miért fontos:** Az `os` importálása platformfüggetlen útvonalkezelést biztosít, míg a `typing.List` segíti az IDE‑k automatikus kiegészítését és a jövőbiztosságot.

---

## 2. lépés – **Extract Text from Images**: Az OCR‑motor inicializálása

A motor létrehozása az első lépés minden OCR feladat felé. Emellett a nyelvet automatikus felismerésre állítjuk, hogy a motor kevert nyelvű dokumentumokkal is tudjon dolgozni.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Magyarázat:** A motor létrehozását egy függvénybe szervezve a kód moduláris marad. Ha később DPI‑t vagy OCR‑módot kell módosítanod, csak ezen a helyen kell változtatnod.

---

## 3. lépés – **List Image Files Python**: Fájlok összegyűjtése egy könyvtárból

Most meg kell találnunk minden képet, amelyet feldolgozni szeretnénk. Az alábbi listakomprehenszió egy gyakori “list image files python” mintát tükröz.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Szélsőséges esetek kezelése:** A függvény figyelmen kívül hagyja az alkönyvtárakat (később hozzáadhatsz rekurziót) és automatikusan kiszűri a rejtett fájlokat, mivel azok általában nem végződnek a támogatott kiterjesztésekkel.

---

## 4. lépés – **Convert Scanned Images to Text**: Kötegelt OCR futtatása

A legtöbb OCR könyvtár biztosít egy kötegelt metódust, amely sokkal gyorsabb, mint egyesével feldolgozni a képeket. Így hívjuk meg.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Miért kötegelt?** Az összes kép egyszerre történő elküldése csökkenti a terhelést (pl. a OCR modell többszöri betöltése) és gyakran jobb CPU/GPU kihasználtságot eredményez.

---

## 5. lépés – **Recognize Text from Pictures**: Az eredmények megjelenítése

Végül végigiterálunk a párosított fájlneveken és OCR‑eredményeken, és minden képhez tiszta fejlécet nyomtatunk.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tipp:** A `strip()` eltávolítja a vezető/utólagos szóközöket, amelyeket az OCR gyakran hozzáad.

---

## Teljes szkript – Összeállítás egyben

Az alábbiakban a teljes, futtatható program található. Mentsd el `batch_ocr.py` néven, és futtasd `python batch_ocr.py <your_folder>` paranccsal.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Várható kimenet

Tegyük fel, hogy a mappa tartalmazza az `invoice1.png` és a `receipt.jpg` fájlokat, akkor a következőhöz hasonló kimenetet láthatsz:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Minden blokk egyértelműen fel van címkézve, ami megkönnyíti a további feldolgozást (pl. adatbázisba mentés).

---

## Gyakori hibák kezelése

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Nem jelenik meg szöveg** | Az OCR nyelv nem lett felismert, vagy a kép túl alacsony kontrasztú. | Kényszerítsd a nyelvet (`engine.language = ocr.Language.English`) vagy előfeldolgozd a képeket (növeld a kontrasztot). |
| **Memóriahiba nagy kötegeknél** | A motor egyszerre próbál betölteni minden képet. | Oszd fel a `image_files` listát darabokra (`batch_size = 20`), és hívd meg többször a `recognize_batch`‑et. |
| **Nem támogatott fájlformátum** | `.gif` vagy `.bmp` fájlt adtál hozzá. | Bővítsd a `supported_exts` tuple‑t, vagy konvertáld a képeket PNG/JPG formátumba előre. |
| **Unicode torzulás** | Az OCR bájtokat ad vissza szöveg helyett. | Győződj meg róla, hogy az OCR könyvtár Unicode‑t ad vissza (`result.text.decode('utf‑8')` szükség esetén). |

---

## A munkafolyamat bővítése

Most, hogy **képek szövegének kinyerését** megvalósítottad, gondolj ezekre a következő lépésekre:

- **Export CSV‑be** – Írd ki minden fájlnevet és a kinyert szöveget egy táblázatba elemzési célokra.
- **Párhuzamos feldolgozás** – Használd a `concurrent.futures.ThreadPoolExecutor`‑t több köteg egyidejű kezeléséhez.
- **Integráció felhő‑OCR‑vel** – Cseréld le a helyi motort Google Vision vagy Azure OCR megoldásra a komplex elrendezések jobb pontossága érdekében.
- **Képelőfeldolgozás hozzáadása** – A Pillow vagy OpenCV könyvtárak segítségével kiegyenesítheted, zajtalaníthatod vagy küszöbölheted a képeket OCR előtt, ezáltal javítva az eredményeket.

Mindezek az ötletek természetesen ugyanazokat a magfunkciókat használják, amelyeket felépítettünk, így nem kell a nulláról kezdened.

---

## Összegzés

Áttekintettük a **képek szövegének kinyerését** Pythonban, lefedve mindent a **list image files python**‑ról a **recognize text from pictures**‑ig, végül a **convert scanned images to text**‑ig egy rendezett kötegben. A szkript szándékosan egyszerű, mégis elég rugalmas ahhoz, hogy alapot nyújtson nagyobb projektekhez – legyen szó számlák digitalizálásáról, kereshető archívum építéséről vagy adatkinyerő csővezetékek üzemeltetéséről.

Próbáld ki, finomítsd az előfeldolgozási lépéseket, és figyeld, ahogy az OCR pontossága javul. Ha problémába ütközöl, nézd meg újra a “Gyakori hibák kezelése” táblázatot; a legtöbb gondot egy apró konfigurációs változtatás oldja meg.

Készen állsz a következő kihívásra? Próbálj meg egy PDF‑kép konverziós lépést hozzáadni a `pdf2image` használatával, majd ezeket a képeket közvetlenül a meglévő csővezetékbe táplálni. A lehetőségek határtalanok, ha az OCR‑t a Python gazdag ökoszisztémájával kombinálod.

Boldog kódolást, és legyen a szöveged mindig olvasható!

## Mit érdemes még megtanulnod?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}