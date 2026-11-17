---
category: general
date: 2026-03-26
description: 如何使用 OCR 提取 PDF 文本。学习将 PDF 加载为图像，识别 PDF 文本，并使用简单的 Python 示例从 PDF 中提取文本。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: zh
og_description: 如何使用 OCR 提取 PDF 文本。本指南向您展示如何将 PDF 加载为图像，识别 PDF 文本并在 Python 中提取 PDF
  文本。
og_title: 如何使用 OCR 提取 PDF 文本 – 完整教程
tags:
- OCR
- Python
- PDF processing
title: 如何使用 OCR 提取 PDF 文本——完整的逐步指南
url: /zh/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR 提取 PDF 文本 – 完整分步指南

是否曾经好奇 **如何提取 PDF** 文件中实际只是扫描图像的内容？你并不孤单——很多开发者在需要可搜索的内容却只有仅图像的 PDF 时都会遇到这个难题。好消息是，只需几行代码和一个可靠的 OCR 库，就能瞬间把这些图片 PDF 转换为纯文本。  

在本教程中，我们将逐步演示 **如何使用 OCR** 将 PDF 加载为图像、识别 PDF 文本，最终 **从 PDF** 文档中 **提取文本**（无论多长）。完成后，你将拥有可运行的脚本、每一步的清晰解释，以及避免常见陷阱的若干技巧。

## 你需要的准备

- Python 3.9 或更高（代码同样适用于 3.10+）  
- `ocr` Python 包（或任何提供 `OcrEngine`、`OcrEngineMode` 和 `Imaging.Image` 的兼容 OCR 库）  
- 一个你想处理的多页 PDF（演示中我们称之为 `multi_page.pdf`）  
- 对虚拟环境的基本了解（可选但推荐）

> **专业提示：** 在 Windows 上建议使用 Anaconda Prompt；在 macOS/Linux 上，直接执行 `python -m venv venv && source venv/bin/activate` 即可。

## 步骤 1：安装 OCR 库

首先，从 PyPI 获取 OCR 包。下面的示例使用一个虚构的 `ocr` 包，其 API 与代码片段中展示的相匹配，但大多数实际库（如 `pytesseract` + `pdf2image`）也遵循相同模式。

```bash
pip install ocr
```

如果你使用的是其他引擎，请将 `ocr` 替换为相应的名称（例如 `pip install pytesseract pdf2image`）。

## 步骤 2：初始化 OCR 引擎

创建引擎实例是 **如何提取 PDF** 文本的基础。可以把引擎想象成解释每页 PDF 像素的“大脑”。

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **为什么重要：** `set_engine_mode` 让你在速度和准确度之间进行权衡。`DEFAULT` 是一个平衡选项；如果需要更高精度，可切换为 `HIGH_ACCURACY`（前提是库支持）。

## 步骤 3：将 PDF 加载为图像对象

OCR 只能处理图像，而不是 PDF 容器，所以我们必须先把 PDF 转换为图像表示。`Imaging.Image.load` 方法会自动处理多页 PDF。

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **边缘情况：** 某些库只接受单页图像。在这种情况下，你需要使用 `pdf2image.convert_from_path` 对每页进行循环。我们的 `load` 调用已经将此抽象为 **load pdf as image** 的一行代码。

## 步骤 4：识别所有页面的文本

现在进入 **recognize PDF text** 的核心。引擎会扫描每一页，返回一个结果对象列表——每页一个。

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

每个 `page_result` 都包含 `get_text()`（纯文本）和 `get_confidence()`（可选的质量指标）等方法。  

> **提示：** 如果只需要第一页，可调用 `recognize(pdf_image[0])` 而不是多页助手。

## 步骤 5：遍历结果并输出提取的文本

最后，我们遍历结果，打印每页的文本。这就完成了 **extract text from PDF** 的工作流。

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### 预期输出

如果 `multi_page.pdf` 包含三页，文字分别为 “Hello”、 “World” 与 “Python”，则会看到：

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

就这样——你的 PDF 现在已经完全可搜索，文本也可以用于后续处理（索引、情感分析，随你所需）。

## 步骤 6：处理常见陷阱

| 问题 | 成因 | 快速解决方案 |
|------|------|--------------|
| **输出为空** | PDF 页面 DPI 较低，字符难以辨认。 | 在 OCR 前放大图像：`pdf_image = pdf_image.resize(300)`（300 DPI 是一个黄金值）。 |
| **出现乱码** | 非拉丁字符需要语言包。 | 加载相应语言模型：`ocr_engine.load_language('spa')` 用于西班牙语，依此类推。 |
| **大文件导致内存爆炸** | 一次性加载所有页面会占用大量 RAM。 | 分块处理页面：`for img in pdf_image.split(batch=10): …`（伪代码）。 |
| **性能慢** | 在巨量文档上使用 `DEFAULT` 模式会比较慢。 | 切换到 `FAST` 模式或使用 `concurrent.futures` 并行 OCR。 |

## 额外：将提取的文本保存到文件

大多数实际流水线都需要持久化文本。下面是一个小工具，将所有内容写入 `output.txt`。

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

现在你可以把 `output.txt` 输入到搜索引擎、数据库或任何 NLP 模型中。

## 综合示例 – 完整脚本

下面是可直接运行的完整程序。复制粘贴，调整文件路径，即可使用。

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

运行它：

```bash
python extract_pdf_ocr.py
```

你应该会在控制台看到每页的内容，并收到文件 `extracted_text.txt` 已创建的确认信息。

## 结论

我们已经完整演示了 **如何提取 PDF** 文本的全过程——从安装库、加载 PDF 为图像、识别多页文本到保存输出。现在你已经掌握了 **如何使用 OCR**、**load PDF as image**、以及 **recognize PDF text** 的可靠方法。  

下一步？尝试将默认引擎模式切换为高精度设置，实验多语言 PDF 的语言包，或将提取的文本导入 Elasticsearch 等全文检索系统。只要掌握了从 PDF 文件提取文本的基础，后续的可能性就无限广阔。

---

![how to extract pdf example](images/ocr_flowchart.png){alt="如何提取 PDF 工作流图"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}