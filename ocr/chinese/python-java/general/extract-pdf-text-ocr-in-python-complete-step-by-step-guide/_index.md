---
category: general
date: 2026-06-25
description: 使用 Python 提取 PDF 文本 OCR。学习如何通过清晰的 Python OCR 示例将 PDF 转换为文本，并快速获得可靠的结果。
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: zh
og_description: 使用 Python 提取 PDF 文本 OCR。本指南展示了一个 Python OCR 示例，可将 PDF 转换为文本，轻松处理多页文档。
og_title: 使用 Python 提取 PDF 文本 OCR – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: 在Python中进行PDF文本OCR提取——完整的逐步指南
url: /zh/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中提取 PDF 文本 OCR – 完整分步指南

是否曾经需要 **提取 PDF 文本 OCR**，却不确定哪个库能够轻松处理多页 PDF？你并不孤单。在许多实际项目中——比如法律合同、扫描的发票或归档报告——从 PDF 中获取干净、可搜索的文本是一项必备技能。

在本教程中，我们将通过一个 **python ocr 示例**，使用 Aspose.OCR **将 PDF 转换为文本**。完成后，你将拥有一个可直接运行的脚本，能够提取每一页的文本、显示预览，并将整个文档保存为单个 `.txt` 文件。没有冗余，只提供可直接投入代码库的实用方案。

## 你将学到的内容

- 如何安装并导入 Aspose OCR 模块（Python 版）。  
- 如何创建 OCR 引擎实例并对多页 PDF 执行 **提取 PDF 文本 OCR**。  
- 如何遍历每页的结果、显示预览以及将完整输出写入磁盘。  
- 处理常见问题的技巧，如空白页或 Unicode 字符。

> **先决条件：** 已安装 Python 3.8+，熟悉 pip 基本用法，并准备好要处理的 PDF 文件。无需事先的 OCR 经验。

---

![提取 PDF 文本 OCR 工作流图](extract-pdf-text-ocr.png "提取 PDF 文本 OCR 过程示意图")

*Alt text: 展示在 Python 中提取 PDF 文本 OCR 工作流的示意图。*

## 第 1 步：安装 Aspose OCR for Python

在编写任何代码之前，需要先获取 Aspose.OCR 包。它通过 PyPI 分发，只需一条 pip 命令即可完成。

```bash
pip install aspose-ocr
```

> **专业提示：** 如果你在虚拟环境中工作（强烈推荐），请先激活它，以保持依赖的隔离。

## 第 2 步：导入模块并创建 OCR 引擎

库已经就绪后，导入它并实例化一个 `OcrEngine`。可以把引擎看作是负责所有繁重任务的大脑——识别字符、处理页面布局并返回干净的 Unicode 字符串。

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **为什么重要：** 只实例化一次引擎并在所有页面间复用，远比为每页创建新引擎更高效，同时还能确保文档整体使用一致的设置。

## 第 3 步：识别 PDF 的所有页面（多页 OCR）

Aspose.OCR 的 `recognize_multi_page` 方法接受文件路径并返回 `OcrResult` 对象列表——每页一个。这正是我们 **将 PDF 转换为文本** 操作的核心。

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **边缘情况：** 若 PDF 受密码保护，需要在调用 `recognize_multi_page` 前通过 `engine.set_password("your_password")` 提供密码。

## 第 4 步：遍历结果并显示预览

快速预览可以帮助你确认 OCR 已经成功捕获文本。我们将打印每页的前 200 个字符，当然你可以根据需要调整切片长度。

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**示例输出**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

上面仅展示了片段，完整文本位于 `page_result.text` 中。

## 第 5 步：将所有页面合并为单个文本文件（可选）

大多数后续工作流——搜索索引、数据分析或简单归档——更倾向于使用单个 `.txt` 文件。我们将把各页内容拼接后写入磁盘。

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **原理说明：** 使用 UTF‑8 编码可防止丢失诸如重音字母或法律文档中常见的特殊符号等字符。

## 第 6 步：处理常见问题

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| 输出中出现空白页 | `page_result.text` 为空 | 确认源 PDF 实际包含扫描图像；某些 PDF 已经是文本形式，需要使用 PDF 文本提取库（如 pdfminer）而非 OCR。 |
| 字符乱码 | 出现奇怪的符号而非字母 | 确保 OCR 引擎的语言设置正确：`engine.language = ocr.Language.English`（或其他语言）。 |
| 大型 PDF 处理时间过长 | 脚本在某页卡住 | 启用多线程：`engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`。 |
| 大文件导致内存错误 | 抛出 `MemoryError` | 将 PDF 分块处理（例如每次 50 页），或提升 Python 的内存限制。 |

## 完整脚本 – 可直接运行

将所有步骤整合后，下面是完整的、可自行复制粘贴到 `extract_pdf_text_ocr.py` 文件中的脚本。

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

在终端运行它：

```bash
python extract_pdf_text_ocr.py
```

你应该会在控制台看到每页的预览输出，随后出现完整文本已保存的确认信息。

## 小结与后续

我们已经演示了如何使用简洁的 **python ocr 示例**，通过 **提取 PDF 文本 OCR** 高效地 **将 PDF 转换为文本**。核心步骤——安装、导入、创建引擎、调用 `recognize_multi_page`、预览以及保存——覆盖了扫描 PDF 最常见的工作流。

**接下来可以做什么？**  

- **微调准确率**：使用 `engine.recognize_multi_page(..., RecognizeOptions(...))` 调整 DPI 或加载语言包。  
- **后处理**：去除多余空白、进行拼写检查，或将文本输送至自然语言处理管道。  
- **批量处理**：遍历文件夹中的多个 PDF，构建可搜索的文档库。  

如果遇到问题，请先确认 PDF 确实包含光栅图像（OCR 只能处理图像，而非嵌入的文本）。对于已经是文本的 PDF，建议使用 `pdfminer.six` 或 `PyMuPDF` 等库。

---

**祝编码愉快！** 如果本指南帮助你 **提取 PDF 文本 OCR**，欢迎在评论中分享你的成果，或在 Aspose OCR 的 GitHub 页面提交功能请求。持续实验，你很快就能拥有一个强大的管道，将任何扫描的 PDF 转换为可搜索、可编辑的文本。

## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [使用 Aspose OCR 提取图像文本 – 分步指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [提取文本图像 – Aspose.OCR for Java OCR 基础](/ocr/english/java/ocr-basics/)
- [使用 Aspose.OCR 进行语言选择的图像文本 OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}