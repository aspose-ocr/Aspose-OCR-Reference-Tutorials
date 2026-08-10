---
category: general
date: 2026-06-25
description: Python OCR 教學，示範如何提取文字 PNG 檔案、讀取文字圖像，並使用簡單、免授權費的引擎辨識圖像文字。
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: zh-hant
og_description: Python OCR 教學教你如何載入影像進行 OCR、提取文字 PNG 檔案，並只需幾行程式碼即可辨識影像文字。
og_title: Python OCR 教學 – 從 PNG 中提取文字
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: Python OCR 教學：從 PNG 圖片提取文字
url: /zh-hant/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教學 – 從 PNG 圖片擷取文字

有沒有想過 **python ocr tutorial** 如何把收據的螢幕截圖轉成可編輯的文字？你並不孤單。在許多實務專案中，我們需要快速 *read text image* 檔案，而自行處理比每次從 GUI 複製貼上更有效率。

在本指南中，我們將手把手示範一個 **extract text PNG** 的範例，說明如何 *load image for OCR*，最後列印 *recognize image text* 的結果——全部使用免費、僅供評估的 OCR 引擎。無需授權金鑰，無需龐大相依套件——只要純 Python 加上幾個小套件。

## 你將學到

- 如何安裝與匯入輕量級 OCR 函式庫。
- **load image for OCR** 的完整步驟與常見陷阱的處理方式。
- 讀取不同品質 *read text image* 檔案的方法。
- 提升 **extract text png** 準確度的技巧。
- 如何顯示辨識出的字串，並可選擇寫入磁碟。

完成本教學後，你將擁有一個可重複使用的腳本，能在任何需要即時 **recognize image text** 的專案中直接套用。沒有魔法，只有清晰的程式碼與說明。

### 前置條件

- Python 3.8 或更新版本（函式庫支援 3.7+，建議使用 3.8+）。
- 基本的 pip 與虛擬環境操作概念。
- 一個名為 `sample.png`（或任意 PNG） 的圖片檔，放在可參照的資料夾內。

如果上述任一項你不熟悉，請先暫停一下完成設定——相信我，收穫絕對值得。

---

## Python OCR 教學 – 設定引擎

首先，我們需要建立一個 OCR 引擎物件。這次使用的函式庫是一個針對原生 OCR 引擎的輕量封裝，開箱即用且僅供評估。它不需要授權金鑰，讓 *python ocr tutorial* 成為快速原型的理想選擇。

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**為什麼這很重要：** 建立引擎可將 OCR 執行環境與其他程式碼分離，讓你在處理多張圖片時不必每次都重新初始化沉重的資源。

---

## Load Image for OCR – 讀取 PNG 檔案

引擎建立好之後，我們必須 *load image for OCR*。函式庫的 `Image.load` 方法接受檔案路徑，會自動解碼 PNG、JPEG、BMP 等格式。

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **專業小技巧：** 若你的 PNG 含有 alpha 通道，函式庫會自動捨棄它。然而，為了在 *read text image* 任務中取得最佳效果，建議先將圖片轉成灰階——這樣能減少雜訊並加速辨識。

---

## Recognize Image Text – 執行 OCR 引擎

當圖片物件準備好後，我們終於可以 **recognize image text**。這是 *python ocr tutorial* 的核心，只需要一行程式碼。

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**底層發生了什麼？** 引擎會先執行一系列前處理濾鏡（去斜、二值化），再將位圖送入訓練了數百萬字元的神經網路。因此，即使是低解析度的 PNG，也常能得到相當準確的輸出。

---

## 顯示與儲存擷取的文字

取得結果固然好，但你可能想要檢視或保存它。`result` 物件提供一個 `text` 屬性，內含純文字字串。

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**預期輸出**（假設 `sample.png` 內的文字為 “Hello, OCR!”）：

```
Eval-mode result: Hello, OCR!
```

如果看到的是亂碼而非可讀文字，請參考下一節的常見修正方法。

---

## 處理常見問題 – 當你 Extract Text PNG 時

即使是最好的 OCR 引擎，也會在特定圖片上卡關。以下列出常見障礙與解決方式。

### 1. 低對比或深色背景

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. 文字傾斜

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. 非英文字元

若你的 PNG 含有重音字母或非拉丁文字，請以相應的語言套件初始化引擎：

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. 超大圖片

處理 4000×3000 的 PNG 可能會很慢。可在保留可讀性的前提下先縮小尺寸：

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

這些調整是 *python ocr tutorial* 在非理想情況下仍能順利運作的關鍵。

---

## 完整腳本 – 單檔解決方案

以下提供完整、可直接執行的腳本，已整合所有步驟與可選的優化。將它複製貼上至 `ocr_extract.py`，然後執行 `python ocr_extract.py`。

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**執行方式：**  
```bash
python ocr_extract.py ./sample.png
```

執行後，你應該會在螢幕上看到辨識出的字串，且在圖片旁產生 `sample_extracted.txt` 檔案。

---

## 視覺概覽

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Python OCR tutorial 圖示，說明從 load image for OCR 到 extract text PNG 的流程圖。*

此圖示說明了 **load image for OCR** → **recognize image text** → **extract text PNG** 的線性流程，並標示出可插入前處理步驟的地方。

---

## 結論

我們剛完成一個 **python ocr tutorial**，示範了如何 *load image for OCR*、*recognize image text*，最後以簡單的 Python 指令 **extract text png**。此腳本功能完整，能處理常見的例外情況，亦可擴充為批次處理或多語言支援。

準備好挑戰下一個目標了嗎？試著將 PDF 轉成圖片後餵給引擎、使用不同語言套件，或把 OCR 步驟整合到 Flask API，讓你的 Web 應用即時讀取上傳的螢幕截圖。*read text image* 的自動化可能性幾乎無限。

有任何問題或遇到難以破解的圖片嗎？在下方留言，我們一起排除故障。祝 coding 愉快！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能在此基礎上延伸技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}