---
category: general
date: 2026-01-12
description: 如何快速執行 OCR 並將圖像轉換為文字。學習辨識特殊字符、從圖像提取文字，以及使用完整的 Python 範例載入圖像進行 OCR。
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: zh-hant
og_description: 如何在 Python 中執行 OCR，將圖像轉換為文字，並辨識特殊字元。跟隨本實作指南，從圖像中提取文字。
og_title: 如何在 Python 中執行 OCR – 完整教學
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中執行 OCR – 步驟指南
url: /zh-hant/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中執行 OCR – 步驟指南

是否曾需要在包含拉丁文和西里爾字元的螢幕截圖上**執行 OCR**？你並不孤單。在許多專案中——無論是數位化收據、索引多語言文件，或建立可搜尋的檔案庫——**如何執行 OCR**很快就會成為最關注的問題。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明如何**將影像轉換為文字**、**辨識特殊字元**，以及**從影像中擷取文字**，全部使用簡單的 Python 函式庫。完成後，你將擁有一個即時可執行的腳本，能載入影像進行 OCR、處理多語言內容，並輸出結果。

## 需要的條件

- 已在電腦上安裝 Python 3.8+。  
- 透過 `pip install ocr` 安裝 `ocr` 套件（或任何相容的 OCR 函式庫）。  
- 一個包含拉丁文與西里爾字形的影像檔 (`multilingual.png`)。  
- 基本的文字編輯器或 IDE——VS Code、PyCharm，甚至簡單的 Notepad 都可。  

如果沒有 `ocr` 套件，你可以改用 `pytesseract`，只需做少量修改；核心概念保持不變。

## 步驟 1：安裝與匯入 OCR 函式庫

首先，讓我們準備好 OCR 引擎。接著匯入函式庫、建立引擎實例，並設定多語言支援。

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**為什麼這很重要：**  
建立引擎是基礎——沒有它就無法在之後**載入影像進行 OCR**。啟用語言套件可確保引擎正確辨識像 “Ŀ”、 “Ҕ”、 “Ǣ” 這類字元。若跳過此步，非拉丁文字將會產生亂碼輸出。

## 步驟 2：載入包含多語言文字的影像

現在將引擎指向要處理的檔案。路徑可以是絕對或相對，只要確保指向可讀取的影像即可。

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![如何執行 OCR 範例](/images/ocr-example.png "在多語言影像上執行 OCR")

**為什麼這很重要：**  
`load_image` 會將像素資料讀入記憶體，為 OCR 演算法做準備。若影像過大，引擎可能會自動降解析度；之後可使用 `engine.set_max_resolution(3000)` 進行微調，以處理高解析度掃描。

## 步驟 3：執行辨識程序

引擎已備妥且影像已載入，現在可以正式擷取文字內容。

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**為什麼這很重要：**  
`recognize()` 在背後執行龐大的神經網路運算。它會回傳一個物件，內含原始文字、信心分數，甚至在需要視覺除錯時的邊界框資訊。

## 步驟 4：輸出辨識文字

讓我們看看引擎找到了什麼。這裡會將文字印到主控台，你也可以寫入檔案或資料庫。

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### 預期輸出

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

如果看到類似的結果，恭喜你——已成功**將影像轉換為文字**並**辨識特殊字元**。

## 處理常見問題

即使腳本相當簡潔，仍可能遇到一些小障礙。以下是我個人實務經驗中的實用技巧。

### 1. 缺少語言套件

如果看到問號 (`?`) 取代西里爾字母，請再次確認已安裝相應的語言套件。對於許多 OCR 引擎，需要下載對應的 `.traineddata` 檔案，並放置於引擎的 `tessdata` 資料夾中。

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. 影像品質低

模糊或低對比度的影像會導致信心分數下降。可使用 OpenCV 先行前處理影像：

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. 大檔案與記憶體使用

處理 10 MB 的照片可能會激增記憶體使用量。可使用 `engine.set_max_image_size(2000)` 限制解析度，或將影像切割成多塊分別 OCR。

### 4. 捕獲邊界框

若需要標示每個單字出現的位置（對 UI 疊加很有用），可存取 `result.boxes`：

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## 完整腳本 – 一鍵執行

將上述所有步驟整合在一起，以下是一個可直接以 `python ocr_demo.py` 執行的單一檔案。內含錯誤處理、可選前處理，以及說明性註解。

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

執行方式：

```bash
python ocr_demo.py path/to/multilingual.png
```

執行後應會看到先前示範的相同輸出，證明已成功**從影像中擷取文字**。

## 結論

我們已從頭到尾說明了在 Python 中**如何執行 OCR**：安裝函式庫、載入影像、辨識多語言內容，並處理最常見的邊緣案例。依照本指南，你現在可以在自己的專案中**將影像轉換為文字**、**辨識特殊字元**，以及**從影像中擷取文字**——不再需要手動抄寫。

接下來可以嘗試：

- 新增更多語言套件（例如 `spa` 代表西班牙語）。  
- 將結果匯出為 JSON，以供後續處理。  
- 將 OCR 步驟整合至 Flask API，讓其他服務呼叫。  

若遇到任何奇怪的情況，OCR 函式庫的社群相當活躍——可搜尋 “ocr library language pack installation” 或在下方留言。祝編程愉快，盡情將圖片變成可搜尋的文字吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}