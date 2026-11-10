---
category: general
date: 2026-03-18
description: 快速在 Python 中修正 OCR 錯誤。學習如何清理 OCR、如何清理 OCR 文字、將零 (0) 替換成 O，並應用 Python
  OCR 後處理。
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: zh-hant
og_description: 快速修正 Python 中的 OCR 錯誤。學習如何清理 OCR、將 0 替換為 O，並在單一教學中使用 Python OCR 後處理。
og_title: 在 Python 中修正 OCR 錯誤 – OCR 文字清理指南
tags:
- OCR
- Python
- Text Cleaning
title: 在 Python 中修復 OCR 錯誤 – OCR 文本清理指南
url: /zh-hant/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 修正 Python 中的 OCR 錯誤 – OCR 文字清理指南

曾經盯著掃描過的發票發呆，心想「*要怎樣在把資料寫入資料庫前先修正 OCR 錯誤呢？*」嗎？你並不孤單。在文件自動化的世界裡，單一個讀錯的字元就可能讓整條流水線崩潰，因此學會 **如何清理 OCR** 輸出相當重要。  

在本教學中，你將看到一個實用、端對端的方式，利用一個小型後處理器將數字「0」替換成字母「O」——這是產品代碼中常見的問題。完成後，你即可將此解決方案套入任何 Python OCR 工作流程，獲得更乾淨、更可靠的文字。

> **你將得到：** 完整可執行的 Python 程式碼、每一行程式碼的說明、擴充邏輯的技巧，以及預期輸出的快速驗證。

## 前置條件 — 開始前需要的東西

- Python 3.8 或更新版本（語法相容於所有近期版本）。  
- 基本的 OCR 函式庫（例如透過 `pytesseract` 使用的 Tesseract），能回傳原始字串。  
- 具備 Python 函式與物件的基本概念。  

如果你已經有 OCR 步驟能輸出字串，就可以直接開始——後處理部分不需要額外安裝。

## 步驟 1：建立最小化的 AI‑like 包裝器（為什麼需要它）

在許多專案中，OCR 引擎會被包在一個更大的「AI」類別裡，負責前處理、推論與後處理。為了讓範例自成一體，我們會建立一個小型的 `AIProcessor` 類別，模擬這個模式。這樣可以輕鬆把程式碼放入既有程式碼庫，而不必重寫任何東西。

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**為什麼這很重要：** 把後處理器與 OCR 引擎分離，符合單一職責原則，讓你在不觸碰 OCR 程式碼的情況下，隨時替換清理邏輯。

## 步驟 2：撰寫 **修正 OCR 錯誤** 的函式

現在我們建立本教學的核心：一個 **修正 OCR 錯誤** 的函式，將數字「0」換成字母「O」。此模式適用於產品代碼、序號以及任何 OCR 常把兩者混淆的字母數字識別碼。

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**為什麼要把 0 換成 O：** 在許多字型中，零與大寫 O 幾乎相同，導致 OCR 常猜錯。提前修正後，下游的驗證（例如正規表達式檢查）才能如預期運作。

## 步驟 3：將後處理器掛載到 AI 實例

有了包裝器與清理函式，我們把它們結合。這與在生產環境中註冊自訂後處理器的方式相同。

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

如果日後需要 **如何清理 OCR** 輸出以因應其他語言或資料格式，只要再寫一個函式並再次呼叫 `set_post_processor` 即可——不必改動管線其他部分。

## 步驟 4：輸入原始 OCR 文字並取得清理後的結果

先模擬一段包含「0」的原始 OCR 字串。實際情況下，你會把占位符換成 `pytesseract.image_to_string(image)` 或類似的呼叫。

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**預期輸出**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

可以看到零已被轉換成大寫 O，得到的字串符合大多數庫存系統的格式要求。

## 步驟 5：擴充邏輯 – 真實情境的變化

上述簡單的替換只能解決單一情況，實務上會遇到其他怪癖：

| 常見錯誤 | OCR 範例 | 期望修正 | 加入方式 |
|----------|----------|----------|----------|
| 「1」被讀成「I」 | `I23` | `123` | `text = text.replace('I', '1')` |
| 「5」被讀成「S」 | `S9` | `59` | `text = text.replace('S', '5')` |
| 多餘空白 | `  ABC  ` | `ABC` | `text = text.strip()` |
| 大小寫混淆 | `oRder` | `Order` | `text = text.title()` |

你可以在 `correct_ocr_errors` 中加入上述任意規則。務必保持每個轉換 **冪等**（執行兩次不會改變結果），以免意外破壞資料。

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**小技巧：** 若手上有有效代碼的目錄，考慮使用正規表達式或查表方式驗證清理後的字串。這一步能捕捉到單純字元替換無法處理的剩餘 OCR 錯誤。

## 步驟 6：與實際 OCR 引擎整合（可選）

以下示範如何把後處理器接入真實的 OCR 流程，使用 `pytesseract`。此部分為可選，但能說明完整的端對端管線。

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **注意：** `pytesseract` 需要系統已安裝 Tesseract OCR。只要將執行檔加入 PATH，以上程式碼在 Windows、macOS 與 Linux 都能正常運作。

## 步驟 7：以程式方式驗證結果

在大量批次自動化時，確認清理步驟如預期執行相當重要。簡單的單元測試能在日後省下大量除錯時間。

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

執行此測試即可驗證函式 **修正 OCR 錯誤** 的一致性，即使有額外空格也能正確處理。

## 圖示說明

以下是管線的視覺草圖（關鍵字已放在 alt 文字中以利 SEO）。

![修正 OCR 錯誤管線圖 – 顯示原始 OCR 輸入至後處理器，將 0 替換為 O]()

## 結論 – 我們完成了什麼

我們一步步走過完整、可執行的範例，示範了 **如何清理 OCR** 輸出於 Python，特別是 **將零換成 O** 以及 **修正 OCR 錯誤** 的模組化後處理方式。透過將清理邏輯與 OCR 引擎分離，你可以獲得彈性、可測試性，以及未來加入其他規則（例如 *如何清理 OCR* 的其他字元混淆）的明確位置。

準備好下一步了嗎？試著為產品代碼加入正規表達式驗證、實作模糊匹配以處理噪聲文字，或探索像 `ocrmypdf` 這類已內建後處理掛鉤的完整套件。我們所介紹的模式具備良好擴充性，無論是處理少量發票或是數百萬份掃描文件，都能輕鬆應對。

---

*祝程式開發順利，願你的 OCR 流程永遠無錯！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}