---
category: general
date: 2026-07-05
description: 使用 Python OCR 从图像中提取文本。学习如何加载图像进行 OCR、从区域读取文本，以及使用几行代码从发票中提取文本。
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: zh
og_description: 使用 Python OCR 从图像中提取文本。本指南展示了如何加载图像进行 OCR、从指定区域读取文本，以及快速提取发票中的文本。
og_title: 从图像中提取文本 – 使用 OCR 读取区域文本
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 从图像中提取文本 – 使用 OCR 读取区域文字
url: /zh/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 使用 OCR 从区域读取文本

是否曾经需要**从图像中提取文本**，但只关心特定部分——比如发票上的总金额？你并不是唯一遇到这种情况的人。在许多实际项目中，你会发现自己需要**从区域读取文本**，而不是解析整张图片。幸运的是，只需几行 Python 代码，你就可以加载用于 OCR 的图像，定义感兴趣区域（ROI），并精确提取所需字符。

在本教程中，我们将逐步演示一个完整且可运行的示例，展示如何**加载用于 OCR 的图像**、设置 ROI，最终**从发票中提取文本**。完成后，你将拥有一个可直接使用的代码片段，适用于任何支持基于区域识别的流行 OCR 库。

---

## 你需要的条件

- Python 3.8+（代码在 3.10 上同样可运行）  
- 一个提供 `OcrEngine` 类的 OCR 包（演示中我们使用虚构的 `ocr` 模块；请将其替换为 `pytesseract`、`easyocr` 或任何支持 ROI 的库）  
- 示例图像——例如 `invoice.png`——其中包含清晰的印刷文本  
- 对 Python 函数和类有基本了解（不需要深度学习背景）

如果你已经具备上述条件，太好了——让我们开始吧。如果没有，请从 python.org 下载最新的 Python，并通过 `pip install your-ocr-lib` 安装 OCR 包。

![从图像中提取文本示例](extract-text-from-image.png "从图像中提取文本 – 基于区域的 OCR 演示")

*上图展示了我们将要针对的区域（红色矩形），用于**从图像中提取文本**。*

## 步骤 1：安装并导入 OCR 库

首先，确保你的环境中已安装 OCR 库。下面的导入方式适用于大多数提供高级 `OcrEngine` 类的包。

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **小技巧：** 如果使用 `pytesseract`，需要单独安装 Tesseract 可执行文件，并将 `pytesseract.pytesseract.tesseract_cmd` 设置为其路径。

## 步骤 2：创建 OCR 引擎并设置语言

创建引擎非常简单，但指定语言可以显著提升准确率，尤其是针对包含数字和英文单词的发票。

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

为什么要这么做？OCR 引擎使用语言模型来预测字符；告知其预期使用英文可以减少误判，例如把“0”误读为“O”。

## 步骤 3：加载用于 OCR 的图像

现在我们实际**加载用于 OCR 的图像**。大多数库接受文件路径或 Pillow 图像对象。这里我们为简便使用库自带的加载器。

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

确保路径指向正确的目录；常见错误是脚本在不同工作目录运行时忘记使用相对路径。

## 步骤 4：定义感兴趣区域（ROI）

定义 ROI 是**从区域读取文本**的核心。可以把它想象成在发票中包含总金额的部分绘制一个矩形。

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` 和 `top` 表示矩形左上角的 X、Y 坐标。  
- `width` 和 `height` 设置矩形的宽度和高度。  
- 你可以使用显示像素坐标的图像查看器来尝试不同的数值。

> **为什么 ROI 很重要：** 对整页进行 OCR 会浪费 CPU 资源，并且常常因无关的文本、表格或图形引入噪声。聚焦于特定区域可以获得更干净的结果并加快处理速度。

## 步骤 5：对指定区域执行 OCR

在一切准备就绪后，我们终于**从图像中提取文本**——但仅限于我们定义的 ROI。

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` 方法返回一个对象，通常包含原始字符串、置信度分数，有时还包括每个单词的边界框。对我们而言，只需要纯文本即可。

## 步骤 6：输出提取的文本

让我们打印结果，看看得到什么。此步骤演示了在真实场景中**从发票中提取文本**。

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### 预期输出

```
Text inside ROI:
Total Amount: $1,245.67
```

如果你的发票采用不同的布局，你会看到矩形内的任何文本——可能是发票号、日期或采购订单编号。

## 步骤 7：将其封装为可复用函数（可选）

为了在多个发票之间复用该方案，将逻辑封装到函数中。这也展示了 **区域 OCR** 作为通用工具的用法。

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

现在你可以使用任意发票调用该函数：

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **空白输出** | ROI 实际上未覆盖任何文本（坐标错误）。 | 使用图像编辑器仔细检查像素值；添加可视化调试覆盖层。 |
| **乱码字符** | 图像分辨率低或对比度差。 | 预处理图像：转换为灰度，应用阈值化（`cv2.threshold`）。 |
| **语言设置错误** | 引擎默认使用不包含所需字符集的语言。 | 显式将 `ocr_engine.language` 设置为 `ENGLISH` 或相应的语言环境。 |
| **性能延迟** | 对大图像反复运行 OCR。 | 在加载前缩放图像，或先裁剪出 ROI 再进行处理。 |

## 扩展示例：多个 ROI

有时发票包含多个需要提取的字段——例如同时提取总金额和发票日期的**从发票中提取文本**。你可以遍历矩形列表：

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

这种模式保持代码整洁，并且以后可以轻松添加更多区域。

## 结论

我们刚刚介绍了使用 Python OCR **从图像中提取文本**的完整端到端工作流，重点在于特定区域。通过**加载用于 OCR 的图像**、定义**感兴趣区域**并调用引擎，你可以可靠地**从区域读取文本**——非常适合从发票中提取总额、从收据中提取日期或任何其他局部数据。  

欢迎随意尝试

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步学习。每个资源都包含完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [提取图像文本 – 使用 Aspose.OCR 进行 .NET OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何通过在 OCR 中准备矩形来提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}