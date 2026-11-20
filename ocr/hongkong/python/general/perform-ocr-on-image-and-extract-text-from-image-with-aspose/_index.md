---
category: general
date: 2026-11-20
description: 使用 Aspose OCR 進行影像文字辨識，然後使用內建 AI 後處理器從影像中提取文字。只需數分鐘即可學會完整的 Python 工作流程。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: zh-hant
lastmod: 2026-11-20
og_description: 使用 Aspose OCR 進行圖像文字辨識，然後透過 AI 後處理從圖像中提取文字。請遵循此一步一步的 Python 指南。
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: 使用 Aspose 進行圖像 OCR 並提取文字
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: 使用 Aspose 在圖像上執行 OCR 並提取文字
url: /zh-hant/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 在圖像上執行 OCR 並提取文字

如果您需要在 Python 中 **perform OCR on image** 檔案，本指南將為您展示完整的端對端解決方案。結合 Aspose OCR 與 Aspose AI 後處理器，您可以可靠地 **extract text from image** 檔案，並使用輕量級語言模型提升原始 OCR 輸出。

在本教學中，您將會：

* 設定 Aspose OCR 引擎。
* 執行 OCR 以 **extract text from image**。
* 可選地設定 AI 模型以進行後處理。
* 註冊自訂後處理函式。
* 產生增強文字並清理資源。

這些步驟適用於任何點陣圖像（PNG、JPEG、BMP），且僅需 `aspose-ocr` 套件。

## Prerequisites

在開始之前，請確保您已具備：

| 需求 | 原因 |
|------|------|
| Python 3.8+ | Aspose SDK 所需的版本。 |
| `aspose-ocr` pip package | 提供 `AsposeOCR`、`AsposeAI` 以及模型設定類別。 |
| 圖像檔案（例如 `sample_image.png`） | 您將 **perform OCR on image** 的來源。 |
| 可選：GPU 支援 | 如果您打算在 GPU 上執行較大的模型，請相應設定 `gpu_layers`。 |

使用以下指令安裝 SDK：

```bash
pip install aspose-ocr
```

## 步驟 1：在圖像上執行 OCR

第一個操作是讀取圖像並取得原始文字。這是核心 **perform OCR on image** 步驟。

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**為什麼這樣可行：** `AsposeOCR.recognize_image` 會執行一個已預訓練的光學字符辨識模型，針對常見字型在速度與準確度上進行最佳化。此方法回傳純 Unicode 字串，作為後續處理的基礎。

> **專業提示：** 若圖像包含多種語言，請在呼叫 `recognize_image` 前設定 `ocr_engine.language = "eng+spa"`（或任何支援的 ISO‑639‑2 代碼）。

## 步驟 2：初始化 AI 後處理器

Aspose AI 提供輕量級的後處理層，可清理 OCR 錯誤、校正標點，或套用自訂商業邏輯。

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**為什麼需要它：** 原始 OCR 常會誤認字符（例如 “0” 與 “O”），AI 步驟會精練輸出，使 **extract text from image** 結果在索引或分析等下游任務中更可靠。

## 步驟 3：（可選）設定 AI 模型

您可以將處理器指向特定的 Hugging Face 模型、啟用自動下載，或強制使用 CPU 執行。此步驟為可選，但在需要確定性行為時相當有用。

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**說明：**  
* `allow_auto_download` 讓您免於手動管理模型。  
* `hugging_face_repo_id` 用於選擇模型；`gpt2` 在尺寸與品質之間取得良好平衡，適用於短文字校正。  
* `gpu_layers` 控制在 GPU 上執行的 transformer 層數；`0` 會強制僅使用 CPU，適用於所有機器。

## 步驟 4：註冊自訂後處理函式

Aspose AI 允許您插入任何可呼叫的函式，該函式接收原始 OCR 字串並回傳轉換後的版本。以下是一個簡單範例，將所有文字轉為大寫。

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**何時自訂：** 當您需要領域特定的清理時，例如剔除機密識別碼、正規化日期，或套用正則表達式校正，可使用自訂函式。AI 模型會在此函式 *之後* 執行，讓您結合確定性規則與機率性改進。

## 步驟 5：使用 AI 後處理器增強 OCR 結果

現在執行完整管線：原始 OCR 文字先經過您的自訂函式，接著經過 AI 模型，最後得到精練的輸出。

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**您應該看到的結果：**  
若原始圖像包含 “Hello world”，控制台可能顯示：

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

在實際情境中，AI 模型會校正拼寫錯誤、補足缺失的標點，或重新格式化換行，為您提供更乾淨的 **extract text from image** 結果，方便儲存或分析。

## 步驟 6：完成後釋放資源

OCR 引擎與 AI 後處理器皆會分配原生資源。明確釋放可避免記憶體泄漏，特別是在長時間執行的服務中。

```python
# Clean up native resources
ai_processor.free_resources()
```

若您同時以較重的後端實例化 `ocr_engine`，亦可以相同方式呼叫 `ocr_engine.dispose()`（若支援）。

## 常見變化與邊緣案例

| 情境 | 建議調整 |
|------|----------|
| **大量頁面的 PDF** | 逐頁迴圈，對每個點陣化頁面呼叫 `recognize_image`，並彙總結果。 |
| **GPU 啟用環境** | 設定 `model_config.gpu_layers` 為您希望在 GPU 上執行的層數（例如 `4`）。確保已安裝 CUDA 驅動程式。 |
| **非英文文字** | 將 `ocr_engine.language` 改為相應的語言代碼，必要時選擇語言專屬的 Hugging Face 模型。 |
| **極度噪聲的掃描件** | 在呼叫 `recognize_image` 前，使用 OpenCV 進行影像前處理（去噪、二值化）。 |
| **需要保留原始大小寫** | 將 `my_post_processor` 函式改為不做任何操作或使用更細緻的規則，而非 `text.upper()`。 |

## 完整範例

將所有步驟整合在一起，以下是一個可直接執行的單一腳本（將 `YOUR_DIRECTORY/sample_image.png` 替換為實際檔案路徑）：

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

執行此腳本會同時印出原始 OCR 輸出與 AI 增強版，示範如何在單一、可重現的工作流程中 **perform OCR on image** 檔案並可靠地 **extract text from image**。

## 結論

您現在已掌握如何使用 Aspose OCR **perform OCR on image**，再透過內建的 AI 後處理器 **extract text from image**。本教學涵蓋：

* 初始化 OCR 引擎。
* 執行 OCR 以取得原始文字。
* （可選）設定輕量級 Hugging Face 模型。
* Adding a

## 接下來該學什麼？

以下教學與本指南示範的技術緊密相關，提供完整的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 與 AI 提取圖像文字 – 完整步驟指南](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [如何校正 OCR 錯誤 – 使用 Aspose OCR 提取圖像文字 – 步驟指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Python 圖像文字提取 – 完整 Aspose OCR 教學](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}