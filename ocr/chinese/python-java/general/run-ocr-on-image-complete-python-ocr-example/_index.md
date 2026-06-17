---
category: general
date: 2026-03-18
description: 使用 Python 快速对图像进行 OCR。学习如何从 PNG 识别文本，加载图像进行 OCR，并在一步步指南中提取图像中的单词。
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: zh
og_description: 使用 Python 对图像进行 OCR。本教程展示如何识别 PNG 中的文本、加载用于 OCR 的图像，并通过完整代码示例从图像中提取单词。
og_title: 在图像上运行 OCR – Python 指南
tags:
- OCR
- Python
- Image Processing
title: 在图像上运行 OCR – 完整的 Python OCR 示例
url: /zh/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上运行 OCR – 完整的 Python OCR 示例

是否曾经需要 **在图像上运行 OCR**，但不知从何入手？你并不孤单；许多开发者在首次处理扫描文档的文本提取时都会遇到这个难题。在本教程中，我们将逐步演示一个 **Python OCR 示例**，帮助你 **从 PNG 文件中识别文本**、**加载图像进行 OCR**，以及 **从图像中提取带置信度的单词**——只需几行代码即可完成。

我们会覆盖所有必需的内容：所需库、如何设置引擎、每一步的意义以及输出的样子。完成后，你可以直接把这段代码片段放入自己的项目，立即从任意图像中提取文本。没有冗余，只提供实用、可运行的解决方案。

## 你需要准备的东西

在开始之前，请确保你已经具备以下条件：

- 已安装 Python 3.8 或更高版本  
- 已安装 `ocrengine` 包（或任何提供 `OcrEngine` 类的库）。可以通过 `pip install ocrengine` 安装——如果使用其他 OCR 库（如 `pytesseract`），请相应更改名称。  
- 一张你想要处理的图像文件（PNG、JPG 等）——本指南使用 `invoice.png` 作为示例。  

就这些。没有笨重的依赖，没有外部服务，纯粹的 Python。

![在图像上运行 OCR 示例，展示一张已扫描的发票](/images/run-ocr-on-image.png)

*Alt text: 在图像上运行 OCR 示例 – 正在处理的已扫描发票*

## 第一步 – 安装并导入 OCR 库

首先，把 OCR 引擎装进环境并导入它。如果你使用的是假设的 `ocrengine` 包，导入方式如下：

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**为什么这一步很重要：** 导入正确的类后，你才能使用后面会调用的 `setImageFromFile`、`recognize` 等方法。如果跳过这一步，Python 会抛出 `ModuleNotFoundError`，导致连图像都加载不了。

## 第二步 – 创建 OCR 引擎实例

库准备好后，我们需要一个引擎对象来保存识别过程的配置和状态。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*小技巧：* 有些 OCR 引擎在此时允许你微调语言模型或 DPI 设置。对于一个基础的 **python OCR 示例**，默认参数已经足够，但如果处理低分辨率扫描件，可以考虑在这里进行调整。

## 第三步 – 加载要处理的图像

接下来合理的步骤是 **加载图像进行 OCR**。只需将引擎指向 PNG（或任何受支持格式）文件的路径即可。

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**内部到底发生了什么？** 引擎读取像素数据，将其转换为识别算法能够理解的格式，并在内部保存。如果文件路径错误，会抛出 `FileNotFoundError`，请务必确认图像文件确实存在。

## 第四步 – 运行识别算法

图像加载完成后，我们终于 **在图像上运行 OCR**，提取文本内容。

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

此时，引擎会扫描位图，进行模式匹配，并返回一个对象，里面包含所有检测到的单词、行以及置信度指标。

## 第五步 – 遍历识别出的单词并显示置信度

任何 OCR 工作流中最有价值的部分，就是查看 **每个提取词的置信度**。这能告诉你引擎对每个单词的确信程度，必要时可以过滤掉低置信度的结果。

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**预期输出**（示例）：

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

现在，你可以清晰地看到 **从图像中提取了哪些单词**，以及每个检测的可靠程度。这正是 **从图像中提取单词** 流程的核心。

## 处理常见的边缘情况

### 如果图像是灰度的怎么办？

某些 OCR 引擎在彩色图像上表现更佳。如果你发现整体置信度偏低，尝试先将 PNG 转换为对比度更高的黑白图像再喂给引擎。可以使用 Pillow 来完成：

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### 处理多语言文档

如果文档同时包含英文和西班牙文，你需要使用多语言模型来 **从 PNG 中识别文本**。大多数引擎允许在初始化时设置语言列表：

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### 过滤低置信度的单词

有时你只想保留置信度高于 90 % 的单词。下面的快速过滤示例可以满足需求：

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## 完整、可直接运行的脚本

将上述所有步骤整合在一起，下面是一段可以复制粘贴并立即运行的完整脚本（只需替换为你的 PNG 路径）。

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

使用以下命令运行：

```bash
python run_ocr_on_image.py
```

你应该会在控制台看到单词列表及其置信度百分比，正如前文示例所示。

## 常见问题

**这能处理 JPG 或 TIFF 文件吗？**  
完全可以。`setImageFromFile` 方法接受底层库能够解码的任何格式，因此你可以 **在图像上运行 OCR**，支持 JPG、TIFF、BMP 等多种类型。

**可以在循环中处理多张图像吗？**  
当然可以。将加载和识别步骤放入 `for` 循环遍历文件路径列表即可。若库要求每张图像使用全新实例，请记得在循环内部重新初始化引擎。

**如果我想要一次性获取整段文本，而不是逐词返回怎么办？**  
大多数 OCR 结果对象都提供 `getText()` 方法，返回完整文档的字符串。例如：

```python
full_text = ocr_result.getText()
print(full_text)
```

## 后续步骤与相关主题

了解了如何 **在图像上运行 OCR** 后，你可以进一步探索：

- **后处理**：使用正则表达式清理从发票中提取的日期、金额或 ID。  
- **批量处理**：结合 `os.listdir()`，一次性处理整个文件夹的扫描文档。  
- **替代库**：`pytesseract` 是一个流行的开源选项，工作流类似——只需替换引擎调用即可。  
- **导出结果**：将提取的单词和置信度写入 CSV，供后续分析使用。  

这些扩展都直接基于我们在此奠定的基础，让你能够将原始 OCR 数据转化为可操作的信息。

---

### TL;DR

我们展示了一个简洁的 **python OCR 示例**，演示了如何 **加载图像进行 OCR**、**在图像上运行 OCR**，以及 **从图像中提取单词** 并报告置信度。完整脚本已准备就绪，你现在掌握了将其迁移到任何需要 **从 PNG（或其他格式）识别文本** 的项目中的方法。快去尝试，调节置信度阈值，让你的应用在几分钟内具备文本感知能力。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}