---
category: general
date: 2026-11-20
description: 使用 Aspose OCR 对图像进行 OCR，然后使用内置的 AI 后处理器提取图像中的文本。几分钟内学习完整的 Python 工作流。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: zh
lastmod: 2026-11-20
og_description: 使用 Aspose OCR 对图像进行 OCR，然后通过 AI 后处理提取图像中的文本。请遵循此一步一步的 Python 指南。
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: 使用 Aspose 对图像执行 OCR 并提取图像中的文本
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
title: 使用 Aspose 对图像执行 OCR 并提取图像中的文本
url: /zh/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 对图像执行 OCR 并提取图像中的文本

如果您需要在 Python 中 **perform OCR on image** 文件，本指南为您展示一个完整的端到端解决方案。结合 Aspose OCR 与 Aspose AI 后处理器，您可以可靠地 **extract text from image** 文件，并使用轻量级语言模型改进原始 OCR 输出。

在本教程中，您将：

* 设置 Aspose OCR 引擎。
* 运行 OCR 以 **extract text from image**。
* 可选地配置用于后处理的 AI 模型。
* 注册自定义后处理函数。
* 生成增强文本并清理资源。

这些步骤适用于任何光栅图像（PNG、JPEG、BMP），仅需 `aspose-ocr` 包。

## 前置条件

在开始之前，请确保您拥有：

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose SDK 所需的版本。 |
| `aspose-ocr` pip package | 提供 `AsposeOCR`、`AsposeAI` 和模型配置类。 |
| An image file (e.g., `sample_image.png`) | 您将 **perform OCR on image** 的源文件。 |
| Optional: GPU support | 如果计划在 GPU 上运行更大的模型，请相应设置 `gpu_layers`。 |

安装 SDK：

```bash
pip install aspose-ocr
```

## 步骤 1：对图像执行 OCR

第一步是读取图像并获取原始文本。这是核心的 **perform OCR on image** 步骤。

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

**为什么这样有效：** `AsposeOCR.recognize_image` 运行一个预训练的光学字符识别模型，针对常见字体在速度和准确性上进行了优化。该方法返回普通的 Unicode 字符串，作为后续处理的基线。

> **小贴士：** 如果图像包含多种语言，请在调用 `recognize_image` 之前设置 `ocr_engine.language = "eng+spa"`（或任何受支持的 ISO‑639‑2 代码）。

## 步骤 2：初始化 AI 后处理器

Aspose AI 提供轻量级的后处理层，可清理 OCR 错误、纠正标点或应用自定义业务逻辑。

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**为什么需要它：** 原始 OCR 常常误识字符（例如 “0” 与 “O”）。AI 步骤对输出进行精炼，使 **extract text from image** 结果在索引或分析等下游任务中更可靠。

## 步骤 3：（可选）配置 AI 模型

您可以将处理器指向特定的 Hugging Face 模型，启用自动下载，或强制使用 CPU 执行。此步骤为可选，但在需要确定性行为时很有用。

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

**说明：**  
* `allow_auto_download` 为您省去手动管理模型的工作。  
* `hugging_face_repo_id` 用于选择模型；`gpt2` 在体积与质量之间是短文本纠正的良好折中。  
* `gpu_layers` 控制在 GPU 上运行的 transformer 层数；`0` 强制纯 CPU 执行，适用于所有机器。

## 步骤 4：注册自定义后处理函数

Aspose AI 允许您接入任意可调用对象，该对象接收原始 OCR 字符串并返回转换后的版本。下面是一个将所有内容转换为大写的简单示例。

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

**何时自定义：** 当您需要特定领域的清理时使用自定义函数，例如剥离机密标识符、标准化日期或应用基于正则表达式的纠正。AI 模型将在此函数 *之后* 运行，使您能够将确定性规则与概率改进相结合。

## 步骤 5：使用 AI 后处理器增强 OCR 结果

现在运行完整的流水线：原始 OCR 文本首先通过您的自定义函数，然后通过 AI 模型，最终得到精炼的输出。

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**您应该看到的结果：** 如果原始图像包含 “Hello world”，控制台可能显示：

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

在实际场景中，AI 模型会纠正拼写错误、添加缺失的标点或重新格式化换行，从而为您提供更干净的 **extract text from image** 结果，便于存储或分析。

## 步骤 6：完成后释放资源

OCR 引擎和 AI 后处理器都会分配本机资源。显式释放它们可避免内存泄漏，尤其在长时间运行的服务中。

```python
# Clean up native resources
ai_processor.free_resources()
```

如果您使用了重量级后端实例化 `ocr_engine`，也可以以同样方式调用 `ocr_engine.dispose()`（如果可用）。

## 常见变体和边缘情况

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Large PDFs with many pages** | 对每页循环，针对每个光栅化页面调用 `recognize_image`，并汇总结果。 |
| **GPU‑enabled environment** | 将 `model_config.gpu_layers` 设置为希望在 GPU 上运行的层数（例如 `4`）。确保已安装 CUDA 驱动。 |
| **Non‑English text** | 将 `ocr_engine.language` 更改为相应的语言代码，并在需要时选择特定语言的 Hugging Face 模型。 |
| **Very noisy scans** | 在调用 `recognize_image` 前使用 OpenCV 对图像进行预处理（去噪、阈值化）。 |
| **Need to keep original casing** | 将 `my_post_processor` 函数替换为空操作或更细致的规则，而不是 `text.upper()`。 |

## 完整工作示例

将所有内容整合在一起，以下是一个可以直接运行的完整脚本（将 `YOUR_DIRECTORY/sample_image.png` 替换为实际文件路径）：

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

运行此脚本会打印原始 OCR 输出和 AI 增强版，演示了如何在单一、可复现的工作流中 **perform OCR on image** 文件并可靠地 **extract text from image**。

## 结论

您现在了解如何使用 Aspose OCR **perform OCR on image** 文件，然后使用内置的 AI 后处理器 **extract text from image**。本教程涵盖了：

* 初始化 OCR 引擎。
* 运行 OCR 获取原始文本。
* （可选）配置轻量级 Hugging Face 模型。
* 添加一个

## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方式。

- [使用 Aspose OCR 与 AI 提取图像文本 – 完整分步指南](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [如何纠正 OCR 错误 – 使用 Aspose OCR 提取图像文本 – 分步指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Python 提取图像文本 – 完整 Aspose OCR 指南](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}