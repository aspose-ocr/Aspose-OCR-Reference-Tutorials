---
category: general
date: 2026-06-06
description: 如何使用 Python 对 PDF 进行 OCR，提取 PDF 文本，转换扫描版 PDF 文本，并在几行代码内更改 OCR 语言。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: zh
og_description: 如何使用 Python 对 PDF 进行 OCR：一本实用指南，教你如何从 PDF 中提取文本、转换扫描 PDF 文本，并轻松更改
  OCR 语言。
og_title: 如何在 Python 中对 PDF 进行 OCR – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: 如何在 Python 中对 PDF 进行 OCR – 完整分步指南
url: /zh/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中进行 PDF OCR – 完整分步指南

有没有想过在不支付昂贵 SaaS 工具费用的情况下 **如何对 PDF 进行 OCR**？你并不是唯一有此需求的人。无论是数字化旧书、从发票中提取数据，还是仅仅需要从扫描报告中获取可搜索的文本，掌握 Python 中的 PDF OCR 都可以为你节省数小时的手动复制工作。

在本教程中，我们将演示一个简洁、可运行的示例，**从 PDF 中提取文本**，展示如何 **将扫描的 PDF 文本** 转换为可编辑的字符串，并演示如果文档不是英文时如何 **更改 OCR 语言**。完成后，你将拥有一个可在任何项目中直接使用的代码片段。

## 前置条件与设置

在开始之前，请确保你已经具备：

- 已安装 Python 3.8+（代码在 3.9、3.10 以及更高版本均可运行）
- 提供 `OcrEngine` 类的 `ocr` 包（可通过 `pip install ocr-lib` 安装——请替换为你实际使用的包名）
- 一个待处理的 PDF 文件；演示中我们使用放在 `YOUR_DIRECTORY` 文件夹下的 `high_res_book.pdf`

如果你使用虚拟环境（强烈推荐），请先激活它：

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **专业提示：** 将 PDF 文件统一放在专用的 `data/` 目录下，可避免后期路径相关的麻烦。

## 步骤 1：创建 OCR 引擎实例（How to OCR PDF – 初始化）

当你想要 **对 PDF 执行 OCR** 时，首先需要实例化引擎。可以把引擎想象成大脑，它会读取每一页、解释字形，并返回纯文本。

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

为什么这很重要：没有引擎，你将没有语言设置、渲染选项或 PDF 处理的上下文。`OcrEngine` 对象保存了所有默认值，并允许你随后进行微调。

## 步骤 2：设置识别语言（Change OCR Language）

大多数 OCR 库默认使用英语，但如果你的文档是法语、德语甚至日语怎么办？只需调用 `set_recognition_language` 即可更改语言。这满足 **change OCR language** 的需求，并提升识别准确度。

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **为何可能需要这样做：** 多语言档案常包含混合语言的页面。即时切换语言可防止字符如 “ß” 或 “ñ” 被误识别。

## 步骤 3：配置 PDF 渲染选项（Convert Scanned PDF Text Effectively）

处理扫描版 PDF 时，分辨率和颜色模式会显著影响 OCR 质量。以 300 DPI 的灰度模式渲染是大多数文档的最佳平衡——既能捕捉细节，又能保持内存占用在合理范围。

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

链式调用看起来很炫，但其实只是返回同一个选项对象的流式 API。如果需要彩色（例如彩色图表），将 `"grayscale"` 替换为 `"color"` 即可。

## 步骤 4：识别 PDF 并获取首页文本（Extract Text from PDF）

现在进入 **如何对 PDF 进行 OCR** 的核心：将文件路径交给引擎并提取识别后的文本。该方法返回一个页面结果列表，每个结果都包含 `text` 属性。

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

如果需要整本文档，可遍历 `results`：

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### 如果 PDF 被加密怎么办？

有些 PDF 受密码保护。这种情况下可以将密码传递给 `recognize_pdf`：

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

引擎会在执行 OCR 前即时解密——无需额外步骤。

## 步骤 5：后处理提取的文本（Fine‑Tuning Extract Text from PDF）

原始 OCR 输出常包含换行、额外空格或偶尔的误识别字符。快速的清理例程可以让提取的字符串准备好用于后续处理（搜索索引、数据库存储等）。

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

现在你可以安全地 **从 PDF 中提取文本**，并将其输入任意 NLP 流程、搜索引擎或简单的 `open(...).write()` 操作。

## 额外内容：批量处理多个 PDF（Scaling Perform OCR on PDF）

如果文件夹中充满了扫描版 PDF，只需将逻辑包装在循环中：

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

该代码片段展示了如何批量 **对 PDF 执行 OCR**，这在数字化项目中非常常见。

## 预期输出

运行单页示例（步骤 4）应打印类似以下内容：

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

如果处理的是多页书籍，控制台会显示每页的清理后文本，批处理脚本会在每个 PDF 旁生成相应的 `.txt` 文件。

## 常见陷阱及避免方法

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| 低分辨率源 PDF | 字符乱码、缺失单词 | 提高 DPI（`set_dpi(400)` 或更高） |
| 语言设置错误 | 大量未知符号，尤其是带重音的字符 | 使用 `engine.set_recognition_language(ocr.Language.FRENCH)` 或相应的枚举 |
| 大文件导致内存错误 | `MemoryError` 或在几页后崩溃 | 分块处理页面（`engine.recognize_pdf(..., max_pages=10)`） |
| PDF 中缺少字体 | 某些页面输出为空白 | 确认 PDF 实际包含光栅图像；有些 PDF 为矢量文件，需要不同的处理方式 |

## 图片示例

下面是一张工作流的快速示意图。alt 文本特意采用 SEO 友好的描述。

![如何进行 PDF OCR 工作流图，展示引擎初始化、语言设置、渲染选项、识别和文本提取](/images/ocr-workflow.png)

*该图并非代码运行的必需，但有助于视觉学习者了解每一步的定位。*

## 结论

我们已经从头到尾覆盖了在 Python 中 **如何对 PDF 进行 OCR**：创建 OCR 引擎、**更改 OCR 语言**、配置渲染以 **转换扫描的 PDF 文本**，以及最终 **从 PDF 中提取文本** 供后续使用。完整、可运行的示例已准备好直接嵌入任何项目，且可选的批处理脚本展示了如何扩展该方案。

接下来，你可能想探索：

- 通过遍历语言列表，为多语言档案添加 **对 PDF 执行 OCR** 的功能。
- 将提取的文本与 Elasticsearch 集成，实现全文搜索。
- 使用 OCR 创建可搜索的 PDF，方法是将文本层嵌入原始文件（许多库提供 `save_as_searchable_pdf` 方法）。

欢迎随意实验，调整 DPI 设置，或切换到其他 OCR 后端。基本原理保持不变，而你已经拥有了坚实的基础来进一步构建。

祝编码愉快，愿你的扫描文档终成可搜索的资源！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都提供完整的可运行代码示例和逐步解释。

- [识别 PDF 文本 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [使用 Aspose.OCR 进行图像文本 OCR 并选择语言](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [如何在 .NET 中使用 Aspose.OCR 进行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}