---
category: general
date: 2025-12-27
description: 使用 Aspose OCR 从图像中提取文本并纠正 OCR 错误。了解如何加载图像进行 OCR 并快速修正错误。
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本并即时纠正 OCR 错误。按照本教程加载图像进行 OCR 并清理结果。
og_title: 使用 Aspose OCR 从图像提取文本 – 完整指南
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: 使用 Aspose OCR 从图像提取文本 – 步骤指南
url: /zh/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像中提取文本 – 步骤指南

是否曾经需要**从图像中提取文本**却被凌乱的 OCR 输出搞得头疼？你并不孤单。在许多自动化项目中——比如发票处理、收据扫描或旧文档数字化——首要难题就是从图片中获取干净、可搜索的文本。  

在本教程中，我们将逐步演示一个完整、可运行的示例，展示如何**加载图像进行 OCR**、运行识别，然后使用 Aspose 的 AI 驱动拼写检查后处理器**纠正 OCR 错误**。完成后，你将拥有一个脚本，能够将发票的 PNG 转换为精炼、可搜索的文本，供后续工作流使用。

## 您将学习

- 如何在 Python 中安装并导入 Aspose OCR 和 AI 库。  
- 加载图像进行 OCR 所需的完整代码（无需猜测）。  
- 如何运行 OCR 引擎并捕获原始字符串。  
- 为什么 OCR 常会产生拼写错误，以及内置的拼写检查处理器如何**自动纠正 OCR 错误**。  
- 处理多页 PDF 或低分辨率扫描等边缘情况的技巧。

> **先决条件：** Python 3.8+、有效的 Aspose OCR 许可证（或免费试用版），以及你想要处理的图像文件（例如 `invoice.png`）。

---

## 从图像中提取文本 – 设置 Aspose OCR

在我们开始任何操作之前，需要准备好相应的包。Aspose 将其 OCR 引擎以 pip 可安装模块的形式分发。

```bash
pip install aspose-ocr
```

如果您也需要 AI 后处理器，请安装配套的包：

```bash
pip install aspose-ocr-ai
```

> **专业提示：** 保持你的包为最新版本。本文撰写时，最新版本为 `aspose-ocr 23.12` 和 `aspose-ocr-ai 23.12`。

一旦这些库已安装到系统中，导入你将使用的类：

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **为何重要：** 导入特定类可以保持命名空间整洁，并明确哪些组件负责识别，哪些负责后处理。

---

## 加载图像进行 OCR – 准备你的发票 PNG

接下来的逻辑步骤是将引擎指向你想读取的文件。这正是**加载图像进行 OCR**关键字大显身手的地方。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **说明：** `OcrEngine()` 创建一个带有默认设置（英语、自动旋转等）的全新引擎。`load_image()` 方法接受文件路径、流或字节数组——因此你可以从磁盘、网络或内存缓冲区中提供图像。

### 加载图像时的常见陷阱

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| 低 DPI (<300) | 字符乱码，数字缺失 | 在加载前将图像重新采样至 300 dpi 或更高 |
| 颜色模式错误（CMYK） | 字符形状错误 | 使用 Pillow 将其转换为 RGB (`Image.convert("RGB")`) |
| 多页 PDF | 仅处理第一页 | 将每页转换为图像并循环处理 |

---

## 执行 OCR 并获取原始文本

现在引擎已经知道图片所在位置，我们可以真正读取它了。

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

`recognize()` 调用返回一个普通的 Python 字符串。在许多真实场景中，输出会包含多余的空格、误读字符或断裂的换行——尤其是使用压缩字体的收据。

> **为何先捕获 raw_text：** 这为后续与清理后版本的对比提供基线，有助于调试或审计。

---

## 如何纠正 OCR 错误 – 使用 Aspose AI 拼写检查

Aspose 提供了一个轻量级的 AI 包装器，能够对原始输出运行拼写检查后处理器。这直接回答了**如何纠正 OCR 错误**的问题。

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

如果你的使用场景需要，你可以将 `"spell_check"` 替换为其他处理器，如 `"grammar_check"` 或 `"named_entity_recognition"`。

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### 拼写检查在内部的工作原理

1. **Tokenisation** – 将原始字符串拆分为单词和标点。  
2. **Dictionary Lookup** – 将每个标记与英文词典（或你提供的自定义词典）进行比对。  
3. **Contextual Scoring** – 使用小型语言模型判断纠正是否符合上下文。  
4. **Replacement** – 返回一个已应用最可能纠正的新字符串。

> **边缘情况：** 如果源语言不是英文，在创建 `AsposeAI()` 时传入相应的语言代码（例如 `AsposeAI(language="fr")`）。

---

## 验证并使用清理后的文本

此时你拥有两个变量：`raw_text`（直接的 OCR 转储）和 `clean_text`（拼写检查后的版本）。保留哪一个取决于你的下游需求。

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

如果你将结果输入到搜索引擎、数据库或机器学习模型中，始终优先使用**清理后**的版本——否则 OCR 噪声会在整个流水线中传播。

---

## 完整可运行示例

下面是完整脚本，你可以复制粘贴到名为 `extract_invoice.py` 的文件中。它假设你已经安装了两个 Aspose 包，并且在 `YOUR_DIRECTORY/invoice.png` 处有一张图像。

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

使用以下方式运行：

```bash
python extract_invoice.py
```

运行后你会看到原始转储以及更整洁的版本，并且同文件夹下会生成名为 `invoice_extracted.txt` 的文件。

---

## 常见问题解答 (FAQ)

**Q: 这能用于 PDF 吗？**  
A: 不能直接处理。请先将每页 PDF 转换为图像（例如使用 `pdf2image`），然后对生成的 PNG 循环执行脚本。

**Q: 我的语言不是英语——还能使用拼写检查吗？**  
A: 可以。将所需语言代码传给 `AsposeAI(language="de")`（德语）、`"es"`（西班牙语）等即可。

**Q: 如果 OCR 引擎误识别表格布局怎么办？**  
A: Aspose OCR 提供 `set_layout_analysis(True)` 标志。启用后可提升表格检测效果，但可能会增加处理时间。

**Q: 如何处理极大批量的文件？**  
A: 将核心逻辑封装为函数，并使用线程池或异步 IO 在多核或多机器上并行处理。

---

## 总结

我们展示了如何使用 Aspose OCR **从图像中提取文本**、如何**加载图像进行 OCR**，以及使用内置 AI 拼写检查**纠正 OCR 错误**的最直接方法。完整、可运行的脚本演示了从加载发票 PNG 到保存干净、可搜索的 `.txt` 文件的端到端流程。

欢迎自行实验：将拼写检查换成语法纠正，将输出喂入 NLP 分类器，或集成到更大的文档管理系统中。一旦拥有可靠、已纠正的文本，可能性无限。

还有关于 OCR、Aspose 或 Python 自动化的其他问题吗？在下方留言吧，祝编码愉快！

---

![从图像中提取文本示例](extract_text_image.png "使用 Aspose OCR 从图像中提取文本")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}