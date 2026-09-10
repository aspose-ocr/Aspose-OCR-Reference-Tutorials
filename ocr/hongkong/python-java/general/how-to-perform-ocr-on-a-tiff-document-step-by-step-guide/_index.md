---
category: general
date: 2026-01-12
description: 如何快速且準確地執行 OCR。學習在文件上執行 OCR、從 TIFF 提取文字、載入影像進行 OCR，以及在 Python 中設定 OCR
  語言。
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: zh-hant
og_description: 如何在 Python 中執行 OCR。本教學會示範如何對文件執行 OCR、從 TIFF 擷取文字、載入影像進行 OCR 以及設定 OCR
  語言。
og_title: 如何對 TIFF 文件執行 OCR – 完整指南
tags:
- OCR
- Python
- Image Processing
title: 如何對 TIFF 文件執行 OCR – 步驟指南
url: /zh-hant/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 TIFF 文件上執行 OCR – 完整指南

有沒有想過 **如何在掃描的 TIFF 檔案上執行 OCR**，卻不想花上數小時去尋找合適的函式庫？你並不孤單。許多開發者在需要從 tiff 圖片中擷取文字時會卡住，特別是當效能與語言設定很重要時。

在本教學中，我們將逐步說明你需要了解的所有內容：從安裝 OCR 套件、載入 OCR 圖片、設定 OCR 語言，到最後 **run OCR on document** 並取得乾淨的文字。完成後，你將擁有一個可直接執行的腳本，隨時可放入任何專案。

> **Pro tip:** 雖然範例使用的是通用的 `ocr` 模組，但相同概念同樣適用於 Tesseract、EasyOCR，或任何提供 Python API 的現代 OCR 引擎。

---

## 需要的條件

- Python 3.8+（任何較新的版本皆可）
- 提供 `OcrEngine` 類別的 OCR 函式庫（範例使用虛構的 `ocr` 套件；請換成你實際使用的套件）
- 你想處理的多頁 TIFF 檔案（此處稱為 `big_document.tif`）
- 若要設定執行緒數量，需具備至少 4 核心的機器

不需要外部服務，也不需要雲端金鑰——只要本機程式即可在數秒內完成。

![執行 OCR 範例](/images/ocr-example.png "在 TIFF 文件上執行 OCR")

*圖片說明：在 TIFF 文件上執行 OCR – 擷取文字的預覽。*

## 步驟 1：安裝並匯入 OCR 函式庫

首先，先把函式庫安裝到你的機器上。大多數 OCR 套件都在 PyPI 上，可直接使用 `pip install` 完成安裝。

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

接著匯入你需要的類別。若使用 Tesseract，匯入語句會有所不同，但其餘程式碼保持不變。

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*為什麼這很重要：* 事先匯入正確的符號可避免之後的命名空間衝突，並讓腳本更易閱讀。

## 步驟 2：建立並設定 OCR 引擎（設定 OCR 語言）

設定引擎的地方就是 **set OCR language**，以取得精確的辨識。預設為英文，但只要一行程式碼即可切換至法文、德文，甚至多語言模式。

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **為什麼要使用 4 個執行緒？** 大多數現代筆記型電腦至少有四核心，限制執行緒數量可防止 OCR 程序佔用整台機器——在共用伺服器上執行腳本時特別有用。

如果需要其他語言，只要將 `ocr.Language.ENGLISH` 替換為 `ocr.Language.FRENCH`、`ocr.Language.SPANISH` 等即可。

## 步驟 3：載入 OCR 圖片（Load Image for OCR）

現在我們 **load image for OCR**。`Image.load` 方法會將 TIFF 檔案讀入記憶體，並自動處理多頁文件。

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*邊緣情況：* 若檔案過大，可能會耗盡記憶體。此時可考慮使用 `Image.load_page(page_number)` 逐頁載入（前提是函式庫支援）。

## 步驟 4：對文件執行 OCR

引擎已就緒且圖片已載入，現在可以 **run OCR on document**。`process` 方法負責繁重的運算，並回傳結果物件。

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

在背後，引擎會將圖片切分為文字區塊，執行辨識模型，並將結果拼接。此呼叫為阻塞式，表示腳本會等到整個 TIFF 處理完畢——非常適合批次作業。

## 步驟 5：從 TIFF 擷取文字並驗證輸出

最後，我們透過存取結果的 `text` 屬性 **extract text from tiff**。先印出前 200 個字元作為快速檢查。

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**預期輸出（範例）：**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

若需要完整文字，只要使用 `ocr_result.text`。若要進一步處理，可能會想將其寫入 `.txt` 檔案：

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

## 完整範例

將上述步驟整合起來，以下是一個可直接執行的腳本。請將佔位套件名稱換成你實際安裝的套件。

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

使用以下指令執行腳本：

```bash
python ocr_tiff_example.py
```

你應該會在終端機看到預覽，且會產生名為 `extracted_text.txt` 的檔案，內含完整的文字稿。

## 常見問題與邊緣情況

- **如果 TIFF 包含多頁怎麼辦？**  
  大多數 OCR 引擎會在內部將每頁視為獨立影像。`ocr_result.text` 會在頁面之間插入換行符號。若需逐頁處理，可使用 `Image.load_page(page_number)` 迭代。

- **我可以處理 PNG 或 JPEG 而非 TIFF 嗎？**  
  當然可以。`Image.load` 方法通常接受 Pillow 或底層函式庫支援的任何格式，只要更改檔案副檔名即可。

- **文字亂碼—需要更換語言嗎？**  
  需要。`set OCR language` 步驟對非英文文件至關重要。請確認已安裝相應的語言套件（例如法文的 `tesseract‑lang‑fra`）。

- **記憶體不足？**  
  降低 `set_memory_limit` 或逐頁處理。有些引擎還允許在辨識前將影像縮小。

## 結論

以上就是使用 Python 在 TIFF 檔案上 **how to perform OCR** 的簡明完整指南。我們涵蓋了從安裝函式庫、設定引擎（包括 **set OCR language**）、**load image for OCR**、**run OCR on document**，最後 **extract text from tiff** 的全部步驟。

歡迎自行實驗：調整執行緒數量、切換語言，或將 OCR 輸出導入自然語言處理管線。掌握基礎後，想做什麼都沒有限制。

還有其他問題嗎？在下方留言，我們祝你編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}