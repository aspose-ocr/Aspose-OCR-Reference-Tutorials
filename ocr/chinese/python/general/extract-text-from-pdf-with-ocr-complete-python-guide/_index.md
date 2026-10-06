---
category: general
date: 2026-02-09
description: 使用 Aspose 在 Python 中通过 OCR 提取 PDF 文本。学习如何使用 OCR 读取 PDF，加载 PDF 进行 OCR，并掌握高效提取
  PDF 文本的方法。
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load pdf for ocr
- how to extract pdf text
language: zh
og_description: 使用 Aspose 通过 OCR 从 PDF 中提取文本。本指南展示了如何使用 OCR 读取 PDF、加载 PDF 进行 OCR，并解答如何提取
  PDF 文本。
og_title: 使用 OCR 从 PDF 提取文本 – Python 教程
tags:
- OCR
- Python
- PDF processing
title: 使用 OCR 从 PDF 提取文本 – 完整 Python 指南
url: /zh/python/general/extract-text-from-pdf-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR 从 PDF 中提取文本 – 完整 Python 指南

是否曾经需要 **从 PDF 中提取文本**，但文件只是扫描的图片？你并不是唯一遇到这种情况的人。在许多真实项目中，收到的 PDF 只有图像，直接调用 “读取 PDF” 什么也得不到。这时 OCR 就派上用场了，今天我们将展示如何使用 Aspose OCR for Python **提取 PDF 文本**。

在本教程中，你将学习 **使用 OCR 读取 PDF**，了解 **加载 PDF 进行 OCR 的最佳方式**，并通过完整示例返回每个单词及其置信度分数。没有模糊的引用——只有可运行的脚本、每行代码意义的解释以及可直接应用的技巧。

## 本指南涵盖内容

我们将先安装 Aspose OCR 包，然后创建 `OcrEngine`，加载 PDF，执行结构化识别，最后提取每个单词及其置信度。完成后，你就能回答 “**如何提取 PDF 文本**？” 的问题，并了解结构化 OCR 与普通 OCR 的取舍。

前置条件很少：Python 3.8+、可通过 pip 安装的 Aspose OCR 库，以及一份待处理的 PDF。如果你熟悉基本的 Python 循环，就可以开始了。

为什么这很重要？因为置信度分数可以让你自动过滤低质量结果，结构化文本则提供页面、块、行、单词的层级信息——非常适合后续分析或可搜索索引。

---

![使用 Aspose OCR 提取 PDF 文本](https://example.com/placeholder-image.jpg "提取 PDF 文本")

*图片替代文字: “extract text from pdf using Aspose OCR engine in Python”*

## 第一步 – 安装并导入 Aspose OCR

在运行任何代码之前，需要先安装库。Aspose OCR 以纯 Python wheel 形式发布，只需一条 `pip` 命令即可完成。

```bash
pip install aspose-ocr
```

现在导入模块。导入语句可能看起来有点奇怪（`aspose.ocr as aocr`），但它可以保持命名空间整洁。

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr
```

*为什么重要:* 导入 `aspose.ocr` 后即可使用 `OcrEngine`，这是处理文件加载到返回结构化结果的核心类。

## 第二步 – 创建 OCR 引擎实例

`OcrEngine` 对象封装了语言、识别模式和性能设置等配置。大多数情况下默认设置已足够，后续仍可自行调优。

```python
# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()
```

> **专业提示:** 如果你知道 PDF 只包含英文文本，可设置 `ocr_engine.language = aocr.Language.English` 以提升速度。

## 第三步 – 加载 PDF 进行 OCR

现在我们 **加载 PDF 进行 OCR**。`load_image` 方法支持多种格式——PDF、JPG、PNG、TIFF——因此同一段代码也可用于其他来源。

```python
# Step 3: Load the document you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.pdf")
```

*内部原理是什么？* Aspose 会将每页解析为栅格图像，OCR 引擎随后把这些图像当作普通图片处理。这就是为何可以直接传入多页 PDF；引擎会在内部遍历每页。

## 第四步 – 执行结构化识别

结构化识别会返回一个 `OcrResult` 对象，保留布局层级（页面 → 块 → 行 → 单词）。这远比纯文本输出更丰富。

```python
# Step 4: Perform structured recognition to obtain detailed results
ocr_result = ocr_engine.recognize_structured()   # returns an OcrResult object
```

如果只需要原始文本，也可以调用 `ocr_engine.recognize()`，但会失去置信度分数和位置信息——这些信息在验证流水线中往往至关重要。

## 第五步 – 提取单词及置信度分数

下面展示 **如何提取 PDF 文本** 并获取置信度值。嵌套循环遍历层级，收集 `(word, confidence)` 元组。

```python
# Step 5: Extract recognized words and their confidence scores
recognized_words = []
for page in ocr_result.structured_text.pages:
    for block in page.blocks:
        for line in block.lines:
            for word in line.words:
                recognized_words.append((word.text, word.confidence))
```

*为何采用这种循环方式？* 每一层（页面 → 块 → 行 → 单词）都提供上下文。例如，后续可以将单词重新组合成句子，或忽略来自标题块（通常置信度较低）的单词。

### 边缘情况处理

- **空 PDF:** 如果 `ocr_result.structured_text.pages` 为空，`recognized_words` 也会保持为空——请做好容错处理。
- **低置信度:** 你可能想过滤掉 `confidence < 0.6` 的单词。例如：

```python
high_confidence = [(t, c) for t, c in recognized_words if c >= 0.6]
```

## 第六步 – 显示示例单词及其置信度

快速的完整性检查是打印第一条单词及其置信度。这可以确认引擎确实读取到了内容。

```python
# Step 6: Show a sample word with its confidence
if recognized_words:
    sample_text, sample_conf = recognized_words[0]
    print(f"{sample_text} (conf: {sample_conf:.2f})")
```

典型输出如下：

```
Invoice (conf: 0.98)
```

如果看到置信度低于 0.5，建议在 OCR 前进行图像预处理（如去倾斜）以提升效果。

## 第七步 – 汇总识别到的单词总数

最后，为用户提供一个简要的统计信息。这在日志或 UI 反馈中非常实用。

```python
# Step 7: Summarize the total number of words recognized
print(f"Total words recognized: {len(recognized_words)}")
```

示例控制台输出：

```
Total words recognized: 1,342
```

## 完整可运行示例

将所有代码组合在一起，下面是完整脚本，可直接复制到名为 `extract_ocr.py` 的文件中。将 `"YOUR_DIRECTORY/input.pdf"` 替换为你的 PDF 路径。

```python
# extract_ocr.py – Complete example to extract text from PDF with OCR

import aspose.ocr as aocr

def extract_words(pdf_path):
    # Initialize OCR engine
    ocr_engine = aocr.OcrEngine()
    
    # Load PDF (this is the step where we **load PDF for OCR**)
    ocr_engine.load_image(pdf_path)
    
    # Run structured recognition
    ocr_result = ocr_engine.recognize_structured()
    
    # Collect words + confidence
    words = []
    for page in ocr_result.structured_text.pages:
        for block in page.blocks:
            for line in block.lines:
                for word in line.words:
                    words.append((word.text, word.confidence))
    return words

if __name__ == "__main__":
    pdf_file = "YOUR_DIRECTORY/input.pdf"
    recognized = extract_words(pdf_file)
    
    # Show first word as a quick sanity check
    if recognized:
        txt, conf = recognized[0]
        print(f"{txt} (conf: {conf:.2f})")
    
    # Summary
    print(f"Total words recognized: {len(recognized)}")
```

运行该脚本会打印示例单词及其置信度以及总计数——正是验证 **使用 OCR 读取 PDF** 是否成功所需的全部信息。

## 常见问题与注意事项

| 问题 | 解答 |
|----------|--------|
| *我的 PDF 有密码保护怎么办？* | 调用 `ocr_engine.load_image("file.pdf", password="secret")`。引擎会在栅格化前先解密。 |
| *能批量处理多个 PDF 吗？* | 完全可以。将 `extract_words` 调用放在遍历文件路径列表的循环中即可。 |
| *是否需要额外安装语言包？* | 对于非英文 PDF，需要安装对应语言包（`pip install aspose-ocr‑lang‑<lang>`）。 |
| *如何提升低置信度分数？* | 在加载前对 PDF 页面进行预处理（提高 DPI、二值化），或启用 `ocr_engine.image_preprocessing = True`。 |

## 后续步骤 – 超越基础提取

既然已经掌握了 **如何提取 PDF 文本** 并获取置信度分数，你可以进一步探索：

- **将单词索引到 Elasticsearch**，实现全文搜索。
- **将结构化层级导出为 JSON**，供下游分析使用。
- **结合 PDF‑to‑image 工具**，微调 DPI 设置以获得更佳识别效果。
- **将流水线集成到 Flask 或 FastAPI 接口**，提供 OCR 即服务。

这些扩展都基于我们刚才讲解的核心代码，能够让你快速迭代。

---

### 结论

我们完整演示了如何使用 Aspose OCR 在 Python 中 **从 PDF 提取文本**。通过加载 PDF 进行 OCR、执行结构化识别并遍历页面、块、行、单词，你不仅可以获得原始文本，还能得到每个单词的置信度——这对质量控制至关重要。

欢迎自行修改脚本、添加预处理步骤，或将其嵌入更大的文档处理工作流。如有疑问，欢迎在下方留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}