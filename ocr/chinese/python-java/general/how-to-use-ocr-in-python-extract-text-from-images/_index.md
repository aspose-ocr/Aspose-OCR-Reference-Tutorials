---
category: general
date: 2026-06-16
description: 如何在 Python 中使用 OCR 从 PNG 等图像文件中提取文本。学习使用 Aspose OCR 将图像逐步转换为文本。
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: zh
og_description: 如何在 Python 中使用 OCR 从图像中提取文本。本指南将带您了解如何使用 Aspose OCR 将 PNG 文件转换为可搜索的文本。
og_title: 如何在 Python 中使用 OCR – 从图像中提取文本
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: 如何在 Python 中使用 OCR – 从图像中提取文本
url: /zh/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 从图像中提取文本

是否曾想过 **如何在 Python 项目中使用 OCR**？你并不孤单。无论是构建收据扫描器、文档归档系统，还是仅仅想把截图转换为可编辑文本，**从图像文件中提取文本**的能力都是改变游戏规则的关键。

在本教程中，我们将完整演示整个过程——从安装 Aspose OCR 库到读取 PNG 文件中的文本——让你只需几行代码即可 **将图像转换为文本**。结束时，你将能够 **从 PNG 中读取文本**，甚至自动处理多语言内容。

> **专业提示：** Aspose OCR 的自动语言检测意味着你无需事先猜测语言——这对跨国应用来说完美。

## 您需要的准备

在开始之前，请确保具备以下条件：

- Python 3.8+（最新稳定版即可）
- 有效的 Aspose OCR 许可证文件（`Aspose.OCR.lic`）。免费试用可用于测试，但正式许可证会移除评估限制。
- 通过 `pip` 安装的 Aspose OCR 包：

```bash
pip install aspose-ocr
```

- 一张需要处理的图像文件——这里我们使用 `sample-multi-lang.png` 作为示例。

准备好这些前置条件可以让流程顺畅，避免后期出现 “module not found” 的意外。

![在 Python 中使用 OCR 的工作流程](https://example.com/ocr-workflow.png "在 Python 中使用 OCR – 步骤说明")

*图片说明：展示如何在 Python 中使用 OCR 从图像中提取文本的示意图。*

## 第一步：应用您的 Aspose OCR 许可证（每个应用只需一次）

任何严肃的 OCR 项目首先要做的就是加载许可证。若未加载，Aspose 会抛出警告并限制可处理的页数。

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **为什么重要：** 提前加载许可证可确保 **ocr image to text python** 引擎以最高速度运行且不出现水印。可以把它看作在开始转换前解锁高级功能。

## 第二步：创建 OCR 引擎并启用自动语言检测

现在我们实例化核心引擎。启用 `language_auto_detect` 在你不确定图像中包含英语、西班牙语、中文或多种语言混合时至关重要。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

如果你**事先知道语言**，可以将 `ocr_engine.language = "English"`（或任意受支持的 ISO 代码）设置，以稍微提升速度。但对于通用的 “从 PNG 读取文本” 实用工具来说，自动检测是最安全的选择。

## 第三步：加载要处理的图像

Aspose OCR 支持多种格式——PNG、JPEG、BMP、TIFF，样样俱全。我们来加载一张包含多语言的 PNG 文件。

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **边缘情况：** 若图像体积很大（超过几 MB），建议先缩小尺寸以提升性能。Aspose 提供 `ocr_image.resize(width, height)` 方法来完成此操作。

## 第四步：执行 OCR 识别

所有准备就绪后，实际的文本提取只需一次方法调用。返回的结果对象同时提供识别出的文本和检测到的语言。

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

在幕后，Aspose 运行复杂的神经网络和模式匹配算法，将每个像素簇转换为字符。繁重的计算全部在本地代码中完成，即使在普通硬件上也能实现 **快速、准确的 OCR**。

## 第五步：显示检测到的语言和识别的文本

最后，打印我们得到的结果。`detected_language` 属性告诉你 Aspose 猜测的语言，`text` 则包含完整的转录内容。

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### 预期输出

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

如果在包含英文和日文的图像上运行脚本，你会看到语言自动切换——这正是我们之前启用的自动检测功能的效果。

## 常见问题处理

### 1. 未找到许可证

如果出现 `License file not found` 错误，请再次确认传递给 `set_license` 的路径是否正确。使用原始字符串（`r"..."`）可以避免 Windows 上的转义字符问题。

### 2. 输出为空

`ocr_result.text` 为空通常意味着图像噪声过大或文字太淡。可以尝试提升图像对比度：

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. 语言检测错误

若自动检测选错语言，你可以强制指定：

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## 扩展示例：批量处理多个 PNG 文件

通常你会想 **将图像转换为文本** 对整个文件夹进行操作，而不是单个文件。下面的循环示例会处理目录中的每个 PNG：

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

此代码片段演示了在批量文档数字化流水线中 **从图像文件中提取文本** 的实用方法。

## 完整可运行脚本

将所有内容整合后，下面是一份可以端到端运行的单文件脚本：

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

将其保存为 `ocr_demo.py`，运行 `python ocr_demo.py`，即可在控制台看到语言和文本的输出。

## 结论

我们从头到尾完整演示了 **如何在 Python 中使用 OCR**，包括 **从图像中提取文本**、**从 PNG 读取文本**，以及使用 Aspose 强大引擎 **将图像转换为文本** 的全过程。通过加载许可证、启用自动语言检测并将图像传入 `OcrEngine`，你可以在几秒钟内获得干净、可搜索的文本。

接下来可以尝试用开源的 Tesseract 替代 Aspose 进行准确性对比，实验 PDF 输入，或将 OCR 步骤集成到 Flask API 中实现即时图像处理。掌握了 **ocr image to text python** 的基础后，想象力就是唯一的限制。

对处理特殊字体、性能调优或许可证有疑问？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程涵盖了与本指南紧密相关的主题，帮助你在已有技术之上进一步提升。每篇资源都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并探索替代实现方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}