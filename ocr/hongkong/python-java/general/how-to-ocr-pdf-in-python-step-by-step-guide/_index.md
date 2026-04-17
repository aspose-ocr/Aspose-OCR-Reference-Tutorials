---
category: general
date: 2026-03-28
description: 快速學習如何使用 Python 進行 PDF OCR。本指南將向您展示如何從 PDF 中提取文字、辨識 PDF 文字，以及使用 Aspose
  OCR 將掃描的 PDF 轉換為文字。
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: zh-hant
og_description: 掌握如何使用 Python 進行 PDF OCR。從 PDF 提取文字、辨識 PDF 文字，並在數分鐘內將掃描版 PDF 轉換為文字。
og_title: 如何在 Python 中對 PDF 進行 OCR – 完整指南
tags:
- PDF
- OCR
- Python
- Aspose
title: 如何在 Python 中對 PDF 進行 OCR – 逐步指南
url: /zh-hant/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR PDF – 步驟指南

有沒有想過 **如何 OCR PDF**，當檔案只是一頁的圖片時？你並不是唯一有此疑問的人。在本教學中，我們將一步步說明如何 OCR PDF 檔案、從 PDF 中擷取文字，並將掃描版 PDF 轉換為可搜尋的文字——全部使用純 Python 程式碼。

我們會從安裝 Aspose OCR 函式庫說起，直到把每一頁辨識出的文字取出。完成後，你將能夠 **OCR PDF with Python**、**extract text from PDF**，以及 **convert scanned PDF to text**，不必在零散的文件中四處搜尋。沒有多餘的說明，只有可直接執行、可直接 copy‑paste 的實作範例。

## 您需要的條件

在開始之前，請確保你已擁有：

* Python 3.8+（建議使用最新的穩定版）  
* Aspose OCR for Python 授權或免費試用金鑰 – 可從 Aspose 官方網站取得。  
* 一個想要處理的掃描版 PDF（我們稱之為 `input.pdf`）。  

如果你已經備妥上述條件，太好了——讓我們馬上開始。若尚未安裝套件，也非常簡單，我們會一步步示範。

## 如何 OCR PDF – 環境設定

首先必須把 Aspose OCR 模組安裝到你的機器上。套件名稱為 `aspose-ocr`，可透過 pip 安裝：

```bash
pip install aspose-ocr
```

> **Pro tip:** 使用虛擬環境 (`python -m venv venv`) 以保持相依套件的整潔。

套件安裝完成後，即可匯入並啟動 OCR 引擎。這是之後所有 **ocr pdf with python** 工作流程的基礎。

## OCR PDF with Python – 匯入 Aspose OCR

現在函式庫已可使用，讓我們把它帶入腳本中。同時將引擎設定為 *direct PDF mode*，讓 Aspose 直接從檔案讀取 PDF 位元組，而不是先把每頁轉成影像再處理。

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

為什麼要使用 `PdfMode.DIRECT`？因為它會省去額外的光柵化步驟，使處理速度更快，且能保留原始版面的排版——在需要 **recognize text from PDF** 時特別有用。

## Recognize Text from PDF – 執行引擎

引擎就緒後，指向你的掃描檔。`recognize_from_pdf` 方法會完成所有繁重工作：解析每一頁、執行 OCR 演算法，並回傳一個 `OcrResult` 物件，裡面包含多個 `Page` 物件。

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

如果你在想這會不會支援加密的 PDF——答案是可以，只要在呼叫 `recognize_from_pdf` 前先設定 `ocr_engine.password = "secret"` 即可。許多教學會忽略這個邊緣案例，但在實務流程中相當實用。

## Extract Text from PDF – 取得頁面結果

`ocr_result.pages` 陣列每個元素對應一頁。每個 `Page` 物件都有 `.text` 屬性，內含該頁的純文字表示。讓我們遍歷並印出結果，讓你清楚看到被擷取的內容。

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

執行腳本後會得到類似以下的輸出：

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

此輸出證明你已成功 **extract text from PDF** 並 **recognize text from PDF**，且是使用 Aspose OCR。接下來可以把這些字串寫入資料庫、搜尋索引，或任何後續的 NLP 流程。

![如何 OCR PDF 範例](placeholder-image.png "如何 OCR PDF 範例")

*圖片替代文字:* **如何 OCR PDF 範例** – 顯示每頁已識別文字的控制台輸出。

## Convert Scanned PDF to Text – 儲存輸出

大多數開發者不只想在 console 看到文字，還需要將結果寫入永久檔案。以下是一個小幫手，會把每頁文字寫入獨立的 `.txt` 檔，等同於在 `output` 資料夾中 **convert scanned PDF to text**。

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

腳本執行完畢後，你會得到一個整齊的目錄：

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

現在你已完整 **convert scanned PDF to text**，可以把這些檔案餵入任何後續流程——搜尋、分析，甚至簡單的 `grep`。

## 常見問題與邊緣案例

**如果我的 PDF 同時包含圖片與真實文字，該怎麼辦？**  
Aspose OCR 會嘗試辨識全部內容，但你可以透過停用已含可選文字的頁面來加速。設定 `ocr_engine.auto_detect_page_orientation = True`，然後對已知可選文字的頁面呼叫 `ocr_engine.recognize_from_pdf(..., detect_text=False)`。

**我可以控制語言模型嗎？**  
當然可以。於呼叫 `recognize_from_pdf` 前設定 `ocr_engine.language = aocr.Language.English`（或任何支援的語言）。這能提升非英語文件的辨識精度。

**如何處理非常大的 PDF（超過 100 頁）？**  
將檔案分批處理。`recognize_from_pdf` 方法接受 `page_range` 參數，例如 `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`。以此方式迭代不同區段，可降低記憶體使用量。

## 完整範例

將所有步驟整合起來，以下是一個可直接存為 `ocr_pdf.py` 並執行的單一腳本：

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

執行方式：

```bash
python ocr_pdf.py
```

執行後，你應該會在 console 看到每頁文字的確認訊息，並顯示 `.txt` 檔案的儲存位置。

## 結論

我們已說明 **how to OCR PDF** 的 Python 實作，示範了乾淨的 **ocr pdf with python** 方法，教你如何 **extract text from PDF**，解析了 **recognize text from PDF** 的運作機制，最後提供可直接使用的程式碼片段，完成 **convert scanned PDF to text**。整個流程已完整包裝。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}