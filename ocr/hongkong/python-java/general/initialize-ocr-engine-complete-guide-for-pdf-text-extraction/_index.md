---
category: general
date: 2026-06-25
description: 在 Python 中初始化 OCR 引擎，使用自訂字典、語言設定與區域定位，從多頁 PDF 提取文字。
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: zh-hant
og_description: 在 Python 中初始化 OCR 引擎，以可靠地讀取越南文 PDF，設定語言、前處理及自訂詞典，以獲得精確結果。
og_title: 初始化 OCR 引擎 – 步驟式 PDF 擷取指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 初始化 OCR 引擎 – PDF 文字提取完整指南
url: /zh-hant/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 初始化 OCR 引擎 – PDF 文字提取完整指南

曾經需要 **初始化 OCR 引擎** 來處理一批越南發票，但不知從何開始嗎？你並不孤單。在許多實務專案中，第一道障礙往往是讓 OCR 函式庫能夠順利讀取 PDF，尤其當你必須調整語言、前處理或自訂字典時。

在本指南中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **初始化 OCR 引擎**、設定語言、啟用智慧影像前處理、加入自訂字典，最後從多頁 PDF 的每一頁抽取結構化資料。完成後，你將得到一段可直接放入自己專案的自包含腳本——沒有遺漏、沒有「請參考文件」的捷徑。

## 你將學會

- 如何 **初始化 OCR 引擎** 並支援越南語。  
- 為何 **設定 OCR 語言** 對準確度至關重要。  
- 使用 **OCR 影像前處理** 選項，如自動去斜與自動二值化。  
- 加入 **OCR 自訂字典** 以提升領域特定詞彙的辨識率。  
- **辨識多頁 PDF** 並抽取特定區域（例如總金額）。  
- 將原始結果轉換為乾淨的 JSON‑like 結構，以供後續處理。

### 前置條件

- 已安裝 Python 3.8+。  
- 具備提供 `OcrEngine` 類別的 OCR 函式庫（範例使用假想的 `ocr` 套件；請以實際 SDK 取代）。  
- 在已知目錄中放置範例多頁 PDF（`sample.pdf`）。  
- 具備 Python 字典與迴圈的基本概念。

如果你已具備上述條件，讓我們開始吧。

---

## 步驟 1：在 Python 中如何初始化 OCR 引擎

首先必須 **初始化 OCR 引擎**。可以把它想成開啟機器，並告訴它即將處理的語言。

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **為何這很重要：**  
> 大多數 OCR 引擎預設只提供通用語言套件。透過明確設定 `ocr_engine.language`，可避免引擎自行猜測錯誤的字元，從而大幅降低越南語常見變音符號的誤辨率。

### 小技巧
如果需要在同一次執行中支援多種語言，可在處理每一頁前即時切換 `ocr_engine.language`。只要記得在 SDK 要求的情況下重新載入較重的模型即可。

---

## 步驟 2：啟用 OCR 影像前處理選項

原始掃描檔很少是完美的。頁面傾斜、光線不均或對比度低都會讓即使是最優秀的辨識器卡關。因此，我們在初始化後立即 **設定 OCR 影像前處理**。

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

這兩個旗標通常足以清理大多數掃描發票。若來源 PDF 已是高品質，亦可關閉它們以節省每頁數毫秒的處理時間。

---

## 步驟 3：加入 OCR 自訂字典

領域特定詞彙——例如訂單代碼、商品編號或法律縮寫——在通用語言模型中很少出現。透過提供 **OCR 自訂字典**，即可給引擎一張「小抄」。

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **底層發生了什麼？**  
> 引擎會提升與此清單中任意詞彙相符的單字的信心分數，使其不太可能被誤讀為其他文字。

---

## 步驟 4：辨識多頁 PDF – 一次抽取全部文字

現在引擎已完整設定，我們可以 **辨識多頁 PDF**。`recognize_multi_page` 方法會回傳一個列表，列表中的每個元素代表已完成 OCR 處理的單一頁面。

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

若要處理大型 PDF（數百頁），建議分批處理以降低記憶體使用量。大多數 SDK 也提供串流 API 以因應此類情境。

---

## 步驟 5：從每一頁抽取特定區域

大多數發票的「總金額」欄位都位於每頁相同位置。與其解析整頁文字，我們可以指示引擎只聚焦於一個矩形區域。

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **為何要鎖定區域？**  
> 限制 OCR 只在小範圍內執行，可加速處理並減少誤判，特別是當頁面其他部分雜訊較多時。

---

## 步驟 6：為每頁組裝 JSON‑Like 字典

取得原始文字固然好，但下游系統通常需要結構化資料。以下程式碼會建立一個乾淨的字典，包含頁碼、完整頁面文字、抽取出的總金額，以及所有辨識字詞與其信心分數的列表。

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

執行腳本後會輸出一系列字典——每頁一個——大致如下：

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

你可以輕鬆將輸出導向檔案（`> results.jsonl`），以便之後批次處理。

---

## 完整可執行範例

將所有步驟整合起來，以下即為可直接複製貼上執行的完整腳本：

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### 預期輸出

對一份三頁的發票 PDF 執行腳本，可能得到：

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

隨後可將結果 pipe 給 `jq` 或任何 JSON 解析器，以驗證結構是否正確。

---

## 常見問題與邊緣案例

| 問題 | 解答 |
|----------|--------|
| **如果我的 PDF 有密碼保護該怎麼辦？** | 大多數 SDK 允許在 `recognize_multi_page` 時傳入 `password` 參數。只要在呼叫時加入 `password="mySecret"` 即可。 |
| **我的掃描是灰階而非黑白。** | `auto_binarize` 選項會處理此情況，亦可在送入 `recognize_region` 前使用 `Pillow` 手動轉換。 |
| **總金額有時會出現在不同座標。** | 可以動態計算矩形（例如透過模板匹配），或先執行全頁 OCR，之後使用正則表達式如 `r'\d{1,3}(,\d{3})* VND'` 於文字中搜尋。 |
| **在 500 頁的 PDF 上效能很慢。** | 分批處理：一次處理 50 頁，寫入結果後清空 `pages` 列表釋放記憶體。若掃描已經校正，亦可關閉 `auto_deskew`。 |
| **之後想支援其他語言該怎麼做？** | 只要在呼叫 `recognize_multi_page` 前改成 `ocr_engine.language = ocr.Language.English`（或任何支援的列舉值），其餘流程保持不變。 |

---

## 產品上線部署的實務建議

1. **錯誤處理** – 將 OCR 呼叫包在 `try/except` 區塊；在失敗時記錄頁面索引，以便日後重試。  
2. **日誌記錄** – 使用 Python 的 `logging` 模組取代 `print`，以獲得彈性的詳細程度設定。  
3. **平行處理** – 若 OCR 函式庫支援執行緒安全，可使用 `ThreadPoolExecutor` 同時處理多頁。  
4. **設定檔** – 將語言、字典與矩形座標存於 JSON/YAML 檔案，讓腳本在不同專案間更具可重用性。  
5. **測試** – 建立小型測試集，使用已知 PDF 斷言抽出的 `total_amount` 與預期值相符。  

---

## 結論

您剛剛學會了 **

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並探索在專案中實作的其他方式。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}