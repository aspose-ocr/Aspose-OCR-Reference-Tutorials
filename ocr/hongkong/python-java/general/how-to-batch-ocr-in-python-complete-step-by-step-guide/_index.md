---
category: general
date: 2026-06-28
description: 如何使用 Python 批次進行 OCR。學習對多張圖片進行 OCR、從 PNG 提取文字，並將圖片轉換為文字的完整 Python OCR
  教學。
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: zh-hant
og_description: 在第一句說明如何在 Python 中批次執行 OCR。跟隨本 Python OCR 教學，即可高效從 PNG 檔案中擷取文字。
og_title: 如何在 Python 中批量 OCR – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中批次執行 OCR – 完整逐步指南
url: /zh-hant/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中批次 OCR – 完整步驟指南

有沒有想過 **how to batch OCR** 一堆掃描頁面卻不想寫會阻塞 UI 的迴圈？你並不是唯一有這個疑問的人。一次處理數十個 PNG 檔案，若每張圖片解碼需要一兩秒，感覺就像在看油漆乾一樣慢。

在本教學中，我們會示範一種乾淨、非阻塞的方式，同時 **OCR 多張圖片**、**從 PNG 抽取文字**，以及 **將影像轉換成文字**，使用現代的 Python OCR 引擎。完成後，你將得到一個可直接放入任何專案的腳本——非常適合作為快速 *python ocr tutorial*，或是正式的批次工作。

## 你將會建立的功能

- 初始化 OCR 引擎並設定語言為 Latin（或任何你需要的語言）。  
- 將圖片路徑清單（本例為 PNG）傳給引擎。  
- 發起一個批次操作，回傳類似 Future 的物件。  
- 使用執行緒池同時取得所有結果，讓主執行緒保持空閒。  
- 為每一頁印出辨識出的文字，並以清晰的分隔顯示。

沒有隱藏的魔法，只有純粹的 Python 加上第三方 OCR 函式庫（此處以虛構的 `pyocr` 套件說明）。

**先備條件**  
- 已安裝 Python 3.8+。  
- 具備 Python 函式與 `concurrent.futures` 的基本概念。  
- 取得提供 `OcrEngine` 類別的 OCR 函式庫（例如 `pip install pyocr`）。  

如果缺少上述任一項，請立即安裝——其實比想像中更簡單。

---

## How to Batch OCR in Python – Core Concepts

在寫程式碼之前，先說明每一步「為什麼」這樣做。

1. **為什麼要設定語言？**  
   當引擎知道要辨識哪些字符時，OCR 的準確度會大幅提升。Latin 適用於英文、法文、西班牙文等。若需要日文或阿拉伯文，可改用 `Language.Japanese` 或 `Language.Arabic`。

2. **為什麼使用批次操作？**  
   批次呼叫讓引擎在內部自行排程工作，通常會利用原生執行緒或 GPU 加速。它會回傳一個稍後可查詢的 handle，這樣就不會在每張圖片處理時阻塞程式。

3. **為什麼使用 ThreadPoolExecutor？**  
   我們取得的 Future 物件是 *lazy* 的——只有在我們要求時才開始取回結果。把執行緒池交給 `getAll`，就能讓 Python 同時抓取每頁文字，顯著縮短總執行時間。

4. **為什麼要列舉（enumerate）結果？**  
   結果的順序會與輸入路徑的順序相同，因此我們可以安全地為每頁標註頁碼。

了解這些「為什麼」之後，你就能把這套模式套用到其他函式庫或更大的資料集。

---

## Step 1: Install and Import Required Packages

首先，確保 OCR 函式庫已安裝。範例使用通用的 `pyocr` 套件；若你使用其他套件（例如 `pytesseract`、`easyocr`），請自行替換。

```bash
pip install pyocr
```

接著匯入所有需要的模組。

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** 使用 `pathlib` 的 `Path` 可以讓腳本跨平台，且程式碼更易讀。

---

## Step 2: Create the OCR Engine and Set Language

建立引擎非常簡單。我們在此示範將語言鎖定為 Latin。

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

`setLanguage` 的呼叫對某些引擎來說是可選的，但養成這個好習慣很有幫助。它會告訴 OCR 模型只關注你所需的字元集，從而提升速度與準確度。

---

## Step 3: List the Image Files to Process (Extract Text from PNG)

收集所有想要轉換的 PNG 檔案。使用 `Path.glob` 可以讓你只要把整個資料夾丟進來，就不必修改程式。

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **為什麼這麼做很重要：** 先排序清單可保證順序一致，之後才能正確對應每個結果與頁碼。

---

## Step 4: Launch a Batch OCR Operation (Convert Image to Text)

現在把清單交給引擎。此方法會回傳一個類似 Future 的容器，我們稍後再去輪詢。

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

在底層，引擎可能會自行啟動工作執行緒，甚至是 GPU 管線。我們只需要拿到 `batch_future` 這個 handle，就能取得各別結果。

---

## Step 5: Retrieve All Results Concurrently (OCR Multiple Images)

這裡才是真正的「批次」工作。把 `ThreadPoolExecutor` 傳給 `getAll`，每頁文字就會在自己的執行緒中被抓取。

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

`max_workers` 可以依你的 CPU 核心數或 OCR 函式庫的建議做調整。更多執行緒不一定代表更快——請留意 CPU 使用率。

---

## Step 6: Output the Recognised Text (Python OCR Tutorial Finale)

最後，印出每頁的文字。`Result` 物件提供 `getText()` 方法——若你的函式庫使用不同名稱，請自行調整。

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**預期輸出（範例）**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

若有圖片處理失敗，大多數引擎會回傳空字串或拋出例外——你可以把迴圈包在 `try/except` 中，以優雅處理邊緣情況。

---

## Full Script – Ready to Run

以下是完整、獨立的腳本。將內容複製貼上成 `batch_ocr.py`，調整 `YOUR_DIRECTORY` 後執行 `python batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

儲存、執行，然後觀察 console 中被抽出的文字。簡單、快速，且完全非同步。

---

## Common Pitfalls & How to Avoid Them

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| **沒有輸出** – 空字串 | OCR 引擎找不到文字（影像噪點過多） | 前置處理影像：二值化、去斜或提升 DPI |
| **`FileNotFoundError`** | 資料夾路徑錯誤或缺少 PNG 檔案 | 再次確認 `YOUR_DIRECTORY`，確保檔案副檔名為 `.png` |
| **CPU 使用率過高** | `max_workers` 設定過高，超出機器負載 | 降低 `max_workers`，或在支援的情況下啟用 GPU 加速 |
| **Unicode 亂碼** | 引擎預設語言不符 | 在批次 OCR 前呼叫 `engine.setLanguage(Language.Latin)`（或其他語言） |

提前處理這些常見問題，可為你省下大量除錯時間。

---

## Extending the Tutorial – Next Steps

- **OCR 多種格式**（JPEG、TIFF）——只要改變 glob pattern 即可。  
- **從 PNG 抽取文字**，再將結果寫入搜尋索引（例如 Elasticsearch）。  
- **將影像轉文字**，再用 `reportlab` 或 `PyPDF2` 產生 PDF。  
- **跨機器平行化**，使用 `multiprocessing` 或 Celery 等工作佇列，處理海量資料集。  

上述每個主題都自然延伸自你剛完成的 **python ocr tutorial**。

---

## Conclusion

我們已完整示範 **how to batch OCR** 一批 PNG 檔案，說明批次 API 的威力，並展示如何以執行緒池方式 **extract text from PNG**。上方的完整腳本已具備生產環境可用的水準，現在你可以把它套用到任何需要大量 OCR 的 Python 專案。

試著執行、調整語言設定，甚至把 `pyocr` 換成 `pytesseract`——模式不變。若有任何問題或想分享有趣的應用案例，歡迎留言，我們一起討論。

*Happy coding!*

## What Should You Learn Next?

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索不同的實作方式。

- [從圖片中抽取文字 – Aspose OCR 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 OCR 操作資料夾抽取文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [在 Aspose.OCR for .NET 中以 List 批次 OCR 圖片](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}