---
category: general
date: 2026-09-22
description: 学习如何使用 Aspose OCR 对图像进行 OCR，配置 OCR 模型，从发票中提取文本，并在 Python 中提升 OCR 准确率。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: zh
lastmod: 2026-09-22
og_description: 使用 Aspose OCR 对图像进行 OCR，配置 OCR 模型，从发票中提取文本，并在完整的分步教程中提升 OCR 准确率。
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: 使用 Aspose OCR 对图像进行 OCR – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: 如何使用 Aspose OCR 对图像进行文字识别并提升准确率
url: /zh/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 对图像进行 OCR 并提升准确率

如果您需要在 Python 中 **run OCR on image** 文件，本指南将向您展示一个完整的、可投入生产的工作流。您将了解如何配置 OCR 模型、从发票图片中提取文本，以及使用 Aspose 的 AI 后处理器提升 OCR 准确率。

处理扫描的发票是一个常见的痛点——原始 OCR 往往会返回拼写错误的单词或断开的数字。完成本教程后，您将拥有一个可直接运行的脚本，能够提供更清晰、更可靠的文本提取，并且您将了解每个配置步骤的意义。

## 前置条件

* 已安装 Python 3.8 或更高版本。
* 有效的 Aspose OCR 许可证（免费试用可用于评估）。
* 一张示例发票图片（例如 `sample_invoice.png`），放置在已知目录中。
* 基本了解 Python 包的安装。

无需额外的系统级依赖；SDK 会自动处理模型下载。

## 步骤 1：安装 Aspose OCR 包

您首先需要将 Aspose OCR 库添加到您的环境中。该包自带 AI 模型和后处理器，后者将在后续使用。

```bash
pip install aspose-ocr
```

运行此命令会安装 `asposeocr`，它提供了 `AsposeAI` 类，用于 **configure OCR model** 设置，例如自动下载和仅 CPU 执行。

## 步骤 2：配置 OCR 模型（可选但推荐）

微调模型可以提升速度和准确率，尤其是在对包含大量数字和特殊字符的发票图像进行 OCR 时。以下代码演示了最有用的设置：

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*为什么使用这些标志？*  
* `allow_auto_download` 确保即使在全新机器上也会拥有 OCR 模型。  
* `gpu_layers = 0` 取消对 CUDA 兼容 GPU 的需求，而多数开发者并没有 GPU。  
* `context_size` 控制 AI 在纠错时考虑的周围 token 数量；更大的窗口通常能 **improve OCR accuracy**，尤其是对发票等密集文本。

## 步骤 3：初始化 AI 引擎

初始化会验证模型文件已就绪并将其加载到内存中。跳过此步骤可能导致在后续调用后处理器时出现运行时错误。

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

如果引擎初始化失败，异常会明确指出问题所在，帮助您节省调试时间。

## 步骤 4：在图像上运行标准 OCR 引擎

现在您可以 **run OCR on image** 文件了。`OcrEngine` 类执行原始文本提取，不包含任何基于 AI 的校正。

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` 保存 OCR 引擎识别的纯字符串。对于典型的发票，您可能会看到缺失的数字、错位的标点或断开的单词。

## 步骤 5：应用 AI 后处理器提升 OCR 准确率

Aspose 的 AI 后处理器会分析原始输出并修复常见的 OCR 错误（例如 “5um” → “Sum”）。执行此步骤是对金融文档 **improve OCR accuracy** 的关键。

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

后处理器使用您在步骤 2 中设置的配置，因此更大的 `context_size` 有助于更可靠的校正。

## 步骤 6：从发票中提取文本并显示结果

此时您拥有两种提取的文本版本：原始 OCR 输出和 AI 增强版。打印两者可以让您验证改进效果，同时也方便将原始数据记录用于审计。

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Typical output**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

请注意 AI 步骤纠正了零与一的混淆并修复了金额格式——这正是您在 **extract text from invoice** 文件时所需的改进。

## 步骤 7：释放资源

最后，释放 AI 引擎使用的本地资源。这在长期运行的服务或批处理作业中尤为重要。

```python
# Release resources when finished
ai.free_resources()
```

如果忽略此调用，可能会导致内存泄漏，因为底层模型在本地代码中运行。

## 完整脚本，复制粘贴即可

下面是完整可运行的程序，包含上述所有步骤。请将 `YOUR_DIRECTORY` 替换为您图像文件的实际路径。

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

将其保存为 `process_invoice.py` 并运行：

```bash
python process_invoice.py
```

您应该会在控制台看到原始文本和校正后的文本，确认您已成功 **run OCR on image**、**configured OCR model**，并为发票提取任务 **improved OCR accuracy**。

## 常见问题与边缘情况

| 问题 | 答案 |
|----------|--------|
| *如果模型下载失败怎么办？* | 确保您的机器能够访问互联网，并且 `allow_auto_download` 标志已设置为 `"true"`。您也可以从 Aspose 门户手动下载模型，并通过 `ai.model_path = "path/to/model"` 将 `AsposeAI` 指向本地文件夹。 |
| *我可以在 GPU 上运行吗？* | 可以。将 `ai.gpu_layers` 设置为正整数（例如 `2`），并安装相应的 CUDA 库。GPU 执行可以加速大批量处理，但需要兼容的 GPU。 |
| *如何处理文件夹中的大量发票？* | 将核心逻辑包装在遍历 `os.listdir(folder)` 的循环中。请记得仅在循环结束后调用 `ai.free_resources()`，而不是每处理完一个文件后调用，以保持模型加载状态。 |
| *后处理器对非英文发票安全么？* | 默认模型是基于英文文本训练的。对于其他语言，请下载相应的语言包并设置 `ai.language = "fr"`（或相应的 ISO 代码）。 |
| *如果 OCR 结果为空怎么办？* | 确认 `image_path` 指向可读取的图像且文件未损坏。您也可以增大 `ai.context_size`，为低质量扫描提供更多上下文。 |

## 后续步骤

既然您已经能够 **run OCR on image** 并可靠地 **extract text from invoice** 文件，请考虑以下扩展：

* **批量处理** – 将脚本与 `multiprocessing` 结合，以并行处理数千张发票。  
* **数据验证** – 使用正则表达式在提取后验证发票号码、日期和金额。  
* **与数据库集成** – 将清理后的文本直接存入 PostgreSQL 或 MongoDB，以供后续分析。  
* **自定义模型微调** – 如果您拥有大量专有数据集，可训练特定领域模型并将 `ai.model_path` 指向该模型，以获得更高的准确率。  

通过尝试这些思路，您可以将简单的 OCR 演示转变为满足生产需求的稳健文档处理流水线。

---

*您现在已经了解如何使用 Aspose OCR 对图像文件进行 OCR、为获得最佳性能配置 OCR 模型，以及使用 AI 后处理器提升 OCR 准确率。将这些步骤应用于您自己的发票处理工作流，享受更清晰、更可靠的文本提取。*

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在发票上运行 OCR – 使用 Python 从图像提取文本](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [将图像转换为文本：使用 Aspose OCR (Python) 提取图像文本](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}