---
category: general
date: 2026-06-25
description: 使用 Python 对图像进行 OCR 预处理并识别扫描文档中的文本。一步一步的教程，附完整代码。
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: zh
og_description: 使用 Python 对图像进行 OCR 预处理并识别扫描文档中的文本。请跟随本详细且可运行的教程。
og_title: Python 中的 OCR 图像预处理 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python 中的 OCR 图像预处理——完整指南
url: /zh/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中对 OCR 进行图像预处理 – 完整指南

是否曾想过如何 **preprocess image for OCR**，让文字输出干净可靠？你并不孤单——大多数开发者在扫描页倾斜或对比度混乱时都会遇到同样的问题。好消息是，只需几行 Python 代码就能把这堆乱七八糟的图像矫正、二值化，并返回清晰、可搜索的文本。

在本教程中，我们将逐步演示 **preprocess image for OCR** *以及* **recognize text from scanned document** 文件的完整步骤，使用流行的 OCR 库。完成后，你将拥有一个可直接运行的脚本，了解每个设置背后的原因，并知道如何在棘手的边缘案例中进行调优。

## 你需要准备什么

- Python 3.8 或更高（代码在 3.10+ 也可运行）
- 一个提供 `OcrEngine`、`ImagePreProcessingOptions` 和 `Image` 类的 OCR 包（例如示例中使用的虚构 `ocr` 模块）
- 一份略有倾斜或对比度低的扫描或拍摄文档
- 你喜欢的 IDE 或一个简单的终端——无需繁重的 GUI

就这些。无需额外的二进制文件，也不需要 Docker 操作。让我们开始吧。

## Preprocess Image for OCR – 步骤详解

下面是核心工作流，分为五个清晰阶段。每个阶段包括 **为什么** 要这么做、完整的 **代码**，以及对底层实现的简短 **解释**。

### 步骤 1：创建 OCR 引擎实例

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*为什么这很重要：*  
`OcrEngine` 对象是整个操作的大脑。它保存语言包、置信度阈值等配置，最重要的是图像‑预处理标志。先实例化它可以为后续的技巧提供干净的起点。

### 步骤 2：启用自动去倾斜和二值化

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*为什么这很重要：*  
- **Deskewing** 将图像旋转，使文本行水平。基线倾斜超过几度时，OCR 引擎会表现不佳。  
- **Binarization** 将图片转换为纯黑白，去除可能干扰字符分类器的背景噪声。  
这两个选项在许多现代库中都是 *automatic* 的，但仍需手动打开——因此需要显式赋值。

> **Pro tip:** 如果你的源图像已经完美对齐，可以将 `auto_deskew=False`，以节省毫秒级的处理时间。

### 步骤 3：加载需要处理的倾斜图像

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*为什么这很重要：*  
`Image.load` 方法将文件读取到内存，并包装成 OCR 引擎能够识别的对象。它还会提取 DPI 等元数据，这会影响默认的去倾斜缩放因子。

> **Edge case:** 如果图像是多页 TIFF，需要遍历每一页或使用类似 `ocr.MultiPageImage.load` 的助手。相同的预处理设置会应用到每一页。

### 步骤 4：对预处理后的图像执行 OCR

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*为什么这很重要：*  
此时引擎会应用前面启用的去倾斜和二值化步骤，然后在清理后的位图上运行神经网络（或经典的 Tesseract‑style 流程）。返回的 `result` 对象通常包含纯文本、置信度分数，有时还会有每个单词的位置数据。

> **What if the text is still garbled?**  
检查图像分辨率：OCR 在 300 dpi 或更高时效果最佳。如果源图像低于此值，考虑在加载前进行放大，或向文档来源请求原始扫描件。

### 步骤 5：输出识别的文本

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*为什么这很重要：*  
`result.text` 是引擎能够读取的所有内容的纯字符串表示。打印它便于快速调试；在实际应用中，你可能会将其写入 `.txt` 文件、数据库，或传递给下游的 NLP 流程。

---

## Recognize Text from Scanned Document – 超越基础

基本流水线已经可用，下面探讨在实际场景中常见的几种变体，帮助你 **recognize text from scanned document** 图像。

### 1. 处理多语言

如果文档同时包含英文和法文，可在步骤 1 前配置引擎：

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

大多数 OCR 引擎接受 ISO‑639‑2 代码；加载额外语言包会带来一点开销，但在多语言页面上的准确率提升显著。

### 2. 微调二值化阈值

自动二值化适用于大多数情况，但某些老旧复印件需要自定义阈值：

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

在 120 到 220 之间尝试不同数值，直至背景消失而不抹去淡弱字符。

### 3. 提取布局信息

有时你需要的不仅是原始文本，还想知道每段落在页面上的位置。许多引擎会暴露 `result.blocks` 集合：

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

这对于重建表格或保持列顺序非常有价值。

### 4. 批量处理文件

如果文件夹中有大量已转为 JPEG 的扫描 PDF，使用循环包装整个流程：

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

循环复用同一个 `engine` 实例，比为每个文件重新创建实例更高效。

### 5. 处理低分辨率扫描

低分辨率图像（< 150 dpi）常导致字符模糊。一个快速的解决办法是使用高质量算法在送入 OCR 引擎前进行放大：

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

放大并不会凭空创造细节，但二值化步骤可以利用更锐利的边缘，从而获得适度提升。

---

## 预期输出

在一张中等倾斜、300 dpi 的扫描图上运行上述五步脚本，应该会打印类似以下内容：

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

如果出现乱码，请再次检查预处理标志、图像分辨率以及语言配置。

---

## 结论

我们已经完整覆盖了使用 Python **preprocess image for OCR** 并 **recognize text from scanned document** 文件的全部步骤。从创建全新引擎实例、启用自动去倾斜和二值化、加载倾斜图像、执行识别到打印干净文本。过程中还探讨了多语言支持、手动阈值调节、布局提取、批量处理以及低分辨率的应对方案。

尝试在自己的扫描件上运行脚本——比如一摞收据、手写表单或旧报纸剪报。熟练后，你可以进一步加入 PDF 生成或将输出送入搜索索引。可能性无限。

**准备好迎接下一个挑战了吗？** 查看我们的教程《“Extract Tables from Scanned PDFs with Python”》和《“Train Custom OCR Models with TensorFlow”》，继续扩展你的文档自动化工具箱。

祝编码愉快，愿你的 OCR 永远清晰！

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [使用 Aspose OCR 从图像提取文本 – 步骤详解指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR for .NET 优化图像 OCR](/ocr/english/net/ocr-optimization/)
- [如何使用 AspOCR：.NET 的图像 OCR 预处理过滤器](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}