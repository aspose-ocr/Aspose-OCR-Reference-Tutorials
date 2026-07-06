---
category: general
date: 2026-01-12
description: 使用 OCR 引擎的 Python 從 PDF 提取文字 – 學習如何使用 OCR 讀取 PDF、載入影像進行 OCR，並取得結構化結果。
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: zh-hant
og_description: 使用 Python OCR 引擎從 PDF 提取文字。本教學展示如何使用 OCR 讀取 PDF、載入影像進行 OCR，以及使用 Python
  OCR 引擎獲得可靠的結果。
og_title: 使用 OCR 引擎 Python 從 PDF 提取文字 – 完整指南
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 使用 Python OCR 引擎從 PDF 提取文字 – 逐步指南
url: /zh-hant/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR Engine Python 從 PDF 提取文字 – 完整教學

曾經需要 **extract text from PDF** 但檔案只是掃描圖像嗎？你並不孤單。在許多實務專案中，你收到的 PDF 沒有可選取的文字，因此唯一的解決方式就是 **read PDF with OCR**。  

在本指南中，我們將逐步示範一個實用的端對端解決方案，完整說明如何 **load image for OCR**、啟動 **OCR engine Python**，並擷取結構化文字供後續流程使用。沒有模糊的參考，只有可直接複製貼上的完整可執行範例。

## 您將學會

- 如何安裝並匯入所需的 Python OCR 套件。  
- 從 PDF 檔案 **load image for OCR** 的精確步驟。  
- 如何呼叫引擎的 `recognize_structured()` 方法，並遍歷 block、line、word。  
- 處理低信心結果與多頁 PDF 的技巧。  

完成本教學後，您將擁有一支可靠的腳本，能夠 **extract text from PDF**，不論文件只有一頁或是一百頁。

---

![顯示 OCR 引擎處理 PDF 並輸出結構化文字的圖示](images/ocr_flow.png "從 PDF 提取文字圖示")

*圖片說明：從 PDF 提取文字圖示說明 OCR 處理步驟。*

## 前置條件

- Python 3.9 或更新版本（程式碼使用 f‑strings 與型別提示）。  
- 可透過 pip 安裝的 OCR 套件，且提供 `OcrEngine` 類別（例如虛構的 `pyocr` 套件）。  
- 您欲處理的 PDF 檔案，已儲存於本機（例如 `form.pdf`）。  

如果缺少 OCR 套件，請執行以下指令安裝：

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## 步驟 1：從 PDF 提取文字 – 設定 OCR 引擎

在我們能 **read PDF with OCR** 之前，需要先建立一個引擎實例。可以把引擎想像成一個大腦，會檢視每個像素並判斷它代表的字元是什麼。

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **為什麼這很重要：** 只要初始化一次引擎，就能在多個檔案間重複使用已載入的語言模型，節省時間與記憶體。

---

## 步驟 2：載入影像以供 OCR – 準備您的 PDF

PDF 本身不是原始影像，通常套件會提供輔助函式，將第一頁（或全部頁面）轉換成 OCR 引擎可辨識的影像。

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **小技巧：** 若 PDF 有多頁，許多 OCR 套件允許傳入 `page=2` 或在迴圈中呼叫 `engine.load_image(pdf_path, page=n)`。處理大型文件時，建議分批載入頁面，以避免記憶體激增。

---

## 步驟 3：使用 OCR Engine Python – 識別結構化文字

現在開始進行重點工作。`recognize_structured()` 會回傳 block → line → word 的層級結構，每個元素都帶有語言、信心分數與邊界框資訊。

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **您會得到：**  
> - `structured_result.blocks` – 最上層容器（通常是段落或欄位）。  
> - 每個 block 包含 `lines`，每條 line 包含 `words`。  
> - 信心分數可用來過濾不可靠的結果。

---

## 步驟 4：遍歷結果 – 存取 Blocks、Lines 與 Words

以下是一段精簡的迴圈，會印出最實用的資訊。您可以自行擴充，寫入 JSON、CSV，或寫入資料庫。

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### 預期輸出

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **為什麼您會喜歡這樣：** 這層級結構與人類閱讀頁面的方式相同，日後重建表格或欄位布局時相當方便。

---

## 步驟 5：處理邊緣案例 – 低信心與多頁 PDF

### 低信心字詞

如果某個字詞的信心低於 `0.70`，您可能想將它標記為需人工審核：

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### 處理所有頁面

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **專業提示：** 若 OCR 套件每次都重新渲染影像，建議將中間產生的 PNG 暫存起來，可為大量批次處理節省數秒時間。

---

## 完整可執行腳本

將上述所有步驟整合成一個檔案，即可直接執行：

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

將此檔案儲存為 `extract_pdf_ocr.py` 後執行：

```bash
python extract_pdf_ocr.py
```

您應該會在主控台看到 block 級別的詳細資訊，並顯示任何低信心的警告。

---

## 結論

我們剛剛完整示範了如何使用 **OCR engine Python** 來 **extract text from PDF**。從安裝套件、**load image for OCR**、**read PDF with OCR**，到遍歷結構化輸出，您現在擁有一支可重複使用的腳本，能夠套用於任何專案。

接下來您可以探索的方向：

- 將層級結構匯出為 JSON，供下游 NLP 流程使用。  
- 加入語言偵測，動態切換 OCR 模型。  
- 結合 `pdf2image` 先行處理具有複雜版面的 PDF。  

試著在多頁發票批次上運行，調整信心門檻，看看多快能把掃描 PDF 轉換成可搜尋、可編輯的文字。若遇到任何問題，歡迎在下方留言——祝您 OCR 順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}