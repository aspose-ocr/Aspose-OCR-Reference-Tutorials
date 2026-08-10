---
category: general
date: 2026-06-25
description: 使用 aocr 函式庫快速取得 OCR 支援的字元。學習如何列出 OCR 字元、設定語言，以及在 Python 中除錯 OCR 引擎。
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: zh-hant
og_description: 使用 aocr 獲取 OCR 支援的字元。本指南將示範如何列出 OCR 字元、選擇語言，以及在 Python 中處理邊緣情況。
og_title: 在 Python 中取得 OCR 支援的字元 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: 取得 Python 支援的 OCR 字元 – 完整指南
url: /zh-hant/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中取得 OCR 支援的字元 – 完整指南

有沒有想過在玩 OCR 引擎時，如何 **取得 OCR 支援的字元** 以對應特定語言？你並不孤單。無論你是在開發收據掃描器或多語言文件解析器，清楚知道引擎能辨識哪些字形都是救命的資訊。在本教學中，我們會一步步說明整個流程——安裝函式庫、設定語言，最後列出那些字元——讓你在幾分鐘內就能除錯並微調 OCR 流程。

我們會使用 **aocr** 函式庫，這是一個輕量的 Python OCR 引擎，能輕鬆查詢語言能力。完成本指南後，你將能 **列出 OCR 字元**、切換 **支援的 OCR 語言**，甚至在生產環境出問題前先發現覆蓋盲點。

---

## 前置條件

在開始之前，請確保你已具備：

* Python 3.8 或更新版本（aocr 套件已不再支援 3.7）
* 可連網的終端機或命令提示字元
* 基本的 Python 腳本知識（只要會寫 `print()` 就行）

不需要額外的外部依賴——只要安裝 `aocr` pip 套件即可。

---

## 安裝 aocr 函式庫（OCR Engine Python）

首先需要一個可運作的 **OCR engine Python** 環境。aocr 套件已上架至 PyPI，只要執行一條 pip 指令即可：

```bash
pip install aocr
```

如果你使用虛擬環境（強烈建議），請先啟動它：

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **小技巧：** 固定版本（`pip install aocr==1.2.4`）可以避免之後因 API 變動而產生的意外。

---

## 選擇語言（Supported OCR Languages）

aocr 內建了數個語言套件。每個套件都定義了引擎可辨識的 Unicode 代碼點。要查詢這些套件，需要在引擎實例上設定 `language` 屬性。

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

你可以把 `aocr.Language.ENGLISH` 換成其他列舉值（`FRENCH`、`GERMAN` 等）。若嘗試指定未隨套件提供的語言，aocr 會拋出 `ValueError`。因此，先檢查 **支援的 OCR 語言** 清單是個好習慣：

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## 取得字元集合（Get OCR Supported Characters）

接下來就是本教學的核心：實際 **取得 OCR 支援的字元**。引擎提供了 `get_supported_characters()` 方法，會回傳單一字元字串的列表。

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

在背後，aocr 會讀取隨語言套件一起打包的 JSON 檔，將每個 Unicode 代碼點轉換成 Python 字串。結果是確定性的，也就是說在相同語言版本下，每次執行腳本都會得到相同的列表。

---

## 顯示支援的字元總數

知道總數能快速判斷覆蓋範圍。以英文為例，通常會看到數千個字元（包含標點與數字）。

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()` 的計算是 O(1)，因為 Python 內部已儲存列表長度，即使是大型字母表也不會造成效能問題。

---

## 預覽前 100 個支援的字元

快速視覺檢查可以讓你確認引擎是否包含所需符號（例如歐元符號或智慧引號）。以下列印前一百個字元：

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join` 會把切片合併成單一字串，比直接印出 Python 列表更易閱讀。

---

## 完整腳本 – 一次搞定所有步驟

以下是完整、可直接執行的範例，將前面的步驟整合在一起。將它存為 `list_supported_chars.py`，然後在終端機執行 `python list_supported_chars.py`。

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**預期輸出（為了篇幅省略）：

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

實際字元總數可能因 aocr 版本略有差異，但你一定會看到一長串字母加上常用標點。

---

## 處理例外情況

### 語言套件遺失時該怎麼辦？

如果請求的語言未隨套件提供，`aocr.Language` 內不會有對應的列舉，會拋出 `AttributeError`。可以先做簡單檢查以避免錯誤：

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### 空字元列表

某些小眾語言可能因訓練資料不完整而回傳空列表。此時可退回預設語言（例如 English）或拋出警告：

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode 正規化

列表中可能會出現組合字元（例如「é」以 `e` + 重音符號表示）。若下游處理需要預組合字形，請先執行正規化步驟：

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## 實務小技巧

* **快取字元列表** – 若要處理成千上萬張影像，於每次迭代都呼叫 `get_supported_characters()` 會增加不必要的開銷。可將列表存於模組層級變數，或序列化為 JSON 供日後重複使用。
* **跨語言驗證** – 當應用同時支援多種語言時，取交集找出共同子集，可協助設計在不同語系下仍保持一致的 UI 元件。
* **除錯 OCR 失敗** – 若引擎將字形辨識錯誤，將問題字元與 `list_supported_chars` 的輸出比對。若缺少該字元，即表示有覆蓋盲點，可能需要自行訓練。
* **結合自訂字型** – aocr 只看 Unicode 範圍，但不同字型的渲染品質會有所差異。請使用與正式環境相同的字型測試支援字元，以免意外。

---

## 常見問題

**Q: 這在 aocr 2.x 版也能用嗎？**  
A: 可以，`get_supported_characters()` 方法在 1.x 與 2.x 皆保持穩定。唯一的變動是語言列舉已移至 `aocr.languages`。

**Q: 我可以取得每個字元的 Unicode 代碼點嗎？**  
A: 當然可以。使用 `ord(ch)` 搭配列表推導式：

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: 那阿拉伯文等從右到左的腳本呢？**  
A: aocr 包含 `ARABIC` 列舉。字元列表會包含阿拉伯字形，但在下游 UI 中可能需要啟用 RTL 渲染。

---

## 結論

現在你已掌握如何使用 aocr 函式庫在 Python 中 **取得 OCR 支援的字元**、切換 **支援的 OCR 語言**，以及為什麼 **列出 OCR 字元** 對於建構穩健的文字辨識管線至關重要。透過完整腳本與上述技巧，你可以快速驗證語言覆蓋、除錯缺失字形，並打造更聰明的 OCR 應用。

準備好下一步了嗎？試著把這份字元清單與自訂詞彙過濾結合，或是改用其他 OCR 引擎（Tesseract、EasyOCR）進行比較。探索得越多，你的 OCR 解決方案就會越完整。

祝程式開發順利，願你的字元集合永遠完整！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能在此基礎上延伸更多技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你熟悉其他 API 功能並探索不同實作方式。

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}