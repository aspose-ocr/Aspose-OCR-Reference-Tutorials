---
category: general
date: 2026-03-26
description: 通过学习如何加载图像进行 OCR 并从特定区域提取数据，快速识别图像中的文字。请跟随本实操指南。
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: zh
og_description: 在 Python 中通过加载图像进行 OCR，定义感兴趣区域，并提取干净的文本来识别图像中的文字。了解完整的工作流程。
og_title: 从图像识别文字 – 完整的 Python OCR 教程
tags:
- OCR
- Python
- Image Processing
title: 从图像识别文本 – 步骤详解 Python OCR 教程
url: /zh/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像识别文本 – 完整的 Python OCR 教程

是否曾需要 **recognize text from image**，却不知从何入手？也许你有一份扫描的表单、收据或截图，只想获取特定框中的文字。好消息是，只需几行 Python 代码，你就可以加载用于 OCR 的图像、聚焦单个区域，并提取出精确的文本——无需手动复制。

在本教程中，我们将完整演示整个流程：加载图像、定义感兴趣区域（ROI）、运行 OCR 引擎并打印结果。结束时，你将能够将此代码片段嵌入任何需要从图像特定部分提取文本的项目中。无需繁重的图像处理管道，只需简洁、可读的代码即可立即使用。

## 前置条件

- 已安装 Python 3.8+  
- `ocr` 包（或任何兼容的 OCR 库）——使用 `pip install ocr-lib` 安装（请替换为实际使用的包名）  
- 包含待读取表单的 PNG/JPEG 图像  
- 对 Python 函数和类有基本了解  

如果你已经熟悉这些内容，太好了——可以直接跳过。如果还不熟悉，请先喝杯咖啡，确保上述项目已就绪；后续步骤默认它们已经准备好。

## 步骤 1：创建 OCR 引擎实例 – “recognize text from image” 核心

我们首先需要一个能够与 OCR 引擎通信的对象。它相当于大脑，后续会 **recognize text from image** 数据。

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **为什么重要：** 只初始化一次引擎即可在多张图像之间复用设置（如语言包），这能提升性能并保持代码整洁。

## 步骤 2：加载用于 OCR 的图像 – 将图片读入内存

现在我们真正 **load image for OCR**。库提供了一个便利的静态方法来读取文件并返回引擎可识别的对象。

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **小技巧：** 如果图像很大，考虑在加载前先缩放。较小的图像可以加快 OCR 速度，而对大多数印刷文本的准确性影响不大。

## 步骤 3：定义 OCR 感兴趣区域（ROI）

通常你并不需要整页内容——只需用户填写的特定框。定义 **OCR region of interest** 可以让引擎忽略其他部分，从而降低噪声并加快处理速度。

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **为何聚焦 ROI？**  
> - **速度：** 引擎扫描的像素更少。  
> - **准确性：** ROI 之外的背景图形可能干扰字符识别。  
> - **简洁性：** 你得到的字符串恰好对应关心的字段。

## 步骤 4：运行 OCR 过程 – 真正的时刻

一切准备就绪后，我们终于在定义好的 ROI 中 **recognize text from image**。

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

如果引擎支持多个区域，`ocr_result` 将是一个列表；在单 ROI 情况下，它是一个带有 `get_text()` 方法的简单对象。

## 步骤 5：提取并打印文本 – 获取最终输出

现在我们从结果对象中取出纯字符串并显示。此时你可以将输出写入数据库、CSV 文件或任何后续逻辑。

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**预期输出**（以填写的姓名字段为例）：

```
Text inside ROI:
 John Doe
```

如果 OCR 引擎返回了多余的空格或换行符，可以使用 `.strip()` 或正则表达式进行清理。

## 处理常见边缘情况

| 情况                                    | 处理方法                                                                    |
|----------------------------------------|-----------------------------------------------------------------------------|
| **低分辨率图像**                         | 使用 `Pillow` 的 `Image.resize` 进行放大后再加载。                           |
| **倾斜或旋转的文字**                     | 应用旋转校正，例如 `ocr.Imaging.Image.rotate`。                              |
| **多语言**                               | 在引擎上设置语言包：`ocr_engine.set_language('eng+spa')`。                 |
| **未定义 ROI**                           | 跳过 `add_region_of_interest`，引擎将处理整张图像。                         |
| **出现意外字符（如逗号）**               | 对字符串后处理：`extracted_text.replace(',', '')`。                        |

这些技巧可以让你的 **load image for OCR** 流程在源材料不完美时仍保持稳健。

## 完整可运行示例 – 复制、粘贴、运行

下面是完整脚本，可直接保存为 `.py` 文件并执行。它包含所有导入、错误处理以及一个用于验证图像是否存在的简易辅助函数。

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

运行此脚本后，会打印出 ROI 中清理后的字符串，为你提供可直接使用的数据。

## 结论

现在，你已经掌握了一套完整的 **recognize text from image** 方法：先 **load image for OCR**，再定义精确的 **OCR region of interest**，最后提取干净的文本。该方法适用于任何遵循上述模式的 Python OCR 库，并且可以轻松扩展以处理多个 ROI、不同语言或前置处理步骤。

接下来，你可以探索：

- **image preprocessing for OCR**（阈值化、去噪）以提升噪声扫描的准确率。  
- 使用 **extract text from ROI** 的结果填充 pandas DataFrame，进行批量数据分析。  
- 当需要更高可靠性和规模时，切换到云端 OCR 服务（Google Vision、Azure Computer Vision）。

动手试一试，调整矩形坐标以匹配自己的表单，让自动化为你工作。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}