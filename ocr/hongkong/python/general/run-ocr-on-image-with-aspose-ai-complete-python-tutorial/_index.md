---
category: general
date: 2026-07-18
description: 使用 Aspose OCR 於 Python 執行圖像 OCR。學習如何從圖像中提取純文字、套用 AI 後處理，快速獲得乾淨的結果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: zh-hant
lastmod: 2026-07-18
og_description: 使用 Aspose OCR 與 Python 進行圖片 OCR。此教學示範如何從圖片中提取純文字，並透過 AI 後處理器提升準確度。
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: 對圖像執行 OCR – 完整 Python 指南與 Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: 使用 Aspose AI 於圖像執行 OCR – 完整 Python 教學
url: /zh-hant/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在影像上執行 OCR（Aspose AI） – 完整 Python 教學

有沒有想過如何在不與低階 API 纏鬥的情況下**在影像上執行 OCR**？您並不孤單。在許多專案——發票處理、收據掃描或舊文件數位化——從圖片取得乾淨、可搜尋的文字往往是第一步，也是最困難的一步。

本教學將帶您一步步實作範例，不僅**在影像上執行 OCR**，還示範如何使用 Aspose 的 OCR 引擎**從影像中提取純文字**，並以小型 AI 後處理器進行潤飾。完成後，您將擁有可直接執行的腳本、對每個環節的清晰了解，以及避免常見陷阱的幾項技巧。

![執行 OCR 影像範例](/images/run-ocr-on-image.png){: .align-center alt="執行 OCR 後的主控台輸出，顯示原始文字與 AI 增強文字"}

## 您需要的環境

- 已安裝 Python 3.8 以上（程式碼可在 Windows、macOS 與 Linux 上執行）。
- 有效的 Aspose OCR for Python 授權或免費試用（套件名稱為 PyPI 上的 `aspose-ocr`）。
- 本機已儲存的範例影像檔（例如掃描的發票或收據）。
- 可選：若稍後要調整 `gpu_layers` 設定，請使用具 GPU 的機器。

就這樣——不需要大型 OCR 引擎，也不需呼叫外部雲端服務，只要一次 pip 安裝與幾行程式碼即可。

## 步驟 1：安裝 Aspose OCR 套件

在終端機中執行以下指令：

```bash
pip install aspose-ocr
```

此套件會同時安裝核心 OCR 引擎以及我們在整個教學中會使用的輕量級 `aspose.ocr` 命名空間。

## 步驟 2：匯入必要的類別

我們先匯入兩個主要類別：`AsposeAI` 用於 AI 增強的後處理，`OcrEngine` 用於實際的文字擷取。

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*為什麼這很重要*：`OcrEngine` 負責辨識字形的繁重工作，而 `AsposeAI` 讓我們能掛接自訂邏輯（例如將每個單字大寫），無需重新編寫 OCR 核心。

## 步驟 3：建立 AsposeAI 實例（可選的記錄器）

若需要詳細日誌，可傳入自訂 logger；但預設設定已足以應付大多數情況。

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## 步驟 4：微調底層模型（可選）

Aspose OCR 內建預設語言模型，但您可以指向 HuggingFace 儲存庫或強制使用 CPU 執行。以下示範啟用自動下載並選擇小型 `gpt2` 模型——僅用於說明可調整的參數。

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **專業小技巧**：若您擁有支援 CUDA 的 GPU，將 `gpu_layers` 提升至 `1` 或 `2` 可顯著加速。

## 步驟 5：註冊簡易後處理器

我們的目標是**從影像中提取純文字**，並讓其更易閱讀。以下是一個將每個單字大寫的簡易函式，您也可以改為拼字檢查、語言偵測，甚至完整的 LLM 呼叫。

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

`custom_settings` 字典允許您之後傳入額外參數——在演進處理器時相當有用。

## 步驟 6：載入影像並執行 OCR

現在我們終於**在影像上執行 OCR**。我們會取得兩種輸出形式：

1. **純文字** – 不含版面資訊的原始字串。  
2. **結構化文字** – 具版面感知，保留欄位與表格。

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **為什麼兩者都要？** `plain_text` 適合快速搜尋，`structured_text` 則在需要重建表格或保持欄位對齊時表現更佳。

## 步驟 7：使用 AI 後處理器增強 OCR 輸出

取得 OCR 結果後，我們將其傳給 `AsposeAI.run_postprocessor`，此時先前的 `capitalize_words` 函式會被執行。

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

若日後想換成更進階的後處理器（例如文法校正），只需在第 5 步更換函式，其餘流程保持不變。

## 步驟 8：檢視結果

讓我們將結果並排印出，方便比較原始 OCR 與 AI 增強版的差異。

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### 預期輸出

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

請注意 AI 後處理器將全小寫的單字轉為大寫，使文字更易閱讀。您可以套用任何想要的轉換——這僅是概念驗證。

## 步驟 9：清理資源

Aspose 會將大型模型檔載入記憶體。完成後請釋放它們，以避免記憶體洩漏，尤其在長時間執行的服務中。

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## 常見問題與邊緣情況

| 問題 | 解答 |
|----------|--------|
| **我可以在迴圈中對多張影像執行 OCR 嗎？** | 當然可以。只需先實例化一次 `OcrEngine`，在迴圈內呼叫 `load_image`，並重複使用相同的 `AsposeAI` 實例進行後處理。 |
| **如果影像解析度太低怎麼辦？** | 在送入 `OcrEngine` 前，可使用 OpenCV 進行前處理（例如 `cv2.resize` 與 `cv2.threshold`）。 |
| **我需要 GPU 嗎？** | 不需要。預設的 CPU 模式已能滿足大多數文件。只有在擁有相容的 GPU 且需要加速時，才將 `ai.config.gpu_layers` 設為大於 0。 |
| **如何在其他語言中從影像提取純文字？** | 在呼叫 `recognize` 前，將 `ocr_engine.language = "fr"`（或任何 ISO‑639‑1 代碼）改為目標語言。後處理器仍會執行，但可能需要語言特定的邏輯。 |

## 完整可執行腳本

將上述所有步驟整合，以下是完整、可直接執行的程式碼：

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

將其儲存為 `run_ocr_on_image.py`，將佔位路徑替換為實際影像路徑，然後執行 `python run_ocr_on_image.py`。您應該會看到如上範例的前後輸出。

## 結論

我們已成功使用 Aspose OCR **在影像檔上執行 OCR**，示範了如何 **從影像中提取純文字**，並展示了使用 AI 後處理器提升可讀性的輕量方式。核心模式——OCR

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以示範的技術為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 從影像提取文字 – 步驟教學](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR 於 C# 提取影像文字並選擇語言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [從影像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}