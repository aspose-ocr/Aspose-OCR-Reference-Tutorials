---
category: general
date: 2026-06-22
description: 仅用几行 Python 代码即可对图像进行 OCR。学习如何加载用于 OCR 的图像、识别 PNG 中的文本，并高效使用 OCR 引擎。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: zh
og_description: 使用 Python 快速对图像进行 OCR。本教程展示如何加载 OCR 图像、从 PNG 识别文本，以及使用带置信度的 OCR 引擎。
og_title: 使用 Python 对图像进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中对图像进行 OCR – 完整指南
url: /zh/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中对图像执行 OCR – 完整指南

是否曾经想要 **对图像文件执行 OCR**，却在第一行代码就卡住了？你并不孤单。在本教程中，我们将一步步演示如何 **加载图像进行 OCR**、搭建轻量级 **OCR 引擎**，以及仅用几条命令 **从 PNG 中识别文本**。

我们会覆盖从安装库到微调白名单，只保留数字和大写字母的全部过程。完成后，你将拥有一个可直接在任何项目中使用的脚本——没有神秘步骤，也没有多余内容。

## 你将学到

- 如何在 Python 中 **以编程方式使用 OCR 引擎**。  
- **从本地文件夹加载图像进行 OCR** 的完整步骤。  
- 为什么以及如何将识别限制在自定义字符集上。  
- 如何 **从 PNG 中识别文本** 并安全地处理结果。  

**先决条件：** 已安装 Python 3.7+，熟悉终端操作，并准备好一张想要读取的图像（例如 `serial-number.png`）。无需任何 OCR 经验。

---

## Perform OCR on Image – 初始化 OCR 引擎

首先需要创建 OCR 引擎的实例。可以把引擎想象成分析像素并将其转化为字符的大脑。

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*为什么这很重要：* 没有引擎就没有办法处理图像。`OcrEngine` 类把所有繁重的工作——预处理、分割和字符分类——封装到一个可复用的对象中。

---

## Load Image for OCR – 提供 PNG 文件

引擎创建好后，需要把要读取的图片喂给它。库期望一个 `ImageStream` 对象，你可以直接从文件路径创建它。

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*小技巧：* 保持图像为高对比度格式（黑字白底），并避免压缩伪影；这些会干扰 OCR 算法。

---

## Restrict Characters – 白名单仅限数字和大写字母

通常你只关心一小部分字符——比如仅包含 A‑Z 和 0‑9 的序列号。设置白名单后，引擎会忽略其他所有字符，从而显著提升准确率。

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*底层原理是什么？* 引擎会在最终分类阶段之前构建一个过滤器，剔除不在白名单中的字形。当图像中有噪点或不需要的装饰性文字时，这尤其有用。

---

## Recognize Text from PNG – 运行 OCR 过程

在引擎准备好且图像已加载后，你终于可以 **对图像执行 OCR**。`recognize()` 调用会运行完整的流水线并返回一个结果对象。

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

如果你关心性能，这个方法在现代笔记本上对 300 × 200 px 的 PNG 通常只需几百毫秒即可完成。

---

## Output and Verify – 获取识别文本

最后一步是从结果对象中提取纯文本。任何未匹配白名单的字符都会自动被丢弃，得到的字符串即可直接用于后续处理。

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*典型输出：* `AB12C3D4E5`（假设图像中正好包含该序列号）。  

如果输出为空或乱码，请再次检查图像质量和白名单；常见的坑是不小心遗漏了需要的字符。

---

## Edge Cases & Common Gotchas

| 情况 | 检查要点 | 建议解决方案 |
|-----------|---------------|---------------|
| **文件未找到** | 路径拼写错误或文件缺失 | 使用 `os.path.abspath` 在调用 `set_image` 前验证完整路径。 |
| **低对比度图像** | 文本与背景融合 | 在将图像喂给引擎前使用 `Pillow` 或 `OpenCV` 进行简单阈值化处理。 |
| **出现意外字符** | 白名单过于严格 | 将缺失的字符添加到白名单字符串中。 |
| **大尺寸图像** | 识别速度慢 | 将图像宽度最大限制为 1024 px；OCR 质量通常仍然保持良好。 |

---

## Full Script – 可直接运行

下面是完整的、独立的脚本，整合了所有步骤。将其保存为 `ocr_demo.py`，将 `YOUR_DIRECTORY` 替换为实际文件夹路径，然后运行 `python ocr_demo.py`。

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*预期控制台输出*（当 PNG 包含 `SN12345` 时）：

```
Recognized text: SN12345
```

---

## Conclusion

现在，你已经掌握了在 Python 中 **对图像执行 OCR** 的完整流程，从 **加载图像进行 OCR** 到 **从 PNG 中识别文本**，并使用可自定义的 **OCR 引擎** 提取干净的结果。该方法简洁、可扩展，几乎可以直接用于所有序列号类扫描任务。

接下来可以尝试将白名单换成小写字母，实验不同的图像格式（JPEG、BMP），或将脚本集成到批处理流水线中。引擎 → 图像 → 设置 → 识别 → 输出 的模式几乎适用于所有 OCR 场景。

有问题或遇到顽固的图像无法识别？在下方留言吧，祝编码愉快！

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram showing how to perform OCR on image with a Python OCR engine")


## 接下来该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助你在已有技巧的基础上进一步深入。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索项目中的替代实现方式。

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}