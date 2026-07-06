---
category: general
date: 2026-03-26
description: 如何使用 OCR 提取 PDF 文字。學習將 PDF 載入為圖像、識別 PDF 文字，並使用簡單的 Python 範例從 PDF 中提取文字。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: zh-hant
og_description: 如何使用 OCR 提取 PDF 文字。此指南將示範如何將 PDF 載入為圖像、辨識 PDF 文字，並在 Python 中提取 PDF
  文字。
og_title: 如何使用 OCR 提取 PDF 文字 – 完整教學
tags:
- OCR
- Python
- PDF processing
title: 如何使用 OCR 提取 PDF 文字 – 完整逐步指南
url: /zh-hant/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR 提取 PDF 文字 – 完整逐步指南

有沒有想過 **如何提取 PDF**（實際上只是掃描圖像的）檔案？你並不孤單——許多開發者在需要可搜尋內容卻只有僅圖像的 PDF 時都會碰到這個問題。好消息是？只要幾行程式碼加上一個可靠的 OCR 函式庫，就能把這些圖片 PDF 迅速轉換成純文字。  

在本教學中，我們將逐步說明 **如何使用 OCR** 來將 PDF 載入為圖像、辨識 PDF 文字，最後 **從 PDF 中提取文字**，不論文件長度為何。完成後，你將擁有可執行的腳本、每一步的清晰說明，以及避免常見陷阱的幾個小技巧。

## 需要的環境

- Python 3.9 或更新版本（程式碼同樣支援 3.10+）  
- `ocr` Python 套件（或任何提供 `OcrEngine`、`OcrEngineMode` 與 `Imaging.Image` 的相容 OCR 函式庫）  
- 想要處理的多頁 PDF（示範檔名為 `multi_page.pdf`）  
- 基本的虛擬環境使用經驗（非必須，但建議）  

> **專業提示：** 若你使用 Windows，建議使用 Anaconda Prompt；在 macOS/Linux 上，只要執行 `python -m venv venv && source venv/bin/activate` 即可完成環境設定。

## Step 1: Install the OCR Library

首先，從 PyPI 取得 OCR 套件。下方範例使用一個虛構的 `ocr` 套件，其 API 與程式碼片段中顯示的相同，但大多數實務上常用的函式庫（例如 `pytesseract` + `pdf2image`）也遵循相同的模式。

```bash
pip install ocr
```

如果你使用其他引擎，請將 `ocr` 替換成相應的名稱（例如 `pip install pytesseract pdf2image`）。

## Step 2: Initialize the OCR Engine

建立引擎實例是 **如何提取 PDF** 文字的基礎。可以把引擎想像成會解讀每一頁 PDF 像素的“大腦”。

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **為什麼重要：** `set_engine_mode` 讓你在速度與精確度之間取得平衡。`DEFAULT` 為均衡選擇；若需要更高精度，可切換至 `HIGH_ACCURACY`（前提是函式庫支援）。

## Step 3: Load the PDF as an Image Object

OCR 只能處理圖像，無法直接讀取 PDF 容器，因此必須先將 PDF 轉換為圖像表示。`Imaging.Image.load` 方法會自動處理多頁 PDF。

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **邊緣情況：** 部分函式庫只接受單頁圖像。若遇到此情況，需使用 `pdf2image.convert_from_path` 逐頁迭代。我們的 `load` 呼叫已將此抽象化，使 **load pdf as image** 成為一行程式碼即可完成。

## Step 4: Recognize Text on All Pages

接下來就是 **辨識 PDF 文字** 的核心。引擎會掃描每一頁，回傳一個結果物件列表——每頁一個。

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

每個 `page_result` 都提供 `get_text()`（純文字）與 `get_confidence()`（可選的品質指標）等方法。  

> **小技巧：** 若只需要第一頁的文字，可呼叫 `recognize(pdf_image[0])`，而非使用多頁輔助函式。

## Step 5: Iterate Through Results and Output the Extracted Text

最後，我們遍歷所有結果，將每頁的文字印出。這樣就完成了 **從 PDF 中提取文字** 的工作流程。

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### 預期輸出

如果 `multi_page.pdf` 包含三頁，分別寫有 “Hello”、 “World” 與 “Python”，則會看到：

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

就這樣——你的 PDF 現在已完全可搜尋，文字也可供後續處理（索引、情感分析，隨你需求）。

## Step 6: Handling Common Pitfalls

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **輸出為空白** | PDF 頁面掃描 DPI 較低，導致字元無法辨識。 | 在 OCR 前放大圖像：`pdf_image = pdf_image.resize(300)`（300 DPI 為較佳取值）。 |
| **出現雜訊字元** | 非拉丁字母需要額外語言套件。 | 載入相應語言模型：`ocr_engine.load_language('spa')` 以支援西班牙文等。 |
| **大型 PDF 記憶體暴增** | 一次載入所有頁面會佔用大量 RAM。 | 分批處理頁面：`for img in pdf_image.split(batch=10): …`（偽代碼）。 |
| **效能緩慢** | 在龐大文件上使用 `DEFAULT` 模式可能較慢。 | 改用 `FAST` 模式，或使用 `concurrent.futures` 進行平行 OCR。 |

## Bonus: Saving Extracted Text to a File

大多數實務流程都需要將文字保存下來。以下是一個簡易輔助程式，會把所有內容寫入 `output.txt`。

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

現在，你可以將 `output.txt` 匯入搜尋引擎、資料庫，或任何 NLP 模型中使用。

## Putting It All Together – Full Script

以下是完整、可直接執行的程式。複製貼上、調整檔案路徑，即可開始使用。

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

執行方式：

```bash
python extract_pdf_ocr.py
```

執行後，你應該會在主控台看到每頁的內容，並收到 `extracted_text.txt` 已建立的確認訊息。

## Conclusion

我們已說明 **如何提取 PDF** 文字，從安裝函式庫、載入 PDF 為圖像、辨識 PDF 文字，到最後儲存輸出。現在你已掌握 **如何使用 OCR**、**如何載入 PDF 為圖像**，以及 **如何可靠地辨識 PDF 文字**。  

接下來的步驟是什麼？可以嘗試將預設的引擎模式切換為高精度設定、為多語言 PDF 測試不同語言套件，或將提取的文字導入 Elasticsearch 等全文檢索系統。只要掌握了 PDF 文字提取的基礎，未來的可能性無限。

---

![how to extract pdf example](images/ocr_flowchart.png){alt="如何提取 PDF 工作流程圖"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}