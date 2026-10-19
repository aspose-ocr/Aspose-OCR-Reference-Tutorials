---
category: general
date: 2026-06-25
description: 在 Python 中初始化 OCR 引擎，以使用自定义词典、语言设置和区域定位从多页 PDF 中提取文本。
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: zh
og_description: 在 Python 中初始化 OCR 引擎，以可靠地读取越南语 PDF，配置语言、预处理和自定义词典，确保结果准确。
og_title: 初始化 OCR 引擎 – 步骤式 PDF 提取指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: 初始化 OCR 引擎——PDF 文本提取完整指南
url: /zh/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 初始化 OCR 引擎 – PDF 文本提取完整指南

是否曾经需要为一批越南发票 **初始化 OCR 引擎**，却不知从何入手？你并不孤单。在许多真实项目中，第一道难关就是让 OCR 库能够读取你的 PDF，尤其是当你需要调整语言、预处理或自定义词典时。

在本指南中，我们将通过一个完整、可运行的示例，演示如何 **初始化 OCR 引擎**、配置语言、启用智能图像预处理、添加自定义词典，最后从多页 PDF 的每一页中提取结构化数据。阅读完毕后，你将拥有一个可以直接放入自己项目的独立脚本——没有缺失的部分，也没有“请参阅文档”的捷径。

## 你将学到

- 如何 **初始化 OCR 引擎** 并支持越南语。  
- 为什么 **配置 OCR 语言** 对准确性至关重要。  
- 使用 **OCR 图像预处理** 选项，如自动去倾斜和自动二值化。  
- 添加 **OCR 自定义词典** 以提升领域专用术语的识别率。  
- **识别多页 PDF** 并提取特定区域（例如总金额）。  
- 将原始结果转化为干净的 JSON‑like 结构，以便后续处理。

### 前置条件

- 已安装 Python 3.8+。  
- 一个提供 `OcrEngine` 类的 OCR 库（示例使用假想的 `ocr` 包；请替换为实际的 SDK）。  
- 将示例多页 PDF（`sample.pdf`）放置在已知目录下。  
- 对 Python 字典和循环有基本了解。

如果你满足以上条件，下面开始吧。

---

## 步骤 1：如何在 Python 中初始化 OCR 引擎

首先必须 **初始化 OCR 引擎**。可以把它想象成打开机器并告诉它将要处理的语言。

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **为什么这很重要：**  
> 大多数 OCR 引擎默认提供通用语言包。通过显式设置 `ocr_engine.language`，可以避免引擎误判字符，从而显著降低越南语中常见变音符号的识别错误。

### 小技巧
如果需要在同一次运行中支持多种语言，可以在处理每页前动态切换 `ocr_engine.language`。只需记得在 SDK 要求的情况下重新加载重量级模型。

---

## 步骤 2：启用 OCR 图像预处理选项

原始扫描件很少完美。页面倾斜、光照不均或对比度低都会让即使是最好的识别器也束手无策。因此在初始化后立即 **配置 OCR 图像预处理**。

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

这两个标志通常足以清理大多数扫描发票。如果你的源 PDF 已经是高质量的，可以关闭它们，以节省每页几毫秒的处理时间。

---

## 步骤 3：添加 OCR 自定义词典

领域专用术语——如订单码、产品 ID 或法律缩写——在通用语言模型中很少出现。通过提供 **OCR 自定义词典**，相当于给引擎一张速查表。

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **底层原理是什么？**  
> 引擎会提升与词典中条目匹配的单词的置信度分数，使其不太可能被误读为其他内容。

---

## 步骤 4：识别多页 PDF – 一次性获取全部文本

引擎配置完成后，我们可以 **识别多页 PDF**。`recognize_multi_page` 方法返回一个列表，每个元素对应一页，已完成 OCR 处理。

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

如果要处理巨大的 PDF（数百页），建议分块处理，以降低内存占用。大多数 SDK 都提供流式 API 来满足此类需求。

---

## 步骤 5：从每页提取特定区域

大多数发票的 “Total Amount” 字段在每页的固定位置。与其解析整页文本，不如让引擎只关注一个矩形区域。

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **为什么要定位区域？**  
> 将 OCR 限制在小范围内可以加快处理速度，并降低误报，尤其是当页面其余部分噪声较多时。

---

## 步骤 6：为每页组装 JSON‑Like 字典

拥有原始文本固然好，但下游系统通常需要结构化数据。下面我们构建一个整洁的字典，包含页码、完整页文本、提取的总额以及所有识别词及其置信度。

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

运行脚本后会输出一系列字典——每页一个——形如：

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

你可以轻松地将输出重定向到文件（`> results.jsonl`），以便后续批处理。

---

## 完整可运行示例

将所有代码组合在一起，下面是可以直接复制粘贴运行的完整脚本：

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### 预期输出

对一个三页发票 PDF 运行脚本可能得到：

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

可以将结果通过 `jq` 或任意 JSON 解析器进行检查。

---

## 常见问题与边缘情况

| 问题 | 解答 |
|----------|--------|
| **如果我的 PDF 有密码保护怎么办？** | 大多数 SDK 允许在 `recognize_multi_page` 中传入 `password` 参数。只需在调用时添加 `password="mySecret"` 即可。 |
| **我的扫描是灰度而不是黑白的。** | `auto_binarize` 选项会处理这种情况，当然也可以在将图像传给 `recognize_region` 前使用 `Pillow` 手动转换。 |
| **总金额有时出现在不同的坐标。** | 可以动态计算矩形（例如通过模板匹配），或先进行整页 OCR，再使用正则 `r'\d{1,3}(,\d{3})* VND'` 在文本中搜索。 |
| **在 500 页 PDF 上性能很慢。** | 批量处理页面：一次处理 50 页，写入结果后清空 `pages` 列表以释放内存。如果扫描已经是正的，可关闭 `auto_deskew`。 |
| **以后想支持其他语言怎么办？** | 在调用 `recognize_multi_page` 前只需更改 `ocr_engine.language = ocr.Language.English`（或任意受支持的枚举），其余流程保持不变。 |

---

## 生产环境部署技巧

1. **错误处理** – 将 OCR 调用包装在 `try/except` 中；在失败时记录页索引，以便后续重试。  
2. **日志记录** – 使用 Python 的 `logging` 模块代替 `print`，以实现灵活的日志级别控制。  
3. **并行化** – 若 OCR 库是线程安全的，可使用 `ThreadPoolExecutor` 并发处理页面。  
4. **配置文件** – 将语言、词典和矩形坐标存入 JSON/YAML 配置文件，提升脚本在不同项目间的复用性。  
5. **测试** – 编写包含已知 PDF 的小型测试套件，断言提取的 `total_amount` 与预期值相符。  

---

## 结论

你已经学会了 **

## 接下来该学习什么？

以下教程与本指南紧密相关，进一步扩展所示技术。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}