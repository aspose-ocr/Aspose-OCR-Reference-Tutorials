---
category: general
date: 2026-06-28
description: Hogyan végezzünk kötegelt OCR-t Pythonban – szöveg kinyerése képekből
  és beolvasott oldalak szöveggé alakítása kötegelt OCR feldolgozással.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: hu
og_description: Tanulja meg, hogyan végezhet kötegelt OCR-t Pythonban, szöveget nyerhet
  ki képekből, és hatékony kötegelt OCR feldolgozással alakíthatja át a beolvasott
  oldalakat szöveggé.
og_title: Hogyan végezzünk kötegelt OCR-t Pythonban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk kötegelt OCR-t Pythonban – Teljes útmutató a képek szövegének
  kinyeréséhez
url: /hu/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t Pythonban – Teljes útmutató a képekből történő szövegkivonáshoz

Ha kíváncsi vagy **hogyan végezzünk kötegelt OCR-t Pythonban**, jó helyen vagy. Ez az útmutató gyors módot mutat be a **képekből történő szövegkivonásra** és a **beolvasott oldalak szöveggé alakítására** egyetlen OCR motor példány használatával. Nincs több másolás‑beillesztés egyes fájlok között – hagyd, hogy a kód végezze a nehéz munkát.

Végigvezetünk minden szükséges lépésen: a könyvtár telepítésén, a beolvasott fájlok teljes mappájának betöltésén, a kötegelt OCR feldolgozás futtatásán, és az eredmények elegáns kezelésén. A végére egy újrahasználható szkriptet kapsz, amely néhány másodperc alatt egy PNG‑ vagy JPEG‑készletet kereshető szövegfájlokká alakít.

## Amire szükséged lesz

* Python 3.9+ telepítve (a kód 3.8‑on is működik, de a 3.9+ a legújabb típusdefiníciós funkciókat biztosítja).
* Egy modern OCR könyvtár – itt a **Aspose.OCR for Python via .NET**‑t használjuk, amely a `OcrEngine` osztályt teszi elérhetővé, ahogy az eredeti kódrészletben látható.  
  ```bash
  pip install aspose-ocr
  ```
* Egy mappa beolvasott oldalakkal (`page1.png`, `page2.png`, …). Bármilyen formátum, amit a Pillow megnyithat, működik, így a PDF‑ek, TIFF‑ek vagy BMP‑k is rendben vannak.
* Egy kis kíváncsiság – ha még sosem automatizáltad a kép‑szöveg átalakítást, most meglátod, miért forradalmi a kötegelt OCR.

> **Pro tipp:** Ha inkább egy tisztán Pythonos könyvtárat szeretnél, cseréld le az `OcrEngine`‑t a `pytesseract.image_to_string`‑re. A környező logika változatlan marad.

## Hogyan végezzünk kötegelt OCR-t Pythonban – Lépésről‑lépésre útmutató

Az alábbiakban a teljes, futtatható szkript található. Minden sor meg van kommentálva, így láthatod, *miért* fontos az egyes részek, nem csak *mit* csinálnak.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Várható kimenet

A szkript futtatása egy három PNG‑es beolvasott fájlt tartalmazó mappán valami ilyesmit eredményez:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Az előnézet minden oldal első 200 karakterét mutatja, a teljes szöveg pedig az `ocr_output` könyvtárban található.

## Szöveg kinyerése képekből egyetlen motor használatával

Miért hozunk létre **egy** `OcrEngine`‑t és használjuk újra? A motor példányosítása költséges lehet, mivel nyelvi csomagokat és natív DLL‑eket tölt be. Ha ugyanazt az példányt osztod meg a kötegben, a következő előnyöket kapod:

* **Memória megtakarítás** – csak egy erőforráskészlet él a RAM‑ban.
* **Sebesség növelés** – a motor melegen marad, elkerülve az ismételt inicializálást.
* **Következetesség fenntartása** – ugyanazok a felismerési beállítások minden oldalra vonatkoznak, ami elengedhetetlen, ha **képekből szeretnél szöveget kinyerni**, amelyek ugyanazzal a elrendezéssel rendelkeznek.

Ha módosítanod kell a felismerést (például engedélyezni a helyesírás-ellenőrzést vagy megváltoztatni a nyelvet), tedd ezt *a* `recognize_batch` *hívása előtt*. Az összes későbbi oldal automatikusan örökli ezeket a beállításokat.

## Beolvasott oldalak hatékony szöveggé alakítása

A probléma középpontja – **beolvasott oldalak szöveggé alakítása** – a `engine.recognize_batch(images)` megoldja. A könyvtár a háttérben egy szálkészlettel dolgozza fel a képeket, így többmagos gépeken közel lineáris skálázást érhetsz el. Néhány dolog, amit szem előtt kell tartani:

* **A képminőség számít** – 300 dpi vagy annál nagyobb a legjobb eredményt adja. Ha a beolvasott képek alacsony felbontásúak, fontold meg a Pillow‑al való felméretezést, mielőtt a motorba adod őket.
* **Szín vs. szürkeárnyalat** – az OCR motorok általában gyorsabban működnek 8‑bit szürkeárnyalaton. Hozzáadhatsz egy előfeldolgozó lépést:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Nyelvi támogatás** – az Aspose.OCR több mint 40 nyelvet támogat. Állítsd be a `engine.language = "eng"` vagy `"fra"` értéket a köteg hívása előtt, ha nem angol nyelven dolgozol.

## Kötegelt OCR feldolgozás legjobb gyakorlatai

Bár a fenti kód már tömör, a termelési szintű kötegelt OCR gyakran igényel néhány további óvintézkedést:

| Concern | Recommended Approach |
|---------|----------------------|
| **Nagy kötegek ( > 500 fájl )** | Oszd fel 100–200 képes darabokra, hogy a memóriahasználat mérsékelt maradjon. |
| **Sérült vagy nem támogatott fájlok** | A `load_images` segédfüggvény már elkapja a kivételeket és figyelmeztetést naplóz; írhatsz egy tartalék megoldást is, amely kihagyja vagy áthelyezi a hibás fájlokat. |
| **Folyamatkövetés** | A `recognize_batch`-et egy ciklusba ágyazva, amely minden kép után visszaad, ha a könyvtár per‑image visszahívásokat biztosít. |
| **Utófeldolgozás** | Futtass helyesírás-ellenőrzést vagy regex‑tisztítást a kapott karakterláncokon a későbbi kereshetőség javítása érdekében. |
| **Párhuzamosság** | Ha többcsomópontos környezeted van, oszd szét a mappákat a munkavégzők között, és a végén egyesítsd a `.txt` kimeneteket. |

Ezek a tippek segítenek a **kötegelt OCR feldolgozás** skálázásában néhány oldalról több ezerre anélkül, hogy a szkript összeomlana.

## Gyakran Ismételt Kérdések

**K: Használhatom ezt közvetlenül PDF‑ekkel?**  
V: Teljesen. Először konvertáld minden PDF‑oldalt képpé (például a `pdf2image` használatával), majd add át a kapott listát a `recognize_batch`‑nek. A pipeline többi része változatlan marad.

## Mit érdemes következőként megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Szöveg kinyerése képekből OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Hogyan nyerjünk ki szöveget ZIP archívumokból Aspose.OCR for .NET használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}