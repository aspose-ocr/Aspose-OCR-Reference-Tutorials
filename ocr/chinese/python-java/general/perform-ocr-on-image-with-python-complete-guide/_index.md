---
category: general
date: 2026-07-05
description: 在 Python 中快速进行图像 OCR。学习如何加载用于 OCR 的图像、从扫描表单中提取文本，以及在 Python 中使用 OCR 识别图像。
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: zh
og_description: 在 Python 中对图像进行 OCR。本教程展示了如何加载用于 OCR 的图像、从扫描表单中提取文本，以及在 Python 中使用
  OCR 识别图像。
og_title: 使用 Python 对图像进行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 使用 Python 对图像进行 OCR – 完整指南
url: /zh/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 对图像执行 OCR – 完整指南

是否曾经需要对图像文件进行 **对图像执行 OCR**，但不确定在 Python 中从何入手？你并非唯一。无论是数字化收据、从噪声较大的调查表单中提取数据，还是仅仅将扫描的 PDF 转换为可搜索的文本，从扫描表单中提取文本都是许多开发者每天面临的痛点。

在本教程中，我们将逐步演示 **如何使用 OCR Python** 库，从加载图片到显示过滤后的结果。结束时，你将准确了解如何 **加载用于 OCR 的图像**、配置置信度阈值，并调用实际完成核心工作的 **OCR recognize image Python** 方法。

> **你将获得：** 一个可直接运行的脚本，加载图像、执行 OCR，并打印干净、经过置信度过滤的文本。没有模糊的引用，没有缺失的导入——只有完整的复制粘贴即用的解决方案。

---

## 所需条件

在深入之前，请确保你拥有：

* 已安装 Python 3.9 或更高版本（代码在 3.10+ 也可运行）。  
* 一个符合下文 `ocr` API 的 OCR 包——例如虚构的 `simple-ocr` 库，或任何提供 `OcrEngine`、`Language` 和 `Image` 的包装器。  
* 一张包含你想提取文本的图像文件（`.png`、`.jpg` 等）。  
* 一个可以运行单个 Python 脚本的终端或 IDE。

如果你已经具备上述条件，太好了——让我们开始吧。

---

## 对图像执行 OCR – 设置引擎

首先需要做的是创建一个 OCR 引擎实例。可以把引擎看作操作背后的“大脑”；它知道如何解释像素并将其转换为字符。

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*为什么这很重要：* 没有引擎就没有可处理的内容。`OcrEngine` 对象保存了所有后续会调整的配置，如语言和置信度阈值。

---

## 加载用于 OCR 的图像 – 准备你的扫描表单

现在引擎已经创建，我们需要 **加载用于 OCR 的图像**。库的 `Image.load()` 方法会从磁盘读取文件，并将其转换为引擎能够理解的内部表示。

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **提示：** 如果你处理的是 PDF，请先将每页转换为图像（例如使用 `pdf2image`）。OCR 引擎仅接受光栅图像。

---

## 如何使用 OCR Python – 配置语言和置信度

大多数 OCR 引擎支持多语言，并允许过滤低置信度字符。提前设置这些参数可确保只获得可靠的文本。

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*为什么是 85 %？* 实际上，80‑90 % 左右的阈值可以消除大部分乱码，同时保留有价值的内容。可根据扫描质量自行调整。

---

## 从扫描表单中提取文本 – 识别图像

引擎准备就绪且图像已加载，现在是时候实际 **对图像执行 OCR** 了。`recognize()` 方法返回一个结果对象，其中包含提取的文本，以及可选的边界框数据。

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

如果库支持，`result` 还可能提供 `result.confidences`（每个字符的置信度分数列表）和 `result.words`（结构化的单词对象）。本指南将重点关注纯文本输出。

---

## OCR Recognize Image Python – 显示过滤结果

最后，让我们打印过滤后的文本。低置信度的符号会显示为问号（`?`），因为我们将 `min_confidence` 设置为 85 %。

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### 预期输出

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

请注意，无法辨认的签名被转换为 `?`。这正是置信度过滤器的设计目的——保持输出整洁，以便后续处理。

---

## 常见陷阱与专业提示

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **空白输出** | 图像过暗或分辨率过低。 | 使用 OpenCV 预处理：提高对比度，调整大小至 ≥300 dpi。 |
| **乱码字符** | 选择了错误的语言。 | 将 `engine.language` 设置为匹配文档的语言（例如 `ocr.Language.FRENCH`）。 |
| **`?` 符号过多** | 置信度阈值设置过高。 | 将 `engine.min_confidence` 降低至 70‑80 %，以适应噪声较大的扫描。 |
| **Unicode 错误** | 输出包含非 ASCII 字符，但控制台编码不正确。 | 运行 `python -X utf8` 或设置 `PYTHONIOENCODING=utf-8`。 |

**专业提示：** 如果需要提取表格，可在过滤原始文本后再次使用支持布局感知的 OCR 引擎（如 Tesseract 的 `--psm 6`）进行二次处理。

---

## 完整脚本 – 可直接运行

下面是完整的、独立的脚本，包含了所有讨论的步骤。将其保存为 `perform_ocr.py`，修改图像路径后运行 `python perform_ocr.py`。

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

运行它，你将在控制台看到过滤后的文本——正是 **extract text from scanned form** 步骤所承诺的结果。

---

## 接下来做什么？

既然你已经了解如何 **对图像执行 OCR** 和 **从扫描表单中提取文本**，可以进一步探索：

* **批量处理** – 遍历图像目录，生成结果 CSV。  
* **后处理** – 使用正则表达式或 spaCy 提取日期、金额或 ID 等字段。  
* **集成** – 将 OCR 输出写入数据库、Google Sheets 或 REST API。  

所有这些思路本质上都使用了我们覆盖的核心函数：加载图像、配置引擎，以及调用 **OCR recognize image Python** 方法。

## 结论

我们已经完整演示了一个可用于生产环境的 **对图像执行 OCR** 示例。从 **加载用于 OCR 的图像**、配置语言、设置置信度阈值，到最终 **从扫描表单中提取文本**，每一步都配有清晰的代码和说明。现在，你拥有了坚实的基础，能够应对更复杂的场景——无论是批量任务、多语言支持，还是表格提取。

运行脚本，调整阈值，便能在几分钟内让文档可搜索。有什么问题或遇到顽固的表单？在下方留言，我们一起排查。祝编码愉快！

![对图像执行 OCR 示例](example.png "对图像执行 OCR")

## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 AspOCR：针对 .NET 的图像 OCR 预处理过滤器](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [使用 Aspose.OCR 通过语言选择提取图像文本（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}