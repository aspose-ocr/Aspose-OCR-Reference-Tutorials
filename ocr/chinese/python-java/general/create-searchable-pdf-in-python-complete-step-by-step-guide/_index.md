---
category: general
date: 2026-06-19
description: 使用 Python OCR 将图像创建可搜索的 PDF。学习将 OCR 转换为 PDF、从图像提取文本，并快速对图像执行 OCR。
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: zh
og_description: 使用 Python OCR 将图像转换为可搜索的 PDF。本指南展示了如何将 OCR 转为 PDF、从图像中提取文本以及对图像进行
  OCR。
og_title: 使用 Python 创建可搜索的 PDF – 完整编程演练
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: 在 Python 中创建可搜索的 PDF – 完整的逐步指南
url: /zh/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中创建可搜索 PDF – 完整分步指南

是否曾需要从扫描的收据**创建可搜索的 PDF**但不知从何入手？你并不孤单——许多开发者在第一次尝试将文字图片转换为真正可搜索的 PDF 时都会遇到同样的难题。  

在本教程中，我们将演示一个实用方案，让你**对图像执行 OCR**，将 OCR 结果转化为**可搜索的 PDF**，并在需要时提取原始文本进行后续处理。没有冗余，只是一个可以直接复制粘贴到项目中的可运行示例。

## 您将学到的内容

- 如何在 Python 中搭建轻量级的 OCR 引擎  
- 将 **OCR 转换为 PDF** 并保存为可搜索文档的完整步骤  
- 如何 **从图像中提取文本** 以用于下游分析  
- 处理常见坑点（如图像方向、文件过大）的技巧  
- 一个完整的可运行脚本，方便你根据自己的使用场景进行改造  

### 前置条件

- 在机器上已安装 Python 3.8+  
- 对 pip 和虚拟环境有基本了解（可选但推荐）  
- 一张包含清晰、机器可读文本的图片文件（PNG、JPEG 等）  

如果你已经具备这些条件，下面我们开始吧。

## 步骤 1：安装所需库

你之前看到的代码片段使用了一个虚构的 `ocr` 包，但相同的思路同样适用于真实的库，例如 **EasyOCR**、**pytesseract** 或 **pdfminer.six**。本指南将使用 **EasyOCR**，因为它纯 Python 实现，支持多语言，并通过辅助工具提供便利的 PDF 转换方法。

```bash
pip install easyocr pillow
```

> **专业提示：** 在虚拟环境中安装 (`python -m venv venv && source venv/bin/activate`) 可以保持依赖整洁。

## 步骤 2：初始化 OCR 引擎 – 对图像执行 OCR

库准备好后，我们创建一个 OCR 引擎并指定使用英文文本。这是第一次**对图像执行 OCR**的地方。

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

为什么需要专门的 reader 对象？EasyOCR 会预加载语言模型，复用同一个 `reader` 处理多张图片比每次重新初始化要高效得多。

## 步骤 3：加载图像 – 从图像中提取文本

把图片加载到内存中。此步骤后面会**从图像中提取文本**，但现在我们仅仅是把它读进来。

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

如果你的图片是倒置或倾斜的，考虑在送入 OCR 引擎前使用 Pillow 的 `rotate` 或 `transpose` 方法进行校正。快速的目视检查可以为后续调试节省大量时间。

## 步骤 4：运行 OCR 引擎并捕获结果

下面是核心流程——将图像发送给 OCR 引擎并获取结构化数据。

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

`detail=1` 参数会返回边界框，这在后面**将 OCR 转换为 PDF**时会用到。如果你只关心原始字符串，可将其设为 `detail=0`。

## 步骤 5：将 OCR 结果转换为可搜索的 PDF – 将 OCR 转换为 PDF

EasyOCR 并未直接提供 PDF 写入功能，但我们可以使用 Pillow 和 `reportlab` 库自行拼接 PDF。为保持教程轻量，我们采用 `fpdf2`，它可以嵌入原始图像并覆盖不可见的文本层。

```bash
pip install fpdf2
```
```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

刚才发生了什么？我们把扫描的图像作为可见层放置，然后用白色文字（与白色背景融合）写入识别出的单词。搜索工具仍然能够读取隐藏的文字层，从而在不改变视觉效果的前提下，使 PDF **可搜索**。

## 步骤 6：保存 PDF 字节 – 将图像转换为 PDF

如果你更倾向于在内存中处理 PDF（例如通过 API 发送），可以捕获字节流而不是直接写入磁盘。

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

这行代码演示了经典的 **将图像转换为 PDF** 工作流：先有图像，运行 OCR，覆盖文本，最后输出 PDF 流。

## 步骤 7：验证结果 – 快速检查

运行脚本后，用任意 PDF 查看器打开 `receipt_searchable.pdf` 并尝试搜索框（Ctrl + F）。输入收据中已知出现的词汇——如果能跳转到正确位置，说明你已经成功**创建可搜索的 PDF**！  

如果搜索失败，请检查：

1. OCR 置信度分数（`conf` 值）。低置信度可能意味着图像模糊。  
2. 边界框坐标——有时 EasyOCR 会以不同的方向返回。  
3. PDF 查看器是否被设置为“仅图像”模式（虽然少见，但有些查看器有此选项）。

## 完整可运行脚本

将所有步骤组合起来，这就是完整、可直接运行的 Python 文件：

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

将其保存为 `searchable_pdf.py`，将 `YOUR_DIRECTORY` 占位符替换为真实路径，然后执行：

```bash
python searchable_pdf.py
```

你应该会看到确认信息，并在文件夹中得到一个全新的可搜索 PDF。

## 常见问题与边缘情况

**如果图像是彩色的怎么办？**  
EasyOCR 同时支持灰度和彩色图像，但将图像转换为灰度 (`pil_image.convert("L")`) 有时能提升噪声扫描的识别准确率。

**能处理多页 PDF 吗？**  
可以——遍历每一页的图像，执行 OCR 步骤，然后将每页追加到同一个 `FPDF` 对象中。记得在每张新图像前调用 `self.add_page()` 重置页面。

**有没有办法保留原始文本层而不是使用不可见的白色文字？**  
如果需要真正的“文字在图像下方”PDF（例如用于可访问性），可以考虑使用 `pdfminer` 或 `pikepdf` 嵌入带有正确 PDF 标签的隐藏文本层。这属于更高级的做法，但原理仍然是：背景图像 + 覆盖文字。

**如果 OCR 置信度低怎么办？**  
可以过滤掉低置信度的单词：

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## 总结 – 我们的成果

我们从一张简单的收据图片开始，**对图像执行 OCR**，提取识别出的字符串，最终**创建可搜索的 PDF**，其行为与任何专业扫描文档相同。整个过程覆盖了所有次要关键词——**将 OCR 转换为 PDF**、**从图像中提取文本**、**将图像转换为 PDF**、以及**对图像执行 OCR**——因此你现在拥有一个可复用的工具箱，可用于任何类似项目。

### 下一步

- 通过向 `easyocr.Reader(['en', 'es'])` 传入其他语言的 ISO 代码来尝试多语言识别。  
- 如果需要完全离线的解决方案，可将 EasyOCR 替换为 Tesseract；其余流水线保持不变。  
- 添加 OCR 置信度可视化（在图像上绘制边界框），以便调试有问题的扫描件。  

有想法想分享吗？留下评论，或者 fork 本项目。

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都提供完整的可运行代码示例和逐步解释。

- [使用 Aspose OCR 从图像中提取文本 – 分步指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [C# 将图像转换为 PDF – 保存多页 OCR 结果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [如何进行图像 OCR – 在 OCR 图像识别中执行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}