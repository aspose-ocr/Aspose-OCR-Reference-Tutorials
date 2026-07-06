---
category: general
date: 2026-01-12
description: 使用 Python 快速對 PNG 檔案執行 OCR。了解如何從圖像和發票中提取文字，並使用 Aspose.OCR 載入圖像進行 OCR。
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: zh-hant
og_description: 即時對 PNG 進行 OCR。本指南示範如何從圖片與發票中提取文字、載入圖片進行 OCR，並將結果儲存為 JSON 與 CSV。
og_title: 在 PNG 上執行 OCR – 完整 Python 教學
tags:
- OCR
- Python
- Image Processing
title: 在 PNG 上執行 OCR – 完整的 Python 圖像文字提取指南
url: /zh-hant/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PNG 上執行 OCR – 完整的 Python 指南，從圖像中提取文字

曾經需要 **在 PNG 上執行 OCR**，卻不確定哪個函式庫能提供乾淨、結構化的結果嗎？你並不孤單。在許多實務專案中——例如發票自動化或收據掃描——第一步就是 **從圖像中提取文字**，而 PNG 是常見的格式，因為它保留了無損品質。

在本教學中，我們將以 Aspose.OCR Python 套件示範一個實作範例。完成本指南後，你將會知道如何 **載入圖像以進行 OCR**、提取每一行文字、將資料轉換為整齊的 JSON 物件，甚至匯出為 CSV 供後續處理。沒有冗長說明，只有實用、可直接執行的解決方案。

## 你將學會

- 如何安裝與匯入 Aspose.OCR 函式庫。  
- 執行 **在 PNG 上執行 OCR** 並處理結果物件的完整步驟。  
- 從 **發票** 檔案中 **提取文字** 並將輸出格式化為 JSON 或 CSV 的方法。  
- 處理低對比度圖像、多語言文件與信心分數的技巧。  
- 一個完整、可直接複製貼上的程式碼範例，讓你今天就能執行。

> **前置條件：** Python 3.8 以上，且具備基本的 pip 使用經驗。如果你從未使用過 Aspose，也不必擔心——本指南涵蓋了入門所需的一切。

## 步驟 1 – 安裝 Aspose.OCR 並準備環境

在我們能 **在 PNG 上執行 OCR** 之前，必須先在系統上安裝此函式庫。

```bash
pip install aspose-ocr
```

> **小技巧：** 使用虛擬環境（`python -m venv venv`）來隔離相依套件。若同時處理多個專案，可避免版本衝突。

安裝完成後，匯入我們需要的模組：

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

此處引入 `asposeocr` 以負責主要的 OCR 工作，並使用內建的 `json` 函式庫以便之後的序列化。

## 步驟 2 – 建立 OCR 引擎並設定語言

OCR 引擎是實際讀取像素的核心元件。對於大多數英文發票，你會需要英文語言套件：

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **為什麼這很重要：** 指定語言會縮小字元集合，從而提升準確度並加快處理速度。如果需要處理多語言發票，只要將 `ocr.Language.ENGLISH` 替換為相應的列舉即可。

## 步驟 3 – 載入圖像以進行 OCR

現在我們要 **載入圖像以進行 OCR**。`Image.load` 方法接受檔案路徑，且支援 PNG、JPEG、BMP 等格式。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **特殊情況：** 如果 PNG 檔案異常大（超過 5 MB），建議先調整大小以降低記憶體使用。Pillow 可在一行程式碼內完成：

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## 步驟 4 – 在 PNG 上執行 OCR 並取得結果

引擎已就緒且圖像已載入，現在可以 **在 PNG 上執行 OCR** 並取得結構化結果。

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` 物件包含一系列 `OcrRegion` 項目，每個項目都有辨識出的文字與信心分數（0‑100）。這就是取得 **從發票中提取文字** 所需的細節資料的地方。

## 步驟 5 – 將結果轉換為 JSON 並美化輸出

大多數下游系統都偏好 JSON，因此我們將 OCR 輸出轉換為格式化的字串。

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### 範例輸出

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

請注意每一行都包含信心指標——若你打算自動 **從發票中提取文字**，可用於過濾低信心的條目。

## 步驟 6 – 將 OCR 資料儲存為 CSV（每行文字 + 信心）

CSV 非常適合用於試算表或快速資料匯入。Aspose 提供一行程式碼即可將所有資料匯出為 CSV 檔案。

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

產生的 CSV 會是這樣的：

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

現在你可以在 Excel、Google Sheets 開啟，或將其匯入資料庫。

## 加分項 – 處理低信心文字與多頁 PDF

### 依信心過濾

如果只想保留高信心的行，請在寫出之前先過濾 JSON：

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### 多頁文件

Aspose.OCR 會自動為多頁 PNG 或 PDF 的每一頁建立新的 `page` 條目。遍歷 `ocr_data["pages"]` 即可處理全部頁面——不需要額外程式碼。

## 完整範例程式

以下是你可以直接複製、貼上並執行的 **完整腳本**。將 `YOUR_DIRECTORY` 替換為存放 PNG 檔案的資料夾路徑。

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

使用 `python run_ocr.py` 執行腳本，你將在主控台看到 JSON 輸出、磁碟上的 CSV 檔案，以及高信心條目的過濾清單。

## 常見問題

**Q: 我可以用這個來從掃描的收據而非發票中提取文字嗎？**  
A: 當然可以。工作流程相同，只要把 `image_path` 指向你的收據 PNG。如果收據使用其他語言，請相應調整 `engine.language`。

**Q: 如果我的 PNG 包含旋轉的文字該怎麼辦？**  
A: Aspose.OCR 會自動偵測方向，但對於較頑固的情況，你可以在送入引擎前使用 Pillow 手動旋轉圖像。

**Q: 使用 Aspose.OCR 是否需要付費授權？**  
A: 此函式庫提供帶有浮水印的免費評估模式。若要在正式環境使用，需購買授權，可從 Aspose 官方網站取得。

## 結論

我們已完整說明如何使用 Python **在 PNG 上執行 OCR**：安裝 SDK、載入圖像、提取結構化文字，並將結果儲存為 JSON 或 CSV。無論你是想為簡單腳本 **從圖像中提取文字**，或為自動化會計流程 **從發票中提取文字**，上述步驟都提供了穩固、可投入生產的基礎。

接下來，你可以探索：

- 將 CSV 輸出整合至資料庫，以批次儲存發票。  
- 使用正規表達式進行後處理，抽取日期、金額或稅號。  
- 若發票含有 QR Code，可使用 `ocr_engine.recognize_barcode` 功能。

試試看，調整信心門檻，讓你的文件處理流程變得輕鬆自如。還有其他問題或想分享有趣的使用案例嗎？在下方留言吧——祝 OCR 順利！

![在 PNG 上執行 OCR 範例](run-ocr-on-png.png "在 PNG 上執行 OCR – OCR 結果的視覺範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}