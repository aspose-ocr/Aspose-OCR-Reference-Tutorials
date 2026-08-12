---
category: general
date: 2026-08-12
description: 使用 Python 與 Aspose AI 執行影像 OCR，提取影像文字，並透過拼寫檢查後處理器提升 OCR 準確度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: zh-hant
lastmod: 2026-08-12
og_description: 在 Python 中對圖像執行 OCR，即時提取圖像文字，並透過 Aspose AI 後處理提升 OCR 準確度。
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: 使用 Python 於圖像執行 OCR – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 使用 Python 在圖像上執行 OCR – 步驟指南
url: /zh-hant/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 上執行影像 OCR – 步驟指南

如果你需要在 Python 中 **run OCR on image** 檔案，本指南將帶領你完成整個工作流程。你將學會如何 **extract text from image**、套用 **OCR text correction**，以及僅用幾行程式碼 **improve OCR accuracy**。

處理掃描文件、收據或螢幕截圖時，常會得到雜訊較多的文字。透過加入拼字檢查的後處理程序，你可以將原始 OCR 輸出轉換為乾淨且可搜尋的內容，而不必切換到其他工具。本教學涵蓋所有必要步驟——從載入影像到顯示校正結果。

## 前置條件

* 已安裝 Python 3.9 或更新版本。
* 取得 Aspose.OCR 與 Aspose.AI Python 套件（或其等效的開源封裝）。
* 有一張範例影像（例如 `sample.png`）放在已知目錄中。
* 具備 Python 函式與物件導向程式碼的基本概念。

你可以使用 pip 安裝所需的函式庫：

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** 使用虛擬環境（`python -m venv .venv`）以保持相依套件的獨立性。

## 步驟 1：Run OCR on image – 建立引擎實例

第一步是建立一個 `OcrEngine` 物件。此物件封裝了 OCR 引擎的設定，並提供影像處理與辨識的方法。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

只建立一次引擎並在多張影像間重複使用，可減少啟動開銷，並確保整個工作階段的設定保持一致。

## 步驟 2：Load image for OCR

在進行辨識之前，引擎必須知道要分析哪張圖片。`load_image` 方法接受檔案路徑或二進位串流。

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Why this matters:** 正確載入影像是取得精確 OCR 的基礎。提供高解析度影像（300 dpi 或更高）通常會 **improve OCR accuracy**，因為引擎能更清楚辨識字元。

## 步驟 3：Extract text from image – 執行基本辨識

影像載入後，你可以呼叫 `recognize()` 取得結果物件。結果包含原始文字、信心分數，並可選擇提供每個單字的邊界框。

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

此時你已成功 **run OCR on image** 並擷取到原始字元。然而，文字可能包含拼寫錯誤，尤其是低品質掃描時。

## 步驟 4：OCR text correction – 加入後處理拼字檢查器

Aspose AI 提供彈性的後處理管線。透過插入自訂的拼字檢查器，你可以校正常見的 OCR 錯誤（例如 “l” 與 “1”、 “O” 與 “0”）。

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**How the spell‑checker works:** `MySpellChecker` 應實作 `process(text: str) -> str` 方法。於其中，你可以使用 `pyspellchecker` 或 `symspellpy` 等函式庫，將不太可能的詞序取代為字典驗證過的替代詞。

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## 步驟 5：Display original and corrected OCR text

最後，將原始與校正後的輸出做比較。這可協助你驗證 **OCR text correction** 確實 **improved OCR accuracy**，符合你的使用情境。

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### 預期輸出

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

校正後的行顯示拼字檢查器已取代常見的 OCR 誤辨識（`Th1s` → `This`、`s4mpl3` → `simple`、`rec3pt` → `receipt`、`som3` → `some`、`err0rs` → `errors`）。

## 步驟 6：Improve OCR accuracy – 最佳實踐清單

即使有後處理，你仍可提升 OCR 引擎的基礎品質：

| 檢查項目 | 說明 |
|----------------|--------------|
| **Use high‑resolution images (≥300 dpi)** | 更多像素資料可降低字元模糊度。 |
| **Convert colored images to grayscale** | 移除可能混淆引擎的色度雜訊。 |
| **Apply image deskewing** | 校正傾斜文字，避免換行錯誤。 |
| **Set language/locale explicitly** | 引導辨識器使用正確的字元集。 |
| **Enable language model** (if the library supports it) | 提供情境感知的預測，進一步 **improve OCR accuracy**。 |

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## 完整可執行腳本

將所有步驟整合後，以下腳本可直接複製貼上至名為 `run_ocr.py` 的檔案並執行。

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

執行腳本會印出原始與校正後的文字，證實你已成功 **run OCR on image**、**extract text from image**，以及透過 **OCR text correction** **improve OCR accuracy**。

## 結論

現在你已了解如何在 Python 中 **run OCR on image** 檔案、擷取原始文字，並套用後處理拼字檢查器以取得更乾淨的結果。依循 **improve OCR accuracy** 的清單，你可以將此工作流程套用於收據、發票、身分證或任何掃描文件。

### 接下來？

* 探索多語言 OCR 的 **language‑specific dictionaries**。
* 將管線整合至資料庫或搜尋索引（例如 Elasticsearch），使擷取的文字可被搜尋。
* 以神經語言模型（例如基於 GPT 的校正）取代簡易拼字檢查器，以獲得更高準確度。

歡迎嘗試不同的影像前處理技術、不同的後處理器或替代的 OCR 引擎。核心流程—**run OCR on image → extract text from image → OCR text correction → improve OCR accuracy**—保持不變，為任何文件數位化專案提供堅實的基礎。

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}