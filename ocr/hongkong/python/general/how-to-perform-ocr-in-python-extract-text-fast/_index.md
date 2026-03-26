---
category: general
date: 2026-03-26
description: 學習如何在 Python 中執行 OCR，並輕鬆從圖像提取文字、讀取掃描檔文字，或使用簡易 OcrEngine 從發票中提取文字。
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: zh-hant
og_description: 如何在 Python 中執行 OCR？本指南將教你如何在數分鐘內從圖片提取文字、從掃描檔讀取文字，以及從發票中提取文字。
og_title: 如何在 Python 中執行 OCR – 快速擷取文字
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中執行 OCR – 快速提取文字
url: /zh-hant/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中執行 OCR – 快速提取文字

有沒有想過 **如何在掃描收據或模糊的 PDF 上執行 OCR**？你並不孤單。在許多專案中，**從圖像提取文字**的需求往往很快就會出現，而傳統的「手動輸入全部」方式根本無法擴展。  

在本教學中，你將看到一個完整、可直接執行的範例，示範 **如何使用 OCR** 從掃描件讀取文字、從發票提取資料，甚至處理自動傾斜校正——只需幾行 Python 程式碼。

## 你將學會什麼

我們會一步步說明你需要知道的一切：

* 所需的精確相依套件與匯入語句。
* 如何建立與設定 `OcrEngine` 實例。
* 使用相同引擎執行 **從圖像提取文字**、**從掃描件讀取文字**、以及 **從發票提取文字** 的方法。
* 常見陷阱（語言設定錯誤、檔案遺失、大圖像）以及避免方式。
* 預期輸出，以便驗證 OCR 是否成功。

不需要外部文件連結——所有內容皆自成一體，你可以直接複製貼上程式碼，即時看到結果。

## 前置條件

在深入之前，請確保你已具備：

* 已安裝 Python 3.8 以上（`ocr` 套件相容於任何近期版本）。
* 已取得 `ocr` 函式庫（`pip install ocr‑engine` – 如有不同請改為實際套件名稱）。
* 一個欲處理的影像檔案——示範中我們使用位於 `YOUR_DIRECTORY` 資料夾下的 `invoice.png`。

就這樣。如果你已具備上述條件，即可開始。

## 第 1 步：安裝與匯入 OCR 模組

First things first: we need the OCR library. If you haven’t installed it yet, run the following command in your terminal:

```bash
pip install ocr-engine
```

Now we import the module in our script.

```python
# Step 1: Import the OCR module
import ocr
```

> **小技巧：** 保持虛擬環境整潔；當你之後加入其他影像處理套件時，可避免版本衝突。

## 第 2 步：建立與設定 OCR 引擎

Creating the engine is as simple as calling its constructor, but the real power lies in configuring it correctly. We’ll set the language to English and turn on automatic skew correction, which is essential when dealing with scanned invoices that aren’t perfectly aligned.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

為什麼要啟用 `auto_skew`？許多掃描器產生的影像會有幾度的傾斜。若未校正，引擎可能遺漏字元，將本來清晰的發票變成亂碼。

## 第 3 步：對目標影像執行 OCR

Now we feed the image file into the engine. The `recognize_image` method returns an object that holds the raw text as well as confidence scores (if the library provides them).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

如果你處理的是 **從掃描件讀取文字** 的情境，只需將路徑換成已轉為 PNG 或 JPEG 的掃描 PDF。相同的呼叫可支援底層函式庫所支援的任何影像格式。

## 第 4 步：檢視與使用擷取的文字

Let’s print the raw OCR output. In a real‑world invoice‑processing pipeline you’d probably parse this string, extract line items, totals, and dates, but for now a quick glance will confirm that the OCR succeeded.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Expected output (truncated for brevity):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

如果輸出看起來是亂碼，請再次確認影像是否清晰，以及 `engine.language` 是否與文件語言相符。

## 第 5 步：處理常見例外情況

### 大圖像

Processing a 5000 × 5000 pixel scan can be memory‑hungry. A quick way to mitigate this is to downscale the image before sending it to the engine:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### 多語言

If you need to **extract text from image** that contains both English and Spanish, you can set a list of languages:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

引擎會嘗試辨識兩種語言的字元。

### 錯誤處理

Never assume the file exists. Wrap the call in a try‑except block to give a friendly message:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## 視覺參考

Below is a screenshot of the sample invoice we used in the demo. Notice the slight tilt—exactly what `auto_skew` fixes.

![how to perform OCR on an invoice](/images/ocr-example.png)

*替代文字：* 如何在發票圖像上執行 OCR，顯示自動傾斜校正。

## 完整、可執行範例

Putting everything together, here’s a single script you can run from the command line. It covers installation, configuration, error handling, and a simple post‑processing step that writes the extracted text to a file called `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

執行 `python full_ocr_demo.py` 會將擷取的文字印在終端機，並儲存至 `output.txt`。之後你可以使用正規表達式、CSV 寫入器，或任何其他邏輯，來實作 **從發票提取文字** 的自動化。

## 結論

現在你已掌握在 Python 中 **如何執行 OCR** 的完整解決方案。透過建立 `OcrEngine`、設定語言與傾斜校正，並處理幾個實務例外情況，你可以可靠地 **從圖像提取文字**、**從掃描件讀取文字**，以及 **從發票提取文字**，無需在零散文件中搜尋。

接下來可以做什麼？試著將一批檔案放入迴圈處理、實驗不同語言，或將輸出接入 PDF 產生函式庫，製作可搜尋的 PDF。沒有極限，而剛才看到的程式碼就是堅實的起跳平台。

對特定檔案格式有疑問，或需要協助微調信心門檻嗎？在下方留言——我們很樂意協助你微調 OCR 流程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}