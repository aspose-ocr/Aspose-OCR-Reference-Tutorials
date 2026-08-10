---
category: general
date: 2026-06-22
description: 學習如何在 Python 中對 PDF 檔案進行 OCR，從 PDF 中提取文字，並使用串流式方法將 PDF 轉換為文字。簡單步驟處理掃描
  PDF。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: zh-hant
og_description: 如何在 Python 中對 PDF 檔案進行 OCR？請跟隨本指南從 PDF 中提取文字、將 PDF 轉換為文字，並使用串流處理掃描版
  PDF。
og_title: 如何在 Python 中對 PDF 進行 OCR – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 如何在 Python 中對 PDF 進行 OCR – 完整指南：從 PDF 中提取文字
url: /zh-hant/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR PDF – 完整指南：從 PDF 提取文字

有沒有想過在不與笨重桌面工具糾纏的情況下 **how to OCR PDF** 檔案？你並不是唯一有此疑問的人。在許多真實世界的專案中——例如發票自動化或數位化檔案掃描——你需要一個可靠的方式，將掃描的 PDF 轉換成可搜尋、可編輯的文字。

在本教學中，我們將示範一個簡潔、端到端的範例，使用輕量級的 Python OCR 引擎 **extracts text from PDF** 頁面。完成後，你將清楚知道如何 **convert PDF to text**、如何 **load PDF from stream**，以及如何有效率地 **process scanned PDF**。沒有魔法，只有可以直接套用到專案中的純 Python 程式碼。

## 你將學到

- 安裝與設定能夠辨識 PDF 輸入的 Python OCR 套件。  
- 啟用 PDF 辨識模式並將輸出格式設定為純文字。  
- 從檔案串流載入多頁 PDF（經典的「load pdf from stream」模式）。  
- 在所有頁面上執行 OCR，取得文字內容。  
- 列印或儲存結果，以供後續處理。

**先備條件**  
- 已在機器上安裝 Python 3.8+。  
- 具備 pip 與虛擬環境的基本概念。  
- 有一個掃描的 PDF 檔（範例中名為 `multipage.pdf`），放置於已知目錄。

如果上述任一項你不熟悉，也別擔心——每一步都會以簡單語言說明，我們也會提供完整指令。

---

## 步驟 1：安裝 OCR 引擎（how to OCR PDF）

首先，你需要一個能處理 PDF 輸入的 OCR 引擎。本指南使用假想的 `ocr` 套件（其 API 與市面上常見的商業 SDK 類似，使用方式同樣適用於 Tesseract‑OCR、ABBYY 或 Google Vision，只要適當包裝即可）。

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **小技巧：** 若你在 Windows 上遇到權限錯誤，請改用 `pip install --user ocr`。

套件安裝完成後，即可在腳本中匯入並建立引擎實例——這正是 **how to OCR PDF** 的核心。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` 物件會保存所有稍後要調整的設定，例如語言、DPI，以及最關鍵的 PDF 模式。

---

## 步驟 2：啟用 PDF 辨識並選擇輸出格式（extract text from PDF）

預設情況下，多數 OCR SDK 皆假設你提供的是影像。為了讓引擎將傳入的串流視為 PDF，我們必須開啟 PDF 辨識旗標，並要求輸出純文字。

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

為什麼要明確指定輸出格式？因為有些引擎可以回傳帶有隱藏文字層的 PDF、可搜尋的 PDF，或是包含邊界框的 JSON。對於大多數資料抽取流程而言，**extract text from PDF** 為純字串是最乾淨的下游格式。

---

## 步驟 3：從檔案串流載入 PDF（load PDF from stream）

從串流載入 PDF 是一種記憶體友善的做法——你不必一次將整個檔案讀入 RAM。處理大型多頁文件時特別有用。

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **如果檔案位於 S3 或其他雲端儲存桶呢？**  
> 只要將 `from_file` 改成接受位元緩衝區的方法（例如 `ImageStream.from_bytes(s3_object.read())`），其餘流程保持不變。

---

## 步驟 4：對所有頁面執行 OCR（process scanned PDF）

現在開始真正的重活。引擎會遍歷每一頁，執行辨識，並回傳一個頁面物件清單——每個物件皆提供其文字內容。

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

在背後，OCR 函式庫會解壓每一頁 PDF，依設定的 DPI 進行光柵化，然後將位圖送入神經網路模型。最終得到的就是一組 `Page` 物件，隨時可供抽取。

---

## 步驟 5：取得並顯示辨識文字（convert PDF to text）

最後，我們遍歷回傳的頁面，印出辨識出的文字。這就是 **convert PDF to text** 真正發生的時刻。

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### 預期輸出

若 `multipage.pdf` 包含三頁掃描文件，畫面會類似以下內容：

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

可以看到頁面之間有清晰的分隔——如果你需要將每頁文字存入資料庫，或是傳給下游的 NLP 模型，這樣的格式非常方便。

---

## 處理常見邊緣情況

### 1. 同時含有影像與文字層的 PDF
某些 PDF 已經內建隱藏文字層（例如從 Word 匯出）。若想讓 OCR 引擎 **ignore existing text** 並重新處理影像，可設定：

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. 超大檔案超出記憶體限制
面對 GB 級別的 PDF 時，建議分塊處理：

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. 語言與字型支援
若掃描文件為法文或包含特殊字元，請告訴引擎使用哪種語言模型：

```python
settings.set_language("fr")   # or "en", "de", etc.
```

---

## 完整腳本 – 可直接執行

以下是完整、可直接執行的範例，將所有步驟串起來。將檔案存為 `ocr_pdf.py`，然後執行 `python ocr_pdf.py`。

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**執行腳本** 後會把每頁文字印到主控台，正如「預期輸出」區塊所示。之後你可以把輸出導向檔案：

```bash
python ocr_pdf.py > extracted_text.txt
```

---

## 結論

我們已完整說明 **how to OCR PDF** 檔案在 Python 中的全流程。只要設定好引擎、以串流方式載入文件，並逐頁遍歷，即可 **extract text from PDF**、**convert PDF to text**，以及 **process scanned PDF**，僅需幾行程式碼。此方法可從兩頁的小發票擴展到上百頁的大型檔案。

接下來可以嘗試把抽取出的字串送入搜尋索引、語言模型摘要器，或是資料驗證管線。你也可以實驗 JSON 等輸出格式，以保留位置資訊，進行進階文件分析。

對於加密 PDF 的處理或與雲端儲存的整合有任何問題，歡迎在下方留言——祝編程愉快！

![顯示 OCR PDF 工作流程圖 – how to OCR PDF、load PDF from stream、recognize pages 以及 extract text](ocr-pdf-workflow.png "how to OCR PDF 工作流程圖")


## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步延伸本章所示技巧。每篇資源皆提供完整可執行的程式碼範例，並附上逐步說明，協助你掌握更多 API 功能，或在自己的專案中探索替代實作方式。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}