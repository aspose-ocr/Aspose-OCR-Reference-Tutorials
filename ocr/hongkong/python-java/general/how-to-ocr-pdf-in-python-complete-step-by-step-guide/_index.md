---
category: general
date: 2026-06-06
description: 如何使用 Python 進行 PDF OCR，從 PDF 中提取文字，轉換掃描 PDF 的文字，並僅用幾行程式碼更改 OCR 語言。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: zh-hant
og_description: 如何使用 Python 進行 PDF OCR：實用指南，教您如何從 PDF 提取文字、轉換掃描 PDF 文字，並輕鬆變更 OCR 語言。
og_title: 如何在 Python 中對 PDF 進行 OCR – 完整程式設計教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: 如何在 Python 中對 PDF 進行 OCR – 完整逐步指南
url: /zh-hant/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR PDF – 完整步驟指南

有沒有想過在不付高價 SaaS 工具的情況下 **如何 OCR PDF** 檔案？你並不是唯一有此需求的人。無論是將舊書數位化、從發票中提取資料，或只是需要從掃描報告中取得可搜尋的文字，掌握 Python 的 PDF OCR 能為你節省大量手動複製的時間。

在本教學中，我們將示範一個簡潔且可運作的範例，該範例 **從 PDF 中提取文字**，示範如何 **將掃描的 PDF 文字** 轉換為可編輯的字串，甚至演示如何 **變更 OCR 語言**（若文件不是英文）。完成後，你將擁有一段可重複使用的程式碼片段，隨時可嵌入任何專案。

## 前置條件與設定

- 已安裝 Python 3.8+（程式碼在 3.9、3.10 及更新版本皆可執行）
- 提供 `OcrEngine` 類別的 `ocr` 套件（可透過 `pip install ocr-lib` 安裝——請替換為實際使用的套件名稱）
- 想要處理的 PDF 檔案；示範中使用放在 `YOUR_DIRECTORY` 資料夾下的 `high_res_book.pdf`

如果你使用虛擬環境（強烈建議），請先啟動它：

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **小技巧：** 請將 PDF 檔案放在專屬的 `data/` 目錄下，以免日後遭遇路徑相關的麻煩。

## 步驟 1：建立 OCR 引擎實例（How to OCR PDF – 初始化）

當你想要 **對 PDF 執行 OCR** 時，第一件事就是實例化引擎。可以把引擎想像成大腦，負責閱讀每一頁、解讀字形，並回傳純文字。

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

為什麼這很重要：若沒有引擎，就無法設定語言、渲染選項或 PDF 處理的相關資訊。`OcrEngine` 物件保存了所有預設值，並允許你之後進行調整。

## 步驟 2：設定辨識語言（變更 OCR 語言）

大多數 OCR 函式庫預設為英文，但若文件是法文、德文，甚至日文該怎麼辦？只要呼叫 `set_recognition_language` 即可變更語言。這就滿足了 **變更 OCR 語言** 的需求，並提升辨識準確度。

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **為什麼可能需要這樣做：** 多語言檔案庫常包含混合語言的頁面。即時切換語言可避免將 “ß” 或 “ñ” 等字元誤辨。

## 步驟 3：設定 PDF 渲染選項（有效轉換掃描 PDF 文字）

處理掃描 PDF 時，解析度與色彩模式會大幅影響 OCR 品質。以 300 DPI 的灰階方式渲染，對大多數文件而言是最佳平衡——足以捕捉細節，同時不會佔用過多記憶體。

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

鏈式呼叫看起來很炫，但其實只是回傳同一個選項物件的流暢 API。若需要彩色（例如彩色圖表），只要將 `"grayscale"` 改成 `"color"` 即可。

## 步驟 4：辨識 PDF 並取得第一頁文字（從 PDF 提取文字）

現在進入 **如何 OCR PDF** 的核心：將檔案路徑傳給引擎，取得辨識後的文字。此方法會回傳每頁結果的列表；每個結果都有 `text` 屬性。

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

若需要整本文件，可遍歷 `results`：

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### 若 PDF 被加密怎麼辦？

有些 PDF 受密碼保護。此時可將密碼傳給 `recognize_pdf`：

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

引擎會在執行 OCR 前即時解密——不需要額外步驟。

## 步驟 5：後處理提取的文字（微調從 PDF 提取的文字）

原始 OCR 輸出常帶有換行、額外空格或偶發的錯誤字元。快速清理例程可讓提取的字串可直接用於後續處理（搜尋索引、資料庫儲存等）。

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

現在你可以安全地 **從 PDF 提取文字**，並將其輸入任何 NLP 流程、搜尋引擎，或簡單的 `open(...).write()` 操作。

## 加分項：批次處理多個 PDF（擴展 PDF OCR）

如果你有一個資料夾裡放滿掃描 PDF，只需將邏輯包在迴圈中：

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

此程式碼片段示範如何批量 **對 PDF 執行 OCR**，這是數位化專案的常見需求。

## 預期輸出

執行單頁範例（步驟 4）時，應會印出類似以下內容：

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

若處理的是多頁書籍，控制台會顯示每頁清理過的文字，且批次腳本會在每個 PDF 旁產生相應的 `.txt` 檔案。

## 常見陷阱與避免方法

| 問題 | 徵兆 | 解決方式 |
|-------|----------|-----|
| 來源 PDF 解析度過低 | 字元亂碼、遺失文字 | 提升 DPI（`set_dpi(400)` 或更高） |
| 語言設定錯誤 | 大量未知符號，尤其是帶重音的字元 | 使用 `engine.set_recognition_language(ocr.Language.FRENCH)` 或相應的列舉值 |
| 大型 PDF 造成記憶體錯誤 | `MemoryError` 或在數頁後當機 | 分批處理頁面（`engine.recognize_pdf(..., max_pages=10)`） |
| PDF 缺少字型 | 某些頁面輸出為空白 | 確認 PDF 確實包含點陣圖像；有些 PDF 為純向量，需要其他處理方式 |

## 圖像說明

以下是一張工作流程的快速示意圖。alt 文字特意設計為 SEO 友好。

![如何 OCR PDF 工作流程圖，顯示引擎初始化、語言設定、渲染選項、辨識與文字提取](/images/ocr-workflow.png)

*此圖示對程式執行並非必要，但有助於視覺學習者了解每個步驟的定位。*

## 結論

我們已完整說明如何在 Python 中 **OCR PDF**：建立 OCR 引擎、**變更 OCR 語言**、設定渲染以 **轉換掃描 PDF 文字**，最後 **從 PDF 提取文字** 供後續使用。完整且可執行的範例已可直接嵌入任何專案，且可選的批次腳本示範了如何擴展此解決方案。

接下來，你可能想探索：

- 為多語言檔案庫加入 **對 PDF 執行 OCR**，透過迴圈遍歷語言清單。
- 將提取的文字整合至 Elasticsearch 以進行全文搜尋。
- 使用 OCR 產生可搜尋的 PDF，將文字層嵌入原始檔案（許多函式庫提供 `save_as_searchable_pdf` 方法）。

歡迎自行實驗、調整 DPI 設定，或切換至其他 OCR 後端。基本原理不變，現在你已具備堅實的基礎可供延伸。

祝程式開發順利，願你的掃描文件終於變得可搜尋！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [辨識 PDF 文字 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [如何使用 Aspose.OCR 以語言辨識圖像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [如何在 .NET 使用 Aspose.OCR OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}