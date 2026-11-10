---
category: general
date: 2026-09-19
description: Python OCR 教程展示如何使用 Aspose OCR 将 PNG 转换为文本。学习 Python OCR 文本提取，并从扫描图像中提取文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: zh
lastmod: 2026-09-19
og_description: Python OCR 教程将指导您使用 Aspose OCR 将 PNG 转换为文本。掌握 OCR 文本提取 Python，并从扫描图像中提取文本。
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Python OCR 教程 – 使用 Aspose 将 PNG 转换为文本
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: Python OCR 教程：使用 Aspose 将 PNG 转换为文本
url: /zh/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教程：使用 Aspose 将 PNG 转换为文本

如果您需要一个 **python OCR 教程**，将 PNG 图像转换为可编辑文本，本指南提供了完整、可直接运行的解决方案。您将看到如何安装 Aspose OCR 库、加载图像、运行识别引擎并打印结果——全部只需几个简洁的步骤。

扫描文档并提取文本往往会让人感到繁琐，尤其是在处理图像格式和语言设置时。本教程通过展示确切的调用方法及其意义，消除猜测，让您专注于将 OCR 集成到自己的应用中。

您还将学习如何 **convert PNG to text**、处理常见的陷阱，并将代码适配到 JPEG 或 TIFF 等其他图像类型。完成后，您即可自信地从任何扫描图像中提取文本。

## Prerequisites

在开始之前，请确保您具备以下条件：

* 已安装 Python 3.8 或更高版本。
* 有可用的网络连接以下载 Aspose OCR 包。
* 拥有一张包含可读文本的 PNG 图像（或任何受支持的格式）。

您 **不** 需要单独的 OCR 引擎或外部二进制文件——Aspose OCR 已将所需全部内容打包。

## Step 1: Install the Aspose OCR package

第一步是将库添加到您的环境中。Aspose 提供了一个纯 Python 包，可通过 pip 安装。

```bash
pip install aspose-ocr
```

> **Pro tip:** 使用虚拟环境（`python -m venv venv`）可以将依赖与其他项目隔离。

安装该包后，`aspose.ocr` 模块即可使用，其中包含本教程中贯穿始终的 `OcrEngine` 类。

## Step 2: Import the OCR engine class

现在库已经就绪，导入驱动识别过程的类。

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` 封装了加载图像、配置语言和提取文本的全部逻辑。将其放在脚本顶部符合标准 Python 习惯，也能保持代码整洁。

## Step 3: Create an instance of the OCR engine

创建实例会得到一个带有默认设置的全新引擎。随后您可以自定义语言或图像预处理等属性。

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

新的 `engine` 对象代表一次 OCR 会话。对多个图像复用同一实例可以提升性能，因为内部资源会被缓存。

## Step 4: Load the image you want to process

指定要转换的 PNG 文件路径。`load_image` 方法接受 Aspose OCR 支持的任何格式，您同样可以传入 JPEG、BMP 或 TIFF 文件。

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

如果文件未找到，`load_image` 会抛出 `FileNotFoundError`。在生产代码中建议使用 try/except 包裹，以提供友好的错误提示。

## Step 5: Perform OCR to extract text from the image

调用 `recognize` 会运行识别流水线并返回提取的字符串。该方法会自动处理版面分析、字符分割以及语言检测（默认英语）。

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

您可以在调用 `recognize` 之前更改语言：

```python
engine.language = "fr"   # for French text
```

当需要对多语言文档进行 **OCR text extraction python** 时，这种灵活性非常有用。

## Step 6: Output the recognized text

最后，打印或保存结果。快速检查时，`print` 会在控制台显示原始字符串。

```python
# Step 6: Output the recognized text
print(text)
```

### Expected output

如果 `sample.png` 包含句子 “Hello, world!”，控制台将显示：

```
Hello, world!
```

输出可能会包含换行或额外空白，这取决于原始版面。您可以使用 `str.strip()` 或正则表达式对字符串进行后处理以清理。

## Handling common edge cases

### 1. Non‑PNG formats

虽然本教程聚焦于 **convert PNG to text**，但您可能会收到 JPEG 或 TIFF 文件。代码保持不变，只需在 `load_image` 中更改文件扩展名即可。

```python
engine.load_image("scanned_page.tiff")
```

### 2. Low‑resolution images

当分辨率低于 150 dpi 时，OCR 准确率会下降。如果遇到效果不佳，可先使用 Pillow 对图像进行放大：

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extracting text from a scanned image with multiple languages

设置以逗号分隔的语言代码列表：

```python
engine.language = "en,es,de"
```

Aspose OCR 将尝试识别所有列出语言的字符。

### 4. Large documents

一次处理大量页面可能会耗尽内存。建议逐页处理：

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Full, runnable script

将所有步骤组合在一起，即得到一个可直接复制、粘贴并执行的完整程序。

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

运行脚本：

```bash
python python_ocr_tutorial.py
```

您应该会在控制台看到提取的文本。

## Conclusion

本 **python OCR 教程** 演示了如何使用 Aspose OCR **convert PNG to text**，涵盖了安装、图像加载、识别以及输出处理。您现在拥有可靠的 **OCR text extraction python** 模式，并且可以将代码适配为 **extract text image python**，从任何扫描文档中提取文本。

接下来，您可以考虑：

* 将脚本集成到 Web 服务（例如 Flask），提供 OCR API。
* 将提取的文本存入数据库，以实现可搜索的档案。
* 尝试不同的语言设置，处理多语言扫描件。

祝编码愉快，尽情将图像转换为可搜索、可编辑的文本吧！

## What Should You Learn Next?

以下教程涵盖与本指南紧密相关的主题，帮助您在项目中进一步使用 API 功能并探索替代实现方式，每个资源均提供完整可运行的代码示例和逐步解释。

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Extract Table Text from Images](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}