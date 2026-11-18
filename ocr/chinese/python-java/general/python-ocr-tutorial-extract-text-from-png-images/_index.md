---
category: general
date: 2026-06-25
description: Python OCR 教程，展示如何提取 PNG 文件中的文本、读取文本图像，并使用简单、免授权的引擎识别图像文字。
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: zh
og_description: Python OCR 教程教你如何加载图像进行 OCR，提取文本 PNG 文件，并仅用几行代码识别图像文本。
og_title: Python OCR 教程 – 从 PNG 提取文本
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: Python OCR 教程：从 PNG 图像中提取文本
url: /zh/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教程 – 从 PNG 图像中提取文本

有没有想过 **python ocr tutorial** 如何把收据的截图转换为可编辑文本？你并不孤单。在许多实际项目中，我们需要快速 *read text image* 文件，而自己动手比每次从 GUI 复制粘贴更有效。

在本指南中，我们将通过一个动手示例，**extract text PNG** 文件，展示如何 *load image for OCR*，并最终打印 *recognize image text* 的结果——全部使用免费、仅供评估的 OCR 引擎。无需许可证密钥，无需繁重依赖——只需普通的 Python 和几个小型包。

## 你将学到的内容

- 如何安装并导入轻量级 OCR 库。
- **load image for OCR** 的完整步骤以及常见坑点的处理。
- 读取不同质量的 *read text image* 文件的方法。
- 提高 **extract text png** 文件准确性的技巧。
- 如何显示识别出的字符串并可选地写入磁盘。

完成本教程后，你将拥有一个可复用的脚本，能够在任何需要 **recognize image text** 的项目中即插即用。没有魔法，只有清晰的代码和解释。

### 前置条件

- Python 3.8 或更高（库兼容 3.7+，但推荐 3.8+）。
- 基本了解 pip 和虚拟环境。
- 一个名为 `sample.png` 的图像文件（或任意想要测试的 PNG），放在可引用的文件夹中。

如果上述任意一点不熟悉，请暂停一分钟进行设置——相信我，回报是值得的。

---

## Python OCR 教程 – 设置引擎

首先：我们需要一个 OCR 引擎对象。我们使用的库是对本地 OCR 引擎的轻量包装，开箱即用用于评估。它不需要许可证密钥，使得 *python ocr tutorial* 非常适合快速原型。

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**为什么重要：** 创建引擎可以将 OCR 运行时与其余代码隔离，允许你在多张图像之间复用，而无需每次重新初始化沉重资源。

---

## Load Image for OCR – 读取 PNG 文件

引擎已经创建完毕，接下来要 *load image for OCR*。库的 `Image.load` 方法接受路径并自动解码 PNG、JPEG、BMP 等几种格式。

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **专业提示：** 如果你的 PNG 包含 alpha 通道，库会自动丢弃它。不过，为了在 *read text image* 任务中获得最佳效果，建议将图像保持为灰度——这可以降低噪声并加快识别速度。

---

## Recognize Image Text – 运行 OCR 引擎

图像对象准备好后，终于可以 **recognize image text** 了。这是 *python ocr tutorial* 的核心，只需一行代码。

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**内部发生了什么？** 引擎会先执行一系列预处理过滤（去倾斜、二值化），然后将位图送入经过数百万字符训练的神经网络。这就是即使在低分辨率 PNG 上也能得到惊人准确输出的原因。

---

## 显示并保存提取的文本

得到结果固然好，但你可能想查看或存储它。`result` 对象提供了 `text` 属性，包含纯字符串输出。

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**预期输出**（假设 `sample.png` 包含 “Hello, OCR!”）：

```
Eval-mode result: Hello, OCR!
```

如果得到的是乱码而非可读字符，请参考下一节的常见修复方法。

---

## 处理提取 Text PNG 时的常见问题

即使是最好的 OCR 引擎也会在某些图像上卡壳。下面列出典型障碍及其解决方案。

### 1. 低对比度或深色背景

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. 文字倾斜

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. 非英文字符

如果你的 PNG 包含带重音的字母或非拉丁脚本，请使用相应语言包初始化引擎：

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. 超大图像

处理 4000×3000 的 PNG 可能会很慢。可以在保持可读性的前提下降低分辨率：

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

这些调整是 *python ocr tutorial* 在非理想情况下仍能可靠运行的关键。

---

## 完整脚本 – 单文件解决方案

下面是完整的、可直接运行的脚本，已整合所有步骤及可选改进。复制粘贴到 `ocr_extract.py`，然后执行 `python ocr_extract.py`。

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**运行方式：**  
```bash
python ocr_extract.py ./sample.png
```

你应该会看到识别出的字符串被打印，并在图像旁生成 `sample_extracted.txt` 文件。

---

## 可视化概览

![Python OCR 教程 – 加载图像进行 OCR 并从 PNG 中提取文本](/images/python-ocr-flow.png)

*Alt text:* *Python OCR 教程图示，展示从 load image for OCR 到 extract text PNG 的流程。*

该图示说明了 **load image for OCR** → **recognize image text** → **extract text PNG** 的线性过程，并标出可插入预处理步骤的位置。

---

## 结论

我们刚刚完成了一个 **python ocr tutorial**，演示了如何 *load image for OCR*、*recognize image text*，以及仅用几行 Python 命令 **extract text png** 文件。该脚本功能完整，能够处理常见边缘情况，并可扩展用于批处理或多语言支持。

准备好迎接下一个挑战了吗？尝试将 PDF 转为图像后喂入引擎，实验不同语言包，或将 OCR 步骤集成到 Flask API 中，让你的 Web 应用能够实时读取上传的截图。*read text image* 自动化的可能性几乎是无限的。

有问题或遇到难以破解的图像？在下方留言，我们一起排查。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每个资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索项目中的替代实现方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}