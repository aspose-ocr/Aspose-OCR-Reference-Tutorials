---
category: general
date: 2026-09-29
description: 学习如何使用 Python OCR 和 AsposeAI 后处理从 JPG 图像中提取文本，实现可靠的图像转文本转换。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from JPG image
- Python OCR
- AsposeAI post‑processing
- image to text conversion
- optical character recognition python
language: zh
lastmod: 2026-09-29
og_description: 使用 Python OCR 和 AsposeAI 后处理从 JPG 图像提取文本。遵循本完整指南，实现精准的图像转文本转换。
og_image_alt: Python code extracting text from a JPG image with OCR and AI post‑processing
og_title: 使用 Python OCR 从 JPG 图像提取文本——一步步指南
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to extract text from JPG image with Python OCR and AsposeAI
    post‑processing for reliable image‑to‑text conversion.
  headline: How to extract text from JPG image using Python OCR
  type: TechArticle
tags:
- OCR
- Python
- AsposeAI
title: 如何使用 Python OCR 从 JPG 图像中提取文本
url: /zh/python/general/how-to-extract-text-from-jpg-image-using-python-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 从 JPG 图像中提取文本

如果您需要快速 **从 JPG 图像中提取文本**，本指南将展示一个完整的 Python 工作流，结合基础 OCR 与 AI 驱动的校正。教程结束时，您将拥有一个可直接运行的脚本，能够从任何 JPG 照片中输出干净、可搜索的文本。

从 JPG 图像中提取文本是数字化收据、发票或扫描文档的常见需求。本教程涵盖您所需的全部内容：安装 SDK、在 Python 中运行光学字符识别（OCR），以及使用 AsposeAI 后处理来提升准确性。

## 前置条件

在开始之前，请确保您具备以下条件：

- 已安装 Python 3.8 或更高版本。
- 拥有 Aspose.OCR for Python via .NET 包的有效许可证（或免费试用）。
- 要处理的 JPG 文件（将其放在类似 `YOUR_DIRECTORY/sample.jpg` 的文件夹中）。
- 基本熟悉命令行和 Python 虚拟环境。

您无需任何额外的图像处理工具；Aspose OCR 引擎内部已处理 JPEG 解码。

## 步骤 1：运行 OCR 从 JPG 图像中提取文本

第一步是加载图像并运行内置的 OCR 引擎。这会得到一个原始字符串，可能包含误识别，尤其是在低质量照片上。

```python
# Step 1: Load the image and run basic OCR
from aspose.ocr import OcrEngine

# Create an OcrEngine instance
ocr_engine = OcrEngine()

# Load the JPG file you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample.jpg")

# Perform optical character recognition (OCR)
raw_result = ocr_engine.recognize()          # raw_result.text holds the initial recognition
print("Raw OCR output:", raw_result.text)
```

**为什么这样有效：** `OcrEngine` 实现了光学字符识别的 Python 逻辑，扫描每个像素，检测字符边界，并映射到 Unicode 符号。`recognize()` 调用返回一个对象，其 `text` 属性包含原始转录文本。

## 步骤 2：设置 AsposeAI 进行后处理

基础 OCR 往往会留下杂散字符或误检单词。AsposeAI 提供轻量级神经模型，可自动纠正这些错误。启用自动下载可确保在首次运行脚本时获取模型。

```python
# Step 2: Prepare AsposeAI for post‑processing (auto‑download ensures the model is present)
from aspose.ai import AsposeAI

post_processor = AsposeAI()
post_processor.allow_auto_download = "true"
```

**此举的重要性：** `AsposeAI` 类加载预训练语言模型，能够理解上下文、标点和常见 OCR 错误。将 `allow_auto_download` 设置为 `"true"` 可省去手动下载模型的步骤，使脚本更具可移植性。

## 步骤 3：应用基于 AI 的校正以提升 OCR 输出

现在将原始 OCR 结果输入 AI 后处理器。模型返回清理后的文本，修复常见错误，如字符颠倒、缺失空格或大小写错误。

```python
# Step 3: Apply AI‑based correction to improve the OCR output
clean_result = post_processor.run_postprocessor(raw_result)
```

**工作原理：** `run_postprocessor` 分析原始字符串，进行语言模型推断，并输出新的结果对象。`clean_result` 的 `text` 属性保存校正后的转录文本，通常比原始 OCR 输出更为准确。

## 步骤 4：查看校正后的输出

打印最终的 AI 增强文本以验证转换。您也可以将其写入文件以供后续处理。

```python
# Step 4: Display the corrected text
print("Corrected text:", clean_result.text)

# Optional: Save the result to a .txt file
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(clean_result.text)
```

**预期结果：** 对于清晰的收据图像，您可能会看到类似如下内容：

```
Corrected text: Total: $23.45
Date: 2026-09-28
Item 1  Apple   $1.20
Item 2  Bread   $2.50
...
```

AI 后处理器通常会去除杂散符号（`#`、`@`）并恢复正确的换行。

## 步骤 5：清理资源

脚本结束时，释放 AsposeAI 引擎占用的任何本地资源。这可防止长时间运行的应用程序出现内存泄漏。

```python
# Step 5: Release AI resources when done
post_processor.free_resources()
```

**最佳实践：** 在 `finally` 块中始终调用 `free_resources()`，或在将此代码集成到更大服务时使用上下文管理器。

## 常见陷阱与技巧

| 问题 | 原因 | 解决方法 |
|-------|----------------|---------------|
| **Blurry JPG** | 低对比度会降低 OCR 准确性。 | 在第 1 步之前使用 `opencv` 对图像进行预处理以提升对比度。 |
| **Missing language model** | 自动下载被禁用或无网络连接。 | 将 `post_processor.allow_auto_download = "false"`，并手动将模型放置在预期文件夹中。 |
| **Large PDFs split into many JPGs** | 每页都需要单独的 OCR 调用。 | 在目录中遍历文件并将 `clean_result.text` 结果拼接起来。 |
| **Non‑Latin characters** | 默认模型仅针对英文训练。 | 在运行后处理器之前使用 `post_processor.set_language("es")`（或其他受支持的语言）。 |

这些技巧结合了 **Python OCR** 功能和 **AsposeAI 后处理**，使整个 **图像转文本** 流程更加稳健。

## 完整脚本，复制粘贴即可

下面是完整的可运行程序，包含所有步骤和错误处理。

```python
# extract_text_from_jpg.py
import sys
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI

def extract_text(image_path: str, output_path: str = "extracted_text.txt"):
    # Initialize OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.load_image(image_path)

    # Perform basic OCR
    raw_result = ocr_engine.recognize()
    print("Raw OCR output:", raw_result.text)

    # Set up AsposeAI post‑processor
    post_processor = AsposeAI()
    post_processor.allow_auto_download = "true"

    # Run AI correction
    clean_result = post_processor.run_postprocessor(raw_result)

    # Show corrected text
    print("Corrected text:", clean_result.text)

    # Save to file
    with open(output_path, "w", encoding="utf-8") as f:
        f.write(clean_result.text)

    # Release resources
    post_processor.free_resources()

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_text_from_jpg.py <path_to_jpg>")
        sys.exit(1)

    image_file = sys.argv[1]
    extract_text(image_file)
```

在命令行中运行脚本：

```bash
python extract_text_from_jpg.py YOUR_DIRECTORY/sample.jpg
```

程序会打印原始文本和校正后的文本，然后将清理结果写入 `extracted_text.txt`。

## 结论

您现在已经了解如何使用可靠的 Python OCR 工作流并结合 AsposeAI 后处理来 **从 JPG 图像中提取文本**。本指南涵盖了 SDK 的安装、运行光学字符识别（Python）、应用基于 AI 的校正以及清理资源。

从这里您可以：

- 将脚本集成到批处理器中，以处理数十张图像。
- 尝试使用其他 **图像转文本** 库（如 Tesseract）进行对比实验。
- 探索更多 AsposeAI 功能，如特定语言模型或自定义词汇表。

祝编码愉快，尽情将图片转换为可搜索的文本！

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [将图像转换为文本：使用 Aspose OCR (Python) 提取图像文本](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [如何在发票上运行 OCR – 使用 Python 提取图像文本](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}