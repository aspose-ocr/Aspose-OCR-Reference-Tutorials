---
category: general
date: 2026-06-16
description: 如何在几分钟内使用 Python 对 PDF 进行 OCR——学习从 PDF 中提取文本、对 PDF 进行 OCR，以及高效转换扫描 PDF
  文本。
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: zh
og_description: 如何使用 Python 对 PDF 进行 OCR：一步一步的指南，提取 PDF 文本、对 PDF 进行 OCR，并转换扫描 PDF
  文本。
og_title: 如何在Python中对PDF进行OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 如何在 Python 中对 PDF 进行 OCR – 完整指南
url: /zh/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中对 PDF 进行 OCR – 完整指南

有没有想过 **如何对 PDF 进行 OCR** 而不费吹灰之力？你并不是唯一的开发者；无数人在尝试将扫描页转换为可搜索文本时都会遇到同样的难题。好消息是，只需几行 Python 代码，你就可以加载 PDF 进行 OCR、对 PDF 页面执行 OCR，并在几秒钟内提取出干净、可编辑的字符串。

在本教程中，我们将通过一个真实案例，向你展示如何对 PDF 文档进行 OCR、从 PDF 页面提取文本，甚至将扫描的 PDF 文本转换为 JSON 结构化结果。没有废话，只有可以直接放入项目的可运行脚本。

## 你需要准备的东西

- Python 3.8+（任何近期版本均可）
- `ocr` 库（或兼容的包装器——这里我们假设使用遵循下述 API 的通用 `ocr` 包）
- 一个需要处理的多页扫描 PDF
- 你喜欢的 IDE 或编辑器（VS Code、PyCharm，甚至是普通文本编辑器）

就这些。如果你已经准备好，就可以像专业人士一样开始从 PDF 文件中提取文本了。

## 第一步 – 设置 OCR 引擎（如何对 PDF 进行 OCR）

首先：创建一个 OCR 引擎实例。把引擎想象成读取文档每个像素的大脑。

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **小贴士：** 初始化引擎的开销很小，但如果你计划批量处理数十个 PDF，重复使用同一个 `engine` 对象可以节省内存。

![OCR 流程图，展示如何对 PDF 进行 OCR](/images/ocr-pdf-workflow.png "如何对 PDF 进行 OCR 工作流")

## 第二步 – 选择正确的语言（对 PDF 运行 OCR）

如果你的扫描件是英文的，请显式设置语言。跳过此步骤会让引擎自行猜测，速度会更慢且有时准确率不高。

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

为什么要这么做？因为明确告诉引擎 **对 PDF 运行 OCR** 并指定语言，可显著提升识别率——尤其是包含技术术语的文档。

## 第三步 – 聚焦特定页面（加载 PDF 进行 OCR）

如果只需要前几章，处理一个 500 页的大档案显得多余。你可以这样限制页面范围：

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

这小小的调整让引擎 **加载 PDF 进行 OCR** 时只处理你关心的页面，从而节省时间和 CPU 资源。

## 第四步 – 加载文档（加载 PDF 进行 OCR）

现在把引擎指向实际文件。确保路径正确，否则会抛出 `FileNotFoundError`。

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

此时引擎已经 **加载了 PDF 进行 OCR**，解析了内部结构，准备开始繁重的工作。

## 第五步 – 启动识别（对 PDF 运行 OCR）

这就是魔法发生的时刻。`recognize()` 调用会扫描每个像素、应用语言模型，并返回一个丰富的结果对象。

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

在幕后，引擎 **对 PDF 页面运行 OCR**，构建文本层，甚至为每个词保存置信度分数。

## 第六步 – 提取完整文本（从 PDF 中提取文本）

大多数场景只需要纯文本。`text` 属性会给你一个包含引擎看到的所有内容的连接字符串。

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

现在你已经成功 **从 PDF 中提取文本**——可以将其喂入搜索索引、数据库，或直接 `print()`。

## 第七步 – 检查详细结果（转换扫描的 PDF 文本）

如果你需要的不止原始字符串——比如想要获取边界框或置信度分数——可以使用 JSON 导出。这实际上是 **将扫描的 PDF 文本转换** 为机器可读的格式。

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

JSON 包含每页的数组，每个条目保存识别的文本、在页面上的位置以及置信度指标。非常适合后续的实体抽取或自定义高亮等处理。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **乱码字符** | 语言设置错误或缺少字体 | 明确将 `engine.language` 设置为正确的语言。 |
| **缺页** | `pdf_page_range` 设得太窄 | 再次确认元组 `(start, end)` 与文档页数匹配。 |
| **性能下降** | 大 PDF 一次性处理 | 将 PDF 拆分为块，或使用 `concurrent.futures` 并行处理页面。 |
| **输出为空** | 文件路径拼写错误或 PDF 无法读取 | 确认文件存在且未被密码保护。 |

提前解决这些问题可以为你省下大量调试时间。

## 示例扩展

- **批量处理：**遍历 PDF 目录，复用同一个 `engine` 实例。
- **自定义输出：**将 `pdf_result.text` 写入 `.txt` 文件，或直接送入 Elasticsearch 等搜索引擎。
- **图像提取：**部分 OCR 库会提供每页图像，你可以提取出来进行视觉校验。

下面是一个小片段，演示如何批量处理文件夹：

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## 小结 – 我们覆盖了哪些内容

我们从 **如何在 Python 中对 PDF 进行 OCR** 的问题出发，随后：

1. 初始化了 OCR 引擎。
2. 设置语言（可选但推荐）。
3. 限制页面范围以提升速度。
4. 加载了 PDF 文件。
5. 对文档运行 OCR。
6. **从 PDF 中提取文本** 供即时使用。
7. 将详细结果导出为 **转换扫描的 PDF 文本** 的 JSON。

这些步骤为将任何扫描 PDF 转换为可搜索、可编辑内容奠定了坚实基础。

## 下一步

- 尝试不同语言（`ocr.Language.SPANISH`、`ocr.Language.FRENCH`），看看引擎如何处理多语言文档。
- 若扫描件分辨率低，可调节 `engine.dpi` 参数——更高 DPI 往往能提升准确率。
- 将 OCR 输出与 spaCy 等自然语言处理库结合，自动抽取实体、日期或关键短语。

对 **加载 PDF 进行 OCR** 有疑问，或在 **对 PDF 运行 OCR** 时遇到卡顿？在下方留言，我们一起排查。祝编码愉快，享受将顽固扫描件变成可搜索金矿的过程！

## 接下来你可以学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索项目中的替代实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}