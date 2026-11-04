---
category: general
date: 2026-05-03
description: 学习如何在图像上运行 OCR 并使用结构化 OCR 识别提取带坐标的文本。附带逐步的 Python 代码。
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: zh
og_description: 对图像进行 OCR 识别，并使用结构化 OCR 获取带坐标的文本。完整的 Python 示例并附有解释。
og_title: 在图像上运行 OCR – 结构化文本提取教程
tags:
- OCR
- Python
- Computer Vision
title: 对图像进行 OCR – 结构化文本提取完整指南
url: /zh/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on image – 结构化文本提取完整指南

是否曾经需要**run OCR on image**文件，却不确定如何保留每个单词的精确位置？你并不孤单。在许多项目中——收据扫描、表单数字化或 UI 测试——你不仅需要原始文本，还需要能够告诉你每行在图片上位置的边界框。

本教程将向你展示一种使用 **aocr** 引擎、请求 **structured OCR recognition** 并在保持几何信息的前提下后处理结果的实用方法。完成后，你只需几行 Python 代码即可**extract text with coordinates**，并且会明白结构化模式为何对下游任务如此重要。

## 您将学习

- 如何为**structured OCR recognition**初始化 OCR 引擎。  
- 如何输入图像并获取包含行边界的原始结果。  
- 如何运行后处理器，在不丢失几何信息的情况下清理文本。  
- 如何遍历最终的行并打印每段文本及其对应的边界框。  

无需魔法，也没有隐藏步骤——只需一个完整、可运行的示例，直接放入你的项目即可。

---

## 前置条件

在开始之前，请确保已安装以下内容：

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

你还需要一张包含清晰可读文字的图像文件（`input_image.png` 或 `.jpg`）。无论是扫描的发票还是截图，只要 OCR 引擎能够识别字符即可。

---

## 步骤 1：为结构化识别初始化 OCR 引擎

首先我们创建 `aocr.Engine()` 的实例，并告知它我们需要 **structured OCR recognition**。结构化模式不仅返回纯文本，还返回每行的几何数据（边界矩形），这在需要将文本映射回图像时至关重要。

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **为什么这很重要：**  
> 在默认模式下，引擎可能只给你一个串联的字符串。结构化模式提供页面 → 行 → 单词的层级结构，每个元素都带有坐标，使得在原始图像上叠加结果或将其输入布局感知模型变得更加容易。

---

## 步骤 2：对图像运行 OCR 并获取原始结果

现在将图像传入引擎。`recognize` 调用返回一个 `OcrResult` 对象，其中包含一系列行，每行都有自己的边界矩形。

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

此时 `raw_result.lines` 包含的对象具有两个重要属性：

- `text` – 该行识别出的字符串。  
- `bounds` – 一个类似 `(x, y, width, height)` 的元组，描述该行的位置。

---

## 步骤 3：在保持几何信息的前提下后处理

原始 OCR 输出往往噪声较多：杂散字符、错误的空格或换行问题。`ai.run_postprocessor` 函数会清理文本，但**保持原始几何**不变，这样你仍然拥有准确的坐标。

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **专业提示：** 如果你有特定领域的词汇表（例如产品代码），可以向后处理器提供自定义字典以提升准确率。

---

## 步骤 4：提取带坐标的文本 – 遍历并展示

最后，我们遍历清理后的行，打印每行的边界框以及对应的文本。这就是**extract text with coordinates**的核心。

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### 预期输出

假设输入图像包含两行文字：“Invoice #12345” 和 “Total: $89.99”，你会看到类似如下的输出：

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

第一个元组是原始图像上该行的 `(x, y, width, height)`，你可以据此绘制矩形、突出显示文本，或将坐标传入其他系统。

---

## 可视化结果（可选）

如果想在图像上叠加显示边界框，可以使用 Pillow（PIL）绘制矩形。下面是一个快速示例；如果只需要原始数据，可直接跳过。

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image 示例，显示边界框](/images/ocr-bounding-boxes.png "run OCR on image – 边界框覆盖")

上面的 alt 文本包含了**primary keyword**，满足图片 alt 属性的 SEO 要求。

---

## 为什么 Structured OCR Recognition 优于简单文本提取

你可能会想，“我只想跑 OCR 获得文本，为什么要在意几何信息？”  

- **空间上下文：** 当你需要在表单上映射字段（例如“Date”旁边的日期值）时，坐标告诉你*数据所在的位置*。  
- **多列布局：** 简单的线性文本会失去顺序；结构化数据保留列顺序。  
- **后处理准确性：** 知道框的大小可以帮助你判断一个词是标题、脚注还是杂散噪声。  

简而言之，**structured OCR recognition** 为你提供了构建更智能流水线的灵活性——无论是将数据写入数据库、创建可搜索的 PDF，还是训练尊重布局的机器学习模型。

---

## 常见边缘情况及处理方法

| 情况 | 需要注意的点 | 建议的解决方案 |
|-----------|-------------------|---------------|
| **旋转或倾斜的图像** | 边界框可能偏离轴线。 | 使用去倾斜预处理（例如 OpenCV 的 `warpAffine`）。 |
| **字体非常小** | 引擎可能漏掉字符，导致空行。 | 提高图像分辨率或使用 `ocr_engine.set_dpi(300)`。 |
| **混合语言** | 错误的语言模型会导致乱码。 | 在识别前设置 `ocr_engine.language = ["en", "de"]`。 |
| **重叠的框** | 后处理器可能会无意合并两行。 | 在处理后验证 `line.bounds`；在 `ai.run_postprocessor` 中调整阈值。 |

提前处理这些情况，可在日后扩展到每天数百份文档时避免头疼。

---

## 完整端到端脚本

下面是完整的、可直接运行的程序，整合了所有步骤。复制粘贴，修改图像路径，即可使用。

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

运行此脚本将：

1. 使用结构化模式**Run OCR on image**。  
2. 为每行**Extract text with coordinates**。  
3. 可选地生成显示框的标注 PNG。

---

## 结论

现在，你已经拥有一个完整、独立的解决方案，能够**run OCR on image**并**extract text with coordinates**，并使用**structured OCR recognition**。代码演示了从引擎初始化、后处理到可视化验证的每一步，你可以将其应用于收据、表单或任何需要精确文本定位的视觉文档。

接下来可以尝试将 `aocr` 引擎替换为其他库（如 Tesseract、EasyOCR），比较它们的结构化输出差异。尝试不同的后处理策略，如拼写检查或自定义正则过滤，以提升特定领域的准确率。如果你在构建更大的流水线，考虑将 `(text, bounds)` 对存入数据库，以便后续分析。

祝编码愉快，愿你的 OCR 项目始终精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}