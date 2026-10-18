---
category: general
date: 2026-03-26
description: 如何對 PNG 檔案執行 OCR，並使用自訂字典從圖片中擷取文字，以提升 OCR 準確度。學習快速載入圖片進行 OCR。
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: zh-hant
og_description: 如何在 PNG 檔案上執行 OCR，並使用自訂詞典從圖像中提取文字，以提升 OCR 準確度。逐步指南。
og_title: 如何執行 OCR – 使用 Python 從圖片提取文字
tags:
- OCR
- Python
- Image Processing
title: 如何執行 OCR – 在 Python 中從圖像提取文字
url: /zh-hant/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中執行 OCR – 從影像中擷取文字

曾經想過 **如何在掃描的發票或螢幕截圖上執行 OCR**，並取得乾淨、可搜尋的文字嗎？你並不孤單。在許多專案中，瓶頸往往只是載入影像進行 OCR，然後讓引擎理解領域專屬的詞彙。

在本教學中，我們將一步步示範一個完整、可直接執行的範例，**從影像檔案擷取文字**、說明如何 **從 PNG 資源辨識文字**，並展示使用自訂字典與特殊字元提升 OCR 準確度的技巧。完成後，你將擁有一個可直接放入任何 Python 程式碼庫的獨立腳本。

## 你需要的環境

- Python 3.8+（程式碼使用型別提示，但在較早的 3.x 版本亦可執行）
- 目標 OCR 引擎所提供的 `ocr` 套件（使用 `pip install ocr‑engine` 安裝 – 請以實際套件名稱取代）
- 一張欲處理的影像檔（`input.png`）
- 可選：一個純文字檔（`invoice_terms.txt`），內含領域專屬詞彙，每行一個

不需要大型外部依賴，也不需要雲端 API 金鑰，只要本機 OCR 引擎即可。

---

## 步驟 1：安裝並匯入 OCR 套件

首先，確保已安裝 OCR 套件。若使用假想的 `ocr-engine` 套件，請執行：

```bash
pip install ocr-engine
```

接著匯入所需的類別：

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **小技巧：** 若你使用虛擬環境，請先啟動它再安裝，以免汙染全域的 Python 環境。

## 步驟 2：建立 OCR 引擎實例

建立引擎物件是所有 OCR 任務的入口點。把它想像成在軟體中開啟掃描器硬體。

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

為什麼這很重要：引擎會保存語言套件、辨識模式以及稍後會附加的自訂資源等設定。沒有它，你就無法 **load image for OCR** 或執行辨識流程。

## 步驟 3：載入欲辨識的影像

這一步實際上是 **load image for OCR**。`Imaging.Image.load()` 方法會讀取檔案，並轉換成引擎所需的內部位圖格式。

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

若是 JPEG 或 TIFF，同樣的方法也適用，只要把副檔名改掉即可。引擎會自動偵測格式。

> **邊緣情況：** 超過 5 MP 的大型影像可能會造成記憶體激增。如遇效能問題，建議先使用 Pillow 進行縮小後再載入。

## 步驟 4：提供自訂字典以提升準確度

大多數 OCR 引擎僅附帶通用語言模型。對於發票、收據或法律文件，常會出現遺漏詞彙。提供自訂詞表即可告訴引擎「這些詞是合法的，請視為正確」。

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

典型的條目可能是：

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

加入這些字詞後，**improve OCR accuracy** 的指標會顯著提升，尤其是非 ASCII 符號。

## 步驟 5：加入預設集合未涵蓋的特殊字元

若你的領域使用歐元符號（€）或斯堪的納維亞字母 Ø 等符號，可明確加入：

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

引擎在辨識階段會將這些字形視為有效，降低產生「垃圾」輸出的機率。

## 步驟 6：執行 OCR 流程並取得文字

最後，呼叫辨識器並取得純文字結果。`recognize()` 會回傳一個豐富的物件，我們只需要其中的原始字串即可滿足大多數使用情境。

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**預期輸出**（為簡潔起見已截斷）：

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

若輸出看起來雜亂，請再次確認自訂字典與特殊字元是否正確載入。

---

## 視覺概覽

![how to run OCR diagram](ocr-workflow.png){alt="如何執行 OCR 流程圖"}

上圖說明了從載入影像到取得乾淨文字的整體流程，並標示出可插入自訂字典與字元集的環節。

---

## 常見問題與注意事項

### 這能處理多頁 PDF 嗎？

可以——只要先將每一頁轉成 PNG（使用 `pdf2image` 或類似工具），再依序餵給同一個 `ocr_engine` 實例。引擎會獨立處理每張影像，最終得到可串接的字串列表。

### 若影像是旋轉的怎麼辦？

大多數現代 OCR 引擎會自動偵測方向，但你也可以強制旋轉：

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### 如何支援非英語語系？

在載入影像前切換語言模型：

```python
ocr_engine.set_language("de")  # German
```

請確保已安裝相對應的語言套件。

---

## 完整腳本 – 直接複製貼上

以下是完整程式碼，請在替換佔位路徑後即可執行。

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

執行方式：

```bash
python run_ocr.py
```

執行後，你應該會在終端看到擷取出的文字。之後可以將其寫入檔案、寫入資料庫，或傳遞給下游的 NLP 流程。

---

## 重點回顧與後續步驟

我們已說明 **how to run OCR** 在 PNG 上的操作、**extract text from image** 的方法，並示範如何在 **recognize text from PNG** 時透過字典與自訂字元 **improve OCR accuracy**。  

接下來可考慮：

- **批次處理：** 迴圈遍歷整個影像目錄。
- **後處理：** 使用正規表達式抽取發票號碼或日期。
- **整合：** 將腳本掛接至 Flask API，提供即時 OCR 服務。

若想深入更進階的主題，可參考 **load image for OCR** 搭配 OpenCV 前處理的教學，或探索基於深度學習的 OCR 模型（如 Tesseract 4+ 搭配 LSTM 層）。

---

### 持續實驗吧！

嘗試把 `invoice_terms.txt` 換成醫療術語清單、加入希臘字母，或使用低解析度照片測試，引擎的準確度會有什麼變化。實驗越多，你就越能了解前處理、自訂詞彙與引擎設定之間的取捨。

祝編程愉快，願你的 OCR 結果始終清晰可辨！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}