---
category: general
date: 2026-06-06
description: 使用 Python OCR 從圖片 PDF 中提取文字。了解如何透過非同步批次辨識快速將掃描文件轉換為文字。
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: zh-hant
og_description: 使用 Python 從圖片 PDF 中提取文字。本分步指南展示如何使用非同步 OCR 將掃描文件轉換為文字。
og_title: 從圖片 PDF 中提取文字 – Python OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 從影像 PDF 中提取文字 – Python 教學：將掃描文件轉換為文字
url: /zh-hant/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像 PDF 提取文字 – Python 教學：將掃描文件轉換為文字

是否曾經想要 **從圖像 PDF 提取文字**，卻不想花上數小時重新打字？在本教學中，我們將示範如何使用簡單的非同步 OCR 工作流程，於 Python 中 **將掃描文件轉換為文字**。

如果你曾經盯著一堆掃描的 PDF，心想「一定有更快的方法」，那麼你來對地方了。我們會逐行說明程式碼，解釋每個部份的意義，甚至涵蓋你可能會遇到的幾個邊緣情況。

## 你將學會

- 如何啟動 OCR 引擎並設定辨識語言。  
- 如何將 PNG 與 PDF 的混合清單餵入批次辨識器。  
- 以非同步方式執行 OCR 工作，讓你的應用保持回應。  
- 取得結果、將其與來源檔案配對，並輸出整潔的文字。  

**先備條件**：Python 3.8+、對 `asyncio` 或 `concurrent.futures` 有基本了解，以及一個提供類似 `OcrEngine` 類別的 OCR 函式庫（例如 Aspose.OCR、Tesseract 包裝器，或自訂包裝器）。不需要繁雜的設定——只要安裝函式庫即可開始。

![從圖像 PDF 提取文字](https://example.com/placeholder.png "OCR 輸出截圖 – 從圖像 PDF 提取文字")

## 從圖像 PDF 提取文字 – 設定 OCR 引擎

首先，你需要一個已設定好文件語言的 OCR 引擎實例。此範例使用法文，你可以自行換成任何支援的語言。

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**為什麼這很重要**：事先設定語言能大幅提升辨識準確度。引擎會使用語言專屬的字典與字元模型；若使用錯誤的語言，常會出現亂碼。

## 準備檔案清單 – 圖片與 PDF 同時處理

我們的批次辨識器能同時處理點陣圖 (`.png`, `.jpg`) 與 PDF 容器。只要提供一個普通的 Python 檔案路徑清單即可。

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**小技巧**：保持清單為單層結構；引擎會在內部將每個 PDF 頁面解壓為圖像再進行辨識。如果檔案數量達到數千，建議將清單切成較小的批次，以避免記憶體激增。

## 發起非同步批次辨識

我們不會阻塞主執行緒，而是將 OCR 工作放到背景執行。此方法會回傳一個 `Future`，最終會持有 `OcrResult` 物件的清單。

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**運作原理**：在底層，引擎會建立執行緒池（或非同步任務，視實作而定）。這讓你可以同時執行其他工作——例如更新 UI、取得更多檔案，或記錄進度——而繁重的辨識工作則在其他地方完成。

## OCR 執行時做點有用的事

常見錯誤是空等並在緊密迴圈中輪詢 `Future`。相反地，你可以在此期間執行任何不相關的工作。以下示範僅列印一行狀態訊息。

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## 未來完成後收集結果

當你準備好取得 OCR 輸出時，使用 `concurrent.futures` 的 `as_completed`。無論是單一 `Future` 或多個，都適用此模式。

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**你會看到的結果**：每個檔案路徑後面接著抽取出的純文字。對於 PDF，`result.text` 包含所有頁面的合併文字。

### 預期輸出（範例）

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

如果發現缺字，請再次確認設定的語言與文件語言相符，並考慮在送入引擎前先對圖像做前處理（去斜、提升對比度）。

## 處理邊緣情況與常見陷阱

| 情況 | 處理方式 |
|-----------|------------|
| **混合語言** | 先執行語言偵測，再為每種語言建立獨立的引擎。 |
| **大型 PDF（> 100 MB）** | 使用 `PyPDF2` 等工具將 PDF 拆成單頁檔案，並分別作為條目餵入。 |
| **非拉丁文字** | 確認 OCR 函式庫已包含所需語言套件；部分函式庫需自行下載額外資料檔。 |
| **效能瓶頸** | 增加執行緒池大小（`engine.set_thread_pool_size(8)`）或改用支援 GPU 的後端（若有）。 |
| **低解析度圖像缺字** | 使用 OpenCV 前處理：`cv2.resize`、`cv2.threshold`、`cv2.medianBlur` 以提升可讀性。 |

## 完整可執行範例（直接複製貼上）

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

將此檔案存為 `extract_text_async.py`，將 `YOUR_DIRECTORY` 替換成你的檔案路徑，安裝 OCR 套件（`pip install your-ocr-lib`），然後執行 `python extract_text_async.py`。你應該會看到前面示範的主控台輸出。

## 往後的步驟 – 超越基礎抽取

- **後處理**：去除多餘空白、正規化 Unicode（`unicodedata.normalize`），或使用拼字檢查器清理 OCR 噪聲。  
- **結構化輸出**：將結果匯出為 CSV、JSON，或直接寫入資料庫，以供後續搜尋使用。  
- **平行批次**：若有上百個檔案，可同時啟動多個 `Future`，並使用佇列讓 CPU 持續忙碌而不致記憶體過載。  
- **整合 Web 框架**：將此腳本掛接至 Flask 或 FastAPI 端點，提供即時 OCR 服務。

---

### TL;DR

現在你已掌握如何使用最小的 Python 腳本，透過非同步 OCR **從圖像 PDF 提取文字**，在程式保持回應的同時 **將掃描文件轉換為文字**。可自行調整語言設定、批次大小與前處理技巧，以爭取最高的辨識正確率。

有任何想法想分享——例如手寫筆記的 OCR，或雲端服務的應用？歡迎留言，祝開發愉快！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能在此基礎上延伸更多 API 功能與實作方式，並提供完整可執行的程式碼範例與逐步說明，協助你在自己的專案中深入應用。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}