---
category: general
date: 2026-06-28
description: 學習如何從圖像中辨識文字，並使用 Aspose OCR for Python 執行圖像 OCR。包括設定 OCR 語言及提取信心分數的步驟。
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: zh-hant
og_description: 使用 Aspose OCR 在 Python 中辨識圖像文字。本指南說明如何設定 OCR 語言、對圖像執行 OCR，以及讀取信心等級。
og_title: 從圖像辨識文字 – 完整 Python OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: 使用 Aspose OCR 從圖像識別文字 – 完整 Python 指南
url: /zh-hant/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 進行圖像文字辨識 – 完整 Python 指南

是否曾需要 **從圖像中辨識文字**，卻不確定哪個函式庫能同時提供速度與準確度？你並不孤單。在文件自動化的世界裡，**對圖像檔執行 OCR** 是日常需求——無論是數位化收據、掃描護照，或是從多語言標示中擷取資料。

本教學將手把手示範如何使用 Aspose OCR for Python 來 **從圖像中辨識文字**，同時說明 **如何設定 OCR 語言**，讓引擎知道是拉丁文、斯拉夫文或其他文字。完成後，你將擁有一個可直接執行的腳本，能印出完整文字、逐行信心分數，甚至每個單字的邊界框。

## 需要的環境

- **Python 3.8+**（程式碼在任何近期版本皆可執行）
- **Aspose.OCR for Python via Java** 套件 ─ 以 `pip install aspose-ocr` 安裝
- 一張圖像檔（例如 `mixed_script.png`），內含你想擷取的文字
- 基本的 IDE 或編輯器──VS Code、PyCharm，或簡單的文字編輯器皆可

不需要繁重的相依套件，也不必編譯原生二進位檔。只要 pip 安裝一次，即可開始。

## 步驟 1：安裝並匯入 OCR 引擎

首先，將函式庫安裝到你的機器上，並匯入所需的類別。

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **小技巧：** 若你身處公司內部網路且需要代理伺服器，請在 pip 指令後加上 `--proxy` 參數。這能省下日後大量的除錯時間。

## 步驟 2：建立引擎並 **how to set OCR language**

建立 `OcrEngine` 實例只要呼叫建構子即可，但真正的威力在於告訴引擎預期的語言。這正是回答 “**how to set OCR language**” 的關鍵。

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

為什麼這麼重要？OCR 演算法會使用語言特定的字元模型；正確設定語言能大幅提升準確度，尤其是字形相近的腳本（例如拉丁文的 “0” 與 “O”，以及斯拉夫文的 “О”）。

## 步驟 3：**perform OCR on image** – 辨識文字

現在把圖像路徑交給引擎，讓它自行處理。此方法會回傳一個 `RecognitionResult` 物件，內含所有你可能需要的資訊。

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

若找不到檔案，Aspose 會拋出 `FileNotFoundError`。在正式環境建議使用 `try/except` 包住呼叫，以免未處理的例外導致服務中斷。

## 步驟 4：輸出完整辨識文字

最常見的需求就是 “給我文字”。`getText()` 方法會把所有偵測到的行合併成單一字串。

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

執行結果可能類似：

```
Full text: Hello World!
This is a sample mixed‑script image.
```

這就是 **recognize text from image** 的核心──一行程式碼即可取得引擎解讀的全部內容。

## 步驟 5：（可選）顯示每行的信心分數

信心分數可協助判斷可靠度。分數低於 0.70 的行可能需要人工審核。

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

典型輸出：

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## 步驟 6：（可選）取得每個單字的邊界框 – 方便 UI 高亮

若你在開發一個檢視器，讓使用者點擊單字即可看到其 OCR 資料，邊界框座標就是關鍵資訊。

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

範例輸出：

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

座標以像素為單位，基於原始圖像，因此可直接在畫布上疊加顯示。

## 完整可執行腳本

將上述所有步驟整合，以下是一個可直接執行的腳本範例。只需把 `YOUR_DIRECTORY/mixed_script.png` 替換成實際的圖像路徑即可。

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

執行方式：

```bash
python ocr_demo.py
```

執行後，你會在主控台看到完整的文字、信心分數與邊界框資訊。

## 常見問題與特殊情況

### 圖像中包含多種語言該怎麼辦？

Aspose OCR 支援多語言偵測，只要傳入 **組合語言旗標** 即可。例如，同時辨識拉丁文與斯拉夫文：

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

使用管道符號 (`|`) 合併列舉值。這樣即可滿足 “**perform OCR on image**” 在多語言情境下的需求。

### 如何提升低解析度圖像的辨識準確度？

- **前置處理**：提升對比、二值化，或使用 Pillow 等函式庫放大圖像。
- **設定正確的 DPI**：若已知 DPI，Aspose 會依據圖像的 metadata 進行處理。
- **選擇正確的語言**：語言設定越精確，模型表現越好。

### 能只擷取圖像的特定區域嗎？

可以。使用 `recognizeRegion` 方法（基本範例未示）並傳入定義感興趣區域的矩形物件。這在只需要表格或特定文字區塊時非常實用。

## 結論

我們已完整示範如何使用 Aspose OCR for Python **recognize text from image**，包括 **perform OCR on image**、正確 **set OCR language**，以及取得信心分數與單字層級的邊界框，供後續 UI 使用。

接下來你可以：

- 嘗試其他語言 (`Language.Arabic`, `Language.Japanese` 等)
- 將腳本整合至 Web 服務（Flask/Django），提供 OCR API
- 結合邊界框資料與前端 Canvas，讓使用者自行高亮文字

只要有需要數位化的文件，可能性就無限。遇到難辨識的圖像嗎？留下評論，我們一起排除問題。祝開發順利！

![recognize text from image example](/images/ocr_example.png "recognize text from image – Aspose OCR output")


## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你對 API 功能的掌握，並探索在實際專案中的其他實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}