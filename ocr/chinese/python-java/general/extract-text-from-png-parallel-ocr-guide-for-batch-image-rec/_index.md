---
category: general
date: 2026-03-18
description: 使用 Python 和 Aspose OCR 从 PNG 中提取文本。了解如何加载图像进行 OCR，批量处理多个文件，并通过并行图像识别实现批量
  OCR 图像。
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: zh
og_description: 使用 Aspose OCR 在 Python 中从 PNG 提取文本。本教程展示了如何加载图像进行 OCR、处理多个文件的 OCR，以及使用并行图像识别批量运行
  OCR 图像。
og_title: 从 PNG 中提取文本 – 并行 OCR 指南
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: 从 PNG 中提取文本 – 批量图像识别的并行 OCR 指南
url: /zh/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 中提取文本 – 批量图像识别的并行 OCR 指南

是否曾需要**从 PNG 中提取文本**但在单张图片处理时间过长时卡住了？你并不孤单。在许多真实项目中——比如发票扫描仪、收据数字化或档案工具——速度至关重要，逐个处理 PNG 根本不可行。  

在本指南中，我们将逐步演示一个完整、可直接运行的解决方案，它**加载图像进行 OCR**，以**批量 OCR 图像**的方式运行**ocr multiple files**，并利用 Python 的 `threading` 模块实现**并行图像识别**。完成后，你将拥有一个脚本，能够在秒级而非分钟级从任意数量的 PNG 中提取文本。

## 你需要的条件

- Python 3.8 或更高版本（示例语法在 3.10+ 亦可运行）。  
- Aspose OCR for Java/​Python 包（`aspose-ocr`）。可通过 `pip` 安装。  
- 一个包含若干 PNG 文件的文件夹，供你处理。  
- 适量的内存——每个线程持有一个小型 OCR 引擎实例，即使是笔记本电脑也能启动数十个工作线程。

无需外部服务、无需云密钥，也不需要神秘的配置文件。只需纯 Python 代码，复制粘贴即可运行。

## 为什么要并行提取 PNG 文本？

处理 PNG 属于 CPU 密集型任务：OCR 引擎会运行一系列图像分析算法，对像素数据进行处理。当你有十张、二十张甚至上百张图片时，总运行时间基本等于每张图片单独运行时间的累加。

通过为每个文件生成一个线程，我们让操作系统能够并发调度这些 CPU 密集型任务。在多核机器上，这通常能将实际耗时减半——甚至减至四分之一。代价是略高的内存占用，但对大多数批处理任务而言，速度提升是值得的。

> **Pro tip:** 如果要处理数百兆字节的图像，考虑使用 `concurrent.futures.ProcessPoolExecutor` 替代 `threading`。进程能够在受 GIL 限制的 CPython 解释器上实现真正的并行，只是会带来稍多的开销。

## 第一步：安装 Aspose OCR for Python

首先，让我们把 OCR 库装到系统中。

```bash
pip install aspose-ocr
```

这行命令会拉取最新的 Aspose OCR 二进制文件及其 Python 绑定。如果出现权限错误，请尝试添加 `--user` 或使用虚拟环境。

## 第二步：加载图像进行 OCR – 工作函数

现在我们定义将在每个线程中执行的核心例程。它**加载图像进行 OCR**，执行识别，并打印提取文本的预览。

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

需要注意的几点：

- **为什么每个线程都要新建 `OcrEngine`？** 引擎内部持有缓冲区，共享同一个实例会导致竞争条件和乱码。  
- **为什么要去除换行符？** 在控制台日志中这样可以保持行的整洁。  
- **错误处理？** 在生产环境中，你应当将函数体包裹在 `try/except` 中，并可能将错误记录到文件——我们稍后会介绍。

## 第三步：列出要处理的 PNG 文件

你可以硬编码文件列表，但更灵活的做法是扫描目录。下面手动列出三个文件以示例说明；请将路径替换为你自己的文件夹。

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

如果更倾向于自动发现：

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

这个小改动让你能够**批量提取 PNG 文本**，而无需每次都修改源码。

## 第四步：设置 ocr multiple files 与 batch OCR images

我们现在为每张图片创建一个线程。这就是 **batch OCR images** 模式的核心。

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

列表推导式让代码保持简洁，每个 `Thread` 对象保存目标函数及其参数（`image_path`）。  

> **Side note:** Python 的 `threading` 模块使用原生 OS 线程，所以在一台四核笔记本上通常最多会有四个线程真正同时运行；其余线程会在核心空闲时被调度。

## 第五步：运行并行图像识别

启动工作线程非常直接：遍历列表并调用 `start()`。随后使用 `join()` 等待所有线程结束。

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

脚本执行完毕后，你会看到类似以下的输出行：

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

这些输出确认每个 PNG 已被处理，提取的文本可供后续使用（例如保存到数据库或喂入 NLP 流水线）。

## 第六步：验证结果并处理边缘情况

### 检查空结果

有时图像噪声过大，或 OCR 引擎未能检测到任何字符。快速的有效性检查可以避免下游错误。

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### 限制并发线程数量

如果在资源有限的 VM 上运行，生成上百个线程可能会压垮调度器。可以使用信号量来限制并发数：

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### 将结果保存到文件

除了打印，你可能希望生成一个 CSV，记录文件名和提取的文本：

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

务必在工作函数外部**一次性**打开 CSV，以避免竞争条件；`csv` 模块的 writer 对简单写入是线程安全的。

## 完整工作示例

将所有内容组合在一起，下面是一个可以保存为 `batch_ocr.py` 并直接运行的脚本：

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}