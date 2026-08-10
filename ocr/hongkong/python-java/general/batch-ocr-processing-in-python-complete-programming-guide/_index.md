---
category: general
date: 2026-06-25
description: 批次 OCR 處理在 Python 中變得輕鬆。學習如何從圖像批次提取文字，並以平行執行緒掌握批次圖像文字提取。
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: zh-hant
og_description: 在 Python 中進行批次 OCR 處理，可快速從圖像批次中提取文字。本教學將帶領您使用平行 OCR，並提供清晰的程式碼範例。
og_title: Python 批次 OCR 處理 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python 批次 OCR 處理 – 完整程式設計指南
url: /zh-hant/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 批次 OCR 處理（Python） – 完整程式指南

有沒有需要 **批次 OCR 處理**，卻不確定如何在數十頁掃描檔上有效執行？你並不是唯一遇到這個問題的人——開發者在嘗試從大量影像中擷取文字時，常常會卡在 CPU 負荷過高的問題上。

在本指南中，我們將示範一種直接的方式，使用 Python 的 OCR 引擎 **從影像批次中擷取文字**，並以最多八條執行緒執行工作，最後顯示每張影像貢獻了多少字元。完成後，你將擁有一個可重複使用的腳本，能像專業人士一樣處理 **批次影像文字擷取**。

## 本教學涵蓋內容

我們會一步步走過三個實用步驟：

1. 建立要辨識的影像檔案清單。  
2. 以 `max_threads=8` 的平行方式啟動 OCR 引擎。  
3. 迭代結果並印出簡潔的摘要。

不需要外部服務，也不需要奇怪的函式庫——只要純 Python 加上一個常見的 OCR 包裝器（例如 `easyocr` 的 `ocr` 或自訂的包裝器）。只要你已安裝 Python 3.8+ 與 OCR 套件，就可以直接複製貼上並執行。

---

## 步驟 1：為批次 OCR 處理準備影像檔案清單

首先，你需要一組影像路徑。把它想成 OCR 引擎的購物清單；每一項都指向一個 PNG、JPEG 或 TIFF 檔案，裡面包含你想讀取的文字。

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**為什麼這很重要：**  
提前建立清單讓 OCR 引擎能以真正的批次模式運作。它同時提供一個單一位置，讓你日後可以新增或移除檔案，而不必觸碰處理邏輯。此 sanity check 能防止在長時間執行時因「找不到檔案」而崩潰。

---

## 步驟 2：以平行執行緒執行批次 OCR（Extract Text from Image Batch）

現在把清單交給 OCR 引擎。大多數現代 OCR 包裝器都提供 `recognize_batch` 方法，接受 `max_threads` 參數。將它設為 `8`，即告訴函式庫啟動八條工作執行緒，在支援超執行緒的四核心 CPU 上可大幅縮短處理時間。

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**為什麼平行化有幫助：**  
OCR 是 CPU 密集型工作；每張影像都要通過神經網路或傳統引擎。逐一處理會非常慢，特別是高解析度的掃描檔。平行執行緒能讓所有核心保持忙碌，將 5 分鐘的工作縮減到約 1 分鐘（以一般硬體為例）。

**小技巧：** 若你使用 `easyocr`，在迴圈中呼叫的方式會是 `reader.readtext(image_path, detail=0)`。我們的 `recognize_batch` 抽象隱藏了這層複雜度，但如果函式庫本身不支援批次，你仍可自行改用 `ThreadPoolExecutor` 來實作。

---

## 步驟 3：遍歷結果並彙總批次影像文字擷取

OCR 完成後，你會得到一個結果物件的清單。把原始檔案路徑與對應的 OCR 輸出配對，然後為每張影像印出一行，顯示辨識出的字元數量。

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**你會看到的內容：**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**為什麼這一步很實用：**  
快速的字元計數讓你一眼就能判斷影像是否正確處理。若字元數異常低，可能是掃描模糊、語言設定錯誤，或檔案損毀——這些問題可以在進入後續分析前先行處理。

---

## 加分項：處理例外情況與常見陷阱

### 缺失或損毀的影像  
如果影像無法開啟，多數 OCR 函式庫會拋出例外，導致整個批次中止。請在批次函式內部使用 `try/except` 包住呼叫，或在步驟 1 的 sanity check 中先過濾掉問題檔案。

### 語言與 DPI 設定  
對於多語言文件，可傳入 `langs` 參數（例如 `langs=['en', 'de']`）。若掃描解析度過低，建議先用 `Pillow` 以 300 DPI 進行升級前處理——這通常能提升辨識準確度。

### 記憶體限制  
八條執行緒在處理大型影像時會佔用大量 RAM。若遭遇記憶體錯誤，可降低 `max_threads`，或將清單分成較小的區塊處理：

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## 完整可執行腳本

將上述所有部份組合起來，即得到一個完整、可直接執行的範例。將 `"YOUR_DIRECTORY"` 替換成存放 PNG 檔案的路徑，並確保已安裝 `ocr` 模組。

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**預期輸出**（你的數字會不同）：

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

使用 `python batch_ocr.py` 執行腳本，觀察終端機上快速產生的統計資訊。

---

## 視覺概覽

![Batch OCR processing flow diagram](image-placeholder.png "Diagram illustrating batch OCR processing steps")

*圖片說明：* *批次 OCR 處理流程圖，展示檔案清單建立、平行 OCR 執行與結果彙總的步驟。*

---

## 結論

現在你已掌握在 Python 中進行 **批次 OCR 處理** 的完整基礎。透過建立乾淨的影像清單、利用平行執行緒 **Extract Text from Image Batch**，以及彙總結果，你可以把繁雜的手動工作轉變為快速、可重複的管線。

接下來你可以：

- 將每個 `result.text` 儲存為 `.txt` 檔，以供後續 NLP 使用。  
- 結合字元計數與信心分數，過濾低品質頁面。  
- 把腳本整合進更大的文件匯入工作流程，甚至餵入搜尋索引。

無論是數位化檔案、開發收據掃描應用，或是為語言模型準備訓練資料，本文的概念都能在數百甚至數千檔案上以最小調整順利擴展。

對語言設定、影像前處理，或在雲端部署有任何疑問？歡迎留言或參考相關教學，如 *Python image preprocessing* 與 *asynchronous OCR with asyncio*。祝 coding 愉快！

## 接下來該學什麼？

以下教學與本指南的技巧緊密相關，能進一步深化你的能力。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}