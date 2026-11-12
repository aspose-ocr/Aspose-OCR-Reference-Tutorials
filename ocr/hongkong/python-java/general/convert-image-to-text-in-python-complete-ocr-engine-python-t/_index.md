---
category: general
date: 2026-07-05
description: 使用 Python OCR 將圖像轉換為文字 – 一個一步一步的 Python OCR 範例，示範如何從圖像提取文字以及如何辨識 JPG
  圖片中的文字。
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: zh-hant
og_description: 使用 Python OCR 將圖像轉換為文字。跟隨此 Python OCR 範例，即可在數分鐘內從圖像提取文字並識別 JPG 中的文字。
og_title: 在 Python 中將圖像轉換為文字 – 完整 OCR 引擎指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: 在 Python 中將圖像轉換為文字 – 完整 OCR 引擎 Python 教學
url: /zh-hant/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中將圖像轉換為文字 – 完整 OCR 引擎 Python 教程

有沒有曾經需要**將圖像轉換為文字**，卻不確定該信任哪個函式庫？你並不是唯一遇到這種情況的人——許多開發者在首次嘗試從掃描收據或標誌照片中提取字元時，都會卡在這裡。好消息是？Python 的 OCR 生態系統讓這項工作幾乎毫不費力。

在本**python ocr example**中，我們將示範一個真實情境：你有一張包含西里爾字元的 JPEG，想要可靠地**extract text from image**。完成後，你將了解如何**recognize text from jpg**檔案、每個步驟的重要性，以及如何將程式碼套用到其他語言或圖像格式。

## 需要的環境

* 已安裝 Python 3.8+（最佳使用最新穩定版）。
* 具備可用的網際網路連線以安裝 OCR 套件。
* 一個圖像檔案（例如 `cyrillic_sample.jpg`），其中包含你想提取的文字。
* 可選但方便：使用虛擬環境來保持相依性整潔。

不需要繁重的作業系統層級相依性，也不需要陌生的建置工具——只要幾個 pip 指令與少量程式碼即可。

## 步驟 1：安裝 OCR 引擎 Python 套件

首先，你必須取得一個能與 Python 良好配合的 OCR 引擎。此教學中，我們將使用虛構的 `ocr` 套件，因為它的 API 與許多真實的函式庫（如 `pytesseract` 或 `easyocr`）相似。使用以下指令安裝：

```bash
pip install ocr
```

> **Why this step matters:** 安裝套件會下載原生二進位檔與語言資料檔，這些才是真正執行繁重工作的部分。若跳過此步驟，當你嘗試 `import ocr` 時會拋出 `ImportError`。

## 步驟 2：匯入模組並設定環境

現在庫已安裝在你的機器上，匯入所需的模組。我們也會設定 logging，讓你能看到引擎在底層的運作——在之後處理**extract text from image**且不夠乾淨的檔案時非常有用。

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **Pro tip:** 若你在 Jupyter notebook 中工作，可能想設定 `logging.getLogger().setLevel(logging.DEBUG)` 以查看更多細節。

## 步驟 3：建立 OCR 引擎實例

建立引擎是任何**ocr engine python**工作流程的基石。可將其想像成在暗室中開燈；若沒有它，後續的管線將無法看見任何東西。

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **Why this step is crucial:** `OcrEngine` 物件保存了語言套件、前處理選項與硬體加速旗標等設定。之後變更任何這些設定都會影響所有後續的辨識。

## 步驟 4：選擇正確語言 – 支援西里爾文

如果你處理的是西里爾文字（或任何非拉丁文字），必須告訴引擎載入哪個語言模型。否則會得到亂碼，甚至是空字串。

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **Edge case:** 某些引擎需要你另行下載語言資料。若看到 `LanguageDataNotFound` 錯誤，請在設定語言前執行 `ocr.download_language('CYRILLIC')`。

## 步驟 5：載入要從中 **convert image to text** 的圖像

這就是**convert image to text**真正開始發揮作用的地方。OCR 引擎是針對 `Image` 物件運作，而非直接使用檔案路徑，因此我們需要先將 JPEG 包裝成 `Image`。

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **Why this matters:** 載入圖像讓引擎能檢查其尺寸、色深與 DPI。這些屬性會影響引擎對**recognize text from jpg**檔案的辨識效果。

## 步驟 6：辨識文字 – Python OCR Example 的核心

現在我們終於請求引擎執行其設計目的：將像素轉換為字元。`recognize` 方法會回傳一個結果物件，內含提取出的字串、信心分數與邊界框。

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **What you get back:** `ocr_result.text` 為普通的 Python 字串，保留換行。若需要字詞層級的位置資訊，可查看 `ocr_result.boxes`。

## 步驟 7：輸出辨識文字 – 驗證你的 **convert image to text** 成功

檢查是否成功**convert image to text**的最簡單方法是印出結果。實際應用中，你可能會將其寫入資料庫或文字檔。

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### 預期輸出

假設 `cyrillic_sample.jpg` 包含短語 “Привет, мир!” 時，控制台會顯示：

```
=== OCR OUTPUT ===
Привет, мир!
```

若輸出為空或毫無意義，請再次確認語言設定與圖像品質。模糊或低對比度的圖像常導致不佳的**extract text from image**結果。

## 處理常見問題

| Problem | Why it Happens | Quick Fix |
|---------|----------------|-----------|
| **Empty string** | 語言模型未載入或圖像過暗 | 確保 `ocr_engine.language` 與文字腳本相符；使用 `ocr.Image.adjust_contrast()` 提高圖像對比度 |
| **Garbage characters** | 語言設定錯誤或混合腳本 | 設定 `ocr_engine.language = ocr.Language.MULTI` 或分兩次辨識（先拉丁文再西里爾文） |
| **Slow performance on large batches** | 引擎逐一處理圖像 | 啟用多執行緒：`ocr_engine.set_threads(4)` |
| **Memory leaks** | 未釋放圖像資源 | 在辨識後呼叫 `cyrillic_image.close()` |

> **Pro tip:** 在批次處理時，將辨識迴圈包在 `try/except` 區塊中，以捕捉偶發的 `ocr.EngineError` 例外，避免整個工作中斷。

## 擴充範例 – 從 JPEG 到 PDF，從西里爾文到多語言

我們使用的**convert image to text**模式適用於任何點陣圖格式：PNG、BMP、TIFF，甚至掃描的 PDF（先將頁面提取為圖像）。若需要**extract text from image**包含多種語言的檔案，可傳入列表：

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

如果你處理的是手機拍攝的高解析度照片，建議加入前處理步驟：

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

這些調整常能將普通的**python ocr example**升級為可投入生產的程式碼。

## 完整可執行腳本

以下是完整、可直接執行的腳本，將所有步驟整合在一起。將其儲存為 `convert_image_to_text.py`，然後執行 `python convert_image_to_text.py`。



## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}