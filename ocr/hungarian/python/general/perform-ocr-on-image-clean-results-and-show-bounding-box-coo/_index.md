---
category: general
date: 2026-03-28
description: Képen OCR-t hajtson végre, és kapjon tiszta szöveget a körülhatároló
  doboz koordinátáival. Tanulja meg, hogyan lehet kinyerni az OCR-t, megtisztítani
  azt, és lépésről lépésre megjeleníteni az eredményeket.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: hu
og_description: Képen OCR-t végez, megtisztítja a kimenetet, és egy tömör útmutatóban
  megjeleníti a körülhatároló doboz koordinátáit.
og_title: OCR végrehajtása képen – Tiszta eredmények és határoló dobozok
tags:
- OCR
- Computer Vision
- Python
title: Kép OCR végrehajtása – Tiszta eredmények és a körülhatároló doboz koordinátáinak
  megjelenítése
url: /hu/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép OCR végrehajtása – Tiszta eredmények és a körülhatároló doboz koordináták megjelenítése

Volt már, hogy **képen OCR-t kellett végrehajtani**, de csak rendezetlen szöveget kaptál, és nem tudtad, hol helyezkedik el az egyes szavak a képen? Nem vagy egyedül. Sok projektben – számlák digitalizálása, nyugták beolvasása vagy egyszerű szövegkinyerés – a nyers OCR kimenet csak az első akadály. A jó hír? Tisztíthatod ezt a kimenetet, és azonnal megtekintheted az egyes régiók körülhatároló doboz koordinátáit anélkül, hogy rengeteg sablonkódot kellene írnod.

Ebben az útmutatóban végigvezetünk a **OCR kinyerésének**, egy **OCR tisztító** post‑processzor futtatásának, és végül minden tisztított régió **körülhatároló doboz koordinátáinak** megjelenítésének lépésein. A végére egyetlen, futtatható szkriptet kapsz, amely egy homályos fényképet rendezett, strukturált szöveggé alakít, készen állva a további feldolgozásra.

## Amire szükséged lesz

- Python 3.9+ (az alábbi szintaxis 3.8 és újabb verziókon is működik)
- Egy OCR motor, amely támogatja a `recognize(..., return_structured=True)` hívást – például a példakódban szereplő fiktív `engine` könyvtárat. Cseréld le Tesseract-ra, EasyOCR-ra vagy bármely SDK-ra, amely régióadatokat ad vissza.
- Alapvető ismeretek a Python függvényekről és ciklusokról
- Egy képfájl, amelyet be szeretnél olvasni (PNG, JPG, stb.)

> **Pro tipp:** Ha Tesseract-ot használsz, a `pytesseract.image_to_data` függvény már eleve adja a körülhatároló dobozokat. Egy kis adapterrel becsomagolhatod az eredményt, hogy utánozza a lent bemutatott `engine.recognize` API-t.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: diagram, amely bemutatja, hogyan kell OCR-t végrehajtani képen, és a körülhatároló doboz koordinátákat megjeleníteni*

## 1. lépés – OCR végrehajtása képen és strukturált régiók lekérése

Az első dolog, hogy az OCR motorát megkérjük, ne csak egyszerű szöveget, hanem egy strukturált szövegrégió-listát adjon vissza. Ez a lista tartalmazza a nyers karakterláncot és a körülötte lévő téglalapot.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Miért fontos ez:**  
Ha csak egyszerű szöveget kérsz, elveszíted a térbeli kontextust. A strukturált adatok lehetővé teszik, hogy később **megjelenítsd a körülhatároló doboz koordinátákat**, szöveget táblázatokhoz igazíts, vagy pontos helyzeteket adj egy downstream modellnek.

## 2. lépés – OCR kimenet tisztítása post‑processzorral

Az OCR motorok jól felismerik a karaktereket, de gyakran hagynak meg felesleges szóközöket, sortörés‑artifaktusokat vagy hibásan felismert szimbólumokat. Egy post‑processzor normalizálja a szöveget, javítja a gyakori OCR hibákat, és levágja a fölösleges whitespace‑t.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Ha saját tisztítót építesz, fontold meg:

- Nem‑ASCII karakterek eltávolítása (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Több szóköz egyetlen szóközzé összevonása
- Egy helyesírás‑ellenőrző, például a `pyspellchecker` használata nyilvánvaló elírások javításához

**Miért érdemes foglalkozni vele:**  
A rendezett karakterlánc sokkal megbízhatóbbá teszi a keresést, indexelést és a downstream NLP folyamatokat. Más szóval, a **hogyan tisztítsuk az OCR-t** gyakran a használható adatállomány és a fejfájás közti különbség.

## 3. lépés – Körülhatároló doboz koordináták megjelenítése minden tisztított régióhoz

Most, hogy a szöveg már tiszta, végigiterálunk minden régión, kiírva a téglalapot és a tisztított karakterláncot. Ez a rész, ahol végre **megjelenítjük a körülhatároló doboz koordinátákat**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Minta kimenet**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Ezeket a koordinátákat most már átadhatod egy rajzoló könyvtárnak (pl. OpenCV), hogy dobozokat helyezz a eredeti képre, vagy adatbázisban tárold későbbi lekérdezésekhez.

## Teljes, futtatható szkript

Az alábbiakban a teljes program látható, amely összekapcsolja a három lépést. Cseréld le a helyőrző `engine` hívásokat a saját OCR SDK-dra.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Hogyan futtassuk

```bash
python perform_ocr.py sample_invoice.jpg
```

A kimenet egy listát fog mutatni a körülhatároló dobozokról, párosítva a tisztított szöveggel, pontosan úgy, mint a fenti minta kimenet.

## Gyakran ismételt kérdések és széljegyek

| Kérdés | Válasz |
|----------|--------|
| **Mi a teendő, ha az OCR motor nem támogatja a `return_structured` opciót?** | Írj egy vékony wrapper‑t, amely a motor nyers kimenetét (általában szavak listája koordinátákkal) átalakítja olyan objektumokká, amelyek `text` és `bounding_box` attribútumokkal rendelkeznek. |
| **Kaphatok megbízhatósági pontszámokat?** | Sok SDK biztosít konfidencia‑metrikát régiónként. Egészítsd a kiírást: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Hogyan kezeljem a forgatott szöveget?** | Előfeldolgozásként használd az OpenCV `cv2.minAreaRect` függvényét a dőlés korrigálásához, mielőtt meghívod a `recognize`‑t. |
| **Mi a teendő, ha JSON‑formátumban szeretném a kimenetet?** | Sorosítsd a `processed_result.regions`‑t a `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` hívással. |
| **Van mód a dobozok vizualizálására?** | Használd az OpenCV‑t: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` a ciklusban, majd `cv2.imwrite("annotated.jpg", img)`. |

## Összegzés

Most már megtanultad, **hogyan kell OCR-t végrehajtani képen**, tisztítani a nyers kimenetet, és **megjeleníteni a körülhatároló doboz koordinátákat** minden régióhoz. A háromlépéses folyamat – felismerés → post‑processzálás → iteráció – egy újrahasználható minta, amelyet bármely Python projektbe beilleszthetsz, amely megbízható szövegkinyerést igényel.

### Mi következik?

- **Fedezz fel különböző OCR háttérmotorokat** (Tesseract, EasyOCR, Google Vision) és hasonlítsd össze a pontosságot.
- **Integráld egy adatbázissal**, hogy a régióadatokat kereshető archívumokban tárold.
- **Adj hozzá nyelvfelismerést**, hogy minden régiót a megfelelő helyesírás‑ellenőrzőn keresztül irányítsd.
- **Helyezz dobozokat az eredeti képre** a vizuális ellenőrzéshez (lásd a fenti OpenCV kódrészletet).

Ha bármilyen furcsasággal találkozol, ne feledd, hogy a legnagyobb előny egy szilárd post‑processzálási lépésből származik; egy tiszta karakterlánc sokkal könnyebben kezelhető, mint egy nyers karakterhalmaz.

Boldog kódolást, és legyenek mindig rendezettek az OCR csővezetékek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}