---
category: general
date: 2026-03-28
description: 對圖片執行光學字符辨識，取得帶有邊框座標的乾淨文字。學習如何提取 OCR、清理 OCR，並一步一步顯示結果。
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: zh-hant
og_description: 對圖像執行 OCR、清理輸出，並在簡潔教學中顯示邊框座標。
og_title: 在圖像上執行 OCR – 清晰的結果與邊框
tags:
- OCR
- Computer Vision
- Python
title: 對圖像執行 OCR – 清理結果並顯示邊框座標
url: /zh-hant/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 清理結果並顯示邊界框座標

有沒有過想 **在圖像上執行 OCR** 卻得到一堆雜亂文字，且不清楚每個字在圖片中的位置？你並不孤單。無論是發票數位化、收據掃描，或是簡單的文字擷取，取得原始 OCR 輸出只是第一道關卡。好消息是，你可以清理這些輸出，並立即看到每個區域的邊界框座標，且不需要寫大量樣板程式碼。

在本指南中，我們將逐步說明 **如何擷取 OCR**、執行 **如何清理 OCR** 的後處理，最後 **顯示每個清理後區域的邊界框座標**。完成後，你將擁有一個可直接執行的腳本，能把模糊的照片轉換成整齊、結構化的文字，供後續處理使用。

## 你需要的環境

- Python 3.9+（以下語法在 3.8 及以上皆可執行）
- 支援 `recognize(..., return_structured=True)` 的 OCR 引擎——例如本文片段中使用的虛構 `engine` 函式庫。實際使用時可改成 Tesseract、EasyOCR 或任何會回傳區域資料的 SDK。
- 基本的 Python 函式與迴圈概念
- 一張想要掃描的圖像檔（PNG、JPG 等）

> **專業小技巧：** 若使用 Tesseract，`pytesseract.image_to_data` 已經會回傳邊界框。只要把它的結果包裝成一個小型適配器，模擬下方 `engine.recognize` 的 API 即可。

---

![在圖像上執行 OCR 範例](image-placeholder.png "在圖像上執行 OCR 範例")

*Alt text: 顯示如何在圖像上執行 OCR 並視覺化邊界框座標的示意圖*

## 步驟 1 – 在圖像上執行 OCR 並取得結構化區域

首先，要請 OCR 引擎回傳的不僅是純文字，而是一個包含文字區域的結構化清單。此清單會同時提供原始字串與包圍它的矩形。

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**為什麼這很重要：**  
只取得純文字會失去空間資訊。結構化資料讓你之後可以 **顯示邊界框座標**、將文字對齊到表格，或將精確位置傳給下游模型。

## 步驟 2 – 使用後處理器清理 OCR 輸出

OCR 引擎雖然擅長辨識字元，但常會留下多餘的空格、換行符或錯誤辨識的符號。後處理器會正規化文字、修正常見的 OCR 錯誤，並去除多餘的空白。

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

如果你自行開發清理程式，可考慮以下做法：

- 移除非 ASCII 字元（`re.sub(r'[^\x00-\x7F]+',' ', text)`）
- 將多個連續空格合併為單一空格
- 使用 `pyspellchecker` 等拼字檢查工具修正明顯的錯別字

**為什麼你需要在意：**  
乾淨的字串在搜尋、索引以及後續的 NLP 流程中會更可靠。換句話說，**如何清理 OCR** 常常是資料可用與頭痛之間的分水嶺。

## 步驟 3 – 為每個清理後的區域顯示邊界框座標

文字整理好之後，我們遍歷每個區域，印出其矩形與清理過的字串。這一步就是最終 **顯示邊界框座標** 的地方。

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**範例輸出**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

接著，你可以把這些座標傳給繪圖函式庫（例如 OpenCV）在原圖上疊加方框，或是存入資料庫以供日後查詢。

## 完整、可直接執行的腳本

以下程式碼把上述三個步驟整合成一個完整範例。只要把佔位的 `engine` 呼叫換成實際的 OCR SDK 即可。

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### 如何執行

```bash
python perform_ocr.py sample_invoice.jpg
```

執行後，你應該會看到一串邊界框與清理後文字的列表，與上方範例輸出相同。

## 常見問題與特殊情況

| 問題 | 解答 |
|----------|--------|
| **如果 OCR 引擎不支援 `return_structured`，該怎麼辦？** | 寫一個薄層封裝器，將引擎的原始輸出（通常是帶座標的單字清單）轉換成具備 `text` 與 `bounding_box` 屬性的物件。 |
| **可以取得信心分數嗎？** | 許多 SDK 會提供每個區域的信心指標。只要在印出語句中加入：`print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")` 即可。 |
| **如何處理旋轉文字？** | 在呼叫 `recognize` 前，先使用 OpenCV 的 `cv2.minAreaRect` 進行去斜處理。 |
| **如果需要 JSON 格式的輸出呢？** | 使用 `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` 序列化 `processed_result.regions`。 |
| **有沒有方法可視化這些方框？** | 在迴圈內使用 OpenCV：`cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)`，然後 `cv2.imwrite("annotated.jpg", img)`。 |

## 結語

你剛剛學會了 **如何在圖像上執行 OCR**、清理原始輸出，並 **顯示每個區域的邊界框座標**。這套「辨識 → 後處理 → 迭代」的三步流程是一個可重複使用的模式，能輕鬆嵌入任何需要可靠文字擷取的 Python 專案。

### 接下來可以做什麼？

- **探索不同的 OCR 後端**（Tesseract、EasyOCR、Google Vision）並比較準確度。
- **結合資料庫**，將區域資料儲存起來，打造可搜尋的檔案庫。
- **加入語言偵測**，讓每個區域自動走對應的拼字檢查流程。
- **在原圖上疊加方框** 以進行視覺驗證（參考上方的 OpenCV 片段）。

若在實作過程中遇到怪異情況，請記得：最關鍵的勝利往往來自穩固的後處理步驟；乾淨的字串遠比一堆原始字符更易於操作。

祝程式開發順利，願你的 OCR 流程永遠保持整潔！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}