---
category: general
date: 2026-03-26
description: 快速辨識圖像文字，學習如何載入圖像進行 OCR，並從特定區域提取資料。請跟隨此實作指南。
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: zh-hant
og_description: 在 Python 中透過載入圖像進行 OCR、設定感興趣區域，並擷取乾淨文字，來辨識圖像中的文字。了解完整工作流程。
og_title: 從圖像辨識文字 – 完整的 Python OCR 教學
tags:
- OCR
- Python
- Image Processing
title: 從圖像辨識文字 – 步驟式 Python OCR 教學
url: /zh-hant/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字 – 完整 Python OCR 教學

是否曾經需要 **從圖像辨識文字**，卻不知從何下手？也許你手上有掃描的表格、收據或螢幕截圖，只想取得特定框格內的文字。好消息是，只要幾行 Python 程式碼，就能載入圖像、聚焦單一區域，並抽取所需的文字——不必手動複製。

在本教學中，我們會一步步說明整個流程：載入圖像、定義感興趣區域（ROI）、執行 OCR 引擎、印出結果。完成後，你就能把這段程式碼嵌入任何需要從圖像特定部位抽取文字的專案。無需繁雜的影像處理管線，只要乾淨、易讀且即時可用的程式碼。

## 前置條件

- 已安裝 Python 3.8+  
- `ocr` 套件（或任何相容的 OCR 函式庫）— 使用 `pip install ocr-lib` 安裝（請以實際套件名稱取代）  
- 含有欲讀取表單的 PNG/JPEG 圖像檔  
- 具備基本的 Python 函式與類別概念  

如果你已經熟悉上述項目，太好了——可以直接跳過。否則，先喝杯咖啡，確保上述環境已就緒；之後的步驟會假設它們已經配置好。

## 步驟 1：建立 OCR 引擎實例 – 「從圖像辨識文字」核心

首先，我們需要一個能與 OCR 引擎溝通的物件。把它想像成大腦，之後會 **從圖像辨識文字**。

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **為什麼重要：** 只要初始化一次引擎，就能在多張圖像間重複使用設定（例如語言套件），提升效能並保持程式碼整潔。

## 步驟 2：載入圖像以供 OCR – 把圖片載入記憶體

接著，我們真正 **載入圖像以供 OCR**。函式庫提供便利的靜態方法，讀取檔案並回傳引擎可理解的物件。

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **小技巧：** 若圖像尺寸過大，考慮先縮小再載入。較小的圖像可加速 OCR，且對大多數印刷文字的準確度影響不大。

## 步驟 3：定義 OCR 感興趣區域（ROI）

通常你不需要整頁文字——只要使用者填寫的特定框格。定義 **OCR 感興趣區域** 可讓引擎忽略其他部分，減少雜訊並加快處理速度。

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **為什麼要聚焦 ROI？**  
> - **速度：** 引擎掃描的像素更少。  
> - **準確度：** ROI 之外的背景圖形可能干擾字元辨識。  
> - **簡潔性：** 直接取得與目標欄位完全對應的乾淨字串。

## 步驟 4：執行 OCR 程序 – 真正的關鍵時刻

所有設定完成後，我們終於在定義好的 ROI 內 **從圖像辨識文字**。

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

如果引擎支援多區域，`ocr_result` 會是一個列表；在單一 ROI 的情況下，它是一個具備 `get_text()` 方法的簡易物件。

## 步驟 5：抽取並印出文字 – 取得最終輸出

現在把結果物件中的純文字抽出並顯示。你可以將輸出寫入資料庫、CSV 檔，或交給後續的任何邏輯處理。

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**預期輸出**（以填寫姓名欄位為例）：

```
Text inside ROI:
 John Doe
```

若 OCR 引擎回傳多餘的空白或換行符號，可使用 `.strip()` 或正規表達式進行清理。

## 常見邊緣案例處理

| 情境                                   | 處理方式                                                                    |
|----------------------------------------|-----------------------------------------------------------------------------|
| **低解析度圖像**                       | 使用 `Pillow` 的 `Image.resize` 先放大再載入。                              |
| **文字傾斜或旋轉**                     | 套用旋轉校正，例如 `ocr.Imaging.Image.rotate`。                              |
| **多語言**                              | 在引擎上設定語言套件：`ocr_engine.set_language('eng+spa')`。                |
| **未定義 ROI**                         | 省略 `add_region_of_interest`，引擎會處理整張圖像。                         |
| **出現非預期字元（例如逗號）**         | 後處理字串：`extracted_text.replace(',', '')`。                            |

以上技巧可讓你的 **載入圖像以供 OCR** 流程在來源資料不完美時仍保持穩定。

## 完整範例 – 複製、貼上、執行

以下是可直接存成 `.py` 檔並執行的完整腳本，內含所有匯入、錯誤處理，以及驗證圖像是否存在的簡易輔助函式。

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

執行此腳本會印出 ROI 內清理過的字串，讓你得到即時可用的資料。

## 結論

現在你已掌握一套完整、端到端的 **從圖像辨識文字** 方法：先 **載入圖像以供 OCR**，再定義精確的 **OCR 感興趣區域**，最後抽取乾淨的文字。此流程適用於任何遵循上述模式的 Python OCR 函式庫，且可輕鬆擴充為多 ROI、不同語言或前處理步驟。

接下來，你可以探索：

- **OCR 前處理**（二值化、去噪）以提升噪聲掃描的辨識率。  
- 使用 **從 ROI 抽取文字** 的結果填入 pandas DataFrame，進行批次資料分析。  
- 當需要更高可靠性與規模時，改用雲端 OCR 服務（Google Vision、Azure Computer Vision）。

試著調整矩形座標以符合自己的表單，讓自動化為你工作。祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}