---
category: general
date: 2026-06-22
description: 只需幾行 Python 程式碼，即可對圖像執行 OCR。了解如何載入 OCR 圖片、從 PNG 識別文字，以及高效使用 OCR 引擎。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: zh-hant
og_description: 使用 Python 快速執行影像 OCR。本教學示範如何載入影像進行 OCR、從 PNG 辨識文字，以及使用具信心度的 OCR 引擎。
og_title: 在 Python 中對圖片執行 OCR – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中對圖像執行 OCR – 完整指南
url: /zh-hant/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 執行影像 OCR – 完整指南

是否曾經需要 **perform OCR on image** 檔案，但在第一行程式碼就卡住了？你並不孤單。在本教學中，我們將完整示範如何 **load image for OCR**、設定輕量級的 **OCR engine**，最後只用幾個指令就 **recognize text from PNG**。

我們會從安裝函式庫說明到微調 whitelist，使只有數字與大寫字母會被辨識。完成後，你將擁有一個可直接執行的腳本，隨時可放入任何專案——沒有神祕、沒有額外贅述。

## 你將學會

- 如何在 Python 中以程式方式 **use OCR engine**。  
- 從本機資料夾 **load image for OCR** 的完整步驟。  
- 為何以及如何將辨識限制於自訂字元集。  
- 如何 **recognize text from PNG** 並安全處理結果。  

**Prerequisites:** 已安裝 Python 3.7+、熟悉的終端機，以及想要讀取的影像（例如 `serial-number.png`）。不需要先前的 OCR 經驗。

---

## 執行影像 OCR – 初始化 OCR Engine

首先，你需要建立 OCR engine 的實例。可以把 engine 想像成會分析像素並轉換成字元的大腦。

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* 若沒有 engine，影像就無法被處理。`OcrEngine` 類別將所有繁重的工作——前處理、分割與字元分類——封裝成可重複使用的單一物件。

---

## 載入影像以進行 OCR – 提供 PNG 檔案

既然 engine 已建立，你需要將想要讀取的圖片提供給它。函式庫需要一個 `ImageStream` 物件，你可以直接從檔案路徑建立。

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* 請使用高對比度的影像（黑字白底），並避免壓縮產生的雜訊；這些會干擾 OCR 演算法。

---

## 限制字元 – Whitelist 數字與大寫字母

通常你只在意特定子集的字元，例如只包含 A‑Z 與 0‑9 的序號。設定 whitelist 後，engine 會忽略其他字元，從而大幅提升辨識準確度。

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* engine 會建立一個過濾器，在最終分類階段之前剔除不在 whitelist 中的字形。當影像含有雜訊或不需要的裝飾文字時，這特別有用。

---

## 從 PNG 辨識文字 – 執行 OCR 流程

在 engine 已就緒且影像已載入後，你終於可以 **perform OCR on image**。呼叫 `recognize()` 會執行完整流程，並回傳結果物件。

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

如果你關心效能，這個方法在現代筆記型電腦上處理 300 × 200 px 的 PNG 通常只需數百毫秒即可完成。

---

## 輸出與驗證 – 取得辨識文字

最後一步是從結果物件中提取純文字。任何未符合 whitelist 的字元都會自動被剔除，讓你得到乾淨的字串，可供後續處理。

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5`（假設影像中確實包含此序號）。  

如果輸出為空或雜亂，請再次檢查影像品質與 whitelist；常見的錯誤是不小心遺漏了必要的字元。

---

## 邊緣案例與常見陷阱

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **File not found** | 路徑拼寫錯誤或檔案遺失 | 在呼叫 `set_image` 前使用 `os.path.abspath` 來驗證完整路徑。 |
| **Low contrast image** | 文字與背景融合 | 在將影像提供給 engine 前，先套用簡單的閾值處理（`Pillow` 或 `OpenCV`）。 |
| **Unexpected characters** | Whitelist 設定過於嚴格 | 將缺少的字元加入 whitelist 字串中。 |
| **Large images** | 辨識速度緩慢 | 將影像寬度調整至最高 1024 px；OCR 品質通常仍保持良好。 |

---

## 完整腳本 – 可直接執行

以下是完整且獨立的腳本，將所有步驟串接起來。將其存為 `ocr_demo.py`，將 `YOUR_DIRECTORY` 替換為實際資料夾路徑，然後執行 `python ocr_demo.py`。

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output*（當 PNG 包含 `SN12345` 時）：

```
Recognized text: SN12345
```

---

## 結論

現在你已掌握在 Python 中 **perform OCR on image** 檔案的完整流程，從 **loading image for OCR** 到 **recognize text from PNG**，最後使用可自訂的 **OCR engine** 取得乾淨的結果。此方法簡單、可擴充，且能即時處理大多數序號類型的掃描。

接下來可以嘗試將 whitelist 換成小寫字母、實驗不同的影像格式（JPEG、BMP），或將腳本整合至批次處理流程。相同的模式——engine → image → settings → recognize → output——幾乎適用於所有 OCR 任務。

有任何問題或遇到奇怪的影像無法辨識？歡迎在下方留言，祝 coding 愉快！ 

![說明使用 Python 執行影像 OCR 步驟的圖示](https://example.com/ocr-flow.png "顯示如何使用 Python OCR 引擎執行影像 OCR 的圖示")

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，進一步延伸所示技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [將影像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何使用 AspOCR：為 .NET 預處理影像 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [如何透過準備矩形於 OCR 中擷取影像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}