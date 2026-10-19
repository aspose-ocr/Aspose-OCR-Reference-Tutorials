---
category: general
date: 2026-06-19
description: 學習如何在 Python 中使用 Aspose OCR 及 AI 後處理器對圖像執行光學字符識別。包括自動下載模型、拼寫檢查及 GPU 加速。
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: zh-hant
og_description: 使用 Aspose OCR 與 AI 後處理器對圖像執行 OCR。逐步指南，包含自動下載模型、拼寫檢查與 GPU 加速。
og_title: 在圖像上執行 OCR – 完整 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: 使用 Aspose AI 於圖像執行 OCR – 完整 Python 指南
url: /zh-hant/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整 Python 教程

有沒有想過如何 **在圖像上執行 OCR** 而不必與大量函式庫糾纏？依我之見，痛點通常是先要對原始 OCR 引擎摸索，然後再處理雜訊輸出。幸好，Aspose OCR for Python 搭配其 AI 後處理器，整個流程就變得輕鬆。

在本指南中，我們將逐步示範一個實務、端到端的範例，說明如何 **在圖像上執行 OCR**、使用自動下載的模型提升準確度、啟用拼寫檢查，甚至在有可用的 GPU 時使用加速。完成後，你將擁有一個可重複使用的腳本，能直接套用於發票、收據掃描或文件數位化專案。

## 你將建立的內容

我們會製作一個小型 Python 程式，功能如下：

1. 初始化 Aspose OCR 引擎並載入範例發票圖像。  
2. 執行基本 OCR 並印出原始文字。  
3. 使用 **Aspose AI** 並從 Hugging Face **自動下載模型**。  
4. 執行 **AI 後處理器**（包含 **拼寫檢查後處理器**）以清理 OCR 輸出。  
5. 清潔地釋放所有資源。

不需要外部服務、API 金鑰——只要幾行 Python 程式碼與 Aspose 的威力。

> **專業提示：** 若你的機器配備了不錯的 GPU，設定 `gpu_layers` 可以為後處理步驟省下數秒時間。

## 前置條件

- Python 3.8 或更新版本（程式碼使用型別提示，但非必須）。  
- 透過 `pip` 安裝 `aspose-ocr` 與 `aspose-ai` 套件。  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- 一張範例圖像（PNG、JPG 或 TIFF），放在可參考的位置，例如 `sample_invoice.png`。  
- （可選）具備 CUDA 支援的 GPU 以及相應驅動程式，若想使用 **GPU 加速**。

基礎建設完成後，讓我們深入程式碼。

![在圖像上執行 OCR 示例](image.png)

## 在圖像上執行 OCR – 步驟 1：初始化 OCR 引擎並載入圖像

首先，我們需要一個 OCR 引擎實例。Aspose OCR 提供乾淨、物件導向的 API，將低階圖像前處理抽象化。

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**為何重要：**  
提前設定語言可告訴引擎預期的字元集，從而提升辨識速度與準確度。若處理多語言文件，只需將 `"en"` 換成 `"fr"`、`"de"` 等相應語言代碼即可。

## 步驟 2：執行基本 OCR 並檢視原始文字

現在正式執行辨識。結果物件會包含原始文字、信心分數，甚至在需要時提供邊界框資訊。

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

典型輸出可能如下（留意偶爾出現的錯讀字元）：

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

你會看到零 (`0`) 被誤讀為字母 “O”。這正是 **AI 後處理器** 發揮作用的地方。

## 設定 Aspose AI – 自動下載模型與拼寫檢查

在將原始 OCR 結果交給 AI 層之前，我們必須告訴 Aspose AI 使用哪個模型。此函式庫能自動從 Hugging Face 下載模型，免除自行管理大型 `.bin` 檔案的麻煩。

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**設定說明**

| 設定 | 功能說明 | 何時調整 |
|------|----------|----------|
| `allow_auto_download` | 允許 Aspose 在首次執行時自動取得模型。 | 除非已離線預先下載，否則保持 `true`。 |
| `hugging_face_repo_id` | Hugging Face 上模型的識別碼。 | 若需特定領域模型，可替換為其他 repo ID。 |
| `hugging_face_quantization` | 選擇量化等級（`int8`、`float16` 等）。 | 記憶體受限時使用 `int8`，追求更高精度則用 `float16`。 |
| `gpu_layers` | 在 GPU 上執行的 transformer 層數。 | 設為 `0` 代表僅使用 CPU，或設定為模型總層數上限（Qwen2.5‑3B 為 20）。 |

## 在 OCR 結果上執行 AI 後處理器

引擎就緒後，只需將原始 OCR 輸出送入 AI 流程。內建的 **拼寫檢查後處理器** 會校正明顯的錯字，若稍後啟用其他處理器，語言模型亦能重新措辭或補齊缺失資訊。

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

拼寫檢查步驟後的預期輸出：

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

可見零已被正確轉為字母，且錯拼的 “Am0unt” 變成了 “Amount”。**AI 後處理器** 透過將原始文字送入選定模型，返回依模型訓練結果精煉過的版本。

### 邊緣案例與技巧

- **低解析度圖像**：若 OCR 引擎表現不佳，可先使用 `Pillow` 放大圖像，或提升 `ocr_engine.ImagePreprocessingOptions`。  
- **非拉丁文字**：將 `ocr_engine.Language` 改為相應的 ISO 代碼（例如中文使用 `"zh"`，阿拉伯文使用 `"ar"`）。  
- **未偵測到 GPU**：若找不到相容的 GPU，`gpu_layers` 會自動回退至 CPU，無需額外錯誤處理。  
- **模型大小限制**：Qwen2.5‑3B 模型壓縮後約 4 GB，請確保磁碟有足夠空間供自動下載。

## 釋放資源 – 清潔關閉

Aspose 物件持有原生句柄，完成後釋放它們是良好慣例。這可防止記憶體泄漏，尤其在長時間服務中更為重要。

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

若喜歡明確的清理方式，可將整個腳本包在 `try…finally` 區塊中。

## 完整腳本 – 直接複製貼上

以下是完整程式碼，請將 `YOUR_DIRECTORY` 替換為圖像所在路徑後即可執行。

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

執行方式：

```bash
python perform_ocr_on_image.py
```

執行後，你應該會在主控台看到原始與清理後的輸出。

## 結論


## 接下來該學什麼？

以下教學與本指南的技巧密切相關，提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}