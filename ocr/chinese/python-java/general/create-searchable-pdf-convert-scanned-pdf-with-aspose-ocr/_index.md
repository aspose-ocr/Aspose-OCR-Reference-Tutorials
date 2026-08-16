---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 将扫描文件创建为可搜索的 PDF。了解如何快速转换扫描 PDF、从 PDF 提取文本以及识别文本 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: zh
og_description: 即时创建可搜索的 PDF。请按照本指南将扫描的 PDF 转换、从 PDF 中提取文本，并使用 Aspose OCR 识别文本 PDF。
og_title: 使用 Aspose OCR 创建可搜索 PDF – 步骤指南
tags:
- OCR
- PDF
- Aspose
- Python
title: 创建可搜索的 PDF – 使用 Aspose OCR 将扫描的 PDF 转换
url: /zh/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建可搜索 PDF – 步骤指南  

是否曾需要从一堆扫描页 **create searchable PDF**，但不确定从何入手？你并不孤单——大多数开发者在第一批扫描文件上传到服务器时都会遇到这个难题。  

好消息是，使用 Aspose OCR，你可以仅用几行代码 **convert scanned pdf**，并且可以 **extract text from pdf** 进行验证，甚至可以实时 **recognize text pdf**。在本教程中，我们将从安装库到保存完整的可搜索文档，完整演示整个过程，并提供一些处理 **convert image pdf** 边缘情况的技巧。  

## 你将实现的目标  

* 将扫描的 PDF（或仅包含图像的 PDF）加载到 Aspose OCR 中。  
* 告诉引擎处理哪些页面——当只需要处理子集时非常方便。  
* 将 OCR 结果嵌入原始文件，使输出成为真正的 **searchable PDF**。  
* 通过打印页数来验证操作，如有需要，还可以导出提取的文本。  

无需外部服务，也没有隐藏的魔法——仅使用纯 Python 和 Aspose 自己的 API。  

## 先决条件  

* Python 3.8 或更高版本。  
* `aspose-ocr` 包 – 使用 `pip install aspose-ocr` 安装。  
* 一个扫描的 PDF 文件（或仅包含图像的 PDF）。  
* 对 Python 脚本有基本了解。  

如果你已经具备上述条件，太好了——让我们开始吧。

<img src="searchable-pdf-workflow.png" alt="创建可搜索 PDF 工作流">  

（OCR 流程图示 – 对代码不是必需的，但有助于视觉学习者。）  

## 步骤 1 – 初始化 OCR 引擎  

首先，你需要一个 `OcrEngine` 实例。可以把它想象成读取每个像素并将其转换为 Unicode 字符的大脑。

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Why this matters:** 没有引擎你无法设置选项或运行识别。提前初始化还能为以后附加自定义词典提供位置。  

## 步骤 2 – 加载源 PDF  

Aspose OCR 可以直接读取 PDF，这意味着你无需自行栅格化每页。只需将引擎指向该文件即可。

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Pro tip:* 如果 PDF 很大，考虑从流中加载，以避免锁定磁盘上的文件。  

## 步骤 3 – 配置 PDF 识别选项  

这里是次要关键字发挥作用的地方。你可以让引擎仅在特定页面 **convert scanned pdf**，嵌入识别的文本，甚至保持原始图像不变。

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Why this matters:**  
* `setEmbedRecognisedText(True)` 是将栅格 PDF 转换为 **searchable PDF** 的关键。  
* `setPageRange` 帮助你有选择地 **convert image pdf**——对只需 OCR 几页的大文档很有用。  
* 启用文本提取后，你以后可以 **extract text from pdf** 而无需打开查看器。  

## 步骤 4 – 将选项附加到引擎  

现在将选项绑定到引擎。此步骤容易被忽视，但如果跳过，引擎将使用默认设置运行（没有可搜索的文本）。

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## 步骤 5 – 对选定页面运行 OCR  

所有配置就绪后，实际的识别只需一次方法调用。

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

如果你正在处理多兆字节的文档，可能需要将其包装在 try/except 块中，以捕获 `OcrException` 并记录出现问题的页面。  

## 步骤 6 – 验证结果  

快速的完整性检查是打印引擎认为已处理的页数。如果需要进行进一步分析，你也可以提取原始文本以 **extract text from pdf**。

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Why you care:** 查看页数可确认 `setPageRange` 已生效，提取的文本片段证明 OCR 实际识别了字符。  

## 步骤 7 – 保存可搜索 PDF  

最后，将输出写回磁盘。`ImageFormats.PDF` 常量告诉 Aspose 将文件保持为 PDF，并加入可搜索的文本。

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

在任意 PDF 阅读器中打开生成的文件并尝试文本搜索——瞧，你已经 **created searchable pdf**！  

## 处理常见边缘情况  

### 当源是 *仅图像* PDF  

如果你的输入 PDF 只包含图像（没有文本层），相同的代码仍然适用——只需确保 `setEmbedRecognisedText(True)` 仍然启用。你可能还想提升 DPI 以获得更高的准确度：

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### 处理多语言  

Aspose OCR 支持语言包。在调用 `recognize()` 之前加载语言：

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### 大文档  

处理 500 页的扫描 PDF 可能会占用大量内存。将任务拆分：

1. 遍历页面范围 (`setPageRange(start, end)`)。  
2. 将每个块保存为临时的可搜索 PDF。  
3. 使用 `PdfMerger`（另一个 Aspose 组件）合并这些块。  

## 完整工作示例（所有步骤合在一起）

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

运行此脚本将生成一个 **searchable PDF**，你可以在 Adobe Reader、Chrome 或任何 PDF 阅读器中打开并立即搜索文字。  

## 结论  

现在，你已经拥有使用 Aspose OCR 创建 **create searchable PDF** 文件的完整端到端解决方案。从加载源文件、配置 **convert scanned pdf** 选项、提取并验证文本，到最终保存可搜索的结果，所有步骤均已涵盖。  

接下来，你可能想探索 **convert image pdf** 场景，即源是打包成 PDF 的一系列 JPEG，或深入研究特定语言的 OCR，以提升多语言文档的准确性。无论如何，模式保持不变：设置选项，运行 `recognize()`，然后保存。  

随意尝试——更改页面范围、调整 DPI，或插入自定义词典。如果遇到问题，欢迎在下方留言或查阅 Aspose 官方文档获取最新 API 细节。祝 OCR 愉快  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}