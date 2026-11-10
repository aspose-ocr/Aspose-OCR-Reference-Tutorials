---
category: general
date: 2026-07-05
description: 使用 Python OCR 将 PDF 转换为文本。学习如何从 PDF 中提取文本、执行批量 OCR 处理，以及在几个简单步骤中加载 PDF
  进行 OCR。
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: zh
og_description: 快速将 PDF 转换为文本。本教程展示了如何从 PDF 中提取文本、运行批量 OCR 处理，以及使用 Python 识别扫描的 PDF
  文件。
og_title: 使用 Python OCR 将 PDF 转换为文本 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: 使用Python OCR将PDF转换为文本——完整指南
url: /zh/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 将 PDF 转换为文本 – 完整指南

有没有想过如何 **convert PDF to text** 而不费吹灰之力？也许你手头有一堆扫描的合同、发票或研究论文，需要将它们转换为纯文本以便索引或分析。好消息是，只需几行 Python 代码就能帮你完成繁重的工作。

在本教程中，我们将演示一个实用方案，既能 **convert pdf to text**，又展示如何 **extract text from pdf**、设置 **batch OCR processing**，以及正确 **load pdf for OCR**。完成后，你将拥有一个可直接运行的脚本，一次性 **recognize scanned pdf** 所有页面。

## 你将学到

- 安装并配置 Python OCR 库（本文以通用的 `ocr` 包为例）。  
- 加载多页 PDF 并将其送入 OCR 引擎。  
- 遍历结果并打印或保存提取的文本。  
- 处理常见的边缘情况，如大文件、加密 PDF 和混合语言文档。  

无需繁重的 GUI 工具，无需手动复制——只需纯代码，随时可以嵌入 CI 流水线或桌面工具。

![Convert PDF to Text using Python OCR](https://example.com/images/convert-pdf-to-text.png "Convert PDF to Text using Python OCR")

## 前置条件

在开始之前，请确保你具备以下条件：

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | 现代语法、类型提示以及更佳性能。 |
| `ocr` library (or a wrapper around Tesseract) | 提供示例中使用的 `OcrEngine`、`Language` 和 `Image` 类。 |
| 一个多页扫描 PDF（例如 `contract.pdf`） | 这就是你将 **load pdf for OCR** 的源文件。 |
| 基本的命令行使用经验 | 用于安装包和运行脚本。 |

如果你底层使用 Tesseract，请通过操作系统的包管理器安装（Linux 上 `apt-get install tesseract-ocr`，macOS 上 `brew install tesseract`），随后添加 Python 包装器：

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## 步骤 1：创建 OCR 引擎并设置识别语言

首先，需要创建一个 OCR 引擎实例。将语言设为英文是常见的默认选项，后续也可以切换为其他支持的语言。

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**为什么重要：** 引擎是解释像素数据的大脑。通过显式定义 `engine.language`，可以避免在每页都进行语言检测，从而显著提升 **batch OCR processing** 的速度。

## 步骤 2：加载 PDF 文档以供 OCR

接下来将 PDF 读取到内存中。`ocr.Image.load` 方法接受文件路径并返回引擎可识别的对象。

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**小技巧：** 如果 PDF 设置了密码，大多数库都允许传入 `password` 参数。提前处理可以避免后续出现“无法打开文件”的模糊错误。

## 步骤 3：一次性对所有页面运行 OCR – Recognize Scanned PDF in One Call

逐页运行 OCR 对大文档来说非常慢。`recognize_multi_page` 方法内部实现了 **batch OCR processing**，并在可能的情况下使用多线程。

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**底层原理是什么？** 引擎会将每页流式传递给底层 OCR 引擎（如 Tesseract），收集文本并封装为 `OcrResult`。这种方式降低了 I/O 开销，并为后续 **extract text from pdf** 提供了整洁的接口。

## 步骤 4：遍历结果并输出识别的文本

最后，遍历每个 `OcrResult` 并打印文本。你也可以将每页保存为单独的 `.txt` 文件，或将它们合并为一个文档。

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**为什么使用 enumerate？** `enumerate(..., start=1)` 能给出人类可读的页码，方便后续引用原 PDF 中的特定章节。

### 预期输出

对一个 3 页的合同运行脚本可能得到：

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

如果某页没有可识别的文字，对应的 `result.text` 将是空字符串——这对于快速发现空白页或仅含图片的页非常有用。

## 处理大 PDF 与内存限制

一次性加载 500 页的 PDF 可能会耗尽内存。下面提供两种策略：

1. **分块加载** – 部分库支持一次加载指定页码范围：

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **流式写入磁盘** – 将每页的文本直接写入文件，而不是保存在内存中的列表里。

这两种方法都能让你的 **convert pdf to text** 工作流保持可扩展性。

## 错误处理与边缘情况

- **加密 PDF** – 将密码传给 `Image.load`：

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **混合语言** – 若检测到不同脚本，可在每页切换语言：

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **低分辨率扫描** – 使用 `Pillow` 等库预处理图像，提高对比度后再 OCR。这可以显著提升 **recognize scanned pdf** 步骤的质量。

## 完整脚本：一次性将 PDF 转换为文本

下面是完整、可直接运行的脚本。将其保存为 `pdf_to_text.py`，然后执行 `python pdf_to_text.py`。

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**运行脚本** 后会在 `output` 文件夹中生成 `page_1.txt`、`page_2.txt` 等文件，实质上以结构化方式 **extract text from pdf**。

## 方案测试

1. **基本检查** – 打开生成的 `.txt` 文件，确认前几行与原文档标题一致。  
2. **性能测试** – 使用 `time` 命令对 100 页 PDF 计时。如果耗时过长，考虑启用库的多线程选项（通常是 `engine.set_threads(4)`）。  
3. **质量保证** – 使用 diff 工具将 OCR 输出与手动录入的摘录进行比对。对清晰扫描件目标是达到 >95 % 的字符准确率。

## 后续步骤与相关主题

- **提升准确率**：尝试设置 `engine.dpi = 300` 或在 OCR 前进行图像预处理（去倾斜、去噪）。  
- **可搜索 PDF**：使用 `PyPDF2` 或 `pdfplumber` 等库将提取的文本嵌入原 PDF，使其可搜索。  
- **自然语言处理**：将提取的文本喂给 spaCy 或 NLTK，进行实体抽取、情感分析或关键词标注。  
- **自动化流水线**：结合 `watchdog` 监控文件夹，自动在有新文件时 **convert pdf to text**。

掌握这些模式后，你将能够

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每篇都提供完整可运行的代码示例和逐步解释，帮助你深入掌握更多 API 功能并在项目中探索替代实现方案。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}