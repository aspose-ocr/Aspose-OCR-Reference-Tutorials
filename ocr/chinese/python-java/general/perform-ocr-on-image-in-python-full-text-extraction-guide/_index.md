---
category: general
date: 2026-06-19
description: 使用 Python 的 OCR 库对图像进行 OCR。学习如何从图像中检测文本、从 JPEG 中识别文本，以及高效地从扫描图像中提取文本。
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: zh
og_description: 使用 Python 对图像进行 OCR 并从扫描文件中提取文本。本指南将一步步带您完成图像加载、去倾斜和文本识别。
og_title: 在 Python 中对图像进行 OCR – 完整文本提取指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 在 Python 中对图像进行 OCR – 完整文本提取指南
url: /zh/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中对图像执行 OCR – 完整文本提取指南

是否曾经需要**对图像执行 OCR**但因为代码晦涩而卡住？你并不是唯一遇到这种情况的人。无论是将一堆扫描的收据转换为可搜索的 PDF，还是从 JPEG 中提取标题用于数据科学项目，能够识别 JPEG 等格式中的文本是当今每个开发者必备的技能。

在本教程中，我们将逐步演示一个完整且可运行的示例，展示如何**从图像中检测文本**文件、**从扫描图像中提取文本**文档，甚至**加载图像进行 OCR**，仅需几行代码。完成后，你将拥有一个可靠的、可直接用于生产环境的代码片段，能够直接嵌入自己的项目——无需缺失的导入，也不需要模糊的“查看文档”快捷方式。

## 你将构建的内容

- 一个小型的 Python 脚本，用于创建 OCR 引擎、启用自动去倾斜、加载 JPEG（或任何受支持的格式），并打印识别的文本。
- 解释每个设置**为何**重要，而不仅仅是**如何**编写。
- 提供处理多页 PDF、非英文语言以及常见问题（如模糊扫描）的技巧。

### 前置条件

- 已安装 Python 3.8+（示例使用通过 `pip install ocr-lib` 获得的 `ocr` 包——请替换为实际使用的库名）。
- 对 Python 函数和虚拟环境有基本了解。
- 一张你想要处理的图像文件（JPEG、PNG、TIFF），我们将使用 `skewed_page.jpg` 作为占位符。

> **专业提示：**如果你使用 Windows，在安装 OCR 库时请以管理员身份运行终端，以避免权限问题。

---

## 对图像执行 OCR – 设置与配置

首先，你需要一个干净的 OCR 引擎实例。可以把它看作操作背后的“大脑”；如果配置不当，即使是最清晰的图像也会返回乱码。

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**为什么这很重要：**  
设置 `engine.language` 可以限定 OCR 引擎预期的字符集，显著提升准确率。如果省略此设置，引擎会自行猜测，常常误读简单词汇。

---

## 启用自动去倾斜 – 修正倾斜扫描

扫描的页面很少是完全平整的。轻微的倾斜会导致字符分割错误，把 “Hello” 变成 “H3llo”。`auto_deskew` 标志会为你完成这项繁重的工作。

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**边缘情况：**如果你确信图像已经是正的，禁用去倾斜可以节省几毫秒的处理时间——在批量处理数千页时非常有用。

---

## 加载图像进行 OCR – 支持 JPEG、PNG、TIFF

现在我们真正**加载图像进行 OCR**。`ocr.Image.load` 方法非常灵活；它接受任意受支持的栅格格式的路径。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **为什么此步骤至关重要：**库会将文件读取为内部位图，并进行必要的颜色空间转换。如果跳过此步骤直接传入原始字节流，会抛出 `FileNotFoundError`，甚至更糟，悄悄产生空结果。

如果你需要专门**从 JPEG 文件中识别文本**，只需确保文件扩展名为 `.jpeg` 或 `.jpg`。同样的调用对 PNG（`.png`）或 TIFF（`.tif`）同样适用，无需修改。

---

## 对图像执行 OCR – 运行引擎

引擎已准备好且图像已加载到内存，现在是**对图像执行 OCR**的时刻。这一行代码完成了繁重的工作：预处理、分割、分类以及文本组装。

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**内部发生了什么？**  
- 引擎应用去倾斜变换（如果已启用）。  
- 它运行神经网络或 Tesseract 后端来识别字符。  
- 最后，它将字符拼接成单词和行，返回一个丰富的 `result` 对象。

---

## 从扫描图像中提取文本 – 输出结果

最后一步是**从扫描图像中提取文本**并显示。`result.text` 属性包含纯文本表示。

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

典型的输出如下：

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

如果 OCR 引擎未能找到任何字符，`result.text` 将为空字符串。此时，请再次检查图像质量，或考虑调整 `engine.confidence_threshold` 属性（如果你的库支持）。

---

## 处理常见变体

### 从 JPEG 与 PNG 识别文本

两种格式均受支持，但 JPEG 压缩可能产生干扰引擎的伪影。如果你发现频繁误识别，尝试先将 JPEG 转为 PNG：

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### 检测多语言图像文本

如果文档中混合了英语和西班牙语，请设置多语言模式：

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

引擎将在识别时同时考虑这两套字母表。

### 从扫描的 PDF 中提取文本

对于 PDF，需要先将每页栅格化为图像。`pdf2image` 等库可以轻松完成此操作：

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## 完整可运行示例

下面是完整的脚本，你可以复制粘贴到 `ocr_demo.py` 文件中。它包括错误处理以及一个用于测量执行时间的小助手。

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**预期输出**（假设扫描清晰）：

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## 常见问题

**Q: 我可以在无头服务器上运行吗？**  
A: 当然可以。该库无需 GUI 即可工作，只需确保服务器上已安装必要的本地二进制文件（例如 Tesseract）。

**Q: 如果图像模糊怎么办？**  
A: 可以在 `engine.recognize` 之前添加锐化滤镜。许多 OCR 库提供 `image_preprocessing.sharpen = True`，或者你可以使用 OpenCV 的 `cv2.GaussianBlur` 的逆操作。

**Q: 脚本支持批量处理吗？**  
A: 支持。将 `perform_ocr` 包裹在遍历文件路径列表的循环中，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}