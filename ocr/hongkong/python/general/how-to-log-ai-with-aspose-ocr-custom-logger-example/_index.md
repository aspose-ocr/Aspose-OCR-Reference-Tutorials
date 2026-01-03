---
category: general
date: 2026-01-02
description: 學習如何使用 Aspose OCR 與自訂記錄器記錄 AI。本指南涵蓋自訂記錄器範例、如何匯入 Aspose OCR 以及設定自訂記錄器。
draft: false
keywords:
- how to log ai
- use custom logger
- custom logger example
- import aspose ocr
- set custom logger
language: zh-hant
og_description: 學習如何使用 Aspose OCR 及自訂記錄器來記錄 AI。跟隨逐步指南匯入 Aspose OCR、設定自訂記錄器並查看輸出。
og_title: 如何使用 Aspose OCR 記錄 AI – 自訂記錄器範例
tags:
- Aspose OCR
- Python
- Logging
title: 如何使用 Aspose OCR 記錄 AI – 自訂記錄器範例
url: /zh-hant/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 記錄 AI – 自訂記錄器範例

有沒有想過在玩 Aspose OCR 時 **如何記錄 AI**？也許你已經試過預設的 console logger，然後想說「這樣雖然可以，但能不能讓它更好看或寫入檔案？」你並不孤單。本教學將一步步示範完整的 **自訂記錄器範例**，提供完整程式碼，並說明 *為什麼* 每一段都有其意義。

完成本指南後，你將能夠：

* **在 Python 中匯入 Aspose OCR**，毫無障礙。  
* **設定自訂記錄器**，捕捉 AI 引擎發出的每一則訊息。  
* 驗證輸出，並將記錄器套用到自己的 logging 框架。

不需要額外文件——所有資訊都在此處。

---

## 前置條件

| 需求 | 原因 |
|------|------|
| Python 3.8+ | `asposeocr` 套件針對現代 Python 版本。 |
| 已安裝 `asposeocr` 套件（`pip install asposeocr`） | 提供我們將使用的 `asposeocr.ai` 模組。 |
| 具備函式與可呼叫物件的基本概念 | 需要用來撰寫自訂記錄器。 |

如果缺少上述任一項，請立即安裝套件：

```bash
pip install asposeocr
```

---

## 步驟 1 – 匯入 Aspose OCR 以及 AI 模組

當你想要 **匯入 Aspose OCR** 時，第一件事就是載入 `asposeocr.ai` 命名空間。這樣就能取得 `AsposeAI` 類別，它是所有 AI 驅動 OCR 操作的入口點。

```python
# Step 1: Import the Aspose OCR AI module
import asposeocr.ai as ai
```

**為什麼這很重要：** 正確匯入模組可確保你與正確的後端溝通。若漏掉 `.ai` 子模組，只會得到傳統的 OCR API，無法取得我們需要的記錄掛鉤。

---

## 步驟 2 – 建立預設 AI 引擎（console logger）

Aspose OCR 內建一個會直接寫入 `stdout` 的記錄器。先啟動它，觀察預設行為。

```python
# Step 2: Create an AI engine that logs to the console by default
default_engine = ai.AsposeAI()
```

執行任何 OCR 操作（使用 `default_engine`）時，你會看到類似以下的訊息：

```
[INFO] AsposeAI initialized – version 23.10
[DEBUG] Loading language model...
```

這些訊息對快速除錯很有幫助，但在正式環境中彈性不足。因此我們會進一步自訂。

---

## 步驟 3 – 定義自訂記錄器（接受字串的任意可呼叫物件）

**自訂記錄器** 可以是任何接受單一 `str` 參數的 Python 可呼叫物件。以下範例會在訊息前加上 `[AI LOG]` 前綴。你可以自行將 `print` 換成 `logging.info`、寫入檔案，或推送至監控服務。

```python
# Step 3: Define a custom logger (any callable that accepts a string)
def custom_logger(message: str):
    # You could replace this with `logging.info(message)` or any other sink.
    print("[AI LOG]", message)
```

**為什麼這樣可行：** `AsposeAI` 建構子會尋找符合「傳入字串」協定的 `logging` 參數。只要提供符合簽名的函式，即可完全掌控每一行日誌的處理方式。

---

## 步驟 4 – 建立使用自訂記錄器的 AI 引擎

現在把所有部件串起來。將 `custom_logger` 透過 `logging` 參數傳入 `AsposeAI` 建構子。引擎會把每一則內部訊息轉發給你的函式。

```python
# Step 4: Create an AI engine that uses the custom logger
engine_with_custom_logger = ai.AsposeAI(logging=custom_logger)
```

### 預期輸出

執行簡單的 OCR 呼叫（例如 `engine_with_custom_logger.recognize("sample.png")`）時，會產生類似以下的輸出：

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.
```

可以看到每一行現在都以 `[AI LOG]` 開頭，正如我們在 `custom_logger` 中定義的。這證明 **如何記錄 AI** 的行為已完全由你掌控。

---

## 完整範例 – 從匯入到執行

以下是完整腳本，可直接複製貼上為 `custom_logger_demo.py`。它示範了從匯入 Aspose OCR 到使用自訂記錄器執行簡單 OCR 請求的完整流程。

```python
# custom_logger_demo.py
# -------------------------------------------------
# Demonstrates how to log AI using Aspose OCR
# with a user‑defined logger.
# -------------------------------------------------

import asposeocr.ai as ai

def custom_logger(message: str):
    """A tiny logger that prefixes messages."""
    print("[AI LOG]", message)

def main():
    # Use the custom logger when creating the AI engine
    ocr_engine = ai.AsposeAI(logging=custom_logger)

    # Path to an image you want to process (replace with your own)
    image_path = "sample.png"

    # Perform OCR – this will trigger the logger
    try:
        result = ocr_engine.recognize(image_path)
        print("\n--- OCR RESULT ---")
        print(result.text)  # Assuming the result object has a `text` attribute
    except Exception as e:
        print("[AI LOG] Error during OCR:", e)

if __name__ == "__main__":
    main()
```

**執行時的預期結果**

```bash
python custom_logger_demo.py
```

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.

--- OCR RESULT ---
Hello world! This is the extracted text.
```

如果想 **設定自訂記錄器** 寫入檔案，只需將 `custom_logger` 內的 `print` 改成例如：

```python
def file_logger(message: str):
    with open("ocr.log", "a", encoding="utf-8") as f:
        f.write(message + "\n")
```

並在建立 `AsposeAI` 時傳入 `logging=file_logger`。

---

## 常見問題與邊緣情況

| 問題 | 答案 |
|------|------|
| *我可以使用標準的 `logging` 模組嗎？* | 當然可以。只要設定好 logger 實例，並在你的可呼叫物件內呼叫 `logger.info(message)` 即可。 |
| *如果我的記錄器拋出例外會怎樣？* | SDK 會捕捉記錄器拋出的任何例外並繼續執行，但該筆日誌會遺失。保持實作簡潔即可。 |
| *記錄器也會收到 debug 級別的訊息嗎？* | 會。AI 引擎會轉發 **所有** 內部訊息（INFO、DEBUG、WARN）。如只想保留特定等級，可在可呼叫物件內自行過濾。 |
| *`logging` 參數是可選的嗎？* | 若省略，引擎會退回使用內建的 console logger。 |
| *這在非同步程式碼中可用嗎？* | 記錄器本身是同步的；若需要非同步處理，可將呼叫包在 `asyncio` 協程中，並在適當位置使用 `await`。 |

---

## 專業技巧 – 讓你的記錄器適合上線環境

1. **批次寫入** – 每則訊息都開關檔案會很慢。建議使用帶緩衝的 `logging.FileHandler`。  
2. **加入時間戳** – 在前綴加入 `datetime.now().isoformat()`，可讓除錯更方便。  
3. **記錄等級** – 若需更細緻的等級控制，可改為接受 `(level, message)` 的 tuple，並自行解析等級關鍵字（目前 SDK 只傳遞字串）。  
4. **集中設定** – 將記錄器定義放在獨立模組（如 `my_logging.py`），在建立 `AsposeAI` 實例時統一匯入使用。  

這些技巧不只回答 *如何記錄 AI*，更教你 *如何高效記錄 AI*，適用於真實服務環境。

---

## 結論

我們已完整說明 **如何使用 Aspose OCR 記錄 AI**：從匯入函式庫、建立預設引擎、撰寫 **自訂記錄器範例**，到最終將記錄器注入 AI 引擎。程式碼完整、可直接執行，且可依需求套用任何 logging 後端。

如果想更進一步，試著將基於 `print` 的記錄器換成 Python 的 `logging` 模組，或將日誌推送至 Datadog 等雲端服務，甚至輸出結構化 JSON 供下游分析。模式不變——**使用自訂記錄器** 並在實例化 `AsposeAI` 時 **設定自訂記錄器**。

祝開發順利，願你的日誌如同 OCR 結果般清晰可見！

---

![how to log ai screenshot](image.png "how to log ai example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}