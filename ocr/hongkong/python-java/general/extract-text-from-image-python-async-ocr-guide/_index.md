---
category: general
date: 2026-01-12
description: 使用 Aspose OCR 於 Python 從圖像提取文字。學習如何在短短幾分鐘內使用非同步程式碼將掃描圖像轉換為文字。
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: zh-hant
og_description: 使用 Aspose OCR 在 Python 中提取圖像文字。本教程展示如何使用非同步函式將掃描圖像轉換為文字。
og_title: 從圖片提取文字 Python – 非同步 OCR 指南
tags:
- python
- ocr
- async
title: 從圖像提取文字 Python – 非同步 OCR 指南
url: /zh-hant/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字（Python） – 非同步 OCR 指南

是否曾在 **extract text from image Python** 腳本中卡住 OCR 部分？你並不孤單。許多開發者在面對掃描文件、想將其轉換為可搜尋文字時，常會感到無從下手。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何使用 Aspose OCR 的非同步 API **convert scanned image to text**。完成後，你將得到一個可直接嵌入任何專案的單一函式，並了解即使 OCR 需要數秒鐘，非同步處理也能讓應用保持回應。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.8+（非同步功能至少需要 3.7）
- `asposeocr` 套件（`pip install asposeocr`）– 本教學所使用的函式庫
- 一張掃描圖像檔（TIFF、PNG、JPEG – 任意 Aspose OCR 支援的格式）
- 基本的 `asyncio` 概念（若不熟悉也沒關係，我們會逐步說明）

不需要額外的系統相依性；Aspose OCR 已將所有必要組件打包。

![Diagram showing async OCR flow – extract text from image python](https://example.com/async-ocr-diagram.png "async OCR flow – extract text from image python")

## 步驟 1 – 建立非同步輔助函式  

解決方案的核心是一個 `async` 函式，負責載入圖像、啟動 OCR，然後等待結果。將函式設為非同步，可讓你在 OCR 引擎背景執行時，同時執行其他協程（例如下載更多檔案）。

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**為什麼這很重要：** 透過回傳 `Future`，Aspose OCR 會在獨立的執行緒池中完成繁重工作。`await` 會釋放事件迴圈，使你的應用保持流暢。若需要同時處理多張圖像，只要使用 `asyncio.gather` 排程多個 `async_ocr` 呼叫即可。

## 步驟 2 – 在事件迴圈中執行協程  

有了輔助函式後，我們需要執行它。`asyncio.run` 會建立全新的事件迴圈，執行協程，並在結束時乾淨地關閉。

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**小技巧：** 若將此程式碼整合到較大的非同步應用（例如 FastAPI），可以直接使用 `await async_ocr(...)`，而不必再呼叫 `asyncio.run`。

## 步驟 3 – 驗證輸出  

執行腳本後，應該會看到類似以下的結果：

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

若輸出雜亂，請檢查以下項目：

1. 圖像是否清晰且未過度壓縮。  
2. 是否選擇了正確的語言（`ocr.Language.ENGLISH` 適用於大多數拉丁文字）。  
3. 檔案路徑是否正確且檔案可讀取。

## 步驟 4 – 處理例外情況  

### 多語言  

若需 **convert scanned image to text** 成其他語言，只要更改語言屬性：

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### 大檔案  

對於非常大的 TIFF，建議先調整尺寸或轉換為較低解析度的 PNG 再送入 OCR。這樣可減少記憶體負擔並加快處理速度。

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### 錯誤處理  

將 OCR 呼叫包在 `try/except` 區塊中，以捕捉網路或授權相關的錯誤。

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## 步驟 5 – 大規模處理：同時處理多張圖像  

因為函式是非同步的，你可以一次發起多筆 OCR 工作：

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

此模式在 OCR 引擎平行運作時，讓 CPU 持續忙碌，顯著縮短總處理時間。

## 結論  

現在你已擁有一套完整的 **extract text from image Python** 解決方案，利用 Aspose OCR 的非同步 API。完整範例示範了如何：

1. 初始化 OCR 引擎並選擇語言。  
2. 使用 `process_async` 非同步啟動 OCR。  
3. 以 `await` 取得結果而不阻塞事件迴圈。  
4. 處理常見問題，如大檔案與多語言支援。  

歡迎將此程式碼套用到自己的工作流程——無論是文件管理系統、搜尋索引器，或是簡易的命令列工具。未來可進一步：

- 將提取的文字存入資料庫，以支援全文搜尋。  
- 加入 PDF 產生（例如使用 `PyPDF2`）以建立可搜尋的 PDF。  
- 結合 FastAPI 等 Web 框架，打造 RESTful OCR 服務。

祝開發順利，享受將掃描圖像轉換為可搜尋、可編輯文字的樂趣！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}