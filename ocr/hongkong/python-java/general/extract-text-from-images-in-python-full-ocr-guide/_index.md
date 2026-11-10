---
category: general
date: 2026-06-19
description: 使用 Python OCR 從圖片提取文字。於簡潔教學中學習自動語言偵測、平行處理與批次辨識。
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: zh-hant
og_description: 使用 Python OCR 從圖像中提取文字。本指南在單一教學中展示自動語言偵測、平行處理與批次辨識。
og_title: 使用 Python 從圖像提取文字 – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中從圖片提取文字 – 完整 OCR 指南
url: /zh-hant/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖片中擷取文字 – 完整 OCR 教學

有沒有想過 **從圖片中擷取文字** 而不必手動輸入每個字？你並不是唯一有這個需求的人。無論是要數位化舊收據、建立可搜尋的文件庫，或只是想玩玩 AI 小技巧，從圖片中抽取文字都是現今 Python 開發者必備的技能。

在本教學中，我們將一步步示範一個完整、可直接執行的範例，使用熱門的 OCR 引擎 **擷取圖片文字**。內容涵蓋自動語言偵測、平行處理加速，以及批次影像辨識，讓你能在數秒內處理數十個檔案。聽起來正是你需要的嗎？讓我們開始吧。

## 你將學到什麼

- 如何使用 `ocr.OcrEngine` 建立 OCR 引擎實例。  
- 啟用 **自動語言偵測**，讓引擎自行選擇正確語言。  
- 以自訂執行緒池設定 **平行處理 OCR**。  
- 在檔案清單上執行 **批次影像辨識**。  
- 印出每張圖片的辨識文字，方便儲存或建立索引。

不需要額外文件說明——所有必要資訊都在此，且程式碼可直接使用 `ocr` 套件（透過 `pip install ocr` 安裝）即跑通。

## 前置條件

在開始之前，請確保你已具備：

1. Python 3.8 或更新版本。  
2. `ocr` 套件（`pip install ocr`）。  
3. 一個放有 PNG（或 JPG）圖片的資料夾。  
4. 基本的 Python 函式與迴圈概念。

就這樣——沒有繁重的相依套件，亦不需要 GPU，只要純 Python。

![從圖片中擷取文字範例](https://example.com/ocr-demo.png "螢幕截圖顯示從圖片中擷取文字的輸出")

*Alt text: 從圖片中擷取文字示範螢幕截圖*

## 第一步 – 設定 OCR 引擎 (Primary Keyword in Action)

首先，建立一個 OCR 引擎實例。把 `ocr.OcrEngine()` 想成整個流程的「大腦」；它負責辨識字元、行與段落。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

為什麼需要顯式建立引擎？因為 **ocr.OcrEngine 的使用方式** 能讓你細部控制語言設定、執行緒等，是相較於單行輔助函式最彈性的 **從圖片中擷取文字** 方法。

## 第二步 – 讓引擎自動偵測語言

大多數 OCR 函式庫都需要你手動指定語言。對單一語言的專案還好，但面對混合語言的批次時就相當麻煩。幸好，`ocr` 套件支援 **自動語言偵測**。

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

將 `engine.language` 設為 `ocr.Language.Auto` 後，引擎會自行嗅探每張圖片並挑選適當的語言模型。這一行程式碼能為你省下處理國際文件時的數小時手動設定時間。

## 第三步 – 使用平行處理加速 OCR

如果你的電腦有四核心以上的 CPU，何不善加利用？引擎可以啟動執行緒池，讓多張圖片同時被處理。這正是 **平行處理 OCR** 發揮威力的地方。

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

依照你的機器自行調整 `4` 的數值。執行緒越多 → 批次執行越快，但每條執行緒都會佔用記憶體，請找出最適合你環境的平衡點。

## 第四步 – 收集要處理的圖片

接下來需要一個檔案路徑清單。你可以手動寫入、從 CSV 讀取，或使用 `glob`。為了說明，我們直接硬寫一小段清單：

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

把 `YOUR_DIRECTORY` 替換成你實際的路徑。如果有數十個檔案，只要 `glob.glob("*.png")` 就能快速抓取。

## 第五步 – 執行批次影像辨識

以下程式碼是本教學的核心：一次呼叫即可處理 `files` 中的所有圖片，並回傳結果物件清單。這就是讓大規模 OCR 成為可能的 **批次影像辨識** 功能。

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

在背後，引擎會把每個檔案分配給先前設定的四個工作執行緒，同時自動偵測每張圖片的語言。回傳的清單中，每個元素都包含辨識出的文字與相關中繼資料。

## 第六步 – 印出（或儲存）擷取的文字

最後，我們遍歷結果並印出文字。實務上你可能會把它寫入資料庫或 CSV 檔，但為了簡化示範，我們直接印出。

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**預期輸出**（為簡潔起見已截斷）：

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

每個區塊會先顯示檔名，接著是 OCR 產生的字串。若圖片包含多種語言，感謝前面的 **自動語言偵測** 步驟，對應的字元會正確顯示。

## 專業小技巧與常見陷阱

- **影像品質很重要** – 模糊或低對比的照片會產生雜訊。必要時可使用 OpenCV（`cv2.threshold`、`cv2.resize`）前處理。  
- **執行緒數 vs. I/O** – 若圖片儲存在慢速網路磁碟，增加執行緒未必有效。可使用 `top` 或 `Task Manager` 觀察 CPU 使用率。  
- **Unicode 處理** – `result.text` 為 Unicode 字串。寫檔時請以 `encoding="utf‑8"` 開啟，以免拋出 `UnicodeEncodeError`。  
- **記憶體使用** – 大型 PDF 可能佔用大量 RAM。若遭遇 `MemoryError`，請縮減執行緒池大小或分批處理圖片。

## 完整可執行腳本

以下是完整、可直接複製貼上的腳本，已整合上述所有步驟。將它存為 `batch_ocr.py`，然後執行 `python batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

執行方式如下：

```bash
python batch_ocr.py ./my_images 4
```

執行後，你會看到每張圖片對應的格式化文字區塊，證明你已能 **從圖片中擷取文字**，且規模化處理。

## 接下來可以做什麼？

既然已掌握使用 Python **從圖片中擷取文字** 的基礎，以下方向值得一試：

- **後處理**：使用正規表達式或自然語言處理套件清理 OCR 輸出。  
- **PDF 轉換**：將擷取的字串輸入 PDF 產生器，製作可搜尋的 PDF。  
- **雲端 OCR 服務**：將本地 `ocr` 結果與 Google Vision、Azure OCR 等服務比較，提升邊緣案例的準確度。  
- **GUI 前端**：打造小型 Flask 或 FastAPI 應用，讓使用者上傳圖片即時看到擷取結果。

以上主題皆以本次建立的 **Python OCR 套件** 為基礎，且同樣受惠於 **平行處理 OCR** 的技巧。

---

*祝編程愉快！若遇到任何問題，歡迎在下方留言，我隨時樂於協助排除 OCR 的各種怪癖。*


## 接下來該學什麼？

以下教學與本篇指南的技巧密切相關，能幫助你在專案中深入探索其他 API 功能與替代實作方式，每篇皆提供完整可執行的程式碼範例與逐步說明。

- [使用 Aspose OCR 從圖片擷取文字 – 步驟教學](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 OCR 操作資料夾批次擷取文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}