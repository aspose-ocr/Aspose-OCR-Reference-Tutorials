---
category: general
date: 2026-03-26
description: 建立 ROI 多邊形以在選定區域執行 OCR。了解如何定義多個區域、註冊它們，並使用 Python OCR 引擎提取文字。
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: zh-hant
og_description: 使用 Python 引擎建立 ROI 多邊形並對選取區域執行 OCR。完整程式碼、說明與技巧一應俱全。
og_title: 建立 ROI 多邊形 – 在選取區域快速 OCR
tags:
- OCR
- Python
- Image Processing
title: 建立 ROI 多邊形 – 選取區域 OCR 逐步指南
url: /zh-hant/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 ROI 多邊形 – 完整教學：對選取區域執行 OCR

是否曾需要 **create ROI polygon** 以便只對影像中重要的部分執行 OCR？也許你在掃描收據時只在乎總金額，或是表單中只需要讀取簽名欄位。在這些情況下，**ocr on selected area** 可以節省時間並提升準確度。  

在本指南中，我們將逐步說明所有必備步驟：從定義兩個多邊形、向 OCR 引擎註冊它們，到一次呼叫即可取得辨識文字。完成後，你將擁有可直接執行的腳本，並深入了解聚焦於感興趣區域的重要性。

## 你將學會

- 如何使用一般的 OCR 函式庫 **create ROI polygon** 物件。
- 定義單一區域與多個區域的差異。
- 如何將這些區域註冊到引擎，以執行 `ocr on selected area`。
- 預期輸出以及如何排除常見問題（例如 ROI 重疊、結果為空）。

### 前置條件

- 已安裝 Python 3.8 以上版本。
- 具備提供 `Polygon`、`Point` 與 `add_region_of_interest` 方法的 OCR 函式庫（範例使用虛構的 `ocr` 模組；請改用實際的 SDK，例如 Tesseract‑Python 包裝或 EasyOCR）。
- 一張樣本影像檔 (`sample.png`)，其中包含下列座標所指的文字。

> **Pro tip:** 若使用真實函式庫，請確保影像載入時使用相同的座標系統（原點在左上角，X 向右遞增，Y 向下遞增）。  

---  

## 步驟 1：匯入 OCR 模組並載入影像  

首先，將 OCR 套件匯入程式範圍，並讀取欲處理的影像。  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Why this matters:* 引擎在你附加任何 **ROI polygon** 前，需要先取得影像資料。有些函式庫允許稍後再傳入影像，但提前初始化可讓工作流程更整潔。

## 步驟 2：定義第一個 ROI 多邊形  

現在我們建立第一個感興趣區域。可以把它想像成在表格標題周圍畫一個矩形。  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explanation:*  
- `ocr.Point(x, y)` 使用像素座標。  
- 點的列表須按順時針排序，這是大多數引擎的預期格式。  
- 你可以加入任意多的點以形成不規則形狀；矩形只是其中一種特殊情況。

## 步驟 3：定義其他 ROI 多邊形（可選）

你不必只停在一個。以下是第二個多邊形，用於捕捉頁面下方的簽名欄位。  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Why add more?* 為多個區域執行 **ocr on selected area**，可在一次處理中抽取不同的資料片段，速度遠快於逐一裁切並分別處理每個切片。

## 步驟 4：向 OCR 引擎註冊 ROI  

多邊形準備好後，告訴引擎要檢查哪些區域。  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Important note:* 某些 SDK 需要在新增新區域前呼叫 `clear_regions()` 方法，特別是當你重複使用同一個引擎處理不同影像時。

## 步驟 5：執行 OCR 並取得文字  

最後，觸發辨識。引擎只會檢查我們剛剛加入的多邊形內部。  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Expected output**（假設 `sample.png` 在第一個 ROI 內含有文字 “Invoice Total: $123.45”，在第二個 ROI 內含有 “Signature: John Doe”）：

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

如果輸出為空，請再次確認座標確實與文字相交，且影像解析度與座標系統相符。

## 邊緣情況與常見陷阱  

| 情況                               | 需留意的地方                               | 修正／解決方法                              |
|-----------------------------------|--------------------------------------------|---------------------------------------------|
| **重疊的 ROI**                    | 文字可能會被返回兩次。                     | 保持多邊形不重疊或對輸出去重。 |
| **ROI 超出影像範圍**           | 引擎可能拋出錯誤或什麼也不返回。          | 將座標限制在 `0 ≤ x < width`、`0 ≤ y < height` 之間。 |
| **ROI 太小**                     | 因像素不足導致 OCR 準確度下降。            | 將多邊形擴大幾個像素或先將影像放大。 |
| **非矩形形狀**               | 部分引擎僅支援凸多邊形。                    | 將複雜形狀拆分為多個凸多邊形 ROI。 |
| **影像尺寸變化**                | 硬編碼的座標會失效。                       | 根據影像尺寸（例如百分比）計算 ROI 座標。 |

## 完整範例程式  

以下是完整腳本，你可以直接複製貼上並執行（請將 `ocr` 替換為實際使用的函式庫）。  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

使用 `python ocr_roi_example.py` 執行，應會看到兩個定義區域中抽取出的字串。

## 後續步驟  

- **Dynamic ROI generation:** 取代硬編碼座標，使用影像處理（例如 OpenCV 輪廓偵測）自動定位表格或欄位。  
- **Post‑processing:** 去除空白、套用正規表達式，或將數字轉換為正確的資料型別。  
- **Batch processing:** 迴圈處理資料夾內的多張影像，若版面一致可重複使用相同的 ROI 定義。  

如果你對更複雜文件的 **ocr on selected area** 感興趣——例如多頁 PDF 或掃描表單——可探索支援逐頁 ROI 註冊的函式庫。

---  

### 視覺概覽  

![示意圖：樣本影像上的兩個 ROI 多邊形](roi_diagram.png){alt="建立 ROI 多邊形範例，顯示兩個選取區域"}

---  

## 結論  

我們剛剛 **created ROI polygon** 物件，將它們註冊到 OCR 引擎，並在乾淨且可重現的腳本中執行 `ocr on selected area`。透過限制引擎只處理你關心的區域，可縮短處理時間、提升準確度，並讓後續資料處理變得更簡單。  

試著使用自己的影像來操作——調整座標、加入更多多邊形，或將輸出連接至資料庫。掌握基於區域的 OCR 後，應用的可能性無限。  

有任何問題或想分享有趣的使用案例嗎？在下方留言，祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}