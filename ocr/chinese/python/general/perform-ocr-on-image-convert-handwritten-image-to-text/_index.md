---
category: general
date: 2026-03-18
description: 对图像进行 OCR 并从照片中提取手写文字。了解如何将手写图像转换、从 JPG 中提取文字以及识别照片中的文字。
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: zh
og_description: 对图像执行 OCR，以从照片中提取手写文本。本教程展示如何将手写图像转换并识别 JPG 文件中的文本。
og_title: 对图像进行 OCR – 完整手写文本指南
tags:
- OCR
- Python
- Handwriting Recognition
title: 对图像进行 OCR – 将手写图像转换为文本
url: /zh/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 执行 OCR on Image – 全栈手写文本提取

是否曾经需要 **perform OCR on image** 文件，却不确定引擎能否读取凌乱的手写文字？你并不孤单。在许多真实场景的应用中——比如费用收据扫描器或记笔记工具——你会遇到需要将涂鸦照片转换为纯文本的情况。

在本指南中，我们将展示如何 **convert handwritten image** 文件、**extract text from jpg**，甚至 **recognize text from photo** 流，通过一个轻量的 Python 风格库 `ocr`。阅读完本篇，你将拥有一个可直接运行的脚本，能够从手写笔记中提取每一个单词，无论笔迹多么摇晃。

## 你需要准备的东西

- Python 3.8+（代码在任何近期解释器上均可运行）
- 假设的 `ocr` 包 – 使用 `pip install ocr-lib` 安装（请替换为你实际使用的包名）
- 一张保存为 `note.jpg`（或其他任意图片格式）的清晰手写笔记照片
- 一点好奇心——无需高级机器学习背景

就这些。无需外部服务、API 密钥，只需一个本地引擎即可 **perform OCR on image** 数据。

![perform OCR on image screenshot](example.png)

*Alt text: perform OCR on image screenshot showing code editor with OCR script.*

## 步骤实现

下面我们把整个过程拆解为若干小块。每个标题都包含关键词，方便快速浏览；每个代码块都会解释 **为什么** 要这么做，而不仅仅是 **做什么**。

### 步骤 1：安装并验证 OCR 库

在能够 **perform OCR on image** 文件之前，需要先确保库已在环境中就绪。打开终端并运行：

```bash
pip install ocr-lib
```

> **小贴士：** 如果你使用虚拟环境（强烈推荐），请先激活它。这样可以保持依赖整洁，避免版本冲突。

安装完成后，确认 Python 能够导入该包：

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

如果看到成功提示，说明已经可以 **convert handwritten image** 数据了。

### 步骤 2：创建引擎实例并选择手写模式

大多数 OCR 引擎默认识别印刷体。因为我们要 **extract handwritten text**，所以必须显式切换模式。此步骤至关重要，因为手写文字往往需要不同的预处理（例如平滑笔画）。

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*为什么重要：* 手写字符的大小和倾斜度差异极大。通过设置 `RecognitionMode.HANDWRITTEN`，引擎会使用在草写样本上训练的模型，显著提升准确率。

### 步骤 3：加载待分析的照片

现在我们真正 **perform OCR on image** 内容。`load_image` 方法接受路径或类文件对象。演示中我们加载 JPEG，但同样的调用也适用于 PNG、BMP，甚至 PDF 页面。

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

如果你的图片存放在云存储桶中，只需先下载或传入 `BytesIO` 流——`ocr` 足够灵活，能够同时处理这两种情况。

### 步骤 4：运行识别过程

引擎准备就绪、图像已加载到内存后，终于可以 **perform OCR on image** 并获取原始文本。

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

`recognize()` 调用返回一个普通的 Unicode 字符串。大多数场景下，你可以直接写入 `.txt` 文件、喂入自然语言处理管道，或在 GUI 中显示。

### 步骤 5：可选 – 清理或后处理输出

手写 OCR 并非完美；常会出现多余的换行或误读字符。快速的清理步骤可以提升后续结果的质量。

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

根据业务需求，你可以接入拼写检查器、语言模型或自定义正则表达式。

### 完整脚本 – 复制粘贴即用

将上述所有步骤整合，下面是完整可运行的程序，它 **extracts handwritten text** 自 JPEG 并打印整洁结果。

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**预期输出**（实际文本当然会不同）：

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

如果出现乱码，请检查图像质量（光线充足、模糊最小）并确保已切换到 `HANDWRITTEN` 模式。这两个因素是导致大多数识别错误的根源。

## 常见问题 (FAQ)

| Question | Answer |
|----------|--------|
| **Can I use this to extract text from a PNG?** | Absolutely. `engine.load_image("scan.png")` works the same way. |
| **What if my image is a PDF page?** | Convert the page to an image first (e.g., with `pdf2image`) then feed it to the engine. |
| **Is the library thread‑safe?** | Yes, you can instantiate separate `OcrEngine` objects per thread. |
| **How does this differ from `pytesseract`?** | `ocr` abstracts away the Tesseract binary and includes a built‑in handwritten model, so you don’t need to install external executables. |
| **What if I need to **extract text from JPG** files in bulk?** | Wrap the script in a loop, or use `engine.load_image` on each file and collect results in a list or CSV. |

## 边缘情况与最佳实践

1. **低对比度照片** – 在加载前编程提升对比度，或使用 `engine.apply_preprocessing('contrast', level=2)`。
2. **印刷体与手写体混合** – 进行两轮识别：先用 `HANDWRITTEN`，再用 `PRINTED`，最后合并输出。
3. **大尺寸图像** – 将宽度下采样至约 1500 px；OCR 引擎在较小的缓冲区下通常更快且不损失精度。
4. **Unicode 字符** – 库返回 UTF‑8 字符串，能够直接处理表情符、重音字母或数学符号。

## 小结

我们已经完整演示了如何 **perform OCR on image** 文件，特别是针对手写笔记。通过安装 `ocr` 包、将引擎配置为 `HANDWRITTEN` 模式、加载照片并调用 `recognize()`，你可以 **convert handwritten image** 数据为干净、可搜索的文本。

接下来，你可以 **extract text from jpg** 文件批量处理、将输出导入记笔记应用，或结合语音合成提升可访问性。上面的代码为你提供了坚实的实验基础。

有什么新思路想分享——比如不同的文件格式或奇特的预处理技巧？欢迎留言，让我们一起讨论。祝编码愉快，享受把涂鸦变成数字金矿的过程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}