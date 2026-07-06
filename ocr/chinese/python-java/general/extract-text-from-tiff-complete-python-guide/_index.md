---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Python 中提取 TIFF 文件的文本。了解如何快速可靠地将 TIFF 转换为文本。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: zh
og_description: 使用 Aspose OCR 在 Python 中提取 TIFF 文件中的文本。本指南逐步展示如何将 TIFF 转换为文本。
og_title: 从 TIFF 中提取文本 – 完整的 Python 指南
tags:
- OCR
- Python
- Aspose
title: 从 TIFF 中提取文本 – 完整 Python 指南
url: /zh/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIFF 中提取文本 – 完整 Python 指南

需要在 Python 项目中 **从 TIFF 中提取文本** 吗？本指南将向您展示如何使用 Aspose OCR 库 **将 TIFF 转换为文本**，并且以即使是初学者也能跟随的方式进行。  

如果您曾经盯着多页 TIFF，想知道如何在不手动输入的情况下获取其中的文字，那么您来对地方了。我们将完整演示整个过程——从安装包到处理加密文件等边缘情况——让您专注于构建真正重要的功能。

## 您将学到的内容

在本教程中您将了解到：

* 如何为 Python 设置 Aspose OCR。
* 读取多页 TIFF 每一页所需的完整代码。
* 处理常见陷阱的方法，如缺失字体或损坏的页面。
* 在大规模 **从 TIFF 中提取文本** 时提升准确性和性能的技巧。

完成后，您将拥有一个可直接运行的脚本，能够将任意 TIFF 转换为纯文本，供索引、搜索或下游 NLP 流程使用。

### 前置条件

* Python 3.8 或更高（库支持 3.7+）。
* 有效的 Aspose OCR 许可证——或者您可以先使用免费试用版（代码在评估模式下可运行，只是输出会带有水印）。
* 对 Python 虚拟环境有基本了解（可选但推荐）。

---

## 第一步 – 安装 Aspose OCR 包

首先：您需要 `aspose-ocr` 包。它托管在 PyPI 上，只需简单的 `pip` 安装即可。

```bash
pip install aspose-ocr
```

> **专业提示：** 使用虚拟环境（`python -m venv venv`）来保持依赖隔离。这可以防止与其他项目的版本冲突。

> **原因说明：** 安装该包会拉取实际执行重活的本机 OCR 引擎二进制文件。没有这些二进制文件，`recognize_from_tiff` 方法将不存在，您会遇到 `ImportError`。

---

## 第二步 – 导入库并创建 OCR 引擎

库已经在您的机器上后，导入它并实例化一个 `OcrEngine`。这个对象是处理图像数据的核心。

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*`OcrEngine` 类封装了所有 OCR 设置，如语言、分辨率和预处理选项。我们稍后会微调其中的几个，以提升准确性。*

---

## 第三步 – 指向您的多页 TIFF 文件

您需要提供 TIFF 文件的路径。库支持绝对路径或相对路径，但使用绝对路径可以避免脚本在不同工作目录下运行时出现意外。

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **常见错误：** 在 Windows 上忘记对反斜杠进行转义（`C:\\Images\\file.tif`）。使用原始字符串（`r"C:\Images\file.tif"`）或正斜杠可以避免此问题。

---

## 第四步 – 识别所有页面的文本

下面是本教程的核心：调用 `recognize_from_tiff`。该方法返回一个 `OcrResult` 对象列表——每页对应一个，您可以逐个遍历。

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**工作原理：** Aspose OCR 在内部将 TIFF 拆分为各个帧，对每帧运行 OCR 引擎，并将结果打包返回。这比使用 Pillow 或 ImageMagick 手动分离页面要可靠得多。

---

## 第五步 – 遍历结果并输出文本

最后，遍历 `OcrResult` 列表并打印（或保存）提取的文本。如果您的工作流需要，也可以将每页写入单独的 `.txt` 文件。

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**预期输出**（为简洁起见已截断）：

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **边缘情况处理：** 如果某页没有可识别的文本，`page_result.text` 将是空字符串。您可能需要记录这些页面，以便后续手动检查。

---

## 进阶 – 调整 OCR 设置以获得更高准确度

有时默认配置不足，尤其是低分辨率扫描或非常规字体。下面列出了一些可调节的设置：

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*这些选项是可选的，但它们常常决定输出是乱码还是干净、可搜索的稿件。*

---

## 常见陷阱及规避方法

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 所有页面输出为空 | 文件路径错误或不受支持的 TIFF 压缩方式 | 核实路径，确保 TIFF 使用受支持的压缩（如 LZW、PackBits）。 |
| 字符乱码（如 �） | 语言设置错误或缺少字体文件 | 将 `ocr_engine.language` 设置为正确的地区语言；在宿主操作系统上安装所需字体。 |
| 大型 TIFF 处理缓慢 | 默认单线程模式 | 若库版本支持，可使用 `ocr_engine.recognize_from_tiff(..., parallel=True)`。 |
| 许可证警告 | 使用试用版且未提供许可证文件 | 通过 `aocr.License().set_license("Aspose.OCR.lic")` 提供许可证密钥。 |

---

## 完整脚本 – 可直接运行

下面是完整的、独立的脚本，已整合上述所有步骤和可选调优。复制粘贴到名为 `extract_tiff_text.py` 的文件中，然后运行 `python extract_tiff_text.py`。

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**运行脚本**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

您将在控制台看到每页的预览，并在名为 `output` 的文件夹中得到 `page_1.txt`、`page_2.txt` 等文件。

---

## 结论

我们已经完整演示了如何使用 Python 和 Aspose OCR **从 TIFF 中提取文本**。从安装包到处理多页文档、调优设置以提升准确度、保存结果，整个工作流现在触手可及。  

如果您希望在生产流水线中 **将 TIFF 转换为文本**，可以考虑批量处理文件、并行化 OCR 调用，并将输出存入可搜索的索引（如 Elasticsearch）。想要更进一步的，可以尝试其他语言（`aocr.Language.Spanish`）或将原始 OCR 结果喂入拼写检查库，以清理 OCR 噪声。

对扩展、授权或与云存储集成有疑问？在下方留言吧，祝编码愉快！

---

![从 TIFF 文件到提取文本的 OCR 流程图](https://example.com/placeholder-image.png "使用 Python 提取 TIFF 文本")

*图片替代文字：使用 Python 提取 TIFF 文本的 OCR 流程图*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}