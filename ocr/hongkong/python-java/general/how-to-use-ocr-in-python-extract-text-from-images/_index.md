---
category: general
date: 2026-06-16
description: 如何在 Python 中使用 OCR 從 PNG 等圖像檔案提取文字。學習使用 Aspose OCR 逐步將圖像轉換為文字。
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: zh-hant
og_description: 如何在 Python 中使用 OCR 從圖像提取文字。本指南將帶您一步步將 PNG 檔案轉換為可搜尋的文字，使用 Aspose OCR。
og_title: 如何在 Python 中使用 OCR – 從圖片提取文字
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: 如何在 Python 中使用 OCR – 從圖像提取文字
url: /zh-hant/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 從圖像提取文字

有沒有想過在 Python 專案中 **如何使用 OCR**？你並不是唯一有此疑問的人。無論你是要建立收據掃描器、文件歸檔系統，或只是好奇如何將螢幕截圖轉換成可編輯的文字，**從圖像提取文字** 的能力都是改變遊戲規則的利器。

在本教學中，我們將一步步說明完整流程——從安裝 Aspose OCR 函式庫到讀取 PNG 檔案中的文字——讓你只需幾行程式碼即可 **將圖像轉換為文字**。完成後，你將清楚知道如何 **從 PNG 讀取文字**，甚至能自動處理多語言內容。

> **專業提示：** Aspose OCR 的自動語言偵測功能讓你不必事先猜測語言——對於跨國應用來說相當完美。

## 需要的條件

- Python 3.8+（最新的穩定版即可）
- 有效的 Aspose OCR 授權檔案 (`Aspose.OCR.lic`)。免費試用版可用於測試，但正式授權可移除評估限制。
- 透過 `pip` 安裝的 Aspose OCR 套件：

```bash
pip install aspose-ocr
```

- 你想要處理的圖像檔案——這裡以 `sample-multi-lang.png` 作為示範。

事先準備好上述前置條件，可讓流程順暢，避免之後出現 “module not found” 的錯誤。

![如何在 Python 中使用 OCR 工作流程](https://example.com/ocr-workflow.png "如何在 Python 中使用 OCR – 步驟說明圖")

*圖片說明文字：示意圖顯示如何在 Python 中使用 OCR 從圖像提取文字。*

## 步驟 1：套用你的 Aspose OCR 授權（每個應用程式只需一次）

任何嚴肅的 OCR 專案首先要做的事就是載入授權。若未載入，Aspose 會拋出警告並限制可處理的頁數。

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **為什麼這很重要：** 事先載入授權可確保 **ocr image to text python** 引擎全速運行且不會出現浮水印。把它想像成在開始轉換前先解鎖高級功能。

## 步驟 2：建立 OCR 引擎並啟用自動語言偵測

現在我們實例化核心引擎。啟用 `language_auto_detect` 在你不確定圖像中包含英語、西班牙語、中文或多種語言混合時尤為重要。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

如果你*事先*知道語言，可以設定 `ocr_engine.language = "English"`（或任何支援的 ISO 代碼）以提升速度。但對於一般的 “read text from PNG” 工具而言，自動偵測是最安全的選擇。

## 步驟 3：載入要處理的圖像

Aspose OCR 支援多種格式——PNG、JPEG、BMP、TIFF，應有盡有。現在載入一個包含多種語言的 PNG 檔案。

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **特殊情況：** 若圖像檔案過大（超過數 MB），你可能需要先縮小尺寸以提升效能。Aspose 提供 `ocr_image.resize(width, height)` 供此使用。

## 步驟 4：執行 OCR 辨識

所有設定完成後，實際的文字提取只需呼叫一次方法。結果物件會同時提供辨識出的文字與偵測到的語言。

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

在背後，Aspose 使用先進的神經網路與模式匹配演算法，將每個像素群轉換為字元。所有繁重運算皆在原生程式碼中完成，即使在一般硬體上也能得到 **快速、精確的 OCR**。

## 步驟 5：顯示偵測到的語言與辨識文字

最後，讓我們印出取得的結果。`detected_language` 屬性會告訴你 Aspose 猜測的語言，而 `text` 則包含完整的文字稿。

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### 預期輸出

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

如果在同時包含英語與日語的圖像上執行腳本，你會看到語言自動切換——這要歸功於先前啟用的自動偵測功能。

## 處理常見問題

### 1. 找不到授權檔案

如果看到類似 `License file not found` 的錯誤，請再次確認傳給 `set_license` 的路徑。使用原始字串 (`r"..."`) 可避免 Windows 上的跳脫字元問題。

### 2. 輸出為空白

空白的 `ocr_result.text` 通常表示圖像過於雜訊或文字太淡。嘗試提升圖像對比度：

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. 語言偵測錯誤

如果自動偵測選錯語言，你可以強制指定：

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## 擴充範例：批次處理多個 PNG 檔案

通常你會想要 **將圖像轉換為文字** 整個資料夾，而不只單一檔案。以下是一個快速迴圈，處理目錄中每個 PNG 檔案：

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

此程式碼片段示範了批量 **從圖像提取文字** 檔案的實用方法，這是文件數位化流程中常見的需求。

## 完整可執行腳本

將其儲存為 `ocr_demo.py`，執行 `python ocr_demo.py`，即可在主控台看到語言與文字的輸出。

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

## 結論

我們已從頭到尾說明了在 Python 中 **如何使用 OCR**，示範了如何 **從圖像提取文字**、**從 PNG 讀取文字**，以及一般使用 Aspose 強大引擎 **將圖像轉換為文字**。只要載入授權、啟用自動語言偵測，並將圖像傳入 `OcrEngine`，即可在數秒內取得乾淨且可搜尋的文字。

接下來可以怎麼做？試著將 Aspose 換成開源的 Tesseract 以比較準確度、嘗試 PDF 輸入，或將 OCR 步驟整合到 Flask API 以即時處理圖像。掌握了 **ocr image to text python** 的基礎後，想像力就是唯一的限制。

對於處理特殊字型、效能調校或授權有任何疑問？在下方留言，我們祝你編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟說明指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [使用 Aspose.OCR 以語言選擇方式提取圖像文字（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}