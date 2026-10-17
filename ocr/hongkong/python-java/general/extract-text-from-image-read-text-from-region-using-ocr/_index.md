---
category: general
date: 2026-07-05
description: 使用 Python OCR 從圖像提取文字。了解如何載入圖像進行 OCR、從區域讀取文字，以及用幾行程式碼從發票中提取文字。
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: zh-hant
og_description: 使用 Python OCR 從圖像提取文字。此指南展示如何載入圖像進行 OCR、從區域讀取文字，以及快速從發票中提取文字。
og_title: 從圖像提取文字 – 使用 OCR 從區域讀取文字
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 從圖像提取文字 – 使用 OCR 從區域讀取文字
url: /zh-hant/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 – 使用 OCR 從區域讀取文字

是否曾需要**從圖像提取文字**，但只關注特定部份——例如發票上的總金額？你並非唯一有此需求的人。在許多實務專案中，你會發現自己需要**從區域讀取文字**，而不是解析整張圖片。幸好，只要幾行 Python 程式碼，就能載入圖像以供 OCR、定義感興趣區域（ROI），並精確擷取所需的字元。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明如何**載入圖像以供 OCR**、設定 ROI，最後**從發票提取文字**。完成後，你將擁有一段即插即用的程式碼，可與任何支援區域辨識的主流 OCR 函式庫搭配使用。

---

## 需要的條件

- Python 3.8+（此程式碼亦相容於 3.10）  
- 一個提供 `OcrEngine` 類別的 OCR 套件（示範中我們使用虛構的 `ocr` 模組；請改為 `pytesseract`、`easyocr`，或任何支援 ROI 的函式庫）  
- 範例圖像，例如 `invoice.png`，內含清晰的印刷文字  
- 基本了解 Python 函式與類別（不需要深度學習背景）

如果你已具備上述條件，太好了——讓我們開始吧。若尚未安裝，請從 python.org 下載最新的 Python，並使用 `pip install your-ocr-lib` 安裝 OCR 套件。

![從圖像提取文字範例](extract-text-from-image.png "從圖像提取文字 – 基於區域的 OCR 示範")

*上圖說明了我們將針對的區域（紅色矩形），以**從圖像提取文字**。*

## 步驟 1：安裝並匯入 OCR 函式庫

首先，確保你的環境中已安裝 OCR 函式庫。以下的匯入方式適用於大多數提供高階 `OcrEngine` 類別的套件。

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **小技巧：** 若使用 `pytesseract`，需另行安裝 Tesseract 可執行檔，並將 `pytesseract.pytesseract.tesseract_cmd` 設為其路徑。

## 步驟 2：建立 OCR 引擎並設定語言

建立引擎相當簡單，但指定語言能顯著提升準確度，尤其是包含數字與英文單詞的發票。

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

為什麼要這麼做？OCR 引擎會使用語言模型來預測字元；告訴它預期使用英文可減少誤判，例如把「0」誤讀為「O」。

## 步驟 3：載入圖像以供 OCR

現在我們真正**載入圖像以供 OCR**。大多數函式庫接受檔案路徑或 Pillow 圖像物件。此處為了簡化，我們使用函式庫內建的載入器。

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

請確認路徑指向正確的目錄；常見錯誤是腳本在不同工作目錄執行時忘記使用相對路徑。

## 步驟 4：定義感興趣區域 (ROI)

定義 ROI 是**從區域讀取文字**的核心。可以把它想像成在發票中包含總金額的部份畫一個矩形。

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` 與 `top` 代表矩形左上角的 X 與 Y 座標。  
- `width` 與 `height` 設定框的寬度與高度。  
- 你可以使用能顯示像素座標的圖像檢視器，嘗試不同的數值。

> **為何 ROI 重要：** 在整頁執行 OCR 會浪費 CPU 時間，且常因無關的文字、表格或圖形產生噪聲。聚焦於特定區域可得到更乾淨的結果，且處理速度更快。

## 步驟 5：對指定區域執行 OCR

所有設定完成後，我們終於**從圖像提取文字**——但僅限於先前定義的 ROI 內。

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` 方法會回傳一個物件，通常包含原始字串、信心分數，有時還會有每個單字的邊界框。對於本範例，我們只需要純文字。

## 步驟 6：輸出擷取的文字

讓我們印出結果，看看得到什麼。此步驟示範了在實務情境中**從發票提取文字**。

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### 預期輸出

```
Text inside ROI:
Total Amount: $1,245.67
```

如果你的發票版面不同，將會看到矩形內的任何文字——可能是發票號碼、日期，或採購單編號。

## 步驟 7：將整個流程封裝成可重複使用的函式（可選）

為了讓此解決方案能在多張發票間重複使用，將邏輯封裝成函式。這同時示範了**區域 OCR**作為通用工具的用法。

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

現在你可以使用任意發票呼叫此函式：

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## 常見問題與避免方法

| 問題 | 發生原因 | 解決方式 |
|------|----------|----------|
| **空白輸出** | ROI 並未實際覆蓋任何文字（座標錯誤）。 | 使用影像編輯器再次確認像素值；加入視覺除錯覆層。 |
| **雜訊字元** | 圖像解析度低或對比度差。 | 先前處理圖像：轉為灰階，套用閾值 (`cv2.threshold`)。 |
| **語言設定錯誤** | 引擎預設語言不包含所需字元集。 | 明確將 `ocr_engine.language` 設為 `ENGLISH` 或相應的語系。 |
| **效能延遲** | 重複對大型圖像執行 OCR。 | 載入前先縮放圖像，或先裁切出 ROI 再進行處理。 |

## 擴充範例：多個 ROI

有時發票包含多個欄位需要擷取——例如同時**從發票提取文字**的總金額與發票日期。你可以對矩形清單進行迴圈：

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

此模式讓程式碼保持整潔，且日後可輕鬆加入更多區域。

## 結論

我們剛剛完整說明了使用 Python OCR **從圖像提取文字**的端對端工作流程，重點放在特定區域。透過**載入圖像以供 OCR**、定義**感興趣區域**，並呼叫引擎，你即可可靠地**從區域讀取文字**——非常適合從發票中抽取總金額、從收據中取得日期，或任何其他局部資料。  

歡迎自行實驗


## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從圖像提取文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [從圖像提取文字 – 使用 Aspose.OCR 於 .NET 的 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [如何透過在 OCR 中準備矩形來提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}