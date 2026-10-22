---
category: general
date: 2026-06-19
description: Utwórz przeszukiwalny PDF z obrazu przy użyciu OCR w Pythonie. Dowiedz
  się, jak konwertować OCR na PDF, wyodrębniać tekst z obrazu i szybko przeprowadzać
  OCR na obrazie.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: pl
og_description: Utwórz przeszukiwalny PDF z obrazu przy użyciu OCR w Pythonie. Ten
  przewodnik pokazuje, jak przekonwertować OCR na PDF, wyodrębnić tekst z obrazu i
  wykonać OCR na obrazie.
og_title: Utwórz przeszukiwalny PDF w Pythonie – Pełny przewodnik programistyczny
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
title: Tworzenie przeszukiwalnego PDF w Pythonie – Kompletny przewodnik krok po kroku
url: /pl/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF w Pythonie – Kompletny przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **utworzyć przeszukiwalny PDF** ze zeskanowanego paragonu, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — wielu programistów napotyka tę samą przeszkodę, gdy po raz pierwszy próbują zamienić zdjęcie tekstu w PDF, który naprawdę można przeszukiwać.  

W tym samouczku przeprowadzimy Cię przez praktyczne rozwiązanie, które pozwala **wykonać OCR na obrazie**, przekształcić wynik OCR w **przeszukiwalny PDF**, a nawet wyciągnąć surowy tekst, jeśli potrzebujesz go do dalszego przetwarzania. Bez zbędnych ozdobników, tylko działający przykład, który możesz skopiować i wkleić do swojego projektu już dziś.

## Co się nauczysz

- Jak skonfigurować lekki silnik OCR w Pythonie  
- Dokładne kroki, aby **przekształcić OCR do PDF** i zapisać go jako przeszukiwalny dokument  
- Sposoby na **wyodrębnienie tekstu z obrazu** do dalszej analizy  
- Wskazówki dotyczące radzenia sobie z typowymi problemami, takimi jak orientacja obrazu i duże pliki  
- Kompletny, gotowy do uruchomienia skrypt, który możesz dostosować do własnego przypadku użycia

### Wymagania wstępne

- Python 3.8+ zainstalowany na Twoim komputerze  
- Podstawowa znajomość pip i środowisk wirtualnych (opcjonalnie, ale zalecane)  
- Plik obrazu (PNG, JPEG itp.) zawierający wyraźny, maszynowo‑czytelny tekst  

Jeśli masz to wszystko, zanurzmy się.

## Krok 1: Zainstaluj wymaganą bibliotekę

The code snippet you saw earlier uses a fictional `ocr` package, but the same ideas apply to real‑world libraries such as **EasyOCR**, **pytesseract**, or **pdfminer.six**. For this guide we’ll use **EasyOCR** because it’s pure Python, supports many languages, and returns a handy PDF conversion method via an auxiliary helper.

```bash
pip install easyocr pillow
```

> **Pro tip:** Zainstaluj w środowisku wirtualnym (`python -m venv venv && source venv/bin/activate`), aby utrzymać porządek w zależnościach.

## Krok 2: Zainicjalizuj silnik OCR – Wykonaj OCR na obrazie

Now that the library is ready, we create an OCR engine and tell it to work with English text. This is the first place where we **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Why do we need a dedicated reader object? EasyOCR pre‑loads language models, so re‑using the same `reader` for multiple images is far more efficient than re‑initializing it each time.

## Krok 3: Załaduj obraz – Wyodrębnij tekst z obrazu

Let’s bring the picture into memory. This step is where we **extract text from image** later, but first we just load it.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

If your image is upside‑down or skewed, consider using Pillow’s `rotate` or `transpose` methods before feeding it to the OCR engine. A quick visual check can save you hours of debugging later.

## Krok 4: Uruchom silnik OCR i przechwyć wyniki

Here’s the core of the process—sending the image to the OCR engine and getting back structured data.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

The `detail=1` flag gives us bounding boxes, which we’ll need when we later **convert OCR to PDF**. If you only care about raw strings, set `detail=0`.

## Krok 5: Przekształć wynik OCR w przeszukiwalny PDF – Convert OCR to PDF

EasyOCR doesn’t provide a direct PDF writer, but we can stitch together the PDF ourselves using Pillow and the `reportlab` library. To keep the tutorial lightweight, we’ll use `fpdf2`, which lets us embed the original image and overlay invisible text.

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

What just happened? We placed the scanned image as the visible layer, then wrote the recognized words on top using white text that blends into the white background. Search tools still read the hidden layer, so the PDF becomes **searchable** without altering the visual appearance.

## Krok 6: Zapisz bajty PDF – Convert Image to PDF

If you prefer to handle the PDF in memory (e.g., sending it over an API), you can capture the bytes instead of writing directly to disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

That line demonstrates the classic **convert image to PDF** workflow: you start with an image, run OCR, overlay text, and finally emit a PDF stream.

## Krok 7: Zweryfikuj wynik – Szybkie kontrole

After you run the script, open `receipt_searchable.pdf` in any PDF viewer and try the search box (Ctrl + F). Type a word you know appears in the receipt—if it jumps to the right spot, you’ve successfully **create searchable pdf**!  

If the search fails, double‑check:

1. Wyniki pewności OCR (`conf`). Niska pewność może oznaczać, że obraz jest rozmazany.  
2. Współrzędne ramki ograniczającej — czasami EasyOCR podaje je w innej orientacji.  
3. Czy przeglądarka PDF nie jest ustawiona w tryb „tylko obraz” (rzadko, ale niektóre przeglądarki mają taką opcję).

## Pełny działający skrypt

Putting everything together, here’s the complete, ready‑to‑run Python file:

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

Save this as `searchable_pdf.py`, replace the `YOUR_DIRECTORY` placeholders with real paths, and run:

```bash
python searchable_pdf.py
```

You should see a confirmation message and a brand‑new searchable PDF sitting in your folder.

## Często zadawane pytania i przypadki brzegowe

**Co zrobić, jeśli obraz jest kolorowy?**  
EasyOCR works with both grayscale and color images, but converting to grayscale (`pil_image.convert("L")`) can sometimes improve accuracy on noisy scans.

**Czy mogę obsługiwać wielostronicowe PDFy?**  
Yes—loop over each page image, run the OCR steps, and append each page to the same `FPDF` object. Just remember to reset the cursor (`self.add_page()`) for each new image.

**Czy istnieje sposób, aby zachować oryginalną warstwę tekstową zamiast niewidocznego białego tekstu?**  
If you need a true “text‑under‑image” PDF (e.g., for accessibility), consider using `pdfminer` or `pikepdf` to embed a hidden text layer with proper PDF tags. That’s more advanced, but the principle remains the same: background image + overlay text.

**Co zrobić, gdy pewność OCR jest niska?**  
You can filter out low‑confidence words:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Podsumowanie – Co osiągnęliśmy

We started with a simple image of a receipt, **performed OCR on image**, extracted the recognized strings, and finally **create searchable pdf** that behaves like any professionally scanned document. The process covered every secondary keyword—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, and **perform OCR on image**—so you now have a reusable toolbox for any similar project.

### Kolejne kroki

- Eksperymentuj z innymi językami, przekazując ich kody ISO do `easyocr.Reader(['en', 'es'])`.  
- Zamień EasyOCR na Tesseract, jeśli potrzebujesz w pełni offline'owego rozwiązania; reszta pipeline pozostaje taka sama.  
- Dodaj wizualizację pewności OCR (rysowanie ramek na obrazie), aby debugować problematyczne skany.  

Masz własny pomysł, którym chciałbyś się podzielić? Dodaj komentarz, fork

## Co powinieneś nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}