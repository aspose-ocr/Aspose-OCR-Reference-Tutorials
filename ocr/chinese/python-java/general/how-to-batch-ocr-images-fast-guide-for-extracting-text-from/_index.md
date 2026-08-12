---
category: general
date: 2026-01-12
description: 如何在 Python 中快速批量 OCR 图像并从 JPEG 文件提取文本。通过完整可运行的示例学习逐步批处理。
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: zh
og_description: 如何批量 OCR 图像并从 JPEG 文件中提取文本。本指南将带您完成一个完整的、可直接运行的 Python 解决方案。
og_title: 如何批量 OCR 图像 – 快速 Python 教程
tags:
- OCR
- Python
- image processing
title: 如何批量 OCR 图像 – JPEG 文件文字提取快速指南
url: /zh/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR 图像 – 快速提取 JPEG 文件文本指南

是否曾想过 **如何批量 OCR 图像** 而不必为每个文件单独编写脚本？你并不孤单。在许多项目中——发票扫描、档案数字化或内容审核——我们需要一次性从数十甚至数百个 JPEG 文件中提取文本。好消息是，只需几行 Python 代码，你就能拥有一个可复用的引擎，随时嵌入任何流水线。

在本教程中，我们将精准演示 **如何批量 OCR 图像**，随后逐步讲解从 JPEG 文件提取文本、处理边缘情况以及验证输出。完成后，你将拥有一个可自行运行的脚本，能够针对任意图像文件夹执行，并了解批处理对性能和可维护性的重要性。

## 你将学到

- 搭建一个简单的 OCR 引擎并配置为英文。
- 使用 `pathlib` 收集目录下的所有 JPEG 文件。
- 一次性调用 OCR 引擎处理整个批次。
- 为每张图像显示识别文本的预览。
- 处理大批量、不同语言以及常见陷阱的技巧。

**前置条件**：Python 3.8+、`ocr` 库（或任何兼容的包装器），以及你想要分析的 JPEG 图像文件夹。无需外部服务——全部在本地运行。

---

## 步骤 1：初始化 OCR 引擎 – 批量 OCR 图像的核心

在我们能够 **批量 OCR 图像** 之前，需要一个能够读取文本的引擎。大多数库都通过创建引擎对象、可选地设置语言，然后在每个文件上复用该对象。

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*为什么重要*：只初始化一次引擎可以避免重复加载语言模型的开销。同时，你可以在单一位置调整设置（例如 DPI、字符白名单），这些设置会应用于整个批次。

> **专业提示**：如果你计划处理多语言文档，将 `ocr.Language.ENGLISH` 替换为 `ocr.Language.MULTI`，或在批次开始前加载多个语言包。

---

## 步骤 2：收集所有 JPEG 文件 – “从 JPEG 文件提取文本” 部分

引擎准备好后，需要告诉它要处理哪些图像。使用 `pathlib` 可以让代码跨平台且简洁。

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*为什么重要*：先收集文件列表后，我们可以一次性将整个集合传递给 OCR 引擎——这正是 **如何批量 OCR 图像** 的核心。如果有子文件夹，可将 `glob("**/*.jpg")` 改为递归搜索。

> **边缘情况**：如果你的图像扩展名混杂（`.jpeg`, `.JPG`），请扩展 glob 模式：`image_dir.rglob("*.[jJ][pP][eE]?g")`。

---

## 步骤 3：一次性处理整个批次 – 批量 OCR 的真正威力

大多数现代 OCR 库都提供 `process_batch`（或类似命名）方法，接受可迭代的文件路径。这是高效 **如何批量 OCR 图像** 的核心。

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*为什么重要*：一次批量调用可以减少 Python 与 C 之间的切换次数，保持语言模型常驻内存，并且通常支持内部并行化。返回的结果是一个对象列表——每个对象包含识别文本和置信度分数。

> **性能提示**：对于非常大的批次（数千张图像），考虑将列表拆分为更小的块（例如 200 文件）以避免过度占用内存。

---

## 步骤 4：显示提取文本的预览 – 快速验证

批次完成后，查看每个结果的前几个字符非常有用。这可以帮助你确认 OCR 是否真的从 JPEG 文件中提取了文本。

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*为什么重要*：简短的预览让你在不打开每个文件的情况下发现明显的失败（如空输出、乱码）。如果发现系统性问题，可调整引擎设置后重新运行批次。

> **常见陷阱**：忘记去除换行符会导致预览杂乱。`replace("\n", " ")` 这一行可以清理它。

---

## 完整工作示例 – 所有步骤合并

下面是完整脚本，你可以复制粘贴、修改目录路径后直接运行。它演示了从头到尾的 **如何批量 OCR 图像** 工作流。

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**预期输出**（示例）：

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

如果预览显示了有意义的文本，说明你已经成功使用批量方式 **从 JPEG 文件提取文本**。

---

## 处理大批量及高级场景

### 将大型工作负载分块
当处理成千上万张图像时，内存可能成为瓶颈。将列表拆分为更小的块：

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### 切换语言
如果文档包含法语或西班牙语，请在批次前更改语言：

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### 将结果保存到磁盘
如果不想仅仅打印输出，可以将每个 OCR 结果写入 `.txt` 文件：

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## 结论

现在你已经掌握 **如何批量 OCR 图像** 并可靠地 **从 JPEG 文件提取文本**，只需一个简洁的 Python 脚本。通过一次性初始化引擎、收集所有 JPEG 路径、在单个批次中处理它们并预览输出，你即可实现速度与简洁性的双赢。接下来，你可以扩展工作流——添加多语言支持、将结果存入数据库，或将脚本集成到更大的文档处理流水线中。

准备好下一步了吗？尝试将 `ocr` 库换成 Tesseract，实验不同的图像预处理（阈值化、缩放），或将提取的文本喂入自然语言处理模型进行自动分类。天地无限，而你已经拥有坚实的基础。

祝编码愉快，愿你的 OCR 批次永远无错误！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}