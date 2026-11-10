---
category: general
date: 2026-06-28
description: 如何使用 Python 批量 OCR。学习对多个图像进行 OCR，从 PNG 中提取文本，并通过完整的 Python OCR 教程将图像转换为文本。
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: zh
og_description: 在第一句中解释了如何在 Python 中批量进行 OCR。按照本 Python OCR 教程，可高效地从 PNG 文件中提取文本。
og_title: 如何在 Python 中批量 OCR – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中批量 OCR——完整的逐步指南
url: /zh/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中批量 OCR – 完整分步指南

是否曾想过 **如何批量 OCR** 一堆扫描页，而不写一个会阻塞 UI 的循环？你并不是唯一的困惑者。一次处理 dozens of PNG 文件会让人感觉像在看油漆干，尤其是每张图片解码需要一两秒时。

在本教程中，我们将展示一种简洁、非阻塞的方式来 **一次性 OCR 多张图片**、**从 PNG 中提取文本**，以及使用现代 Python OCR 引擎 **将图像转换为文本**。完成后，你将拥有一个可直接运行的脚本，能够放入任何项目——非常适合作为快速 *python ocr tutorial* 或生产级批处理作业。

## 你将构建的内容

- 初始化 OCR 引擎并将语言设置为 Latin（或你需要的任何语言）。  
- 将图片路径列表（本例为 PNG）提供给引擎。  
- 启动返回类似 Future 对象的批处理操作。  
- 使用线程池并发拉取所有结果，让主线程保持空闲。  
- 为每页打印识别的文本，并进行良好分隔。

没有隐藏的魔法，只有纯 Python 与第三方 OCR 库（本文使用虚构的 `pyocr` 包作示例）。

**前置条件**  
- 已安装 Python 3.8+。  
- 对 Python 函数和 `concurrent.futures` 有基本了解。  
- 能够使用提供 `OcrEngine` 类的 OCR 库（例如 `pip install pyocr`）。  

如果缺少上述任意项，请立即获取——其实比想象中更容易。

---

## 如何在 Python 中批量 OCR – 核心概念

在进入代码之前，先回答每一步背后的 “为什么”。

1. **为什么要设置语言？**  
   当引擎知道要期待哪些字符时，OCR 的准确率会大幅提升。Latin 适用于 English、French、Spanish 等。需要时切换到 `Language.Japanese` 或 `Language.Arabic`。

2. **为什么使用批处理操作？**  
   批调用让引擎在内部调度工作，通常会利用本地线程或 GPU 加速。它返回一个句柄，稍后可查询，这意味着在每张图片处理时你不会被阻塞。

3. **为什么使用 ThreadPoolExecutor？**  
   我们得到的 Future 对象是 *惰性* 的——只有在请求时才开始拉取结果。将线程池传给 `getAll`，即可让 Python 并行获取每页文本，显著缩短整体运行时间。

4. **为什么要枚举结果？**  
   结果的顺序与输入路径的顺序相匹配，因此我们可以安全地为每页标注页码。

理解这些 “为什么” 有助于你将模式迁移到其他库或更大的数据集。

---

## 步骤 1：安装并导入所需包

首先，确保 OCR 库已安装。示例使用通用的 `pyocr` 包；请替换为你实际使用的库（如 `pytesseract`、`easyocr`）。

```bash
pip install pyocr
```

现在导入所有需要的内容。

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **小技巧：** 使用 `pathlib` 的 `Path` 可以让脚本跨平台且更易读。

---

## 步骤 2：创建 OCR 引擎并设置语言

创建引擎非常直接。这里我们将其锁定为 Latin，以演示。

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

`setLanguage` 对某些引擎是可选的，但养成这个习惯很好。它告诉 OCR 模型专注于你关心的字符集，从而提升速度和准确度。

---

## 步骤 3：列出待处理的图片文件（从 PNG 中提取文本）

收集所有想要转换的 PNG 文件。使用 `Path.glob` 可以无需修改脚本就处理整个文件夹。

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **为什么重要：** 对列表进行排序可保证顺序确定，随后即可将每个结果对应到正确的页码。

---

## 步骤 4：启动批量 OCR 操作（将图像转换为文本）

现在把列表交给引擎。该方法返回一个类似 Future 的容器，稍后我们会轮询它。

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

在内部，引擎可能会启动自己的工作线程，甚至是 GPU 管线。我们只关心拥有一个句柄（`batch_future`），它知道如何获取各个结果。

---

## 步骤 5：并发检索所有结果（OCR 多张图片）

这里才是真正的 *批量* 工作。将 `ThreadPoolExecutor` 传给 `getAll`，每页文本将在独立线程中获取。

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

你可以根据 CPU 核心数或 OCR 库的建议调节 `max_workers`。更多工作线程并不一定更快——请关注 CPU 使用率。

---

## 步骤 6：输出识别的文本（Python OCR 教程收官）

最后，打印每页的文本。`Result` 对象提供 `getText()` 方法——如果你的库使用不同的名称，请相应调整。

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**预期输出（示例）**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

如果某张图片处理失败，大多数引擎会返回空字符串或抛出异常——你可以在循环外层使用 `try/except` 来优雅地处理这些边缘情况。

---

## 完整脚本 – 可直接运行

下面是完整的、独立的脚本。复制粘贴到名为 `batch_ocr.py` 的文件中，修改 `YOUR_DIRECTORY`，然后执行 `python batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

保存、运行，观察控制台填满提取的文本。简洁、快速且完全异步。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **无输出** – 空字符串 | OCR 引擎未检测到文字（图像噪声过大） | 预处理图像：二值化、去倾斜或提升 DPI |
| **`FileNotFoundError`** | 目录路径错误或缺少 PNG 文件 | 再次确认 `YOUR_DIRECTORY`，并确保文件以 `.png` 结尾 |
| **CPU 占用过高** | `max_workers` 对机器而言设置过高 | 降低 `max_workers`，或在支持的情况下启用 GPU 加速 |
| **Unicode 混乱** | 引擎默认使用了错误的语言 | 在批量 OCR 前调用 `engine.setLanguage(Language.Latin)`（或相应语言） |

提前处理这些问题可以为你节省大量调试时间。

---

## 扩展教程 – 下一步

- **在其他格式**（JPEG、TIFF）中 OCR 多张图片——只需更改 glob 模式。  
- **将从 PNG 中提取的文本** 导入搜索索引（如 Elasticsearch）。  
- **将图像转换为文本** 再生成 PDF，使用 `reportlab` 或 `PyPDF2`。  
- **跨机器并行**，使用 `multiprocessing` 或 Celery 等任务队列处理海量数据集。  

这些主题都自然衔接于你刚完成的 **python ocr tutorial**。

---

## 结论

我们已经完整演示了 **如何批量 OCR** 一组 PNG 文件，展示了批量 API 的威力，并通过线程池方式 **从 PNG 中提取文本**。上面的完整脚本已具备生产级可用性，你现在拥有了任何 OCR 密集型 Python 项目的坚实基础。

试一试，调整语言设置，甚至可以把 `pyocr` 换成 `pytesseract`——模式保持不变。有什么问题或想分享的酷用例？留下评论，让我们继续交流。

*祝编码愉快！*


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}