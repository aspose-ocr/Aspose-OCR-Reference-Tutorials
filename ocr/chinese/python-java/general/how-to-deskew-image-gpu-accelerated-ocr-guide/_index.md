---
category: general
date: 2026-01-02
description: 学习如何校正图像倾斜并提升图像对比度，以快速获取纯文本。包括逐步的 Python 代码和提取文本的技巧。
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: zh
og_description: 如何校正图像倾斜并提升对比度以获取纯文本。完整的 Python 示例，包括表格提取和 GPU 加速。
og_title: 如何去除图像倾斜 – 完整的 GPU OCR 教程
tags:
- OCR
- Python
- Image Processing
title: 如何对图像进行去倾斜 – GPU 加速的 OCR 指南
url: /zh/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正图像倾斜 – GPU 加速 OCR 指南

有没有想过在收据倾斜时**如何校正图像倾斜**？你并不孤单；倾斜的照片会把本来清晰的收据变成一团乱麻。好消息是，只需几行 Python 代码，你就可以自动校正倾斜、提升对比度，并提取干净的纯文本——无需手动使用 Photoshop。

在本教程中，我们将演示一个完整且可运行的示例，既展示**如何校正图像倾斜**，又展示**如何提升对比度**、**如何获取纯文本**，甚至**如何从 OCR 引擎检测到的表格中提取文本**。完成后，你将拥有一个可直接放入任何项目的独立脚本。

## 你需要的环境

- 已安装 Python 3.9+（代码使用类型提示，建议使用较新的解释器）
- 提供 `OcrEngine`、`EngineMode`、`ImageProcessingOptions` 和 `OcrResult` 的 `ocr` 库（通过 `pip install ocr‑sdk` 安装——请替换为你实际使用的包名）
- 如需加速，可使用带兼容驱动的 GPU（可选但推荐）
- 一张略有旋转或对比度低的图像文件，例如 `receipt_skewed.jpg`

> **专业提示：** 如果没有 GPU，只需将 `EngineMode.GPU` 改为 `EngineMode.CPU`，脚本仍可运行——只是稍慢一些。

## 步骤实现

下面我们将解决方案拆分为若干逻辑块。每个块都有描述性的 **H2**，其中包含主要关键词 *how to deskew image* 或次要关键词。代码完整、带注释，随时可运行。

### 使用 GPU 加速 OCR 校正图像倾斜

我们首先让 OCR 引擎在 GPU 上运行并启用自动校正倾斜功能。自动校正会分析图像几何并将其旋转回正。

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **为什么重要：** GPU 加速可以将处理时间从秒级缩短到毫秒级，这在每分钟处理数十张收据时至关重要。

### 提升图像对比度以获得更好识别

低对比度的收据对任何 OCR 系统都是噩梦。提升对比度可以为引擎提供更清晰的边缘。

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **如何提升对比度：** `set_contrast_boost` 方法接受百分比；30 % 是对大多数扫描收据安全的默认值。如果图像非常暗，可提升至 50 % 或自行实验。

### 从处理后的图像获取纯文本

现在图像已校正且亮度提升，我们将其送入引擎并请求获取纯文本结果。

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**预期输出**（为简洁起见已截断）：

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **如何获取纯文本：** `get_text()` 方法会去除所有布局信息，返回干净的字符串，你可以将其存入数据库、发送到 API，或用于后续分析。

### 如何从检测到的表格中提取文本

收据通常包含表格数据（商品、数量、价格）。OCR SDK 能检测表格，并允许你遍历行和单元格。

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**示例表格输出**：

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **为什么要提取表格：** 结构化数据可以轻松计算总额、生成报告或导入会计软件。

### 完整可运行脚本

将所有内容整合后，以下是可以复制粘贴到 `deskew_and_ocr.py` 的脚本：

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

使用以下方式运行：

```bash
python deskew_and_ocr.py
```

你应该会在控制台看到已清理的文本以及任何检测到的表格。

## 常见边缘情况及处理方法

| 情况 | 处理方法 |
|-----------|------------|
| **图像颠倒** | 如果 SDK 提供 `set_rotation_correction(True)`，可同时调用以提升 `set_auto_deskew(True)` 的置信度。 |
| **对比度提升导致图像过亮** | 降低传递给 `set_contrast_boost` 的百分比（例如 15 %）。 |
| **GPU 不可用** | 将 `EngineMode.GPU` 切换为 `EngineMode.CPU`；其余流程保持不变。 |
| **表格未被检测** | 尝试更高分辨率的扫描，或如果库提供 `set_table_detection(True)`，则启用它。 |

## 下一步：从纯文本到结构化数据

现在你已经了解**如何校正图像倾斜**、**如何提升对比度**以及**如何获取纯文本**，你可能想要：

- 使用正则表达式解析纯文本，提取键值对（例如 `total`、`date`）。
- 将结果存入 SQLite 或 PostgreSQL 数据库，以便后续报告。
- 将脚本接入无服务器函数（AWS Lambda、Azure Functions），实现上传自动处理。

所有这些扩展都基于我们在此介绍的相同基础。

## 结论

我们已经演示了如何使用 GPU 加速的 OCR 引擎**校正图像倾斜**，展示了**提升对比度**以获得更清晰的识别，明确说明了**如何获取纯文本**，甚至涵盖了**如何从表格中提取文本**。完整的可运行脚本将所有内容整合在一起，你可以将其放入任何 Python 项目，立即从倾斜、低对比度的照片中提取干净的数据。

使用你自己的几张收据试一试，调整对比度水平，让 OCR 完成繁重的工作。如果遇到问题，回顾上面的边缘情况表——大多数问题只需微调即可解决。

祝编码愉快，愿你的图像永远保持正直且明亮！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}