---
category: general
date: 2026-06-25
description: Python OCR oktatóanyag, amely megmutatja, hogyan lehet szöveget kinyerni
  PNG fájlokból, szöveges képet olvasni, és képszöveget felismerni egy egyszerű, licencdíjmentes
  motor segítségével.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: hu
og_description: A Python OCR útmutató megmutatja, hogyan tölts be képet OCR-hez, hogyan
  nyerj ki szöveget PNG fájlokból, és hogyan ismerd fel a képen lévő szöveget néhány
  sor kóddal.
og_title: Python OCR útmutató – Szöveg kinyerése PNG‑ből
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Python OCR útmutató: Szöveg kinyerése PNG képekből'
url: /hu/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR bemutató – Szöveg kinyerése PNG képekből

Gondolkodtál már azon, hogy a **python ocr tutorial** hogyan tud egy nyugta képernyőképet szerkeszthető szöveggé alakítani? Nem vagy egyedül. Sok valós projektben gyorsan kell *read text image* fájlokat olvasni, és ha magad csinálod, az sokkal jobb, mint minden alkalommal a GUI‑ból másolgatni.  

Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be, hogyan **extracts text PNG** fájlokat, hogyan *load image for OCR*, és végül kiírja a *recognize image text* eredményt – mindezt egy ingyenes, csak értékelésre szánt OCR motorral. Nincs licenckulcs, nincs nehéz függőség – csak tiszta Python és néhány apró csomag.

## Mit tanulhatsz meg

- Hogyan telepítsd és importáld a könnyűsúlyú OCR könyvtárat.
- A pontos lépések a **load image for OCR** és a gyakori buktatók kezelése.
- Módszerek **read text image** fájlok különböző minőségben történő olvasására.
- Tippek a pontosság javításához, amikor **extract text png** fájlokat használsz.
- Hogyan jelenítsd meg a felismert karakterláncot, és opcionálisan írd ki a lemezre.

A tutorial végére egy újrahasználható szkriptet kapsz, amelyet bármely olyan projektbe beilleszthetsz, amelynek **recognize image text** funkcióra van szüksége valós időben. Nincs varázslat, csak tiszta kód és magyarázatok.

### Előfeltételek

- Python 3.8 vagy újabb (a könyvtár működik 3.7+ verzióval is, de a 3.8+ ajánlott).
- Alapvető ismeretek a pip‑ről és a virtuális környezetekről.
- `sample.png` nevű képfájl (vagy bármely tesztelni kívánt PNG), amely egy elérhető mappában van elmentve.

Ha bármelyik ismeretlennek tűnik, tarts egy perc szünetet, és állítsd be őket – higgy nekem, megéri.

---

## Python OCR Tutorial – A motor beállítása

Először is: szükségünk van egy OCR motor objektumra. A könyvtár, amelyet használni fogunk, egy apró wrapper egy natív OCR motor körül, amely azonnal működik értékelésre. Nem igényel licenckulcsot, ami a *python ocr tutorial*-t tökéletessé teszi gyors prototípusokhoz.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Miért fontos ez:** A motor létrehozása elszigeteli az OCR futtatókörnyezetet a kód többi részétől, lehetővé téve, hogy több képnél is újrahasználhasd anélkül, hogy minden alkalommal újra inicializálnád a nehéz erőforrásokat.

---

## Kép betöltése OCR‑hez – PNG fájl olvasása

Most, hogy a motor létezik, *load image for OCR* kell végrehajtanunk. A könyvtár `Image.load` metódusa elfogad egy útvonalat, és automatikusan dekódolja a PNG, JPEG, BMP és néhány egyéb formátumot.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tipp:** Ha a PNG‑d alfa csatornát tartalmaz, a könyvtár automatikusan eltávolítja azt. Azonban a legjobb eredmény érdekében a *read text image* feladatoknál tartsd a képet szürkeárnyalatos formában – ez csökkenti a zajt és felgyorsítja a felismerést.

---

## Kép szövegének felismerése – OCR motor futtatása

Miután a képobjektum készen áll, végre **recognize image text** hajtható végre. Ez a *python ocr tutorial* középpontja, és csak egy sor kódot igényel.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Mi történik a háttérben?** A motor egy sor előfeldolgozó szűrőt (kiegyenesítés, binarizálás) futtat, mielőtt a bitmapet egy több millió karakteren tanított neurális hálózatba táplálná. Ezért gyakran meglepően pontos kimenetet kapsz még alacsony felbontású PNG‑k esetén is.

---

## A kinyert szöveg megjelenítése és mentése

Az eredmény birtoklása nagyszerű, de valószínűleg szeretnéd megtekinteni vagy valahová elmenteni. A `result` objektum egy `text` attribútumot biztosít, amely a sima karakterlánc kimenetet tartalmazza.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Várható kimenet** (feltételezve, hogy a `sample.png` tartalmazza a „Hello, OCR!” szöveget):

```
Eval-mode result: Hello, OCR!
```

Ha olvashatatlan karaktereket kapsz a helyett, ellenőrizd a következő szekciót a gyakori javításokért.

---

## Gyakori problémák kezelése PNG szöveg kinyerésekor

Még a legjobb OCR motorok is elakadhatnak bizonyos képeknél. Az alábbiakban tipikus akadályok és azok megoldásai.

### 1. Alacsony kontraszt vagy sötét háttér

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Ferde szövegsorok

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Nem‑angol karakterek

Ha a PNG‑d ékezetes betűket vagy nem latin írásrendszert tartalmaz, inicializáld a motort a megfelelő nyelvi csomaggal:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Nagyon nagy képek

Egy 4000×3000 méretű PNG feldolgozása lassú lehet. Méretezd le, miközben megőrzöd az olvashatóságot:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Ezek a finomhangolások egy robusztus *python ocr tutorial* részei, amely a kedvező eseteken túl is működik.

---

## Teljes szkript – Egy‑fájl megoldás

Az alábbiakban a teljes, azonnal futtatható szkript található, amely tartalmazza az összes lépést és a megvitatott opcionális fejlesztéseket. Másold be a `ocr_extract.py` fájlba, és futtasd a `python ocr_extract.py` parancsot.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Futtasd:**  
```bash
python ocr_extract.py ./sample.png
```

Látni fogod a felismert karakterláncot a konzolon, és egy `sample_extracted.txt` fájl jön létre a kép mellett.

---

## Vizuális áttekintés

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alternatív szöveg:* *Python OCR tutorial diagram, amely bemutatja a folyamatot a kép betöltésétől OCR‑hez a szöveg PNG‑k kinyeréséig.*

---

## Következtetés

Épp most befejeztünk egy **python ocr tutorial**-t, amely bemutatja, hogyan *load image for OCR*, *recognize image text*, és végül **extract text png** fájlokat csak néhány Python parancs segítségével. A szkript teljesen működőképes, kezeli a gyakori szélsőséges eseteket, és bővíthető kötegelt feldolgozásra vagy többnyelvű támogatásra.

Készen állsz a következő kihívásra? Próbáld meg a motort PDF‑ek képpé konvertált változataival, kísérletezz különböző nyelvi csomagokkal, vagy integráld az OCR lépést egy Flask API‑ba, hogy a webalkalmazásod valós időben olvassa a feltöltött képernyőképeket. A *read text image* automatizálás lehetőségei gyakorlatilag végtelenek.

Van kérdésed vagy egy nehéz képed, amit nem tudsz feloldani? Írj egy megjegyzést alább, és közösen megoldjuk. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Szöveg kinyerése képből – OCR optimalizálás Aspose.OCR‑rel .NET‑hez](/ocr/english/net/ocr-optimization/)
- [Hogyan OCR‑eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}