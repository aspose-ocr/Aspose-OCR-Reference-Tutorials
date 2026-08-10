---
category: general
date: 2026-06-19
description: 使用 Python OCR 從影像建立可搜尋的 PDF。學習將 OCR 轉換為 PDF、從影像擷取文字，並快速執行影像 OCR。
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: zh-hant
og_description: 使用 Python OCR 從圖像建立可搜尋的 PDF。本指南說明如何將 OCR 轉換為 PDF、從圖像擷取文字，以及對圖像執行 OCR。
og_title: 在 Python 中建立可搜尋 PDF – 完整程式教學
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
title: 使用 Python 建立可搜尋 PDF – 完整逐步指南
url: /zh-hant/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立可搜尋的 PDF – 完整步驟指南

有沒有曾經需要從掃描的收據**建立可搜尋的 PDF**，卻不知從何開始？你並不孤單——許多開發者在首次嘗試將文字圖片轉換成可搜尋的 PDF 時，都會碰到同樣的障礙。  

在本教學中，我們將逐步說明一個實用解決方案，讓你**對圖像執行 OCR**，將 OCR 結果轉換為**可搜尋的 PDF**，甚至在需要時提取原始文字以供後續處理。內容直截了當，只提供一個可直接複製貼上到專案中的可運作範例。

## 你將學會

- 如何在 Python 中設置輕量級的 OCR 引擎  
- 將 **OCR 轉換為 PDF** 並儲存為可搜尋文件的完整步驟  
- 如何 **從圖像提取文字** 以進行後續分析  
- 處理常見問題（如圖像方向與大型檔案）的技巧  
- 一個完整、可執行的腳本，讓你可依需求自行調整

### 前置條件

- 在機器上已安裝 Python 3.8+  
- 對 pip 與虛擬環境有基本認識（非必須，但建議使用）  
- 一個包含清晰、機器可讀文字的圖像檔案（PNG、JPEG 等）  

如果你已具備以上條件，讓我們開始吧。

## 步驟 1：安裝必要的函式庫

The code snippet you saw earlier uses a fictional `ocr` package, but the same ideas apply to real‑world libraries such as **EasyOCR**, **pytesseract**, or **pdfminer.six**. For this guide we’ll use **EasyOCR** because it’s pure Python, supports many languages, and returns a handy PDF conversion method via an auxiliary helper.

```bash
pip install easyocr pillow
```

> **小技巧：** 在虛擬環境中安裝 (`python -m venv venv && source venv/bin/activate`) 以保持相依套件整潔。

## 步驟 2：初始化 OCR 引擎 – 對圖像執行 OCR

Now that the library is ready, we create an OCR engine and tell it to work with English text. This is the first place where we **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Why do we need a dedicated reader object? EasyOCR pre‑loads language models, so re‑using the same `reader` for multiple images is far more efficient than re‑initializing it each time.

## 步驟 3：載入圖像 – 從圖像提取文字

Let’s bring the picture into memory. This step is where we **extract text from image** later, but first we just load it.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

If your image is upside‑down or skewed, consider using Pillow’s `rotate` or `transpose` methods before feeding it to the OCR engine. A quick visual check can save you hours of debugging later.

## 步驟 4：執行 OCR 引擎並取得結果

Here’s the core of the process—sending the image to the OCR engine and getting back structured data.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

The `detail=1` flag gives us bounding boxes, which we’ll need when we later **convert OCR to PDF**. If you only care about raw strings, set `detail=0`.

## 步驟 5：將 OCR 結果轉換為可搜尋的 PDF – OCR 轉 PDF

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

## 步驟 6：儲存 PDF 位元組 – 圖像轉 PDF

If you prefer to handle the PDF in memory (e.g., sending it over an API), you can capture the bytes instead of writing directly to disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

That line demonstrates the classic **convert image to PDF** workflow: you start with an image, run OCR, overlay text, and finally emit a PDF stream.

## 步驟 7：驗證結果 – 快速檢查

After you run the script, open `receipt_searchable.pdf` in any PDF viewer and try the search box (Ctrl + F). Type a word you know appears in the receipt—if it jumps to the right spot, you’ve successfully **create searchable pdf**!  

If the search fails, double‑check:

1. OCR 信心分數（`conf` 值）。低信心可能表示圖像模糊。  
2. 邊界框座標——有時 EasyOCR 會以不同方向回報。  
3. PDF 檢視器未設定為「僅圖像」模式（雖少見，但部分檢視器有此選項）。

## 完整可執行腳本

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

## 常見問題與邊緣情況

**如果圖像是彩色的呢？**  
EasyOCR 同時支援灰階與彩色圖像，但將圖像轉為灰階（`pil_image.convert("L")`）有時能提升噪點掃描的辨識準確度。

**我可以處理多頁 PDF 嗎？**  
可以——對每一頁圖像迴圈，執行 OCR 步驟，並將每頁加入同一個 `FPDF` 物件。只需記得對每張新圖像呼叫 `self.add_page()` 以重設游標。

**有沒有方法保留原始文字層，而不是使用不可見的白色文字？**  
如果需要真正的「文字在圖像下」PDF（例如為了無障礙需求），可考慮使用 `pdfminer` 或 `pikepdf` 來嵌入帶有正確 PDF 標籤的隱藏文字層。這較為進階，但原理相同：背景圖像 + 覆蓋文字。

**如果 OCR 信心太低怎麼辦？**  
You can filter out low‑confidence words:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## 總結 – 我們完成了什麼

We started with a simple image of a receipt, **performed OCR on image**, extracted the recognized strings, and finally **create searchable pdf** that behaves like any professionally scanned document. The process covered every secondary keyword—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, and **perform OCR on image**—so you now have a reusable toolbox for any similar project.

### 往後的步驟

- 嘗試傳入其他語言的 ISO 代碼至 `easyocr.Reader(['en', 'es'])` 以支援多語言。  
- 若需要完全離線的解決方案，可改用 Tesseract 取代 EasyOCR；其餘流程保持不變。  
- 加入 OCR 信心可視化（在圖像上繪製邊界框）以除錯有問題的掃描。  

Got a twist you’d like to share? Drop a comment, fork

## 接下來該學什麼？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [將圖像轉為 PDF（C#） – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [如何 OCR 圖像 – 在 OCR 圖像辨識中執行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}