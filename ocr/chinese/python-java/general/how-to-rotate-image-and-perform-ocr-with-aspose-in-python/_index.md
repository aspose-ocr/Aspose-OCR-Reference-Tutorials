---
category: general
date: 2026-03-26
description: 学习如何在 Python 中旋转图像并执行 OCR。本指南还展示了如何对图像进行 OCR 预处理以及高效地从图像中提取文本。
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: zh
og_description: 如何正确旋转图像，然后使用 Aspose OCR 识别图像中的文字。请按照本分步教程对图像进行 OCR 预处理并提取文字。
og_title: 如何旋转图像并执行 OCR – 完整的 Python 指南
tags:
- Aspose
- Python
- Image Processing
- OCR
title: 如何在 Python 中使用 Aspose 进行图像旋转和 OCR
url: /zh/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 在 Python 中旋转图像并执行 OCR

是否曾想过 **如何旋转图像** 以便 OCR 引擎能够真正读取文本？也许你扫描的表单最终是横向的，或者相机拍摄的图片顺时针旋转了 90°。在这种情况下，肉眼看文字是正常的，但 OCR 引擎却看到一团乱。好消息是？只需几行 Python 代码和 Aspose 库，就能轻松修正方向、裁剪感兴趣的区域，然后提取文本。

在本教程中，我们将完整演示工作流：从加载旋转的 TIFF、纠正其方向、**为 OCR 预处理图像**，到最终 **从图像识别文本**。完成后，你将掌握 **如何执行 OCR**，并能够自信地 **从图像中提取文本**。

## 您需要的环境

- Python 3.8+（代码在任何近期版本均可运行）
- 通过 `pip` 安装的 `asposeocrjava` 与 `asposeimaging` 包
- 一张需要旋转的示例图片（例如 `rotated_form.tif`）
- 对图像处理有一点好奇心

不需要重量级框架——只需这两个 Aspose 包和一点 Python 逻辑。

---

## 第一步：安装 Aspose 包（如何执行 OCR）

在我们能够 **旋转图像** 或 **从图像识别文本** 之前，需要先安装实际完成这些工作的库。

```bash
pip install asposeocrjava asposeimaging
```

> **小贴士：** 如果你在公司代理后面，向命令添加 `--proxy http://proxy:port`。这些包是 Aspose .NET/Java 核心的纯 Python 包装器，安装通常是瞬间完成的。

---

## 第二步：加载源文件并旋转——核心的 “如何旋转图像” 步骤

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **为什么要旋转？** 大多数 OCR 引擎默认文本从左到右、从上到下排列。如果位图横向放置，引擎要么返回乱码，要么根本没有结果。旋转可以将像素网格对齐到预期的阅读顺序，从而显著提升准确率。

> **边缘情况：** 如果不确定图像需要旋转 90°、180° 还是 270°，可以检查 `source_image.width` 与 `source_image.height`，或使用 `exif` 方向标签。Aspose 的 `rotate_flip` 方法同样支持 `ROTATE_180` 和 `ROTATE_270_CLOCKWISE`。

> **图像预览（可选）：**  
> ![如何旋转图像示例](/assets/rotate-demo.png "如何旋转图像 – 旋转前后对比")

---

## 第三步：裁剪感兴趣区域——为 OCR 预处理图像

通常你只需要页面的一小块——比如签名栏或一段数字。裁剪可以去除噪声并加快 **如何执行 OCR** 的速度。

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **为什么要裁剪？** 缩小图像尺寸可以限制 OCR 引擎的搜索空间，降低误报并缩短处理时间。如果源文件中包含水印或其他可能干扰引擎的图形，裁剪同样有帮助。

> **提示：** 如果需要处理多个字段，可对不同的矩形重复裁剪步骤，并分别对每块执行 OCR。

---

## 第四步：初始化 OCR 引擎——“如何执行 OCR” 的核心

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **内部原理：** Aspose OCR 结合了 Tesseract 与专有图像分析技术。一次实例化引擎并在多张图像间复用，比每次创建新对象更高效。

---

## 第五步：输入裁剪后的图像并识别文本——如何从图像提取文本

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### 预期输出

如果 ROI 包含短语 “Invoice #12345 – Paid”，你会看到类似如下的输出：

```
Invoice #12345 – Paid
```

如果 OCR 表现不佳，可能会出现多余空格或字符误读（例如 “Invo1ce #I2345 – Pa1d”）。这时 **为 OCR 预处理图像** 的技巧——如调节对比度或二值化——就派上用场了。Aspose 还提供了可在第 5 步之前链式使用的额外过滤器，但上述基本流程已能满足大多数干净扫描件。

---

## 第六步：可选——微调 OCR 设置（高级 “如何执行 OCR”）

如果需要针对特定语言提升准确率，或想忽略某些字符，可对引擎进行调参：

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **何时使用：** 当文档中包含大量装饰符号且你不关心它们时，使用黑名单可以减少误检。

---

## 完整端到端脚本

将所有步骤整合在一起，下面是一段可直接运行的脚本，能够 **如何旋转图像**、**为 OCR 预处理图像**，并最终 **从图像识别文本**：

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

运行此脚本会将识别的文本打印到控制台，并将处理后的 ROI 保存为 `processed_roi.png`。你可以打开该 PNG 文件，验证旋转和裁剪是否如预期。

---

## 常见问题与注意事项

| 问题 | 答案 |
|----------|--------|
| **如果图像已经是正向的怎么办？** | 旋转步骤是幂等的——对已经正确方向的图像再旋转 90° 显然会把它弄歪。因此在调用 `rotate_flip` 前，应检查 `source_image.width` 与 `height`，或使用 EXIF 方向数据。 |
| **我的 OCR 输出包含多余的换行。** | 使用 `result.get_text().replace("\n", " ").strip()` 进行清理，或启用 `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`。 |
| **可以直接处理 PDF 吗？** | 可以——Aspose Imaging 能将 PDF 页面加载为图像（`Image.load("file.pdf")`），随后按照相同的旋转和 OCR 步骤处理。 |
| **有没有办法批量处理大量文件？** | 将 `ocr_rotated_image` 包装在遍历目录的循环中，或使用 Python 的 `concurrent.futures` 实现并行。 |
| **如何处理非英文语言？** | 通过 `ocr_engine.get_recognition_settings().set_recognition_language("fr")` 设置识别语言，例如法语等。 |

---

## 结论

我们已经完整演示了 **如何正确旋转图像**、通过裁剪 **为 OCR 预处理图像**，以及最终 **如何执行 OCR** 以 **从图像识别文本** 并 **提取文本**，全部使用 Aspose 的 Python 库。完整脚本展示了一个实用、可投入生产的工作流，能够轻松嵌入任何自动化流水线。

如果想进一步探索，可尝试：

- **图像增强**（对比度、二值化）在 OCR 前处理
- **多 ROI 提取** 用于包含多个字段的表单
- **批量处理** 整个扫描文档文件夹
- **与下游系统集成**（例如将提取的数据写入数据库）

欢迎根据自己的使用场景自行改造代码，祝编码愉快！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}