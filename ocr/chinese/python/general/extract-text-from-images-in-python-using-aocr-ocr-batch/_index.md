---
category: general
date: 2026-06-25
description: 使用 Python aocr 库从图像中提取文本——学习批量 OCR，设置识别模式为 printed，并添加 AI 后处理器。
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: zh
og_description: 使用 Python aocr 库从图像中提取文本。本教程展示批量 OCR、印刷体识别模式以及可选的 AI 后处理器。
og_title: 在Python中从图像提取文本 – 完整的aocr批处理指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: 使用 aocr OCR 批处理在 Python 中从图像提取文本
url: /zh/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 aocr OCR 批处理在 Python 中提取图像文本

是否曾经需要**提取图像中的文本**，却被成百上千的细小步骤弄得不知所措？你并不孤单。无论是数字化扫描表单、从收据中提取数据，还是构建可搜索的档案库，在大规模获取可靠的 OCR 结果时，都可能感觉像在爬一座陡坡。

好消息是？使用 **aocr 库**，只需几行代码就能启动完整的 **Python OCR 批处理**。本指南将带你一步步创建 OCR 批处理，加载文件夹中所有受支持的图像，选择正确的 **recognition mode printed**，甚至附加 **AI 后处理器**以获得额外的准确性提升。完成后，你将拥有一个可直接运行的脚本，能够从图像中提取文本并显示每个文件捕获的字符数。

## 你将学到

- 如何安装并导入 `aocr` 包。
- 设置 `OcrBatch` 以自动处理成千上万的文件。
- 为印刷文档选择最佳的识别模式。
- （可选）挂载 AI 后处理器以清理噪声结果。
- 显示每个文件路径以及其提取文本的长度。
- 处理不支持的格式或空白页等边缘情况的技巧。

### 前置条件

- 已在机器上安装 Python 3.8 或更高版本。  
- 对 Python 脚本有基本了解（循环、导入等）。  
- 拥有一文件夹的扫描图像（PNG、JPG、TIFF 等）。  

如果你满足以上条件，下面就可以开始——无需外部服务。

## 第一步：安装 aocr 库

首先，`aocr` 包不在标准库中，需要从 PyPI 拉取。

```bash
pip install aocr
```

> **专业提示：** 使用虚拟环境（`python -m venv .venv`）来保持依赖隔离。  

安装完成后，即可导入核心类。

```python
# core imports
import aocr
```

## 第二步：创建 OCR 批处理实例

`OcrBatch` 是负责遍历目录并跟踪每个图像文件的工作马。可以把它想象成一条输送带，把图片送入 OCR 引擎。

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

此时批处理为空，我们将在下一步填充它。

## 第三步：从文件夹递归添加所有受支持的图像

你可能拥有嵌套的文件夹结构——比如每个客户或每个月一个子文件夹。`add_folder` 方法会为你遍历整棵树，拉入所有可读取的图像。

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

将 `"YOUR_DIRECTORY/scanned_forms/"` 替换为系统中的真实路径。调用后，`ocr_batch.file_paths` 将保存绝对文件名列表，批处理也会知道将要处理的项目数量。

## 第四步：为印刷文本选择识别模式

`aocr` 引擎支持多种模式（手写、印刷、混合）。因为我们处理的是干净的印刷表单，需要相应设置模式。这个小标志可以显著提升准确率，因为引擎会跳过针对草写文字的繁重启发式判断。

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **为何重要：** 印刷文本拥有一致的基线和字符形状，OCR 模型可以使用更紧凑的字符字典。如果保持“auto”模式，低分辨率扫描可能会产生额外噪声。

## 第五步：（可选）附加 AI 后处理器

如果扫描件出现模糊、对比度低或字体异常，AI 后处理器可以在将原始 OCR 输出交给下游系统前进行清理。`set_ai_postprocessor` 方法期望一个实现 `process(text: str) -> str` 接口的对象。

下面是使用虚构的 `SimpleCleaner` 类的最小示例。实际使用时，你可以接入 HuggingFace Transformer、定制语言模型，甚至基于规则的拼写检查器。

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

如果跳过此步骤，批处理将直接返回原始 OCR 字符串。

## 第六步：在整个批处理中运行 OCR 并收集结果

现在开始真正的重活。`run` 方法会遍历每个文件，运行 OCR 引擎，将输出通过可选的 AI 后处理器，并返回一个字符串列表——每张图像对应一个元素。

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

由于该方法返回普通的 Python 列表，你可以像处理其他集合一样使用它——存储、写入 CSV，或写入数据库。

## 第七步：显示每个文件路径及其提取文本的长度

一个快速的完整性检查是打印每个文件提取了多少字符。如果页面为空或 OCR 失败，你会看到长度为 `0`。

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

典型输出如下：

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

看到 `0` 标记会立刻告诉你哪些文件需要二次检查（可能已损坏或根本不是图像）。

## 处理常见边缘情况

### 1. 不支持的文件类型

`aocr` 会悄悄跳过无法解码的文件。如果怀疑文件夹中混有 PDF 或 BMP，可在添加前进行过滤：

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. 大批量与内存消耗

处理成千上万的高分辨率扫描会导致内存激增。可通过分块处理来缓解：

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. 空白或低对比度页面

如果某页字符数少于 10，建议标记为手动复审：

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## 完整可运行示例

将所有内容组合起来，下面是一个可以直接复制粘贴并立即运行的脚本。将其保存为 `batch_ocr.py`。

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**预期输出**（为简洁起见已截断）：

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

运行方式：

```bash
python batch_ocr.py
```

如果一切配置正确，你将看到每张图像对应的一行，报告提取文本的字符数。

## 常见问题

**Q: 这能处理 PDF 吗？**  
A: 不能直接处理。`aocr` 只支持光栅图像。请先将 PDF 转为 PNG/TIFF（例如使用 `pdf2image`）。

**Q: 能把识别模式改为手写吗？**  
A: 完全可以——只需将 `aocr.RecognitionMode.PRINTED` 替换为 `aocr.RecognitionMode.HANDWRITTEN`。运行时间会变慢，但对草写笔记的效果更好。

**Q: 如果需要多语言支持怎么办？**  
A: 库自带语言包。安装所需语言模块（例如 `pip install aocr-lang-fr` 用于法语），并在运行前设置 `ocr_batch.language = "fr"`。

## 后续步骤与相关主题

- **并行处理：** 将批处理包装在 `concurrent.futures.ThreadPoolExecutor` 中，以利用多核 CPU。  
- **存储结果：** 将 `ocr_results` 写入 CSV 或 SQLite 数据库，以供下游分析使用。  
- **集成云 AI：** 用 HuggingFace 的 Transformer 模型替换 `SimpleCleaner`，实现最先进的拼写纠正。  
- **微调 aocr：** 若拥有自定义字体集，可探索 `aocr.Trainer` 以提升印刷模式的准确度。

---

这就是全部内容——现在你已经掌握了一套可靠的批量 OCR 方案。

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}