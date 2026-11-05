---
category: general
date: 2026-06-06
description: 如何使用 Python 对 PDF 进行 OCR 并从图像创建可搜索的 PDF 文件。学习在几分钟内添加可搜索文本并将图像转换为 PDF/A。
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: zh
og_description: 一步步教你对 PDF 进行 OCR。学习使用简单的 Python 脚本添加可搜索文本并将图像转换为 PDF/A。
og_title: 如何对PDF进行OCR – 创建可搜索PDF的快速指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: 如何在 Python 中对 PDF 进行 OCR – 从图像创建可搜索的 PDF
url: /zh/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何对 PDF 进行 OCR – 将扫描图像转换为可搜索的 PDF

是否曾经想过 **如何对 PDF 进行 OCR**，当你手头只有发票或收据的扫描图像时？你并不孤单。在许多办公室，收到的纸质文件往往是平面的 PNG 或 JPEG，接下来——让这些内容可搜索——常常像是一个黑盒。

好消息是，只需几行 Python 代码，你就可以 **创建可搜索的 PDF**，**添加可搜索的文本**，甚至 **将图像转换为 PDF/A** 以便长期存档。在本教程中，我们将逐步演示每一步，解释其意义，并提供一个可直接运行的脚本，供你在任何项目中使用。

> **小技巧：** 同样的方法适用于多页扫描，只需遍历文件，引擎会自动完成繁重的工作。

---

## 所需条件

在开始之前，请确保你的机器上具备以下条件：

| 条件 | 为什么重要 |
|------|------------|
| Python 3.9 或更高版本 | 支持现代语法并拥有更好的库兼容性 |
| 基于 `pdfium` 的 OCR 引擎（如 `pdfocr` 或商业 SDK） | 同时处理图像识别和 PDF/A 生成 |
| 需要转换为可搜索 PDF 的图像文件（PNG、JPEG、TIFF） | 文本的来源 |
| 对输出文件夹的写入权限 | 脚本才能保存新生成的 PDF |

如果尚未安装 OCR SDK，请运行：

```bash
pip install pdfocr   # replace with your vendor's package name
```

就这么简单——无需复杂的系统依赖，只需一次 pip 安装。

---

## OCR PDF 概览

从宏观上看，这个过程包括三个简单的操作：

1. **识别** 图像中的文字，同时保留原始图形。  
2. **导出** OCR 结果并将原始图像一起保存为 **可搜索的 PDF/A**（适合长期保存的 PDF 版本）。  
3. **验证** 生成的文件是否在原始图片上叠加了可选中、可搜索的文字层。

下面的代码展示了每一步，并解释了背后的 *why*。

---

## 步骤 1：从图像中识别文字

首先让 OCR 引擎读取像素并返回一个结果对象，该对象同时包含原始图像和提取的文字。可以把它想象成引擎为你“阅读”发票。

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### 为什么重要

- **保留图形** 意味着布局（表格、徽标、印章）保持扫描时的原始样子。  
- `result` 对象通常包含一个隐藏的文字层，稍后我们会把它嵌入 PDF。  
- 使用 `recognize_image` 而非 `recognize_pdf` 可以避免额外的转换步骤，从而加快单页图像的处理速度。

#### 常见变体

- 如果你有 **多页 TIFF**，直接传入文件路径；大多数引擎会把每页当作单独的图像处理。  
- 对于已经包含图像的 PDF，你可以调用 `engine.recognize_pdf("file.pdf")`，直接跳过此步骤。

---

## 步骤 2：将 OCR 结果导出为可搜索的 PDF/A

现在我们把步骤 1 中得到的 `result` 交给引擎，生成一个新文件。这里的关键标志是 *PDF/A*——PDF 的 ISO 标准长期保存版本。

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### 为什么重要

- **可搜索的 PDF**：输出文件包含隐藏的、可选中的文字层。现在可以使用 Ctrl + F 在文档中搜索。  
- **PDF/A 合规**：某些组织（法律、金融）要求使用 PDF/A 进行审计存档；此步骤会自动满足该要求。  
- 此方法还能 **在不扁平化图像的情况下添加可搜索文字**，保持视觉保真度。

#### 边缘情况：需要普通 PDF？

如果不在乎 PDF/A，只需将 `save_as_pdfa` 替换为 `save_as_pdf`，其余工作流保持不变。

---

## 步骤 3：验证可搜索的 PDF

一次快速的完整性检查可以帮助你避免后期的神秘错误。用任意 PDF 查看器打开生成的文件，尝试选中一个单词并使用搜索功能。

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### 预期输出

运行脚本后，控制台会打印：

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

打开文件后，你应当看到原始发票图像上叠加了一层淡淡的、不可见的文字层。选中任意单词，你会发现它是可选中的——**这就是刚刚添加的可搜索文字**。

---

## 为已有 PDF 添加可搜索文字（进阶）

有时你已经拥有一个 PDF，但仍需要 **为其添加可搜索文字**。同样的引擎可以将 OCR 结果覆盖到已有的 PDF 上：

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

这里的 `apply_to` 会把隐藏层与原始页面合并，让你 **在不重新扫描的情况下创建可搜索 PDF**。

---

## 常见陷阱与技巧

| 陷阱 | 如何避免 |
|------|----------|
| **低分辨率源图像** (< 150 dpi) | 放大或请求更高分辨率的扫描；低于 150 dpi 时 OCR 准确率会显著下降。 |
| **缺少语言数据** | 为你的 OCR 引擎安装相应的语言包（`pip install pdfocr[eng,spa]`）。 |
| **输出文件夹不可写** | 以足够权限运行脚本或选择其他目录。 |
| **PDF/A 验证失败** | 确保未嵌入不受支持的字体或 JavaScript；大多数 SDK 在使用 `save_as_pdfa` 时会自动处理。 |

---

## 完整脚本 – 单文件解决方案

下面是一段自包含的脚本，整合了上述所有步骤。复制粘贴后，替换占位路径，即可在几秒钟内 **将图像转换为 PDF/A**。

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**脚本功能概述：**  
1. 加载 OCR 引擎。  
2. 读取指定图像并提取文字。  
3. 写入 **可搜索的 PDF/A**，即可直接分发或归档。

如果需要一次性处理整个文件夹，只需将 `main` 逻辑包装成函数，遍历 `os.listdir()` 并对每个文件重复上述三步。

---

## 后续步骤与相关主题

掌握了 **如何对 PDF 进行 OCR** 之后，你可以进一步探索以下方向：

- **批量处理：** 使用 `concurrent.futures` 并行 OCR 处理数十份发票。  
- **元数据注入：** 为 PDF 添加创建日期或发票编号，便于后续索引。  
- **混合 PDF：** 将可搜索文字与原始图像嵌入同一文件，形成文档的 “数字孪生”。  
- **其他输出格式：** 如需可编辑的下游系统，可导出为 **DOCX** 或 **HTML**。

这些都建立在你刚学到的核心概念之上——识别、导出、验证。

---

## 小结

简而言之，你现在已经掌握了 **如何对 PDF 进行 OCR**：只需三行 Python 代码，就能把普通图像转换为 **可搜索的 PDF/A**。脚本负责繁重的工作，保留原始图形，并生成符合标准的文档，供搜索、归档或共享使用。

试着用自己的发票、收据或扫描合同来运行它吧。如果遇到问题，欢迎在下方留言或查阅 SDK 官方文档——通常会有更多示例。祝编码愉快，尽情享受让任何图像瞬间可搜索的全新能力！

![如何对 PDF 进行 OCR 示例，展示原始图像与可搜索 PDF 的叠加效果](placeholder.png "如何对 PDF 进行 OCR 示例")

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，每篇都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 .NET 中使用 Aspose.OCR 进行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [使用 Aspose.OCR for Java 进行 PDF 文本识别 – OCR 操作](/ocr/english/java/ocr-operations/)
- [C# 将图像转换为 PDF – 保存多页 OCR 结果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}