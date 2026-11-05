---
category: general
date: 2026-06-06
description: 使用 Python OCR 在几分钟内从图像中提取文本。了解多语言图像 OCR、自动检测语言的 OCR，以及如何准确提取 OCR 文本。
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: zh
og_description: 使用 Python OCR 快速提取图像中的文本。学习多语言图像 OCR、自动检测语言的 OCR，以及一步步提取 OCR 文本的方法。
og_title: 使用 Python OCR 从图像提取文本 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: 使用 Python OCR 从图像中提取文本 – 完整指南
url: /zh/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 从图像提取文本 – 完整指南

是否曾经需要**从图像中提取文本**，却不确定哪个库能够自动处理多语言？你并不孤单——开发者在处理国际文档、收据或扫描传单时，常常会问*如何提取 OCR 文本*。在本教程中，我们将通过一个实用的 Python 示例，演示不仅可以从图像中提取文本，还能**实时检测语言**，让多语言图像 OCR 轻而易举。

我们将从安装 OCR 包、启用**自动检测语言 OCR**、在示例图片上运行引擎，到最终打印检测到的语言和提取的字符串，全部一步步讲解。完成后，你将拥有一段可复用的代码片段，能够直接嵌入任何项目，无论是构建翻译流水线还是数据摄取服务。

## 提取图像文本 – 环境搭建

在编写代码之前，请确保你的工作站满足以下最低要求：

- Python 3.8 或更高（该库使用了旧版本不支持的类型提示）
- `pip` 用于包管理
- 一张包含至少两种不同语言文本的图像文件（例如 English + Spanish）

你还需要为本演示准备的 OCR 库。为了本指南的方便，我们使用虚构的 `ocr` 包，它的功能类似于 Tesseract、EasyOCR 等主流工具，但提供了简洁的 Python API。

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **小技巧：** 如果遇到权限错误，可在命令前加上 `python -m`，或使用虚拟环境——这样可以保持全局 site‑packages 的整洁。

## 创建 OCR 引擎实例

库准备好后，第一步是**创建 OCR 引擎实例**。可以把引擎想象成一个可在喂入图像前进行配置的智能扫描仪。

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

为什么要单独实例化引擎，而不是直接调用静态方法？引擎对象保存了配置状态（如语言偏好），这样在处理多张图片时可以复用，避免每次都重新初始化带来的开销。

## 启用自动检测语言 OCR

大多数 OCR 工具需要你手动指定语言代码——`eng` 表示英语，`spa` 表示西班牙语，依此类推。手动猜测语言会破坏**多语言图像 OCR**工作流的初衷。幸运的是，`ocr` 包提供了*自动检测语言 OCR*模式，能够在后台检查图像并自动选择最佳语言模型。

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

以这种方式启用**检测语言 OCR**，就不必维护冗长的语言代码列表。引擎会尝试匹配图像中出现的文字脚本——拉丁文、西里尔文、汉字等——并自动加载相应模型。

## 执行多语言图像 OCR

引擎准备就绪后，就可以真正**从图像中提取文本**了。`recognize_image` 方法接受文件路径，返回一个结果对象，包含原始文本以及检测到的语言。

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

如果你想知道*如何从 PDF 而不是 PNG 提取 OCR 文本*，同一引擎提供 `recognize_pdf`——只需更换方法名即可。底层的检测逻辑保持不变，仍然受益于相同的**自动检测语言 OCR**特性。

## 显示检测到的语言和提取的文本

最后，我们输出引擎发现的内容。结果对象公开 `detected_language`（如 `en`、`es` 的 BCP‑47 标签）和 `text`（原始 OCR 输出）。

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

在示例图片上运行脚本，应该会得到类似以下的输出：

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

可以看到，引擎正确识别出英语为主要语言，同时也捕获了西班牙语行——这正是一个健壮的**多语言图像 OCR**解决方案所应具备的表现。

### 检测失败怎么办？

如果图像模糊或脚本过于冷门，OCR 引擎可能会回退到默认语言（通常是英语）。此时可以强制指定语言列表：

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

但请记住，强制指定语言会削弱**自动检测语言 OCR**的便利性，仅在已知语言子集的情况下使用。

## 常见陷阱及可靠提取 OCR 文本的技巧

即使开启了自动检测，仍有一些常见问题可能导致错误：

1. **低分辨率图像** – 当分辨率低于 150 dpi 时，OCR 准确率会急剧下降。请放大图像或获取更高分辨率的扫描件。
2. **噪声和压缩伪影** – 在将图像送入引擎前，使用简单的阈值过滤（`opencv` 或 `Pillow`）进行预处理。
3. **单页混合脚本** – 某些引擎在同时处理拉丁文和中日韩字符时会出现困难。必要时将页面划分为多个区域，分别进行识别。

解决这些问题可以显著提升**从图像提取文本**的质量，尤其是在处理真实世界的多语言文档时。

## 完整可运行示例

下面是结合上述所有步骤的完整脚本。将其保存为 `multilingual_ocr.py`，然后在命令行执行。

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**预期输出**（假设示例图片包含英文和西班牙文）：

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

你可以将 `multilang_page.png` 替换为任何包含其他语言文本的图片——得益于**自动检测语言 OCR**，脚本仍会返回合理的语言标签和对应的文本。

![Extract text from image example](https://example.com/ocr-sample.png "Extract text from image")

## 结论

现在，你已经掌握了**如何从图像中提取 OCR 文本**、如何启用**自动检测语言 OCR**，以及如何用最少的代码处理**多语言图像 OCR**场景。通过创建 OCR 引擎实例、打开自动语言检测，并调用 `recognize_image`，你可以可靠地获取语言标识和原始文本。

接下来可以尝试将提取的字符串送入翻译 API、存入可检索的数据库，或将多页合并为单个 PDF 报告。你也可以在保持相同高层工作流的前提下，尝试不同的 OCR 后端（Tesseract、EasyOCR、Google Vision）——这得益于统一的**检测语言 OCR**接口。

如果遇到奇怪的问题，请回顾“常见陷阱”章节或微调图像预处理步骤。祝编码愉快，愿你的下一个项目充满正确检测、完美提取的文本！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步扩展。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索替代实现方案。

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}