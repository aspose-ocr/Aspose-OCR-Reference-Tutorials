---
category: general
date: 2026-03-26
description: Python OCR 教學：學習如何從圖像提取文字、載入圖像進行 OCR，並使用 Aspose OCR 只需幾個步驟即可辨識收據文字。
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: zh-hant
og_description: Python OCR 教學：快速學習從圖像提取文字、載入圖像進行 OCR，並使用 Aspise OCR 識別收據文字。
og_title: Python OCR 教學 – 從圖片提取文字
tags:
- OCR
- Aspose
- Python
title: Python OCR 教程 – 使用 Aspose 從圖像提取文字
url: /zh-hant/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教學 – 使用 Aspose 從圖像提取文字

有沒有想過在不花費數小時撰寫自訂正則表達式的情況下，從模糊的收據或掃描的表單中抽取文字？你並不孤單。在本 **python ocr tutorial** 中，我們將逐步說明如何載入圖像進行 OCR、在 Python 中執行 OCR，最後使用 Aspose OCR 函式庫辨識收據檔案中的文字。

閱讀完本指南後，你將擁有一個可直接執行的腳本，能讀取任何支援的圖像格式、抽取文字內容，並將結果印到主控台。無需外部服務、無需 API 金鑰——只要純粹的 Python 加上一個強大的 OCR 引擎。

## 需要的環境

- Python 3.8 或更新版本（程式碼使用型別提示，建議使用較新的直譯器）
- 透過 `pip install aspose-ocr` 安裝 `asposeocrjava` 套件
- 範例圖像，例如 `receipt_noisy.jpg`，內含一般商店收據
- （可選）使用虛擬環境以保持相依性整潔

只要上述條件皆已符合，我們就可以直接進入程式碼部分。

## 步驟 1：安裝並匯入 Aspose OCR 類別

首先，確保已安裝 Aspose OCR 套件，接著匯入我們需要的類別。

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**為什麼這很重要：** 只匯入必要的符號可以保持命名空間乾淨，並向直譯器表明我們實際使用的函式庫部分。這同時也能縮短後續程式碼行數，讓教學更易於跟隨。

> **小技巧：** 若你使用 Jupyter Notebook，請在安裝指令前加上 `!` 以在儲存格內執行。

## 步驟 2：建立 OCR 引擎並啟用深度學習模式

Aspose 提供多種引擎模式。對於大多數實務收據而言，深度學習模型提供最高的準確度，尤其在噪點較多的掃描圖像上。

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**為什麼選擇深度學習？** 傳統的規則式 OCR 在低對比或變形字元上容易失敗。深度學習模型以數百萬個字形訓練，對變化的適應性更佳——這正是你在 *perform OCR in Python* 時，使用手機相機拍攝的收據所需要的。

## 步驟 3：載入圖像以供 OCR 使用

現在我們真正 **load image for OCR**。Aspose.Imaging 支援 PNG、JPEG、BMP、TIFF 等多種格式，幾乎可以處理任何文件照片。

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**常見陷阱：** 忘記在引擎上設定圖像會導致執行時拋出 `NullReferenceException`。載入檔案後務必呼叫 `set_image`。

## 步驟 4：執行 OCR 並抽取文字

引擎已就緒且圖像已附加，我們終於可以 **perform OCR in Python**，並取得文字結果。

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

`recognize()` 方法會回傳一個 `OcrResult` 物件，裡面不只包含原始文字，還有信心分數、邊界框與語言資訊。對於快速的 **extract text from image** 用例，我們只需要 `get_text()`。

## 步驟 5：顯示辨識出的文字

讓我們看看引擎實際從收據讀取了什麼內容。

```python
print("Recognized text:\n", recognized_text)
```

典型的輸出會是：

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

如果輸出出現亂碼，請考慮在將圖像送入 OCR 引擎前先做前處理（例如提升對比或套用去斜角濾鏡）。Aspose.Imaging 提供完整的影像增強工具，可串接使用。

## 處理邊緣案例與提升準確度的技巧

### 1. 應對極度噪點的收據
若收據嚴重污損，可先切換至 `OcrEngineMode.HIGH_SPEED` 以快速（但較不精確）掃描，之後再對清理過的圖像使用 `DEEP_LEARNING` 進行第二輪辨識。

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. 指定語言
預設情況下 Aspose 會自動偵測語言。對於英文收據，你可以明確鎖定語言：

```python
ocr_engine.set_language("eng")
```

### 3. 記憶體管理
在迴圈中處理大量圖像時，請明確釋放資源：

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. 將 OCR 結果寫入檔案
有時需要將抽取的文字持久化以供後續分析。

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## 完整範例程式

以下是將所有步驟串接起來的完整腳本。將它貼到名為 `receipt_ocr.py` 的檔案中，調整圖像路徑後執行 `python receipt_ocr.py`。

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

執行腳本後，主控台會顯示收據內容，同時會產生 `receipt_output.txt`，內含相同資料。

![Python OCR tutorial – sample receipt output](https://example.com/receipt_output.png "python ocr tutorial example")

*圖片替代文字:* **python ocr tutorial – sample receipt output**

## 重點回顧與後續步驟

我們剛完成一個 **python ocr tutorial**，示範了如何 **load image for OCR**、**perform OCR in Python**，以及最終 **recognize text from receipt** 檔案，全部使用 Aspose。主要重點如下：

- 選擇合適的引擎模式（深度學習可提升準確度）
- 呼叫 `recognize()` 前務必先附加圖像
- 使用 `OcrResult` 物件取得乾淨文字，然後依需求儲存或進一步處理

接下來可以考慮串接 Aspose Imaging 濾鏡以改善低對比掃描，或將腳本整合到 Flask API，讓使用者可透過網頁表單上傳收據。亦可探索將 OCR 資料匯出為 CSV，以實作會計自動化。

對多頁 PDF 或非拉丁文字有疑問嗎？歡迎留言，我很樂意協助！

**準備好提升文件自動化層級了嗎？** 取得程式碼、嘗試不同圖像，讓 OCR 引擎幫你完成繁重工作。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}