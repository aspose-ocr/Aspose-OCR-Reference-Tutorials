---
category: general
date: 2026-01-12
description: Hogyan végezzünk OCR-t gyorsan és pontosan. Tanulja meg, hogyan futtasson
  OCR-t dokumentumon, hogyan nyerjen ki szöveget TIFF-ből, hogyan töltsön be képet
  OCR-hez, és hogyan állítsa be az OCR nyelvet Pythonban.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: hu
og_description: Hogyan végezzünk OCR-t Pythonban. Ez az útmutató megmutatja, hogyan
  futtassunk OCR-t dokumentumon, hogyan nyerjünk ki szöveget TIFF-ből, hogyan töltsünk
  be képet OCR-hez, és hogyan állítsuk be az OCR nyelvét.
og_title: Hogyan végezzünk OCR-t egy TIFF dokumentumon – Teljes útmutató
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk OCR-t egy TIFF dokumentumon – Lépésről lépésre útmutató
url: /hu/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t egy TIFF dokumentumon – Teljes útmutató

Valaha is elgondolkodtál már **hogyan végezzünk OCR-t** egy beolvasott TIFF fájlon anélkül, hogy órákat töltenél a megfelelő könyvtár keresésével? Nem vagy egyedül. Sok fejlesztő akad el, amikor szöveget kell kinyerni tiff képekből, különösen, ha a teljesítmény és a nyelvi beállítások fontosak.

Ebben az oktatóanyagról végigvezetünk minden szükséges lépésen: az OCR csomag telepítésétől, a kép betöltéséig OCR-hez, az OCR nyelv beállításáig, egészen a **run OCR on document** végrehajtásáig és a tiszta szöveg kinyeréséig. A végére egy kész‑futtatható szkriptet kapsz, amelyet bármely projektbe beilleszthetsz.

> **Pro tip:** Míg a példa egy általános `ocr` modult használ, ugyanazok a koncepciók alkalmazhatók a Tesseract, EasyOCR vagy bármely modern OCR motorra, amely Python API-t biztosít.

---

## Amire szükséged lesz

- Python 3.8+ (bármely friss verzió működik)
- Egy OCR könyvtár, amely biztosítja az `OcrEngine` osztályt (a példa egy fiktív `ocr` csomagot használ; cseréld le a sajátodra)
- Egy többoldalas TIFF fájl, amelyet feldolgozni szeretnél (ezt `big_document.tif`‑nek hívjuk)
- Egy gép, amely legalább 4 CPU maggal rendelkezik, ha szál számot szeretnél beállítani

Nincs külső szolgáltatás, nincs felhő kulcs – csak helyi kód, amely másodpercek alatt fut.

![hogyan végezzünk OCR-t példa](/images/ocr-example.png "hogyan végezzünk OCR-t egy TIFF dokumentumon")

*Kép alt szöveg: hogyan végezzünk OCR-t egy TIFF dokumentumon – a kinyert szöveg előnézete.*

## 1. lépés: Az OCR könyvtár telepítése és importálása

Először is: szerezd be a könyvtárat a gépedre. A legtöbb OCR csomag a PyPI-n érhető, így egy egyszerű `pip install` megoldja a feladatot.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Most importáld a szükséges osztályokat. Ha Tesseract‑ot használsz, az import sor más lesz, de a kód többi része változatlan marad.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Miért fontos ez:* A megfelelő szimbólumok korai importálása megakadályozza a névtérütközéseket később, és olvashatóbbá teszi a szkriptet.

## 2. lépés: Az OCR motor létrehozása és konfigurálása (OCR nyelv beállítása)

A motor konfigurálása során **set OCR language** a pontos felismeréshez. Az angol az alapértelmezett, de egyetlen sorral átválthatsz francia, német vagy akár többnyelvű módra.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Miért 4 szál?** A legtöbb modern laptop legalább négy maggal rendelkezik, és a szálak számának korlátozása megakadályozza, hogy az OCR folyamat az egész gépet leterhelje – különösen hasznos, ha a szkript megosztott szerveren fut.

Ha más nyelvre van szükséged, egyszerűen cseréld le a `ocr.Language.ENGLISH`‑t `ocr.Language.FRENCH`, `ocr.Language.SPANISH` stb. értékre.

## 3. lépés: Kép betöltése OCR-hez (Load Image for OCR)

Most **load image for OCR**. A `Image.load` metódus beolvassa a TIFF fájlt a memóriába, automatikusan kezelve a többoldalas dokumentumokat.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Külön eset:* Ha a fájl hatalmas, elfogyhat a RAM. Ebben az esetben fontold meg, hogy egy oldalt töltesz be egyszerre a `Image.load_page(page_number)`‑vel (ha a könyvtár támogatja).

## 4. lépés: OCR futtatása a dokumentumon

A motor készen áll és a kép betöltve, itt az ideje a **run OCR on document** végrehajtásának. A `process` metódus elvégzi a nehéz munkát és egy eredményobjektumot ad vissza.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

A háttérben a motor a képet szövegrészekre bontja, futtatja a felismerő modellt, és összefűzi az eredményeket. A hívás blokkoló, vagyis a szkript addig vár, amíg a teljes TIFF feldolgozásra kerül – tökéletes kötegelt feladatokhoz.

## 5. lépés: Szöveg kinyerése a TIFF‑ből és a kimenet ellenőrzése

Végül **extract text from tiff** a `text` attribútum elérésével a eredményből. Nyomtassuk ki az első 200 karaktert gyors ellenőrzésként.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Várható kimenet (példa):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Ha a teljes szövegre van szükséged, egyszerűen használd az `ocr_result.text`‑et. A további feldolgozáshoz érdemes lehet `.txt` fájlba írni:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

## Teljes működő példa

Összegezve, itt egy kész‑futtatható szkript. Cseréld le a helyőrző csomagnevet arra, amelyet valójában telepítettél.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Futtasd a szkriptet a következővel:

```bash
python ocr_tiff_example.py
```

A konzolon egy előnézetet kell látnod, valamint egy `extracted_text.txt` nevű fájlt, amely a teljes átiratot tartalmazza.

## Gyakori kérdések és külön esetek

- **Mi van, ha a TIFF több oldalt tartalmaz?**  
  A legtöbb OCR motor belsőleg minden oldalt külön képként kezel. Az `ocr_result.text` új sort tartalmaz az oldalak között. Ha oldalankénti kezelést igényelsz, iterálj a `Image.load_page(page_number)`‑vel.

- **Feldolgozhatok PNG‑t vagy JPEG‑t TIFF helyett?**  
  Természetesen. A `Image.load` metódus általában bármely, a Pillow vagy az alaprendszer által támogatott formátumot elfogad. Csak változtasd meg a fájl kiterjesztését.

- **A szövegem összezavarodott – változtassak nyelvet?**  
  Igen. A `set OCR language` lépés kulcsfontosságú a nem angol dokumentumoknál. Győződj meg róla, hogy a nyelvi csomag telepítve van (pl. `tesseract‑lang‑fra` a franciához).

- **Elfogy a memória?**  
  Csökkentsd a `set_memory_limit` értéket vagy dolgozd fel az oldalakat egyesével. Néhány motor lehetővé teszi a kép felbontásának csökkentését a felismerés előtt.

## Összegzés

Ezzel elkészült egy tömör, teljesen működő útmutató a **how to perform OCR** egy TIFF fájlra Python használatával. Kitértük a könyvtár telepítését, a motor konfigurálását (beleértve a **set OCR language**‑t), a **load image for OCR**‑t, a **run OCR on document**‑t, és végül a **extract text from tiff**‑et.  

Nyugodtan kísérletezz: állítsd be a szálak számát, válts nyelvet, vagy irányítsd az OCR kimenetet egy természetes nyelvi feldolgozási csővezetékbe. A lehetőségek határtalanok, ha már elsajátítottad az alapokat.

Van még kérdésed? Írj egy megjegyzést alább, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}