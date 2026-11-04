---
category: general
date: 2026-08-12
description: 如何在 Python 中使用 OCR 從圖像識別文字、提取文字、將圖像轉換為文字，並透過 AI 後處理清理 OCR 文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: zh-hant
lastmod: 2026-08-12
og_description: 如何在 Python 中使用 OCR 將圖片轉換為可編輯文字。學習從圖像辨識文字、提取文字、將圖像轉為文字，並使用 AI 清理 OCR
  文字。
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: 在 Python 中使用 OCR 的完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: 如何在 Python 中使用 OCR – 步驟指南
url: /zh-hant/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 步驟指南

如果你需要 **how to use OCR** 來將掃描文件或螢幕截圖轉換為可編輯的文字，本教學將示範完整的 Python 解決方案。你將學會如何從影像辨識文字、從影像擷取文字、將影像轉換為文字，並使用輕量化 AI 後處理器清理 OCR 文字。

本指南涵蓋從安裝必要套件到處理低品質影像的全部步驟，讓你能在任何自動化流程中整合 OCR，且不必猜測缺少哪一步。

## 你將會建立的功能

閱讀完本文後，你將擁有一個單一的 Python 腳本，能夠：

1. 載入影像檔案（PNG、JPEG 或 TIFF）。  
2. 使用 OCR 引擎辨識影像中的文字。  
3. 以 AI 驅動的後處理器提升原始輸出品質。  
4. 將清理過的文字輸出至主控台。

不需要任何外部服務——全部在本機執行，適用於離線環境或對隱私有高度要求的專案。

## 前置條件

- Python 3.9 或更新版本。  
- `pytesseract` 與 `Pillow` 套件（`pip install pytesseract pillow`）。  
- 已安裝 Tesseract‑OCR 二進位檔，且在系統 `PATH` 中可被找到。  
- 具備基本的 Python 函式概念。  

如果上述條件皆已具備，可直接跳至第一段程式碼區塊。

## 如何在 Python 中使用 OCR

**how to use OCR** 的核心在於初始化 OCR 引擎並將影像傳入。本教學使用 `pytesseract`，它是開源 Tesseract 引擎的輕量封裝。

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **為什麼這一步很重要** – Tesseract 需要乾淨且正確方向的影像。使用 Pillow 可確保在 OCR 執行前影像資料已正規化，從而提升後續 **recognize text from image** 操作的準確度。

## 從影像辨識文字

現在呼叫 `pytesseract.image_to_string` 以取得原始字串。這就是經典的「recognize text from image」呼叫。

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **為什麼要把功能拆開** – 將 OCR 步驟獨立，可在之後輕鬆換成其他引擎（例如改用 EasyOCR），而不必修改管線其他部分。也讓單元測試更方便。

## 從影像擷取文字並提升品質

原始 OCR 輸出常會出現換行、雜訊字元或辨識錯誤。AI 後處理器能自動清理這些雜訊。以下示範使用 `transformers` 套件在本機執行小型語言模型。若有需要，也可改用任何專屬服務。

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **為什麼 AI 後處理器有幫助** – 傳統 OCR 引擎擅長字元辨識，但在版面與噪聲處理上較弱。語言模型能理解上下文，將「Th1s 1s 4 test.」轉成「This is a test.」此步驟直接回應 **clean up OCR text** 的需求。

## 影像轉文字 – 完整腳本

將上述所有程式碼整合，即可得到一個 **convert image to text** 的端對端短腳本。

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### 預期輸出

以範例影像 (`sample.png`) 執行腳本，可能得到：

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

可以看到 AI 後處理器校正了錯讀的字元並移除多餘的換行。此範例展示了完整的 **extract text from image** 工作流程，並說明清理 OCR 文字的好處。

## 處理常見邊緣案例

| 情境                                   | 推薦調整方式                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------|
| 低對比度影像                           | 先轉成灰階，並使用 `ImageEnhance` 提升對比度後再送入 OCR。                     |
| 多語言文件                             | 在 `lang` 參數傳入逗號分隔的語言列表（例如 `lang='eng+fra'`）。                |
| 超大影像（> 2000 px）                  | 使用 `img.thumbnail((2000, 2000))` 縮小尺寸，以加速 Tesseract。                |
| 找不到 Tesseract 二進位檔               | 確認 `pytesseract.pytesseract.tesseract_cmd` 指向正確的執行檔路徑。            |
| AI 後處理器過慢                         | 改用更小的模型（如 `t5-small`）或在 GPU 上執行後處理器。                     |

> **專業小技巧**：如範例所示，在模組匯入時就快取 AI 模型物件 (`_ai_postprocessor`)，可避免每次呼叫都重新載入，對大量影像的處理延遲可大幅降低。

## 替代方案

- **EasyOCR**：純 Python OCR 套件，支援超過 80 種語言，無需外部二進位檔。若想使用純 pip 解決方案，可將 `ocr_recognize` 換成 `EasyOCR.Reader`。  
- **雲端 OCR API**：Google Cloud Vision、Azure Computer Vision 或 Amazon Textract 在處理複雜版面時精度更高，但需要網路存取與計費。  
- **自訂後處理**：若只需決定性清理，可使用正規表達式 (`re.sub`) 修正常見模式（例如去除連字換行），不必使用 AI 模型。

## 小結

現在你已掌握 **how to use OCR** 在 Python 中的完整流程，能夠從影像辨識文字、擷取文字、將影像轉文字，並使用 AI 後處理器清理 OCR 文字。完整腳本示範了一條可投入生產的管線，你可以再加入額外的前處理（降噪、去斜）或下游動作（寫入資料庫、送入搜尋索引）。

### 往後的步驟

- 嘗試不同的 AI 模型（如 `gpt‑2`、`flan‑ul2`），找出最適合你領域的清理效果。  
- 使用 Flask 或 FastAPI 將管線整合成 Web 服務，將腳本變成即時 OCR 端點。  
- 探索批次處理：遍歷影像資料夾，將每個清理後的輸出寫入對應的 `.txt` 檔案。

歡迎依照自己的工作流程調整程式碼，讓乾淨、可搜尋的文字為你的應用程式下一階段提供動力。祝編程愉快！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能在此基礎上延伸技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並探索在專案中實作的其他方式。

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}