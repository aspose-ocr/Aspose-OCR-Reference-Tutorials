---
category: general
date: 2026-06-28
description: 学习如何使用 Aspose OCR for Python 从图像中识别文本并执行 OCR。包括设置 OCR 语言和提取置信度分数的步骤。
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: zh
og_description: 使用 Aspose OCR 在 Python 中识别图像文字。本指南展示如何设置 OCR 语言、对图像执行 OCR，以及读取置信度水平。
og_title: 从图像识别文字 – 完整的 Python OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: 使用 Aspose OCR 识别图像中的文本 – 完整 Python 指南
url: /zh/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 进行图像文字识别 – 完整 Python 指南

是否曾经需要 **从图像中识别文字**，但不确定哪个库能够兼顾速度和准确性？你并不孤单。在文档自动化的世界里，能够 **对图像执行 OCR** 是日常需求——无论是数字化收据、扫描护照，还是从多语言标志中提取数据。

在本教程中，我们将通过一个动手示例，展示如何使用 Aspose OCR for Python **从图像中识别文字**，并且我们还会介绍 **如何设置 OCR 语言**，让引擎知道它正在处理拉丁文、 Cyrillic（西里尔文）或其他任何脚本。完成后，你将拥有一个可直接运行的脚本，能够打印完整文本、逐行置信度，甚至每个单词的边界框。

## 你需要的东西

- **Python 3.8+** (代码在任何近期版本上都可运行)
- **Aspose.OCR for Python via Java** 包 – 使用 `pip install aspose-ocr` 安装
- 一个图像文件（例如 `mixed_script.png`），其中包含你想提取的文本
- 基本的 IDE 或编辑器——VS Code、PyCharm，甚至简单的文本编辑器都可以

无需繁重的依赖，也不需要编译本地二进制。只需 pip 安装，即可使用。

## 步骤 1：安装并导入 OCR 引擎

首先，让我们把库安装到机器上并导入所需的类。

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **小贴士：** 如果你在公司代理后面，向 pip 命令添加 `--proxy` 参数。这样可以省去后期大量的排查工作。

## 步骤 2：创建引擎并 **如何设置 OCR 语言**

创建 `OcrEngine` 实例就像调用其构造函数一样简单，但真正的威力在于告诉引擎期望的语言。这正是回答 “**如何设置 OCR 语言**” 问题的部分。

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

这有什么重要性？OCR 算法使用特定语言的字符模型；设置正确的语言可以显著提升准确率，尤其是对于字符形状相似的脚本（比如拉丁文中的 “0” 与 “O” 与西里尔文中的 “О”）。

## 步骤 3：**对图像执行 OCR** – 识别文本

现在我们将图像路径交给引擎，让它完成魔法。该方法返回一个 `RecognitionResult` 对象，包含你可能需要的所有信息。

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

如果文件未找到，Aspose 会抛出 `FileNotFoundError`。在生产代码中请将调用包装在 `try/except` 块中——没有什么比未处理的异常导致服务崩溃更糟糕的了。

## 步骤 4：输出完整识别文本

最常见的需求就是“给我文本”。`getText()` 方法会将所有检测到的行连接成一个字符串。

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

你会看到类似如下内容：

```
Full text: Hello World!
This is a sample mixed‑script image.
```

这就是 **从图像中识别文字** 的核心——一行代码即可返回引擎能够解读的全部内容。

## 步骤 5：（可选）显示每行检测的置信度

置信度分数让你评估可靠性。分数低于 0.70 的行可能需要人工审查。

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

典型输出：

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## 步骤 6：（可选）获取每个单词的边界框 – 适用于 UI 高亮

如果你在构建一个查看器，让用户点击单词以查看其 OCR 数据，边界框坐标就是宝贵信息。

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

示例输出：

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

这些坐标以像素为单位，相对于原始图像，因此可以直接在画布上叠加。

## 完整可运行脚本

将所有内容组合在一起，这里提供一个可直接运行的脚本，你可以放入任何项目。只需将 `YOUR_DIRECTORY/mixed_script.png` 替换为实际的图像路径。

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

使用以下方式运行：

```bash
python ocr_demo.py
```

你应该会在控制台看到完整的提取文本、置信度分数和边界框。

## 常见问题与边缘情况

### 如果我的图像包含多种语言怎么办？

Aspose OCR 支持多语言检测，但需要传入 **组合语言标志**。例如，要同时处理拉丁文和西里尔文：

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

管道符 (`|`) 操作符合并枚举。这满足了多语言场景下的 “**对图像执行 OCR**” 需求。

### 如何提升低分辨率图像的准确性？

- **预处理** 图像：提高对比度、进行二值化，或使用 Pillow 等库进行放大。
- **设置正确的 DPI**（如果已知）；Aspose 会遵循图像元数据。
- **选择正确的语言**——越具体，模型表现越好。

### 我可以仅提取图像的特定区域吗？

可以。使用 `recognizeRegion` 方法（在基础示例中未展示），并传入定义感兴趣区域的矩形对象。当你只需要表格或特定文本块时，这非常方便。

## 结论

我们刚刚完整演示了如何使用 Aspose OCR for Python **从图像中识别文字** 的端到端示例。现在你已经了解如何 **对图像执行 OCR**，正确设置 **OCR 语言**，以及获取置信度分数和单词级别的边界框，以用于后续的 UI 工作。

从这里你可能：

- 尝试其他语言（`Language.Arabic`、`Language.Japanese` 等）
- 将脚本集成到 Web 服务（Flask/Django）中，提供 OCR API
- 将边界框数据与前端画布结合，让用户高亮文本

可能性与您需要数字化的文档一样广阔。遇到顽固的图像无法识别？留下评论，我们一起排查。祝编码愉快！

![图像文字识别示例](/images/ocr_example.png "图像文字识别 – Aspose OCR 输出")

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本教程演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose OCR 进行多语言图像文字识别](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [如何在 OCR 图像识别中设置阈值](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}