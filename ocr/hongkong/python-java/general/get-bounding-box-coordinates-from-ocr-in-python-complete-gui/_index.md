---
category: general
date: 2026-06-22
description: 使用 Python 從圖像獲取邊界框座標。學習如何在數分鐘內使用 Aspose OCR 及 JSON 解析從圖片中提取文字。
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: zh-hant
og_description: 使用 Python 從圖像取得邊界框座標。本指南示範如何使用 Aspose OCR 於 Python 提取圖像文字並解析版面資料。
og_title: 使用 Python 從 OCR 獲取邊界框座標 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: 從 OCR 獲取 Python 中的邊界框座標 – 完整指南
url: /zh-hant/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 OCR 獲取 Python 中的邊界框座標 – 完整指南

是否曾需要 **取得每個單詞的邊界框座標** 以處理掃描發票，但不知從何開始？你並不孤單。在許多自動化專案中，需要在影像上定位文字以進行標註、遮蔽或輸入後續分析。好消息是，只要幾行 Python 程式碼加上 Aspose.OCR，就能一次取得文字 **以及** 其精確位置。

在本教學中，我們將手把手示範一個實作範例，說明如何 **以 image python 風格抽取文字**，再深入 JSON 版面資料取得那些邊界框。沒有多餘說明，只有可執行的腳本、每一步重要性的說明，以及避免常見陷阱的技巧。

---

## 你將會建立什麼

完成本指南後，你將擁有一個可直接執行的 Python 腳本，具備以下功能：

1. 載入影像（例如發票 PNG）至 Aspose OCR。
2. 設定引擎輸出 JSON 版面資訊。
3. 將 JSON 解析為 Python 字典。
4. 逐一遍歷每個辨識出的單詞，印出其文字 **以及** 邊界框座標。

你也會看到如何將程式碼套用於多頁 PDF、不同影像格式，以及自訂座標系統。

### 前置條件

- 已在機器上安裝 Python 3.8+。  
- 具備有效的 Aspose.OCR for Python 授權或免費試用版（未授權時仍可使用，但會加上浮水印）。  
- `pip install aspose-ocr`（PyPI 上的套件名稱）。  
- 準備一張名為 `invoice.png` 的範例影像，放在可參照的資料夾內。

就這樣——不需要大型框架，也不需要外部服務。讓我們開始吧。

---

## Step 1: Install and Import the Required Libraries

首先，確保已安裝 Aspose OCR 套件，且內建的 `json` 模組可用。`json` 模組隨 Python 一起提供，我們只需要安裝 Aspose。

```bash
pip install aspose-ocr
```

現在在腳本中匯入它們：

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **為什麼這很重要：** 匯入 `aspose.ocr` 後即可使用高效能的 OCR 引擎，而 `json` 則讓你把原始版面字串轉換為原生的 Python 字典，方便遍歷。

---

## Step 2: Create the OCR Engine and Load Your Image

引擎是整個流程的核心。先實例化它，然後指向要掃描的影像。

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **專業提示：** 請將 `"YOUR_DIRECTORY/invoice.png"` 替換為指向實際檔案的絕對或相對路徑。若找不到檔案，Aspose 會拋出 `FileNotFoundError`，請務必檢查拼寫。

---

## Step 3: Configure the Engine to Output JSON Layout Data

Aspose OCR 可以回傳純文字、僅 OCR 的 JSON，或包含單詞、行甚至單字座標的完整版面 JSON。若要 **取得邊界框座標**，我們需要版面 JSON。

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **為什麼使用 JSON？** JSON 與語言無關、易於閱讀，且能直接映射為 Python 字典。版面 JSON 包含一個 `"words"` 陣列，每個條目都保存文字與一個由八個數字組成的 `boundingBox` 陣列（四個角點座標）。

---

## Step 4: Run Recognition and Grab the Raw JSON String

現在真正執行 OCR。`recognize()` 方法會回傳 `OcrResult` 物件，我們可以從中取得 JSON 字串。

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

如果列印 `layout_json`，會看到類似以下的內容：

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **邊緣情況：** 某些影像可能產生空的 `"words"` 陣列，表示 OCR 引擎無法偵測到任何文字。此時請先確認影像品質（對比度、解析度）再繼續。

---

## Step 5: Parse the JSON into a Python Dictionary

使用原生 Python 結構遠比字串處理來得簡單。利用 `json.loads()` 函式將字串轉換為字典。

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

現在 `layout_data["words"]` 是一個字典列表，每個元素代表一個單詞及其邊界框。

---

## Step 6: Iterate Over Words and **Get Bounding Box Coordinates**

以下是本教學的核心：遍歷每個單詞、擷取文字，並印出座標。這正是我們 **取得邊界框座標** 的地方。

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**範例輸出**（數值會因影像而異）：

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **為什麼是八點格式？** 四個角點（左上、右上、右下、左下）讓你即使在文字傾斜時也能畫出多邊形。如果只需要簡單的矩形，可計算 `x_min = min(x1, x2, x3, x4)`、`y_min = min(y1, y2, y3, y4)`、`width = max(x…) - x_min`，以及 `height = max(y…) - y_min`。

---

## Optional Enhancements

### 1. Convert Bounding Boxes to Simple Rectangles

如果下游工具期待 `(x, y, width, height)` 而非八點座標，可加入以下輔助函式：

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Handle Multi‑Page PDFs

Aspose OCR 能接受 PDF 串流。將載入影像的程式碼改為：

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

再對每一頁呼叫 `set_page_number`，即可收集各頁的座標。

### 3. Visualize Bounding Boxes

若想在原始影像上看到框線，可使用 Pillow：

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

現在你會看到每個辨識單詞周圍的紅色輪廓——非常適合除錯或 UI 疊加。

---

## Common Questions & Gotchas

- **如果 JSON 很大怎麼辦？** 對於大型文件，建議串流處理 JSON 或逐頁解析，以降低記憶體使用量。  
- **為什麼有些單詞會遺失？** 低對比度或手寫文字常讓 OCR 引擎失效。請在送入 Aspose 前先對影像做前處理（提升對比度、二值化）。  
- **能取得字元層級的座標嗎？** 可以——設定 `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`，即可取得包含各自 `boundingBox` 的 `"characters"` 陣列。  
- **座標系統是從 0 開始嗎？** 完全正確。(0, 0) 為影像左上角。

---

## Full Script – Ready to Copy & Run

以下是完整、可直接執行的範例，結合了所有步驟。將其儲存為 `extract_bboxes.py`，然後執行 `python extract_bboxes.py`。

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


以下教學與本指南所示技術緊密相關，能進一步擴展你的應用。每個資源皆提供完整可執行的程式碼範例，並附有逐步說明，協助你掌握更多 API 功能，或在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}