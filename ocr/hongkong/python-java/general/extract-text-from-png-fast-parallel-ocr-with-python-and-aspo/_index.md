---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Python 中快速從 PNG 提取文字。學習如何利用平行影像辨識 Python 轉換掃描頁面的文字，實現高效能結果。
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: zh-hant
og_description: 使用 Aspose OCR 在 Python 中快速從 PNG 提取文字。本指南說明如何利用平行影像辨識將掃描頁面文字轉換，實現高速結果。
og_title: 從 PNG 中提取文字 – 使用 Python 的快速平行 OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: 從 PNG 提取文字 – 使用 Python 與 Aspose 的快速平行 OCR
url: /zh-hant/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 提取文字 – 使用 Python 的快速平行 OCR

是否曾經需要 **從 PNG 提取文字**，卻發現單執行緒的 OCR 速度緩慢？你並不孤單。無論是要將一堆掃描收據數位化，或是把課堂投影片轉成可搜尋的 PDF，瓶頸通常都出現在 OCR 步驟本身。

在本教學中，我們將示範一個完整、即時可執行的解決方案，使用 Aspose OCR 的非同步批次模式結合 Python 的 `ThreadPoolExecutor`，以平行方式 **轉換掃描頁面的文字**。完成後，你將能以 **recognize image text python** 風格辨識圖片文字，處理數十張圖片的時間僅是單純迴圈的零頭。

> **學完你會得到**  
> * 一個能同時從 PNG 圖片擷取文字的完整腳本。  
> * 為何非同步批次模式能提升效能的原理說明。  
> * 將解決方案擴展至更大工作負載的技巧。

## 你需要的環境

| 前置條件 | 原因 |
|--------------|--------|
| Python 3.9+ | 支援現代語法與型別提示。 |
| `aspose-ocr` 與 `aspose-storage` 套件 | 提供 OCR 引擎與圖片載入功能。 |
| 一個 PNG 檔案資料夾（例如掃描頁面） | 你想要處理的來源素材。 |
| 基本的 Python 並行概念 | 有助於理解但非必須，我們會一步步說明。 |

你可以使用以下指令安裝 Aspose 函式庫：

```bash
pip install aspose-ocr aspose-storage
```

> **小技巧：** 定期更新套件（`pip list --outdated`）以獲得最新的效能改進。

## 步驟 1：以非同步批次模式初始化 Aspose OCR 引擎

首先建立 `OcrEngine` 實例，並切換至 **非同步批次模式**。此模式會在內部排隊辨識請求，讓引擎能在不阻塞 Python 執行緒的情況下，同時處理多張圖片。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*為何使用 async？*  
在同步模式下呼叫 `recognize` 會阻塞，直到圖片完全處理完畢。非同步模式則允許引擎在當前圖片仍在解碼時，就開始處理下一張圖片，實現 I/O 與 CPU 工作的重疊。

## 步驟 2：列出要處理的 PNG 檔案

在這裡我們定義要處理的圖片集合。實務上你可能會動態產生此清單（例如 `glob.glob("*.png")`），但寫死列表可以讓範例更易於閱讀。

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **注意：** 請將 `YOUR_DIRECTORY` 替換成實際存放 PNG 掃描檔的路徑。若檔案數量達數百甚至上千，建議改用 `os.listdir` 並以 `.png` 為條件過濾。

## 步驟 3：撰寫載入圖片並回傳文字的輔助函式

此輔助函式將 **Aspose Storage** 載入檔案的兩步驟抽象化，然後交給 OCR 引擎辨識。加入簡短的 docstring 讓函式自說自話，方便未來維護。

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*為何要拆成獨立函式？*  
讓 ThreadPool 的程式碼保持簡潔，且可在其他地方（例如 Flask 端點）重複使用。將 I/O 與辨識分離也更易除錯——若某檔案失敗，例外追蹤中會直接顯示檔名。

## 步驟 4：使用 ThreadPoolExecutor 執行平行圖片辨識

現在引入 `ThreadPoolExecutor`。預設建立四個工作執行緒，你可以依 CPU 核心數與圖片數量調整 `max_workers`。

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### 為何這樣就能實現 Parallel Image Recognition Python

* **ThreadPoolExecutor** 會產生一組工作執行緒，每個執行緒都呼叫 `recognize_image`。  
* 由於 OCR 引擎處於非同步批次模式，每個執行緒在將工作交給引擎後仍能保持回應。  
* `as_completed` 會依照未來物件完成的順序產生結果，讓你能即時取得已完成的文字——非常適合串流大量批次。

> **常見陷阱：** 設定 `max_workers=1` 會失去平行化的意義。在 8 核心機器上，`max_workers=8` 通常能取得最佳吞吐量，但仍建議測試不同數值以找出最適配置。

## 步驟 5：驗證輸出並處理例外情況

執行腳本後，應會看到每個 PNG 的文字區塊，前面會標示檔名：

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

若有圖片讀取失敗（檔案損毀、格式不支援），`except` 區塊會印出友善的錯誤訊息，而不會讓整個批次崩潰。

### 延伸應用

| 情境 | 建議調整 |
|----------|-----------------|
| **上千頁文件** | 改用 `ProcessPoolExecutor` 以利用多個 CPU 行程，或將清單切塊分批處理。 |
| **其他影像格式（JPG、TIFF）** | `storage.Image.load` 會自動偵測格式，只要把檔案加入 `input_images` 即可。 |
| **需要儲存結果** | 在 `else` 區塊內將 `text` 寫入 `.txt` 檔或寫入資料庫。 |
| **效能監控** | 用計時器（`time.perf_counter`）包住 `recognize_image`，並記錄每個檔案的處理時間。 |

## 完整範例（直接複製貼上）

以下是完整腳本，可直接存為 `parallel_ocr.py`。內容完整，無遺漏，直接使用即可。

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

儲存檔案後，調整 `YOUR_DIRECTORY` 佔位符，然後執行：

```bash
python parallel_ocr.py
```

你應該會在終端看到每個 PNG 的擷取文字，與前面示範的結果相同。

## 結論

我們已示範如何透過結合 Aspose OCR 的非同步批次模式與 Python 的 `ThreadPoolExecutor`，高效 **從 PNG 提取文字**。此腳本以平行方式轉換掃描頁面的文字，提供一種可擴充的方式來 **recognize image text python**，而不必自行實作複雜的執行緒池。

如果想進一步優化，可考慮：

* 將結果寫入可搜尋的 SQLite 資料庫。  
* 在 OCR 前使用 OpenCV 進行影像前處理（去斜、去噪）。  
* 將腳本部署為 Flask 或 FastAPI 後端的微服務。

記住，高效 OCR 的關鍵不僅是更快的引擎，還在於如何以最大化併發的方式供給引擎工作。使用本範例的模式，你可以輕鬆處理數十甚至數百張 PNG 掃描檔，僅需極少的程式碼變更。

祝開發順利，願你的 PDF 永遠可搜尋！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}