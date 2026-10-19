---
category: general
date: 2026-03-18
description: 使用 Python 快速執行影像 OCR。學習如何從 PNG 識別文字、載入影像進行 OCR，並在一步一步的指南中從影像中提取詞彙。
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: zh-hant
og_description: 使用 Python 在圖像上執行 OCR。本教程示範如何從 PNG 識別文字、載入圖像進行 OCR，並以完整程式碼範例從圖像中提取詞彙。
og_title: 在圖像上執行 OCR – Python 指南
tags:
- OCR
- Python
- Image Processing
title: 在圖像上執行 OCR – 完整 Python OCR 範例
url: /zh-hant/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 執行影像 OCR – 完整 Python OCR 範例

有沒有需要 **在影像上執行 OCR** 卻不知從何下手？你並不孤單；許多開發者在第一次處理掃描文件的文字抽取時，都會卡在這裡。在本教學中，我們將一步步示範一個 **Python OCR 範例**，讓你能 **從 PNG 檔案辨識文字**、**載入影像以供 OCR**，以及 **從影像中抽取單字並取得信心分數**，全部只需幾行程式碼。

我們會說明所有必備項目：所需函式庫、如何設定引擎、每一步的意義，以及輸出結果長什麼樣子。完成後，你只要把這段程式碼貼到自己的專案，即可立即從任何影像中擷取文字。沒有冗長說明，只有可直接執行的實用解決方案。

## 你需要的環境

在開始之前，請確保你已具備：

- 已安裝 Python 3.8 或更新版本  
- `ocrengine` 套件（或任何提供 `OcrEngine` 類別的函式庫）。可使用 `pip install ocrengine` 安裝——若使用其他 OCR 函式庫（如 `pytesseract`），請自行調整套件名稱。  
- 一張想要處理的影像檔（PNG、JPG 等），本教學以 `invoice.png` 為例。  

就這樣。沒有大型相依套件、沒有外部服務，純粹使用 Python。

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: 執行影像 OCR 範例 – 正在處理的掃描發票*

## 第一步 – 安裝並匯入 OCR 函式庫

首先，將 OCR 引擎安裝到環境中並匯入。如果你使用的是假想的 `ocrengine` 套件，匯入方式如下：

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**為什麼這很重要：** 匯入正確的類別才能使用稍後會呼叫的 `setImageFromFile`、`recognize` 等方法。若省略此步，Python 會拋出 `ModuleNotFoundError`，甚至連影像都無法載入。

## 第二步 – 建立 OCR 引擎實例

函式庫已就緒後，我們需要一個引擎物件來保存辨識過程的設定與狀態。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*小技巧：* 某些 OCR 引擎允許在此階段調整語言模型或 DPI 設定。對於基本的 **python OCR example**，預設值已足夠，但若面對低解析度掃描，建議在此調整。

## 第三步 – 載入要處理的影像

接下來的合理步驟是 **載入影像以供 OCR**。只要把 PNG（或任何支援格式）的檔案路徑傳給引擎即可。

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**底層發生了什麼？** 引擎會讀取像素資料，轉換成辨識演算法可理解的格式，並在內部保存。若檔案路徑錯誤，會拋出 `FileNotFoundError`，請務必確認影像檔案確實存在。

## 第四步 – 執行辨識演算法

影像載入完成後，我們終於 **在影像上執行 OCR**，以抽取文字內容。

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

此時引擎會掃描位圖、套用模式匹配，並回傳一個物件，內含所有偵測到的單字、行以及信心指標。

## 第五步 – 逐一檢視辨識出的單字與信心分數

任何 OCR 工作流程中最實用的部分，就是看到 **每個抽取字元的信心**。這能讓你根據需要過濾低信心的結果。

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**預期輸出**（範例）：

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

現在你可以清楚看到 **從影像中抽取了哪些單字**，以及每個偵測的可靠程度。這正是 **從影像抽取單字** 流程的核心。

## 處理常見的例外情況

### 影像是灰階的怎麼辦？

某些 OCR 引擎在彩色影像上表現較佳。若發現整體信心偏低，可先將 PNG 轉為對比度較高的黑白版再送入引擎。Pillow 可協助完成：

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### 同時處理多種語言

若文件同時包含英文與西班牙文，你需要 **從 PNG 辨識文字** 時使用多語言模型。大多數引擎允許在初始化時設定語言清單：

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### 過濾低信心的單字

有時只想保留信心高於 90 % 的單字，簡易過濾寫法如下：

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## 完整、可直接執行的腳本

把所有步驟整合起來，以下是一個可直接複製貼上並執行的單一腳本（只需將 PNG 路徑改成自己的檔案）。

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

執行方式：

```bash
python run_ocr_on_image.py
```

執行後，你應該會在主控台看到單字與信心百分比的清單，與前面示範的結果完全相同。

## 常見問答

**這能處理 JPG 或 TIFF 檔案嗎？**  
當然可以。`setImageFromFile` 方法接受底層函式庫能解碼的任何格式，因此你可以 **在影像上執行 OCR**，支援 JPG、TIFF、BMP 等。

**可以在迴圈中處理多張影像嗎？**  
沒問題。只要把載入與辨識步驟包在 `for` 迴圈裡，遍歷檔案路徑清單即可。若函式庫要求每張影像必須重新建立實例，記得在迴圈內重新初始化引擎。

**如果想要一次取得整段文字，而不是逐字返回，該怎麼做？**  
大多數 OCR 結果物件都提供 `getText()` 方法，可一次回傳整篇文件。例如：

```python
full_text = ocr_result.getText()
print(full_text)
```

## 往後的步驟與相關主題

既然已掌握 **在影像上執行 OCR**，可以進一步探索：

- **後處理**：使用正規表達式清理發票中的日期、金額或 ID。  
- **批次處理**：結合 `os.listdir()`，一次處理整個資料夾的掃描文件。  
- **替代函式庫**：`pytesseract` 是常見的開源選擇，工作流程相似，只要換掉引擎呼叫即可。  
- **匯出結果**：將抽取的單字與信心分數寫入 CSV，供後續分析使用。

上述每個延伸都直接建立在本教學的基礎上，讓你能把原始 OCR 資料轉化為可行的資訊。

---

### TL;DR

我們示範了一個簡潔的 **python OCR example**，說明如何 **載入影像以供 OCR**、**在影像上執行 OCR**，以及 **從影像抽取單字** 同時回報信心分數。完整腳本已備妥，你現在也能把它套用到任何需要 **從 PNG 辨識文字**（或其他格式）的專案。快試試看，調整信心門檻，讓你的應用在幾分鐘內變得具備文字感知能力。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}