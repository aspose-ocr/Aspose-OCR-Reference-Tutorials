---
category: general
date: 2026-07-05
description: 使用 Python OCR 从图像中提取文本。了解如何识别图像中的文字、加载 OCR 图像以及仅用几行代码设置 OCR 语言。
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: zh
og_description: 使用 Python OCR 从图像中提取文本。本指南展示了如何识别图像中的文本、加载用于 OCR 的图像、以 Python 方式创建
  OCR 引擎以及设置 OCR 语言。
og_title: 在 Python 中从图像提取文本 – 快速识别文本
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 使用 Python 从图像中提取文本 – 快速识别文本
url: /zh/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中从图像提取文本 – 快速识别文字

是否曾经需要 **从图像中提取文本**，却不知道该选哪个库？如果你曾经问自己 *如何在不使用外部工具的情况下识别图像中的文字*，那么你来对地方了。在本教程中，我们将启动一个小型 OCR 引擎，指向一张图片，并提取其中的文字——仅此而已。

我们将逐步演示：**创建 OCR 引擎 python**、**设置 OCR 语言**、**加载图像进行 OCR**、异步触发识别，最后读取结果。完成后，你将拥有一个可直接嵌入任何项目的独立脚本，无论是文档数字化工具还是读取表情包的聊天机器人。

## 你需要准备的环境

- Python 3.8+（代码在 3.10 及更高版本同样可用）  
- `ocr` 包（Tesseract 的轻量包装器 – 使用 `pip install ocr` 或你喜欢的分支安装）  
- 包含可读文字的图像文件（`.jpg`、`.png` 等）  
- 对异步部分稍作耐心（很快的，放心）

就这些——没有笨重的依赖，没有本地编译。如果系统已经装有 Tesseract，`ocr` 包会自动检测到。

## 步骤 1：创建 OCR 引擎 – 提取的核心

首先，你需要一个能够与底层 OCR 引擎通信的对象。可以把它想象成后续处理图片的“大脑”。

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*为什么重要*：没有引擎就没有语言设置或异步能力的上下文。`OcrEngine` 类封装了对 Tesseract 的低层命令行调用，提供了简洁的 Python API。

## 步骤 2：设置 OCR 语言 – 告诉引擎期待什么

如果文档是英文，可以使用默认设置，但显式设置是个好习惯。这也演示了如何 **设置 OCR 语言** 以适配其他语言环境。

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **专业提示**：对于多语言 PDF，你可以传入类似 `[ocr.Language.ENGLISH, ocr.Language.FRENCH]` 的列表。引擎会自动尝试这两种语言。

## 步骤 3：加载图像进行 OCR – 将图片读入内存

现在我们实际 **加载图像进行 OCR**。包装器支持惰性加载，文件只有在引擎需要时才会被读取。

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*边缘情况*：如果图像非常大（超过 5 MB），建议先缩放以加快识别速度。可以使用 Pillow 完成：

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## 步骤 4：启动异步识别 – 不阻塞应用

OCR 可能需要一两秒，尤其是大幅扫描时。`recognize_async` 方法返回一个 future，你可以稍后轮询，让 **在 OCR 背景运行时执行其他工作**。

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

为什么使用异步？在 Web 服务器中，你不希望单个请求卡住整个工作池。future 对象让你可以在异步代码中 `await`，或仅在真正需要结果时阻塞。

## 步骤 5：获取结果 – 仅在必要时阻塞

当你真正需要文字时，调用 `future.get()`。此调用 **仅在此处阻塞**，意味着程序的其余部分在 OCR 完成前仍保持响应。

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

如果你在 `asyncio` 循环中，也可以直接 `await future` ——包装器兼容这两种写法。

## 步骤 6：使用识别出的文本 – 数据已就绪

现在有了 `result` 对象，获取纯字符串非常简单。我们先打印出来，并演示如何写入文件。

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**预期输出**（为简洁起见已截断）：

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

如果图像中没有文字，`result.text` 将是空字符串——请优雅地处理这种情况。

## 完整工作示例 – 一步到位的脚本

下面是完整、可直接运行的程序。复制粘贴，修改 `image_path`，即可使用。

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **注意**：将 `"YOUR_DIRECTORY/large_document.jpg"` 替换为实际的图像路径。只要系统已安装 Tesseract 并在 `PATH` 中可访问，脚本在 Windows、macOS 和 Linux 上均可运行。

## 常见陷阱与规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **乱码字符** | 语言设置错误或缺少语言数据文件。 | 确保 `engine.language` 与文本语言匹配，并且相应的 `.traineddata` 文件已放置在 Tesseract 的 `tessdata` 目录下。 |
| **大图像性能慢** | OCR 的耗时大致与像素数量成正比。 | 在送入引擎前进行缩放或下采样（参考 Pillow 示例）。 |
| **Future 永不完成** | 图像文件损坏或不可读取。 | 将 `future.get()` 包裹在 try/except 中，并在识别前使用 `image.is_valid()` 验证图像。 |
| **Unicode 丢失** | | |

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索项目中的其他实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [使用 Aspose OCR 提取图像文字 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [将图像转换为文字 – 从 URL 执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [提取图像文字 – 使用 Aspose OCR 进行 .NET OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}