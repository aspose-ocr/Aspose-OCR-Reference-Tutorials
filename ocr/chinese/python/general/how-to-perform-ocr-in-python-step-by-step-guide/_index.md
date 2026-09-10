---
category: general
date: 2026-01-12
description: 如何快速执行 OCR 并将图像转换为文本。学习识别特殊字符、从图像中提取文本，并使用完整的 Python 示例加载图像进行 OCR。
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: zh
og_description: 如何在 Python 中进行 OCR，将图像转换为文本，并识别特殊字符。请遵循本实用指南，从图像中提取文本。
og_title: 如何在 Python 中进行 OCR – 完整教程
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中进行 OCR – 步骤指南
url: /zh/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中执行 OCR – 步骤指南

是否曾需要对包含拉丁字符和西里尔字符的截图**执行 OCR**？你并不孤单。在许多项目中——无论是数字化收据、索引多语言文档，还是构建可搜索的档案——**如何执行 OCR**很快就会成为最关键的问题。

在本教程中，我们将通过一个完整、可运行的示例，展示如何**将图像转换为文本**、**识别特殊字符**，以及使用一个简单的 Python 库**从图像中提取文本**。完成后，你将拥有一个可直接运行的脚本，能够加载图像进行 OCR，处理多语言内容，并打印结果。

## 你需要的准备

在开始之前，请确保具备以下前置条件：

- 已在机器上安装 Python 3.8+。  
- 通过 `pip install ocr` 安装 `ocr` 包（或任何兼容的 OCR 库）。  
- 一张包含拉丁和西里尔字形的图像文件（`multilingual.png`）。  
- 一个基本的文本编辑器或 IDE——VS Code、PyCharm，甚至是记事本都可以。  

如果没有 `ocr` 包，你可以改用 `pytesseract`，只需做少量修改；核心概念保持不变。

## 步骤 1：安装并导入 OCR 库

首先，让我们准备好 OCR 引擎。我们将导入库，创建引擎实例，并为多语言支持进行配置。

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**为什么重要：**  
创建引擎是基础——没有它，后续就无法**加载图像进行 OCR**。启用语言包可确保引擎正确识别诸如 “Ŀ”、 “Ҕ”、 “Ǣ” 等字符。如果跳过此步骤，非拉丁脚本的输出将会乱码。

## 步骤 2：加载包含多语言文本的图像

现在我们将引擎指向要处理的文件。路径可以是绝对或相对的，只要确保指向可读取的图像即可。

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![如何执行 OCR 示例](/images/ocr-example.png "在多语言图像上执行 OCR 的方法")

**为什么重要：**  
`load_image` 调用会将像素数据读取到内存，为 OCR 算法做好准备。如果图像较大，引擎可能会自动降采样；你可以稍后使用 `engine.set_max_resolution(3000)` 对高分辨率扫描进行微调。

## 步骤 3：运行识别过程

引擎准备就绪且图像已加载后，我们终于可以提取文本内容了。

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**为什么重要：**  
`recognize()` 在后台运行强大的神经网络。它返回一个对象，包含原始文本、置信度分数，甚至在需要时提供边界框，以便进行可视化调试。

## 步骤 4：输出识别的文本

看看引擎找到了什么。我们将文本打印到控制台，你也可以将其写入文件或数据库。

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### 预期输出

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

如果看到类似的结果，恭喜你——已经成功**将图像转换为文本**并**识别特殊字符**。

## 处理常见问题

即使脚本很简洁，你仍可能遇到一些小障碍。以下是我个人经验中的实用技巧。

### 1. 缺少语言包

如果出现问号 (`?`) 而不是西里尔字母，请再次确认已安装语言包。对于许多 OCR 引擎，需要下载相应的 `.traineddata` 文件并放置在引擎的 `tessdata` 文件夹中。

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. 图像质量低

模糊或低对比度的图像会导致低置信度分数。可以使用 OpenCV 进行预处理：

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. 大文件与内存占用

处理 10 MB 的照片可能会导致内存激增。使用 `engine.set_max_image_size(2000)` 限制分辨率，或将图像切分为多个瓦片分别 OCR。

### 4. 捕获边界框

如果需要高亮每个单词出现的位置（对 UI 覆盖层很有用），访问 `result.boxes`：

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## 完整脚本 – 一键执行

将所有内容整合在一起，下面是一个可以直接运行的文件 `python ocr_demo.py`。它包含错误处理、可选的预处理步骤以及清晰的注释。

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

运行方式：

```bash
python ocr_demo.py path/to/multilingual.png
```

你应该会看到前面展示的相同输出，确认已经成功**从图像中提取文本**。

## 结论

我们已经从头到尾覆盖了在 Python 中**如何执行 OCR**：安装库、加载图像、识别多语言内容，以及处理最常见的边缘情况。通过本指南，你现在可以在自己的项目中**将图像转换为文本**、**识别特殊字符**并**从图像中提取文本**——不再需要手动转录。

接下来可以尝试：

- 添加更多语言包（例如 `spa` 用于西班牙语）。  
- 将结果导出为 JSON，以便下游处理。  
- 将 OCR 步骤集成到 Flask API 中，让其他服务调用。  

如果遇到任何奇怪的问题，大多数 OCR 库都有活跃的社区——搜索 “ocr library language pack installation” 或在下方留言。祝编码愉快，享受将图片转化为可搜索文本的乐趣！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}