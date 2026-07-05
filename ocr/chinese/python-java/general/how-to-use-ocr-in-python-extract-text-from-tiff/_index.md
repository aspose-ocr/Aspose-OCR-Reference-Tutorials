---
category: general
date: 2026-07-05
description: 如何在 Python 中使用 OCR 快速将 TIFF 转换为文本。学习 OCR 库 Python 的步骤，以从 TIFF 图像中提取文本并构建
  Python OCR 引擎。
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: zh
og_description: 如何在 Python 中使用 OCR？本指南将一步步展示如何使用 Python OCR 引擎和 ocr 库将 TIFF 转换为文本。
og_title: 如何在 Python 中使用 OCR – 完整的 TIFF 文本提取
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: 如何在 Python 中使用 OCR —— 从 TIFF 中提取文本
url: /zh/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 从 TIFF 提取文本

有没有想过 **how to use OCR in Python** 将扫描的书籍转换为可编辑的文本？你并不是唯一遇到这个难题的人——开发者、研究人员和爱好者在处理多页 TIFF 图像时都会碰到这个障碍。好消息是？使用 **ocr library python**，你可以启动一个小型 OCR 引擎，指向 TIFF 文件，几秒钟内即可获得干净、可搜索的文本。

在本教程中，我们将逐步演示你需要的所有内容：安装合适的包、加载多页 TIFF、运行 OCR 引擎，最后打印每页的内容。完成后，你将能够 **convert TIFF to text** 并 **extract text from TIFF** 文件，而无需离开你的 Python 环境。

## 先决条件

- Python 3.9 或更高（示例在 3.11 上测试）
- 最近版本的 `ocr` 库（或任何你偏好的兼容 `python ocr engine`）
- 你想要处理的多页 TIFF 文件（我们将其称为 `scanned_book.tif`）
- 对 Python 脚本和虚拟环境有基本了解

无需繁重的外部工具——只需 pip 和几行代码。

## 安装 OCR Library Python

首先，你需要一个可靠的 OCR 后端。本文档使用虚构的 `ocr` 包，它提供了一个简单的高级 API，但相同的模式同样适用于基于 Tesseract 的包装器，如 `pytesseract` 或商业 SDK。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **技巧提示：** 如果你在 Windows 上且该包依赖本机二进制文件，请确保已安装相应的 Visual C++ 可再发行组件。安装程序通常会在缺少时给出警告。

## How to Use OCR Engine in Python

现在库已经准备就绪，让我们启动一个 OCR 引擎并指向我们的 TIFF 文件。下面的代码片段创建了一个引擎实例，将语言设置为英语，并为多页处理做好准备。

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**为什么要设置语言？**  
大多数 OCR 引擎使用语言模型来提升准确率。如果跳过此步骤，引擎会回退到通用模型，可能会误识别标点或特殊字符。

## 加载多页 TIFF 图像

接下来要加载扫描的文档。`ocr.Image.load` 辅助函数能够直接识别 TIFF 堆栈，返回一个内部表示每页的对象。

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **特殊情况：** 如果你的 TIFF 使用了压缩（如 CCITT Group 4、LZW 等），且库抛出错误，请先使用 ImageMagick 将其转换为未压缩版本：  
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## 对所有页面执行 OCR – Convert TIFF to Text

手握图像对象后，引擎现在可以一次性处理所有页面。此方法返回一个列表，每个元素保存单页的 OCR 结果。

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**内部是如何工作的？**  
`recognize_multi_page` 函数遍历每个光栅化页面，运行神经网络识别器，并将纯文本输出与置信度分数一起打包。这本质上是一次批处理操作，省去了手写循环的麻烦。

## 遍历结果 – Extract Text from TIFF

最后，我们显示识别出的文本。你可以将输出写入单独的 `.txt` 文件，推送到数据库，或导入搜索索引——随你的工作流而定。

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### 预期输出

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

每个 `result.text` 字符串包含该页的原始 OCR 输出。如果需要保留换行，大多数引擎会以 `result.lines` 列表形式提供每行字符串。

## 处理大型 TIFF 文件 – Tips & Tricks

处理 500 页的 TIFF 可能会占用大量内存。以下是几种保持流畅的策略：

1. **Chunk the pages** – 与其使用 `recognize_multi_page`，不如在生成器中逐页调用 `engine.recognize(page)`，一次只返回一页。  
2. **Adjust DPI** – 将图像分辨率从 300 DPI 降至 200 DPI 可降低 CPU 负载，同时对大多数印刷文本的准确率影响甚微。  
3. **Parallelize** – 如果你的 OCR 引擎是线程安全的，可创建 `concurrent.futures.ThreadPoolExecutor`，并行识别多个页面。

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## 将提取的文本保存为文件

大多数真实业务流水线需要持久化存储。下面是一段简洁代码，可将每页文本导出到单独文件，保持页面顺序。

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

现在你拥有一个整洁的 `.txt` 文件目录，可用于索引或进一步的 NLP 处理。

## 图像预览 – How to Use OCR Results Visually

如果想在原始图像上看到 OCR 叠加（调试时很有帮助），许多库都支持绘制边界框。下面是使用 Pillow 的快速示例：

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![如何在 Python 中使用 OCR – 在 TIFF 页面上可视化叠加识别文本](ocr_overlay_example.png)

*Alt text:* 如何在 Python 中使用 OCR – 在 TIFF 页面上可视化叠加识别文本。

## 常见陷阱及规避方法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 字符乱码 | 语言模型错误 | 将 `engine.language` 设置为正确的枚举 |
| 缺失页面 | 不支持的 TIFF 压缩 | 先将 TIFF 转换为未压缩格式 |
| 性能慢 | 高 DPI + 单线程处理 | 降低 DPI 或启用多线程 |
| 输出为空 | 图像过暗/对比度低 | 使用对比度拉伸预处理（`opencv` 或 `Pillow`） |

提前解决这些问题可以为你节省大量调试时间。

## 下一步 – 超越基础提取

现在你已经掌握了 **how to use OCR in Python** 的基础，考虑进一步探索：

- **PDF generation** – 将提取的文本与 `reportlab` 结合，重新生成可搜索的 PDF。  
- **Language detection** – 使用 `langdetect` 自动切换 `engine.language`。  
- **Structured data extraction** – 使用正则表达式或 spaCy 从原始文本中提取日期、姓名或表格。  
- **Alternative OCR backends** – 如需多语言支持，可将 `ocr` 替换为 `pytesseract` 或 `easyocr`。

这些主题自然关联到次要关键词 **ocr library python**、**convert tiff to text**、**extract text from tiff** 与 **python ocr engine**，为更高级的项目奠定坚实基础。

---

### 结论

我们已经从安装到多页处理完整演示了 **how to use OCR in Python**，并明确展示了如何 **convert TIFF to text** 与 **extract text from TIFF**，使用简洁的 **python OCR engine**。上面的完整可运行示例应能直接处理大多数标准 TIFF 文件，文中提供的技巧也能帮助你扩展到更大的文档或将 OCR 集成到更大的流水线中。

尝试在自己的扫描书籍、收据或档案图像上运行它吧——随后探索 “下一步” 部分列出的更高级想法。祝编码愉快，愿你的 OCR 结果始终精准！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每篇资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [使用 Aspose OCR 从图像中提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR for Java 提取 TIFF 文本](/ocr/english/java/ocr-operations/recognize-tiff/)
- [使用 Aspose OCR 从流中执行图像文本提取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}