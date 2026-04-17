---
category: general
date: 2026-03-26
description: 學習如何在 Python 中旋轉圖像並執行 OCR。本指南亦示範如何為 OCR 預處理圖像，以及如何高效地從圖像中提取文字。
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: zh-hant
og_description: 如何正確旋轉圖像，然後使用 Aspose OCR 識別圖像中的文字。請跟隨本步驟教學，為 OCR 預處理圖像並提取圖像文字。
og_title: 如何旋轉圖像並執行 OCR – 完整 Python 指南
tags:
- Aspose
- Python
- Image Processing
- OCR
title: 如何在 Python 中使用 Aspose 旋轉圖像並執行 OCR
url: /zh-hant/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 在 Python 中旋轉圖像並執行 OCR

有沒有想過 **如何旋轉圖像** 讓 OCR 引擎真的能讀取文字？也許你掃描的表單被翻成側向，或是相機拍攝的畫面順時針旋轉了 90°。在人眼看來文字仍然正常，但 OCR 引擎卻會看到一團亂。好消息是，只要幾行 Python 程式碼與 Aspose 套件，就能輕鬆修正方向、裁切關注的區域，並抽取文字。

在本教學中，我們將完整示範工作流程：從載入已旋轉的 TIFF、校正方向、**為 OCR 前處理圖像**，最後**從圖像辨識文字**。完成後，你將了解**如何執行 OCR**，並能自信地**從圖像檔案抽取文字**。

## 您需要的條件

- Python 3.8+（任何近期版本皆可）
- 透過 `pip` 安裝 `asposeocrjava` 與 `asposeimaging` 套件
- 一張需要旋轉的範例圖像（例如 `rotated_form.tif`）
- 對影像處理有一點好奇心

不需要大型框架——只要兩個 Aspose 套件與少量 Python 邏輯即可。

---

## 步驟 1：安裝 Aspose 套件（如何執行 OCR）

在我們能**旋轉圖像**或**從圖像辨識文字**之前，需要先安裝能完成這些工作的函式庫。

```bash
pip install asposeocrjava asposeimaging
```

> **小技巧：** 若你身處公司代理伺服器後方，請在指令後加入 `--proxy http://proxy:port`。這些套件是 Aspose .NET/Java 核心的純 Python 包裝器，安裝通常即時完成。

---

## 步驟 2：載入來源檔案並旋轉——核心「**如何旋轉圖像**」步驟

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **為什麼要旋轉？** 大多數 OCR 引擎假設文字由左至右、由上至下排列。若位圖側向，引擎會回傳亂碼或根本沒有結果。旋轉可將像素格對齊預期的閱讀順序，顯著提升準確度。

> **邊緣情況：** 若不確定圖像需要 90°、180° 或 270° 旋轉，可檢查 `source_image.width` 與 `source_image.height`，或使用 `exif` 方向標籤。Aspose 的 `rotate_flip` 方法亦支援 `ROTATE_180` 與 `ROTATE_270_CLOCKWISE`。

> **圖像預覽（可選）：**  
> ![如何旋轉圖像示例](/assets/rotate-demo.png "如何旋轉圖像 – 旋轉前後比較")

---

## 步驟 3：裁切感興趣區域——**為 OCR 前處理圖像**

通常只需要頁面中的小區塊，例如簽名欄位或一串數字。裁切可去除雜訊並加速**如何執行 OCR**。

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **為什麼要裁切？** 縮小圖像尺寸會限制 OCR 引擎的搜尋空間，減少偽陽性並縮短處理時間。若來源檔案含有浮水印或其他圖形，裁切也能避免引擎被干擾。

> **提示：** 若需處理多個欄位，可使用不同的矩形重複裁切步驟，並分別對每個區塊執行 OCR。

---

## 步驟 4：初始化 OCR 引擎——「**如何執行 OCR**」核心

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **背後原理：** Aspose OCR 結合 Tesseract 與專有影像分析。一次實例化引擎並在多張圖像間重複使用，比每次都建立新物件更有效率。

---

## 步驟 5：將裁切後的圖像送入並辨識文字——**如何從圖像抽取文字**

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### 預期輸出

若 ROI 包含文字「Invoice #12345 – Paid」，你會看到類似以下結果：

```
Invoice #12345 – Paid
```

若 OCR 表現不佳，可能會出現多餘空格或錯讀字元（例如「Invo1ce #I2345 – Pa1d」）。這時就需要**為 OCR 前處理圖像**的技巧——如調整對比或套用二值化。Aspose 亦提供可在第 5 步前串接的額外濾鏡，但上述基本流程已能處理大多數乾淨掃描。

---

## 步驟 6：可選——微調 OCR 設定（進階「**如何執行 OCR**」）

若需針對特定語言提升準確度，或想忽略某些字元，可調整引擎設定：

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **使用時機：** 當文件中包含大量你不在意的裝飾符號時，使用黑名單可減少誤偵測。

---

## 完整端對端腳本

將所有步驟整合，以下是一個可直接執行的腳本，能**旋轉圖像**、**為 OCR 前處理圖像**，最後**從圖像辨識文字**：

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

執行此腳本會將辨識出的文字印到主控台，並將處理後的 ROI 以 `processed_roi.png` 儲存。你可以開啟該 PNG 以驗證旋轉與裁切是否如預期。

---

## 常見問題與注意事項

| 問題 | 解答 |
|----------|--------|
| **如果圖像已經是正立的該怎麼辦？** | 旋轉步驟是冪等的——若對已正立的圖像再旋轉 90° 會破壞方向，因此在呼叫 `rotate_flip` 前，應先檢查 `source_image.width` 與 `height`，或使用 EXIF 方向資訊。 |
| **我的 OCR 輸出出現多餘的換行。** | 使用 `result.get_text().replace("\n", " ").strip()` 進行清理，或啟用 `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`。 |
| **可以直接處理 PDF 嗎？** | 可以——Aspose Imaging 能將 PDF 頁面載入為圖像 (`Image.load("file.pdf")`)，之後即可套用相同的旋轉與 OCR 步驟。 |
| **有沒有辦法批次處理大量檔案？** | 將 `ocr_rotated_image` 包在目錄迴圈中，或使用 Python 的 `concurrent.futures` 進行平行化。 |
| **如何處理非英文語言？** | 透過 `ocr_engine.get_recognition_settings().set_recognition_language("fr")` 設定法語，其他語言同理。 |

---

## 結論

我們已完整說明**如何正確旋轉圖像**、**如何透過裁切為 OCR 前處理圖像**，以及**如何執行 OCR**以**辨識圖像文字**並**從圖像抽取文字**，全部使用 Aspose 的 Python 函式庫。完整腳本展示了一個實務、可投入生產環境的工作流程，能直接嵌入任何自動化管線。

若想更進一步，可嘗試：

- **影像增強**（對比、二值化）於 OCR 前
- **多 ROI 抽取**，處理含多欄位的表單
- **批次處理** 整個資料夾的掃描文件
- **與下游系統整合**（例如將抽取的資料寫入資料庫）

歡迎依需求自行調整程式碼，祝開發順利！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}