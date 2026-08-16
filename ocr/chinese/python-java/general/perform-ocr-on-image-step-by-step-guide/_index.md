---
category: general
date: 2026-03-18
description: 对图像执行 OCR，以快速提取图像中的文本。了解如何加载图像进行 OCR，创建 OCR 引擎，并通过语言选项提升 OCR 准确性。
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: zh
og_description: 使用本详细指南对图像进行 OCR。学习如何加载图像进行 OCR，创建 OCR 引擎，并提升 OCR 准确率，实现可靠的文本提取。
og_title: 对图像进行 OCR – 完整编程教程
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 对图像进行 OCR – 步骤指南
url: /zh/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上执行 OCR – 完整编程教程

是否曾经需要**在图像上执行 OCR**，但不确定该选哪个库或如何获得可靠的结果？你并不孤单。在本指南中，我们将逐步讲解**从图像中提取文本**所需的一切，从加载图片到调整语言选项，让你在每一步都**提升 OCR 准确率**。

我们将介绍如何**为 OCR 加载图像**、如何**创建 OCR 引擎**以及每个设置为何重要。完成后，你将拥有一个可直接运行的脚本，打印识别出的文本，并且了解每行代码背后的“原因”——不再是模糊的“查看文档”捷径。让我们开始吧。

## 你需要的环境

- Python 3.8+（代码使用 f‑strings 和类型提示）
- 假设的 `ocr_lib` 包 – 使用 `pip install ocr_lib` 安装
- 包含清晰印刷文本的图像文件（例如 `lab_report.png`）
- 基本的文本编辑器或 IDE（VS Code、PyCharm，随你喜欢）

如果你已经拥有这些，太好了——已准备就绪。如果没有，请从 python.org 下载 Python 并运行 pip 命令；只需一分钟。

![在图像上执行 OCR – 示例输出显示提取的文本](/images/ocr-example.png)

## 步骤 1：创建 OCR 引擎 – 如何在 Python 中**创建 OCR 引擎**

在进行任何识别之前，库需要一个保存配置和运行时状态的引擎对象。可以把引擎看作是整个操作的大脑。

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**为什么这很重要：** 早期实例化引擎可以让你随后附加语言选项，并且它会缓存内部模型，以加快后续调用的速度。

## 步骤 2：为 OCR 加载图像 – 正确的**加载图像用于 OCR**方式

现在我们已有引擎，需要给它提供要读取的内容。`setImageFromFile` 方法接受文件系统路径；该路径可以是绝对路径，也可以是相对于脚本工作目录的相对路径。

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**小技巧：** 使用绝对路径或 `os.path.join`，以避免脚本在不同文件夹运行时出现“文件未找到”的意外。

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## 步骤 3：提升 OCR 准确率 – 调整**语言选项**以**提升 OCR 准确率**

开箱即用的 OCR 能工作，但特定领域的词汇（如实验室术语）常常会让它出错。通过提供自定义词典和黑名单，可以减少诸如将“0”误认成“O”等错误。

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**为什么这有帮助：** 词典告诉 OCR 模型“HPLC”是有效的词元，防止它将该词拆分成乱码。黑名单则让模型将模糊符号视为噪声，从而直接**提升 OCR 准确率**。

## 步骤 4：在图像上执行 OCR – 核心的**在图像上执行 OCR**调用

引擎已准备好并且图像已加载，现在是实际识别文本的时候了。此步骤返回一个 `OcrResult` 对象，你可以查询原始文本、置信度分数或边界框。

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

如果图像模糊，结果中的置信度数值会较低。这提示你需要在将图像送入引擎前进行预处理（例如，提高对比度）。

## 步骤 5：从图像中提取文本 – 获取最终字符串

最后，我们向 `OcrResult` 请求其文本表示。`getText()` 方法返回一个纯文本字符串，可用于后续处理（保存到文件、写入数据库等）。

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**预期输出：** 假设 `lab_report.png` 包含一个简单表格，你可能会看到类似如下内容：

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

这就完成了**从图像中提取文本**的部分。

## 完整工作示例 – 综合全部步骤

下面是一段将前面各部分拼接在一起的完整脚本。你可以将其复制粘贴到 `run_ocr.py` 中，然后执行 `python run_ocr.py`。

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### 快速验证清单

| ✅ | 项目 |
|---|------|
| ✔️ | 引擎已创建（`create OCR engine`） |
| ✔️ | 图像已加载（`load image for OCR`） |
| ✔️ | 语言选项已设置（`improve OCR accuracy`） |
| ✔️ | 已执行 OCR（`perform OCR on image`） |
| ✔️ | 已提取文本（`extract text from image`） |

运行脚本并观察控制台。如果看到包含报告内容的“OCR Output”块，说明你已成功**在图像上执行 OCR**。

## 常见陷阱及避免方法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **模糊的输入** | OCR 模型无法区分字符 | 使用 OpenCV 进行预处理：`cv2.GaussianBlur` 或提高 DPI |
| **语言错误** | 默认语言可能设置为非英文 | 在 `recognize()` 之前调用 `engine.setLanguage("eng")` |
| **缺少词典条目** | 特定领域的词汇会变成乱码 | 如步骤 3 所示，通过 `setDictionary` 添加它们 |
| **黑名单字符导致** |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}