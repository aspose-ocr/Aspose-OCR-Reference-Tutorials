---
category: general
date: 2026-04-26
description: 如何在扫描的PDF上使用OCR，提取PDF文本，运行PDF的OCR，并在几步内将扫描的PDF转换为可搜索的文件。
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: zh
og_description: 如何在 Python 中使用 OCR：学习如何从 PDF 中提取文本，对 PDF 进行 OCR，以及将扫描的 PDF 转换为可搜索的文档。
og_title: 如何使用 OCR – 提取 PDF 文本的快速指南
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 如何使用 OCR – 用 Python 从 PDF 中提取文本
url: /zh/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR – 使用 Python 从 PDF 中提取文本

是否曾想过 **如何使用 OCR** 从扫描的合同、收据或电子书中提取文本？你并不孤单。在许多实际项目中，你收到的 PDF 仅仅是图像，如果没有 OCR，就无法搜索、索引或分析其内容。  

在本教程中，我们将演示一个完整且可运行的示例，展示 **如何使用 OCR**、**从 PDF 中提取文本** 的方法，以及为何你可能想要 **将扫描的 PDF** 转换为可搜索的文档。我们还会涉及 **将 PDF 加载为图像** 的细微技巧，以便 OCR 引擎能够清晰地看到每一页。

> **快速预览：** 完成后，你将拥有一个脚本，能够加载多页 PDF，对每页运行 OCR，并打印识别出的文本——无需任何外部服务。

## 你需要的环境

- Python 3.9+（任何近期版本均可）
- `aocr` 包（或任何提供 `OcrEngine` 和 `Image.load` 的兼容 OCR 库）
- 要处理的扫描 PDF 文件（例如 `contract.pdf`）
- 适量的内存（每 100 页 PDF 大约 200 MB 通常足够）

如果你还没有安装 OCR 库，请运行：

```bash
pip install aocr
```

> **专业提示：** 使用虚拟环境来保持依赖整洁。

## 第一步：将 PDF 加载为图像 – 拼图的第一块

在进行任何 OCR 之前，必须先将 PDF 表示为图像。这正是次要关键词 **load pdf as image** 发挥作用的地方。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*为何这一步重要：* `aocr.Image.load` 会在内部将每页 PDF 光栅化为位图，供 OCR 引擎识别。如果跳过此步骤直接传入原始 PDF，引擎会报错，因为它期望的是像素数据，而不是矢量数据。

> **注意：** 路径可以是绝对路径或相对路径。确保文件可读，否则会触发 `FileNotFoundError`。

## 第二步：在 PDF 上运行 OCR – 将像素转化为字符

现在 PDF 已经以图像形式存在，我们终于可以 **在 PDF 上运行 OCR**。下面的代码片段一次性处理所有页面：

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*内部到底发生了什么？* `process_all_pages` 会遍历光栅化后的页面，调用 OCR 模型，并返回一个结果对象列表——每页一个。每个结果包含识别的文本、置信度分数以及（如果需要）边界框信息。

## 第三步：从 PDF 中提取文本 – 把字符串拉出来

有了 OCR 结果，提取纯文本变得非常简单。我们将遍历各页并打印输出，以演示次要关键词 **extract text from pdf**。

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**预期输出**（为简洁起见已截断）：

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

如果需要将文本合并为单个字符串，只需连接即可：

```python
full_text = "\n".join(r.text for r in page_results)
```

至此，你已经成功 **使用 OCR 从 PDF 中提取文本**。

## 第四步：转换扫描的 PDF – 让它可搜索

许多下游工具（如 Elasticsearch 或 SharePoint）期望的是可搜索的 PDF，而不是纯文本转储。你可以将 OCR 输出嵌入原始 PDF，从而 **将扫描的 PDF** 转换为可搜索的版本。

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*为何要这样做？* 可搜索的 PDF 保留了原始布局和图像，同时支持文本选择和索引——对人和机器都是双赢。

## 常见陷阱与边缘情况

### 大于内存的多页 PDF

如果你的 PDF 有数百页，一次性加载全部可能会耗尽内存。`aocr` 库支持惰性加载：

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

然后逐页处理：

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### 低质量扫描

模糊或低对比度的扫描会显著降低 OCR 准确率。在将图像送入引擎之前，考虑进行预处理：

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### 语言支持

默认情况下引擎假设文本为英文。若要 **在 PDF 上运行 OCR** 并使用其他语言，请设置语言代码：

```python
ocr_engine.language = "spa"  # Spanish
```

确保已安装相应的语言模型。

## 完整工作示例

将所有内容组合在一起，下面是一个可直接保存为 `ocr_pdf.py` 并立即运行的自包含脚本：

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

运行方式如下：

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

你将在控制台看到打印的文本，如果提供了 `-o` 参数，还会在原文件旁生成一个可搜索的 PDF。

## 专业技巧与最佳实践

- **批量处理：** 在处理数十个 PDF 时，将上述逻辑包装在循环中，并记录每个文件的成功/失败。
- **置信度过滤：** 每个 `page_result` 包含置信度指标。对置信度低的页面进行丢弃或标记，以便人工审查。
- **并行处理：** 如果 CPU 有多个核心，考虑使用 `concurrent.futures` 并行处理页面——但要注意内存使用。
- **版本锁定：** `aocr` API 可能会变化。在 `requirements.txt` 中固定版本（例如 `aocr==2.3.1`），以避免破坏性更改。

## 结论

我们已经完整演示了 **如何使用 OCR** 来 **从 PDF 中提取文本**、**在 PDF 上运行 OCR**、**将 PDF 加载为图像**，以及 **将扫描的 PDF** 转换为可搜索的格式。代码已完整，解释覆盖了 *做什么* 与 *为什么*，现在你拥有了一个可复用的模式，适用于任何基于图像的 PDF 项目。

接下来可以尝试将提取的文本喂入自然语言处理流水线，用 Elasticsearch 索引可搜索的 PDF，或尝试不同的 OCR 后端，如 Tesseract 或 Azure Computer Vision。天地无限，工具尽在指尖。

祝编码愉快，愿你的 PDF 永远可搜索！

![如何使用 OCR 示例](/images/ocr_workflow.png "如何使用 OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}