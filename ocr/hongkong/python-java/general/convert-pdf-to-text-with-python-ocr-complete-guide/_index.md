---
category: general
date: 2026-07-05
description: 使用 Python OCR 將 PDF 轉換為文字。了解如何從 PDF 提取文字、執行批次 OCR 處理，以及在幾個簡單步驟中載入 PDF
  進行 OCR。
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: zh-hant
og_description: 快速將 PDF 轉換為文字。本教學示範如何從 PDF 提取文字、執行批次 OCR 處理，以及使用 Python 識別掃描的 PDF
  檔案。
og_title: 使用 Python OCR 將 PDF 轉換為文字 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: 使用 Python OCR 將 PDF 轉換為文字 – 完整指南
url: /zh-hant/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 轉換 PDF 為文字 – 完整指南

有沒有想過如何 **將 PDF 轉換為文字** 而不費吹灰之力？也許你手頭上有一堆掃描過的合約、發票或研究論文，需要純文字版本來做索引或分析。好消息是，只要幾行 Python 程式碼就能幫你完成繁重的工作。

在本教學中，我們將一步步示範一個實用的解決方案，不僅能 **將 PDF 轉換為文字**，還會教你如何 **從 PDF 中擷取文字**、設定 **批次 OCR 處理**，以及正確 **載入 PDF 以供 OCR**。完成後，你將擁有一個可直接執行的腳本，能一次性 **辨識掃描 PDF** 頁面。

## 你將學會

- 安裝與設定 Python OCR 套件（此處以通用的 `ocr` 套件為例）。  
- 載入多頁 PDF 並將其送入 OCR 引擎。  
- 迭代結果以列印或儲存擷取出的文字。  
- 處理常見的例外情況，例如大型檔案、加密 PDF 以及多語言文件。  

不需要繁雜的 GUI 工具，也不必手動複製——只要純程式碼，就能直接放入 CI 流程或桌面工具中使用。

![使用 Python OCR 轉換 PDF 為文字](https://example.com/images/convert-pdf-to-text.png "使用 Python OCR 轉換 PDF 為文字")

## 前置需求

在開始之前，請確保你已具備以下條件：

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | 現代語法、型別提示與更佳效能。 |
| `ocr` library (or a wrapper around Tesseract) | 提供範例中使用的 `OcrEngine`、`Language` 與 `Image` 類別。 |
| 多頁掃描 PDF（例如 `contract.pdf`） | 這是你要 **載入 PDF 以供 OCR** 的來源。 |
| 基本的指令列操作經驗 | 用於安裝套件與執行腳本。 |

如果你是使用 Tesseract 作為底層引擎，請先透過作業系統的套件管理員安裝（Linux 上 `apt-get install tesseract-ocr`、macOS 上 `brew install tesseract`），再加入 Python 包裝器：

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## 步驟 1：建立 OCR 引擎並設定辨識語言

首先，我們需要建立一個 OCR 引擎實例。將語言設為英文是常見的預設值，之後也可以切換成其他支援的語言。

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**為什麼這很重要：** 引擎是解讀像素資料的大腦。透過明確指定 `engine.language`，可以避免在每一頁都進行語言偵測，從而大幅提升 **批次 OCR 處理** 的速度。

## 步驟 2：載入 PDF 文件以供 OCR

接下來，我們把 PDF 載入記憶體。`ocr.Image.load` 方法接受檔案路徑，並回傳引擎可理解的物件。

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**小技巧：** 若 PDF 受密碼保護，大多數函式庫都允許傳入 `password` 參數。提前處理可避免之後出現「無法開啟檔案」的神祕錯誤。

## 步驟 3：一次辨識所有頁面 – 單次呼叫即 **辨識掃描 PDF**

逐頁執行 OCR 速度較慢，尤其是大型文件。`recognize_multi_page` 方法會在內部執行 **批次 OCR 處理**，並在可能的情況下使用多執行緒。

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**底層發生了什麼？** 引擎會把每一頁串流至底層的 OCR 引擎（如 Tesseract），收集文字後包裝成 `OcrResult`。這種方式減少 I/O 開銷，讓你之後能輕鬆 **從 PDF 中擷取文字**。

## 步驟 4：遍歷結果並輸出辨識出的文字

最後，我們遍歷每個 `OcrResult` 並列印文字。你也可以把每頁寫入獨立的 `.txt` 檔，或是合併成一個完整文件。

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**為什麼使用 enumerate？** `enumerate(..., start=1)` 會產生易讀的頁碼，當你需要對照原始 PDF 的特定章節時非常方便。

### 預期輸出

對一份 3 頁的合約執行腳本，可能會得到：

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

若某頁沒有可辨識的文字，對應的 `result.text` 會是空字串——這對於偵測空白或僅含影像的頁面相當有用。

## 處理大型 PDF 與記憶體限制

一次載入 500 頁的 PDF 可能會耗盡記憶體。以下提供兩種策略：

1. **分段載入** – 部分函式庫允許一次載入特定頁碼範圍：

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **串流寫入磁碟** – 直接把每頁文字寫入檔案，而不是保留整個列表於記憶體。

這兩種技巧都能讓你的 **將 PDF 轉換為文字** 工作流程保持可擴展。

## 錯誤處理與例外情況

- **加密 PDF** – 在 `Image.load` 時傳入密碼：

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **多語言文件** – 若偵測到不同語系，可在每頁切換語言：

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **低解析度掃描** – 使用 `Pillow` 等套件先做影像前處理（提升對比度），再送入 OCR。這能顯著改善 **辨識掃描 PDF** 的品質。

## 完整腳本：一次執行將 PDF 轉換為文字

以下是完整、可直接執行的腳本，將所有步驟串接起來。將其存為 `pdf_to_text.py`，然後執行 `python pdf_to_text.py`。

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**執行腳本** 後會在 `output` 資料夾產生 `page_1.txt`、`page_2.txt` 等檔案，實際上就是 **從 PDF 中擷取文字** 的結構化結果。

## 測試解決方案

1. **基本檢查** – 開啟產生的 `.txt` 檔，確認前幾行與原始文件的標題相符。  
2. **效能測試** – 使用 `time` 指令測試 100 頁 PDF 的執行時間。若耗時過長，可考慮開啟函式庫的多執行緒選項（通常是 `engine.set_threads(4)`）。  
3. **品質保證** – 用 diff 工具將 OCR 輸出與手動輸入的摘錄比對，目標是掃描品質良好時達到 >95 % 的字元正確率。

## 往後的步驟與相關主題

- **提升準確度**：嘗試設定 `engine.dpi = 300`，或在 OCR 前做影像前處理（去斜、去噪）。  
- **可搜尋 PDF**：使用 `PyPDF2` 或 `pdfplumber` 等套件，將擷取的文字嵌回原始 PDF，讓檔案變成可搜尋。  
- **自然語言處理**：將擷取的文字餵給 spaCy 或 NLTK，進行實體抽取、情感分析或關鍵字標記。  
- **自動化流水線**：結合 `watchdog` 監控資料夾，當有新檔案出現時自動 **將 PDF 轉換為文字**。

掌握這些模式後，你將能夠

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，提供完整的程式碼範例與逐步說明，幫助你深入了解其他 API 功能，並在自己的專案中探索不同的實作方式。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}