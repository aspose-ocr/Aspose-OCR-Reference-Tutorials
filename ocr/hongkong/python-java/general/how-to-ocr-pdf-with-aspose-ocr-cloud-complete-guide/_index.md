---
category: general
date: 2026-06-06
description: 如何使用 Aspose OCR Cloud 進行 PDF OCR。學習從 PDF 提取文字、將 PDF 頁面轉換為 PNG，並在 Python
  中儲存 PDF 頁面圖像。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: zh-hant
og_description: 如何使用 Aspose OCR Cloud 進行 PDF OCR。本指南說明如何提取純文字 PDF、將 PDF 頁面轉換為 PNG，以及保存
  PDF 頁面圖像。
og_title: 如何使用 Aspose OCR Cloud 進行 PDF OCR – 步驟說明
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: 如何使用 Aspose OCR Cloud 進行 PDF OCR – 完整指南
url: /zh-hant/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR Cloud 進行 PDF OCR – 完整指南

有沒有想過在不與笨重的桌面工具搏鬥的情況下 **如何 OCR PDF** 檔案？你並不孤單——許多開發者在需要快速、程式化地從掃描文件中提取文字時，都會碰到這個問題。好消息是？使用 Aspose OCR Cloud，你可以 **從 PDF 提取文字**，將每一頁轉成 PNG，甚至 **保存 PDF 頁面圖像** 以供日後使用，全部只需一段簡潔的 Python 程式碼。

在本教學中，我們將逐步說明你需要了解的所有內容：從安裝 SDK、授權引擎、辨識多頁 PDF，到提取純文字、將頁面轉換為 PNG，以及將這些圖像持久化到磁碟。完成後，你將擁有一段可重複使用的程式碼片段，能夠嵌入任何需要 **如何 OCR PDF** 功能的專案中。

## 你需要的條件

- **Python 3.8+**（此程式碼亦可在 3.10 及更新版本上執行）  
- 一個 Aspose OCR Cloud 帳號 – 你將獲得免費試用授權檔 (`Aspose.OCR.lic`)  
- `asposeocrcloud` 套件（`pip install asposeocrcloud`）  
- 一個你想要處理的掃描多頁 PDF  

就這樣。無需額外的二進位檔案，無需原生相依性，僅需純 Python。

## 如何 OCR PDF – 設定與授權

在呼叫任何 OCR 方法之前，你必須先告訴 SDK 你的身份。Aspose 使用一個輕量級的授權檔案，你需要將它放在腳本可存取的位置。

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*小技巧：* 如果跳過授權步驟，SDK 仍會運作，但會在輸出圖像中嵌入小水印。這對於正式環境並不理想。

## 步驟 2：安裝 Aspose OCR Cloud Python SDK

在終端機中執行以下指令：

```bash
pip install asposeocrcloud
```

此套件會自動下載所有必要的相依套件（如 requests、pillow 等），讓你不必自行搜尋其他套件。

## 步驟 3：建立 OCR 引擎並選擇語言

引擎是此操作的核心。你可以指定任何 Aspose 支援的語言；英語在大多數情況下皆適用。

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

為什麼要設定語言？因為 OCR 引擎會使用特定語言的字典來提升辨識準確度。如果你在處理法文 PDF，只需將 `ENGLISH` 換成 `FRENCH` 即可。

## 步驟 4：指向你的多頁 PDF

將檔案的完整路徑提供給引擎，以便處理。只要相對路徑能從腳本的工作目錄解析，即可使用相對路徑。

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

確保檔案可讀取；否則會拋出 `FileNotFoundError`。

## 步驟 5：執行 OCR – 取得結果清單

呼叫 `recognize_pdf` 會回傳一個清單，清單中的每個元素對應來源 PDF 的一頁。

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

每個 `OcrResult` 包含兩個實用屬性：

* `text` – 該頁面的純文字表示（適用於 **extract plain text pdf**）
* `image` – 渲染頁面的 Pillow `Image` 物件（適用於 **convert pdf page png**）

## 步驟 6：從 PDF 提取文字並將頁面轉為 PNG

現在我們遍歷結果，印出提取的文字，並將每一頁儲存為 PNG 版本。

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### 預期的主控台輸出

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

你還會在 `YOUR_DIRECTORY` 中看到 `page_1.png`、`page_2.png` … 等檔案。這些是已光柵化的頁面圖像，可供後續的影像處理流程使用。

## 步驟 7：保存 PDF 頁面圖像（可選的後處理）

如果你只需要圖像而不需要文字，可以省略 `print(res.text)` 那一行。相反地，若想將文字存成獨立的 `.txt` 檔，只需加上一小段寫入程式碼：

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

這個小小的補充示範了在 **save PDF page images** 的同時，如何輕鬆保存提取的內容。

## 完整可執行範例

將所有步驟整合起來，以下是可直接複製貼上至 `ocr_pdf.py` 的完整腳本：

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

使用以下指令執行：

```bash
python ocr_pdf.py
```

你應該會在主控台看到每頁文字的輸出，並產生一系列 PNG 檔案

## 接下來你可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}