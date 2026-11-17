---
category: general
date: 2026-05-31
description: 学习如何使用批量图像转文本脚本在 Python 中将图像转换为文本。使用 Aspose.OCR 在几分钟内识别扫描图像中的文本。
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: zh
og_description: 使用 Python 即时将图像转换为文本。本指南展示批量图像转文本转换以及如何使用 Aspose.OCR 从扫描图像中识别文本。
og_title: 将图像转换为文本 Python – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: 将图像转换为文本（Python）——完整逐步指南
url: /zh/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图像转换为文本（Python） – 完整分步指南

有没有想过如何 **convert images to text python** 而不需要搜索数十个库？你并不是唯一的。无论是数字化旧收据、从扫描的发票中提取数据，还是构建可搜索的 PDF 档案，将图片转换为纯文本文件都是许多开发者的日常工作。

在本教程中，我们将演示一个 **bulk image to text conversion** 流程，该流程能够识别扫描图像中的文本，将每个结果保存为单独的 `.txt` 文件，并且只需几行 Python 代码即可完成。无需为晦涩的 API 四处寻找——Aspose.OCR 完成繁重的工作，我们将向您展示如何正确使用它。

## 您将学到的内容

- 如何安装和配置 Aspose.OCR for Python 包。  
- 使用 `BatchOcrEngine` 进行 **convert images to text python** 的确切代码。  
- 处理常见陷阱（如不受支持的格式或损坏的文件）的技巧。  
- 验证 **recognize text from scanned images** 步骤实际成功的方法。  

阅读完本指南后，您将拥有一个可直接运行的脚本，能够一次性处理成千上万的图像——非常适合任何批处理场景。

## 前提条件

- 在机器上已安装 Python 3.8+。  
- 一个包含图像文件（PNG、JPEG、TIFF 等）的文件夹，您希望将其转换为文本。  
- 有效的 Aspose Cloud 账户或免费试用许可证（免费层已足以进行测试）。  

如果您已具备上述条件，让我们开始吧。

---

## 第一步 – 设置 Python 环境

在编写任何 OCR 代码之前，请确保您在一个干净的虚拟环境中工作。这可以隔离依赖并防止版本冲突。

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **专业提示：** 保持项目目录整洁——创建一个名为 `ocr_project` 的子文件夹并将脚本放入其中。这会让后续的路径处理变得轻而易举。

## 第二步 – 安装 Aspose.OCR for Python

Aspose.OCR 是商业库，但它提供了一个可从 PyPI 获取的免费 NuGet 风格的 wheel 包。请在已激活的虚拟环境中运行以下命令：

```bash
pip install aspose-ocr
```

如果遇到权限错误，请添加 `--user` 标志或使用 `sudo` 运行该命令（仅限 Linux/macOS）。安装完成后，您应该会看到类似如下的输出：

```
Successfully installed aspose-ocr-23.9.0
```

> **为什么选择 Aspose？** 与许多开源 OCR 工具不同，Aspose.OCR 开箱即支持 **bulk image to text conversion**，并且能够在无需额外配置的情况下处理多种图像格式。它还提供了 `BatchOcrEngine` 类，使得 “convert images to text python” 任务只需一行代码即可完成。

## 第三步 – 使用批量 OCR 将图像转换为文本（Python）

现在进入教程的核心。下面是一个可直接运行的脚本，它会：

1. 导入 OCR 引擎类。  
2. 实例化一个 `BatchOcrEngine`。  
3. 将引擎指向包含图像的输入文件夹。  
4. 指定引擎将每个提取的文本文件写入输出文件夹。  
5. 调用 `recognize()` 方法，逐个 **recognize text from scanned images**。  

将以下内容保存为项目文件夹中的 `batch_ocr.py`：

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### 工作原理

- **`BatchOcrEngine`** 包装了普通的 `OcrEngine`，并添加了文件夹级别的编排功能，这正是批量 **convert images to text python** 时所需的。  
- `input_folder` 属性告诉引擎在哪里查找源图像。它会自动扫描目录并排队所有受支持的文件类型。  
- `output_folder` 属性决定每个 `.txt` 文件的存放位置。引擎会保持原始文件名的对应关系，例如 `receipt1.png` 会生成 `receipt1.txt`。  
- 调用 `recognize()` 会触发内部循环，加载每张图像、执行 OCR 并写入结果。该方法会阻塞直至所有文件处理完毕，便于后续操作（例如压缩输出文件夹）。  

#### 预期输出

运行脚本时：

```bash
python batch_ocr.py
```

您应该会看到：

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

在 `output_texts` 中，您会找到每张图像对应的纯文本文件。使用文本编辑器打开任意文件，您将看到原始 OCR 结果——通常与原始印刷文本非常接近。

## 第四步 – 验证结果并处理错误

即使是最好的 OCR 引擎，也可能在低分辨率扫描或严重倾斜的页面上出现错误。以下是一种快速检查输出并记录任何失败的方法。

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

**为什么要添加此代码？**  
- 它可以捕获引擎静默生成空字符串的情况（在不可读的图像中很常见）。  
- 它会提供问题文件列表，方便您手动检查或使用不同设置重新运行（例如，增加 `OcrEngine.preprocess` 选项）。

### 边缘情况与调整

| 情况 | 建议解决方案 |
|-----------|----------------|
| 图像旋转了 90° | 设置 `batch_engine.ocr_engine.rotation_correction = True`。 |
| 混合语言（英语 + 法语） | 在调用 `recognize()` 之前使用 `batch_engine.ocr_engine.language = "eng+fra"`。 |
| 先将大型 PDF 转换为图像 | 将 PDF 拆分为单页图像，然后将文件夹提供给批处理引擎。 |
| 在超大批次上出现内存错误 | 顺序处理较小的子文件夹，或增加 `batch_engine.max_memory_usage`。 |

## 第五步 – 自动化整个工作流（可选）

如果您需要每天夜间运行此转换，可将脚本包装在简单的 shell 或 Windows 批处理文件中，并使用 `cron`（Linux/macOS）或任务计划程序（Windows）进行调度。以下是适用于类 Unix 系统的最小化 `run_ocr.sh`：

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

使其可执行（`chmod +x run_ocr.sh`），并添加 cron 条目：

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

这将在每天凌晨 2 点运行转换，并记录所有输出以供后续查看。

---

## 结论

您现在拥有一种经过验证、可投入生产的方式，使用 Aspose.OCR 的 `BatchOcrEngine` **convert images to text python**。该脚本能够处理 **bulk image to text conversion**，优雅地将每个结果写入专属文件，并包含验证步骤，以确保您能够正确 **recognize text from scanned images**。

接下来您可以：

- 尝试不同的 OCR 设置（语言包、去倾斜、降噪）。  
- 将生成的文本导入 Elasticsearch 等搜索索引，实现即时全文搜索。  
- 将此流水线与 PDF 转换工具结合，一次性处理扫描的 PDF。  

有任何问题，或发现某种文件类型出现异常？请在下方留言，我们一起排查。祝编码愉快，愿您的 OCR 运行快速且无错误！

## 接下来您可以学习什么？

- [使用 Aspose OCR 从图像提取文本 – 分步指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用文件夹 OCR 操作提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [使用 Aspose.OCR 提取图像文本（C#）并选择语言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}