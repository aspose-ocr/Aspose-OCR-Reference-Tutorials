---
category: general
date: 2026-03-28
description: Python OCR 教程，展示如何使用 Aspose OCR Cloud 在 Python 中提取图像文字。学习如何加载图像进行 OCR，并在几分钟内将图像转换为纯文本。
draft: false
keywords:
- python ocr tutorial
- extract text image python
- ocr image to text
- load image for ocr
- convert image plain text
language: zh
og_description: Python OCR 教程解释如何加载图像进行 OCR 并使用 Aspose OCR Cloud 将图像转换为纯文本。获取完整代码和技巧。
og_title: Python OCR 教程 – 从图像中提取文本
tags:
- OCR
- Python
- Image Processing
title: Python OCR 教程——从图像中提取文本
url: /zh/python/general/python-ocr-tutorial-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教程 – 从图像中提取文本

有没有想过如何把一张凌乱的收据照片转换成干净、可搜索的文本？你并不是唯一有这种想法的人。根据我的经验，最大的障碍并不是 OCR 引擎本身，而是将图像转换为正确的格式并顺利提取纯文本。

本 **python ocr tutorial** 将逐步指导你完成每一步——加载用于 OCR 的图像、运行识别，最后将图像的纯文本转换为可以存储或分析的 Python 字符串。完成后，你就能以 **extract text image python** 的方式提取文本，而且无需任何付费许可证即可开始。

## 你将学到的内容

- 如何安装并导入 Aspose OCR Cloud SDK for Python。  
- 获取用于 **load image for OCR** 的确切代码（PNG、JPEG、TIFF、PDF 等）。  
- 如何调用引擎执行 **ocr image to text** 转换。  
- 处理常见边缘情况的技巧，例如多页 PDF 或低分辨率扫描。  
- 验证输出的方法以及当文本出现乱码时的处理方式。

### 前提条件

- 在机器上已安装 Python 3.8+。  
- 拥有免费 Aspose Cloud 账户（试用版无需许可证即可使用）。  
- 对 pip 和虚拟环境有基本了解——无需高级技巧。

> **专业提示：** 如果你已经在使用 virtualenv，请立即激活它。这可以让依赖保持整洁，避免版本冲突。

![Python OCR 教程截图，显示识别的文本](path/to/ocr_example.png "Python OCR 教程 – 提取的纯文本显示")

## 第一步 – 安装 Aspose OCR Cloud SDK

首先，我们需要与 Aspose OCR 服务通信的库。打开终端并运行：

```bash
pip install asposeocrcloud
```

该单行命令会拉取最新的 SDK（当前版本为 23.12）。该包已包含所有必需内容——无需额外的图像处理库。

## 第二步 – 初始化 OCR 引擎（关键字示例）

SDK 准备好后，我们即可启动 **python ocr tutorial** 引擎。构造函数在试用期间不需要任何许可证密钥，这让过程更简单。

```python
import asposeocrcloud as ocr

# Initialise the OCR engine – no licence needed for trial use
ocr_engine = ocr.OcrEngine()
```

> **为什么重要：** 只初始化一次引擎可以保持后续调用的快速。如果为每张图像都重新创建对象，会浪费网络往返。

## 第三步 – 加载用于 OCR 的图像

这正是 **load image for OCR** 关键字发挥作用的地方。SDK 的 `Image.load` 方法接受文件路径或 URL，并会自动检测格式（PNG、JPEG、TIFF、PDF 等）。我们来加载一个示例收据：

```python
# Step 3: Load the input image (PNG, JPEG, TIFF, PDF …)
input_image = ocr.Image.load(r"YOUR_DIRECTORY/receipt.png")
```

如果处理的是多页 PDF，只需指向该 PDF 文件；SDK 会在内部将每页视为单独的图像。

## 第四步 – 执行 OCR 图像转文本转换

图像已加载到内存后，实际的 OCR 只需一行代码即可完成。`recognize` 方法返回一个 `OcrResult` 对象，其中包含纯文本、置信度分数，甚至在需要时的边界框。

```python
# Step 4: Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)
```

> **边缘情况：** 对于低分辨率图片（低于 300 dpi），可能需要先放大图像。SDK 提供了 `Resize` 辅助工具，但对大多数收据而言默认设置已足够。

## 第五步 – 将图像纯文本转换为可用字符串

拼图的最后一块是从结果对象中提取纯文本。这一步即 **convert image plain text**，将 OCR 数据块转换为可打印、存储或输送到其他系统的内容。

```python
# Step 5: Output the recognised plain text
print("Plain OCR:")
print(ocr_result.text)
```

运行脚本后，你应该会看到类似如下的输出：

```
Plain OCR:
Starbucks Coffee
Date: 2026/03/27
Total: $4.75
Thank you!
```

该输出现在是普通的 Python 字符串，可用于 CSV 导出、数据库插入或自然语言处理。

## 处理常见陷阱

### 1. 空白或噪声图像

如果 `ocr_result.text` 返回为空，请再次检查图像质量。一个快速的解决办法是添加预处理步骤：

```python
# Simple preprocessing – convert to grayscale and increase contrast
processed = input_image.to_grayscale().adjust_contrast(1.2)
ocr_result = ocr_engine.recognize(processed)
```

### 2. 多页 PDF

当你提供 PDF 时，`recognize` 会返回每页的结果。可以这样遍历：

```python
pdf_image = ocr.Image.load("document.pdf")
pages = pdf_image.pages  # collection of page images

for i, page in enumerate(pages, start=1):
    result = ocr_engine.recognize(page)
    print(f"--- Page {i} ---")
    print(result.text)
```

### 3. 语言支持

Aspose OCR 支持超过 60 种语言。要切换语言，请在调用 `recognize` 前设置 `language` 属性：

```python
ocr_engine.language = "fr"  # French
ocr_result = ocr_engine.recognize(input_image)
```

## 完整工作示例

将所有步骤整合在一起，下面是一个完整的、可直接复制粘贴的脚本，涵盖从安装到边缘情况处理的全部内容：

```python
# -*- coding: utf-8 -*-
"""
Python OCR tutorial – complete example using Aspose OCR Cloud.
Demonstrates loading an image, performing OCR, and handling multi‑page PDFs.
"""

import asposeocrcloud as ocr
import os

def ocr_file(filepath: str, language: str = "en"):
    """
    Perform OCR on a given file (image or PDF) and return plain text.
    """
    # Initialise engine (trial licence)
    engine = ocr.OcrEngine()
    engine.language = language

    # Load the file – SDK auto‑detects format
    image = ocr.Image.load(filepath)

    # If it's a PDF, iterate over pages
    if image.is_pdf:
        all_text = []
        for page in image.pages:
            result = engine.recognize(page)
            all_text.append(result.text)
        return "\n".join(all_text)

    # Single‑image case
    result = engine.recognize(image)
    return result.text


if __name__ == "__main__":
    # Example usage – replace with your own path
    sample_path = os.path.join("YOUR_DIRECTORY", "receipt.png")

    if not os.path.exists(sample_path):
        raise FileNotFoundError(f"File not found: {sample_path}")

    extracted = ocr_file(sample_path)
    print("=== Extracted Text ===")
    print(extracted)
```

运行脚本（`python ocr_demo.py`），你将在控制台看到 **ocr image to text** 的输出。

## 回顾 – 我们覆盖的内容

- 已安装 **Aspose OCR Cloud** SDK（`pip install asposeocrcloud`）。  
- **初始化 OCR 引擎**，无需许可证（非常适合试用）。  
- 演示了如何 **load image for OCR**，无论是 PNG、JPEG 还是 PDF。  
- 执行了 **ocr image to text** 转换并 **convert image plain text** 为可用的 Python 字符串。  
- 解决了常见问题，如低分辨率扫描、多页 PDF 和语言选择。

## 后续步骤与相关主题

既然你已经掌握了 **python ocr tutorial**，可以进一步探索：

- **Extract text image python** 用于批量处理大量收据文件夹。  
- 将 OCR 输出与 **pandas** 集成进行数据分析（`df = pd.read_csv(StringIO(extracted))`）。  
- 在网络连接受限时使用 **Tesseract OCR** 作为后备方案。  
- 使用 **spaCy** 添加后处理，以识别日期、金额和商户名称等实体。  

随意尝试：更换不同的图像格式、调整对比度或切换语言。OCR 领域广阔，你刚学到的技能是任何文档自动化项目的坚实基础。

祝编码愉快，愿你的文本始终可读！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}