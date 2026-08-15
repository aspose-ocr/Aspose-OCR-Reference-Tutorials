---
category: general
date: 2026-03-28
description: 快速学习如何使用 Python 对 PDF 进行 OCR。本指南展示了如何从 PDF 中提取文本、识别 PDF 文本，以及使用 Aspose
  OCR 将扫描的 PDF 转换为文本。
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: zh
og_description: 掌握使用 Python 对 PDF 进行 OCR。提取 PDF 文本、识别 PDF 中的文字，并在几分钟内将扫描的 PDF 转换为文本。
og_title: 如何在 Python 中对 PDF 进行 OCR – 完整指南
tags:
- PDF
- OCR
- Python
- Aspose
title: 如何在 Python 中对 PDF 进行 OCR – 步骤指南
url: /zh/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中对 PDF 进行 OCR – 步骤指南

有没有想过 **如何对 PDF 进行 OCR**，当文件只是页面的图片时？你并不是唯一的疑问者。在本教程中，我们将逐步演示如何对 PDF 文件进行 OCR、从 PDF 中提取文本，以及将扫描的 PDF 转换为可搜索的文本——全部使用纯 Python 代码。

我们会覆盖从安装 Aspose OCR 库到提取每页识别文本的全部过程。完成后，你将能够 **使用 Python 对 PDF 进行 OCR**、**从 PDF 中提取文本**，以及 **将扫描的 PDF 转换为文本**，无需在零散的文档中四处寻找。没有冗余，只提供一个可直接复制粘贴的实用示例。

## 你需要准备的东西

在开始之前，请确保你拥有：

* Python 3.8+（最新稳定版最佳）  
* Aspose OCR for Python 的许可证或免费试用密钥——可从 Aspose 官网获取。  
* 一个需要处理的扫描 PDF（我们将其称为 `input.pdf`）。  

如果这些都已经准备好，太好了——我们可以开始了。如果没有，安装该包非常简单，下面会演示如何操作。

## 如何进行 PDF OCR – 环境搭建

首先需要把 Aspose OCR 模块装到本机。该包名为 `aspose-ocr`，可以通过 pip 安装：

```bash
pip install aspose-ocr
```

> **小贴士：** 使用虚拟环境（`python -m venv venv`）可以让依赖保持整洁。

包安装完成后，即可导入并启动 OCR 引擎。这是后续所有 **ocr pdf with python** 工作流的基础。

## 使用 Python 对 PDF 进行 OCR – 导入 Aspose OCR

库已经可用后，我们把它引入脚本。同时将引擎设置为 *direct PDF mode*，这会让 Aspose 直接读取 PDF 字节，而不是先把每页转换为图像。

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

为什么要使用 `PdfMode.DIRECT`？因为它跳过了额外的光栅化步骤，使过程更快，并且保留原始布局——在需要 **recognize text from PDF** 精准识别时尤为方便。

## 从 PDF 中识别文本 – 运行引擎

引擎准备就绪后，指向你的扫描文件。`recognize_from_pdf` 方法会完成所有繁重工作：解析每页、运行 OCR 算法，并返回一个包含 `Page` 对象集合的 `OcrResult` 实例。

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

如果你在想这是否支持加密 PDF——答案是肯定的，只要在调用 `recognize_from_pdf` 前通过 `ocr_engine.password = "secret"` 提供密码即可。这是许多教程忽略的边缘情况，但在实际流水线中非常有用。

## 从 PDF 中提取文本 – 访问页面结果

`ocr_result.pages` 列表为每页保存一个条目。每个 `Page` 对象都有一个 `.text` 属性，存放该扫描页的纯文本表示。下面遍历并打印结果，让你直观看到提取的内容。

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

运行脚本后会得到类似如下的输出：

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

该输出证明你已经成功 **extract text from PDF** 并使用 Aspose OCR **recognize text from PDF**。现在可以把这些字符串写入数据库、搜索索引或任何下游 NLP 流程。

![如何 OCR PDF 示例](placeholder-image.png "如何 OCR PDF 示例")

*图片替代文字:* **如何 OCR PDF 示例** – 展示每页识别文本的控制台输出。

## 将扫描的 PDF 转换为文本 – 保存输出

大多数开发者不只是想在控制台看到文本，他们需要持久化的文件。下面提供一个小工具，将每页文本写入单独的 `.txt` 文件，从而在 `output` 文件夹中实现 **convert scanned PDF to text**。

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

脚本执行完毕后，你会得到一个整洁的目录结构：

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

至此，你已经完整实现 **convert scanned PDF to text**，并可以将这些文件用于搜索、分析，甚至简单的 `grep`。

## 常见问题与边缘情况

**如果我的 PDF 同时包含图片和真实文本怎么办？**  
Aspose OCR 会尝试识别所有内容，但你可以通过对已经包含可选文本的页面禁用 OCR 来加速。设置 `ocr_engine.auto_detect_page_orientation = True`，然后对已知可选文本的页面调用 `ocr_engine.recognize_from_pdf(..., detect_text=False)`。

**我可以控制语言模型吗？**  
当然可以。在调用 `recognize_from_pdf` 前设置 `ocr_engine.language = aocr.Language.English`（或任意受支持语言），这会提升非英文文档的识别准确度。

**如何处理非常大的 PDF（100+ 页）？**  
将其分块处理。`recognize_from_pdf` 方法接受 `page_range` 参数，例如 `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`。循环不同的范围即可降低内存占用。

## 完整工作示例

将所有步骤整合在一起，下面是一段可以保存为 `ocr_pdf.py` 并直接运行的脚本：

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

使用以下命令运行：

```bash
python ocr_pdf.py
```

你应该会在控制台看到每页文本的输出以及保存的 `.txt` 文件位置的确认信息。

## 结论

我们已经介绍了 **如何使用 Python 对 PDF 进行 OCR**，演示了简洁的 **ocr pdf with python** 方法，展示了 **extract text from PDF** 的实现，解释了 **recognize text from PDF** 的工作原理，并提供了一个可直接使用的代码片段，实现 **convert scanned PDF to text**。整个流程已完整封装。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}