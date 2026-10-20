---
category: general
date: 2026-06-22
description: 如何快速變更 OCR 引擎的語言。學習使用簡單程式碼設定阿拉伯語 (ar) OCR 語言，並避免常見陷阱。
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: zh-hant
og_description: OCR 引擎的語言變更方法在第一句說明。跟隨此教學即可快速設定阿拉伯語 OCR 語言。
og_title: 如何在 OCR 中更改語言 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: 如何在 OCR 中更改語言 – 逐步設定阿拉伯語
url: /zh-hant/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 OCR 中更改語言 – 完整程式指南

在處理多語言文件時，如何更改 OCR 引擎的語言是一個常見的障礙。在本教學中，我們將逐步說明如何將 OCR 語言設定為阿拉伯語，並提供可執行的程式範例以及每一行的說明。如果你曾經想過 *“如何將 OCR* 設定為不同的文字系統而不破壞流程*」，那麼你來對地方了*。

我們將涵蓋所有你需要的內容：必備的函式庫、如何取得 OCR 引擎實例、如何存取其設定，最後安全地變更 OCR 語言。完成後，你將能只透過一次方法呼叫，就把語言從英文切換到阿拉伯語（或任何其他支援的語言）。沒有魔法，只有清晰的程式碼與實用的小技巧。

## 前置條件

- Python 3.8+（或任何較新版本）
- 一個能公開設定物件的 OCR 函式庫 – 本範例使用 **pytesseract** 包裝在一個小型輔助類別中，但相同模式也適用於其他引擎，如 EasyOCR 或 Microsoft 的 Computer Vision SDK。
- 已為 OCR 引擎安裝阿拉伯語語言資料（`ara.traineddata` 供 Tesseract 使用）。  
  *Pro tip:* 在 Ubuntu 上可使用 `sudo apt-get install tesseract-ocr-ara` 安裝。

## 如何在 OCR 中更改語言 – 概觀

變更語言本質上是一個三步驟的流程：

1. **取得 OCR 引擎實例** – 這通常是單例或由工廠產生的物件。  
2. **取得設定物件** – 大多數函式庫會將語言、DPI 以及其他選項放在獨立的設定容器中。  
3. **設定語言代碼** – 阿拉伯語的 ISO‑639‑2 代碼為 `"ar"`。

以下是一個最小且可完整執行的腳本，示範上述步驟。

![如何在 OCR 中更改語言的螢幕截圖](image-placeholder.png "如何在 OCR 中更改語言的範例")

## 第一步：建立或取得 OCR 引擎實例

首先我們需要一個引擎。在實際專案中，引擎可能在其他地方建立並傳遞；為了說明清楚，我們就在此處實例化它。

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**為何要包裝引擎** – 許多 OCR SDK（包括 Tesseract）在每次呼叫時都需要以字串傳遞語言。透過將選項封裝在設定物件中，我們得到一個乾淨的、*how to set OCR*‑風格 API，與你提供的原始程式碼片段相呼應。

## 第二步：存取引擎的設定物件

現在我們已有引擎，接著取得它的設定。這與原始範例的第二行 (`settings = engine.get_settings()`) 相同。

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

此處我們透過 `set_language` 讓 **how to set OCR** 語言可被存取。此方法同時執行基本的合理性檢查，是良好的防禦式程式設計習慣。

## 第三步：將 OCR 語言設定為阿拉伯語 (ocr language arabic)

最後，我們以阿拉伯語代碼 `"ar"` 呼叫此方法。這就是 *change OCR language* 操作的核心。

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**預期輸出**

```
Current OCR language: ar
```

如果你取消註解 `recognize` 呼叫並指向真實的阿拉伯語影像，只要已安裝語言資料，就會在主控台上看到阿拉伯文字。

## 如何為多種語言設定 OCR

有時候你需要 *ocr language arabic* **加上** 英文，特別是混合文件。`set_language` 方法可以接受以 `+` 分隔的清單：

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Edge case*: 若請求的語言套件未安裝，Tesseract 會拋出類似 `Error opening language file` 的錯誤。為避免程式當機，你可以捕捉例外並回退至預設語言。

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## 在執行時動態變更 OCR 語言

在許多應用程式中，使用者會從下拉選單選擇語言。因為設定存在於引擎物件內，你可以在不重新實例化引擎的情況下即時切換語言。

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

此模式同時滿足 *set language OCR* 的需求，且保持程式碼整潔。

## 常見陷阱與專業提示

| 陷阱 | 會發生什麼 | 解決方式 |
|------|------------|----------|
| 語言套件遺失 | Tesseract 回傳 “Failed loading language ‘ar’” | 安裝語言資料 (`sudo apt-get install tesseract-ocr-ara` 或從官方倉庫下載)。 |
| 使用錯誤的 ISO 代碼 | 無輸出或出現亂碼 | 確認代碼 (`ar` 代表阿拉伯語，`eng` 代表英文，`chi_sim` 代表簡體中文)。 |
| 忘記重新建構設定 | 引擎仍使用舊語言 | 必須呼叫 `engine._build_config()`（在呼叫 `recognize` 時會自動處理）。 |
| 傳入清單而非字串 | TypeError | 使用單一字串 `"ar+eng"`，而非 `["ar", "eng"]`。 |

## 完整可執行範例（全部組合在一起）

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

使用 `python full_example.py` 執行腳本。若環境設定正確，將會看到：

```
Current OCR language: ar
```

…以及在啟用最後兩行程式碼後，對你的阿拉伯語影像產生的 OCR 輸出。

## 結論

你現在已掌握 **如何在 OCR 中更改語言** 的技巧，特別是使用乾淨且可重用的模式將 OCR 語言設定為阿拉伯語。本指南說明了取得引擎、存取設定，最後套用語言變更的完整流程，涵蓋了 *ocr language arabic* 情境以及更廣泛的 *change OCR language* 用例。

接下來的步驟是什麼？嘗試加入更多語言支援、實驗多語言字串（`"ar+eng"`），或將此邏輯整合到讓使用者上傳任意文字腳本文件的 Web 服務中。如果你對其他函式庫（EasyOCR、Google Vision）中的 *set language OCR* 感興趣

## 接下來該學什麼？

以下教學與本指南所示技術密切相關，能進一步擴展你的能力。每個資源都包含完整可執行的程式範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}