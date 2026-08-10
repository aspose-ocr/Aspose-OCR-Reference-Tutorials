---
category: general
date: 2026-06-16
description: 在 OCR 中定義感興趣區域，以從身分證上提取西班牙文文字。學習如何載入影像以進行 OCR，並有效地指定 ROI。
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: zh-hant
og_description: 在 OCR 中定義感興趣區域，以從身分證上提取西班牙文文字。逐步說明如何載入圖像並指定 ROI。
og_title: 在 OCR 中定義感興趣區域 – 完整 Python 教學
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 定義 OCR 中的感興趣區域 – 完整 Python 教學
url: /zh-hant/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 定義 OCR 中的感興趣區域 – 完整 Python 教學

有沒有想過 **在 OCR 中定義感興趣區域 (ROI)**，只讀取圖像中真正需要的部分？在本教學中，我們會一步步帶你完成這件事，並示範如何 **載入 OCR 圖像**，只用幾行 Python 從身分證上擷取西班牙文文字。

如果你曾經盯著雜訊滿佈的掃描檔，心想「一定有更乾淨的方式抓取姓名欄位」，那麼這裡正是你的起點。完成後，你就能在不受背景雜訊干擾的情況下，抽取身分證上你關心的文字。

## 你將學會

- 為什麼在執行 OCR 前 **先定義感興趣區域** 很重要。  
- 使用流行的 Python OCR 包 **載入 OCR 圖像** 的完整步驟。  
- 如何 **以像素座標指定 ROI**。  
- 即使來源語言是西班牙文，也能 **可靠地擷取身分證文字**。  
- 處理旋轉卡片或低對比掃描等邊緣案例的技巧。  

不需要事先精通 OCR——只要有可運行的 Python 3 環境，以及一張想測試的身分證 JPEG 即可。

---

![Define region of interest illustration](placeholder.png){alt="定義感興趣區域範例，顯示在身分證圖像上以高亮矩形標示的區域"}

## 步驟 1：安裝並匯入 OCR 函式庫

首先，你需要一個提供 `OcrEngine` 類別的函式庫，類似前面示範的程式碼。這裡我們使用虛構的 `ocr` 套件，概念同樣適用於 `pytesseract`、`easyocr` 或任何允許設定語言與 ROI 的封裝。

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*小技巧*：若使用 `pytesseract`，`Rectangle` 類別會變成簡單的 tuple `(left, top, width, height)`。其餘流程保持不變。

## 步驟 2：載入 OCR 圖像

現在我們 **載入 OCR 圖像**。引擎需要一個 `ocr.Image` 物件，因此請指向保存身分證的檔案。路徑可以是絕對路徑或相對於腳本執行目錄的路徑。

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

如果圖像過大，建議先縮小；OCR 引擎在寬度低於 1500 px 的圖像上運行較快。

## 步驟 3：如何指定 ROI（定義感興趣區域）

以下是本教學的核心：**如何指定 ROI**。感興趣區域只是一個矩形，告訴 OCR 引擎「只在這些像素範圍內尋找」。想像你在身分證的姓名欄位周圍畫一個框。

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

為什麼是這些數字？在我們的樣本圖像中，姓名大約距左邊緣 120 px、距上緣 80 px。請依照你處理的卡片版面自行調整。  

*邊緣案例*：若卡片旋轉了 90°，請交換 `width` 與 `height`，並相應調整 `left`/`top`，或在送入引擎前使用 Pillow 先行旋轉圖像。

## 步驟 4：在 ROI 內執行 OCR

ROI 設定好後，引擎會忽略矩形外的所有內容。這不僅加快處理速度，也能減少因背景圖形產生的誤判。

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` 呼叫會回傳一個物件，內含辨識出的文字、信心分數，以及每個詞的邊界框。

## 步驟 5：擷取身分證文字（並驗證西班牙文輸出）

最後，我們 **擷取身分證文字**，從 ROI 結果中取出並印出。因為先前已將語言設為西班牙文，OCR 引擎會套用西班牙語字典，提升對「ñ」或「á」等重音字元的辨識準確度。

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### 預期輸出

```
ROI text: JUAN PÉREZ GARCÍA
```

若看到亂碼，請再次確認圖像確實為西班牙文，且 OCR 函式庫的語言資料檔已正確安裝。

## 常見陷阱與避免方式

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 回傳空字串 | ROI 未與任何文字相交 | 使用影像檢視器驗證座標；若支援，可呼叫 `engine.debug_draw_roi()`。 |
| 出現大量雜訊字元 | 語言套件錯誤 | 重新安裝西班牙語資料或改用 `ocr.Language.AUTO`。 |
| 信心分數低 | 圖像模糊或對比度低 | 使用 OpenCV 前處理 – 套用 `cv2.GaussianBlur` 與 `cv2.threshold`。 |
| OCR 仍在整張圖上執行 | 使用舊版函式庫 | 升級至最新的 `ocr` 套件；舊版會忽略 ROI 設定。 |

## 延伸範例：多個 ROI

有時需要同時擷取多個欄位（例如姓名與身分證號）。做法相同：變更 `engine.region_of_interest` 後再次呼叫 `recognize()`。

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

若函式庫支援，也可以一次批次處理多個矩形，減少與 OCR 引擎的往返次數。

## 完整可執行腳本

把上述所有步驟整合，以下是一個可直接執行的腳本，**定義感興趣區域**、**載入 OCR 圖像**，並 **從身分證擷取西班牙文文字**。

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

執行腳本後，你應該會在主控台看到姓名。調整矩形數值即可針對其他欄位使用，這樣就擁有一個可重複使用的身分證文件抽取工具。

## 往後的方向

- **批次處理**：遍歷身分證資料夾，將每張卡的姓名寫入 CSV 檔。  
- **語言偵測**：讓使用者動態選擇語言；`ocr.Language.AUTO` 非常方便。  
- **後處理**：使用正規表達式清理常見 OCR 錯誤（例如將名字中的「0」換成「O」）。  

掌握 **定義感興趣區域** 後，你就能快速、精準地 **擷取身分證文字**，尤其是處理西班牙語文件時更顯威力。

---

### TL;DR

我們示範了如何 **在 OCR 中定義感興趣區域**、**載入 OCR 圖像**，以及 **指定 ROI** 以 **從身分證圖像中擷取西班牙文文字**。完整範例在不到一分鐘內即可執行，且只要微調座標即可套用於任何版面。快試試看，調整矩形，讓 OCR 如雷射般聚焦。

Happy coding!

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}