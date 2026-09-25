---
category: general
date: 2026-01-12
description: Szöveg kinyerése PDF-ből OCR-motorral Pythonban – tanulja meg, hogyan
  olvasson PDF-et OCR-rel, hogyan töltsön be képet OCR-hez, és hogyan kapjon strukturált
  eredményeket.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: hu
og_description: Szöveg kinyerése PDF-ből OCR-motorral Pythonban. Ez az útmutató bemutatja,
  hogyan olvassunk PDF-et OCR-rel, hogyan töltsünk be képet OCR-hez, és hogyan használjuk
  az OCR-motort Pythonban a megbízható eredményekért.
og_title: PDF-ből szöveg kinyerése OCR motorral Pythonban – Teljes útmutató
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Szöveg kinyerése PDF-ből OCR motorral Pythonban – Lépésről lépésre útmutató
url: /hu/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése PDF‑ből OCR motorral Python – Teljes útmutató

Szükséged volt már **szöveg kinyerésére PDF‑ből**, de a fájl csak beolvasott kép? Nem vagy egyedül. Sok valós projektben a kapott PDF nem tartalmaz kiválasztható szöveget, ezért az egyetlen megoldás a **PDF olvasása OCR‑rel**.  

Ebben az útmutatóban egy gyakorlati, vég‑től‑végig megoldást mutatunk be, amely pontosan bemutatja, hogyan **tölts be képet OCR‑hez**, indítsd el az **OCR motor Python**-t, és nyerj ki strukturált szöveget, amelyet továbbadhatsz a downstream csővezetékeknek. Nincs homályos hivatkozás, csak egy teljes, futtatható példa, amelyet ma másolhatsz‑beilleszthetsz.

## Mit tanulhatsz meg

- Hogyan telepítsd és importáld a szükséges Python OCR könyvtárat.  
- A pontos lépések a **kép betöltéséhez OCR‑hez** egy PDF‑fájlból.  
- Hogyan hívd meg a motor `recognize_structured()` metódusát, és iterálj a blokkok, sorok és szavak felett.  
- Tippek alacsony biztonságú eredmények és többoldalas PDF‑ek kezeléséhez.  

A tutorial végére egy olyan szkriptet kapsz, amely megbízhatóan **kivonja a szöveget PDF‑dokumentumokból**, függetlenül attól, hogy egy vagy akár száz oldalas a fájl.

---

![Diagram, amely bemutatja az OCR motor PDF feldolgozását és a strukturált szöveg kimenetét.](images/ocr_flow.png "PDF‑ből szöveg kinyerése diagram")

*Kép alternatív szövege: PDF‑ből szöveg kinyerése diagram, amely az OCR feldolgozási lépéseket ábrázolja.*

## Előfeltételek

- Python 3.9 vagy újabb (a kód f‑stringeket és típusjelöléseket használ).  
- Egy pip‑en keresztül telepíthető OCR csomag, amely egy `OcrEngine` osztályt biztosít (például egy fiktív `pyocr` könyvtár).  
- Egy PDF fájl, amelyet helyben tárolsz (például `form.pdf`).  

Ha hiányzik az OCR könyvtár, telepítsd a következővel:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## 1. lépés: Szöveg kinyerése PDF‑ből – OCR motor beállítása

Mielőtt **PDF‑t olvasnánk OCR‑rel**, szükségünk van egy motor példányra. Gondolj a motorra, mint egy agyra, amely minden pixelt megnéz, és eldönti, milyen karaktert ábrázol.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Miért fontos:** A motor egyszeri inicializálása lehetővé teszi a nyelvi csomagok újra‑használatát több fájl esetén, ezzel időt és memóriát takarítva meg.

---

## 2. lépés: Kép betöltése OCR‑hez – PDF előkészítése

A PDF nem nyers kép, ezért a könyvtár általában egy segédfüggvényt biztosít, amely az első (vagy az összes) oldalt képpé konvertálja, amit az OCR motor értelmezni tud.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tipp:** Ha a PDF több oldalas, sok OCR könyvtár engedélyezi a `page=2` paraméter átadását, vagy a `engine.load_image(pdf_path, page=n)` ciklus használatát. Nagy dokumentumok esetén érdemes az oldalakat kötegekben feldolgozni, hogy elkerüld a memória csúcsokat.

---

## 3. lépés: OCR Engine Python használata – Strukturált szöveg felismerése

Most történik a nehéz munka. A `recognize_structured()` hívás egy blokk → sor → szó hierarchiát ad vissza, minden elemhez nyelv, biztonság és határoló keret tartozik.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Ami visszakapod:**  
> - `structured_result.blocks` – felső szintű tárolók (gyakran bekezdések vagy oszlopok).  
> - Minden blokk tartalmaz `lines`‑t, és minden sor tartalmaz `words`‑t.  
> - A biztonsági pontszámok segítségével kiszűrheted a kétes eredményeket.

---

## 4. lépés: Eredmények iterálása – Blokkok, sorok és szavak elérése

Az alábbi tömör ciklus kiírja a leghasznosabb információkat. Nyugodtan bővítsd JSON, CSV vagy adatbázis írásra.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Várható kimenet

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Miért fogod szeretni:** A hierarchia úgy tükrözi, ahogy az emberek olvasnak egy oldalt, így később könnyen rekonstruálhatók táblázatok vagy oszlopos elrendezések.

---

## 5. lépés: Különleges esetek kezelése – Alacsony biztonságú és többoldalas PDF‑ek

### Alacsony biztonságú szavak

Ha egy szó biztonsága például `0.70` alá esik, érdemes megjelölni manuális felülvizsgálatra:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Összes oldal feldolgozása

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tipp:** Tárold a köztes képeket PNG‑ként, ha az OCR könyvtár minden alkalommal újra rendereli őket – ez jelentős időmegtakarítást eredményez nagy kötegek esetén.

---

## Teljes működő szkript

Mindent egy helyen, egyetlen fájlban, amelyet azonnal futtathatsz:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Mentsd el `extract_pdf_ocr.py` néven, és futtasd:

```bash
python extract_pdf_ocr.py
```

A konzolon blokk‑szintű részleteket kell látnod, valamint az alacsony biztonságú figyelmeztetéseket.

---

## Összegzés

Most már egy komplett, production‑kész módszert ismersz a **szöveg kinyerésére PDF‑ből** egy **OCR motor Python** segítségével. A könyvtár telepítésétől a **kép betöltéséig OCR‑hez**, a **PDF olvasásáig OCR‑rel**, egészen a strukturált kimenet iterálásáig egy újra‑használható szkriptet kaptál, amelyet bármely projekthez adaptálhatsz.

Következő lépések, amelyeket érdemes felfedezni:

- A hierarchia exportálása JSON‑ba downstream NLP csővezetékekhez.  
- Nyelvfelismerés hozzáadása, hogy dinamikusan válts OCR modellek között.  
- `pdf2image` integrálása a komplex elrendezésű PDF‑ek előfeldolgozásához.  

Próbáld ki egy többoldalas számlakötegben, állítsd be a biztonsági küszöböt, és nézd meg, milyen gyorsan alakíthatod a beolvasott PDF‑eket kereshető, szerkeszthető szöveggé. Ha bármilyen problémába ütközöl, írj egy megjegyzést lent – jó OCR‑olást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}