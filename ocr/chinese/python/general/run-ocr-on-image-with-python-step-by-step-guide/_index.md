---
category: general
date: 2026-08-12
description: 使用 Python 和 Aspose AI 对图像进行 OCR，提取图像中的文本，并通过拼写检查后处理器提升 OCR 准确率。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: zh
lastmod: 2026-08-12
og_description: 在 Python 中对图像进行 OCR，并即时提取图像文字，同时使用 Aspose AI 后处理提升 OCR 准确率。
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: 使用Python对图像进行OCR——完整教程
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 使用 Python 对图像进行 OCR – 逐步指南
url: /zh/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中对图像进行 OCR – 步骤指南

如果您需要在 Python 中**对图像运行 OCR**，本指南将带您完成整个工作流程。您将学习如何**从图像中提取文本**，应用**OCR 文本校正**，以及仅用几行代码**提升 OCR 准确率**。

处理扫描的文档、收据或截图时，往往会得到噪声较多的文本。通过附加拼写检查后处理器，您可以将原始 OCR 输出转换为干净、可搜索的内容，而无需切换到其他工具。本教程涵盖您所需的全部内容——从加载图像到显示校正结果。

## 前置条件

* 已安装 Python 3.9 或更高版本。
* 能够访问 Aspose.OCR 和 Aspose.AI Python 包（或其等价的开源包装器）。
* 在已知目录中放置示例图像（例如 `sample.png`）。
* 对 Python 函数和面向对象代码有基本了解。

您可以使用 pip 安装所需的库：

```bash
pip install aspose-ocr aspose-ai
```

> **专业提示：** 使用虚拟环境（`python -m venv .venv`）来保持依赖隔离。

## 步骤 1：对图像运行 OCR – 创建引擎实例

第一步是创建一个 `OcrEngine` 对象。该对象封装了 OCR 引擎的配置，并提供图像处理和识别的方法。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

一次创建引擎并在多张图像间复用，可减少启动开销，并确保整个会话期间设置保持一致。

## 步骤 2：加载图像进行 OCR

在进行识别之前，引擎必须知道要分析哪张图片。`load_image` 方法接受文件路径或二进制流。

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **为什么重要：** 正确加载图像是实现准确 OCR 的基础。提供高分辨率图像（300 dpi 或更高）通常会**提升 OCR 准确率**，因为引擎能够更清晰地区分字符。

## 步骤 3：从图像提取文本 – 执行基础识别

图像加载后，您可以调用 `recognize()` 获取结果对象。该结果包含原始文本、置信度分数，以及可选的每个单词的边界框。

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

此时，您已经成功**对图像运行 OCR**并提取了原始字符。然而，文本可能包含拼写错误，尤其是低质量扫描时。

## 步骤 4：OCR 文本校正 – 附加后处理拼写检查器

Aspose AI 提供灵活的后处理管道。通过接入自定义拼写检查器，您可以纠正常见的 OCR 错误（例如 “l” 与 “1”、 “O” 与 “0”）。

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**拼写检查器的工作原理：** `MySpellChecker` 应实现 `process(text: str) -> str` 方法。在内部，您可以使用诸如 `pyspellchecker` 或 `symspellpy` 等库，将不太可能的词序列替换为字典验证的替代词。

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## 步骤 5：显示原始和校正后的 OCR 文本

最后，对比原始输出和校正后的输出。这有助于您验证 **OCR 文本校正** 是否真正 **提升了 OCR 准确率**。

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### 预期输出

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

校正后的行显示拼写检查器替换了常见的 OCR 误识别（`Th1s` → `This`，`s4mpl3` → `simple`，`rec3pt` → `receipt`，`som3` → `some`，`err0rs` → `errors`）。

## 步骤 6：提升 OCR 准确率 – 最佳实践清单

即使使用了后处理，您仍然可以提升 OCR 引擎的基线质量：

| Checklist item | Why it helps |
|----------------|--------------|
| **使用高分辨率图像（≥300 dpi）** | 更多像素数据可降低字符歧义。 |
| **将彩色图像转换为灰度** | 去除可能混淆引擎的色度噪声。 |
| **应用图像去倾斜** | 校正倾斜文字，防止换行错误。 |
| **显式设置语言/地区** | 引导识别器使用正确的字符集。 |
| **启用语言模型**（如果库支持） | 提供上下文感知的预测，进一步**提升 OCR 准确率**。 |

您可以在将图像传递给 `ocr_engine` 之前，使用 Pillow 或 OpenCV 实现这些预处理步骤。

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## 完整可运行脚本

将所有内容组合起来，下面的脚本可以直接复制粘贴到名为 `run_ocr.py` 的文件中并执行。

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

运行脚本会打印原始文本和校正后的文本，确认您已成功**对图像运行 OCR**、**从图像中提取文本**，并通过**OCR 文本校正****提升 OCR 准确率**。

## 结论

现在，您已经了解如何在 Python 中**对图像运行 OCR**，提取原始文本，并应用后处理拼写检查器以获得更清洁的结果。通过遵循**提升 OCR 准确率**的清单，您可以将此工作流应用于收据、发票、身份证或任何扫描文档。

### 接下来做什么？

* 探索用于多语言 OCR 的**特定语言词典**。
* 将管道与数据库或搜索索引（例如 Elasticsearch）集成，使提取的文本可搜索。
* 用神经语言模型（例如基于 GPT 的校正）替换简单的拼写检查器，以获得更高的准确率。

欢迎尝试不同的图像预处理技术、不同的后处理器或替代的 OCR 引擎。核心模式——**对图像运行 OCR → 从图像提取文本 → OCR 文本校正 → 提升 OCR 准确率**——保持不变，为任何文档数字化项目提供坚实的基础。

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [将图像转换为文本：使用 Aspose OCR（Python）提取图像文本](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [提取图像文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}