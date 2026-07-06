---
category: general
date: 2026-04-26
description: 如何在 Python 中批量 OCR 文档并从扫描件中提取文本。学习使用 OcrEngine 进行逐步批处理以获取 JSON 输出。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: zh
og_description: 如何批量对扫描文件进行 OCR，并在单个脚本中提取扫描文本。完整代码、技巧及边缘案例处理。
og_title: 如何批量 OCR – 快速 Python 指南
tags:
- OCR
- Python
- Automation
title: 如何批量进行 OCR——高效提取扫描文本
url: /zh/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR – 高效从扫描件提取文本

有没有想过 **如何批量 OCR** 那么多扫描的 PDF，却不让自己抓狂？你并不是唯一的——开发者们经常会问，*“怎么一次性从扫描件中提取文本？”* 好消息是，只需几行 Python 代码，就能把这项繁琐的工作变成流畅的自动化流水线。

在本教程中，我们将逐步演示一个完整、可直接运行的方案，**从扫描件中提取文本**，将结果保存为 JSON，并在最后给出一个快速的 sanity check。无需外部服务，也不需要魔法——仅使用纯 Python、`OcrEngine` 类以及一点文件夹操作。

## 你将收获什么

- 一个能够 **批量 OCR** 任意图像文件夹的完整脚本。
- 对每行代码 *为什么* 存在的清晰解释，而不仅仅是 *它做了什么*。
- 处理空文件夹、非图像文件以及大批量文件的技巧。
- 验证 JSON 输出确实包含提取文本的方法。

### 前置条件（最低要求）

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | 现代语法与类型提示 |
| `OcrEngine` library (or a compatible wrapper) | 核心 OCR 功能 |
| A directory with scanned image files (PNG, JPG, TIFF) | 输入数据 |
| Write permissions for the output folder | 保存 JSON 结果 |

如果你已经具备这些条件，太好了——让我们开始吧。

![how to batch OCR workflow](image-placeholder.png){alt="批量 OCR 工作流"}

## 步骤 1 – 初始化 OCR 引擎（how to batch OCR）

在处理任何内容之前，我们需要一个 OCR 引擎实例。可以把它想象成读取每张图像并输出文本的“大脑”。一次初始化并在整个批处理中复用它是最高效的模式。

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **为什么要复用同一个实例？**  
> 为每个文件创建新引擎会反复将庞大的模型加载到内存中，导致批处理速度大幅下降。使用同一个实例可以让模型常驻 RAM，处理成千上万张图像时几乎没有明显的性能下降。

## 步骤 2 – 指定扫描文件夹（extract text from scans）

你的扫描文件存放在磁盘的某个位置。我们需要告诉脚本去哪里找它们。使用绝对路径可以避免在脚本从不同工作目录启动时出现 “文件未找到” 的意外。

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **小技巧：**  
> 在 Windows 上，使用正斜杠（`/`）配合 `os.path.abspath` 完全没问题，这样就不必对反斜杠进行转义。

## 步骤 3 – 选择 JSON 结果的输出位置

你可能希望为 OCR 结果准备一个整洁的文件夹。将输出与源文件分离，便于后期清理或将 JSON 送入其他流水线。

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **为什么要用代码创建文件夹？**  
> 这样可以确保当目录不存在时脚本不会崩溃，且 `exist_ok=True` 使操作具备幂等性——多次运行脚本也不会报错。

## 步骤 4 – 运行批处理（how to batch OCR）

现在进入关键环节：让 `ocr_engine` 遍历 `input_dir` 中的每个文件，执行 OCR，并将 JSON 写入 `output_dir`。`format="json"` 参数指示引擎以结构化的方式序列化结果，方便下游工具使用。

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### 背后发生了什么？

1. **文件发现** – 引擎递归扫描 `input_folder`，忽略隐藏文件。  
2. **文件校验** – 仅将受支持的图像扩展名（`.png`、`.jpg`、`.tif` 等）送入 OCR 模型。  
3. **OCR 执行** – 每张图像被发送到 OCR 引擎；文本、置信度分数以及布局数据被捕获。  
4. **JSON 序列化** – 结果写入 `output_folder` 中同名但扩展名为 `.json` 的文件。

> **边缘情况处理：**  
> - **空文件夹：** 引擎记录 “No files found” 并优雅返回。  
> - **损坏的图像：** 跳过该文件，在 `batch_errors.log` 中记录错误条目，然后继续。  
> - **超大批次（10k+ 文件）：** 内存占用保持低水平，因为每张图像都是独立处理的。

## 步骤 5 – 确认转换完成

一个简单的 `print` 语句即可在控制台即时反馈。对于生产流水线，你可以将其替换为日志调用或邮件通知。

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

当看到该行输出时，你可以安全地检查 `json_output` 文件夹。每个 JSON 文件大致如下所示：

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

随后，你可以将这些 JSON 文件导入数据库、搜索索引，或任何下游分析工具。

## 常见问题（快速解答）

**Q: 如果需要处理 PDF 而不是图像怎么办？**  
A: 先将每页 PDF 转为图像（例如使用 `pdf2image`），并将生成的 PNG/JPG 文件放入 `input_dir`。批量 OCR 逻辑保持不变。

**Q: 能把输出格式改成纯文本吗？**  
A: 完全可以。将 `format="json"` 替换为 `format="txt"`，引擎就会生成仅包含提取文本的 `.txt` 文件。

**Q: 我的扫描文件分布在多个子文件夹——脚本会递归吗？**  
A: 会的。`batch_process` 默认递归遍历目录树。如果想要平铺输出，可设置 `flatten=True`（若库支持）或在后处理阶段统一 JSON 文件名。

**Q: 如何处理非拉丁文字？**  
A: 在初始化 `OcrEngine` 时传入语言参数，例如 `OcrEngine(lang="spa+eng")`。批处理循环本身无需任何改动。

## 专业技巧与常见坑点

- **批次大小很重要：** 如果出现 CPU 峰值，可在文件之间加入 `time.sleep(0.1)` 限速。  
- **日志记录：** 用 Python 的 `logging` 模块替换 `print`，以捕获时间戳和错误级别。  
- **文件命名冲突：** 若两个扫描在不同子文件夹下却拥有相同的基名，生成的 JSON 会相互覆盖。可在输出名中追加相对路径的哈希值以避免冲突。  
- **内存泄漏：** 某些 OCR 后端会保留本地资源。若库提供清理方法，请在脚本末尾调用 `ocr_engine.close()`。

## 完整脚本 – 直接复制粘贴

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**预期的控制台输出**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

你可以通过文本编辑器打开 `json_output` 中的任意文件，或在 Python 中加载来验证 JSON：

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

你应该会在控制台看到原始的 OCR 提取文本。

## 结语

我们刚刚介绍了 **如何批量 OCR** 整个扫描图像目录，并将 **从扫描件中提取文本** 保存为干净、机器可读的 JSON 文件。整个思路刻意保持简洁：一次性创建引擎实例，指向目标文件夹，让库负责繁重的工作。接下来，你可以：

- 将 JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}