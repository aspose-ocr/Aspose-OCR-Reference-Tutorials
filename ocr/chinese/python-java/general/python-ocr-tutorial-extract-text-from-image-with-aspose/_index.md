---
category: general
date: 2026-03-26
description: Python OCR 教程：学习如何从图像中提取文本、加载图像进行 OCR，并使用 Aspose OCR 在几步内识别收据文本。
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: zh
og_description: Python OCR 教程：快速学习从图像中提取文本，加载图像进行 OCR，并使用 Aspise OCR 识别收据文本。
og_title: Python OCR 教程 – 从图像中提取文本
tags:
- OCR
- Aspose
- Python
title: Python OCR 教程 – 使用 Aspose 从图像提取文本
url: /zh/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR 教程 – 使用 Aspose 从图像中提取文本

有没有想过如何在不花费数小时编写自定义正则表达式的情况下，从模糊的收据或扫描的表单中提取文本？你并不孤单。在本 **python ocr tutorial** 中，我们将演示如何加载用于 OCR 的图像、在 Python 中执行 OCR，最后使用 Aspose OCR 库识别收据文件中的文本。  

阅读完本指南后，您将拥有一个可直接运行的脚本，它可以读取任何受支持的图像格式，提取文本内容，并将其打印到控制台。无需外部服务，无需 API 密钥——仅使用纯 Python 和强大的 OCR 引擎。  

## 您需要的条件

- Python 3.8 或更高（代码使用类型提示，建议使用较新的解释器）
- 通过 `pip install aspose-ocr` 安装 `asposeocrjava` 包
- 示例图像——例如包含典型商店收据的 `receipt_noisy.jpg`
- （可选）使用虚拟环境以保持依赖整洁

如果您已经满足以上条件，我们可以直接进入代码。  

## 步骤 1：安装并导入 Aspose OCR 类

首先，确保已安装 Aspose OCR 包。然后导入我们需要的类。

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**为什么重要：** 仅导入必要的符号可以保持命名空间整洁，并向解释器指明我们实际使用的库部分。这也能缩短后续代码行，使教程更易于阅读。

> **专业提示：** 如果您使用 Jupyter Notebook，请在安装行前加上 `!` 以在单元格中运行。

## 步骤 2：创建 OCR 引擎并启用深度学习模式

Aspose 提供多种引擎模式。对于大多数实际收据，深度学习模型提供最高的准确率，尤其是在噪声较多的扫描件上。

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**为什么使用深度学习？** 传统的基于规则的 OCR 在低对比度或变形字符上容易出错。深度学习模型经过数百万字形的训练，能够更好地适应变化——这正是您在手机拍摄的收据上 *perform OCR in Python* 时所需要的。

## 步骤 3：加载图像用于 OCR

现在我们真正 **load image for OCR**。Aspose.Imaging 支持 PNG、JPEG、BMP、TIFF 等多种格式，几乎可以指向任何文档图片。

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**常见陷阱：** 忘记在引擎上设置图像会导致运行时出现 `NullReferenceException`。加载文件后务必调用 `set_image`。

## 步骤 4：执行 OCR 并提取文本

在引擎准备就绪并附加图像后，我们终于可以 **perform OCR in Python** 并获取文本结果。

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

`recognize()` 方法返回一个 `OcrResult` 对象，其中不仅包含原始文本，还包括置信度分数、边界框和语言信息。对于快速的 **extract text from image** 场景，我们只需要 `get_text()`。

## 步骤 5：显示识别的文本

让我们看看引擎实际从收据中读取了什么。

```python
print("Recognized text:\n", recognized_text)
```

典型的输出如下：

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

如果输出包含乱码，请考虑在将图像加载到 OCR 引擎之前进行预处理（例如，提高对比度或应用去倾斜过滤器）。Aspose.Imaging 提供完整的图像增强工具套件，您可以将其串联使用。

## 处理边缘情况与提升准确性的技巧

### 1. 处理极度嘈杂的收据
如果收据严重模糊，您可以切换到 `OcrEngineMode.HIGH_SPEED` 模式进行更快但精度稍低的处理，然后在清理后的图像上再次使用 `DEEP_LEARNING` 进行第二遍处理。

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. 指定语言
默认情况下，Aspose 会尝试自动检测语言。对于英文收据，您可以锁定语言：

```python
ocr_engine.set_language("eng")
```

### 3. 内存管理
在循环处理大量图像时，请显式释放资源：

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. 将 OCR 结果保存到文件
有时您需要将提取的文本持久化，以便后续分析。

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## 完整工作示例

下面是将所有内容整合在一起的完整脚本。将其复制粘贴到名为 `receipt_ocr.py` 的文件中，调整图像路径，然后运行 `python receipt_ocr.py`。

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

运行脚本后，应该在控制台显示收据内容，并创建包含相同数据的 `receipt_output.txt`。

![Python OCR 教程 – 示例收据输出](https://example.com/receipt_output.png "python ocr 教程 示例")

*图片替代文字:* **python ocr tutorial – sample receipt output**

## 回顾与后续步骤

我们刚刚完成了一个 **python ocr tutorial**，展示了如何 **load image for OCR**、**perform OCR in Python**，以及最终使用 Aspose **recognize text from receipt** 文件。关键要点如下：

- 选择合适的引擎模式（深度学习以获得更高准确率）
- 在调用 `recognize()` 之前务必先附加图像
- 使用 `OcrResult` 对象提取干净的文本，然后根据需要存储或处理

接下来可以做什么？考虑将 Aspose Imaging 过滤器串联使用，以提升低对比度扫描的效果，或将脚本集成到 Flask API 中，以便通过网页表单上传收据。您也可以探索将 OCR 数据导出为 CSV，以实现会计自动化。

对处理多页 PDF 或非拉丁文字有疑问吗？留下评论——乐意帮助！

**准备提升您的文档自动化水平吗？** 获取代码，尝试不同的图像，让 OCR 引擎完成繁重的工作。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}