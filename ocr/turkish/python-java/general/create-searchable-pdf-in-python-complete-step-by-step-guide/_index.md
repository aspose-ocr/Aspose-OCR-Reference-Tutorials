---
category: general
date: 2026-06-19
description: Python OCR kullanarak bir görüntüden aranabilir PDF oluşturun. OCR'yi
  PDF'ye dönüştürmeyi, görüntüden metin çıkarmayı ve görüntü üzerinde hızlıca OCR
  yapmayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: tr
og_description: Python OCR ile bir görüntüden aranabilir PDF oluşturun. Bu kılavuz,
  OCR'yi PDF'ye dönüştürmeyi, görüntüden metin çıkarmayı ve görüntü üzerinde OCR yapmayı
  gösterir.
og_title: Python’da Aranabilir PDF Oluşturma – Tam Programlama Rehberi
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
title: Python'da Aranabilir PDF Oluşturma – Tam Adım Adım Rehber
url: /tr/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Aranabilir PDF Oluşturma – Tam Adım‑Adım Kılavuz

Tarayıcıdan alınan bir makbuzdan **aranabilir PDF** oluşturmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz—birçok geliştirici, metnin bir resmini gerçekten arayabileceğiniz bir PDF'ye dönüştürmeye çalıştıklarında aynı engelle karşılaşıyor.  

Bu öğreticide, **perform OCR on image** yapmanızı, OCR sonucunu **searchable PDF**'ye dönüştürmenizi ve gerektiğinde ham metni dışa aktarmanızı sağlayan pratik bir çözümü adım adım inceleyeceğiz. Süslü şeyler yok, bugün projenize kopyalayıp yapıştırabileceğiniz çalışan bir örnek.

## What You’ll Learn

- Python'da hafif bir OCR motoru nasıl kurulur  
- **convert OCR to PDF** adımları ve bunu aranabilir bir belge olarak kaydetme  
- **extract text from image** için yöntemler ve sonraki analizler için kullanım  
- Görüntü yönlendirme ve büyük dosyalar gibi yaygın tuzaklarla başa çıkma ipuçları  
- Kendi kullanım senaryonuza uyarlayabileceğiniz tam, çalıştırılabilir bir betik

### Prerequisites

- Makinenizde Python 3.8+ yüklü  
- pip ve sanal ortamlar hakkında temel bilgi (isteğe bağlı ama önerilir)  
- Açık, makine‑okunabilir metin içeren bir görüntü dosyası (PNG, JPEG vb.)  

Eğer bunlara sahipseniz, başlayalım.

## Step 1: Install the Required Library

The code snippet you saw earlier uses a fictional `ocr` package, but the same ideas apply to real‑world libraries such as **EasyOCR**, **pytesseract**, or **pdfminer.six**. For this guide we’ll use **EasyOCR** because it’s pure Python, supports many languages, and returns a handy PDF conversion method via an auxiliary helper.

```bash
pip install easyocr pillow
```

> **Pro tip:** Sanal bir ortam içinde kurun (`python -m venv venv && source venv/bin/activate`) böylece bağımlılıklarınız düzenli kalır.

## Step 2: Initialize the OCR Engine – Perform OCR on Image

Now that the library is ready, we create an OCR engine and tell it to work with English text. This is the first place where we **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Why do we need a dedicated reader object? EasyOCR pre‑loads language models, so re‑using the same `reader` for multiple images is far more efficient than re‑initializing it each time.

## Step 3: Load the Image – Extract Text from Image

Let’s bring the picture into memory. This step is where we **extract text from image** later, but first we just load it.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

If your image is upside‑down or skewed, consider using Pillow’s `rotate` or `transpose` methods before feeding it to the OCR engine. A quick visual check can save you hours of debugging later.

## Step 4: Run the OCR Engine and Capture Results

Here’s the core of the process—sending the image to the OCR engine and getting back structured data.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

The `detail=1` flag gives us bounding boxes, which we’ll need when we later **convert OCR to PDF**. If you only care about raw strings, set `detail=0`.

## Step 5: Convert OCR Result to a Searchable PDF – Convert OCR to PDF

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

## Step 6: Save the PDF Bytes – Convert Image to PDF

If you prefer to handle the PDF in memory (e.g., sending it over an API), you can capture the bytes instead of writing directly to disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

That line demonstrates the classic **convert image to PDF** workflow: you start with an image, run OCR, overlay text, and finally emit a PDF stream.

## Step 7: Verify the Result – Quick Checks

After you run the script, open `receipt_searchable.pdf` in any PDF viewer and try the search box (Ctrl + F). Type a word you know appears in the receipt—if it jumps to the right spot, you’ve successfully **create searchable pdf**!  

If the search fails, double‑check:

1. The OCR confidence scores (`conf` values). Low confidence may mean the image is blurry.  
2. Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.  
3. That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers have that option).

## Full Working Script

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

## Common Questions & Edge Cases

**What if the image is in color?**  
EasyOCR works with both grayscale and color images, but converting to grayscale (`pil_image.convert("L")`) can sometimes improve accuracy on noisy scans.

**Can I handle multi‑page PDFs?**  
Yes—loop over each page image, run the OCR steps, and append each page to the same `FPDF` object. Just remember to reset the cursor (`self.add_page()`) for each new image.

**Is there a way to keep the original text layer instead of invisible white text?**  
If you need a true “text‑under‑image” PDF (e.g., for accessibility), consider using `pdfminer` or `pikepdf` to embed a hidden text layer with proper PDF tags. That’s more advanced, but the principle remains the same: background image + overlay text.

**What if OCR confidence is low?**  
You can filter out low‑confidence words:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Wrap‑Up – What We Achieved

We started with a simple image of a receipt, **performed OCR on image**, extracted the recognized strings, and finally **create searchable pdf** that behaves like any professionally scanned document. The process covered every secondary keyword—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, and **perform OCR on image**—so you now have a reusable toolbox for any similar project.

### Next Steps

- Experiment with other languages by passing their ISO codes to `easyocr.Reader(['en', 'es'])`.  
- Swap EasyOCR for Tesseract if you need a fully offline solution; the rest of the pipeline stays the same.  
- Add OCR confidence visualisation (draw bounding boxes on the image) to debug problematic scans.  

Got a twist you’d like to share? Drop a comment, fork


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}