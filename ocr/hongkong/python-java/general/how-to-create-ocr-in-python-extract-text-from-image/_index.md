---
category: general
date: 2026-04-26
description: 快速且可靠地建立 OCR。學習如何從圖像提取文字、載入圖像進行 OCR，並使用自訂詞典對 PNG 進行 OCR。
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: zh-hant
og_description: 如何在 Python 中建立 OCR 並從圖像提取文字。本指南示範如何載入圖像以進行 OCR、在 PNG 上執行 OCR，以及使用自訂字典。
og_title: 如何在 Python 中建立 OCR – 快速文字提取
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中建立 OCR – 從影像提取文字
url: /zh-hant/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中建立 OCR – 步驟指南

有沒有想過 **如何建立 OCR**，讓它能讀取你的掃描 PDF、螢幕截圖或手寫筆記？你並不孤單。在許多實務專案中，我們需要 *從影像檔案中擷取文字*，但現成的引擎常常在領域特定詞彙上卡關。

在本教學中，你將看到一個完整、可執行的範例，示範如何 **載入影像進行 OCR**、套用自訂字典，最後 **對 PNG 檔執行 OCR**。完成後，你就能從任何影像擷取文字，並依照自己的術語調整引擎。

## 本教學涵蓋內容

我們會一步步說明你需要的所有操作：

* 安裝小巧卻功能強大的 `aocr` 套件（或任何相容的函式庫）。  
* 設定 **自訂字典**，讓 `aspocorp` 或 `licensekey` 等詞彙被正確辨識。  
* **載入影像進行 OCR**，不論是 PNG、JPEG，或是掃描的 PDF 頁面。  
* 執行 OCR 程序並印出結果。  

不提供外部文件連結，全部都是可直接複製貼上、立即執行的完整解決方案。

### 前置條件

* Python 3.8 或更新版本（程式碼使用 f‑string）。  
* 基本的指令列操作知識 – 只要打幾個 `pip install` 指令即可。  
* 一個影像檔（教學範例中的 `technical_doc.png`），放在可參考的路徑下。  

只要符合上述三項，你就可以開始了。  

---

## 步驟 1：安裝 OCR 函式庫

首先，我們需要一個支援可程式化設定物件的 OCR 引擎。`aocr` 套件是原生 OCR 引擎的輕量包裝，十分適合示範使用。

```bash
# Install the library (run once)
pip install aocr
```

> **小技巧：** 若你在 Windows 上遇到編譯錯誤，請改用 `pip install aocr‑binary`，它提供已編譯好的 wheel。

### 為何要安裝這個函式庫？

`aocr` 讓我們可以直接存取 `config` 物件，並注入 **自訂字典**。這正是提升特定詞彙辨識準確度的關鍵。

---

## 步驟 2：建立 OCR 引擎實例並加入自訂字典

現在我們啟動引擎，並告訴它哪些詞彙應被視為已知。

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### 為何自訂字典如此重要

標準 OCR 模型是以通用語料庫訓練的。當模型看到 “aspocorp” 時，可能會把它切成 “aspo corp” 或直接遺漏字母。透過自訂清單，我們能將辨識器偏向正確的拼寫，大幅減少後處理工作。

---

## 步驟 3：載入要處理的影像

接下來就是 **載入影像進行 OCR**。`Image.load` 方法接受路徑字串，會自動判斷檔案類型。

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **特殊情況：** 若來源是多頁 PDF，請先將每頁轉成 PNG（例如使用 `pdf2image`），再逐一送入引擎。

### 提升影像品質的技巧

* 解析度至少保持在 300 dpi。  
* 確保影像方向正確，必要時使用 `Pillow` 旋轉。  
* 將彩色掃描轉為灰階，以降低雜訊。

---

## 步驟 4：對 PNG 檔執行 OCR

在引擎設定完成且影像已載入後，我們終於 **對 PNG 執行 OCR**。

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()` 呼叫會回傳一個物件，內含辨識出的文字、信心分數以及每個單字的邊界框。

---

## 步驟 5：輸出辨識結果文字

最簡單的方式就是印出 `text` 屬性。

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### 預期輸出

如果 `technical_doc.png` 包含句子 *“The Aspocorp licensekey expires on 2025‑12‑31.”*，控制台應顯示：

```
The Aspocorp licensekey expires on 2025-12-31.
```

可見自訂字典成功保留了品牌名稱——這是一般 OCR 常會搞亂的部分。

---

## 完整可執行範例（即貼即用）

以下是完整腳本，請存成 `run_ocr.py`。只要把佔位路徑改成你的影像所在位置即可。

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

在終端機執行：

```bash
python run_ocr.py
```

你應該會在控制台看到與前述範例相同的擷取文字。

---

## 常見問題 (FAQ)

| 問題 | 答案 |
|----------|--------|
| **我可以從掃描的 PDF 取得文字嗎？** | 可以。先將每頁轉成 PNG（或 TIFF），再使用相同腳本處理。 |
| **如果我的影像是 JPEG 而不是 PNG，怎麼辦？** | `Image.load` 本身支援 JPEG、BMP、TIFF 與 PNG，只要更換副檔名即可。 |
| **如何提升低對比度掃描的準確度？** | 使用 `Pillow` 前處理——提升對比、二值化，或使用 `opencv` 去除傾斜。 |
| **能取得每個單字的信心分數嗎？** | `ocr_result` 包含 `words`，每個 word 都有 `confidence` 屬性，可自行迭代。 |
| **可以在無頭伺服器上執行嗎？** | 完全可以。`aocr` 沒有 GUI 依賴，適合 CI pipeline 使用。 |

---

## 後續步驟與相關主題

既然你已掌握 **如何建立 OCR** 以及 **從影像檔案擷取文字**，可以進一步探索：

* **前處理技術** – `load image for OCR` 只是第一步，使用 `opencv` 進行去噪或銳化。  
* **批次處理** – 迴圈遍歷 PNG 目錄，產生可搜尋的檔案庫。  
* **多語言支援** – 若需讀取法文或德文文件，可加入語言套件。  
* **結合 Elasticsearch** – 將擷取文字索引至 Elasticsearch，實現掃描資產的全文搜尋。  

上述延伸皆以本教學的核心模式為基礎，轉換起來相當順暢。

---

## 小結

只要幾分鐘，我們就說明了 **如何建立 OCR**，讓它可靠 **從影像檔案（特別是 PNG）擷取文字**，並示範了 **載入影像進行 OCR**、套用 **自訂字典**、以及 **對 PNG 執行 OCR**，全程不依賴外部服務。  

試跑腳本、調整字典以符合你的行業術語，你就擁有了文件數位化的堅實基礎。  

若在執行過程中遇到任何問題，歡迎在下方留言，我很樂意協助。也別忘了分享你的成功案例，社群最需要真實的應用經驗。  

**想自動化你的文件處理嗎？** 立即取得程式碼、依需求調整，今天就把像素轉換成可搜尋的文字吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}