---
category: general
date: 2026-03-26
description: 如何使用 Python 高效批量 OCR——学习从图像和 PDF 中提取文本并进行并行处理的 OCR 转换。
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: zh
og_description: 如何高效批量 OCR——使用 Python 的图像文字提取、PDF OCR 转换和批量 OCR 处理分步指南
og_title: 如何批量 OCR：快速并行文本提取
tags:
- OCR
- Python
- Parallel Computing
title: 如何批量 OCR：快速并行文本提取
url: /zh/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR：快速并行文本提取

有没有想过 **how to batch ocr**，当你手头有几十页扫描件、截图和 PDF 时该怎么办？你并不是唯一的——大多数开发者都会遇到同样的难题：逐个处理文件会成为痛苦的瓶颈。  

好消息是，你可以启动少量工作线程，将所有文件喂给它们，然后观看 OCR 引擎并行处理批次。在本教程中，我们将演示一个完整、可直接运行的示例，展示 **extract text from images**、执行 **pdf ocr conversion**，并利用 **parallel ocr processing** 提速。

> **你将收获**  
> * 一个完整的 Python 脚本，能够一次性处理 PNG、TIFF、PDF 和 JPG 的混合列表。  
> * 理解线程池为何能加速 I/O 密集型 OCR 任务。  
> * 处理错误、大型 PDF 和自定义线程数的技巧。  

## 前置条件

在开始之前，请确保你具备以下条件：

| 要求 | 原因 |
|------|------|
| Python 3.8+ | 支持现代语法与 `concurrent.futures` |
| `ocr` 库（或任何兼容的 OCR 包装器） | 提供 `OcrBatchProcessor` 与结果对象 |
| 若干示例文件（PNG、TIFF、PDF、JPG） | 便于演示 **extract text from images** 的效果 |
| 对线程的基本了解（可选） | 有帮助但非必需 |

如果尚未安装 `ocr` 包，请运行：

```bash
pip install ocr-lib   # replace with the actual package name
```

环境准备就绪后，让我们拆解问题。

## 第一步：导入辅助模块并实例化批处理器

我们首先需要一个地方来收集所有 OCR 任务。`OcrBatchProcessor` 类正是为此而生——它会将工作项排队，并返回一组 `Future` 对象。

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*为何重要*：导入 `as_completed` 让我们能够在每个任务完成后立即响应，而不是等最慢的文件完成。这是 **batch ocr processing** 的核心。

## 第二步：为并行执行调优工作线程池

默认情况下处理器可能只使用单线程，这会抵消批处理的意义。我们显式指定四个工作线程——如果需要，可将此数字提升至 CPU 核心数。

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*小技巧*：对于 OCR 这类 I/O 密集型任务，`CPU cores * 2` 之后往往收益递减。尝试几个数值，找到最佳平衡点。

## 第三步：将所有待 OCR 文件加入队列

这里我们添加了一组混合的图片和 PDF 文件。`add` 方法仅记录路径；实际工作会在提交批次后才开始。

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

如果需要处理整个文件夹，只需一个简短的 `glob` 循环即可：

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## 第四步：启动任务并收集 futures

调用 `submit_all` 为处理器点亮绿灯。它返回一组 `Future` 对象——可以把它们视为稍后会出现结果的占位符。

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

此时 OCR 引擎已在后台忙碌，每个线程都在处理各自的文件。

## 第五步：在任务完成后立即获取结果

使用 `as_completed`，我们按完成顺序遍历 futures，而不是提交顺序。这让脚本保持响应，尤其是当某些 PDF 比普通 PNG 耗时更长时。

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**预期输出**（为简洁起见已截断）：

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

每个块对应原始文件的纯文本表示。如果你在进行 **pdf ocr conversion**，文本将包含 OCR 引擎从每页识别出的全部内容。

## 处理边缘情况与常见陷阱

| 场景 | 需要注意的点 | 快速解决方案 |
|------|--------------|--------------|
| 损坏的图像 | `future.result()` 抛出 `OSError` | 使用 `try/except` 包裹（参见上方代码） |
| 超大 PDF（> 100 MB） | 内存压力增大，线程变慢 | 适度增加 `thread_count` 或先将 PDF 拆分为章节 |
| 多语言文档 | 默认 OCR 模型可能误识别 | 若库支持，可向 `OcrBatchProcessor` 传入语言提示 |
| 需要保留布局 | 直接 `get_text()` 会丢失列信息 | 使用 `ocr_result.get_hocr()` 或其他布局感知方法 |

### 小技巧：根据文件类型自定义线程数

如果大多数工作负载是 PDF，可以为 PDF 分配更多线程，而为小 PNG 分配更少。有的库允许为每个任务设置 `priority`；否则，你可以创建两个独立批次——一个用于图片，一个用于 PDF——并并行运行。

## 可视化概览（可选）

![如何批量 OCR 工作流图示](https://example.com/ocr-workflow.png "如何批量 OCR 工作流")

*该图展示了从文件发现 → 批次创建 → 并行执行 → 结果聚合的整个流程。*

## 完整脚本，复制粘贴即用

下面是完整程序，可直接保存为 `.py` 文件。它整合了上述所有代码片段，并附带一个自动发现目录中支持文件的简易助手。

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

将其保存为 `batch_ocr.py`，指向包含扫描件的文件夹，即可在控制台看到提取的文本。  

### 为什么这样可行

* **线程池** – OCR 大多在等待磁盘 I/O 与外部引擎调用，多线程可让 CPU 保持忙碌。  
* **`as_completed`** – 结果一旦准备好就立刻返回，适合 UI 反馈或流式管道。  
* **错误隔离** – 单个坏文件不会导致整个批次失败，`try/except` 块将失败局部化。

## 结论

简而言之，你现在已经掌握了使用 Python 的 `concurrent.futures` 结合支持批处理的 OCR 库来 **how to batch ocr**。通过配置适度的线程池、将所有支持的文件加入队列，并在完成后即时获取结果，你可以实现快速的 **parallel ocr processing**，且可靠性不受影响。  

接下来你可以：

* 将输出接入搜索索引，实现文档快速检索。  
* 扩展脚本，使每个结果写入与原文件同名的 `.txt` 文件。  
* 若 OCR 库提供异步 API，可将内置线程池替换为 `asyncio`。  

继续实验——换用 Tesseract、Azure Cognitive Services 或 Google Vision，你会发现同样的模式同样适用。祝你 OCR 愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}