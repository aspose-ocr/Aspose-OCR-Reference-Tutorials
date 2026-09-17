---
category: general
date: 2026-01-12
description: 使用 OCR 引擎的 Python 从 PDF 中提取文本——学习如何使用 OCR 读取 PDF、加载图像进行 OCR，并获取结构化结果。
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: zh
og_description: 使用 Python OCR 引擎从 PDF 中提取文本。本教程展示了如何使用 OCR 读取 PDF、加载图像进行 OCR，以及使用
  Python OCR 引擎获得可靠的结果。
og_title: 使用 OCR 引擎的 Python 提取 PDF 文本 – 完整指南
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 使用 OCR 引擎的 Python 从 PDF 提取文本 – 步骤指南
url: /zh/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR 引擎 Python 从 PDF 提取文本 – 完整教程

是否曾经需要**从 PDF 提取文本**，但文件只是扫描的图像？你并不孤单。在许多真实项目中，收到的 PDF 没有可选文本，因此唯一的办法是**使用 OCR 读取 PDF**。  

在本指南中，我们将逐步演示一个实用的端到端解决方案，准确展示如何**加载图像进行 OCR**，启动**OCR 引擎 Python**，并提取结构化文本以供下游流水线使用。没有模糊的引用，只有一个完整、可直接运行的示例，您今天即可复制粘贴使用。

## 您将学到的内容

- 如何安装并导入所需的 Python OCR 库。  
- 从 PDF 文件**加载图像进行 OCR**的完整步骤。  
- 如何调用引擎的 `recognize_structured()` 方法并遍历块、行和单词。  
- 处理低置信度结果和多页 PDF 的技巧。  

通过本教程，您将拥有一个可靠的脚本，能够**从 PDF 文档中提取文本**，无论文档是一页还是一百页。

---

![展示 OCR 引擎处理 PDF 并输出结构化文本的示意图](images/ocr_flow.png "从 PDF 提取文本示意图")

*图片替代文字：展示 OCR 处理步骤的从 PDF 提取文本示意图。*

## 前置条件

- Python 3.9 或更高版本（代码使用 f‑string 和类型提示）。  
- 一个可通过 pip 安装的 OCR 包，提供 `OcrEngine` 类（例如，虚构的 `pyocr` 库）。  
- 要处理的本地 PDF 文件（例如 `form.pdf`）。  

如果缺少 OCR 库，请使用以下方式安装：

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## 步骤 1：从 PDF 提取文本 – 设置 OCR 引擎

在我们能够**使用 OCR 读取 PDF**之前，需要先创建一个引擎实例。可以把引擎想象成大脑，它查看每个像素并判断它对应的字符。

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **为什么这很重要：** 只初始化一次引擎即可在多个文件之间复用已加载的语言包，从而节省时间和内存。

---

## 步骤 2：加载图像进行 OCR – 准备 PDF

PDF 不是原始图像，因此库通常提供辅助函数，将第一页（或全部页面）转换为 OCR 引擎能够识别的图像。

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **提示：** 如果 PDF 有多页，许多 OCR 库允许传入 `page=2` 或在 `engine.load_image(pdf_path, page=n)` 上循环。对于大型文档，建议分批处理页面以避免内存激增。

---

## 步骤 3：使用 OCR Engine Python – 识别结构化文本

现在开始进行繁重的工作。`recognize_structured()` 调用会返回块 → 行 → 单词的层级结构，每个元素都带有语言、置信度和边界框等注释。

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **你将得到：**  
> - `structured_result.blocks` – 顶层容器（通常是段落或列）。  
> - 每个块包含 `lines`，每行包含 `words`。  
> - 置信度分数可用于过滤可疑结果。

---

## 步骤 4：遍历结果 – 访问块、行和单词

下面是一个简洁的循环，打印最有用的信息。您可以自由扩展它，以写入 JSON、CSV 或写入数据库。

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### 预期输出

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **为什么您会喜欢它：** 该层级结构模拟了人类阅读页面的方式，便于后续重建表格或列布局。

---

## 步骤 5：处理边缘情况 – 低置信度与多页 PDF

### 低置信度单词

如果单词的置信度低于例如 `0.70`，您可能需要将其标记为手动审查：

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### 处理所有页面

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **专业提示：** 如果 OCR 库每次都重新渲染图像，请将中间图像缓存为 PNG，这可以为大批量处理节省数秒时间。

---

## 完整可运行脚本

将所有内容整合在一起，以下是一个可以立即运行的单文件脚本：

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

将其保存为 `extract_pdf_ocr.py` 并运行：

```bash
python extract_pdf_ocr.py
```

您应该会在控制台看到块级细节的打印，以及任何低置信度警告。

---

## 结论

我们刚刚介绍了一种完整、可用于生产环境的方式，使用 **OCR engine Python** **从 PDF 提取文本**。从安装库、通过 **加载图像进行 OCR**、到 **使用 OCR 读取 PDF**，再到遍历结构化输出，您现在拥有一个可复用的脚本，可适配任何项目。

您可以进一步探索的下一步：

- 将层级结构导出为 JSON，以供下游 NLP 流水线使用。  
- 添加语言检测，以实时切换 OCR 模型。  
- 结合 `pdf2image` 预处理包含复杂布局的 PDF。  

在多页发票批次上尝试一下，调整置信度阈值，看看您能多快将扫描的 PDF 转换为可搜索、可编辑的文本。如果遇到任何问题，请在下方留言——祝您 OCR 愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}