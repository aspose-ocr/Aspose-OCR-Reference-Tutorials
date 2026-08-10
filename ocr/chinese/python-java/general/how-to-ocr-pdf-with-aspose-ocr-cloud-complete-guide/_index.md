---
category: general
date: 2026-06-06
description: 如何使用 Aspose OCR Cloud 对 PDF 进行 OCR。学习从 PDF 中提取文本、将 PDF 页面转换为 PNG，并在 Python
  中保存 PDF 页面图像。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: zh
og_description: 如何使用 Aspose OCR Cloud 对 PDF 进行 OCR。本指南展示了如何提取纯文本 PDF、将 PDF 页面转换为 PNG，以及保存
  PDF 页面图像。
og_title: 如何使用 Aspose OCR Cloud 对 PDF 进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: 如何使用 Aspose OCR Cloud 对 PDF 进行 OCR – 完整指南
url: /zh/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR Cloud 对 PDF 进行 OCR – 完整指南

是否曾经想过 **如何对 PDF 进行 OCR** 而不必使用笨重的桌面工具？你并不孤单——许多开发者在需要快速、可编程地从扫描文档中提取文本时都会遇到这个难题。好消息是？使用 Aspose OCR Cloud，你可以 **从 PDF 中提取文本**、将每页转换为 PNG，甚至 **保存 PDF 页面图像** 以供后续使用，全部通过一个简洁的 Python 脚本完成。

在本教程中，我们将逐步讲解你需要了解的所有内容：从安装 SDK、授权引擎、识别多页 PDF，到提取纯文本、将页面转换为 PNG，以及将这些图像持久化到磁盘。完成后，你将拥有一个可复用的代码片段，能够在任何需要 **如何对 PDF 进行 OCR** 功能的项目中直接使用。

## 你需要准备的环境

- **Python 3.8+**（代码在 3.10 及更高版本同样适用）  
- Aspose OCR Cloud 账户——你将获得一个免费试用的许可证文件 (`Aspose.OCR.lic`)  
- `asposeocrcloud` 包（`pip install asposeocrcloud`）  
- 一份需要处理的扫描版多页 PDF  

就这些。无需额外的二进制文件、无需本地依赖，纯 Python 即可。

## 如何对 PDF 进行 OCR – 设置与授权

在调用任何 OCR 方法之前，你必须告诉 SDK 你的身份。Aspose 使用一个轻量级的许可证文件，你只需将其放在脚本可访问的位置。

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*小技巧*：如果跳过授权步骤，SDK 仍然可以工作，但会在输出图像中嵌入一个小水印。生产环境下并不理想。

## 步骤 2：安装 Aspose OCR Cloud Python SDK

打开终端并运行：

```bash
pip install asposeocrcloud
```

该包会自动拉取所有必需的依赖（requests、pillow 等），你无需额外寻找任何东西。

## 步骤 3：创建 OCR 引擎并选择语言

引擎是整个操作的核心。你可以指定 Aspose 支持的任意语言；英文在大多数情况下都能工作。

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

为什么要设置语言？因为 OCR 引擎会使用特定语言的词典来提升识别准确率。如果你要处理法语 PDF，只需将 `ENGLISH` 换成 `FRENCH` 即可。

## 步骤 4：指向你的多页 PDF

为引擎提供待处理文件的完整路径。相对路径同样可以，只要它们相对于脚本的工作目录能够解析即可。

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

确保文件可读；否则会抛出 `FileNotFoundError`。

## 步骤 5：运行 OCR – 你将得到一个结果列表

调用 `recognize_pdf` 会返回一个列表，列表中的每个元素对应源 PDF 的一页。

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

每个 `OcrResult` 包含两个实用属性：

* `text` – 页面对应的纯文本表示（非常适合 **提取 PDF 纯文本**）  
* `image` – 渲染后页面的 Pillow `Image` 对象（完美用于 **将 PDF 页面转换为 PNG**）

## 步骤 6：从 PDF 中提取文本并将页面转换为 PNG

现在我们遍历结果，打印提取的文本，并保存每页的 PNG 版本。

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### 预期的控制台输出

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

你还会在 `YOUR_DIRECTORY` 中看到 `page_1.png`、`page_2.png` … 等文件。这些就是可以进一步用于下游图像处理流水线的栅格化页面图像。

## 步骤 7：保存 PDF 页面图像（可选后处理）

如果你只需要图像而不需要文本，可以省略 `print(res.text)` 那一行。相反，如果你想把文本存入单独的 `.txt` 文件，只需添加一小段写入代码：

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

这段小小的补充演示了在 **保存 PDF 页面图像** 的同时，也能轻松持久化提取的内容。

## 完整可运行示例

将所有内容整合在一起，下面是可以直接复制到 `ocr_pdf.py` 的完整脚本：

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

使用以下命令运行：

```bash
python ocr_pdf.py
```

你应该会在控制台看到每页文本的输出，同时生成一系列 PNG 文件。

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步深入。每篇资源都提供了完整的可运行代码示例以及逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}