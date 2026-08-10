---
category: general
date: 2026-06-19
description: 如何使用 OCR 在 Python 中提取 PDF – 步骤详解教程，涵盖从 PDF 提取文本、从图像识别文本以及 OCR Python
  示例。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: zh
og_description: 如何使用 Python 通过 OCR 提取 PDF。学习从 PDF 中提取文本、从图像中识别文本，并查看完整的 OCR Python
  示例。
og_title: 如何使用 Python OCR 提取 PDF 文本 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: 如何在 Python 中使用 OCR 提取 PDF 文本——完整指南
url: /zh/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR 在 Python 中提取 PDF 文本 – 完整指南

是否曾想过 **如何提取 PDF** 内容，而文件仅是扫描的图像？你并不孤单。在许多真实项目中——比如合同、发票或历史档案——收到的 PDF 没有可选取的文本。好消息是，只需几行 Python 代码，就能将这些仅图像的页面转换为可搜索、可编辑的文本。

在本教程中，我们将通过一个实用的 **OCR Python 示例**，演示如何读取 PDF、将其首页渲染为图像，然后使用 OCR 引擎 **从 PDF 中提取文本**。完成后，你将清楚地了解 **如何使用 OCR 读取 PDF**、每一步的意义，以及如何将代码扩展到多页文档或不同语言。

## 您将学习的内容

- 为 Python 安装并配置可靠的 OCR 库。  
- 将 PDF 页面转换为适合 OCR 的图像。  
- **从图像识别文本** 并获取干净的 Unicode 字符串。  
- 常见陷阱（低分辨率 PDF、页面旋转）及其规避方法。  
- 扩展脚本以处理多页或批量处理。

**前置条件**：Python 3.8+、pip，以及对虚拟环境的基本了解。无需任何 OCR 经验——只需跟随操作即可。

---

## ## 使用 OCR 在 Python 中提取 PDF 文本

此 H2 标题正好包含我们的主要关键词，符合搜索引擎的喜好。让我们直接进入代码。

### Step 1 – Install the Required Packages

首先，我们需要一个 OCR 引擎。下面的示例使用流行的 **ocr** 包（Tesseract 的轻量封装）。如果你更倾向于其他后端，概念保持不变。

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **专业提示：** 在 Linux 上，你还需要安装 Tesseract 二进制文件：`sudo apt-get install tesseract-ocr`。macOS 用户可以通过 Homebrew 安装：`brew install tesseract`。

### Step 2 – Initialize the OCR Engine and Set Language

现在我们启动引擎并指定使用英文字符。你可以将 `ocr.Language.English` 替换为任意受支持的语言代码。

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**为什么重要：** 指定语言可以显著提升准确率，因为引擎能够使用语言特定的词典和字符模型。

### Step 3 – Load a PDF Page as an Image

OCR 只能处理光栅图像，而不是 PDF 对象。`ocr.Image.from_pdf` 辅助函数会将指定页面渲染为位图。通过修改 `page_number` 可选择其他页面（从 0 开始计数）。

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **特殊情况：** 如果 PDF 包含矢量图形而非扫描图像，你可能会得到清晰的渲染。对于低分辨率扫描，建议提升 DPI：`ocr.Image.from_pdf(..., dpi=300)`。

### Step 4 – Recognize Text from the Rendered Image

下面是 **ocr python 示例** 的核心。引擎处理位图并返回包含提取字符串的对象。

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

`ocr_result.text` 属性保存纯文本输出，并在可能的情况下保留换行。

### Step 5 – Print or Store the Extracted Text

最后，我们输出结果。在实际应用中，你可能会将其写入文件或数据库。

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

运行脚本后应显示类似如下内容：

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

这就是使用 OCR 完整的 **从 PDF 提取文本** 工作流。

---

## ## 从图像识别文本 – 调整准确度

如果你只关心 **从图像识别文本**（例如收据的 JPEG），可以跳过 PDF 转换步骤：

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**提升效果的技巧：**

- **预处理** 图像：转换为灰度、应用阈值或去倾斜。Pillow 可以轻松完成。  
- **提升 DPI**：在 PDF 渲染时使用更高分辨率，可为 OCR 引擎提供更多细节。  
- **启用 OCR 引擎的页面分割配置**（`ocr_engine.config = "--psm 6"` 用于均匀块）。

## ## 使用 OCR 读取 PDF – 处理多页

大多数合同都有多页。遍历每一页非常简单：

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

此函数 **使用 OCR 读取 PDF**，将输出拼接，并插入明确的分页标记。随后你可以将 `full_text` 导入搜索索引或保存为 `.txt` 文件。

## ## 常见问题及解决方案

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 字符乱码，出现大量 `?` | 语言设置错误或缺少语言数据文件 | 安装正确的 Tesseract 语言包（`tesseract-ocr-<lang>`）并设置 `ocr_engine.language`。 |
| 行缺失或单词截断 | DPI 过低（低于 150） | 将 PDF 渲染为 300 DPI 或更高（`dpi=300`）。 |
| 文本旋转或倒置 | 扫描页未正向放置 | 在识别前使用 `ocr.Image.deskew(page_image)` 进行去倾斜。 |
| 大型 PDF 处理缓慢 | 单线程顺序处理页面 | 使用 `concurrent.futures.ThreadPoolExecutor` 并行化。 |

## ## 扩展 OCR Python 示例

- **导出为 PDF/A**：提取后，可使用 `reportlab` 或 `pypdf2` 将文本嵌入可搜索的 PDF。  
- **语言检测**：利用 `langdetect` 对 OCR 输出进行检测，动态切换 `ocr_engine.language`。  
- **批量处理**：使用 `os.listdir` 遍历目录，对每个文件调用 `extract_all_pages`。

## ## 预期输出与验证

对清晰的英文扫描件运行脚本时，应看到带有正确标点的整洁文本块。验证方法：

1. 将几行文本与原始扫描图像对比。  
2. 运行简单的词数统计（`len(ocr_result.text.split())`），确保输出非空。  
3. 可选：将结果送入 `pyspellchecker` 等拼写检查器，发现 OCR 错误。

## 结论

我们已经介绍了在传统解析失效时 **如何提取 PDF** 内容，演示了完整的 **ocr python 示例**，并说明了如何 **从图像识别文本** 与 **使用 OCR 读取 PDF**，无论是单页还是多页场景。借助上述代码片段，你现在可以将任何扫描 PDF 转换为可搜索、可编辑的文本——再也不需要手动重新输入。

下一步？尝试将语言切换为西班牙语（`ocr.Language.Spanish`），或实验图像预处理技术以提升准确度。如果你在构建文档管理系统，考虑使用 Elasticsearch 对提取的文本进行索引，以实现闪电般的搜索。

有问题或遇到奇怪的 PDF？留下评论，祝编码愉快！  

![使用 OCR 在 Python 中提取 PDF](image.png "使用 OCR 在 Python 中提取 PDF")

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [识别 PDF 文本 – Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [使用 Aspose.OCR 进行语言选择的 C# 图像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}