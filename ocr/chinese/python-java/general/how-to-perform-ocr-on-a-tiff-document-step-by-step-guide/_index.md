---
category: general
date: 2026-01-12
description: 如何快速、准确地执行 OCR。学习在文档上运行 OCR，从 TIFF 中提取文本，加载图像进行 OCR，并在 Python 中设置 OCR
  语言。
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: zh
og_description: 如何在 Python 中执行 OCR。本教程向您展示如何对文档进行 OCR、从 TIFF 中提取文本、加载图像进行 OCR 并设置
  OCR 语言。
og_title: 如何对 TIFF 文档进行 OCR – 完整指南
tags:
- OCR
- Python
- Image Processing
title: 如何对 TIFF 文档进行 OCR – 步骤指南
url: /zh/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何对 TIFF 文档执行 OCR – 完整指南

是否曾想过 **如何对** 扫描的 TIFF 文件 **执行 OCR**，却不想花费数小时寻找合适的库？你并不孤单。许多开发者在需要从 tiff 图像中提取文本时会遇到瓶颈，尤其是当性能和语言设置变得重要时。

在本教程中，我们将逐步讲解你需要了解的一切：从安装 OCR 包、加载图像进行 OCR、设置 OCR 语言，到最终 **对文档运行 OCR** 并提取干净的文本。完成后，你将拥有一个可直接在任何项目中使用的脚本。

> **专业提示：** 虽然示例使用了通用的 `ocr` 模块，但相同的概念同样适用于 Tesseract、EasyOCR 或任何提供 Python API 的现代 OCR 引擎。

---

## 你需要的准备

- Python 3.8+（任意近期版本均可）
- 提供 `OcrEngine` 类的 OCR 库（示例使用虚构的 `ocr` 包；请替换为你实际使用的库）
- 需要处理的多页 TIFF 文件（我们称之为 `big_document.tif`）
- 如果计划设置线程数，机器至少需要 4 个 CPU 核心

无需外部服务，无需云密钥——只需本地代码，几秒钟即可运行。

---

![how to perform ocr example](/images/ocr-example.png "how to perform OCR on a TIFF document")
*图片替代文字：对 TIFF 文档执行 OCR 示例 – 提取文本的预览。*

---

## 第一步：安装并导入 OCR 库

首先要做的事：把库装到你的机器上。大多数 OCR 包都在 PyPI 上，可通过简单的 `pip install` 完成。

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

现在导入所需的类。如果使用 Tesseract，导入语句会有所不同，但其余代码保持不变。

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*为什么重要：* 及早导入正确的符号可以防止后续的命名空间冲突，并让脚本更易阅读。

---

## 第二步：创建并配置 OCR 引擎（设置 OCR 语言）

配置引擎的过程就是 **设置 OCR 语言**，以获得准确的识别。默认是英语，你可以通过一行代码切换到法语、德语，甚至多语言模式。

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **为什么使用 4 线程？** 大多数现代笔记本至少有四个核心，限制线程数可以防止 OCR 进程占用整台机器的资源——在共享服务器上运行脚本时尤为有用。

如果需要其他语言，只需将 `ocr.Language.ENGLISH` 替换为 `ocr.Language.FRENCH`、`ocr.Language.SPANISH` 等。

---

## 第三步：加载图像进行 OCR（Load Image for OCR）

现在我们 **加载图像进行 OCR**。`Image.load` 方法会将 TIFF 文件读取到内存中，并自动处理多页文档。

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*边缘情况：* 如果文件非常大，可能会耗尽内存。在这种情况下，考虑使用 `Image.load_page(page_number)`（如果库支持）一次加载一页。

---

## 第四步：对文档运行 OCR

引擎准备就绪、图像已加载，是时候 **对文档运行 OCR** 了。`process` 方法负责繁重的工作并返回一个结果对象。

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

在内部，引擎会将图像拆分为文本块，运行识别模型，然后将结果拼接。此调用是阻塞的，意味着脚本会等待整个 TIFF 处理完成——非常适合批处理任务。

---

## 第五步：从 TIFF 中提取文本并验证输出

最后，我们通过访问结果的 `text` 属性 **从 tiff 中提取文本**。让我们打印前 200 个字符，以快速进行 sanity check。

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**预期输出（示例）：**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

如果需要完整文本，只需使用 `ocr_result.text`。若要进行后续处理，你可能想将其写入 `.txt` 文件：

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## 完整可运行示例

将所有步骤组合起来，这里是一段可直接运行的脚本。请将占位的包名替换为你实际安装的库。

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

运行脚本：

```bash
python ocr_tiff_example.py
```

你应该会在控制台看到预览输出，并生成名为 `extracted_text.txt` 的文件，里面包含完整的转录内容。

---

## 常见问题与边缘情况

- **如果 TIFF 包含多页怎么办？**  
  大多数 OCR 引擎会在内部将每页视为单独的图像。`ocr_result.text` 会在页面之间插入换行符。如果需要逐页处理，可使用 `Image.load_page(page_number)` 进行迭代。

- **可以处理 PNG 或 JPEG 而不是 TIFF 吗？**  
  完全可以。`Image.load` 方法通常接受 Pillow 或底层库支持的任何格式。只需更改文件扩展名即可。

- **我的文本出现乱码——是否需要更改语言？**  
  是的。**设置 OCR 语言** 步骤对非英文文档至关重要。确保已安装相应语言包（例如法语的 `tesseract‑lang‑fra`）。

- **内存不足怎么办？**  
  降低 `set_memory_limit` 或逐页处理。一些引擎还允许在识别前对图像进行降采样。

---

## 结论

以上就是使用 Python 对 TIFF 文件 **执行 OCR** 的简明完整指南。我们涵盖了从安装库、配置引擎（包括 **设置 OCR 语言**）、**加载图像进行 OCR**、**对文档运行 OCR**，到最后 **从 tiff 中提取文本** 的全部步骤。

欢迎尝试：调整线程数、切换语言，或将 OCR 输出喂入自然语言处理流水线。掌握基础后，想象力就是唯一的限制。

还有其他问题吗？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}