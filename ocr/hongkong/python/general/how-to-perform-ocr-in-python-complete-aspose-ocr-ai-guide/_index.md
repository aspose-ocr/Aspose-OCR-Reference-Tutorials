---
category: general
date: 2026-06-25
description: 學習如何在 Python 中執行 OCR，並發掘載入影像以進行 OCR 的最佳方法，然後透過 Aspose AI 後處理提升準確度。
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: zh-hant
og_description: 如何在 Python 中執行 OCR？請跟隨本指南載入影像進行 OCR、執行基本辨識，並透過 Aspose AI 後處理提升結果。
og_title: 如何在 Python 中執行 OCR – 完整的 Aspose OCR 與 AI 教學
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: 如何在 Python 中執行 OCR – 完整的 Aspose OCR 與 AI 指南
url: /zh-hant/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中執行 OCR – 完整的 Aspose OCR 與 AI 指南

有沒有想過 **如何在 Python 中執行 OCR**，卻不想與低階的影像技巧糾纏？你並不孤單。在本教學中，我們將逐步說明如何載入影像以進行 OCR、執行純文字擷取，然後使用 Aspose 的 AI 後處理器來潤飾輸出。完成後，你將擁有一個即用的腳本，能將雜訊掃描檔轉換為乾淨、可搜尋的文字——不需要額外的服務。

我們會涵蓋從安裝 SDK 到在長時間執行的應用程式中釋放資源的全部內容。如果你曾嘗試 **load image for OCR** 卻得到一團亂碼，這本指南就是解藥。你將會了解為何將傳統 OCR 與語言模型結合，能產生看起來像人手打出的結果。

## 前置條件

- Python 3.9 或更新版本（程式碼使用型別提示，較舊的直譯器不支援）
- 有效的 Aspose OCR 授權或免費試用版（社群版可用於評估）
- 若想加速 AI 模型，需具備至少 4 GB VRAM 的 GPU（可選，但很不錯）
- 範例影像，例如 `sample_invoice.png`，放置於可參考的位置

如果上述任一項目聽起來陌生，別慌——安裝 SDK 只需一行指令，GPU 設定之後也可以關閉。

## 步驟 1：安裝 Aspose OCR 與相依套件

在終端機中執行以下指令：

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

第一個套件會安裝 `aspose.ocr`，第二個則加入 AI 後處理工具。兩者皆為純 Python wheel，無需自行編譯。

## 步驟 2：載入影像以進行 OCR 並初始化引擎

現在我們將使用 Aspose 的 `OcrEngine` **load image for OCR**。可以把它想像成把紙張交給一位非常認真的文員，讓他閱讀每一個字元。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **為何重要：** `load_image` 呼叫是檔案系統與 OCR 引擎之間的橋樑。如果路徑錯誤，會在任何辨識開始前拋出 `FileNotFoundError`。務必再次確認目錄分隔符，特別是在 Windows 與 macOS/Linux 之間的差異。

## 步驟 3：設定 Aspose AI 後處理器

Aspose AI 能從 Hugging Face 下載語言模型，並在本機快取，於 GPU（或 CPU）上執行推論。以下我們設定一個輕量級的 30 億參數模型，適用於大多數現代筆記型電腦。

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **提示：** 若使用僅有 CPU 的機器，將 `gpu_layers = 0`。模型仍會執行，只是稍慢。`int8` 量化可將記憶體佔用降到極低，同時保留大部分模型精度。

## 步驟 4：註冊自訂後處理器

AI 模型需要一段提示詞來告訴它要執行什麼。此處我們請它充當 OCR 校對員，修正拼寫錯誤、合併斷裂的單詞，並移除雜訊。

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **為何使用自訂處理器？** 預設的後處理器可能會加入額外說明或格式，這些你可能不需要。透過提供自訂函式，我們能確保輸出僅為清理過的文字，非常適合後續索引或資料庫儲存。

## 步驟 5：執行 AI 強化的 OCR 流程

現在我們將原始 OCR 輸出送入 AI 層。引擎會呼叫我們的 `correction_processor`，進而與語言模型互動。

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

你應該會看到明顯的改善：缺失的字元被還原，常見的 OCR 誤讀（例如 “0” 與 “O”）被校正，且換行變得更合乎邏輯。

## 步驟 6：清理 – 釋放資源

如果你打算在 Web 服務或長時間執行的守護程序中使用此程式，釋放 GPU 記憶體相當重要。忘記呼叫 `free_resources` 可能會在數百次請求後導致「記憶體不足」的崩潰。

```python
ocr_ai.free_resources()
```

就這樣——你的完整 OCR 流程已經可以投入生產使用。

## 完整腳本回顧

以下是完整且可執行的範例。將其複製貼上至名為 `ocr_with_ai.py` 的檔案，調整影像路徑，然後執行 `python ocr_with_ai.py`。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### 預期輸出

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

請留意 “Inv0ice” 被修正為 “Invoice”，且金額後多餘的 “O” 消失。這就是 AI 的魔法。

## 常見問題與邊緣案例

### 如果我沒有 GPU 該怎麼辦？

將 `model_config.gpu_layers = 0`，並可選擇將 `model_config.context_size` 提升至 2048，以提升 CPU 效能。模型會較慢，但仍能得到相同品質的校正。

### 我的影像是旋轉的——`load_image` 能處理嗎？

Aspose OCR 會自動偵測方向，但對於極度傾斜的掃描，你可能需要先使用 Pillow 進行預先旋轉：

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### 如何處理資料夾中的多個檔案？

將整個流程包在 `for` 迴圈中，將每個 `enhanced_text` 存入清單或直接寫入 CSV。請記得在迴圈結束後 **一次** 呼叫 `ocr_ai.free_resources()`，而不是每個檔案後呼叫——重複重新初始化模型會浪費資源。

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### 我可以更換語言模型嗎？

當然可以。只要將 `model_config.hugging_face_repo_id` 改為 Hugging Face 上任何支援 GGUF 的模型（例如 `Meta/Llama-3.2-1B-Instruct-GGUF`），並確保量化設定與你的硬體相容。

## 專業提示與陷阱

- **專業提示：** 設定 `temperature=0.0` 以取得確定性的校正。較高的 temperature 可能會產生創意但不正確的變更。
- **注意：** 極長的文件（> 5000 字元）。範例中模型的上下文視窗限制為 1024 個 token；在送入 AI 前請先將文字切分為段落。
- **安全說明：** 若在受管制的環境中執行，請確保模型下載 URL 已列入白名單。`allow_auto_download` 旗標可以

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}