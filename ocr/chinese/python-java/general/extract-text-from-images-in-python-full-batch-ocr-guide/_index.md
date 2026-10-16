---
category: general
date: 2026-06-19
description: 使用简单的 OCR 引擎在 Python 中提取图像文本。了解如何将扫描图像转换为文字、从图片中识别文本，并高效列出图像文件。
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: zh
og_description: 使用轻量级 OCR 引擎在 Python 中提取图像文本。本指南展示了如何将扫描图像转换为文本、从图片中识别文字，并在几步内列出 Python
  的图像文件。
og_title: 使用 Python 从图像中提取文本 – 完整批量 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: 使用 Python 从图像中提取文本 – 完整批量 OCR 指南
url: /zh/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（Python） – 完整批量 OCR 指南

是否曾需要 **从图像中提取文本**，却不知从何入手？你并不孤单——开发者经常面临将扫描的 PDF、拍摄的收据或截图转换为可搜索文本的挑战。在本教程中，我们将演示一个完整、可直接运行的示例，展示如何 **将扫描图像转换为文本**、从图片中识别文字，甚至 **以 python 方式列出图像文件**。完成后，你将拥有一个可一次性处理整个文件夹的可复用脚本。

我们会覆盖所有必需内容：所需库、每一步的意义、边缘情况处理以及一些故障排除。无需查阅外部文档；下面的代码是自包含的，解释同时回答 “怎么做” 与 “为什么”。打开你喜欢的 IDE，开始动手吧。

---

## 你将构建的内容

- 初始化 OCR 引擎（本文示例使用 `ocr` 包）。
- 扫描目录并 **以 python 方式列出图像文件**，过滤 PNG、JPG 和 TIFF。
- 对所有找到的图片执行 **批量 OCR** 操作。
- 为每个文件打印提取的文本，并加上清晰的标签。

> **专业提示：** 如果你没有安装 `ocr` 库，可以改用 `pytesseract`，只需做少量修改——核心逻辑保持不变。

---

## 前置条件

- Python 3.8+（脚本使用 f‑strings 和类型提示）。
- 一个提供 `OcrEngine` 且拥有 `recognize_batch` 方法的 OCR 库。本文假设一个虚构的 `ocr` 包，但该模式同样适用于真实库。
- 一个包含待处理图像文件的文件夹（`.png`、`.jpg`、`.tif`）。

---

## 步骤 1 – 安装并导入所需模块

首先，确保 OCR 包已可用。如果使用真实库如 `pytesseract`，相应替换导入语句。

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **为什么重要：** 导入 `os` 可实现跨平台路径处理，而 `typing.List` 有助于 IDE 自动补全并提升代码的可维护性。

---

## 步骤 2 – **从图像中提取文本**：初始化 OCR 引擎

创建引擎是进行任何 OCR 工作的第一步。我们还将语言设置为自动检测，以便引擎能够处理混合语言文档。

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **解释：** 将引擎创建封装在函数中可以保持代码的模块化。如果以后需要调整 DPI 或 OCR 模式，只需修改这一处。

---

## 步骤 3 – **以 Python 方式列出图像文件**：从目录收集文件

现在需要定位所有待处理的图片。下面的列表推导式对应常见的 “list image files python” 用法。

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **边缘情况处理：** 该函数会忽略子文件夹（如需递归可后续添加），并自动过滤隐藏文件，因为它们通常不以受支持的扩展名结尾。

---

## 步骤 4 – **将扫描图像转换为文本**：执行批量 OCR

大多数 OCR 库都提供批量方法，速度远快于逐张处理。下面演示如何调用它。

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **为什么使用批量？** 一次性发送所有图像可减少开销（例如重复加载 OCR 模型），并且通常能获得更好的 CPU/GPU 利用率。

---

## 步骤 5 – **从图片中识别文本**：显示结果

最后，我们遍历文件名与 OCR 结果的配对，为每张图片打印整洁的标题。

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **小技巧：** `strip()` 会去除 OCR 常常附加的前后空白字符。

---

## 完整脚本 – 综合全部代码

下面是完整、可直接运行的程序。将其保存为 `batch_ocr.py`，然后执行 `python batch_ocr.py <your_folder>`。

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### 预期输出

假设文件夹中包含 `invoice1.png` 和 `receipt.jpg`，可能会看到：

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

每个块都有明确标签，便于后续处理（例如保存到数据库）。

---

## 常见问题处理

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **没有出现文本** | OCR 语言未检测到或图像对比度太低。 | 强制指定语言 (`engine.language = ocr.Language.English`) 或对图像进行预处理（提升对比度）。 |
| **大批量时内存错误** | 引擎一次性加载所有图像。 | 将 `image_files` 分块（如 `batch_size = 20`），并多次调用 `recognize_batch`。 |
| **不支持的文件格式** | 添加了 `.gif` 或 `.bmp`。 | 扩展 `supported_exts` 元组，或事先将图像转换为 PNG/JPG。 |
| **Unicode 乱码** | OCR 返回字节而非字符串。 | 确保 OCR 库输出 Unicode（如有必要使用 `result.text.decode('utf-8')`）。 |

---

## 扩展工作流

既然已经能够 **从图像中提取文本**，可以考虑以下后续步骤：

- **导出为 CSV** – 将每个文件名及其提取的文本写入电子表格，便于分析。
- **并行处理** – 使用 `concurrent.futures.ThreadPoolExecutor` 同时处理多个批次。
- **集成云 OCR** – 将本地引擎替换为 Google Vision 或 Azure OCR，以获得更高的复杂布局识别准确率。
- **添加图像预处理** – 使用 Pillow 或 OpenCV 对图像进行去倾斜、去噪或二值化，在 OCR 前提升效果。

所有这些思路都基于我们已经构建的核心函数，无需从头开始。

---

## 结论

我们已经完整演示了如何在 Python 中 **从图像中提取文本**，涵盖了从 **以 python 方式列出图像文件** 到 **从图片中识别文本**，再到 **将扫描图像转换为文本** 的整套批量流程。该脚本故意保持简洁，却足够灵活，可作为更大项目的基础——无论是数字化收据、构建可搜索档案，还是驱动数据抽取管道。

动手试一试，调整预处理步骤，观察 OCR 准确率的提升。如果遇到问题，回顾 “常见问题处理” 表格；大多数问题都能通过微调配置解决。

准备好迎接下一个挑战了吗？尝试使用 `pdf2image` 添加 PDF‑转‑图像步骤，然后将生成的图像直接喂入同一管道。结合 OCR 与 Python 丰富的生态系统，可能性无限。

祝编码愉快，愿你的文本永远清晰可读！


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧之上进一步提升。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索替代实现方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}