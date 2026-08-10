---
category: general
date: 2026-07-05
description: 在 Python 中快速執行影像光學字符辨識（OCR）。學習如何載入影像以進行 OCR、從掃描表格中提取文字，以及在 Python 中使用
  OCR 辨識影像。
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: zh-hant
og_description: 在 Python 中對圖像執行 OCR。本教學示範如何載入圖像以進行 OCR、從掃描表格提取文字，以及使用 OCR 識別圖像的 Python
  方法。
og_title: 使用 Python 進行圖像 OCR 完整指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 使用 Python 於影像執行 OCR – 完整指南
url: /zh-hant/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 執行影像 OCR – 完整指南

有沒有曾經需要**對影像執行 OCR**卻不知從何開始於 Python？你並非唯一。無論是數位化收據、從雜訊調查表格中提取資料，或只是將掃描的 PDF 轉換為可搜尋的文字，從掃描表格中提取文字是許多開發者每日的痛點。

在本教學中，我們將一步步說明**如何使用 OCR Python**函式庫，從載入圖片到顯示過濾後的結果。最後你將清楚知道如何**載入影像以進行 OCR**、設定信心門檻，並呼叫**OCR recognize image Python**方法來完成繁重的工作。

> **你將得到：**一個即時可執行的腳本，能載入影像、執行 OCR，並印出乾淨、經過信心過濾的文字。沒有模糊的參考、沒有缺少的匯入——只有完整、可直接複製貼上的解決方案。

---

## 需要的環境

在開始之前，請確保你已具備：

* 已安裝 Python 3.9 或更新版本（程式碼亦相容於 3.10 以上）。  
* 一個符合下方 `ocr` API 的 OCR 套件——例如虛構的 `simple-ocr` 函式庫，或任何提供 `OcrEngine`、`Language`、`Image` 的封裝。  
* 一張包含欲提取文字的影像檔（`.png`、`.jpg` 等）。  
* 能執行單一 Python 腳本的終端機或 IDE。

如果你已具備上述條件，太好了——讓我們馬上開始。

---

## 在影像上執行 OCR – 設定引擎

首先必須建立一個 OCR 引擎實例。把引擎想像成操作背後的大腦；它知道如何解讀像素並轉換成字元。

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*為什麼這很重要：* 沒有引擎就無法處理。`OcrEngine` 物件保存了所有稍後會調整的設定，例如語言與信心門檻。

---

## 載入影像以進行 OCR – 準備你的掃描表格

現在引擎已建立，我們需要**載入影像以進行 OCR**。函式庫的 `Image.load()` 方法會從磁碟讀取檔案，並轉換成引擎可理解的內部表示。

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **小技巧：** 若要處理 PDF，請先將每一頁轉為影像（例如使用 `pdf2image`）。OCR 引擎僅接受點陣圖影像。

---

## 如何使用 OCR Python – 設定語言與信心門檻

大多數 OCR 引擎支援多語言，且允許過濾低信心的字元。提前設定這些參數可確保只取得可靠的文字。

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*為什麼是 85 %？* 實務上，80‑90 % 左右的門檻能剔除大部分雜訊，同時保留有效資訊。可依掃描品質自行調整。

---

## 從掃描表格提取文字 – 影像辨識

引擎已就緒且影像已載入，現在可以真正**對影像執行 OCR**。`recognize()` 方法會回傳一個結果物件，內含提取出的文字，並可選擇提供邊界框資料。

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

如果函式庫支援，`result` 也可能提供 `result.confidences`（每個字元的信心分數列表）以及 `result.words`（結構化的字詞物件）。本教學僅聚焦於純文字輸出。

---

## OCR Recognize Image Python – 顯示過濾結果

最後，我們印出過濾後的文字。低信心的符號會顯示為問號（`?`），因為我們將 `min_confidence` 設為 85 %。

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### 預期輸出

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

留意無法辨識的簽名被轉成了 `?`。這正是信心過濾器的設計目的——讓輸出保持整潔，方便後續處理。

---

## 常見問題與專業技巧

| 問題 | 為什麼會發生 | 快速解決方案 |
|------|--------------|--------------|
| **空白輸出** | 影像過暗或解析度過低。 | 使用 OpenCV 前處理：提升對比、將解析度調整至 ≥300 dpi。 |
| **雜訊字元** | 語言設定錯誤。 | 設定 `engine.language` 為文件實際語言（例如 `ocr.Language.FRENCH`）。 |
| **過多 `?` 符號** | 信心門檻設定過高。 | 將 `engine.min_confidence` 降至 70‑80 % 以因應噪聲較大的掃描。 |
| **Unicode 錯誤** | 輸出包含非 ASCII 字元，但主控台編碼不正確。 | 執行 `python -X utf8` 或設定 `PYTHONIOENCODING=utf-8`。 |

**專業小技巧：** 若需提取表格，可在過濾原始文字後，再以支援版面感知的 OCR 引擎（如 Tesseract 的 `--psm 6`）進行第二次辨識。

---

## 完整腳本 – 可直接執行

以下是完整、獨立的腳本，涵蓋本文討論的每一步。將其儲存為 `perform_ocr.py`，調整影像路徑後執行 `python perform_ocr.py`。

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

執行後，你會在主控台看到過濾後的文字——正是**從掃描表格提取文字**步驟所承諾的結果。

---

## 接下來可以做什麼？

既然你已掌握如何**對影像執行 OCR**以及**從掃描表格提取文字**，可以進一步探索：

* **批次處理** – 迴圈遍歷整個影像資料夾，產生 CSV 結果檔。  
* **後處理** – 使用正規表達式或 spaCy 抽取日期、金額、或 ID 等欄位。  
* **整合** – 將 OCR 輸出寫入資料庫、Google Sheets，或透過 REST API 送出。  

上述所有想法皆圍繞我們已介紹的核心功能：載入影像、設定引擎、呼叫**OCR recognize image Python**方法。

---

## 結論

我們已完整示範如何使用 Python **對影像執行 OCR**的生產環境範例。從**載入影像以進行 OCR**、設定語言、調整信心門檻，到最終**從掃描表格提取文字**，每一步皆以清晰的程式碼與說明呈現。現在你已具備穩固的基礎，能應對更複雜的情境——無論是批次作業、多語言支援，或是表格抽取。

試著執行腳本、微調門檻，讓你的文件在數分鐘內變得可搜尋。若有任何問題或遇到棘手的表格，歡迎在下方留言，我們一起排除故障。祝程式寫得開心！

![Perform OCR on image example](example.png "對影像執行 OCR 範例")

## 接下來該學什麼？

以下教學與本指南所示技巧密切相關，提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose OCR 從影像提取文字 – 步驟說明指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 AspOCR：.NET 影像前處理 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [使用 Aspose.OCR 以語言選擇從 C# 影像提取文字](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}