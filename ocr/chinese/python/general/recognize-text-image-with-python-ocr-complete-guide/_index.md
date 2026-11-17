---
category: general
date: 2026-06-28
description: 学习如何使用 Python OCR 识别文本图像，提取文本 PNG 文件，并在具备强大错误处理的情况下打印识别的文本。
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: zh
og_description: 逐步教程：使用 Python 识别文本图像，提取文本 PNG，并安全打印识别的文本。
og_title: 使用 Python OCR 识别文本图像 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 使用 Python OCR 识别文本图像 – 完全指南
url: /zh/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 识别文本图像 – 完整指南

是否曾想过在 Python 脚本中**识别文本图像**而不引入庞大的框架？你并不孤单。许多开发者需要一种快速方式来*加载图像 OCR*——无论是截图、扫描收据，还是简单的 PNG，并获取其中的文字。  

在本教程中，我们将搭建一个最小化的 OCR 引擎，附加自定义日志记录器，**加载图像 OCR**，运行**处理图像 OCR**，最后**打印识别文本**。完成后，你将拥有一个自包含的脚本，能够按需**提取文本 png**文件。

## 你将收获什么

- 一个完整可用的 Python 代码片段，能够创建 OCR 引擎、记录每一步，并优雅地处理错误。  
- 对每行代码**为何重要**的清晰解释——让你能够将代码迁移到 Tesseract、EasyOCR 或其他后端。  
- 常见陷阱（缺少字体、损坏的 PNG）及其调试方法的提示。  

### 前置条件

- 已安装 Python 3.8+  
- 一个提供 `OcrEngine` 类的 OCR 库（示例使用的是虚构但典型的 API；请替换为 `pytesseract`、`easyocr` 等）。  
- 一张你想分析的 PNG 图像，保存为 `input.png`，放在你可控的文件夹中。  

> **专业提示：** 如果使用 `pytesseract`，请先安装系统的 Tesseract 二进制（在 Linux 上 `sudo apt install tesseract-ocr`），随后执行 `pip install pytesseract pillow`。

---

## ## Recognize Text Image: Setting Up the Logger

一个好的日志记录器是任何 OCR 流水线中不被赞颂的英雄。它会告诉你*何时*引擎启动、*哪个*文件被打开、以及*为什么*可能会失败。

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*为什么这很重要：*  
日志记录器将诊断输出与 OCR 核心解耦，使其能够轻松重定向到文件、监控服务，甚至以后在 UI 中展示。  

---

## ## Load Image OCR: Feeding the Engine a PNG

在引擎能够**处理图像 OCR**之前，需要一个合适的图像对象。大多数库接受 Pillow 的 `Image` 实例。

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*关键点：*  

- **load image ocr** – `Image.from_file` 抽象了 PNG 解码的细节。  
- 保持路径可配置；硬编码会让脚本脆弱。  
- 日志调用确认图像已成功读取，这在文件缺失或损坏时非常有用。  

---

## ## Process Image OCR: Recognizing the Text

现在开始真正的重活。引擎扫描位图，应用神经网络或启发式算法，并输出 Unicode 字符串。

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*为何要用 `try/except` 包裹：*  
OCR 在低分辨率 PNG、不受支持的色彩空间或缺少语言数据时可能会崩溃。捕获 `OcrException` 让你仅在实际存在识别结果时**打印识别文本**，避免向终端用户展示晦涩的堆栈跟踪。  

---

## ## Print Recognized Text & Extract Text PNG

如果识别成功，我们会显示结果，并可选地将其写入与原 PNG 同名的 `.txt` 文件。

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*你将得到：*  

- **print recognized text** – 在终端中即时可视化反馈。  
- 一个并行的 `.txt` 文件，实际上实现了**提取文本 png**，可用于后续处理（搜索索引、数据录入等）。  

---

## ## Common Edge Cases & How to Tackle Them

| 情况 | 症状 | 解决方案 |
|-----------|---------|-----|
| PNG 仅为灰度 | OCR 返回空字符串 | 在喂入引擎前使用 `Image.convert("RGB")` 转为 RGB。 |
| 不支持的语言 | `OcrException`，代码为 `LANG_NOT_FOUND` | 安装对应语言包（例如 `tesseract‑lang‑fra` 用于法语），并设置 `ocr_engine.language = "fra"`。 |
| 图像过大（> 5 MB） | 识别缓慢或内存错误 | 在 `set_image` 前使用 `image.thumbnail((2000, 2000))` 降低分辨率。 |
| 出现意外字符 | 输出乱码 | 确认文件真的是 PNG；有些文件伪装成 PNG 实际是 JPEG。使用 `Image.verify()` 进行验证。 |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**预期的控制台输出（正常路径）：**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

如果出现问题，你会看到带有原因的明确 `[ERROR]` 行，这要归功于自定义日志记录器。

---

## ## Next Steps & Related Topics

- **extract text png** 批量处理：将脚本包装在遍历目录树的 `for` 循环中。  
- 使用 OpenCV 在喂入引擎前进行预处理（去倾斜、增强对比度），实现**process image ocr**。  
- 通过替换 `OcrEngine` 实现，切换到云 OCR 服务（Google Vision、Azure Read）——其余代码保持不变。  
- 学习如何使用 `reportlab` 将**print recognized text** 输出到 PDF，实现自动化报告生成。  

---

## Conclusion

我们刚刚演示了一种紧凑、可投入生产的方式，在 Python 中**识别文本图像**——从加载 PNG 到**打印识别文本**并保存结果。通过注入简易日志记录器、处理异常并可选持久化输出，脚本既适合快速实验，也能集成到更大的流水线中。

尝试使用自己的截图运行它，玩转图像预处理，你很快就能从任何 PNG 中提取文字。有什么问题？留言吧——祝你 OCR 愉快！  

![recognize text image example](placeholder.png)


## What Should You Learn Next?


以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}