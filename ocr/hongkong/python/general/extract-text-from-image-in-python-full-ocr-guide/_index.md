---
category: general
date: 2026-06-25
description: 使用 Python OCR 從圖像提取文字。了解如何載入圖像進行 OCR、在 Python 中執行 OCR，以及將收據轉換為 JSON，只需幾個簡單步驟。
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: zh-hant
og_description: 使用 Python OCR 從圖像提取文字。本教程將指導您如何載入圖像進行 OCR、在 Python 中執行 OCR，以及將收據轉換為
  JSON。
og_title: 使用 Python 從圖像提取文字 – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: 在 Python 中從圖像提取文字 – 完整 OCR 指南
url: /zh-hant/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Python） – 完整 OCR 指南

是否曾需要**從圖像中提取文字**卻不知從何入手？在本教學中，我們將一步步說明如何**載入圖像以進行 OCR**、**在 Python 中執行 OCR**，以及**將收據轉換為 JSON**——只需幾行程式碼即可完成。

如果你曾開發過收據掃描應用、費用追蹤器，或只是想自動化資料輸入，你會發現掌握此流程能徹底改變工作方式。完成後，你將擁有一個可讀取收據圖片並輸出乾淨 JSON 負載的腳本，方便後續服務使用。

## 你將學會

我們會涵蓋從安裝 `aocr` 套件到處理原始結果的每一步。具體來說，你將學會：

1. **建立 OCR 引擎實例** – 所有辨識工作的入口點。  
2. **載入圖像以進行 OCR** – 告訴引擎要讀取哪個檔案。  
3. **選擇匯出格式** – JSON 或 XML，我們選擇 JSON，因為更易於消費。  
4. **執行辨識** – 真正於 Python 中執行 OCR。  
5. **列印或儲存結果** – 將收據轉換為 JSON 並查看輸出。

不需要任何 OCR 先前經驗；只要有基本的 Python 環境與一張圖像檔（收據、傳單、任何你需要的）即可。

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="extract text from image using Python OCR"}

## 從圖像中提取文字 – 步驟式 Python OCR

以下是完整、可直接執行的腳本。請將它複製貼上至名為 `receipt_ocr.py` 的檔案，然後執行 `python receipt_ocr.py`。

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### 為什麼這樣可行

- **Engine instance** – `aocr.OcrEngine()` 封裝了所有繁重的工作（模型載入、前處理等）。  
- **Loading the image** – `engine.load_image()` 告訴函式庫要分析哪個位圖；你可以提供 JPEG、PNG，甚至多頁 PDF。  
- **Export format** – 將 `engine.export_format` 設為 `aocr.ExportFormat.JSON` 會產生結構化字串，完美符合需要 JSON 的 API。  
- **Recognition call** – `engine.recognize()` 在幕後執行神經網路推論；它回傳的 JSON 字串包含偵測到的文字區塊、信心分數與版面資訊。  

---

## 使用 aocr 載入圖像以進行 OCR

如果你在想圖像是否需要特別的前處理，簡短的答案是**不需要**——`aocr` 會自動處理大多數常見情況（對比度調整、去斜）。不過，你仍可透過以下方式提升準確度：

- 確保圖像解析度至少為 300 dpi。  
- 裁切掉不相關的邊框。  
- 在送入前轉為灰階（可選，`engine.load_image()` 會自動處理）。

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*小技巧：* 若收據噪點較多，上述額外步驟可顯著提升**在 Python 中執行 OCR**的準確度。

---

## 選擇匯出格式並將收據轉換為 JSON

你可能會問，「為什麼不直接取得純文字？」因為 JSON 能保留層級結構（行、詞、邊界框），之後映射如*總金額*或*日期*等欄位會更容易。

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

執行腳本時，`json_result` 會呈現類似以下（為簡潔起見已裁剪）：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

現在你已擁有一個**將收據轉換為 JSON**的負載，可直接寫入資料庫、REST 端點，或供機器學習模型使用。

---

## 執行辨識並取得結果

最後一步——實際執行 OCR——只要呼叫 `recognize()` 即可。函式庫在幕後會：

1. 將圖像送入預訓練的卷積神經網路。  
2. 將網路輸出解碼為可讀的字元。  
3. 依選定格式（本例為 JSON）封裝所有資訊。

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

若想將輸出寫入檔案而非列印，只需這樣做：

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*特殊情況：* 部分收據可能包含非 ASCII 字元（例如「€」），務必如上例使用 UTF‑8 編碼開啟檔案，以免出現亂碼。

---

## 完整範例（一步到位的腳本）

將所有步驟整合後，以下是可直接執行的最終腳本：

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

執行方式：

```bash
python receipt_ocr.py
```

執行後，你會看到確認訊息，且在同一資料夾內產生 `receipt_output.json`，內含結構化資料。

---

## 結論

你現在已掌握**如何使用 Python 從圖像中提取文字**、**如何載入圖像以進行 OCR**、**如何在 Python 中執行 OCR**，以及**如何將收據轉換為 JSON**供下游使用。這套端對端流程輕量、只需 `aocr` 套件，且可輕鬆嵌入任何自動化管線。

接下來可以嘗試將匯出格式改為 XML、實驗不同的圖像前處理技巧，或打造一個小型 Flask API，接受上傳的收據並即時回傳 JSON 負載。只要掌握基礎，未來的可能性無限。

有任何問題或卡關嗎？在下方留言，我們一起解決，祝開發愉快！

## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，提供完整的程式碼範例與步驟說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟說明指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 優化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 從圖像提取表格](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}