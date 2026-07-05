---
category: general
date: 2026-07-05
description: 使用 Python OCR 将图像转换为文本——一步一步的 Python OCR 示例，展示如何从图像中提取文本并识别 JPG 中的文字。
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: zh
og_description: 使用 Python OCR 将图像转换为文本。按照此 Python OCR 示例，在几分钟内从图像中提取文本并识别 JPG 中的文字。
og_title: 在 Python 中将图像转换为文本 – 完整 OCR 引擎指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: 在 Python 中将图像转换为文本 – 完整的 OCR 引擎 Python 教程
url: /zh/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中将图像转换为文本 – 完整的 OCR 引擎 Python 教程

是否曾经需要**将图像转换为文本**但不确定该信任哪个库？你并不是唯一遇到这种情况的人——许多开发者在首次尝试从扫描的收据或标志照片中提取字符时都会碰壁。好消息是？Python 的 OCR 生态系统让这项工作几乎毫不费力。

在本**python ocr 示例**中，我们将演示一个真实场景：你有一张包含西里尔字符的 JPEG，并希望可靠地**从图像中提取文本**。完成后，你将了解如何**从 jpg 文件中识别文本**，每一步为何重要，以及如何将代码适配到其他语言或图像格式。

## 你需要的准备

在深入之前，请确保你拥有：

* 已安装 Python 3.8+（建议使用最新的稳定版本）。
* 可用的互联网连接，用于安装 OCR 包。
* 包含你想提取文本的图像文件（例如 `cyrillic_sample.jpg`）。
* 可选但有用：使用虚拟环境来保持依赖整洁。

无需繁重的操作系统级依赖，也不需要晦涩的构建工具——只需几个 pip 命令和少量代码行。

## 步骤 1：安装 OCR 引擎 Python 包

首先，你需要获取一个能够良好配合 Python 使用的 OCR 引擎。本文教程中我们使用虚构的 `ocr` 包，因为它的 API 与许多真实库（如 `pytesseract` 或 `easyocr`）相似。使用以下命令进行安装：

```bash
pip install ocr
```

> **此步骤重要原因：** 安装该包会拉取实际执行重活的本地二进制文件和语言数据文件。如果跳过此步骤，一旦尝试 `import ocr` 就会抛出 `ImportError`。

## 步骤 2：导入模块并设置环境

库已经安装到机器后，导入所需的模块。我们还会配置日志，以便你能够看到引擎在底层的工作情况——这在后续对**从图像中提取文本**的文件（尤其是质量不佳的）时非常有用。

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **小技巧：** 如果你在 Jupyter Notebook 中工作，可能想设置 `logging.getLogger().setLevel(logging.DEBUG)` 以查看更多细节。

## 步骤 3：创建 OCR 引擎实例

创建引擎是任何**ocr engine python**工作流的基石。可以把它想象成在黑暗的房间里打开灯光；没有它，后续的流水线将一无所见。

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **此步骤关键原因：** `OcrEngine` 对象保存了语言包、预处理选项和硬件加速标志等配置。之后对这些进行任何更改都会影响后续的所有识别。

## 步骤 4：选择正确的语言 – 西里尔文支持

如果你处理的是西里尔文（或任何非拉丁脚本），需要告诉引擎加载哪个语言模型。否则会得到乱码，甚至空字符串。

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **特殊情况：** 某些引擎需要单独下载语言数据。如果出现 `LanguageDataNotFound` 错误，请在设置语言之前运行 `ocr.download_language('CYRILLIC')`。

## 步骤 5：加载要从中转换图像为文本的图像

这里才是真正开始**将图像转换为文本**的地方。OCR 引擎处理的是 `Image` 对象，而不是原始文件路径，因此我们需要先将 JPEG 包装成对象。

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **此步骤重要原因：** 加载图像后，引擎可以检查其尺寸、色深和 DPI。这些属性会影响引擎对**从 jpg 文件中识别文本**的效果。

## 步骤 6：识别文本 – Python OCR 示例的核心

现在我们终于让引擎完成它的本职工作：将像素转化为字符。`recognize` 方法返回一个结果对象，包含提取的字符串、置信度分数和边界框。

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **返回内容：** `ocr_result.text` 是一个保留换行的普通 Python 字符串。如果需要词级别的位置，可查看 `ocr_result.boxes`。

## 步骤 7：输出识别文本 – 验证你的图像转文本成功

检查是否成功**将图像转换为文本**的最简单方法是打印结果。在实际应用中，你可能会将其写入数据库或文本文件。

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### 预期输出

假设 `cyrillic_sample.jpg` 包含短语 “Привет, мир!” ，控制台将显示：

```
=== OCR OUTPUT ===
Привет, мир!
```

如果输出为空或毫无意义，请再次检查语言设置和图像质量。模糊的图像或低对比度常导致糟糕的**从图像中提取文本**结果。

## 处理常见问题

| 问题 | 出现原因 | 快速解决方案 |
|---------|----------------|-----------|
| **空字符串** | 语言模型未加载或图像太暗 | 确保 `ocr_engine.language` 与脚本匹配；使用 `ocr.Image.adjust_contrast()` 提高图像对比度 |
| **乱码字符** | 语言错误或混合脚本 | 设置 `ocr_engine.language = ocr.Language.MULTI` 或进行两次识别（先拉丁文后西里尔文） |
| **大批量处理慢** | 引擎顺序处理图像 | 启用多线程：`ocr_engine.set_threads(4)` |
| **内存泄漏** | 未释放图像资源 | 识别后调用 `cyrillic_image.close()` |

> **小技巧：** 对于批量处理，可将识别循环放在 `try/except` 块中，以捕获偶发的 `ocr.EngineError` 异常，防止整个任务中止。

## 扩展示例 – 从 JPEG 到 PDF，从西里尔文到多语言

我们用于**将图像转换为文本**的模式适用于任何光栅格式：PNG、BMP、TIFF，甚至扫描的 PDF（只需先将页面提取为图像）。如果需要从包含多种语言的图像文件**提取文本**，可以传入列表：

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

如果处理的是手机拍摄的高分辨率照片，建议加入预处理步骤：

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

这些调整常常能把普通的**python ocr 示例**提升为生产级代码。

## 完整可运行脚本

下面是完整的、可直接运行的脚本，将所有步骤整合在一起。将其保存为 `convert_image_to_text.py` 并执行 `python convert_image_to_text.py`。



## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都提供完整的可运行代码示例和一步步的解释，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [将图像转换为文本 – 从 URL 执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何通过在 OCR 中准备矩形来提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}