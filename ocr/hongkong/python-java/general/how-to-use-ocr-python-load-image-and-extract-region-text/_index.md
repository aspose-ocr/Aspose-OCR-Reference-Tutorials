---
category: general
date: 2026-06-25
description: 如何在 Python 中使用 OCR – 學習如何載入圖像進行 OCR、辨識區域文字，並快速提取該區域文字。
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: zh-hant
og_description: 如何在 Python 中使用 OCR – 逐步指南：載入圖像、辨識特定區域文字，並提取發票號碼。
og_title: 如何使用 OCR Python：載入圖像並提取區域文字
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 如何使用 OCR Python：載入圖像並提取區域文字
url: /zh-hant/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR：載入影像並擷取區域文字

**How to use OCR in Python** 其實比想像中更簡單。是否曾盯著掃描過的發票，想只抓取發票號碼卻不想解析整頁內容？你並不孤單——許多開發者在首次接觸光學字元辨識時都會卡在這裡。本指南將逐步說明如何載入影像供 OCR 使用、定義矩形區域、辨識該區域文字，最後擷取區域文字。完成後，你將擁有一個可直接執行的腳本，能夠分離出任何你需要的文字片段。

> *小技巧：* 若你在處理 PDF，請先將每頁轉成影像——大多數 OCR 套件對 PNG/JPEG 的支援最佳。

## 你需要的條件

- Python 3.8+（建議使用最新穩定版）  
- 提供 `OcrEngine` 類別的 OCR 套件（例如透過 `pip install ocr-lib` 安裝的 **ocr**）  
- 範例影像——此處使用放在你自行管理資料夾中的 `invoice.png`  
- 基本的矩形概念（x、y、寬度、高度）  

不需要大型依賴，也不需要 GPU——純 CPU 即可執行，保持高度可移植性。

---

## 如何使用 OCR：初始化引擎（步驟 1）

在讀取任何文字之前，你必須先建立 OCR 引擎實例。它就像是負責分析像素模式的大腦。

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*為什麼這很重要：* 初始化引擎會載入語言模型並設定預設參數。若跳過此步驟，呼叫 `recognize_region` 時會拋出例外。

---

## 載入影像供 OCR 使用（步驟 2）

引擎就緒後，我們將影像傳入。套件的 `Image.load` 方法會處理常見格式並正規化位圖。

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

如果找不到檔案，Python 會拋出 `FileNotFoundError`。請確保路徑為絕對路徑或相對於腳本執行目錄。

*邊緣情況：* 某些 OCR 引擎需要灰階影像。若發現辨識準確度不佳，請先將影像轉為灰階：

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## 在區域內辨識文字（步驟 3）

定義區域即是告訴引擎「在哪裡」搜尋。`Rectangle` 接受浮點數值，以提供次像素精度，對高解析度掃描特別有用。

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – 矩形左上角座標（單位：像素）  
- **width, height** – 矩形的寬與高  

你可能會好奇這些數值該怎麼取得。快速方法是使用任何影像編輯器（如 GIMP 或 Paint.NET）的選取工具，讀取座標資訊。

*為什麼不直接 OCR 整頁？* 限制辨識範圍可減少雜訊、加速處理，且對發票號碼等小欄位的準確度提升顯著。

---

## 擷取區域文字（步驟 4）

設定好區域後，請求引擎只辨識該切片。回傳的結果物件包含原始文字與信心分數。

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

若 OCR 引擎支援多語言，你可以額外傳入語言代碼：

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*常見陷阱：* 有些引擎會回傳單字列表而非單一字串。此時請自行將它們串接起來：

```python
text = " ".join(region_result.words)
```

---

## 輸出擷取到的發票號碼（步驟 5）

最後，將擷取到的文字印出或儲存。你也可以在字串上做後處理，移除多餘的空白或非數字字元。

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

執行腳本且矩形正確對齊時，應會得到類似以下的輸出：

```
Invoice number: 20231578
```

若出現雜訊字元，請再次檢查矩形座標，或考慮提升影像解析度。

---

## 完整範例程式

將上述步驟整合，以下是一個可直接複製貼上執行的獨立腳本：

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

將檔案另存為 `extract_invoice.py`，將 `YOUR_DIRECTORY` 替換成實際資料夾路徑，然後執行：

```bash
python extract_invoice.py
```

你應該會在主控台看到印出的發票號碼。

---

## 常見問與答

**Q: 若發票號碼使用特殊字體會怎樣？**  
A: 大多數現代 OCR 引擎已能處理各式字體，但你可以透過訓練自訂語言模型或在影像前處理（例如套用閾值濾鏡）來提升準確度。

**Q: 能一次擷取多個欄位嗎？**  
A: 當然可以。建立一個 `Rectangle` 物件的列表——每個欄位一個——然後迭代處理，將每個結果存入字典中。

**Q: 這能用在多頁 PDF 嗎？**  
A: 先將每頁轉成影像（使用 `pdf2image` 或類似套件），再對每頁套用相同的區域擷取流程。

---

## 小結

本教學說明了 **如何在 Python 中使用 OCR**：載入影像、在特定區域辨識文字、並擷取該區域文字——非常適合從掃描文件中抽取發票號碼、訂單編號或任何小段資料。透過聚焦感興趣的區域，你可以獲得更快的速度、更高的準確度，且減少後處理的麻煩。

準備好進一步挑戰了嗎？試著將腳本擴充為 **從批次發票資料夾載入影像**，或將 **在區域內辨識文字** 應用於日期、總金額等不同欄位。模式相同——只要更改矩形座標即可。

如果在實作過程中遇到問題或有改進想法，歡迎在下方留言。祝開發順利，願你的 OCR 流程永遠精準！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索在專案中使用的不同實作方式。

- [使用 Aspose OCR 從影像擷取文字 – 步驟教學](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [透過 OCR 準備矩形以擷取影像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [使用 AspOCR：.NET 影像前處理 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}