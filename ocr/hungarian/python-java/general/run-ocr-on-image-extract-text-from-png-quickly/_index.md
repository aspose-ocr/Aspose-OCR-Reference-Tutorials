---
category: general
date: 2026-03-18
description: Futtass OCR-t a képen, hogy szöveget nyerj ki a PNG-ből, és kereshető
  PDF-et készíts. Tanuld meg, hogyan ismerj fel szöveges képet, és konvertáld a PNG-t
  PDF-be percek alatt.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: hu
og_description: Futtass OCR-t a képen, hogy szöveget nyerj ki a PNG‑ből, felismerd
  a szöveges képet, és kereshető PDF-et készíts. Kövesd ezt a lépésről‑lépésre útmutatót.
og_title: Futtass OCR-t a képen – Szöveg gyors kinyerése PNG-ből
tags:
- OCR
- Python
- Image Processing
title: Futtass OCR-t a képen – Szöveg gyors kinyerése PNG-ből
url: /hu/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen – Szöveg kinyerése PNG‑ből gyorsan

Valaha is szükséged volt **OCR futtatására képfájlokon**, de nem tudtad, hol kezdjed? Lehet, hogy van egy beolvasott cikked `article.png` néven, és csak a sima szöveget szeretnéd, vagy kereshető PDF‑re van szükséged archiváláshoz. Bármelyik is legyen, jó helyen vagy. Ebben az útmutatóban végigvezetünk a PNG‑ből történő szövegkinyerésen, a szövegfelismerésen, és még a PNG‑t kereshető PDF‑vé is átalakítjuk – mindezt néhány sor kóddal.

> **Mit kapsz:** egy teljes, futtatható szkriptet, amely betölti a PNG‑t, futtatja az OCR‑t, elmenti a hOCR kimenetet, és opcionálisan létrehoz egy kereshető PDF‑et. Nincs hiányzó import, nincs „lásd a dokumentációt” holtjáték – csak egy önálló megoldás, amelyet még ma beilleszthetsz a projektedbe.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

- **Python 3.8+** (az itt használt szintaxis bármely friss verzión működik)
- A **`ocr_engine`** könyvtárral, amelyet használsz (a példa egy `OcrEngine` osztályt feltételez; cseréld le Tesseract‑ra, EasyOCR‑ra stb., ha szükséges)
- Egy PNG képre, amelyet feldolgozni szeretnél (pl. `article.png` egy olyan mappában, amelyre hivatkozhatsz)
- Írási jogosultsággal az output könyvtárban

Ha a Tesseract‑ot használod a háttérben, telepítsd a következővel:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Ezután telepítsd a Python‑kötést:

```bash
pip install pytesseract Pillow
```

*Pro tip:* tartsd naprakészen az OCR‑könyvtáradat – új nyelvi csomagok és teljesítményjavítások gyakran érkeznek.

## OCR futtatása képen – Lépésről‑lépésre útmutató

Az alábbi **teljes szkript**. Nyugodtan másold be egy `run_ocr.py` nevű fájlba, és futtasd a `python run_ocr.py` paranccsal.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Mit csinál a szkript, egyszerűen elmagyarázva

1. **Példányosítja** az OCR motorját, hogy szabályozhasd a beállításait.
2. **Betölti** a PNG fájlt (`article.png`). A szkript korán leáll, ha a fájl nem létezik – így elkerülheted a rejtélyes `NoneType` hibákat.
3. **Kiválasztja** a `hocr` exportformátumot. Ez a formátum megőrzi az eredeti elrendezést, ami elengedhetetlen a későbbi kereshető PDF‑hez.
4. **Futtatja** a felismerő motort; itt történik a nehéz munka.
5. **Kiírja** a hOCR XML‑t `article.hocr`‑ba. Most már van egy gép‑olvasható reprezentációd a szövegről és koordinátáiról.
6. *(Opcionálisan)* Átvált `"pdf"`‑re, és egy extra lépésben generál egy kereshető PDF‑et.

A **várt kimenet** egy UTF‑8‑kódolt `.hocr` fájl, amely nagyjából így néz ki (rövidítve a tömörség kedvéért):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Ha feloldod a PDF szekciót, akkor egy `article_searchable.pdf` fájlt is kapsz, amelyet bármely PDF‑olvasóval megnyithatsz, és a **Ctrl + F** keresőmezővel azonnal megtalálhatod a szavakat.

![OCR futtatása képen példakimenet](example.png "OCR futtatása képen – hOCR és PDF eredmények")

## Hogyan nyerjünk ki szöveget PNG‑ből az OcrEngine‑nel

Ha csak a nyers szövegre van szükséged (elrendezés vagy PDF nélkül), kihagyhatod a hOCR lépést teljesen:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Miért válaszd a nyers szöveget?* Könnyű, tökéletes indexeléshez, és remekül működik a downstream NLP pipeline‑okkal.

## Szövegfelismerés képen és kereshető PDF generálása

A kereshető PDF generálása két lépésből áll:

1. **Futtasd az OCR‑t** `hocr`‑val (ahogy fent láttuk), hogy megkapd az elrendezési információkat.
2. **Kombináld** az eredeti PNG‑t a hOCR‑ral egy PDF‑be a motor PDF‑exporterével.

A legtöbb modern OCR‑könyvtár (Tesseract, ABBYY, Google Vision) kínál `pdf` exportot, amely pontosan ezt teszi. A *Opcionális* blokkban a fő szkriptben látható kódrészlet ezt a mintát mutatja. Ha a könyvtárad nem rendelkezik beépített PDF‑exporterrel, használhatod a **`pdf2image`** + **`reportlab`** kombinációt a kép és a hOCR összefűzéséhez – csak jelezd, és megosztok egy gyors extra példát.

## PNG konvertálása PDF‑be OCR kimenettel

Néha csak egy **egyszerű PDF**‑re van szükség, amely tartalmazza a képet (kereshető réteg nélkül). Ez még egyszerűbb:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Ezt kombinálhatod az OCR lépéssel, ha kereshető változatra van szükséged, vagy megtarthatod egyszerűen a vizuálisan hű másolatot archiválási célokra.

## Gyakori hibák és tippek

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Elmosódott vagy alacsony felbontású PNG** | Az OCR pontossága drámaian csökken ~300 DPI alatti felbontásnál. | Méretezd fel `Image.resize((width*2, height*2), Image.LANCZOS)`‑szel, mielőtt a motorba adod. |
| **Rossz nyelv** | A motor alapértelmezés szerint angolt használ; a nem‑angol karakterek torzulnak. | Hívd meg `ocr_engine.setLanguage('deu')`‑t (vagy a megfelelő ISO kódot) a `recognize()` előtt. |
| **Hiányzó hOCR kimenet** | Néhány motor alapértelmezés szerint egyszerű szöveget ad, ha a `setExportFormat` nincs meghívva. | Ellenőrizd, hogy a `setExportFormat("hocr")` **a** `recognize()` **előtt** fut. |
| **Fájl jogosultsági hibák** | Írás egy csak‑olvasásra beállított mappába. | Használj egy projekt‑beli útvonalat vagy előbb hívd meg `os.makedirs(..., exist_ok=True)`‑t. |
| **Nagy PDF‑ek memória‑spike‑et okoznak** | A PDF‑exporter az egész képet RAM‑ban tartja. | Oldald fel az oldalak feldolgozását darabokra, vagy használj streaming PDF‑írót. |

*Pro tip:* mindig tesztelj egy kis mintaképen, mielőtt több ezer képre alkalmaznád. Órakkal spórolhatsz a hibakeresésen.

## Összegzés

Most már tudod, **hogyan futtass OCR‑t képfájlokon**, **hogyan nyerj ki szöveget PNG‑ből**, **hogyan ismerd fel a szöveges képet** downstream feladatokhoz, **hogyan generálj kereshető PDF‑et**, és **hogyan konvertáld a PNG‑t PDF‑be**, ha egyszerű archiválásra van szükséged. A mellékelt szkript egy komplett, másold‑be‑és‑futtasd megoldás, amely azonnal működik, az opcionális részek pedig lehetővé teszik, hogy a kimenetet pontosan a saját munkafolyamatodhoz igazítsd.

### Mi a következő lépés?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}