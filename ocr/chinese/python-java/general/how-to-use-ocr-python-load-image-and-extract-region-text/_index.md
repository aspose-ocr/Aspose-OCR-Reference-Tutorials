---
category: general
date: 2026-06-25
description: 如何在 Python 中使用 OCR —— 学习如何加载用于 OCR 的图像、识别区域文本以及快速提取区域文本。
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: zh
og_description: 如何在 Python 中使用 OCR —— 步骤指南：加载图像、识别特定区域的文本并提取发票号码。
og_title: 如何使用 OCR Python：加载图像并提取区域文本
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 如何使用 OCR Python：加载图像并提取区域文本
url: /zh/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR：加载图像并提取区域文本

**在 Python 中使用 OCR** 比你想象的更简单。是否曾盯着扫描的发票，想只提取发票号码而不解析整页内容？你并不孤单——许多开发者在首次接触光学字符识别时都会遇到这种困扰。在本指南中，我们将演示如何加载图像进行 OCR、定义矩形区域、识别该区域的文本，最后提取区域文本。完成后，你将拥有一个可直接运行的脚本，能够隔离任意所需的文本片段。

> *小技巧：* 如果你处理的是 PDF，先将每页转换为图像——大多数 OCR 库对 PNG/JPEG 支持最佳。

## 您需要的条件

- Python 3.8+（建议使用最新稳定版）  
- 一个提供 `OcrEngine` 类的 OCR 库（例如通过 `pip install ocr-lib` 安装的 **ocr**）  
- 示例图像——这里使用放在你可控文件夹中的 `invoice.png`  
- 对矩形（x, y, width, height）的基本了解  

无需繁重依赖，无需 GPU——仅使用普通 CPU，保持高度可移植。

---

## 如何使用 OCR：初始化引擎（步骤 1）

在读取任何文本之前，你需要创建一个 OCR 引擎实例。它相当于分析像素模式的大脑。

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*为什么重要：* 初始化引擎会加载语言模型并设置默认配置。如果跳过此步骤，一旦调用 `recognize_region` 就会抛出异常。

---

## 加载图像进行 OCR（步骤 2）

引擎准备好后，我们将图像喂给它。库的 `Image.load` 方法支持常见格式并会对位图进行标准化。

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

如果文件未找到，Python 会抛出 `FileNotFoundError`。请确保路径是绝对路径或相对于脚本工作目录的相对路径。  

*边缘情况：* 某些 OCR 引擎要求灰度图像。如果发现准确率低，先将图像转换为灰度：

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## 在区域内识别文本（步骤 3）

定义区域即告诉引擎**在哪里**查找。`Rectangle` 接受浮点数，以实现亚像素精度，这在处理高分辨率扫描时非常有用。

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – 矩形左上角坐标（像素）  
- **width, height** – 矩形的宽高  

你可能会好奇这些数值该如何获取。快速方法是使用任意图像编辑器（如 GIMP 或 Paint.NET）打开图像，利用选区工具读取坐标。  

*为什么不直接 OCR 整页？* 限定区域可以减少噪声、加快处理速度，并显著提升对发票号码等小字段的识别准确度。

---

## 提取区域文本（步骤 4）

设置好区域后，调用引擎仅识别该切片。返回的结果对象包含原始文本和置信度分数。

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

如果 OCR 引擎支持多语言，你可以传入可选的语言代码：

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*常见陷阱：* 有些引擎返回的是单词列表而非单个字符串。此时需要将它们拼接起来：

```python
text = " ".join(region_result.words)
```

---

## 输出提取的发票号码（步骤 5）

最后，打印或保存提取的文本。你还可以对字符串进行后处理，去除多余空白或非数字字符。

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

运行脚本并使用正确对齐的矩形时，输出应类似于：

```
Invoice number: 20231578
```

如果出现乱码，请再次检查矩形坐标，或考虑提升图像分辨率。

---

## 完整工作示例

将上述步骤整合在一起，下面是一个可直接复制粘贴运行的完整脚本：

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

将文件保存为 `extract_invoice.py`，将 `YOUR_DIRECTORY` 替换为实际文件夹路径，然后运行：

```bash
python extract_invoice.py
```

你应该会在控制台看到打印出的发票号码。

---

## 常见问题

**Q: 如果发票号码使用了花哨的字体怎么办？**  
A: 大多数现代 OCR 引擎能够处理各种字体，但你可以通过训练自定义语言模型或对图像进行预处理（例如阈值滤波）来提升准确度。

**Q: 能一次提取多个字段吗？**  
A: 完全可以。创建一个 `Rectangle` 对象列表——每个字段对应一个矩形——然后遍历它们，将每个结果存入字典即可。

**Q: 这在多页 PDF 上有效吗？**  
A: 先使用 `pdf2image` 或类似工具将每页转换为图像，然后对每页执行相同的基于区域的提取即可。

---

## 小结

本教程介绍了**如何在 Python 中使用 OCR**，包括加载图像、在特定区域识别文本以及提取该区域文本——非常适合从扫描文档中提取发票号码、订单 ID 或任何小数据片段。通过聚焦感兴趣的区域，你可以获得更快的速度、更高的准确率以及更少的后处理工作。

准备好下一步了吗？尝试扩展脚本，以**load image for OCR**方式批量处理文件夹中的发票，或尝试对日期、总额等不同字段使用**recognize text in region**。思路相同——只需更改矩形坐标。

如果你遇到任何问题或有改进想法，欢迎在下方留言。祝编码愉快，愿你的 OCR 流程始终精准无误！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [通过准备矩形在 OCR 中提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [如何使用 AspOCR：针对 .NET 的图像 OCR 预处理过滤器](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}