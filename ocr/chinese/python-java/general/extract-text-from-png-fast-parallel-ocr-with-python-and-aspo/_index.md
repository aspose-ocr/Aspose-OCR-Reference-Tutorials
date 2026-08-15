---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Python 中快速提取 PNG 文本。学习使用并行图像识别的 Python 将扫描页的文字转换，以实现高性能结果。
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: zh
og_description: 使用 Aspose OCR 在 Python 中快速提取 PNG 文本。本指南展示了如何通过并行图像识别将扫描页的文本转换为 Python，实现高速结果。
og_title: 从 PNG 中提取文本 – 使用 Python 的快速并行 OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: 从 PNG 中提取文本 – 使用 Python 和 Aspose 的快速并行 OCR
url: /zh/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 中提取文本 – 使用 Python 的快速并行 OCR

是否曾经需要**从 PNG 文件中提取文本**，但发现单线程 OCR 速度极慢？你并不孤单。无论是将一堆扫描收据数字化，还是将讲义幻灯片转换为可搜索的 PDF，瓶颈通常都是 OCR 步骤本身。

在本教程中，我们将展示一个完整、可直接运行的解决方案，使用 Aspose OCR 的异步批处理模式结合 Python 的 `ThreadPoolExecutor`，并行**转换扫描页面文本**。完成后，你将能够以 **recognize image text python** 风格识别图像文本，在处理数十张图片时所需时间仅为普通循环的几分之一。

> **你将收获**  
> * 一个能够并发提取 PNG 图像文本的完整脚本。  
> * 对异步批处理模式为何加速的理解。  
> * 扩展解决方案以处理更大工作负载的技巧。

## 所需条件

| 前置条件 | 原因 |
|--------------|--------|
| Python 3.9+ | 现代语法和类型提示。 |
| `aspose-ocr` and `aspose-storage` packages | 提供 OCR 引擎和图像加载器。 |
| PNG 文件夹（例如扫描页面） | 你想要处理的源材料。 |
| Python 并发的基础知识 | 有帮助但非必需；我们会解释全部内容。 |

你可以使用以下方式安装 Aspose 库：

```bash
pip install aspose-ocr aspose-storage
```

> **专业提示：** 保持你的包是最新的（`pip list --outdated`），以受益于最新的性能改进。

## 步骤 1：在异步批处理模式下初始化 Aspose OCR 引擎

我们首先创建一个 `OcrEngine` 实例并将其切换到**异步批处理模式**。该模式在内部排队识别请求，使引擎能够处理多张图像而不会阻塞你的 Python 线程。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*为什么使用异步？*  
当你在同步模式下调用 `recognize` 时，调用会阻塞，直到图像完全处理完毕。使用异步模式时，引擎可以在当前图像仍在解码时就开始处理下一张图像，从而实现 I/O 与 CPU 工作的重叠。

## 步骤 2：列出要处理的 PNG 文件

这里我们定义图像集合。在实际项目中，你可能会动态生成此列表（例如 `glob.glob("*.png")`），但显式列出可以让示例更易于理解。

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **注意：** 将 `YOUR_DIRECTORY` 替换为 PNG 扫描文件实际所在的路径。如果有数百个文件，考虑使用 `os.listdir` 并过滤 `.png`。

## 步骤 3：编写一个加载图像并返回其文本的辅助函数

该辅助函数抽象了通过 **Aspose Storage** 加载文件并将其传递给 OCR 引擎的两步过程。添加一个简短的文档字符串使函数自我说明——有助于未来的维护。

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*为什么要单独的函数？*  
它保持线程池代码简洁，并且可以在其他地方（例如 Flask 接口）复用该逻辑。此外，隔离 I/O 使调试更容易——如果某个文件失败，你将在异常跟踪中看到文件名。

## 步骤 4：使用线程池运行并行图像识别 Python

现在我们引入 `ThreadPoolExecutor`。默认情况下我们启动四个工作线程，但你可以根据 CPU 核心数和图像集合的大小调节 `max_workers`。

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### 这如何实现并行图像识别 Python

* **ThreadPoolExecutor** 创建一个工作线程池，每个线程调用 `recognize_image`。  
* 由于 OCR 引擎处于异步批处理模式，每个线程可以在保持响应的同时将工作交给引擎。  
* `as_completed` 按完成顺序返回 future，这样你可以在结果准备好时立即获取——非常适合流式处理大批量。

> **常见陷阱：** 将 `max_workers=1` 会抵消并行的意义。在 8 核机器上，`max_workers=8` 通常能获得最佳吞吐量，但请测试几个值以找到适合你硬件的最佳配置。

## 步骤 5：验证输出并处理边缘情况

运行脚本后，你应该会看到每个 PNG 对应的一段文本，前面带有文件名：

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

如果任何图像失败（文件损坏、不支持的格式），`except` 块会打印有用的错误信息，而不是让整个批次崩溃。

### 扩展方案

| 场景 | 建议调整 |
|----------|-----------------|
| **成千上万页** | 切换到 `ProcessPoolExecutor` 以利用多个 CPU 进程，或将列表分块并顺序处理批次。 |
| **不同的图像格式（JPG、TIFF）** | `storage.Image.load` 方法会自动检测格式，所以只需将文件加入 `input_images` 即可。 |
| **需要存储结果** | 将 `text` 写入 `.txt` 文件或在 `else` 块中插入数据库。 |
| **性能监控** | 使用计时器（`time.perf_counter`）包装 `recognize_image` 并记录每个文件的耗时。 |

## 完整可运行示例（复制粘贴即可）

下面是完整脚本，直接放入名为 `parallel_ocr.py` 的文件中即可。没有缺失的部分——你需要的一切都在这里。

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

保存文件，调整 `YOUR_DIRECTORY` 占位符，然后运行：

```bash
python parallel_ocr.py
```

你应该会在控制台看到每个 PNG 的提取文本，正如前面所示。

## 结论

我们刚刚演示了如何通过结合 Aspose OCR 的异步批处理模式和 Python 的 `ThreadPoolExecutor`，高效地**从 PNG 文件中提取文本**。该脚本并行转换扫描页面文本，为你提供了一种可扩展的方式，以 **recognize image text python** 风格进行图像文本识别，而无需从头编写自定义线程池。

如果你准备进一步深入，可尝试：

* 将结果存储在可搜索的 SQLite 数据库中。  
* 在 OCR 前使用 OpenCV 进行图像预处理（去倾斜、去噪）。  
* 将脚本部署为 Flask 或 FastAPI 接口后的微服务。

请记住，高性能 OCR 的关键不仅是更快的引擎——还在于以最大化并发的方式向引擎提供工作。使用这里展示的模式，你可以用最少的代码改动处理数十甚至数百个 PNG 扫描。

祝编码愉快，愿你的 PDF 永远可搜索！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}