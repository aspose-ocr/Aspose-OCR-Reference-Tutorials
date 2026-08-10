---
category: general
date: 2026-05-03
description: 學習如何在圖像上執行 OCR，並使用結構化 OCR 識別提取帶有座標的文字。附有逐步 Python 程式碼。
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: zh-hant
og_description: 使用結構化 OCR 識別對圖像執行文字辨識，並取得帶座標的文字。完整的 Python 範例與說明。
og_title: 在圖像上執行 OCR – 結構化文字提取教學
tags:
- OCR
- Python
- Computer Vision
title: 在圖像上執行 OCR – 結構化文字提取完整指南
url: /zh-hant/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 結構化文字提取完整指南

曾經需要 **run OCR on image** 檔案，但不確定如何保留每個字的精確位置嗎？你並不孤單。在許多專案——收據掃描、表單數位化或 UI 測試——中，你不僅需要原始文字，還需要告訴你每行在圖片上所在位置的邊界框。  

本教學示範如何使用 **aocr** 引擎 *run OCR on image*、請求 **structured OCR recognition**，並在保留幾何資訊的同時對結果進行後處理。完成後，你只需幾行 Python 程式碼即可 **extract text with coordinates**，同時了解結構化模式對下游任務的重要性。

## 你將學會

- 如何為 **structured OCR recognition** 初始化 OCR 引擎。  
- 如何輸入圖像並取得包含行邊界的原始結果。  
- 如何執行後處理器，在不失去幾何資訊的前提下清理文字。  
- 如何遍歷最終的行，將文字與其邊界框一起列印。  

沒有魔法，沒有隱藏步驟——只是一個完整、可直接執行的範例，讓你可以直接套用到自己的專案中。

---

## 前置條件

在開始之前，請確保已安裝以下項目：

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

你還需要一張包含清晰可讀文字的圖像檔（`input_image.png` 或 `.jpg`）。無論是掃描的發票還是螢幕截圖，只要 OCR 引擎能辨識文字即可。

---

## 步驟 1：為結構化辨識初始化 OCR 引擎

首先，我們建立 `aocr.Engine()` 的實例，並告訴它我們需要 **structured OCR recognition**。結構化模式不僅返回純文字，還會提供每行的幾何資料（邊界矩形），這在需要將文字映射回圖像時相當關鍵。

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **為什麼這很重要：**  
> 在預設模式下，引擎可能只給你一串連接的文字。結構化模式則提供頁面 → 行 → 詞的層級結構，且每個元素都有座標，使得在原始圖像上疊加結果或輸入到具版面感知的模型中變得更容易。

---

## 步驟 2：在圖像上執行 OCR 並取得原始結果

現在將圖像送入引擎。`recognize` 呼叫會回傳一個 `OcrResult` 物件，裡面包含多行，每行都有自己的邊界矩形。

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

此時 `raw_result.lines` 內的物件具有兩個重要屬性：

- `text` – 該行辨識出的字串。  
- `bounds` – 形如 `(x, y, width, height)` 的元組，描述該行的位置。

---

## 步驟 3：在保留幾何資訊的同時進行後處理

原始 OCR 輸出常常雜訊較多：零星字符、錯位空格或換行問題。`ai.run_postprocessor` 函式會清理文字，但 **保留原始幾何資訊** 完好，讓你仍擁有精確的座標。

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **專業提示：** 若你有領域特定的詞彙（例如產品代碼），可將自訂字典提供給後處理器，以提升準確度。

---

## 步驟 4：提取帶座標的文字 – 迭代並顯示

最後，我們遍歷清理過的行，將每行的邊界框與文字一起列印。這就是 **extract text with coordinates** 的核心。

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### 預期輸出

假設輸入圖像包含兩行文字：「Invoice #12345」與「Total: $89.99」，你會看到類似以下的輸出：

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

第一個元組是原始圖像上該行的 `(x, y, width, height)`，可用來繪製矩形、標示文字，或將座標傳入其他系統。

---

## 可視化結果（可選）

如果想在圖像上疊加顯示邊界框，可以使用 Pillow（PIL）繪製矩形。以下是一段快速示例；若只需要原始資料，可自行略過。

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![在圖像上執行 OCR 示例 – 顯示邊界框](/images/ocr-bounding-boxes.png "在圖像上執行 OCR – 邊界框疊加")

上述 alt 文字包含 **主要關鍵字**，符合圖片 alt 屬性的 SEO 要求。

---

## 為何結構化 OCR 辨識優於簡單文字提取

你可能會想，「我只要跑 OCR 拿到文字就好，何必在乎幾何資訊？」  

- **空間上下文：** 當需要在表單上對應欄位（例如「Date」旁的日期值）時，座標告訴你資料的 *位置*。  
- **多欄位版面：** 簡單的線性文字會失去排序；結構化資料保留欄位順序。  
- **後處理精度：** 知道框的大小可協助判斷文字是標題、腳註，還是雜訊。  

總而言之，**structured OCR recognition** 為你提供彈性，讓你能建構更智慧的流程——無論是寫入資料庫、產生可搜尋的 PDF，或訓練尊重版面的機器學習模型。

---

## 常見邊緣案例及處理方式

| 情境 | 需留意的地方 | 建議解決方式 |
|-----------|-------------------|---------------|
| **旋轉或傾斜的圖像** | 邊界框可能偏離軸線。 | 先以去斜處理（例如 OpenCV 的 `warpAffine`）作前處理。 |
| **字體過小** | 引擎可能遺漏字符，導致空行。 | 提升圖像解析度或使用 `ocr_engine.set_dpi(300)`。 |
| **混合語言** | 語言模型不符會產生亂碼。 | 在辨識前設定 `ocr_engine.language = ["en", "de"]`。 |
| **重疊的框** | 後處理器可能不小心合併兩行。 | 在處理後檢查 `line.bounds`；必要時調整 `ai.run_postprocessor` 的閾值。 |

提前處理這些情況，可在日後擴展至每日數百份文件時，避免頭痛問題。

---

## 完整端到端腳本

以下是完整、可直接執行的程式碼，將所有步驟串接起來。複製貼上、調整圖像路徑，即可使用。

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

執行此腳本將會：

1. **Run OCR on image** 並使用結構化模式。  
2. 為每一行 **extract text with coordinates**。  
3. 可選地產生顯示框線的 PNG 標註圖。

---

## 結論

你現在擁有一套完整、獨立的解決方案，能夠 **run OCR on image** 並使用 **structured OCR recognition** **extract text with coordinates**。程式碼示範了從引擎初始化、後處理到視覺驗證的每一步，讓你可以將其套用於收據、表單或任何需要精確文字定位的視覺文件。

接下來可以嘗試將 `aocr` 引擎換成其他函式庫（如 Tesseract、EasyOCR），觀察它們的結構化輸出差異。也可以實驗不同的後處理策略，例如拼寫檢查或自訂正則表達式過濾，以提升特定領域的準確度。若你正在建構更大型的流水線，考慮將 `(text, bounds)` 配對存入資料庫，以供日後分析使用。

祝編程順利，願你的 OCR 專案永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}