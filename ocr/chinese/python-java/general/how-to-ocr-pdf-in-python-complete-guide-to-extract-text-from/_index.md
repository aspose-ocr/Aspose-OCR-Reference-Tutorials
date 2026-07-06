---
category: general
date: 2026-06-22
description: 学习如何在 Python 中对 PDF 文件进行 OCR，提取 PDF 文本，并使用基于流的方法将 PDF 转换为文本。处理扫描版 PDF
  的简易步骤。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: zh
og_description: 如何在 Python 中对 PDF 文件进行 OCR？请遵循本指南，从 PDF 中提取文本，将 PDF 转换为文本，并使用流处理扫描的
  PDF。
og_title: 如何在 Python 中对 PDF 进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 如何在 Python 中对 PDF 进行 OCR – 提取 PDF 文本的完整指南
url: /zh/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR PDF – 完整指南：从 PDF 中提取文本

是否曾经想过 **如何 OCR PDF** 文件而不必与笨重的桌面工具苦苦挣扎？你并非唯一。在许多实际项目中——比如发票自动化或数字化档案扫描——你需要一种可靠的方法将扫描的 PDF 转换为可搜索、可编辑的文本。

在本教程中，我们将演示一个简洁的端到端示例，使用轻量级的 Python OCR 引擎 **从 PDF 页面提取文本**。完成后，你将清楚地了解如何 **将 PDF 转换为文本**、如何 **从流加载 PDF**，以及如何高效 **处理扫描的 PDF**。没有魔法，只有可以直接放入项目的普通 Python 代码。

## 你将学到

- 安装并配置能够识别 PDF 输入的 Python OCR 库。  
- 启用 PDF 识别模式并将输出格式设为纯文本。  
- 从文件流加载多页 PDF（经典的 “从流加载 pdf” 模式）。  
- 对所有页面运行 OCR 并获取文本内容。  
- 打印或存储结果以供后续处理。

**先决条件**  
- 在你的机器上已安装 Python 3.8+。  
- 对 pip 和虚拟环境有基本了解。  
- 一个扫描的 PDF 文件（示例中名为 `multipage.pdf`），放置在已知目录中。

如果这些听起来陌生，请不要担心——每一步都用通俗的语言解释，我们会提供所需的完整命令。

---

## 步骤 1：安装 OCR 引擎（how to OCR PDF）

首先——你需要一个能够处理 PDF 输入的 OCR 引擎。本文档中我们使用假想的 `ocr` 包（其 API 与流行的商业 SDK 相似，但相同的模式同样适用于 Tesseract‑OCR、ABBYY 或 Google Vision，只要进行相应封装）。

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **小技巧：** 如果你在 Windows 上遇到权限错误，请改用 `pip install --user ocr`。

包安装完成后，你可以在脚本中导入它并创建引擎实例——这就是 **how to OCR PDF** 的核心。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` 对象保存了我们稍后会调整的所有设置，例如语言、DPI，以及——关键的——PDF 模式。

## 步骤 2：启用 PDF 识别并选择输出（extract text from PDF）

默认情况下，许多 OCR SDK 假设你提供的是图像。为了让引擎将传入的流视为 PDF，我们需要启用 PDF 识别标志并请求纯文本输出。

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

为什么要指定输出格式？因为某些引擎可以返回带有隐藏文本层的 PDF、可搜索的 PDF，或包含边界框的 JSON。对于大多数数据提取流水线来说，**extract text from PDF** 为纯字符串是最简洁的下游格式。

## 步骤 3：从文件流加载 PDF（load PDF from stream）

从流加载 PDF 是一种内存高效的模式——你可以避免一次性将整个文件加载到内存中。这在处理大型多页文档时尤为便利。

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **如果文件位于 S3 或其他云存储桶怎么办？**  
> 只需将 `from_file` 替换为接受字节缓冲区的方法（例如 `ImageStream.from_bytes(s3_object.read())`），其余流水线保持不变。

## 步骤 4：对所有页面运行 OCR（process scanned PDF）

现在开始繁重的工作。引擎会遍历每一页，运行识别引擎，并返回一个页面对象列表——每个对象都提供其文本内容。

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

在幕后，OCR 库会解压每个 PDF 页面，以配置的 DPI 将其光栅化，并将位图送入神经网络模型。结果是？一组准备好提取的 `Page` 对象。

## 步骤 5：获取并显示识别的文本（convert PDF to text）

最后，我们遍历返回的页面并打印识别出的文本。这就是 **convert PDF to text** 真正发生的时刻。

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### 预期输出

如果 `multipage.pdf` 包含三页扫描的页面，你会看到类似如下内容：

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

请注意页面之间的清晰分隔——如果你需要将每页的文本存入数据库或传递给下游的 NLP 模型，这会非常有用。

## 处理常见边缘情况

### 1. 含有图像和文本层的 PDF

有些 PDF 已经包含隐藏的文本层（例如从 Word 导出）。如果你希望 OCR 引擎 **忽略已有文本** 并重新处理图像，请设置：

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. 超出内存限制的大文件

处理 GB 级别的 PDF 时，考虑分块处理：

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. 语言和字体支持

如果你的扫描文档是法语或包含特殊字符，请告知引擎使用哪种语言模型：

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## 完整脚本 – 可直接运行

下面是完整的可运行示例，整合了所有步骤。将其保存为 `ocr_pdf.py` 并执行 `python ocr_pdf.py`。

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**运行脚本** 将把每页的文本打印到控制台，正如 “预期输出” 部分所示。随后你可以将输出重定向到文件：

```bash
python ocr_pdf.py > extracted_text.txt
```

## 结论

我们已经完整演示了在 Python 中 **how to OCR PDF** 文件的全过程。通过配置引擎、通过流加载文档并遍历每个识别的页面，你可以使用仅几行代码 **extract text from PDF**、**convert PDF to text**，以及 **process scanned PDF**。该方法可从小型两页发票扩展到数百页的大型档案。

接下来可以做什么？尝试将提取的字符串输入搜索索引、语言模型摘要器或数据校验流水线。你也可以尝试 JSON 等输出格式，以保留位置信息用于高级文档分析。

如果对处理加密 PDF 或与云存储集成有疑问，请在下方留言——祝编码愉快！ 

![展示 OCR PDF 工作流的示意图 – how to OCR PDF、从流加载 PDF、识别页面并提取文本](ocr-pdf-workflow.png "how to OCR PDF 工作流示意图")


## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 .NET 中使用 Aspose.OCR 进行 OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何使用 Aspose.OCR for .NET 从图像中提取文本](/ocr/english/net/text-recognition/get-recognition-result/)
- [如何使用 Aspose.OCR for .NET 从 ZIP 档案中提取文本](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}