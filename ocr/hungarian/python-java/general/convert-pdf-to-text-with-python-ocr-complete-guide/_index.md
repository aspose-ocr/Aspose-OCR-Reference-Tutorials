---
category: general
date: 2026-07-05
description: PDF konvertálása szöveggé Python OCR segítségével. Tanulja meg, hogyan
  nyerhet ki szöveget PDF-ből, hajthat végre kötegelt OCR-feldolgozást, és tölthet
  be PDF-et OCR-hez néhány egyszerű lépésben.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: hu
og_description: Konvertálja a PDF-et gyorsan szöveggé. Ez az útmutató bemutatja, hogyan
  lehet szöveget kinyerni a PDF-ből, kötegelt OCR-feldolgozást futtatni, és a beolvasott
  PDF-fájlokat Python segítségével felismerni.
og_title: PDF konvertálása szöveggé Python OCR-rel – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: PDF átalakítása szöveggé Python OCR-rel – Teljes útmutató
url: /hu/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF konvertálása szöveggé Python OCR‑rel – Teljes útmutató

Gondoltad már, hogyan **konvertálj PDF‑et szöveggé** anélkül, hogy izzadnál? Lehet, hogy egy csomó beolvasott szerződés, számla vagy kutatási anyag áll előtted, és a tiszta szövegre van szükséged indexeléshez vagy elemzéshez. A jó hír, hogy néhány Python sor elvégzi a nehéz munkát helyetted.

Ebben a bemutatóban egy gyakorlati megoldáson keresztül mutatjuk be, amely nem csak **convert pdf to text**, hanem azt is, hogyan **extract text from pdf**, hogyan állíts be **batch OCR processing**‑t, és hogyan **load pdf for OCR** helyesen. A végére egy futtatható szkriptet kapsz, amely **recognize scanned pdf** oldalakat egy lépésben tud feldolgozni.

## Amit megtanulsz

- Python OCR könyvtár telepítése és konfigurálása (az illusztrációhoz egy általános `ocr` csomagot használunk).  
- Többoldalas PDF betöltése és átadása az OCR motornak.  
- Az eredmények iterálása a kinyert szöveg kiírásához vagy mentéséhez.  
- Gyakori edge case‑ek kezelése, mint nagy fájlok, titkosított PDF‑ek és vegyes nyelvű dokumentumok.  

Nincs nehéz GUI eszköz, nincs kézi másolás – csak tiszta kód, amelyet beilleszthetsz egy CI pipeline‑ba vagy asztali segédprogramba.

![PDF konvertálása szöveggé Python OCR‑rel](https://example.com/images/convert-pdf-to-text.png "PDF konvertálása szöveggé Python OCR‑rel")

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel a következőkkel:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.9+ | Modern szintaxis, típusjelölések és jobb teljesítmény. |
| `ocr` library (or a wrapper around Tesseract) | Biztosítja a példában használt `OcrEngine`, `Language` és `Image` osztályokat. |
| Többoldalas beolvasott PDF (pl. `contract.pdf`) | Ez a forrás, amelyet **load pdf for OCR**‑ra fogsz használni. |
| Alapvető parancssori ismeretek | Csomagok telepítése és a szkript futtatása. |

Ha a Tesseract‑ot használod a háttérben, telepítsd a rendszered csomagkezelőjével (`apt-get install tesseract-ocr` Linuxon, `brew install tesseract` macOS‑on). Ezután add hozzá a Python wrapper‑t:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## 1. lépés: OCR motor létrehozása és a felismerési nyelv beállítása

Először egy OCR motor példányra van szükség. Az angol nyelv beállítása gyakori alapértelmezés, de később átállhatsz más támogatott nyelvekre.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Miért fontos:** A motor az az agy, amely a pixel adatokat értelmezi. Az `engine.language` explicit megadásával elkerülöd a nyelvfelismerés többletterhelését minden egyes oldalon, ami jelentősen felgyorsítja a **batch OCR processing**‑t.

## 2. lépés: PDF dokumentum betöltése OCR‑hoz

Most betöltjük a PDF‑et a memóriába. Az `ocr.Image.load` metódus elfogad egy fájlútvonalat, és olyan objektumot ad vissza, amelyet a motor értelmez.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**Pro tipp:** Ha a PDF jelszóval védett, a legtöbb könyvtár engedélyezi a `password` argumentum átadását. Ennek korai kezelése megakadályozza a későbbi „cannot open file” hibát.

## 3. lépés: OCR futtatása minden oldalon – **recognize scanned pdf** egy hívásban

Az OCR oldalankénti futtatása lassú lehet, különösen nagy dokumentumoknál. A `recognize_multi_page` metódus belsőleg **batch OCR processing**‑t végez, több szál használatával, ha lehetséges.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Mi történik a háttérben?** A motor minden oldalt streameli az alaprendszer OCR motorjához (például Tesseract), összegyűjti a szöveget, és egy `OcrResult` objektumba csomagolja. Ez a megközelítés csökkenti az I/O terhelést, és tiszta módot ad a **extract text from pdf** későbbi végrehajtásához.

## 4. lépés: Eredmények iterálása és a felismert szöveg kiírása

Végül végigjárjuk az egyes `OcrResult` objektumokat, és kiírjuk a szöveget. Írhatsz minden oldalt külön `.txt` fájlba, vagy összefűzheted őket egyetlen dokumentummá.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Miért használjunk enumerate‑t?** Az `enumerate(..., start=1)` emberi olvasásra alkalmas oldalszámot ad, ami hasznos, ha később egy adott szakaszra kell hivatkozni az eredeti PDF‑ben.

### Várt kimenet

A szkript futtatása egy 3‑oldalas szerződésen például a következőt eredményezheti:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Ha egy oldal nem tartalmaz felismerhető szöveget, a hozzá tartozó `result.text` egy üres karakterlánc lesz – tökéletes a üres vagy csak kép‑oldalak felismeréséhez.

## Nagy PDF‑ek és memória korlátok kezelése

Egy 500‑oldalas PDF feldolgozása RAM‑ot tud kimeríteni, ha egyszerre mindent betöltesz. Itt két stratégia:

1. **Chunked Loading** – Néhány könyvtár lehetővé teszi egy oldaltartomány betöltését:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming to Disk** – Írd az egyes oldalak szövegét közvetlenül fájlba, ahelyett, hogy a teljes listát a memóriában tartanád.

Mindkét technika skálázhatóvá teszi a **convert pdf to text** munkafolyamatot.

## Hibák és edge case‑ek kezelése

- **Encrypted PDFs** – Add át a jelszót az `Image.load`‑nak:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Mixed Languages** – Válts nyelvet oldalanként, ha másik írásrendszert észlelsz:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Low‑Resolution Scans** – Előfeldolgozhatod a képeket egy `Pillow`‑alapú könyvtárral, hogy növeld a kontrasztot OCR előtt. Ez drámaian javíthatja a **recognize scanned pdf** lépés minőségét.

## Teljes szkript: PDF konvertálása szöveggé egy futtatásban

Az alábbiakban megtalálod a komplett, azonnal futtatható szkriptet, amely mindent összevon. Mentsd `pdf_to_text.py` néven, majd futtasd `python pdf_to_text.py` paranccsal.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**A szkript futtatása** létrehoz egy `output` mappát, amely `page_1.txt`, `page_2.txt` stb. fájlokat tartalmaz, hatékonyan **extract text from pdf** struktúrált módon.

## A megoldás tesztelése

1. **Sanity Check** – Nyiss meg egy generált `.txt` fájlt, és ellenőrizd, hogy az első néhány sor megegyezik az eredeti dokumentum fejlécével.  
2. **Performance Test** – Időzd a szkriptet egy 100‑oldalas PDF‑en a `time` paranccsal. Ha hosszabb ideig tart, mint várnád, fontold meg a könyvtár több szálas flag‑jének (gyakran `engine.set_threads(4)`) bekapcsolását.  
3. **Quality Assurance** – Hasonlítsd össze az OCR kimenetet egy manuálisan begépelt részlettel diff‑eszközzel. Cél a >95 % karakter pontosság a tiszta beolvasásoknál.

## Következő lépések és kapcsolódó témák

- **Pontosság növelése**: Kísérletezz az `engine.dpi = 300` beállítással vagy alkalmazz képelőfeldolgozást (deskew, denoise) OCR előtt.  
- **Kereshető PDF‑ek**: Használj PDF könyvtárat (például `PyPDF2` vagy `pdfplumber`) a kinyert szöveg visszaágyazásához az eredeti PDF‑be, így kereshetővé téve azt.  
- **Természetes nyelvfeldolgozás**: Tedd a kinyert szöveget spaCy‑val vagy NLTK‑val entitás‑kivonásra, érzelemelemzésre vagy kulcsszó‑címkézésre.  
- **Automatizációs pipeline‑ok**: Kombináld ezt a szkriptet a `watchdog`‑dal, hogy egy mappát figyelj, és automatikusan **convert pdf to text** minden új fájl esetén.

Ezeknek a mintáknak a elsajátításával képes leszel


## Mit tanulj meg legközelebb?


Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}