---
category: general
date: 2026-01-12
description: 学习如何在 Python 中对 PDF 进行 OCR，并快速使 PDF 可搜索。使用 Aspose OCR 将扫描的 PDF 转换、提取文本
  PDF，并对扫描的 PDF 进行 OCR。
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: zh
og_description: 如何在 Python 中对 PDF 进行 OCR？本分步教程展示了如何使用 Aspose OCR 将扫描的 PDF 文件转换为可搜索的
  PDF 并提取文本。
og_title: 如何对 PDF 进行 OCR 并使其可搜索 – Python 指南
tags:
- OCR
- Python
- PDF processing
title: 如何对 PDF 进行 OCR 并使其可搜索 – Python 指南
url: /zh/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何 OCR PDF 并使其可搜索 – Python 指南

是否曾想过 **如何 OCR PDF** 文件而不必在商业软件上花大价钱？你并不孤单。许多开发者在需要将扫描的合同、发票或任何基于图像的 PDF 转换为可搜索文档时会遇到瓶颈。好消息是？只需几行 Python 代码和 Aspose OCR，即可在几分钟内将扫描的 PDF 转换、提取文本 PDF，并最终使 PDF 可搜索。

在本教程中，我们将逐步演示所有必需的内容：从安装库、配置语言、处理扫描的 PDF，到将结果保存为包含原始图像和隐藏文本层的可搜索 PDF。完成后，你将拥有一个可在任何项目中直接使用的可复用脚本——无需手动复制粘贴。

---

## 您需要的条件

- **Python 3.8+**（代码在 3.9、3.10 及更高版本均可运行）
- 有效的 **Aspose OCR for Python** 许可证（免费试用版可用于实验）
- 一个扫描的 PDF 文件（例如 `scanned_contract.pdf`），你希望将其设为可搜索
- 对命令行和虚拟环境有基本了解（可选，但推荐）

> **专业提示：** 如果你还没有许可证，请在 Aspose 网站注册 30 天试用；试用版在开发阶段功能完整。

## 使用 Aspose OCR 进行 PDF OCR（H2 主关键字）

第一步是获取正确的包。Aspose OCR 提供了一个简洁的高级 API，抽象掉了底层图像处理细节。

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

安装完包后，你就可以开始编写脚本了。

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **为什么要设置语言？**  
> OCR 的准确性在很大程度上取决于语言模型。明确告诉引擎期望英文文本，可减少误报并加快处理速度。

## 步骤 2：将扫描的 PDF 转换为可搜索的 PDF

现在引擎已准备就绪，指向你的扫描文档即可。`process_pdf` 方法返回一个 `PdfResult` 对象，包含原始图像数据和识别出的文本。

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

如果需要批量 **convert scanned PDF** 文件，只需遍历目录并对每个文件调用 `process_pdf`。引擎开箱即支持多页 PDF。

## 步骤 3：将结果保存为可搜索的 PDF（使 PDF 可搜索）

最后一步是持久化可搜索版本。Aspose OCR 只需一行代码即可完成：

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

当你在任何 PDF 查看器中打开 `contract_searchable.pdf` 时，会看到原始扫描图像，但现在可以 **search for any word**，即 OCR 引擎识别的任何单词。隐藏的文本层对肉眼不可见，却可以完整索引。

### 完整脚本 – 可直接运行

下面是完整、可运行的示例。将其复制粘贴到名为 `make_searchable.py` 的文件中，并根据你的环境调整路径。

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**预期输出：**  
运行脚本会打印确认信息并生成 `contract_searchable.pdf`。打开文件，按 `Ctrl + F`，输入原始扫描图像中出现的任意单词，即可立即看到匹配结果。

## 常见问题与边缘情况

### 1. 如果 PDF 包含多种语言怎么办？

你可以向引擎传递语言列表：

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR 将尝试在同一页面上识别这两种语言的文本。

### 2. 如何处理低分辨率扫描？

如果源图像低于 150 dpi，OCR 准确度可能下降。可使用 `pdfimages` 等工具提取页面，使用 Pillow 将其放大，然后将更高分辨率的图像重新传入 `process_pdf`。

### 3. 能否在不创建可搜索 PDF 的情况下提取纯文本？

完全可以。`PdfResult` 对象公开了 `text` 属性：

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

当你仅需要原始字符时，这满足 **extract text pdf** 的使用场景。

### 4. 是否有办法批量处理文件夹中的 PDF？

可以——将 `ocr_to_searchable` 函数包装在一个简单循环中：

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

现在你可以使用单个命令 **convert scanned pdf** 文件批量处理。

## 性能技巧

- **Reuse the engine**：为每个文件创建新的 `OcrEngine` 会增加开销。实例化一次并在多次调用中复用。
- **Parallel processing**：对于大批量处理，可考虑 Python 的 `concurrent.futures.ThreadPoolExecutor`——Aspose OCR 对只读操作是线程安全的。
- **Memory management**：如果处理的是非常大的 PDF（数百页），在每个文件处理完后调用 `gc.collect()` 以释放内存。

## 结论

我们已经介绍了在 Python 中 **how to OCR PDF** 的完整流程，将扫描件转换为 **searchable PDFs**，并展示了如何直接 **extract text PDF**。使用 Aspose OCR，你将获得一个可靠的引擎，能够处理多页文档、多语言以及高精度识别——只需几行代码。

尝试在自己的合同、发票或归档的研究论文上运行它吧。掌握基础后，可进一步探索高级功能——如自定义词典、图像预处理，或将输出集成到 Elasticsearch 等全文检索索引中。

对 **ocr scanned pdf python** 有更多疑问或需要帮助排查棘手的扫描文件？在下方留言，祝编码愉快！

--- 

![如何 OCR PDF 示例](image-placeholder.png){alt="如何 OCR PDF 示例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}