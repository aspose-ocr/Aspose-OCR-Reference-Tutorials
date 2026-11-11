---
category: general
date: 2026-06-19
description: Készíts kereshető PDF-et egy képből Python OCR segítségével. Tanuld meg,
  hogyan konvertálj OCR-t PDF-be, hogyan nyerj ki szöveget a képből, és hogyan végezz
  gyors OCR-t a képen.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: hu
og_description: Készíts kereshető PDF-et egy képből Python OCR-rel. Ez az útmutató
  bemutatja, hogyan konvertáljuk az OCR-t PDF-be, hogyan nyerjünk ki szöveget a képből,
  és hogyan hajtsunk végre OCR-t a képen.
og_title: Kereshető PDF létrehozása Pythonban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Kereshető PDF létrehozása Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Pythonban – Teljes lépés‑ről‑lépésre útmutató

Valaha szükséged volt **kereshető PDF** létrehozására egy beolvasott nyugtából, de nem tudtad, hol kezdj? Nem vagy egyedül – sok fejlesztő ugyanazzal a problémával szembesül, amikor először próbálja a szövegképet kereshető PDF‑vé alakítani.  

Ebben a tutorialban egy gyakorlati megoldáson vezetünk végig, amely lehetővé teszi, hogy **perform OCR on image**, az OCR‑eredményt **searchable PDF**‑vé alakítsd, és akár a nyers szöveget is kinyerd, ha további feldolgozásra van szükséged. Nincs felesleges részlet, csak egy működő példa, amelyet ma be‑másolhatsz a projektedbe.

## What You’ll Learn

- Hogyan állíts be egy könnyűsúlyú OCR‑motort Pythonban  
- A pontos lépések a **convert OCR to PDF** elvégzéséhez és a kereshető dokumentum mentéséhez  
- Módszerek a **extract text from image** végrehajtására downstream elemzéshez  
- Tippek a gyakori buktatók, például a kép orientációja és nagy fájlok kezelése kapcsán  
- Egy teljes, futtatható szkript, amelyet saját felhasználási esetedhez adaptálhatsz

### Prerequisites

- Python 3.8+ telepítve a gépeden  
- Alapvető ismeretek a pip‑ről és a virtuális környezetekről (opcionális, de ajánlott)  
- Egy képfájl (PNG, JPEG, stb.), amely tiszta, gép‑olvasható szöveget tartalmaz  

Ha ezek megvannak, vágjunk bele.

## Step 1: Install the Required Library

A korábban látott kódrészlet egy fiktív `ocr` csomagot használ, de ugyanazok az elvek alkalmazhatók valós könyvtárakra, mint a **EasyOCR**, **pytesseract**, vagy **pdfminer.six**. Ehhez a útmutatóhoz a **EasyOCR**‑t használjuk, mert tisztán Python‑alapú, sok nyelvet támogat, és egy kényelmes PDF‑konverziós metódust biztosít egy segédosztályon keresztül.

```bash
pip install easyocr pillow
```

> **Pro tip:** Telepítsd egy virtuális környezetben (`python -m venv venv && source venv/bin/activate`), hogy a függőségek rendezettek maradjanak.

## Step 2: Initialize the OCR Engine – Perform OCR on Image

Most, hogy a könyvtár készen áll, létrehozzuk az OCR‑motort, és megadjuk, hogy angol szöveggel dolgozzon. Ez az első hely, ahol **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Miért van szükség egy dedikált reader objektumra? Az EasyOCR előre betölti a nyelvi modelleket, így ugyanazt a `reader`‑t több képhez újra‑használni sokkal hatékonyabb, mint minden alkalommal újra inicializálni.

## Step 3: Load the Image – Extract Text from Image

Töltsük be a képet a memóriába. Ebben a lépésben később **extract text from image**‑t végzünk, de először csak betöltjük.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Ha a képed fejjel lefelé vagy ferde, fontold meg a Pillow `rotate` vagy `transpose` metódusainak használatát, mielőtt az OCR‑motorhoz adnád. Egy gyors vizuális ellenőrzés órákat takaríthat meg a hibakeresésben.

## Step 4: Run the OCR Engine and Capture Results

Itt van a folyamat központja – a kép elküldése az OCR‑motorba és a strukturált adatok visszakapása.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

A `detail=1` flag bounding box‑okat ad vissza, amelyekre később szükség lesz a **convert OCR to PDF** során. Ha csak a nyers karakterláncok érdekelnek, állítsd `detail=0`‑ra.

## Step 5: Convert OCR Result to a Searchable PDF – Convert OCR to PDF

Az EasyOCR nem biztosít közvetlen PDF‑író funkciót, de saját magunk összeállíthatjuk a PDF‑et a Pillow és a `reportlab` könyvtár segítségével. A tutorial könnyűsúlyú maradása érdekében a `fpdf2`‑t használjuk, amely lehetővé teszi az eredeti kép beágyazását és láthatatlan szöveg réteg felülírását.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Mi történt? A beolvasott képet látható rétegként helyeztük el, majd a felismert szavakat fehér szöveggel írtuk felül, amely beleolvad a fehér háttérbe. A keresőeszközök továbbra is olvassák a rejtett réteget, így a PDF **searchable** marad anélkül, hogy a vizuális megjelenés megváltozna.

## Step 6: Save the PDF Bytes – Convert Image to PDF

Ha inkább memóriában kezeled a PDF‑et (például API‑n keresztül küldöd), a lemezre írás helyett a bájtokat is elkapod.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Ez a sor bemutatja a klasszikus **convert image to PDF** munkafolyamatot: kiindulsz egy képből, futtatod az OCR‑t, felülírod a szöveget, és végül egy PDF‑streamet adsz ki.

## Step 7: Verify the Result – Quick Checks

A szkript futtatása után nyisd meg a `receipt_searchable.pdf`‑t bármely PDF‑olvasóban, és próbáld ki a keresőmezőt (Ctrl + F). Írj be egy szót, amely biztosan szerepel a nyugtán – ha a megfelelő helyre ugrik, sikeresen **create searchable pdf**‑t hoztál létre!  

Ha a keresés nem működik, ellenőrizd a következőket:

1. Az OCR‑bizalmi pontszámok (`conf` értékek). Alacsony bizalom azt jelentheti, hogy a kép elmosódott.  
2. A bounding box koordináták – néha az EasyOCR más orientációban adja vissza őket.  
3. Hogy a PDF‑olvasó nincs „csak kép” módra állítva (ritka, de előfordul).

## Full Working Script

Mindent összegezve, itt a teljes, azonnal futtatható Python‑fájl:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Mentsd el `searchable_pdf.py`‑ként, cseréld ki a `YOUR_DIRECTORY` helyőrzőket valós útvonalakra, és futtasd:

```bash
python searchable_pdf.py
```

Egy megerősítő üzenetet kell látnod, valamint egy vadonatúj kereshető PDF‑et a mappádban.

## Common Questions & Edge Cases

**Mi van, ha a kép színes?**  
Az EasyOCR mind szürkeárnyalatos, mind színes képekkel működik, de a szürkeárnyalatosra (`pil_image.convert("L")`) konvertálás néha javíthatja a pontosságot zajos beolvasásoknál.

**Kezelhetek többoldalas PDF‑eket?**  
Igen – iterálj minden oldal képe fölött, futtasd le az OCR‑lépéseket, és minden oldalt fűzd hozzá ugyanahhoz az `FPDF` objektumhoz. Ne felejtsd el a kurzort resetelni (`self.add_page()`) minden új kép előtt.

**Létezik mód arra, hogy az eredeti szövegréteget tartsam meg a látható fehér szöveg helyett?**  
Ha valódi „text‑under‑image” PDF‑re van szükséged (pl. akadálymentesség miatt), használj `pdfminer`‑t vagy `pikepdf`‑t, hogy egy rejtett szövegréteget ágyazz be megfelelő PDF‑címkékkel. Ez haladóbb, de az elv ugyanaz: háttérkép + szövegréteg.

**Mi van, ha az OCR‑bizalom alacsony?**  
Kiszűrheted az alacsony bizalmi szavakat:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Wrap‑Up – What We Achieved

Egy egyszerű nyugta‑képpel indultunk, **performed OCR on image**, kinyertük a felismert karakterláncokat, és végül **create searchable pdf**‑t hoztunk létre, amely úgy viselkedik, mint egy professzionálisan beolvasott dokumentum. A folyamat lefedte az összes másodlagos kulcsszót – **convert OCR to PDF**, **extract text from image**, **convert image to PDF**, és **perform OCR on image** – így most már van egy újrahasználható eszköztárad bármilyen hasonló projekthez.

### Next Steps

- Kísérletezz más nyelvekkel az `easyocr.Reader(['en', 'es'])`‑hez ISO kódok megadásával.  
- Cseréld le az EasyOCR‑t Tesseract‑ra, ha teljesen offline megoldásra van szükséged; a pipeline többi része változatlan marad.  
- Adj hozzá OCR‑bizalmi vizualizációt (rajzolj bounding box‑okat a képre) a problémás beolvasások hibakereséséhez.  

Van egy trükk, amit meg szeretnél osztani? Írj kommentet, forkold

## What Should You Learn Next?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépés‑ről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív implementációs megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}