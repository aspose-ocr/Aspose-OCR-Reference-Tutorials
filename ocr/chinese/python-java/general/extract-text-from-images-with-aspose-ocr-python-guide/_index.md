---
category: general
date: 2026-03-18
description: 学习如何使用 Aspose OCR 在 Python 中从图像中提取文本，并将扫描图像的文字转换为可编辑的字符串。附带逐步代码示例。
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: zh
og_description: 使用 Aspose OCR 在 Python 中提取图像文本。本教程演示如何仅用几行代码将扫描图像的文字转换。
og_title: 使用 Aspose OCR 从图像提取文本 – Python 指南
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – Python 指南
url: /zh/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 提取图像文本 – Python 指南

是否曾需要**从图像中提取文本**却不知从何入手？你并不孤单——开发者经常要把扫描的 PDF、噪声较大的截图或拍摄的收据转换为可搜索、可编辑的字符串。

好消息是？使用 Aspose OCR for Python，你可以**批量转换扫描图像文本**，且全程不离开 IDE。在本教程中，我们将通过一个完整、可直接运行的示例，逐步演示如何实现、每一步的意义以及需要注意的要点。

## 你将学到

- 在 Python 环境中配置 Aspose OCR 库。  
- 准备一组图像文件列表（PNG、JPG、TIFF 等）。  
- 使用单个方法调用进行批量 OCR。  
- 获取并显示每个文件的提取文本。  
- 处理常见的陷阱，如不支持的格式和大文件内存占用。  

完成后，你将拥有一个可按需**从图像中提取文本**的可复用脚本——非常适合自动化数据录入、文档索引或为下游 NLP 流水线提供输入。

---

![Extract text from images example](/images/ocr-extract-text.png "extract text from images")

*图片替代文字：“使用 Aspose OCR 在 Python 中提取图像文本”*

## 前置条件

- Python 3.8 或更高（代码使用 f‑strings）。  
- 有效的 Aspose OCR for Python 许可证或免费试用密钥。  
- 本地存放的待处理图像（任意组合的 PNG、JPG 或 TIFF）。  

如果已经有虚拟环境，太好了——如果没有，请使用以下命令创建一个：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

现在可以安装 SDK 了。

## 第一步：安装 Aspose OCR SDK

Aspose 通过 PyPI 分发 OCR 引擎，只需一条 `pip` 命令即可完成：

```bash
pip install aspose-ocr
```

> **专业提示：** 固定版本号（例如 `aspose-ocr==22.12`）可以避免后期出现意外的破坏性更改。

## 第二步：导入 OCR 引擎类

你将使用的核心类是 `OcrEngine`。在脚本顶部导入它：

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *为什么重要：* 只导入必需的内容可以保持启动时间短，尤其是在后续将脚本嵌入更大的应用时。

## 第三步：定义要处理的图像文件

创建一个 Python 列表，包含每张待扫描图像的完整路径。将 `YOUR_DIRECTORY` 替换为实际文件夹路径。

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **边缘情况：** 如果文件数以百计，建议使用 `glob.glob('*.png')` 等方式程序化生成列表，避免手动编辑。

## 第四步：一次性对所有图像执行 OCR

Aspose OCR 提供便利的 `processMultiple` 方法，返回 `OcrResult` 对象列表——每个输入文件对应一个对象。

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *为什么使用批处理？* 单独处理每张图像会产生额外开销（初始化引擎、加载本地库）。批量调用可降低 CPU 抖动并加快整体作业速度。

### 优雅地处理错误

如果图像无法读取（文件损坏、不支持的格式），`processMultiple` 会抛出异常。将调用包装在 `try/except` 块中，以保持脚本运行：

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## 第五步：输出每个文件的提取文本

遍历结果，将每个 `OcrResult` 与其原始文件名配对。`getText()` 方法返回识别后的字符串。

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### 预期输出

在三张简单截图上运行完整脚本可能得到如下输出：

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

如果某张图像没有可识别的字符，你会看到空字符串——程序不会崩溃，你可以自行决定是否将该文件标记为手动复核。

## 进阶：微调 OCR 准确度

Aspose OCR 提供若干可选设置，供你实验：

| 设置 | 作用 | 使用时机 |
|------|------|----------|
| `ocr_engine.setLanguage('eng')` | 强制使用英文语言模型（降低误报）。 | 主要处理英文文档时。 |
| `ocr_engine.setResolution(300)` | 提升低 DPI 扫描的准确度。 | 扫描分辨率低于 200 dpi 时。 |
| `ocr_engine.setPageSegMode('single_block')` | 将整张图像视为单块文本。 | 简单收据或身份证等。 |

可以在创建 `ocr_engine` 后立即加入这些行：

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## 常见陷阱及规避方案

1. **大型 TIFF 堆栈** – 多页 TIFF 一次性加载可能占用数 GB 内存。请在喂给 `processMultiple` 前将文件拆分为单页图像。  
2. **非拉丁脚本** – 若需**从图像中提取文本**的图像包含西里尔、阿拉伯或中文字符，请相应更改语言代码（`'rus'`、`'ara'`、`'chi_sim'`）。  
3. **文件路径包含空格** – Windows 带空格的路径可能导致 `FileNotFoundError`。请使用原始字符串（`r"C:\My Folder\image.png"`）或 `os.path.abspath` 包装路径。  

提前处理这些问题，可避免后期出现难以理解的运行时错误。

---

## 完整可运行示例

下面是完整脚本，可直接复制到名为 `batch_ocr.py` 的文件中。它已包含上述所有最佳实践调整。

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

保存后，激活虚拟环境并运行：

```bash
python batch_ocr.py
```

你应该会在控制台看到提取的字符串，随后可进行进一步处理（例如保存到数据库或喂给自然语言模型）。

---

## 结论

本指南展示了如何使用 Aspose OCR for Python **从图像中提取文本**，涵盖了从安装到批量处理以及错误处理的全部步骤。脚本简洁、功能完整且易于扩展——无论是将**扫描图像文本**转换为 CSV、构建搜索索引，还是仅仅自动化数据录入，都可以轻松实现。

准备好继续深入了吗？可以将此 OCR 流水线与 PDF 合并工具结合，生成可搜索的 PDF；或将其挂接到云存储触发器，实现每次上传扫描件即刻处理。可能性无限，而你已经拥有了坚实的基础。

有问题或改进想法？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}