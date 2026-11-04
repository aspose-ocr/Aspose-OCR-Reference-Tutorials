---
category: general
date: 2026-03-26
description: Hogyan lehet PDF szöveget kinyerni OCR-rel. Tanulja meg, hogyan töltsön
  be PDF-et képként, ismerje fel a PDF szövegét, és egyszerű Python példával nyerje
  ki a szöveget a PDF-ből.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: hu
og_description: Hogyan lehet PDF szöveget kinyerni OCR-rel. Ez az útmutató megmutatja,
  hogyan töltsd be a PDF-et képként, ismerd fel a PDF szövegét, és hogyan nyerd ki
  a szöveget a PDF‑ből Pythonban.
og_title: Hogyan nyerjünk ki PDF‑szöveget OCR‑rel – Teljes útmutató
tags:
- OCR
- Python
- PDF processing
title: Hogyan nyerjünk ki PDF‑szöveget OCR‑rel – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan vonjunk ki PDF szöveget OCR-rel – Teljes lépésről‑lépésre útmutató

Valaha is elgondolkodtál **hogyan vonjunk ki PDF** fájlokból, amelyek valójában csak beolvasott képek? Nem vagy egyedül – sok fejlesztő ütközik ebbe a falba, amikor kereshető tartalomra van szükségük, de csak képes PDF‑ek állnak rendelkezésre. A jó hír? Néhány kódsor és egy megbízható OCR‑könyvtár pillanatok alatt szöveggé alakíthatja ezeket a kép‑PDF‑eket.  

Ebben a tutorialban végigvezetünk téged **hogyan használjuk az OCR‑t** egy PDF betöltéséhez képként, a PDF szöveg felismeréséhez, és végül **szöveg kinyeréséhez PDF** dokumentumokból bármilyen hosszúságban. A végére egy futtatható szkriptet, egyértelmű magyarázatot minden lépéshez, és néhány tippet kapsz a szokásos buktatók elkerüléséhez.

## Amit szükséged lesz

- Python 3.9 vagy újabb (a kód 3.10‑n is működik)  
- Az `ocr` Python csomag (vagy bármely kompatibilis OCR könyvtár, amely elérhetővé teszi az `OcrEngine`, `OcrEngineMode` és `Imaging.Image` osztályokat)  
- Egy többoldalas PDF, amelyet feldolgozni szeretnél (demóként `multi_page.pdf`‑nek hívjuk)  
- Alapvető ismeretek a virtuális környezetekkel (opcionális, de ajánlott)

> **Pro tipp:** Ha Windows-t használsz, érdemes az Anaconda Prompt-ot használni; macOS/Linux esetén egy egyszerű `python -m venv venv && source venv/bin/activate` megoldja a feladatot.

## 1. lépés: Az OCR könyvtár telepítése

Először szerezd be az OCR csomagot a PyPI‑ról. Az alábbi példa egy fiktív `ocr` csomagot használ, amely tükrözi a kódrészletben bemutatott API‑t, de a legtöbb valós könyvtár (például `pytesseract` + `pdf2image`) hasonló mintát követ.

```bash
pip install ocr
```

Ha más motorral dolgozol, cseréld le az `ocr`‑t a megfelelő névre (pl. `pip install pytesseract pdf2image`).

## 2. lépés: Az OCR motor inicializálása

Az motor példányának létrehozása a **hogyan vonjunk ki PDF** szöveg alapja. Tekintsd a motort úgy, mint az agyat, amely értelmezni fogja az egyes PDF‑oldalak pixeleit.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Miért fontos:** A `set_engine_mode` lehetővé teszi a sebesség és a pontosság közti kompromisszumot. A `DEFAULT` egy kiegyensúlyozott választás; ha nagyobb pontosságra van szükséged, válts `HIGH_ACCURACY`‑ra (ha a könyvtár támogatja).

## 3. lépés: A PDF betöltése képként

Az OCR képeken működik, nem PDF konténereken, ezért először a PDF‑et képi reprezentációvá kell konvertálni. Az `Imaging.Image.load` metódus automatikusan kezeli a többoldalas PDF‑eket.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Szélsőséges eset:** Egyes könyvtárak csak egyoldalas képet fogadnak el. Ebben az esetben egy ciklussal kellene végigmenni az oldalakon a `pdf2image.convert_from_path` használatával. A mi `load` hívásunk elrejti ezt, így a **load pdf as image** egyetlen soros megoldás.

## 4. lépés: Szöveg felismerése minden oldalon

Most következik a **recognize PDF text** magja. A motor minden oldalt átvizsgál, és egy listát ad vissza eredményobjektumokból – egyet oldalanként.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Minden `page_result` olyan metódusokat tartalmaz, mint a `get_text()` (egyszerű szöveg) és a `get_confidence()` (opcionális minőségi mutató).  

> **Tipp:** Ha csak az első oldalra van szükséged, hívd a `recognize(pdf_image[0])`‑t a többoldalas segédfüggvény helyett.

## 5. lépés: Az eredmények bejárása és a kinyert szöveg kiírása

Végül végigiterálunk az eredményeken, és kiírjuk minden oldal szövegét. Ez befejezi a **extract text from PDF** munkafolyamatot.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Várt kimenet

Ha a `multi_page.pdf` három oldalon a „Hello”, „World” és „Python” szavakat tartalmazza, a következőt fogod látni:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Ennyi – a PDF most már teljesen kereshető, és a szöveg készen áll a további feldolgozásra (indexelés, érzelemelemzés, bármi).

## 6. lépés: Gyakori buktatók kezelése

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Üres kimenet** | A PDF‑oldalak alacsony DPI‑n vannak beolvasva, így a karakterek nem különböztethetők meg. | Nagyítsd fel a képet OCR előtt: `pdf_image = pdf_image.resize(300)` (300 DPI egy jó kiindulási pont). |
| **Rossz karakterek** | A nem latin ábécék nyelvi csomagokat igényelnek. | Töltsd be a megfelelő nyelvi modellt: `ocr_engine.load_language('spa')` spanyolhoz, stb. |
| **Memória túlcsordulás nagy PDF‑eken** | Az összes oldal egyszerre történő betöltése RAM‑ot fogyaszt. | Oldalak feldolgozása darabokban: `for img in pdf_image.split(batch=10): …` (pszeudokód). |
| **Lassú teljesítmény** | A `DEFAULT` használata egy hatalmas dokumentumon lassú lehet. | Válts `FAST` módra vagy futtasd az OCR‑t párhuzamosan a `concurrent.futures`‑szal. |

## Bónusz: Kinyert szöveg mentése fájlba

A legtöbb valós pipeline-nak szüksége van a szöveg megőrzésére. Íme egy apró segédfüggvény, amely mindent az `output.txt`‑be ír.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Most már betáplálhatod az `output.txt`‑t egy keresőmotorba, adatbázisba vagy bármilyen NLP modellbe.

## Összeállítás – Teljes szkript

Az alábbiakban a teljes, azonnal futtatható program található. Másold be, állítsd be a fájlutakat, és már mehetsz is.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Futtasd:

```bash
python extract_pdf_ocr.py
```

Minden oldal tartalma ki lesz nyomtatva a konzolra, majd egy megerősítés követi, hogy a `extracted_text.txt` fájl létrejött.

## Összegzés

Áttekintettük, **hogyan vonjunk ki PDF** szöveget kép‑csak dokumentumokból OCR‑motor segítségével, a könyvtár telepítésétől a többoldalas eredmények kezeléséig és a kimenet mentéséig. Most már tudod, **hogyan használjuk az OCR‑t**, hogyan **töltsük be a PDF‑et képként**, és hogyan **ismerjük fel a PDF szöveget** megbízhatóan.  

Mi a következő lépés? Próbáld ki a motor alapértelmezett módjának cseréjét egy magas pontosságú beállításra, kísérletezz nyelvi csomagokkal többnyelvű PDF‑ekhez, vagy csatlakoztasd a kinyert szöveget egy teljes szöveges keresőindexhez, például az Elasticsearch‑hez. A lehetőségek határtalanok, ha már elsajátítottad a PDF‑szöveg kinyerésének alapjait.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="how to extract pdf workflow diagram"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}