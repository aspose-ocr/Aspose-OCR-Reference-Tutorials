---
category: general
date: 2026-07-05
description: 快速校正圖像傾斜。學習為 OCR 預處理圖像、校正圖像旋轉，並使用 Python 將掃描轉換為文字。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: zh-hant
og_description: 如何校正影像傾斜並進行 OCR 前處理。本指南示範如何校正影像旋轉，並使用 Python 從影像中擷取文字。
og_title: 如何校正圖像傾斜 – 步驟式 OCR 前處理
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: 如何校正影像傾斜 – OCR 前處理完整指南
url: /zh-hant/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – OCR 前處理完整指南

有沒有想過 **如何校正影像傾斜** 的檔案，看起來好像是從歪斜的掃描器拍出來的？你並不是唯一有此疑問的人。在許多實務專案中，於能夠 **從影像中擷取文字** 之前，首先必須先把那個傾斜校正過來。  

在本教學中，我們將逐步示範一個實作、端對端的範例，**為 OCR 前處理影像**、校正旋轉，最後使用 Python OCR 函式庫 **將掃描檔轉換為文字**。不會有模糊的說明，僅提供可直接複製貼上的可執行腳本，並附上常見陷阱的提示。  

## 您將達成的目標

* 載入任何稍微傾斜的掃描 JPEG 或 PNG 檔案。  
* 套用校正傾斜濾鏡與二值化步驟，以提升 OCR 準確度。  
* 執行 OCR 引擎，可靠地 **從影像中擷取文字**。  
* 了解為何 **正確影像旋轉** 對後續文字擷取至關重要。  

### 前置條件

* 在機器上已安裝 Python 3.9 以上版本。  
* 可透過 pip 安裝的 OCR 套件，模仿範例中使用的 `ocr` 命名空間（例如，Tesseract 的輕量封裝）。  
* 具備 Python 函式與影像處理概念的基本認識。  

如果你已具備上述條件，讓我們開始吧。

![how to deskew image example](deskew_before_after.png){alt="如何校正影像傾斜 – 校正前後比較"}

## 步驟 1：設定 OCR 引擎 – 使用 Python 校正影像傾斜

首先，你需要一個能夠理解文件語言的 OCR 引擎。以下程式碼片段展示了建立引擎的最小樣板，並告訴它你正在處理英文文本。

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*為何此步驟重要：* 引擎的語言設定會影響其使用的字元集與字典。若省略此步驟，OCR 可能會誤判常見詞彙，尤其在你 **校正影像旋轉** 後。

## 步驟 2：載入欲校正的掃描影像

現在我們將檔案載入記憶體。請將 `"YOUR_DIRECTORY/skewed_scan.jpg"` 替換為你自己的影像路徑。

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

如果影像已經是 NumPy 陣列或 OpenCV `Mat`，你可以相應地調整載入方式——關鍵是該物件必須具備稍後使用的 `apply_filter` 方法。

## 步驟 3：為 OCR 前處理影像 – 校正傾斜與二值化

這裡就是魔法發生的地方。我們串接兩個濾鏡：

1. **校正傾斜** – 自動偵測主要文字基線，將影像旋轉回水平。  
2. **二值化（Otsu）** – 將圖片轉為純黑白，顯著提升辨識率。  

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*小技巧：* 若二值化後文字仍顯得模糊，可嘗試調整對比度或使用其他閾值方法。`ocr.Filter` 模組通常提供 `adaptive_threshold()` 以應對較困難的情況。

## 步驟 4：執行 OCR – 從影像中擷取文字

使用乾淨且已校正的畫布，我們將影像交給引擎。結果物件包含辨識出的字串、信心分數，甚至在需要時的邊框資訊。

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

典型的輸出如下：

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

有沒有注意到換行位置完美對齊？這正是 **正確影像旋轉** 的好處——OCR 不再需要猜測行的方向。

## 步驟 5：整合全部 – 單一檔案腳本將掃描轉為文字

以下是完整、可執行的腳本，結合了我們討論的所有步驟。將其儲存為 `deskew_ocr.py`，然後執行 `python deskew_ocr.py`。

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### 為何這樣有效

* **先校正傾斜** – 在二值化之前旋轉影像，確保閾值演算法在水平的基礎上運作。  
* **在校正傾斜之後再二值化** – Otsu 方法假設直方圖為雙峰；傾斜的頁面會破壞此假設。  
* **英文語言模型** – 告訴 OCR 預期的字元，減少偽陽性。  

如果需要處理其他語言，只需將 `ocr.Language.ENGLISH` 替換為相應的列舉值即可。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *如果掃描件是顛倒的呢？* | `deskew()` 濾鏡通常也能偵測 180° 旋轉。如果失敗，請在校正傾斜前呼叫 `apply_filter(ocr.Filter.rotate(180))`。 |
| *我的文件有彩色圖形 – 二值化會把它們抹掉嗎？* | 會。對於混合內容，考慮僅使用 `ocr.Filter.deskew()`，然後在彩色影像上執行 OCR。仍可在保留圖形的同時擷取文字。 |
| *我可以一次處理多個檔案嗎？* | 將邏輯包在迴圈中，從清單讀取每個檔案路徑，並將每個 `result.text` 存入獨立的 `.txt` 檔案。 |
| *如何提升低解析度掃描的準確度？* | 在校正傾斜 **之前** 使用雙三次濾鏡將影像放大，然後套用銳化濾鏡。更多像素可為 OCR 引擎提供更好的資訊。 |

## 加分項：校正傾斜的視覺驗證

如果想要並排觀看校正前後的效果，可加入簡短的 Matplotlib 程式碼片段：

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## 結論

我們已說明了 **如何校正影像傾斜**、為何 **為 OCR 前處理影像** 至關重要，以及如何 **從影像中擷取文字**，最終 **將掃描轉為文字**。這個工作流程——載入 → 校正傾斜 → 二值化 → 辨識——確保 OCR 看到的是乾淨、平直的頁面，從而提升準確度並減少人工校正。

接下來的 OCR 之路該怎麼走？不妨嘗試以下方向：

- 不同語言套件（`ocr.Language.FRENCH` 等）。
- 加入版面分析步驟，以偵測欄位或表格。
- 使用 PDF 函式庫將 OCR 結果匯出為可搜尋的 PDF。

如果遇到問題，歡迎留言，或分享你處理特別頑固掃描的自訂技巧。祝程式開發愉快，願你的影像永遠保持完美水平！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本篇示範的技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}