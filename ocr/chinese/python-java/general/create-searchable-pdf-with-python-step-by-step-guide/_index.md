---
category: general
date: 2026-05-31
description: 使用 Python OCR 将扫描图像创建可搜索的 PDF。学习如何将扫描的图像 PDF 转换、将 TIFF 转换为 PDF，并在几分钟内添加
  OCR 文本层。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: zh
og_description: 即时创建可搜索的 PDF。本指南展示如何使用单个 Python 脚本运行 OCR、转换扫描的图像 PDF 并添加 OCR 文本层。
og_title: 使用Python创建可搜索的PDF – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: 使用 Python 创建可搜索 PDF – 步骤指南
url: /zh/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建可搜索 PDF – 步骤指南

是否曾想过 **从扫描页创建可搜索 PDF** 而不需要使用大量工具？你并不孤单。在许多办公流程中，扫描的 TIFF 或 JPEG 会被放到共享磁盘，下一位同事只能手动复制‑粘贴文本——既痛苦又容易出错，还浪费时间。

在本教程中，我们将逐步演示一种简洁的编程解决方案，让你一次性 **转换扫描图像 PDF**、**将 TIFF 转为 PDF**，并 **添加 OCR 文本层**。完成后，你将拥有一个可直接使用的脚本，能够运行 OCR、嵌入隐藏文本，并生成可索引、可搜索或可放心分享的 PDF。

## 所需环境

- Python 3.9+（任意近期版本均可）
- `aspose-ocr` 与 `aspose-pdf` 包（通过 `pip install aspose-ocr aspose-pdf` 安装）
- 一个扫描图像文件（`.tif`、`.png`、`.jpg`，或仅包含图像的 PDF 页面）
- 适量的内存（OCR 引擎轻量，即使是笔记本也能胜任）

> **小贴士：** 如果你使用 Windows，最简便的获取这些包的方式是在提升权限的 PowerShell 窗口中运行上述命令。

```bash
pip install aspose-ocr aspose-pdf
```

现在前置条件已经完成，让我们进入代码部分。

## 步骤 1：创建 OCR 引擎实例 – *create searchable pdf*

首先我们实例化 OCR 引擎。可以把它想象成读取每个像素并转换为字符的大脑。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **为什么重要：** 只初始化一次引擎可以保持内存占用低。如果在循环中对每页都调用 `OcrEngine()`，很快就会耗尽资源。

## 步骤 2：加载扫描图像 – *convert tiff to pdf* & *convert scanned image pdf*

接下来，将引擎指向你想要处理的文件。API 接受任何光栅图像，因此 TIFF 与 JPEG 同样适用。

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

如果你手头有仅包含扫描图像的 PDF，也可以使用 `load_image`，因为 Aspose 会自动提取第一页。

## 步骤 3：准备 PDF 保存选项 – *add OCR text layer*

这里我们配置最终 PDF 的保存方式。关键标志是 `create_searchable_pdf`；将其设为 `True` 即告诉库嵌入一个与可视内容对应的不可见文本层。

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **文本层的作用：** 当你在 Adobe Reader 中打开生成的文件并尝试选取文本时，会看到隐藏的字符。搜索引擎也能索引这些字符——非常适合合规或归档需求。

## 步骤 4：运行 OCR 并保存 – *how to run OCR* in a single call

魔法时刻到来。一次方法调用即可运行识别引擎并将可搜索 PDF 写入磁盘。

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` 方法返回一个状态对象，可用于检查错误，但在大多数直接场景下，上面的简单调用已经足够。

### 预期输出

运行脚本后会打印：

```
PDF saved as searchable PDF.
```

如果打开 `scanned_page_searchable.pdf`，你会发现可以选取文本、复制‑粘贴，甚至使用 `Ctrl+F` 搜索。这正是 **create searchable pdf** 工作流的标志。

## 完整可运行脚本

下面是完整的、可直接运行的脚本。只需将占位路径替换为实际文件位置。

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

将其保存为 `create_searchable_pdf.py` 并执行：

```bash
python create_searchable_pdf.py
```

## 常见问题与边缘情况

### 1️⃣ 能处理多页 PDF 吗？

可以。使用 `ocr_engine.load_image("file.pdf")`，然后在循环中对每页调用 `ocr_engine.recognize(pdf_save_options, page_number)`。库会自动生成多页可搜索 PDF。

### 2️⃣ 如果源文件是高分辨率 TIFF（300 dpi 以上）怎么办？

更高的 DPI 能提升 OCR 准确度，但也会占用更多内存。如果出现 `MemoryError`，请先对图像进行降采样：

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ 如何更改 OCR 的语言？

在加载图像之前，设置引擎的 `language` 属性：

```python
ocr_engine.language = "fra"   # French
```

完整的语言代码列表请参阅 Aspose 文档。

### 4️⃣ 如果需要保持原始图像质量怎么办？

`PdfSaveOptions` 类提供 `compression` 属性。将其设为 `PdfCompression.None` 即可完整保留光栅数据。

```python
pdf_save_options.compression = "None"
```

## 生产环境部署建议

- **批量处理：** 将核心逻辑封装为接受文件路径列表的函数。将每次成功/失败记录到 CSV，以便审计。
- **并行化：** 使用 `concurrent.futures.ThreadPoolExecutor` 在多核上并行运行 OCR。记住每个线程需要独立的 `OcrEngine` 实例。
- **安全性：** 若处理敏感文档，请在沙箱环境中运行脚本，并在处理完毕后立即删除临时文件。

## 结论

现在你已经掌握了使用简洁的 Python 脚本 **create searchable pdf** 的完整方法。通过初始化 OCR 引擎、加载 TIFF（或任意光栅图像）、配置 `PdfSaveOptions` 以 **add OCR text layer**，最后调用 `recognize`，整个 **convert scanned image pdf** 与 **convert TIFF to PDF** 流程即可变成一次可重复执行的命令。

下一步？尝试将此脚本与文件监视器结合，使任何新扫描文件一放入文件夹就自动生成可搜索 PDF。或尝试不同的 OCR 语言，以支持多语言档案。当 OCR 与 PDF 生成相结合时，可能性无限。

对 **how to run OCR** 在其他语言或框架中的实现还有疑问？欢迎在下方留言，祝编码愉快！

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## 接下来该学习什么？

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}