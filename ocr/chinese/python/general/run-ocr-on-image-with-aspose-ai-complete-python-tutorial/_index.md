---
category: general
date: 2026-07-18
description: 使用 Aspose OCR 在 Python 中对图像进行 OCR。学习从图像中提取纯文本，应用 AI 后处理，快速获得干净的结果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: zh
lastmod: 2026-07-18
og_description: 使用 Aspose OCR 和 Python 对图像进行 OCR。本教程展示了如何从图像中提取纯文本，并通过 AI 后处理器提升准确率。
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: 在图像上运行 OCR – 使用 Aspose AI 的完整 Python 指南
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
title: 使用 Aspose AI 对图像进行 OCR – 完整 Python 教程
url: /zh/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose AI 对图像进行 OCR – 完整 Python 教程

是否曾想过在不与底层 API 纠缠的情况下 **run OCR on image** 文件？你并不孤单。在许多项目中——发票处理、收据扫描或旧文档数字化——从图片中获取干净、可搜索的文本是第一步，也是往往最困难的一步。

在本指南中，我们将通过一个动手示例，展示不仅 **run OCR on image**，还演示如何使用 Aspose 的 OCR 引擎 **extract plain text from image**，随后使用一个小型 AI 后处理器对结果进行润色。完成后，你将拥有一个可直接运行的脚本、对每个环节的清晰理解，以及避免常见陷阱的若干技巧。

![运行 OCR 于图像示例](/images/run-ocr-on-image.png){: .align-center alt="运行 OCR 于图像的控制台输出，显示原始文本和 AI 增强后的文本"}

## 您需要的条件

在开始之前，请确保你拥有：

- 已安装 Python 3.8+（代码在 Windows、macOS 和 Linux 上均可运行）。
- 有效的 Aspose OCR for Python 许可证或免费试用版（该包在 PyPI 上为 `aspose-ocr`）。
- 本地保存的示例图像文件（例如扫描的发票或收据）。
- 可选：如果计划稍后更改 `gpu_layers` 设置，则需要支持 GPU 的机器。

就这些——无需重量级 OCR 引擎，无需外部云调用，只需一次 pip 安装和几行代码。

## 步骤 1：安装 Aspose OCR 包

打开终端并运行：

```bash
pip install aspose-ocr
```

该包会拉取核心 OCR 引擎以及我们在整个教程中使用的轻量级 `aspose.ocr` 命名空间。

## 步骤 2：导入所需类

我们首先引入两个主要类：用于 AI 增强后处理的 `AsposeAI`，以及用于实际文本提取的 `OcrEngine`。

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*为何重要*：`OcrEngine` 承担识别字形的重活，而 `AsposeAI` 让我们在不重写 OCR 核心的情况下挂接自定义逻辑——比如对每个单词进行大写处理。

## 步骤 3：创建 AsposeAI 实例（可选日志记录器）

如果想要详细日志，可以传入自定义 logger，但默认设置对大多数情况已经足够。

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## 步骤 4：微调底层模型（可选）

Aspose OCR 附带默认语言模型，但你可以指向 HuggingFace 仓库或强制使用 CPU 执行。下面我们启用自动下载并选择体积小的 `gpt2` 模型——仅用于演示可调参数。

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **专业提示**：如果拥有 CUDA 兼容的 GPU，可将 `gpu_layers` 提升至 `1` 或 `2`，以获得显著的速度提升。

## 步骤 5：注册简单的后处理器

我们的目标是 **extract plain text from image**，随后让它看起来更美观。下面是一个将每个单词首字母大写的简易函数。你可以将其替换为拼写检查、语言检测，甚至是完整的 LLM 调用。

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

`custom_settings` 字典允许你以后传入额外参数——在演进处理器时非常有用。

## 步骤 6：加载图像并运行 OCR

现在我们终于 **run OCR on image**。我们将获取两种输出形式：

1. **Plain text** – 原始字符串，不包含布局信息。  
2. **Structured text** – 保留列和表格的布局感知文本。

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **为何两者都要？** `plain_text` 适合快速搜索，而 `structured_text` 在需要重建表格或保持列对齐时表现更佳。

## 步骤 7：使用 AI 后处理器增强 OCR 输出

拿到 OCR 结果后，我们将其交给 `AsposeAI.run_postprocessor`。这里会执行前面步骤 5 中的 `capitalize_words` 函数。

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

如果以后想换成更高级的后处理器——比如语法纠正器——只需在步骤 5 中替换函数，流水线的其余部分保持不变。

## 步骤 8：查看结果

让我们并排打印所有内容，便于比较原始 OCR 与 AI 增强版本的差异。

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### 预期输出

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

可以看到，AI 后处理器将全部小写单词转为首字母大写，使文本可读性大幅提升。你可以应用任何想要的转换——这只是概念验证。

## 步骤 9：清理资源

Aspose 会将大型模型文件加载到内存中。完成后请释放它们，以避免内存泄漏，尤其是在长时间运行的服务中。

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## 常见问题与边缘情况

| 问题 | 答案 |
|----------|--------|
| **我可以在循环中对多张图像运行 OCR 吗？** | 当然可以。只需实例化一次 `OcrEngine`，在循环中调用 `load_image`，并复用同一个 `AsposeAI` 实例进行后处理。 |
| **如果图像分辨率低怎么办？** | 在将图像传入 `OcrEngine` 之前，使用 OpenCV 进行预处理（例如 `cv2.resize` 和 `cv2.threshold`）。 |
| **我需要 GPU 吗？** | 不需要。默认的 CPU 模式对大多数文档都足够。仅在拥有兼容的 GPU 并需要加速时，将 `ai.config.gpu_layers` 设置为大于 0。 |
| **如何在其他语言中提取图像的纯文本？** | 在调用 `recognize` 之前，将 `ocr_engine.language = "fr"`（或任何 ISO‑639‑1 代码）更改为相应语言。后处理器仍会运行，但可能需要针对特定语言的逻辑。 |

## 完整可运行脚本

将所有内容组合在一起，下面是完整的、可直接运行的程序：

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

将其保存为 `run_ocr_on_image.py`，将占位路径替换为实际图像路径，然后执行 `python run_ocr_on_image.py`。你应当会看到如上示例的前后对比输出。

## 结论

我们已成功 **run OCR on image** 文件，演示了如何 **extract plain text from image**，并展示了一种使用 AI 后处理器提升可读性的轻量方式。核心模式——OCR

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方案，每篇资源均附完整可运行代码示例和逐步解释。

- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR 的语言选择提取图像文本（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [提取图像文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}