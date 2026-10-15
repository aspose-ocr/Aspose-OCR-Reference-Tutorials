---
category: general
date: 2026-04-26
description: 使用 AsposeAI OCR 後處理快速遮蔽信用卡號碼。於一步一步的教學中學習 PCI 合規、正則表達式遮蔽與資料淨化。
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: zh-hant
og_description: 使用 AsposeAI 在 OCR 結果中遮蔽信用卡號碼。本教學涵蓋 PCI 合規、正則表達式遮蔽及資料淨化。
og_title: 遮蔽信用卡號碼 – 完整 Python OCR 後處理指南
tags:
- OCR
- Python
- security
title: 在 OCR 輸出中遮蔽信用卡號碼 – 完整 Python 指南
url: /zh-hant/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 遮蔽信用卡號碼 – 完整 Python 指南

是否曾需要在直接來自 OCR 引擎的文字中**遮蔽信用卡號碼**？你並非唯一遇到此情況的人。在受規管的行業中，暴露完整的 PAN（Primary Account Number）可能會讓你在 PCI 合規審核員面前陷入麻煩。好消息是？只需幾行 Python 以及 AsposeAI 的後處理掛鉤，即可自動隱藏中間八位數，確保安全。

在本教學中，我們將逐步示範一個真實情境：對收據影像執行 OCR，然後套用自訂的 **OCR 後處理** 函式以清理任何 PCI 資料。完成後，你將擁有一段可重複使用的程式碼片段，能直接嵌入任何 AsposeAI 工作流程，並提供處理邊緣案例與擴展解決方案的實用技巧。

## 你將學到

- 如何在 **AsposeAI** 中註冊自訂的後處理器。
- 為何 **正則表達式遮蔽** 方法既快速又可靠。
- **PCI 合規** 與資料清理的基礎知識。
- 如何擴充模式以支援多種卡片格式或國際卡號。
- 預期的輸出以及如何驗證遮蔽是否成功。

> **先決條件** – 你應該具備可運作的 Python 3 環境，已安裝 Aspose.AI for OCR 套件 (`pip install aspose-ocr`)，以及包含信用卡號碼的範例影像（例如 `receipt.png`）。不需要其他外部服務。

---

## 步驟 1：定義遮蔽信用卡號碼的後處理器

解決方案的核心是一個小函式，接收 OCR 結果，執行 **正則表達式遮蔽** 程序，並回傳已清理的文字。

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**為什麼這樣有效：**  
- 正則表達式 `(\d{4})\d{8}(\d{4})` 完全匹配 16 位連續數字，這是 Visa、MasterCard 等常見的格式。  
- 透過捕獲前四位與後四位 (`\1` 與 `\2`)，我們保留足夠的除錯資訊，同時遵守 **PCI 合規** 規則，禁止儲存完整的 PAN。  
- 置換 `\1****\2` 隱藏敏感的中間八位，使 `1234567812345678` 變為 `1234****5678`。

> **專業提示：** 若需支援 15 位數的美國運通卡號，可加入第二個模式，例如 `r'(\d{4})\d{6}(\d{5})'`，並依序執行兩次取代。

## 步驟 2：初始化 AsposeAI 引擎

在我們能掛接後處理器之前，需要先建立 OCR 引擎的實例。AsposeAI 包含 OCR 模型以及供自訂處理使用的簡易 API。

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**為什麼在此初始化？**  
- 只建立一次 `AsposeAI` 物件，並在多張影像間重複使用，可減少開銷。引擎亦會快取語言模型，提升後續呼叫速度——在批次掃描收據時相當方便。

## 步驟 3：註冊自訂遮蔽函式

AsposeAI 提供 `set_post_processor` 方法，允許你插入任何可呼叫的函式。我們將 `mask_pci` 函式與可選的設定字典（目前為空）一起傳入。

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**背後發生了什麼？**  
稍後呼叫 `run_postprocessor` 時，AsposeAI 會將原始 OCR 結果傳給 `mask_pci`。該函式會收到一個輕量物件 (`data`)，其中包含辨識出的文字，而你則回傳一個新字串。此設計讓核心 OCR 保持不變，同時在單一位置強制執行 **資料清理** 政策。

## 步驟 4：對收據影像執行 OCR

既然引擎已知道如何清理輸出，我們就將影像餵給它。為了本教學的方便，我們假設你已擁有一個已配置語言與解析度設定的 `engine` 物件。

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**提示：** 若尚未有預先配置的物件，可使用以下方式建立：

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` 呼叫會回傳一個物件，其 `text` 屬性包含原始、未遮蔽的字串。

## 步驟 5：套用已註冊的後處理器

取得原始 OCR 資料後，我們將其交給 AI 實例。引擎會自動執行先前註冊的 `mask_pci` 函式。

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**為什麼使用 `run_postprocessor` 而非手動呼叫函式？**  
這樣可保持工作流程的一致性，特別是當你有多個後處理器（例如拼寫檢查、語言偵測）時。AsposeAI 會依註冊順序排隊執行，確保輸出具決定性。

## 步驟 6：驗證已清理的輸出

最後，印出已清理的文字，確認所有信用卡號碼已正確遮蔽。

```python
print(final_result.text)
```

**預期輸出**（節錄）：

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

若收據未包含卡號，文字將保持不變——無需遮蔽，也無需擔心。

## 處理邊緣案例與常見變形

### 同一文件中多筆卡號
若收據包含多於一筆 PAN（例如會員卡加付款卡），正則表達式會全域執行，自動遮蔽所有匹配項目。無需額外程式碼。

### 非標準格式
有時 OCR 會插入空格或連字號（`1234 5678 1234 5678` 或 `1234-5678-1234-5678`）。可擴充模式以忽略這些字元：

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

新增的 `[ -]?` 允許在數字區塊之間出現可選的空格或連字號。

### 國際卡片
對於某些地區使用的 19 位 PAN，可擴大模式：

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

只要記住 **PCI 合規** 仍要求遮蔽中間數字，無論長度為何。

### 記錄遮蔽值（可選）
若需要稽核追蹤，可透過 `custom_settings` 傳遞旗標並調整函式：

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

然後這樣註冊：

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

## 完整可執行範例（可直接複製貼上）

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

在包含 `4111111111111111` 的收據上執行此腳本，將產生：

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

這就是完整的流程——從原始 OCR 到 **資料清理**——只需幾行簡潔的 Python 程式碼即可完成。

## 結論

我們剛剛示範了如何使用 AsposeAI 的後處理掛鉤、簡潔的正則表達式程序，以及一系列 **PCI 合規** 的最佳實踐技巧，來 **遮蔽 OCR 結果中的信用卡號碼**。此解決方案完全獨立，適用於任何 OCR 引擎能讀取的影像，且可擴充以支援更複雜的卡片格式或記錄需求。

準備好下一步了嗎？可將此遮蔽與 **資料庫插入** 程式結合，只儲存最後四位作為參考，或整合 **批次處理器**，於夜間掃描整個收據資料夾。你亦可探索其他 **OCR 後處理** 任務，如地址標準化或語言偵測——皆遵循我們此處使用的相同模式。

對於邊緣案例、效能，或如何將程式碼套用至其他 OCR 函式庫有任何疑問嗎？在下方留言，我們一起討論。祝程式開發愉快，保持安全！

![說明在 OCR 流程中遮蔽信用卡號碼運作方式的圖示](https://example.com/images/ocr-mask-flow.png "OCR 後處理遮蔽流程圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}