---
category: general
date: 2026-06-25
description: 如何使用 Aspose OCR Python 执行 OCR——学习在几分钟内加载图像 OCR、处理图像 OCR 并提取 JSON 结果。
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: zh
og_description: 如何使用 Aspose OCR Python 执行 OCR。按照本指南轻松加载图像 OCR、处理图像 OCR 并解析 JSON 输出。
og_title: 如何使用 Aspose OCR Python 执行 OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: 如何使用 Aspose OCR Python 进行 OCR
url: /zh/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR Python 执行 OCR

是否曾想过 **如何使用 Python 对收据、发票或任何扫描文档进行 OCR**？你并不孤单。在许多实际项目中，从图像中提取文本是实现自动化、分析或归档的第一步。

好消息是？使用 **Aspose OCR Python**，只需几行代码即可加载图像 OCR、处理图像 OCR，并获得整洁的 JSON 负载。下面你将看到一个完整、可直接运行的脚本，以及每一步背后的原理，让你真正理解代码为何如此编写。

## 本教程涵盖内容

- 在 Python 中设置 Aspose OCR 引擎  
- 正确 **加载图像 OCR**，处理常见格式如 TIFF、PNG 和 JPEG  
- **处理图像 OCR** 并将结果转换为 JSON  
- 解析 JSON 以获取有用信息（单词、置信度分数等）  
- 故障排查技巧、边缘情况处理以及后续思路  

无需事先了解 Aspose；只需一个可用的 Python 3 环境和一张想要读取的图像文件。

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| Python 3.8+ | Aspose OCR 的 wheel 包针对现代解释器 |
| `aspose-ocr` 包（`pip install aspose-ocr`） | 执行核心 OCR 功能的库 |
| 示例图像（例如 `receipt.tif`） | 需要提供给引擎的输入 |
| 基础 `json` 知识 | 我们将把 OCR 输出解析为 Python dict |

> **专业提示：** 如果你使用 Windows，安装包时请以管理员身份运行命令提示符，以避免权限问题。

---

## 如何使用 Aspose OCR Python 执行 OCR

下面是可以直接复制到名为 `ocr_demo.py` 的文件中的 **完整脚本**。它包含了从导入到最终输出的所有内容，直接运行即可。

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### 预期输出

运行 `python ocr_demo.py`（前提是图像存在且可读取）后，你应该会看到类似如下的输出：

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

具体内容会随源图像而异，但出现 `"words"` 数组即表明 **处理图像 OCR** 已成功。

---

## 加载图像 OCR – 提示与常见陷阱

1. **文件格式很重要** – TIFF 适合扫描文档，PNG 更适合截图，JPEG 适合照片。  
2. **分辨率** – Aspose OCR 在 300 dpi 或更高时表现最佳。如果看到低置信度分数，考虑在加载前对图像进行上采样。  
3. **多页文件** – 如果你的 TIFF 包含多页，`image = ocr.Image.load(path)` 会返回一个堆栈；可以使用 `for page in image.pages:` 并对每页调用 `engine.recognize(page)`。

> **为什么这一步至关重要：** 正确加载图像可确保 OCR 引擎收到干净的像素数据。损坏或不受支持的格式会导致 `engine.recognize` 抛出异常，进而中断整个流水线。

---

## 处理图像 OCR – 高级选项

Aspose OCR 在 `OcrEngine` 对象上公开了多个属性：

| 属性 | 用例 |
|------|------|
| `engine.language = ocr.Language.English` | 当图像包含混合脚本时强制使用英文 |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | 更快但精度略低；适用于快速预览 |
| `engine.auto_rotate = True` | 自动校正旋转页面（对收据特别有用） |

你可以在第 3 步之前设置这些属性，以微调 **处理图像 OCR** 阶段。例如：

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## 理解 Aspose OCR Python 输出

JSON 负载遵循可预测的结构：

- **pages** – 页面对象列表，每个对象包含尺寸和旋转信息。  
- **lines** – 共享同一基线的单词组，便于重建段落。  
- **words** – 单个单词对象，包含 `text`、`confidence`，以及带坐标的 `rectangle`。  
- **language** – 检测到的语言代码（例如 "en"）。  
- **confidence** – 整个文档的整体置信度。

了解此结构后，你就可以精准提取所需信息。例如，要获取所有置信度 < 0.9 的单词（可能的 OCR 错误），可以添加：

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## 边缘情况及处理方式

| 情况 | 建议处理方式 |
|------|--------------|
| **结果为空**（没有单词） | 检查图像质量，确保语言设置正确，必要时提升 DPI。 |
| **多页 PDF** | 先将 PDF 页面转换为图像（如使用 `pdf2image`），再将每页喂入 OCR 引擎。 |
| **非拉丁脚本** | 通过 `engine.add_language(ocr.Language.ChineseSimplified)` 安装额外语言包。 |
| **大文件** | 分块处理；复用同一 `OcrEngine` 实例以避免过度内存分配。 |

---

## 完整工作示例（所有步骤合并）

下面是一个紧凑版，可直接放入 Jupyter Notebook 或脚本中。它包含错误处理、可选设置，并打印整洁的摘要。

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

运行后会得到与前面相同的简洁输出，

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在此基础上进一步掌握 API 功能并探索替代实现方式：

- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何在图像识别中使用 Aspose OCR 获取 JSON 结果](/ocr/english/net/text-recognition/get-result-as-json/)
- [如何使用 Aspose OCR 从流中进行图像文本提取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}