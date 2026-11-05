---
category: general
date: 2026-07-05
description: 使用 Python OCR 从图像中提取表格。学习如何提取表格、将图像转换为 TSV，并掌握 OCR 表格图像的 Python 技巧。
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: zh
og_description: 使用 Python OCR 从图像中提取表格。本指南展示如何提取表格、将图像转换为 TSV，以及使用 OCR 表格图像 Python
  工具。
og_title: 从图像提取表格 – 在 Python 中将图像转换为 TSV
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: 从图像中提取表格 – 使用Python将图像转换为TSV
url: /zh/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取表格 – 将图像转换为 TSV（Python）

有没有想过如何在不抓狂的情况下从图像中提取表格？在本教程中，我们将演示 **如何提取表格** 数据，使用 `aocr` 库，然后将这些数据转换为整洁的 TSV 文件。没有魔法，只需几行 Python 代码和一点 AI 驱动的后处理。

如果你曾经尝试从扫描的发票或截图中复制粘贴表格，却得到一团乱麻，你会明白掌握基于 OCR 的方法有多么重要。完成后，你将能够将任何表格图像喂给 Python，得到干净的制表符分隔值，直接用于电子表格或数据库。

---

## 你需要准备的内容

在开始之前，请确保你的机器上具备以下条件：

| 要求 | 为什么重要 |
|------|------------|
| Python 3.9+ | `aocr` 包面向现代 Python 运行时。 |
| `aocr` 库（`pip install aocr`） | 提供我们将使用的 OCR 引擎和 AI 后处理器。 |
| 包含表格的图像文件（PNG、JPG 等） | 我们要提取的源数据。 |
| 可选：虚拟环境 | 将依赖隔离——强烈推荐。 |

准备好这些可以避免在教程进行到一半时被中断。

---

## 安装依赖

首先，安装 OCR 工具。打开终端并运行：

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **小技巧：** 如果遇到权限错误，在 `pip install` 命令后添加 `--user`，或使用 `pipx` 进行全局安装。

---

## 步骤 1 – 初始化 OCR 引擎

引擎是整个过程的核心。可以把它想象成“脑子”，负责查看每个像素并决定字符归属。

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

为什么要实例化一个引擎而不是直接调用单个函数？引擎对象让我们以后可以附加自定义后处理器，从而对输出进行细粒度控制——在需要 **ocr table image python** 高精度时尤为关键。

---

## 步骤 2 – 附加 AI 后处理器

`aocr` 自带轻量级 AI 后处理器，能够在保留单元格边界的同时清理原始 OCR 结果。无需额外参数，代码保持简洁。

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

如果跳过此步骤，你仍会得到原始文本，但表格结构会很嘈杂——就像每个单元格都是谜团的电子表格。后处理器负责将文本对齐到原始网格。

---

## 步骤 3 – 加载表格图像

你可以从任意路径加载图像，这里为了说明使用占位目录。将 `"YOUR_DIRECTORY/invoice_table.png"` 替换为实际文件路径。

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **注意：** `aocr.Image` 会自动检测图像格式并标准化颜色通道，除非图像严重退化，否则无需预处理文件。

---

## 步骤 4 – 执行结构化 OCR

现在引擎会扫描图像并返回原始表格对象。该对象包含行、列以及每个单元格的原始文本。

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

为什么使用 `recognize_structured` 而不是通用的 `recognize`？结构化版本会尝试推断行/列边界，生成类似矩阵的结果，后续转换为 TSV 时会更容易处理。

---

## 步骤 5 – 使用 AI 后处理器清理数据

运行后处理器会细化原始输出：去除杂散字符、合并被拆分的片段，并确保每个单元格的文本正确对齐。

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

如果检查 `processed_table.table`，你会看到一个行列表，每行都是 `Cell` 对象的列表。每个 `Cell` 都有 `.text` 属性，保存了清理后的字符串。

---

## 步骤 6 – 导出表格为 TSV

最后一步是将处理后的数据写入制表符分隔值（TSV）文件——这正是你在 **convert image to TSV** 时需要的格式，适用于 Excel 或 Google Sheets。

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

运行脚本会将每行打印到控制台（如果你喜欢），并生成一个干净的 TSV 文件，任何电子表格程序都能打开。

### 快速验证

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

你应该会看到整齐对齐的列，例如：

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

如果输出看起来乱七八糟，请检查图像质量（清晰度、对比度），并考虑微调 OCR 引擎的设置——`engine.set_config(...)` 允许你调整语言模型和置信度阈值。

---

## 处理常见边缘情况

| 情况 | 建议解决方案 |
|------|--------------|
| **图像倾斜** | 在将图像传给 `aocr` 前使用 `Pillow` 的 `Image.rotate` 进行预旋转。 |
| **对比度低** | 使用直方图均衡化（`cv2.equalizeHist`）提升可读性。 |
| **单元格合并** | 在 TSV 中根据已知分隔符拆分单元格，或使用 `merge_cells=False` 标志（如果可用）。 |
| **多页 PDF** | 先将每页转换为图像（`pdf2image`），再在循环中运行流水线。 |

这些技巧可以让你的 **ocr table image python** 工作流在各种源材料下保持稳健。

---

## 完整脚本 – 一站式解决方案

下面是完整的、可直接运行的脚本，包含本文讨论的所有步骤。将其保存为 `extract_table.py` 并执行 `python extract_table.py`。

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在本教程的技术基础上进一步深入。每个资源都包含完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 从图像中提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR for .NET 从图像中提取表格](/ocr/english/net/text-recognition/recognize-table/)
- [通过在 OCR 中准备矩形来提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}