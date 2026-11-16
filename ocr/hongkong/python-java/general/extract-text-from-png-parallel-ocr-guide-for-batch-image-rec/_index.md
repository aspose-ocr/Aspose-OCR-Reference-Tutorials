---
category: general
date: 2026-03-18
description: 使用 Python 與 Aspose OCR 從 PNG 提取文字。了解如何載入圖像進行 OCR、對多個檔案執行 OCR，以及使用平行圖像辨識實現批次
  OCR 圖片。
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: zh-hant
og_description: 使用 Aspose OCR 在 Python 中從 PNG 提取文字。本教學示範如何載入影像進行 OCR、批次處理多個檔案，以及利用平行影像辨識執行批量
  OCR。
og_title: 從 PNG 擷取文字 – 平行 OCR 指南
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: 從 PNG 提取文字 – 批量影像辨識的平行 OCR 指南
url: /zh-hant/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 提取文字 – 批次影像辨識的平行 OCR 指南

是否曾需要從 **PNG** 檔案**提取文字**，卻卡在單張影像處理時間過長的階段？你並不孤單。在許多實務專案中——例如發票掃描器、收據數位化或檔案保存工具——速度至關重要，逐一處理每個 PNG 根本無法滿足需求。  

在本指南中，我們將逐步說明一個完整、即時可執行的解決方案，該方案**loads image for OCR**，以**ocr multiple files**的**batch OCR images**方式執行，並利用 Python 的 `threading` 模組實現**parallel image recognition**。完成後，你將擁有一個腳本，能在數秒內（而非數分鐘）從任意數量的 PNG 中提取文字。

## 需要的環境

- Python 3.8 或更新版本（示範的語法在 3.10+ 亦可使用）。  
- Aspose OCR for Java/​Python 套件 (`aspose-ocr`)。可透過 `pip` 安裝。  
- 一個包含多個欲處理 PNG 檔案的資料夾。  
- 適量的記憶體——每個執行緒會持有一個小型 OCR 引擎實例，即使是筆記型電腦也能啟動數十個工作者。

不需要外部服務、雲端金鑰，也不需要神祕的設定檔。只要純粹的 Python 程式碼，直接複製貼上即可執行。

## 為何要平行提取 PNG 文字？

處理 PNG 屬於 CPU 密集型工作：OCR 引擎會執行一系列影像分析演算法，逐像素處理資料。當你有十張、二十張或上百張影像時，總執行時間基本上等於每張單獨處理時間的總和。  

透過為每個檔案產生一個執行緒，我們讓作業系統同時排程這些 CPU 密集的工作。在多核心機器上，這通常能將實際執行時間減半，甚至減至四分之一。缺點是記憶體佔用會稍微增加，但對大多數批次工作而言，速度提升是非常值得的。

> **Pro tip:** 如果你要處理數百 MB 的影像，建議改用 `concurrent.futures.ProcessPoolExecutor` 取代 `threading`。相較於 GIL 限制的 CPython 解釋器，使用多行程可提供真正的平行運算，代價是稍微增加一些開銷。

## 步驟 1：安裝 Aspose OCR for Python

首先，先把 OCR 函式庫安裝到你的系統上。

```bash
pip install aspose-ocr
```

這一行會下載最新的 Aspose OCR 二進位檔及其 Python 綁定。如果遇到權限錯誤，請嘗試加上 `--user` 或使用虛擬環境。

## 步驟 2：載入影像進行 OCR – 工作執行函式

現在我們定義每個執行緒會執行的核心例程。它**loads image for OCR**，執行辨識，並印出提取文字的預覽。

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

需要留意的幾點：

- **Why a new `OcrEngine` per thread?** 引擎會保有內部緩衝區；若共用同一個實例會導致競爭條件與輸出錯亂。  
- **Why strip newlines?** 在 console 輸出時可保持行列整潔。  
- **Error handling?** 在正式環境中，你會將程式本體包在 `try/except` 中，並可能寫入日誌檔——這部分稍後會說明。

## 步驟 3：列出要處理的 PNG 檔案

你可以硬編碼檔案清單，但較彈性的做法是掃描目錄。以下手動列出三個檔案作為示範，請自行將路徑改成你的資料夾。

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

如果你想自動偵測：

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

這個小調整讓你能批次**extract text from PNG**檔案，而不必每次都修改原始碼。

## 步驟 4：設定 ocr multiple files 以執行 batch OCR images

現在我們為每張影像建立一個執行緒。這就是 **batch OCR images** 模式的核心。

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

列表生成式讓程式碼保持簡潔，而每個 `Thread` 物件會保存目標函式及其參數（`image_path`）。

> **Side note:** Python 的 `threading` 模組使用原生作業系統執行緒，因此在四核心筆記型電腦上，通常最多同時有四個執行緒真正執行；其餘的會在核心空閒時被排程。

## 步驟 5：執行平行影像辨識

啟動工作者非常簡單：遍歷清單並呼叫 `start()`。之後使用 `join()` 等待所有執行緒結束。

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

腳本執行完畢後，你會看到類似以下的多行輸出：

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

此輸出證明每個 PNG 已完成處理，且提取的文字可供後續使用（例如儲存至資料庫或輸入 NLP 流程）。

## 步驟 6：驗證結果與處理例外情況

### 檢查空結果

有時影像噪點過多，或 OCR 引擎未偵測到任何字元。快速的健全性檢查可避免後續錯誤。

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### 限制同時執行的執行緒數量

若在資源有限的 VM 上執行，產生數百個執行緒可能會使排程器超載。可使用 semaphore 來限制同時併發數量：

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### 將結果儲存至檔案

若不想直接印出，可將結果寫入 CSV，包含檔名與提取文字：

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

請確保在執行緒函式外部**一次**開啟 CSV，以避免競爭條件；`csv` 模組的 writer 在簡單寫入時是執行緒安全的。

## 完整範例

將上述所有步驟整合起來，以下是一個可直接存為 `batch_ocr.py` 並執行的完整腳本：

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}