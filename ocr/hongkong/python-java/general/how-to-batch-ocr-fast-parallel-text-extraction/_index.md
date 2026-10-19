---
category: general
date: 2026-03-26
description: 如何使用 Python 高效批次 OCR——學習從圖像與 PDF 提取文字，並以平行處理進行 OCR 轉換。
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: zh-hant
og_description: 如何高效批量 OCR——使用 Python 的圖像文字提取、PDF OCR 轉換與批量 OCR 處理逐步指南
og_title: 如何批量 OCR：快速平行文字擷取
tags:
- OCR
- Python
- Parallel Computing
title: 如何批次 OCR：快速平行文字提取
url: /zh-hant/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR：快速平行文字擷取

有沒有想過 **如何批量 OCR**，當你手頭上有數十頁掃描文件、螢幕截圖和 PDF 時？你並不是唯一有此困擾的人——大多數開發者都會碰到同樣的瓶頸：逐一處理每個檔案會變成痛苦的瓶頸。  

好消息是，你可以啟動少量工作執行緒，將所有檔案餵入，然後觀察 OCR 引擎平行處理整批檔案。在本教學中，我們將逐步說明一個完整、可直接執行的範例，展示 **從影像擷取文字**、執行 **PDF OCR 轉換**，以及利用 **平行 OCR 處理** 以提升速度。

> **你將學到的內容**  
> * 一個完整可執行的 Python 腳本，能一次處理 PNG、TIFF、PDF 與 JPG 混合清單。  
> * 了解為何執行緒池能加速 I/O 密集型 OCR 任務。  
> * 處理錯誤、大型 PDF 以及自訂執行緒數量的技巧。  

## 前置條件

在開始之前，請確保你已具備以下條件：

| 需求 | 原因 |
|------|------|
| Python 3.8+ | 現代語法與 `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | 提供 `OcrBatchProcessor` 及結果物件 |
| A handful of sample files (PNG, TIFF, PDF, JPG) | 以觀察 **從影像擷取文字** 的實際效果 |
| Basic familiarity with threads (optional) | 有幫助但非必須 |

如果你尚未安裝 `ocr` 套件，請執行：

```bash
pip install ocr-lib   # replace with the actual package name
```

環境就緒後，讓我們拆解這個問題。

## 步驟 1：匯入輔助工具並實例化批次處理器

我們首先需要一個收集所有 OCR 工作的地方。`OcrBatchProcessor` 類別正是如此——它會排隊工作項目，並回傳 `Future` 物件的清單。

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*為何重要*：匯入 `as_completed` 讓我們能即時回應每個完成的工作，而不必等最慢的檔案。這是 **批量 OCR 處理** 的核心。

## 步驟 2：調整工作執行緒池以平行執行

預設情況下，處理器可能只使用單一執行緒，這會抵消批次處理的意義。我們明確要求使用四個工作執行緒——你可以自行將此數字提升至 CPU 核心數量。

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*專業提示*：對於像 OCR 這類 I/O 密集型任務，超過 `CPU cores * 2` 後通常會遇到報酬遞減。測試幾個數值，找出最佳點。

## 步驟 3：將所有欲 OCR 的檔案加入佇列

此處我們加入混合的影像與 PDF 檔案。`add` 方法僅記錄路徑；實際工作會在提交批次後才開始。

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

如果需要處理整個資料夾，只要使用簡單的 `glob` 迴圈即可：

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## 步驟 4：發送工作並收集 futures

呼叫 `submit_all` 為處理器開綠燈。它會回傳 `Future` 物件的清單——可視為稍後會出現結果的佔位符。

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

此時 OCR 引擎在背景執行，每個執行緒都在處理檔案。

## 步驟 5：在完成時立即取得結果

使用 `as_completed` 我們會依照 futures 完成的順序迭代，而非提交的順序。這讓腳本保持回應性，尤其是當某些 PDF 比簡單的 PNG 花更長時間時。

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**預期輸出**（為簡潔起見已截斷）：

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

每個區塊對應原始檔案的純文字表示。如果你在執行 **PDF OCR 轉換**，文字將包含 OCR 引擎從每頁辨識出的全部內容。

## 處理邊緣案例與常見陷阱

| 情況 | 需留意的地方 | 快速解決方案 |
|------|--------------|--------------|
| 損壞的影像 | `future.result()` 拋出 `OSError` | 使用 `try/except` 包裹（參見上方程式碼） |
| 非常大的 PDF（> 100 MB） | 記憶體壓力、執行緒變慢 | 適度增加 `thread_count` 或先將 PDF 拆分為章節 |
| 混合語言文件 | 預設 OCR 模型可能偵測錯誤 | 若函式庫支援，向 `OcrBatchProcessor` 傳遞語言提示 |
| 需要保留版面 | 純 `get_text()` 會失去欄位 | 使用 `ocr_result.get_hocr()` 或類似的版面感知方法 |

### 專業提示：依檔案類型自訂執行緒數量

如果你知道大部分工作負載是 PDF，則可以為 PDF 分配較多執行緒，為小型 PNG 分配較少。有些函式庫允許傳遞每個工作 `priority`；若無法使用，你可以建立兩個獨立的批次——一個處理影像，一個處理 PDF，並同時執行。

## 視覺概覽（可選）

![批量 OCR 工作流程圖](https://example.com/ocr-workflow.png "批量 OCR 工作流程")

*此圖示說明了從檔案發現 → 批次建立 → 平行執行 → 結果彙總的流程。*

## 完整腳本，直接複製貼上

以下是完整程式碼，可直接放入 `.py` 檔案。它包含上述所有片段，並加入一個自動在目錄中偵測支援檔案的小幫手。

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

將此檔案另存為 `batch_ocr.py`，指向包含掃描檔的資料夾，即可看到主控台充滿擷取出的文字。  

### 為何這樣有效

* **執行緒池** – OCR 大多在等待磁碟 I/O 與外部引擎呼叫，因此多執行緒可讓 CPU 持續忙碌。  
* **`as_completed`** – 你可在結果就緒時立即取得，這對 UI 回饋或串流管線非常理想。  
* **錯誤隔離** – 單一壞檔不會導致整批失敗；`try/except` 區塊可將失敗隔離。

## 結論

總而言之，你現在已掌握使用 Python 的 `concurrent.futures` 搭配支援批次處理的 OCR 函式庫來 **批量 OCR** 的方法。透過設定適度的執行緒池、將所有支援的檔案加入佇列，並在完成時即時取得結果，你即可在不犧牲可靠性的前提下達成快速的 **平行 OCR 處理**。  

接下來，你可以：

* 將輸出掛接至搜尋索引，以快速檢索文件。  
* 擴充腳本，使每個結果寫入與原始檔同目錄的 `.txt` 檔案。  
* 若 OCR 函式庫提供非同步 API，可將內建執行緒池換成 `asyncio`。  

持續實驗——換成 Tesseract、Azure Cognitive Services 或 Google Vision，你會發現相同的模式同樣適用。祝 OCR 順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}