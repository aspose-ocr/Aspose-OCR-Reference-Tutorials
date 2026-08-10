---
category: general
date: 2026-06-28
description: 如何在 Python 中批量 OCR——从图像中提取文本，并使用批量 OCR 处理将扫描页转换为文本。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: zh
og_description: 学习如何在 Python 中批量进行 OCR，提取图像中的文本，并通过高效的批量 OCR 处理将扫描页转换为文本。
og_title: 如何在 Python 中批量 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中批量 OCR – 提取图像文字的完整指南
url: /zh/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中批量 OCR – 完整指南：从图像提取文本

如果你在想 **how to batch OCR in Python**，你来对地方了。本教程向你展示一种快速的方式来 **extract text from images** 并 **convert scanned pages to text**，使用单个 OCR 引擎实例。无需再一次又一次地复制粘贴文件——让代码来完成繁重的工作。

我们将逐步讲解你需要的所有内容：安装库、加载整个扫描文件夹、运行批量 OCR 处理，以及优雅地处理结果。完成后，你将拥有一个可复用的脚本，能够在几秒钟内将一堆 PNG 或 JPEG 转换为可搜索的文本文件。

## 你需要的准备

* 已安装 Python 3.9+（代码在 3.8 也能运行，但 3.9+ 提供最新的类型特性）。
* 一个现代的 OCR 库——这里我们使用 **Aspose.OCR for Python via .NET**，它公开了原始代码片段中展示的 `OcrEngine` 类。  
  ```bash
  pip install aspose-ocr
  ```
* 一个包含扫描页的文件夹（`page1.png`、`page2.png`，…）。只要 Pillow 能打开的格式都可以，因此 PDF、TIFF 或 BMP 也可以。
* 一点点好奇心——如果你从未自动化过 image‑to‑text，你即将看到批量 OCR 为什么是游戏规则的改变者。

> **专业提示：** 如果你更倾向于使用纯 Python 库，可将 `OcrEngine` 替换为 `pytesseract.image_to_string`。其余逻辑保持不变。

## 如何在 Python 中批量 OCR – 步骤指南

下面是完整且可运行的脚本。每行都有注释，帮助你了解 *why* 每个部分重要，而不仅仅是 *what* 它做了什么。

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### 预期输出

对包含三个 PNG 扫描的文件夹运行脚本会产生类似以下的输出：

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

预览显示每页的前 200 个字符，完整文本保存在 `ocr_output` 目录中。

## 使用单个引擎从图像中提取文本

为什么我们只创建 **one** `OcrEngine` 并重复使用它？实例化引擎可能代价高昂，因为它会加载语言包和本机 DLL。通过在批处理中共享同一个实例，你可以：

* **节省内存** – 只在 RAM 中保留一套资源。
* **提升速度** – 引擎保持热状态，避免重复初始化。
* **保持一致性** – 相同的识别设置适用于每一页，这在你想 **extract text from images** 且页面布局相同的情况下至关重要。

如果需要微调识别（例如，启用拼写检查或更改语言），请在调用 `recognize_batch` 之前进行 *before*。所有后续页面将自动继承这些设置。

## 高效地将扫描页转换为文本

问题的核心——**convert scanned pages to text**——由 `engine.recognize_batch(images)` 解决。库在后台线程池中处理每张图像，因此在多核机器上可实现近线性扩展。需要注意的几点有：

* **图像质量很重要** – 300 dpi 或更高可获得最佳效果。如果扫描件分辨率低，考虑在送入引擎前使用 Pillow 进行上采样。
* **彩色与灰度** – OCR 引擎通常在 8 位灰度图像上运行更快。你可以添加预处理步骤：
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **语言支持** – Aspose.OCR 支持超过 40 种语言。如果不是使用英文，请在批处理调用前设置 `engine.language = "eng"` 或 `"fra"`。

## 批量 OCR 处理最佳实践

即使上述代码已经相当简洁，生产级批量 OCR 通常仍需要一些额外的防护措施：

| 关注点 | 推荐做法 |
|---------|----------------------|
| **大批量（> 500 文件）** | 将其拆分为 100–200 张图像的块，以保持内存占用适中。 |
| **损坏或不受支持的文件** | `load_images` 辅助函数已经捕获异常并记录警告；你也可以编写回退机制以跳过或移动损坏文件。 |
| **进度监控** | 如果库提供每图像回调，则在循环中包装 `recognize_batch`，在每张图像后返回。 |
| **后处理** | 对生成的字符串运行拼写检查或正则表达式清理，以提升后续可搜索性。 |
| **并行** | 如果有多节点部署，可将文件夹分配给各工作节点，最后合并 `.txt` 输出。 |

这些技巧帮助你将 **batch OCR processing** 从少量页面扩展到数千页，而不会导致脚本崩溃。

## 常见问题

**Q: 我可以直接在 PDF 上使用吗？**  
A: 当然可以。先将每页 PDF 转换为图像（例如，使用 `pdf2image`），然后将得到的列表传递给 `recognize_batch`。其余管道保持不变

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于其中展示的技术。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 提取图像文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用文件夹的 OCR 操作提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [如何使用 Aspose.OCR for .NET 从 ZIP 存档中提取文本](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}