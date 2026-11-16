---
category: general
date: 2026-06-22
description: 學習如何使用 Python 的 OCR 後處理器清理 OCR 文字。逐步程式碼、說明與可靠結構化 JSON 輸出的技巧。
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: zh-hant
og_description: 即時清理 OCR 文字，只需加入 OCR 後處理器。本指南展示完整的 Python 實作、其原理以及如何調整。
og_title: 使用自訂 OCR 後處理器清理 OCR 文字 – Python 教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: 使用自訂 OCR 後處理器清理 OCR 文本 – 完整 Python 指南
url: /zh-hant/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用自訂 OCR 後處理器清理 OCR 文字 – 完整 Python 指南

是否曾需要 **清理 OCR 文字**，卻因原始輸出中充斥換行、雜散空格與低信心字元而頭疼？你並不是唯一遇到這種情況的人。在許多實務流程中，OCR 引擎會交付一段文字加上信心分數，接著就要自行想辦法把它轉換成有用的資訊。  

好消息是？一個小小的 **OCR 後處理器** 就能整理結果、計算平均信心，甚至把所有資訊封裝成整齊的 JSON 字串——完全不需要觸碰核心引擎。本教學將一步步建立這個後處理器、將它註冊到通用的 AI/OCR 引擎，並逐行說明程式碼，讓你明天就能把它套用到自己的專案中。

---

## 本教學涵蓋的內容

- 如何建立一個 **清理 OCR 文字** 後處理器，正規化空白並去除換行。  
- 為什麼計算 **average confidence** 對下游驗證很有價值。  
- 以 `ai.set_post_processor` 模式將處理器註冊到 OCR 引擎。  
- 顯示結構化的 JSON 並排除常見的邊緣案例。  

不需要任何除 Python 標準函式庫之外的外部套件，您可以在任何支援 Python 3.8+ 的系統上跟隨操作。

---

## 前置條件

- 一個可運作的 OCR 引擎，能提供 `ocr_result` 物件，內含 `text`、`confidence`（float 列表）以及 `bounding_boxes`。  
- 具備基本的 Python 函式與 JSON 處理概念。  
- 可選：使用虛擬環境來保持相依性整潔。  

如果您不確定引擎是否支援自訂後處理器，請查閱文件中是否有 `set_post_processor` 方法——大多數現代 AI 驅動的 OCR SDK 都具備此功能。

---

## 步驟 1：定義 OCR 後處理器以 **清理 OCR 文字**

首先，我們撰寫一個函式，接收原始 OCR 結果、清理文字、計算信心指標，最後回傳 JSON 字串。請注意每個操作都有刻意的註解，這些註解說明「為什麼」——AI 助手特別喜歡引用的部分。

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**為什麼這樣有效：**  
- `replace("\n", " ")` 將多行 OCR 輸出轉為單一、可搜尋的字串——正是大多數流程中「清理 OCR 文字」的意義。  
- 去除前後空格可避免產生虛空的空 token，防止後續分詞器崩潰。  
- 計算平均信心提供一個單一的品質指標；您可以在將結果寫入資料庫前，拒絕低於某個門檻（例如 0.85）的結果。  
- 保持 bounding boxes 不變，意味著若需要標示低信心區域，仍可還原原始版面配置。

---

## 步驟 2：將自訂 **OCR 後處理器** 註冊到您的引擎

大多數 AI 驅動的 OCR SDK 都會提供一個方法，讓您插入後處理回呼函式。以下範例假設有一個名為 `ai`（即引擎）的物件提供 `set_post_processor`。若您的函式庫使用不同名稱，請自行替換。

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**提示：** 若日後需要切換行為（例如開關換行移除），可透過 `custom_settings` 傳入設定。這樣可讓處理器在不同專案間重複使用。

---

## 步驟 3：執行 OCR 引擎 – 結果現在是 JSON 字串

掛上後處理器後，呼叫 `engine.recognize()`（或您 SDK 所使用的任意方法）會自動觸發 `create_structured_json`。引擎接著回傳一個物件，其 `.text` 屬性已包含 JSON 負載。

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **注意：** 某些 SDK 可能回傳純文字字串，而非帶有 `.text` 屬性的物件。請依需求調整下一步的處理方式。

---

## 步驟 4：顯示（或持久化）結構化的 JSON 輸出

最後，我們把 JSON 印到主控台。實務上您可能會將它寫入檔案、訊息佇列或資料庫。

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**預期的主控台輸出**（為了易讀而格式化）：

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

如果看到多餘的換行字元或信心為 `0.0`，請再次確認您的 OCR 引擎真的有填入 `ocr_result.confidence`。後處理器內的防護條件會避免 `ZeroDivisionError`，但仍需要了解為何信心資料缺失。

---

## 處理常見邊緣案例

| 情境 | 需要留意的地方 | 快速修正 |
|-----------|-------------------|-----------|
| **Empty OCR result** | `ocr_result.text` 為 `""` 且 `confidence` 列表為空 | 處理器已回傳空的 `clean_text` 並將 `average_confidence` = 0.0。若想完全跳過 JSON 產生，可自行加入條件提前返回。 |
| **Non‑ASCII characters** | Unicode 被轉義為 (`\u00e9`) | 使用 `ensure_ascii=False`（已在程式碼中）即可保留「é」等字元的可讀性。 |
| **Very long documents** | JSON 大小可能超過 API 限制 | 考慮改為串流輸出或寫入檔案，而非一次回傳單一字串。 |
| **Bounding boxes missing** | 部分 OCR 引擎會省略版面資料 | 將 `boxes` 設為 `None` 或空列表；下游消費者應能優雅處理缺失情況。 |

---

## 專業技巧與最佳實踐

- **批次處理：** 若需 OCR 數百頁，將辨識呼叫包在迴圈中，將每筆 JSON 負載收集到列表，最後一次性寫入單一檔案，方便批次分析。  
- **信心門檻：** 寫入前先檢查 `average_confidence`。一般經驗法則是：關鍵資料錄入任務中，低於 `0.80` 的結果直接拒絕。  
- **使用日誌取代印出：** 正式環境建議以結構化日誌（`logging.info(...)`）取代 `print()`，這樣才能追蹤是哪張圖片產生低信心結果。  
- **測試：** 撰寫單元測試，提供一個已知文字與信心值的 mock `ocr_result`，再斷言產出的 JSON 結構符合預期。  

---

## 完整範例（結合所有步驟）

以下是可直接貼到 `ocr_cleanup.py` 檔案的完整腳本。請務必將佔位的 `engine` 與 `ai` 物件替換成您 OCR SDK 真正的實例。

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

儲存檔案後，執行 `python ocr_cleanup.py`，您應該會看到一個格式化良好的 JSON 字串，內含 **清理 OCR 文字**、平均信心分數以及原始的 bounding boxes。

---

## 結論

您現在已擁有一套完整、可投入生產環境的 **清理 OCR 文字** 解決方案，透過自訂 **OCR 後處理器** 於 Python 實作。此方法正規化空白、避免信心資料缺失，並回傳自我說明的 JSON 負載，讓下游服務無需額外解析即可直接使用。  

接下來您可以：

- 擴充處理器，在建立 `clean_text` 前 **過濾低信心單字**。  
- 加入 **語言偵測**，將 JSON 路由至特定語系的流水線。  
- 結合 **拼寫檢查** 函式庫，為品質再加一層保護。  

歡迎自行調整程式碼、嘗試不同的信心門檻，或在留言中分享您的改進想法。祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能幫助您進一步掌握 API 功能並探索其他實作方式：

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}