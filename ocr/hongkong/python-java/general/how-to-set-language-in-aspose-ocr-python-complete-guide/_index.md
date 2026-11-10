---
category: general
date: 2026-01-12
description: 如何在 Aspose OCR Python 中設定語言並使用自訂字典從圖像提取文字。開發人員逐步教學。
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: zh-hant
og_description: 如何在 Aspose OCR Python 中設定語言，並使用自訂字典從圖片中提取文字。只需數分鐘即可學會完整工作流程。
og_title: 如何在 Aspose OCR Python 中設定語言 – 完整指南
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 如何在 Aspose OCR Python 中設定語言 – 完整指南
url: /zh-hant/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose OCR Python 中設定語言 – 完整指南

有沒有想過在 Python 中使用 Aspose OCR 時 **如何設定語言**？你並不孤單——許多開發者在預設的英語模型無法辨識產品代碼、序號或多語言文字時會卡關。好消息是解決方案既簡單又強大。在本教學中，我們將逐步說明如何設定語言、加入自訂字典、從影像中擷取文字，最後處理影像以獲得最佳 OCR 效果。

我們會涵蓋所有必備知識：從安裝函式庫到執行完整範例並印出擷取的文字。完成後，你將能自信地 **從影像擷取文字**，即使內容包含不尋常的代碼或混合語言。

## 前置條件

* 已安裝 Python 3.8+（程式碼使用 f‑strings，較舊版本無法執行）。
* 具備有效的 Aspose OCR for Python 授權或免費試用金鑰。
* 透過 `pip install asposeocr` 安裝 `asposeocr` 套件。
* 準備一張包含欲讀取文字的範例影像（`product_label.png`）。

如果你已具備上述條件，太好了——讓我們繼續。如果還沒有，請前往 Aspose 官方網站取得免費試用，並執行安裝指令，整個過程只需一分鐘。

## 步驟 1：匯入 Aspose OCR 模組

首先，你需要將 OCR 類別匯入腳本中。這是之後 **如何設定語言** 的基礎。

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Pro tip:** 將匯入語句放在檔案最上方。這樣可以讓程式碼更易於瀏覽，尤其是日後回顧時。

## 步驟 2：如何設定語言

預設情況下，Aspose OCR 會假設使用英語。如果影像中包含法語、德語或其他語言，你必須告訴引擎使用哪種語言。這時主要關鍵字就派上用場了。

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

為什麼這麼重要？OCR 引擎依賴語言特定的字元模型。提供正確的語言可大幅提升辨識精度，尤其是帶有重音符號或語言專屬連字的情況。

> **Note:** 若需同時支援多種語言，可傳入類似 `ocr.Language.ENGLISH | ocr.Language.SPANISH` 的組合。

## 步驟 3：如何加入字典（使用者自訂詞彙）

有時 OCR 會誤讀像 “AB‑1234” 這樣的產品代碼。你可以透過自訂字典提升信心，直接回應 **如何加入字典** 的需求。

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

引擎會將這些詞視為「已知」詞彙，並優先匹配，而非相似的字元。這對 SKU 編號、序列碼或不屬於自然語言的品牌名稱特別有用。

## 步驟 4：如何處理影像

現在引擎已配置完成，你需要載入欲分析的影像。這說明了 **如何處理影像** 的乾淨且可重複的做法。

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

如果要處理 PDF，可先將每頁轉為影像——Aspose OCR 內建支援此功能。

## 步驟 5：如何從影像擷取文字

所有設定就緒後，最後一步是執行 OCR 並取得文字。這正是 **如何從影像擷取文字** 的核心。

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

執行腳本時，你應該會看到類似以下的輸出：

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

如果輸出呈現亂碼，請再次確認已設定正確的語言，且自訂字典中包含了預期的字串。

## 完整可執行範例

將上述步驟整合起來，以下是完整腳本，你可以直接複製貼上為 `extract_label.py`。別忘了將 `YOUR_DIRECTORY` 替換成實際的影像路徑。

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### 預期輸出

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

若看到字典中加入的代碼正確顯示，代表你已成功掌握 **如何設定語言**、**如何加入字典**，以及 **如何從影像擷取文字** 的技巧。

## 處理常見邊緣情況

| Situation | What to Do |
|-----------|------------|
| **影像模糊** | 使用 `ocr.Image.apply_filter()` 進行前處理，以在呼叫 `process()` 前銳化影像。 |
| **單一影像中有多種語言** | 設定 `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`。 |
| **大型 PDF** | 逐頁迴圈，將每頁轉換為 `ocr.Image`，並對每頁呼叫 `process()`。 |
| **非預期字元** | 將它們加入使用者自訂詞彙清單；Aspose OCR 會將其視為高信心的標記。 |

## 視覺參考

![如何在 Aspose OCR 中設定語言示例](image.png "螢幕截圖顯示在 Aspose OCR Python 示例中設定語言的屬性")

*Alt text:* **如何設定語言** 螢幕截圖說明在 Python IDE 中設定 language 屬性的方式。

## 結論

現在你已了解如何在 Aspose OCR Python 中 **設定語言**、如何 **加入字典**，以及 **從影像擷取文字** 與 **處理影像** 的完整步驟，以取得最佳結果。上述完整範例可直接套用於任何專案，依需求調整語言或擴充為批次處理或 PDF 輸入。

準備好接受下一個挑戰了嗎？試著將 `ocr.Language.ENGLISH` 換成 `ocr.Language.FRENCH`，觀察法語標籤的辨識提升。或是使用 `set_user_defined_words` 方法加入整個產品目錄——你的 OCR 引擎會將每個條目視為高信心匹配。

祝程式開發順利，願你的 OCR 結果永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}