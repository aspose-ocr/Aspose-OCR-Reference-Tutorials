---
category: general
date: 2026-06-19
description: 使用 Python 的 OCR 函式庫對圖像執行文字辨識。學習如何從圖像中偵測文字、從 JPEG 辨識文字，以及高效地從掃描圖像中提取文字。
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: zh-hant
og_description: 使用 Python 對圖像執行 OCR，並從掃描檔案中提取文字。本指南將一步步帶領您載入圖像、校正傾斜，並辨識文字。
og_title: 在 Python 中對圖像執行 OCR – 完整文字擷取指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 在 Python 中對圖像執行 OCR – 完整文字提取指南
url: /zh-hant/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中對圖像執行 OCR – 完整文字提取指南

是否曾經需要 **對圖像執行 OCR**，卻因為程式碼看起來晦澀而卡住？你並非唯一遇到這種情況的人。無論是將一堆掃描收據轉成可搜尋的 PDF，或是從 JPEG 中擷取說明文字用於資料科學專案，能夠辨識 JPEG 及其他格式的文字是當今開發者必備的技能。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **從圖像偵測文字**、**從掃描圖像中提取文字**，甚至 **載入圖像以進行 OCR**，只需幾行程式碼。完成後，你將擁有一段穩定、可直接投入生產環境的程式碼片段，無需額外匯入，也不會出現「請參考文件」的模糊說明。

## 您將構建的內容

- 一個小型的 Python 腳本，建立 OCR 引擎、啟用自動去斜、載入 JPEG（或任何支援的格式），並印出辨識出的文字。
- 說明 **為何** 每個設定重要，而不只是 **如何** 輸入。
- 處理多頁 PDF、非英語語系，以及模糊掃描等常見問題的技巧。

### 前置條件

- 已安裝 Python 3.8+（範例使用可透過 `pip install ocr-lib` 安裝的 `ocr` 套件——請依實際使用的函式庫名稱替換）。
- 具備基本的 Python 函式與虛擬環境概念。
- 一張想要處理的圖像檔（JPEG、PNG、TIFF），此處以 `skewed_page.jpg` 作為範例檔名。

> **專業小技巧：** 若你使用 Windows，安裝 OCR 函式庫時請以系統管理員身分執行終端機，以免遭遇權限問題。

---

## Perform OCR on Image – Setup and Configuration

首先，你需要一個乾淨的 OCR 引擎實例。它就像是整個流程的「大腦」；若未正確設定，即使是最清晰的圖像也會產生亂碼。

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**為何這很重要：**  
設定 `engine.language` 可縮小 OCR 引擎預期的字符集，顯著提升辨識準確度。若省略此步驟，引擎會自行猜測，常會誤讀簡單的單詞。

---

## Enable Automatic Deskew – Fix Tilted Scans

掃描的頁面很少能完美平整。輕微的傾斜會影響字符分割，導致「Hello」變成「H3llo」。`auto_deskew` 旗標會自動為你完成這項工作。

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**邊緣情況：** 若你確定圖像已經是直的，關閉去斜功能可節省數毫秒的處理時間——在大量批次作業時特別有用。

---

## Load Image for OCR – Supporting JPEG, PNG, TIFF

現在我們實際 **載入圖像以進行 OCR**。`ocr.Image.load` 方法相當彈性，接受任意支援的點陣圖檔案路徑。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **為何此步驟關鍵：** 函式庫會將檔案讀入內部位圖，並在必要時執行色彩空間轉換。若跳過此步驟直接傳入原始位元串，會拋出 `FileNotFoundError`，甚至在不發出錯誤的情況下產生空結果。

如果你特別想 **從 JPEG 檔案辨識文字**，只要確保檔案副檔名為 `.jpeg` 或 `.jpg`。相同的呼叫方式同樣適用於 PNG（`.png`）或 TIFF（`.tif`），不需額外修改。

---

## Perform OCR on Image – Running the Engine

引擎已就緒且圖像已載入記憶體，接下來就可以 **對圖像執行 OCR**。以下單行程式碼即完成前處理、分割、分類與文字組合等全部工作。

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**底層發生了什麼？**  
- 若已啟用去斜，會先套用去斜變換。  
- 透過神經網路或 Tesseract 後端辨識字符。  
- 最後將字符拼接成單詞與行，回傳一個豐富的 `result` 物件。

---

## Extract Text from Scanned Image – Output the Results

最後一步是 **從掃描圖像中提取文字** 並顯示。`result.text` 屬性即為純文字內容。

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

典型的輸出範例如下：

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

若 OCR 引擎找不到任何字符，`result.text` 會是空字串。此時請檢查圖像品質，或考慮調整 `engine.confidence_threshold`（若你的函式庫支援此屬性）。

---

## Handling Common Variations

### Recognize Text from JPEG vs PNG

兩種格式皆受支援，但 JPEG 壓縮可能產生干擾，引擎容易誤判。若發現誤辨率頻繁，可先將 JPEG 轉為 PNG 再處理：

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Detect Text from Image with Multiple Languages

若文件同時包含英文與西班牙文，請啟用多語言模式：

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

引擎將同時考慮兩種字母表進行辨識。

### Extract Text from Scanned PDFs

對於 PDF，需要先將每頁光柵化為圖像。`pdf2image` 等函式庫可輕鬆完成此步驟：

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Full Working Example

以下是完整腳本，可直接複製貼上至 `ocr_demo.py` 檔案。內含錯誤處理與簡易計時輔助函式。

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**預期輸出**（以清晰掃描為例）：

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Frequently Asked Questions

**Q: 可以在無頭（headless）伺服器上執行嗎？**  
A: 完全可以。此函式庫不依賴 GUI，只要確保伺服器上已安裝必要的原生二進位檔（例如 Tesseract），即可正常運作。

**Q: 若圖像模糊該怎麼辦？**  
A: 考慮在 `engine.recognize` 前加入銳化濾鏡。許多 OCR 函式庫提供 `image_preprocessing.sharpen = True`，或可使用 OpenCV 的 `cv2.GaussianBlur` 反向操作。

**Q: 這個腳本支援批次處理嗎？**  
A: 支援。只要將 `perform_ocr` 包在遍歷檔案路徑清單的迴圈中即可，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}