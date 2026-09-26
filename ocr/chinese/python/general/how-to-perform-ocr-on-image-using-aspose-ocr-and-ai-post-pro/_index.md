---
category: general
date: 2026-09-25
description: 学习如何使用 Aspose OCR 对图像进行 OCR，加载图像进行 OCR，并在完整的 Python 示例中识别收据中的文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: zh
lastmod: 2026-09-25
og_description: 使用 Aspose OCR 在 Python 中对图像进行 OCR。本指南展示了如何加载图像进行 OCR，并通过 AI 增强识别收据中的文本。
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: 使用 Aspose OCR 和 AI 后处理器对图像进行 OCR – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: 如何在 Python 中使用 Aspose OCR 和 AI 后处理器对图像进行 OCR
url: /zh/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 Aspose OCR 和 AI 后处理器对图像执行 OCR

如果您需要在 Python 中 **对图像执行 OCR**，本教程提供了一个完整、可直接运行的解决方案。您将学习如何 **加载图像进行 OCR**、运行 Aspose OCR 引擎，以及使用可选的 AI 驱动后处理器 **从收据文档中识别文本**。

我们将逐步演示，从安装 SDK 到释放资源，帮助您在自己的应用中集成可靠的文本提取，而不会遗漏任何细节。

## 前置条件

在开始之前，请确保您具备以下条件：

- 已安装 Python 3.8+  
- 通过 pip 安装 Aspose OCR for Python (`pip install aspose-ocr`)  
- 有可用的网络连接以下载可选的 AI 模型  
- 将示例收据图像 (`receipt.png`) 放置在已知目录下  

无需额外的外部服务；代码在本地运行，并在有 GPU 层时使用免费的 Qwen2‑3B‑Instruct 模型。

## 第一步：安装所需的包

```bash
pip install aspose-ocr
```

`aspose-ocr` 包同时包含我们将用于 **对图像执行 OCR** 的 `OcrEngine` 类和 `AsposeAI` 后处理器。

## 第二步：创建并配置 OCR 引擎 – 加载图像进行 OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

调用 `load_image` 告诉引擎要分析哪个文件。您可以将路径替换为任意 PNG、JPG 或 TIFF 文件，以 **对图像执行 OCR**。

## 第三步：设置可选的 AsposeAI 后处理器

AI 后处理器可以在返回原始 OCR 结果后纠正拼写、改进格式或应用自定义逻辑。

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

该配置指示处理器下载默认的 Qwen2 模型，使您能够 **对图像执行 OCR** 时拥有更高层次的语言理解。

## 第四步：附加一个简单的后处理函数

您可以插入任何接受原始文本并返回校正后文本的可调用对象。下面是一个修正常见拼写错误的最小示例：

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

由于函数已注册，每次调用 `run_postprocessor` 时，OCR 输出都会经过此步骤。

## 第五步：运行 OCR 并增强结果 – 从收据中识别文本

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

`recognize` 调用返回一个对象，其 `text` 属性包含从收据图像中提取的原始字符。随后调用 `run_postprocessor` 会返回一个新结果，其中已应用我们的拼写检查（以及任何基于模型的改进）。

### 预期输出

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

请注意，AI 增强的文本修正了拼写错误并插入了换行，以提升可读性——这正是您在 **从收据中识别文本** 时所需要的。

## 第六步：清理资源

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

在长时间运行的服务中处理大量图像时，释放资源尤为重要。

## 完整可运行脚本

将所有代码片段组合在一起，即可得到一个可以复制、粘贴并执行的单文件脚本：

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

运行脚本：

```bash
python ocr_receipt.py
```

您应该会在控制台看到原始输出和 AI 增强后的输出。

## 专业提示与常见坑点

- **图像质量很重要** – 确保收据图像光线充足且未过度压缩；否则 OCR 引擎可能漏字符，削弱后处理的效果。  
- **GPU 可用性** – 如果机器没有兼容的 GPU，请将 `gpu_layers=0` 设置为强制使用 CPU 推理；模型仍可运行，只是速度较慢。  
- **自定义后处理器** – 您可以链式调用多个函数，或使用更复杂的语言模型来重新格式化日期、金额或商家名称。  
- **批量处理** – 实例化单个 `AsposeAI` 对象并在多个 `OcrEngine` 实例之间复用，以避免重复下载模型。  

## 结论

现在，您已经掌握了如何使用 Aspose OCR 对 **图像执行 OCR**、如何 **加载图像进行 OCR**，以及如何通过 AI 驱动的增强 **从收据中识别文本**。按照上述步骤，您可以在任何 Python 应用中集成高精度、高吞吐量的收据处理。

**后续步骤**：探索货币标准化等更多后处理技术，将结果集成到数据库，或切换到更大的模型以支持多语言收据。欲进行更深度的自定义，请参阅 Aspose OCR 文档中的自定义语言包和高级图像预处理章节。

祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每个资源均提供完整可运行的代码示例和逐步解释。

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Perform OCR in C# – Extract Text from Image Using Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}