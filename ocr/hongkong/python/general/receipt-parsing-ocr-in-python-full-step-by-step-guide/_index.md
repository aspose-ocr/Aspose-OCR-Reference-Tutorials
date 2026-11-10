---
category: general
date: 2026-06-28
description: 在 Python 中輕鬆實現收據解析 OCR – 學習如何提取收據資料、載入影像 OCR，並查看完整的 Python OCR 範例。
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: zh-hant
og_description: Python 收據解析 OCR：學習如何提取收據資料、載入圖像 OCR，並在幾分鐘內執行完整的 Python OCR 範例。
og_title: Python 收據解析 OCR – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: Python 中的收據解析 OCR – 完整逐步指南
url: /zh-hant/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 收據解析 OCR（Python）全步驟指南

有沒有想過如何把模糊的超市收據變成乾淨、可搜尋的 JSON？**Receipt parsing OCR** 就是答案，而且你不需要計算機視覺博士學位就能讓它運作。在本教學中，我們將一步步示範一個實用的 **python ocr example**，從載入影像、執行結構化文字辨識，到輸出格式化的 JSON 字串——非常適合匯入記帳軟體或分析管線。

我們也會回答最常見的問題：**如何可靠地擷取收據** 資料，即使掃描品質不佳。完成後，你將擁有一個可重複使用的腳本，無論是個人理財 App 或企業級費用追蹤系統，都能直接套用。

## 你將學到什麼

* 如何在 Python 中設置輕量級的 OCR 引擎。  
* **load image OCR** 用於收據檔案的完整步驟。  
* 如何呼叫結構化辨識方法並將結果轉成 JSON。  
* 處理常見邊緣案例的技巧——旋轉的收據、低對比度、以及 Unicode 字元。  
* 完整、可直接複製貼上的程式碼範例，今天就能執行。

### 前置條件

* 已在機器上安裝 Python 3.8 或更新版本。  
* 提供 `OcrEngine` 類別與 `Image` 輔助工具的 OCR 函式庫（許多函式庫都有類似 API；本教學假設使用通用的封裝）。  
* 收據影像（`receipt.png`）已放置於可參照的資料夾中。  
* 可選但建議安裝：`pip install pillow` 以處理影像，及任何 OCR 函式庫所需的其他相依套件。

如果缺少上述任一項，現在就安裝——大多數套件只要一行指令即可完成。

---

## 收據解析 OCR – 步驟 1：安裝與匯入必要模組

首先，先把 Python 環境準備好。我們要匯入 `json` 以便序列化，還有 OCR 專屬的類別。

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*為什麼這很重要*：在檔案最上方匯入可以讓腳本保持整潔，且確保 OCR 引擎在整個程式中皆可使用。若忘記匯入 `json`，之後的 `json.dumps` 會拋出 `NameError`。

**小技巧**：如果你的 OCR 函式庫位於不同的命名空間（例如 `easyocr` 或 `pytesseract`），請相應調整匯入語句。其餘教學內容不變。

---

## 如何擷取收據資料 – 步驟 2：建立 OCR 引擎實例

現在啟動引擎。把 `OcrEngine()` 想成會閱讀收據的大腦。

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

大多數現代 OCR SDK 都允許在此設定語言包或偵測模式。對於一般收據，你會想使用英文（或收據本身的語言）以及「structured」模式（若有提供）。

> **注意**：若你的函式庫需要授權金鑰，請以參數傳入：`engine = OcrEngine(api_key="YOUR_KEY")`。

---

## 載入影像 OCR – 步驟 3：把引擎指向你的收據

引擎就緒後，我們需要把影像檔案餵給它。這就是 **load image OCR** 發揮作用的地方。

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*發生了什麼*：`Image.from_file` 會讀取 PNG（或 JPG、TIFF 等）並包裝成 OCR 引擎能理解的格式。若你的收據是 PDF，請先把第一頁轉成影像——許多函式庫提供 `pdf2image` 輔助工具。

**邊緣案例**：若收據是倒置掃描，只要旋轉後仍可辨識：

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

---

## 如何 OCR 收據 – 步驟 4：執行結構化文字辨識

現在魔法發生了。我們請引擎執行結構化掃描，嘗試將項目、總金額與日期分組。

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

如果你的 OCR 函式庫只提供普通的 `recognize()` 方法，你仍然可以手動擷取欄位，但 `recognize_structured()` 通常會回傳包含 `items`、`total`、`date` 等鍵的字典。

---

## Python OCR 範例 – 步驟 5：將結果轉成 JSON

原始結果物件通常是自訂類別。把它轉成普通的 Python dict 後，就能輕鬆序列化。

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*為什麼要 `ensure_ascii=False`？* 收據可能包含貨幣符號（€, £）或帶重音的字元。此旗標會保留原始字元，而不是轉成 `\u00e9` 之類的 Unicode 逃脫序列。

---

## 如何擷取收據 – 步驟 6：輸出 JSON 表示

最後，我們把 JSON 印出（或寫入檔案），讓你可以把它導入資料庫、試算表或 API。

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**預期輸出**（為了可讀性已做 pretty‑print）：

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

如果看到空的 dict 或缺少欄位，請再次確認收據影像是否清晰，以及 OCR 引擎是否設定了正確的語言。

---

## 專業技巧與常見陷阱（加分章節）

| 問題 | 為什麼會發生 | 快速解決方案 |
|------|--------------|--------------|
| **影像模糊或低對比** | OCR 無法處理噪點 | 使用 OpenCV 前處理：`cv2.threshold` 或 `cv2.bilateralFilter` |
| **收據旋轉** | 引擎預設文字為正立 | 用 `engine.detect_orientation()` 偵測方向，或手動旋轉（參見步驟 3） |
| **非拉丁字元** | 語言包錯誤 | 初始化引擎時指定 `language="spa"`（西班牙語）等 |
| **大型收據導致記憶體錯誤** | 一次載入整張影像 | 裁切感興趣區域：`engine.set_image(image.crop((x, y, w, h)))` |

---

## 接下來可以做什麼？延伸工作流程

你已經掌握了 **receipt parsing OCR** 在 Python 中的完整流程。以下提供幾個延伸想法，讓你持續發揮：

* **批次處理** – 迴圈走訪收據影像資料夾，將每筆 JSON 追加至主檔案。  
* **寫入資料庫** – 使用 `sqlite3` 或 `SQLAlchemy` 把每張收據存成一筆資料列。  
* **機器學習強化** – 把擷取出的項目送入分類模型，進行費用標籤化。  

上述所有步驟皆基於本教學的核心流程，而每個延伸都會遵循相同的 **python ocr example** 模式：載入 → 辨識 → 序列化 → 儲存。

---

## 結論

本指南帶你完整走過 **receipt parsing OCR** 的 Python 工作流程，清楚說明 **如何擷取收據** 資訊、**載入影像 OCR**，並提供可直接執行的 **python ocr example**。只要遵循六個步驟——安裝、匯入、實例化、載入、辨識、序列化——你就擁有了任何收據處理專案的堅實基礎。

歡迎自行實驗：嘗試不同的 OCR 引擎、調整前處理，或加入缺欄位的錯誤處理。結合可靠的 OCR 與 Python 的彈性，幾乎沒有做不到的事。若有任何問題或想分享自己的改良方式，請在下方留言，我們一起討論。

祝程式開發愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能在此基礎上延伸更多技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索不同實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}