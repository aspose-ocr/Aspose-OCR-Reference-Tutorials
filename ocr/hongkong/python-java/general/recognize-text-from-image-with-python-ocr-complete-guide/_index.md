---
category: general
date: 2026-06-16
description: 使用 Python OCR 引擎從圖像辨識文字 – 學習如何從收據中提取文字，並在數分鐘內提升 OCR 準確度。
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: zh-hant
og_description: 快速辨識圖片文字。此指南展示如何從收據中提取文字，並使用 Python 提升 OCR 準確度。
og_title: 使用 Python OCR 從圖像辨識文字 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 使用 Python OCR 從圖像識別文字 – 完整指南
url: /zh-hant/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 從圖像辨識文字 – 完整指南

是否曾需要 **從圖像辨識文字**，卻發現結果像是亂碼？你並非唯一遇到這種情況的人。在許多小型企業的情境中——例如掃描收據、數位化發票，或從身分證上擷取資料——取得乾淨、可靠的輸出往往是流程順暢與頭痛不已的分水嶺。

在本教學中，我們將一步步示範如何使用輕量級的 Python OCR 函式庫 **從圖像辨識文字**。同時，我們也會說明如何 **從收據中擷取文字**，並分享在不購買昂貴軟體的前提下提升 OCR 準確度的技巧。準備好了嗎？讓我們開始吧。

## 你將會建立什麼

完成本指南後，你將擁有一個可直接執行的腳本，具備以下功能：

1. 初始化 OCR 引擎。  
2. 啟用智慧前處理（去斜、去斑點、二值化）。  
3. 載入雜訊較多的收據圖像。  
4. 自動執行辨識流程。  
5. 將乾淨、可搜尋的文字輸出至主控台。

全程不依賴外部服務、也不需要隱藏的 API 金鑰——只有純粹的 Python 程式碼，你可以自行套用到任何專案。

### 前置條件

- 已在機器上安裝 Python 3.8+。  
- 具備基本的 pip 與虛擬環境使用經驗。  
- 準備一張欲處理的收據樣本圖像（JPEG 或 PNG）。  
- `ocr` 套件（範例使用虛構的 `ocr` 模組作說明；實際可改用 `pytesseract`、`easyocr` 或任何提供相似 API 的函式庫）。

> **專業小技巧：** 若遇到缺少相依套件的情況，可先執行 `pip install ocr`（或實際套件名稱）再繼續。

## 步驟 1 – 從圖像辨識文字：設定引擎

首先，我們需要一個能讀取像素資料並轉換成字元的物件。把引擎想像成整個流程的大腦，其他所有步驟都會把資訊傳遞給它。

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

為什麼要手動建立引擎？有些函式庫只要呼叫單一函式即可，但明確的實例讓你能細部控制前處理——這正是之後 **提升 OCR 準確度** 所必須的。

## 步驟 2 – 從收據中擷取文字：啟用前處理

使用手機相機掃描的收據很少是完美的。可能會稍微傾斜、沾有塵點，或因光線不均而失真。啟用前處理會在引擎檢視文字前先完成繁重的工作。

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*去斜* 會校正頁面角度，*去斑點* 會抹除雜散的斑點，*二值化* 則把每個像素強制為黑或白。僅這三個旗標就能在雜訊收據上 **提升 OCR 準確度** 20‑30 %。

## 步驟 3 – 載入欲辨識的圖像

現在把引擎指向實際的檔案。路徑可以是絕對或相對，只要確保圖像檔案真的存在即可。

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

如果你在想引擎是否支援 PDF 或多頁 TIFF，現代的大多數函式庫都有支援——只要查閱文件即可。對於單頁 JPEG，上述程式碼已足夠。

## 步驟 4 – 執行 OCR – 引擎完成其餘工作

前處理設定完成且圖像已載入後，下一行程式碼會一次完成所有工作：執行前處理、跑辨識演算法，最後回傳結果物件。

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

在幕後，引擎可能使用 Tesseract、神經網路，或是專有的辨識引擎。你不需要了解內部細節，只要取得乾淨的結果即可。

## 步驟 5 – 輸出辨識出的文字

最後，我們從結果物件中取出純文字並印出。在真實應用中，你可以把它寫入資料庫、CSV 檔，甚至傳給後續的分析管線。

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### 預期輸出

在一般超市收據上執行腳本，會得到類似以下的結果：

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

如果輸出看起來是亂碼，請再次確認前處理旗標已開啟，且圖像沒有過暗。微調二值化門檻值（部分函式庫允許自行設定）可以進一步 **提升 OCR 準確度**。

## 進階：微調以更快擷取收據文字

雖然五步流程已能應付大多數情況，但若你需要在每晚處理上百張收據，或許想要加速。以下提供兩個可選的優化方式：

### H3 – 裁切至收據區域

如果圖像中包含大量背景（例如桌面照片），先將收據區域裁切：

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – 使用自訂語言套件

若收據內含外語字元（例如 “€” 或 “¥”），請載入對應的語言資料：

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

以上兩招可讓引擎 **從圖像辨識文字** 時更加可靠，特別是來源素材多變的情況下。

## 常見陷阱與避免方法

- **缺少字型**：部分 OCR 引擎需要特定收據字型的字型檔。請安裝相應的語言套件。  
- **噪點過多**：即使開啟 `despeckle=True`，極度顆粒化的掃描仍可能讓引擎困惑。可使用 Pillow 的手動濾鏡 (`Image.filter(ImageFilter.MedianFilter)`) 進行處理。  
- **DPI 不正確**：OCR 引擎預設約 300 dpi。若圖像解析度較低，請先將其放大：`engine.image = engine.image.resize((width*2, height*2))`。

直接解決這些問題即可 **提升 OCR 準確度**，而不必依賴昂貴的第三方服務。

## 完整腳本 – 可直接執行

以下提供完整、可執行的 Python 程式，已整合本文所有步驟。將檔案存為 `receipt_ocr.py`，然後執行 `python receipt_ocr.py`。

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

執行此腳本即可 **從圖像辨識文字**，並在主控台印出格式化的收據資料。你可以自行調整裁切座標、語言設定或前處理旗標，以符合自家收據版型。

## 結論

我們剛剛示範了一種使用 Python **從圖像辨識文字** 的簡易方法，說明了如何 **從收據中擷取文字**，並分享了多項實用技巧以 **提升 OCR 準確度**。核心概念很簡單：建立 OCR 引擎、啟用智慧前處理、提供乾淨的圖像，讓函式庫自行完成繁重的辨識工作。

接下來的步驟是什麼？可以嘗試將多張收據放入迴圈處理、將每筆結果寫入 CSV，或把輸出串接至會計系統。你也可以實驗 `easyocr` 等深度學習型 OCR 函式庫，以在複雜字型上取得更高的準確率。

對特定收據格式有疑問，或想了解如何處理多頁 PDF？歡迎在下方留言，祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能進一步擴展你的能力。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}