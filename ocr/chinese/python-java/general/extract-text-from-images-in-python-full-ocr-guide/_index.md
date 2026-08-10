---
category: general
date: 2026-06-19
description: 使用 Python OCR 从图像中提取文本。在简明教程中学习自动语言检测、并行处理和批量识别。
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: zh
og_description: 使用 Python OCR 从图像中提取文本。本指南在一个教程中展示自动语言检测、并行处理和批量识别。
og_title: 在 Python 中从图像提取文本 – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 使用Python从图像中提取文本 – 完整OCR指南
url: /zh/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 完整 OCR 指南

是否曾想过 **从图像中提取文本** 而不必手动输入每个单词？你并不孤单。无论是数字化旧收据、构建可搜索的文档档案，还是仅仅玩转酷炫的 AI 技巧，从图片中提取文字都是当今任何 Python 开发者的必备技能。

在本教程中，我们将演示一个完整、可直接运行的示例，使用流行的 OCR 引擎 **从图像中提取文本**。我们会涵盖自动语言检测、并行处理加速以及批量图像识别，让你在几秒钟内处理数十个文件。听起来正是你需要的？让我们开始吧。

## 你将学到

- 如何使用 `ocr.OcrEngine` 实例化 OCR 引擎。  
- 启用 **自动语言检测**，让引擎自行选择合适的语言。  
- 使用自定义线程池配置 **并行处理 OCR**。  
- 对文件列表执行 **批量图像识别**。  
- 为每张图像打印识别出的文本，便于保存或建立索引。

无需外部文档——所有内容都在这里，代码开箱即用，只需安装 `ocr` 包（通过 `pip install ocr`）。

## 前置条件

在开始之前，请确保你已具备：

1. 已安装 Python 3.8 或更高版本。  
2. 已安装 `ocr` 包（`pip install ocr`）。  
3. 一个存放 PNG（或 JPG）图像的文件夹。  
4. 对 Python 函数和循环有基本了解。

就是这么简单——没有繁重的依赖，没有 GPU 魔法，纯粹的 Python。

![从图像中提取文本示例](https://example.com/ocr-demo.png "显示从图像中提取文本输出的截图")

*Alt text: 从图像中提取文本演示截图*

## 第一步 – 设置 OCR 引擎（关键字示例）

首先，创建一个 OCR 引擎实例。把 `ocr.OcrEngine()` 当作背后的“大脑”；它知道如何读取字符、行和段落。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

为什么需要显式创建引擎？因为 **ocr.OcrEngine 的使用** 让你能够细粒度地控制语言设置、线程等。相较于一行代码的快捷方式，这是最灵活的 **从图像中提取文本** 方式。

## 第二步 – 让引擎自动检测语言

大多数 OCR 库都要求你手动指定语言。这对单语言项目还算可以，但对混合语言的批处理来说非常繁琐。幸运的是，`ocr` 包支持 **自动语言检测**。

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

将 `engine.language` 设置为 `ocr.Language.Auto`，引擎会嗅探每张图像并挑选合适的语言模型。当你处理国际化文档时，这一行代码可以为你省去数小时的手动配置。

## 第三步 – 使用并行处理加速 OCR

如果你的机器有四核或以上的 CPU，何不充分利用它们？引擎可以启动线程池，让多张图像同时被处理。这正是 **并行处理 OCR** 发光发热的地方。

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

根据你的机器自行调整数字 `4`。线程数越多 → 批处理越快，但请记住每个线程都会占用内存，找到适合你环境的平衡点。

## 第四步 – 收集待处理的图像

现在我们需要一个文件路径列表。你可以手动构建、从 CSV 读取，或使用 `glob`。为保持清晰，这里直接硬编码一个短列表：

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

将 `YOUR_DIRECTORY` 替换为你系统中的实际路径。如果文件数量很多，使用 `glob.glob("*.png")` 可以轻松完成收集。

## 第五步 – 运行批量图像识别

下面是教程的核心：一次调用即可处理 `files` 中的所有图像，并返回结果对象列表。这就是让大规模 OCR 成为可能的 **批量图像识别** 功能。

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

在内部，引擎会把每个文件分配到之前配置的四个工作线程，同时为每张图片自动检测语言。该方法返回的列表中，每个元素都包含识别出的文本及其元数据。

## 第六步 – 打印（或存储）提取的文本

最后，我们遍历结果并打印文本。在真实项目中，你可能会把它写入数据库或 CSV 文件，但这里直接打印更便于演示。

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**预期输出**（为简洁起见已截断）：

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

每个块显示文件名后跟 OCR 生成的字符串。如果图像包含多种语言，你会看到相应的字符出现，这得益于前面的 **自动语言检测** 步骤。

## 专业技巧与常见陷阱

- **图像质量至关重要**——模糊或低对比度的图片会产生垃圾输出。必要时可使用 OpenCV（`cv2.threshold`、`cv2.resize`）进行预处理。  
- **线程数 vs. I/O**——如果图像存放在慢速网络磁盘上，增加线程数可能帮助不大。使用 `top` 或任务管理器监控 CPU 使用率。  
- **Unicode 处理**——`result.text` 为 Unicode 字符串。写入文件时请使用 `encoding="utf‑8"`，避免 `UnicodeEncodeError`。  
- **内存占用**——大批量 PDF 可能消耗大量 RAM。若出现 `MemoryError`，请降低线程池大小或分批处理图像。

## 完整可运行脚本

以下是完整的、可直接复制粘贴的脚本，囊括了我们讨论的所有步骤。将其保存为 `batch_ocr.py` 并运行 `python batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

运行方式如下：

```bash
python batch_ocr.py ./my_images 4
```

你将看到每张图像对应的整齐文本块，证明你可以 **大规模从图像中提取文本**。

## 接下来可以做什么？

掌握了使用 Python **从图像中提取文本** 的基础后，建议进一步探索：

- **后处理**：使用正则或自然语言库清理 OCR 输出。  
- **PDF 转换**：将提取的字符串喂入 PDF 生成器，制作可搜索的 PDF。  
- **云 OCR 服务**：将本地 `ocr` 结果与 Google Vision、Azure OCR 等云服务对比，提升边缘案例的准确率。  
- **GUI 前端**：构建一个小型 Flask 或 FastAPI 应用，让用户上传图像并即时看到提取的文本。

这些主题都基于你刚刚搭建的 **Python OCR 库** 基础，并且同样受益于我们在本教程中使用的 **并行处理 OCR** 技巧。

---

*祝编码愉快！如果遇到任何问题，欢迎在下方留言——我随时乐于帮助解决 OCR 的各种怪癖。*


## 接下来该学什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}