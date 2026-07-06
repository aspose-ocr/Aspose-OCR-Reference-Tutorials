---
category: general
date: 2026-01-12
description: Python OCR 教程，展示如何从图像中提取表格文本。学习使用 Aspose OCR 从图像读取表格并提取选定的文本。
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: zh
og_description: Python OCR 教程，教您如何从图像中提取表格文本、读取图像中的表格以及使用 Aspose OCR 提取选定的文本。
og_title: Python OCR 教程：从图像中提取表格文本
tags:
- OCR
- Python
- AsposeOCR
title: Python OCR 教程：从图像中提取表格文本
url: /zh/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教程：从图像中提取表格文本

是否曾经需要一个实际上演示如何从扫描表单中提取表格的 **python ocr tutorial**？你并不是唯一的需求者。大多数教程只停留在通用文本提取上，让你猜测如何隔离出你关心的整齐数据网格。  

在本指南中，我们将演示一个真实场景：从图像中读取表格，仅提取所需的选定文本，最后打印结果。过程中我们还会提供关于 **how to extract table** 数据可靠提取的技巧，这样你就不必每次都重新发明轮子。

## 你将学到

- 如何为 Python 设置 Aspose OCR。
- 如何定义包含表格的矩形区域。
- **extract table text** 和 **read table from image** 的具体步骤。
- 处理多语言或不规则表格布局的技巧。
- 一个完整、可直接运行的脚本，今天即可加入你的项目。

**先决条件**  
- Python 3.8 或更高版本。  
- 对 OCR 概念有基本了解（无需深入专业知识）。  
- 包含清晰表格的 PNG 或 JPEG 图像（我们称之为 `form_with_table.png`）。  

如果你已经准备好，让我们开始吧——不废话，只提供可操作的代码。

![python ocr 教程 表格区域 示例](table_region_example.png){alt="python ocr 教程 示例显示表格区域"}

## 步骤 1：安装并导入 Aspose OCR

首先，你需要 Aspose OCR 库。该包已发布在 PyPI 上，只需一条 `pip` 命令即可完成安装。

```bash
pip install aspose-ocr
```

现在导入模块以及你需要的任何辅助工具。

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*小技巧：* 将依赖项保存在 `requirements.txt` 文件中。这样可以轻松复现环境。

## 步骤 2：初始化 OCR 引擎（Python OCR 教程核心）

创建引擎是任何 **python ocr tutorial** 的核心。在这里我们还将默认语言设置为英文——以后可以随意更换。

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

为什么设置语言？当引擎知道预期字符时，OCR 准确率会显著提升。如果你处理的是多语言表单，可以设置语言列表或在每个区域单独覆盖（见后文）。

## 步骤 3：加载图像

Aspose OCR 支持大多数常见图像格式。只需指向文件路径，即可获得可供处理的 `Image` 对象。

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*边缘情况：* 大于 5 MB 的大型图像可能会减慢处理速度。如果性能成为问题，请考虑在 OCR 前先调整大小或压缩图像。

## 步骤 4：定义表格区域（从图像读取表格）

现在进入有趣的部分：告诉引擎表格所在的 *位置*。你需要提供一个带有 `Rectangle`（x, y, width, height）的 `OcrRegion`。坐标基于像素，可能需要稍作实验。

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

为什么使用区域？通过将 OCR 限制在表格区域，我们可以更快 **extract selected text**，并避免来自周围标签或图形的噪声。由于引擎可以专注于统一的布局，这也提升了准确性。

## 步骤 5：在定义的区域上运行 OCR

设置好区域后，我们调用 `process_region`。该方法返回一个 `OcrResult` 对象，包含原始文本、置信度分数，甚至在需要时的边界框。

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

如果需要提取多个表格，只需使用不同的矩形重复步骤 4‑5 即可。

## 步骤 6：输出提取的表格文本

最后，打印或保存表格的文本表示。Aspose OCR 返回的纯文本带有换行符，通常与行对应，**使后处理变得简单**。

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**预期输出**（示例）：

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

现在你可以将此字符串输入到 `csv` 解析器、pandas DataFrame 或任何下游 **analytics** 流程中。

## 完整工作示例

将所有步骤整合在一起，这里是可以立即运行的完整脚本。将 `YOUR_DIRECTORY/form_with_table.png` 替换为实际的 **路径** 到你的图像。

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

使用 `python extract_table.py` 运行脚本。如果一切顺利，你将在控制台看到表格打印输出。

## 常见问题与边缘情况处理

**如果表格不是完全矩形怎么办？**  
可以将表格拆分为多个重叠区域，或使用覆盖整个区域的更大矩形，然后对文本进行后处理（例如，按换行符拆分）。

**我能只提取特定列吗？**  
获取完整表格文本后，使用 Python 的 `csv` 或 `pandas` 切取所需列。OCR 步骤本身返回矩形内的全部内容。

**如何处理非英文表格？**  
将 `ocr_engine.language`（或 `region.language`）设置为相应的枚举，例如 `ocr.Language.FRENCH`，或使用 `ocr.Language.ENGLISH | ocr.Language.SPANISH` 组合多种语言。

**有没有办法获取每个单元格的边界框？**  
Aspose OCR 可以返回 `region_result.words`，其中每个单词都包含边界框。你需要将这些框映射回网格——这对高级布局分析很有用。

## 提高准确性的技巧

- **清理图像**：在送入 OCR 前进行二值化或提升对比度。可使用 Pillow 等库。
- **避免压缩伪影**：尽可能将扫描保存为 PNG。
- **注意 DPI**：300 dpi 是最佳值；更低的 DPI 可能导致字符缺失。
- **测试不同的矩形尺寸**：稍大一些的矩形常能捕获属于表格的零散字符。

## 下一步

现在你已经掌握了使用 Aspose OCR **how to extract table** 数据的技巧，可以进一步探索：

- 使用 Python 的 `csv` 模块将提取的文本转换为 CSV 文件。
- 将数据导入 **pandas** DataFrame 进行分析。
- 使用 OCR 读取手写表单（需要不同的引擎或额外训练）。
- 使用简单的 `for` 循环实现对数十个扫描表单的批量处理自动化。

这些扩展都基于本 **python ocr tutorial** 中的核心概念，因此你已具备良好的扩展基础。

---

*祝编码愉快！如果遇到任何问题，请在下方留言——我很乐意帮助你微调提取过程。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}