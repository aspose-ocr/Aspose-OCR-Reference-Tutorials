---
category: general
date: 2026-06-06
description: 使用 Python OCR 从图像 PDF 中提取文本。了解如何使用异步批量识别快速将扫描文档转换为文本。
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: zh
og_description: 使用 Python 从图像 PDF 中提取文本。本分步指南展示了如何使用异步 OCR 将扫描文档转换为文本。
og_title: 从图像 PDF 中提取文本 – Python OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 从图像 PDF 中提取文本 – Python 指南：将扫描文档转换为文本
url: /zh/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图片 PDF 中提取文本 – Python 将扫描文档转换为文本的指南

是否曾经想要 **从图片 pdf 中提取文本**，却不想花费数小时手动重新输入？在本指南中，我们将展示如何使用 Python 中的简单异步 OCR 工作流 **将扫描文档转换为文本**。

如果你曾盯着一堆扫描的 PDF，心想“一定有更快的方法”，那么你来对地方了。我们会逐行讲解代码，说明每一部分为何重要，并且覆盖一些可能遇到的边缘情况。

## 你将学到

- 如何启动 OCR 引擎并设置识别语言。  
- 将 PNG 与 PDF 混合列表喂入批量识别器的工作原理。  
- 异步运行 OCR 任务，使你的应用保持响应。  
- 拉取结果、将其与源文件配对并打印整洁的输出。  

**先决条件**：Python 3.8+、对 `asyncio` 或 `concurrent.futures` 有基本了解，以及一个提供类似 `OcrEngine` 类的 OCR 库（如 Aspose.OCR、Tesseract 包装器或自定义包装器）。无需繁重的配置——只需安装库即可开始。

![extract text from images pdf](https://example.com/placeholder.png "Screenshot of OCR output – extract text from images pdf")

## 从图片 PDF 中提取文本 – 设置 OCR 引擎

首先需要一个已为文档语言配置好的 OCR 引擎实例。本例使用法语，你可以替换为任何受支持的语言。

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**为什么重要**：提前设置语言可以显著提升准确率。引擎会使用语言特定的词典和字符模型；使用错误的语言是导致乱码的常见原因。

## 准备文件列表 – 同时包含图片和 PDF

我们的批量识别器可以处理光栅图像（`.png`、`.jpg`）和 PDF 容器。只需提供一个普通的 Python 文件路径列表。

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**提示**：保持列表为一维；引擎会在内部将每个 PDF 页面解包为图像后再进行识别。如果文件数量达数千，建议将列表分块，以避免内存峰值。

## 启动异步批量识别

我们不在主线程中阻塞，而是在后台启动 OCR 任务。该方法返回一个 `Future`，最终会持有 `OcrResult` 对象列表。

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**工作原理**：底层引擎会创建线程池（或异步任务，取决于实现），这让你可以在 OCR 进行时继续执行其他工作——比如更新 UI、获取更多文件或记录进度。

## OCR 运行时做点有用的事

常见错误是空闲等待并在紧循环中轮询 `Future`。相反，你可以执行任何不相关的工作。这里我们仅打印一行状态信息作示例。

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## 当 Future 完成后收集结果

准备好获取 OCR 输出时，使用 `concurrent.futures` 的 `as_completed`。无论是单个还是多个 Future，这种模式都适用。

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**你会看到**：每个文件路径后面跟随提取出的纯文本。对于 PDF，`result.text` 包含所有页面的合并文本。

### 预期输出（示例）

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

如果发现缺失字符，请再次确认所设置的语言与文档语言匹配，并考虑在喂入引擎前对图像进行预处理（去倾斜、提升对比度）。

## 处理边缘情况和常见陷阱

| 情况 | 处理方法 |
|-----------|------------|
| **混合语言** | 首先进行语言检测，然后为每种语言实例化单独的引擎。 |
| **超大 PDF（> 100 MB）** | 使用 `PyPDF2` 等工具将 PDF 拆分为单页文件，再分别作为条目喂入。 |
| **非拉丁文字** | 确认 OCR 库已包含所需语言包；有些库需要额外下载数据文件。 |
| **性能瓶颈** | 增大线程池规模（`engine.set_thread_pool_size(8)`）或在可用时切换到 GPU 加速后端。 |
| **低分辨率图像缺失文本** | 使用 OpenCV 预处理：`cv2.resize`、`cv2.threshold`、`cv2.medianBlur` 提高可读性。 |

## 完整可运行示例（复制粘贴即用）

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

将其保存为 `extract_text_async.py`，将 `YOUR_DIRECTORY` 替换为你的文件路径，安装 OCR 包（`pip install your-ocr-lib`），然后运行 `python extract_text_async.py`。你将看到前文示例的控制台输出。

## 后续步骤 – 超越基础提取

- **后处理**：去除多余空白、Unicode 正规化（`unicodedata.normalize`），或使用拼写检查器清理 OCR 噪声。  
- **结构化输出**：将结果导出为 CSV、JSON，或直接写入数据库，以供后续检索。  
- **并行批次**：如果文件数以百计，可启动多个 Future 并使用队列保持 CPU 高负载而不致内存耗尽。  
- **与 Web 框架集成**：将此脚本接入 Flask 或 FastAPI 接口，提供按需 OCR 即服务。

---

### TL;DR

你现在已经掌握了使用最小化的 Python 脚本 **异步运行 OCR**，从而 **将扫描文档转换为文本**，且程序保持响应。尝试调节语言设置、批量大小和预处理技巧，以获取最高的字符准确率。

有什么新想法想分享——比如手写笔记的 OCR 或基于云的服务？欢迎留言，祝编码愉快！


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧之上进一步深入。每篇资源都提供完整可运行的代码示例，并配有逐步解释，助你掌握更多 API 功能并探索在项目中的替代实现方式。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}