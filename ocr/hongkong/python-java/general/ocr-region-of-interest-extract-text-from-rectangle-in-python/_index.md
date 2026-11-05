---
category: general
date: 2026-05-31
description: 使用 OCR 感興趣區域載入影像，從矩形中擷取文字，完美適用於辨識發票金額。
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: zh-hant
og_description: 精通 OCR 感興趣區域，載入影像進行 OCR，從矩形提取文字，並在單一教學中辨識發票文字。
og_title: OCR 感興趣區域 – 逐步 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR 感興趣區域 – 在 Python 中從矩形提取文字
url: /zh-hant/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – 在 Python 中從矩形提取文字

有沒有想過如何 **ocr region of interest** 掃描發票的特定部份，而不必把整頁送入引擎？你不是第一個盯著模糊收據想著「要怎樣提取位於右下角的金額？」的人。好消息是，你可以告訴 OCR 函式庫精確的搜尋位置，從而大幅提升速度與準確度。

在本指南中，我們將逐步演示一個完整且可執行的範例，說明如何 **load image for OCR**、定義 **region of interest**，再 **extract text from rectangle**，最終 **recognize text from invoice**，解答那個經典的「如何提取金額」問題。沒有模糊的參考——只有具體程式碼、清晰說明，以及一些你會希望早點知道的專業小技巧。

---

## 您將構建的內容

完成本教學後，你將擁有一個小型的 Python 腳本，能夠：

1. 從磁碟載入發票影像。  
2. 標記出總金額所在的矩形 ROI。  
3. 僅在該 ROI 內執行 OCR。  
4. 輸出已清理的金額字串。  

以上流程適用於任何支援 ROI 的 OCR 函式庫——此處我們使用一個虛構但具代表性的 `SimpleOCR` 套件，模仿 Tesseract 或 EasyOCR 等常見工具。你可以自行替換；概念保持不變。

---

## 前置條件

- 已安裝 Python 3.8+（執行 `python --version` 應顯示 ≥3.8）。  
- 可透過 pip 安裝的 OCR 套件（例如 `pip install simpleocr`）。  
- 一張發票影像（PNG 或 JPEG），放在可參考的資料夾中。  
- 具備基本的 Python 函式與類別概念（不需要進階知識）。

如果你已具備上述條件，太好了——讓我們直接進入。如果還沒有，先取得影像檔；其餘步驟與實際檔案內容無關。

---

## Step 1: Load Image for OCR

任何 OCR 工作流程的第一步都是取得可讀取的點陣圖。大多數函式庫都提供簡單的 `load_image` 方法，接受檔案路徑。以下示範如何使用 `SimpleOCR` 引擎：

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** 使用絕對路徑或 `os.path.join`，可避免在不同工作目錄執行腳本時出現「找不到檔案」的狀況。

---

## Step 2: Define OCR Region of Interest

與其讓引擎掃描整頁，我們直接告訴它 **ocr region of interest** 的精確位置。這一步是可靠抽取的關鍵，尤其當文件包含雜訊的標頭或頁腳時。

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

為什麼是這些數字？`x` 與 `y` 為左上角的像素偏移量，`width` 與 `height` 則描述方框的尺寸。如果不確定，可在任意編輯器中開啟影像，開啟尺規並記錄座標。許多 IDE 甚至允許在游標懸停時即時顯示位置。

---

## Step 3: Extract Text from Rectangle

ROI 設定完成後，我們請引擎 **recognize text from invoice**，但僅限於剛剛定義的矩形。此呼叫會回傳一個結果物件，通常包含原始字串、信心分數，甚至邊界框資訊。

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

在背後，`recognize()` 會遍歷每個 ROI，裁切該區塊、執行 OCR 模型，最後將結果拼接回傳。這也是為什麼定義緊湊的 **extract text from rectangle** 區域能為批次作業節省數秒處理時間的原因。

---

## Step 4: How to Extract Amount – Clean the Output

OCR 並非完美，常會出現多餘的空格、換行，甚至讀錯字元（例如「S」與「5」）。簡單的 `strip()` 加上一小段正規表達式，通常就能正確取得金額。

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** 若要將金額寫入資料庫或付款閘道，必須保證格式一致。去除空白與非數字字元可防止下游錯誤。

---

## Step 5: Recognize Text from Invoice – Full Script

將上述所有步驟整合，即得到完整可執行的腳本。將檔案存為 `extract_amount.py`，然後執行 `python extract_amount.py`。

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### 預期輸出

```
Amount: 1,245.67
```

如果 ROI 對齊不正確，可能會看到類似 `Amount: 1245.6S` 的結果——注意那個多餘的「S」。請調整矩形座標後重新執行，直到輸出乾淨為止。

---

## 常見問題與邊緣案例

| 問題 | 發生原因 | 解決方案 |
|------|----------|----------|
| **ROI 太小** | 金額文字被裁切，導致辨識不完整。 | 將 `width`/`height` 增大約 10‑20 %，再測試。 |
| **DPI 不正確** | 低解析度掃描（≤150 dpi）降低 OCR 準確度。 | 在載入前將影像重新取樣至 300 dpi，或要求掃描器使用更高 DPI。 |
| **多種貨幣** | 正則表達式抓到第一個數字群，可能是發票編號。 | 改寫正則式，先偵測貨幣符號（`$`, `€`, `£`）再匹配數字。 |
| **發票旋轉** | OCR 引擎預設文字為直立，旋轉的頁面會失敗。 | 在加入 ROI 前先執行旋轉校正（`ocr_engine.rotate(90)`）。 |
| **背景噪點** | 陰影或印章干擾模型辨識。 | 使用簡單的閾值處理（`cv2.threshold`）或去噪濾波。 |

提前處理這些情況，可為日後除錯省下大量時間。

---

## 實務專業小技巧

- **批次處理：** 迴圈遍歷發票資料夾，動態計算 ROI（例如根據模板偵測），並將結果寫入 CSV。  
- **模板匹配：** 若需支援多種發票版型，可維護一個 `template_id → ROI 座標` 的 JSON 映射，根據快速版型分類器切換 ROI。  
- **平行執行：** 使用 `concurrent.futures.ThreadPoolExecutor` 同時執行多個 OCR 實例，適合高量能的後勤管線。  
- **信心過濾：** 大多數 OCR 結果會提供信心分數。將低於門檻（例如 85 %）的結果剔除，並標記為需人工審核。

---

## 結論

我們已完整說明如何 **ocr region of interest**、**load image for OCR**、**extract text from rectangle**，最終 **recognize text from invoice**，解決那個經典的 **how to extract amount** 問題。此腳本簡潔卻具彈性，足以因應不同文件格式、語言與 OCR 後端。

掌握基礎後，可進一步擴充工作流程：加入條碼掃描、整合 PDF 解析器，或將抽取的金額推送至會計 API。只要 ROI 定義清晰，你就能持續獲得更快、更乾淨的結果。

若遇到任何問題，歡迎在下方留言——祝 OCR 順利！

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## 接下來該學什麼？

- [如何透過在 OCR 中準備矩形來提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [使用 Aspose.OCR Detect Areas Mode 於 Java 提取圖像文字](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR for .NET 進行圖像文字提取 – OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}