---
category: general
date: 2026-03-26
description: 学习如何在 Python 中执行 OCR，并使用简单的 OcrEngine 轻松从图像中提取文本、读取扫描件中的文字或从发票中提取文本。
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: zh
og_description: 如何在 Python 中执行 OCR？本指南向您展示如何在几分钟内从图像中提取文本、读取扫描件中的文本以及从发票中提取文本。
og_title: 如何在 Python 中执行 OCR – 快速提取文本
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中进行 OCR – 快速提取文本
url: /zh/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中执行 OCR – 快速提取文本

是否曾好奇 **如何执行 OCR** 来处理扫描收据或模糊的 PDF？你并不孤单。在许多项目中，**从图像中提取文本** 的需求往往会提前出现，而传统的 “手动输入所有内容” 方法根本无法扩展。  

在本教程中，你将看到一个完整、可直接运行的示例，展示 **如何使用 OCR** 从扫描件读取文本、从发票中提取数据，甚至自动进行倾斜校正——只需几行 Python 代码。

## 你将学到

我们将逐步讲解你需要掌握的全部内容：

* 精确的依赖项和导入语句。
* 如何创建并配置 `OcrEngine` 实例。
* 使用同一引擎实现 **从图像中提取文本**、**从扫描件读取文本** 和 **从发票中提取文本** 的方法。
* 常见陷阱（语言错误、文件缺失、大图像）以及规避技巧。
* 预期输出，帮助你验证 OCR 是否成功。

无需外部文档链接——所有内容自成一体，你可以直接复制粘贴代码并立刻看到结果。

## 前置条件

在开始之前，请确保你具备以下条件：

* 已安装 Python 3.8+（`ocr` 包兼容任何近期版本）。
* 已获取 `ocr` 库（`pip install ocr‑engine` – 如有不同请替换为实际包名）。
* 准备好要处理的图像文件——演示中我们使用位于 `YOUR_DIRECTORY` 文件夹下的 `invoice.png`。

就这些。如果你已经满足上述条件，即可开始。

## 第 1 步：安装并导入 OCR 模块

首先，需要获取 OCR 库。如果尚未安装，请在终端运行以下命令：

```bash
pip install ocr-engine
```

随后在脚本中导入该模块。

```python
# Step 1: Import the OCR module
import ocr
```

> **专业提示：** 保持虚拟环境整洁；这能避免在后续添加其他图像处理库时出现版本冲突。

## 第 2 步：创建并配置 OCR 引擎

创建引擎只需调用构造函数，但真正的威力在于正确配置。我们将语言设为 English，并开启自动倾斜校正，这在处理未完全对齐的扫描发票时尤为关键。

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

为何要启用 `auto_skew`？许多扫描仪会产生略有倾斜的图像。如果不进行校正，引擎可能会漏掉字符，使本来清晰的发票变成乱码。

## 第 3 步：对目标图像执行 OCR

现在将图像文件传入引擎。`recognize_image` 方法返回一个对象，包含原始文本以及置信度分数（若库提供的话）。

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

如果你处理的是 **从扫描件读取文本** 的场景，只需将路径替换为已转换为 PNG 或 JPEG 的扫描 PDF。该调用同样适用于底层库支持的任何图像格式。

## 第 4 步：检查并使用提取的文本

先打印原始 OCR 输出。在真实的发票处理流水线中，你可能会进一步解析该字符串，提取明细、总计和日期，但此处只需快速浏览即可确认 OCR 是否成功。

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**预期输出（为简洁起见已截断）：**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

如果输出出现乱码，请再次确认图像清晰且 `engine.language` 与文档语言匹配。

## 第 5 步：处理常见边缘情况

### 大图像

处理 5000 × 5000 像素的扫描会消耗大量内存。一个简便的缓解办法是先将图像下采样后再送入引擎：

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### 多语言

如果需要 **从图像中提取文本** 的图像同时包含英文和西班牙文，可设置语言列表：

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

引擎会尝试识别两套字符集。

### 错误处理

切勿假设文件一定存在。将调用包装在 try‑except 块中，以提供友好的错误提示：

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## 可视化参考

下图展示了演示中使用的示例发票截图。请注意轻微的倾斜——这正是 `auto_skew` 所修正的。

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* 展示自动倾斜校正的发票图像。

## 完整、可运行的示例

将所有内容整合在一起，下面是一段可以直接在命令行运行的脚本。它涵盖了安装、配置、错误处理以及一个简单的后处理步骤——将提取的文本写入名为 `output.txt` 的文件。

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

运行 `python full_ocr_demo.py` 将在控制台打印提取的文本，并保存到 `output.txt`。随后，你可以使用正则表达式、CSV 写入器或任何其他逻辑，实现 **从发票中提取文本** 的自动化。

## 结论

现在，你已经掌握了在 Python 中 **如何执行 OCR** 的完整端到端方案。通过创建 `OcrEngine`、配置语言与倾斜校正，并处理几个实用的边缘情况，你可以可靠地 **从图像中提取文本**、**从扫描件读取文本**，以及 **从发票中提取文本**，无需在零散的文档中四处寻找答案。

接下来可以尝试将一批文件放入循环中处理，实验不同语言，或将输出接入 PDF 生成库，创建可搜索的 PDF。可能性无限，而你刚看到的代码正是坚实的起跳板。

对特定文件格式有疑问或需要微调置信度阈值？在下方留言——乐意帮助你进一步调优 OCR 流程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}