---
category: general
date: 2026-08-15
description: 如何快速在 Python 中进行 OCR。学习从 PNG 中提取文本，加载图像进行 OCR，并通过 AI 后处理提升 OCR 准确率。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from PNG
- improve OCR accuracy
- load image for OCR
language: zh
lastmod: 2026-08-15
og_description: 在第一句中解释了如何在 Python 中执行 OCR。请按照本教程从 PNG 图像中提取文本、加载图像进行 OCR，并通过 AI 后处理提升准确性。
og_image_alt: How to perform OCR example output displayed in a Python console
og_title: 如何在 Python 中进行 OCR——开发者完整指南
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: How to perform OCR in Python quickly. Learn to extract text from PNG,
    load image for OCR, and improve OCR accuracy with AI post‑processing.
  headline: How to perform OCR in Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- AI post‑processing
title: 如何在 Python 中进行 OCR——一步步指南
url: /zh/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中执行 OCR – 步骤指南

在需要将扫描的文档或收据数字化时，如何在 Python 中执行 OCR 是一个常见需求。在本教程中，你将学习如何从 PNG 文件中提取文本、加载图像进行 OCR，以及通过使用 AI 驱动的后处理器来提升 OCR 准确度。

你将看到一个完整、可运行的示例：从加载图像开始，运行基础 OCR 引擎，最后得到 AI 增强的文本。无需查阅外部文档——只需按照步骤操作，复制代码并在你的机器上运行即可。

## 前置条件

在开始之前，请确保你已具备：

* 已安装 Python 3.9 或更高版本。
* `ocr-engine` 包（可替代任意 OCR 库，如 Aspose.OCR、Tesseract‑wrapper 等）。
* 提供 `run_postprocessor` 方法的 AI 辅助库（例如轻量级的 OpenAI 包装器）。
* 放置在已知目录中的示例 PNG 图像（例如 `sample_invoice.png`）。

你可以使用以下命令安装所需的包：

```bash
pip install ocr-engine ai-helper
```

> **专业提示：** 如果你倾向于使用开源 OCR 引擎，可将 `ocr-engine` 替换为 `pytesseract` 并相应调整代码。整体流程保持不变。

## 第一步：创建 OCR 引擎实例

首要任务是实例化 OCR 引擎。该对象负责底层图像分析和字符识别。

```python
from ocr_engine import OcrEngine   # Replace with your actual OCR library import

# Initialize the OCR engine
engine = OcrEngine()
```

一次性创建引擎并在多张图像之间复用，可减少初始化开销并确保设置一致。

## 第二步：加载待识别的图像

正确的文件格式加载至关重要。这里演示加载 PNG 图像，这是扫描发票和收据的常见格式。

```python
import os

# Define the path to the PNG file you want to process
image_path = os.path.join("YOUR_DIRECTORY", "sample_invoice.png")

# Load the image into the OCR engine
engine.load_image(image_path)
```

`load_image` 方法将文件读取到内存并为识别做好准备。如果找不到文件，引擎会抛出信息丰富的异常，便于你优雅地处理缺失文件的情况。

## 第三步：执行基础 OCR 操作

图像加载完成后，调用 OCR 引擎的 `recognize` 方法。该方法返回包含原始文本的结果对象。

```python
# Run the OCR process
plain_result = engine.recognize()

# Display the raw OCR output
print("Raw OCR:", plain_result.text)
```

输出通常包含换行符以及偶发的误识别，尤其是在低分辨率扫描时。此时，你已经成功 **从 PNG 中提取文本**，完成了基础 OCR 流程。

### 预期的原始输出（示例）

```
Raw OCR: Invoice #12345
Date: 2023/07/15
Total: $1,234.56
```

## 第四步：使用 AI 后处理器提升 OCR 文本

基础 OCR 在噪声背景、特殊字体或手写笔记面前可能表现不佳。AI 后处理器可以清理原始字符串、纠正拼写错误，甚至重新格式化数据。

```python
from ai_helper import AIHelper   # Replace with your actual AI helper import

# Initialize the AI helper (assumes you have set up API keys elsewhere)
ai = AIHelper()

# Run the AI‑based post‑processor on the raw OCR text
enhanced_text = ai.run_postprocessor(plain_result.text)

# Show the AI‑enhanced result
print("AI‑enhanced OCR:", enhanced_text)
```

AI 模型会分析原始字符串，修正常见 OCR 错误（例如 “1,234.56” → “1,234.56”），并可推断缺失的字段。

### 预期的增强输出（示例）

```
AI‑enhanced OCR: Invoice #12345
Date: 2023‑07‑15
Total: $1,234.56
```

通过此步骤，你 **提升了 OCR 准确度**，而无需调节引擎的底层参数。

## 完整可运行脚本

将所有代码片段组合在一起，即可得到一个可直接执行的脚本：

```python
import os
from ocr_engine import OcrEngine          # OCR library
from ai_helper import AIHelper             # AI post‑processing library

def main():
    # 1️⃣ Create OCR engine
    engine = OcrEngine()

    # 2️⃣ Load PNG image
    image_path = os.path.join("YOUR_DIRECTORY", "sample_invoice.png")
    engine.load_image(image_path)

    # 3️⃣ Basic OCR
    plain_result = engine.recognize()
    print("Raw OCR:", plain_result.text)

    # 4️⃣ AI post‑processing
    ai = AIHelper()
    enhanced_text = ai.run_postprocessor(plain_result.text)
    print("AI‑enhanced OCR:", enhanced_text)

if __name__ == "__main__":
    main()
```

将文件保存为 `ocr_demo.py` 并运行：

```bash
python ocr_demo.py
```

你应当在控制台看到原始 OCR 结果和 AI 增强后的 OCR 结果。

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| **如果图像不是 PNG 格式怎么办？** | 大多数 OCR 库都支持 JPEG、BMP 或 TIFF。只需在 `image_path` 中更改文件扩展名，并确保引擎支持该格式。 |
| **如何处理多页 PDF？** | 首先将每页转换为 PNG（或其他光栅格式），随后遍历各页并使用相同脚本进行处理。 |
| **可以批量处理大量图像吗？** | 可以——将逻辑包装在 `for` 循环中，遍历 PNG 文件所在的目录。复用同一个 `engine` 实例可提升性能。 |
| **如果 AI 辅助库抛出错误怎么办？** | 在 `run_postprocessor` 周围捕获异常，回退到原始 OCR 文本，并记录失败以供后续审查。 |

## 结论

本指南教会你 **如何在 Python 中执行 OCR**：从加载 PNG 图像、提取文本，到使用 AI 后处理器 **提升 OCR 准确度**。完整脚本展示了端到端的工作流，帮助你立即将其集成到更大的自动化流水线中。

接下来，可进一步探索：

* 在批量模式下 **从 PNG 中提取文本**，用于大型文档档案。
* 高级 **加载图像进行 OCR** 技术，如图像预处理（去倾斜、去噪）以提升基线准确率。
* 针对特定文档布局定制的 AI 模型，可在通用后处理之外进一步 **提升 OCR 准确度**。

祝编码愉快，尽情享受可靠 OCR 与 AI 的强大结合！

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在已有技术之上进一步拓展。每个资源均提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索替代实现方式。

- [将图像转换为文本：使用 Aspose OCR（Python）提取图像文本](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [图像文本提取 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}