---
category: general
date: 2026-06-16
description: 在 OCR 中定义感兴趣区域，以从身份证上提取西班牙语文本。了解如何加载图像进行 OCR 并高效指定 ROI。
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: zh
og_description: 在 OCR 中定义感兴趣区域，以从身份证中提取西班牙语文本。逐步指南，介绍如何加载图像并指定 ROI。
og_title: 在 OCR 中定义感兴趣区域 – 完整 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 在 OCR 中定义感兴趣区域 – 完整的 Python 教程
url: /zh/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 中定义感兴趣区域 – 完整 Python 教程

有没有想过如何**在 OCR 中定义感兴趣区域**，只读取图像中实际需要的部分？在本教程中，我们将一步步演示这一过程，并展示如何**加载图像进行 OCR**，以及仅用几行 Python 代码从身份证上提取西班牙语文本。  

如果你曾盯着噪声很大的扫描图像并想：“一定有更干净的方式来获取姓名字段”，那么你来对地方了。阅读完本教程后，你将能够提取所需的身份证文本，而不受背景杂乱的干扰。

## 你将学到

- 为什么在运行 OCR 之前应该**定义感兴趣区域**。  
- 使用流行的 Python OCR 包**加载图像进行 OCR**的完整步骤。  
- 如何使用像素坐标**指定 ROI**。  
- 如何可靠地**提取身份证文本**，即使源语言是西班牙语。  
- 处理诸如卡片旋转或低对比度扫描等边缘情况的技巧。  

不需要任何 OCR 先前经验——只需一个可用的 Python 3 环境以及一张你想测试的身份证 JPEG。

---

![Define region of interest illustration](placeholder.png){alt="Define region of interest example showing a highlighted rectangle on an ID card image"}

## 第一步：安装并导入 OCR 库

首先，你需要一个提供 `OcrEngine` 类的库，类似于你看到的代码片段。本文将使用虚构的 `ocr` 包，但相同的概念同样适用于 `pytesseract`、`easyocr` 或任何能够设置语言和 ROI 的包装器。

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*小贴士：* 如果你使用 `pytesseract`，`Rectangle` 类会变成一个简单的元组 `(left, top, width, height)`。其余流程保持不变。

## 第二步：加载图像进行 OCR

现在我们**加载图像进行 OCR**。引擎期望一个 `ocr.Image` 对象，因此我们将其指向保存身份证的文件。确保路径是绝对路径或相对于脚本工作目录的相对路径。

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

如果图像过大，建议先进行缩放；OCR 引擎在宽度低于 1500 px 的图像上运行更快。

## 第三步：如何指定 ROI（定义感兴趣区域）

这就是本教程的核心：**如何指定 ROI**。感兴趣区域就是一个矩形，告诉 OCR 引擎“只在这些像素范围内查找”。可以把它想象成在身份证的姓名字段上画一个框。

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

为什么是这些数值？在我们的示例图像中，姓名大约距离左边缘 120 px，距离顶部 80 px。请根据你处理的卡片布局进行调整。  

*边缘情况：* 如果卡片旋转了 90°，需要交换 `width` 和 `height` 并相应调整 `left`/`top`，或者在将图像送入引擎之前使用 Pillow 预先旋转图像。

## 第四步：在 ROI 内执行 OCR

在定义了 ROI 后，引擎会忽略矩形之外的所有内容。这不仅加快了处理速度，还能减少因背景图形导致的误报。

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` 调用返回一个对象，其中包含识别的文本、置信度分数以及每个单词的边界框。

## 第五步：提取身份证文本（并验证西班牙语输出）

最后，我们从 ROI 结果中**提取身份证文本**并打印。由于我们之前将语言设置为西班牙语，OCR 引擎会使用针对该语言的词典，提高对诸如 “ñ” 或 “á” 等带重音字符的识别准确度。

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### 预期输出

```
ROI text: JUAN PÉREZ GARCÍA
```

如果出现乱码，请再次确认图像确实是西班牙语，并且 OCR 库的语言数据文件已正确安装。

## 常见陷阱及避免方法

| 症状 | 可能原因 | 解决办法 |
|---------|--------------|-----|
| 返回空字符串 | ROI 未与任何文本相交 | 使用图像查看器验证坐标；如果可用，使用 `engine.debug_draw_roi()`。 |
| 出现大量乱码字符 | 语言包错误 | 重新安装西班牙语语言数据或切换到 `ocr.Language.AUTO`。 |
| 置信度分数低 | 图像模糊或对比度低 | 使用 OpenCV 进行预处理——应用 `cv2.GaussianBlur` 和 `cv2.threshold`。 |
| 尽管设置了 ROI，OCR 仍在整幅图像上运行 | 使用了旧版库 | 升级到最新的 `ocr` 包；旧版本会忽略 ROI。 |

## 扩展示例：多个 ROI

有时你需要提取多个字段（例如姓名和身份证号）。模式保持不变：更改 `engine.region_of_interest` 并再次调用 `recognize()`。

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

如果库支持，你也可以批量处理矩形列表，这样可以减少与 OCR 引擎的往返次数。

## 完整可运行脚本

将所有内容整合在一起，下面是一个可直接运行的脚本，能够**定义感兴趣区域**、**加载图像进行 OCR**，并从身份证中**提取西班牙语文本**。

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

运行脚本后，你应该在控制台看到姓名被打印出来。更改矩形的数值即可定位其他字段，这将成为任何身份证类文档的可复用工具。

## 后续步骤

- **批量处理：** 遍历一个文件夹中的身份证，并将每个提取的姓名保存到 CSV 文件。  
- **语言检测：** 让用户动态选择语言；`ocr.Language.AUTO` 很有用。  
- **后处理：** 使用正则表达式清理常见的 OCR 错误（例如，将姓名中的 “0” 替换为 “O”）。

通过掌握如何**定义感兴趣区域**，你已经开启了一种快速、准确提取**身份证文本**的强大方法，尤其在处理西班牙语文档时。

---

### TL;DR

我们演示了如何**在 OCR 中定义感兴趣区域**、**加载图像进行 OCR**，以及**如何指定 ROI**以从身份证中**提取西班牙语文本**。完整示例在一分钟内即可运行，并且只需微调坐标即可适配任何布局。试一试，调整矩形，感受 OCR 如激光般精准聚焦。

祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [如何通过准备矩形在 OCR 中提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [使用 Aspose.OCR 的语言选择在 C# 中提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [从图像提取文本 – 使用 Aspose.OCR 进行 .NET OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}