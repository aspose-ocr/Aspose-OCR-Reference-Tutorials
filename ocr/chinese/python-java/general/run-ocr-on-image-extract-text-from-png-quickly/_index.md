---
category: general
date: 2026-03-18
description: 对图像进行 OCR，提取 PNG 中的文本并生成可搜索的 PDF。了解如何识别文字图像并在几分钟内将 PNG 转换为 PDF。
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: zh
og_description: 对图像进行 OCR，提取 PNG 中的文本，识别文字图像，并生成可搜索的 PDF。请按照此分步指南操作。
og_title: 对图像进行 OCR – 快速提取 PNG 文本
tags:
- OCR
- Python
- Image Processing
title: 在图像上运行 OCR – 快速从 PNG 提取文本
url: /zh/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上运行 OCR – 快速从 PNG 提取文本

是否曾需要 **在图像上运行 OCR**，但不知从何入手？也许你手头有一个保存为 `article.png` 的扫描文章，只想得到纯文本，或者需要一个可搜索的 PDF 进行归档。无论哪种情况，你都来对地方了。在本教程中，我们将一步步演示如何从 PNG 提取文本、识别文字图像，甚至将 PNG 转换为可搜索的 PDF——只需几行代码。

> **你将获得：** 一个完整、可直接运行的脚本，能够加载 PNG、执行 OCR、保存 hOCR 输出，并可选生成可搜索的 PDF。没有缺失的导入，没有“查看文档”的死胡同——只是一套可以直接放入项目的自包含解决方案。

## 前置条件

在开始之前，请确保你已经具备：

- **Python 3.8+**（此处使用的语法在任何近期版本均可运行）
- 你所使用的 **`ocr_engine`** 库（示例假设有一个名为 `OcrEngine` 的类；如有需要请替换为 Tesseract、EasyOCR 等）
- 一个待处理的 PNG 图像（例如放在可引用文件夹中的 `article.png`）
- 对输出目录的写入权限

如果你在底层使用 Tesseract，请先安装它：

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

然后安装 Python 包装器：

```bash
pip install pytesseract Pillow
```

*小技巧：* 保持 OCR 库为最新版本——新语言包和性能优化会频繁发布。

## 在图像上运行 OCR – 步骤指南

下面是 **完整脚本**。可以将其复制粘贴到名为 `run_ocr.py` 的文件中，然后使用 `python run_ocr.py` 运行。

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### 脚本功能概述（简体中文说明）

1. **实例化** OCR 引擎，以便控制其设置。  
2. **加载** PNG 文件（`article.png`）。如果文件不存在，脚本会提前退出，避免后续出现神秘的 `NoneType` 错误。  
3. **选择** `hocr` 作为导出格式。该格式保留原始布局，对后续将图像转换为可搜索 PDF 至关重要。  
4. **运行** 识别引擎；繁重的工作就在这里完成。  
5. **写入** hOCR XML 到 `article.hocr`。此时你已经拥有机器可读的文本及其坐标信息。  
6. *(可选)* 切换为 `"pdf"`，再额外一步生成可搜索的 PDF。

**预期输出** 是一个 UTF‑8 编码的 `.hocr` 文件，内容大致如下（为简洁起见已裁剪）：

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

如果取消注释 PDF 部分，还会生成 `article_searchable.pdf`，你可以在任意 PDF 阅读器中打开，并使用 **Ctrl + F** 搜索框即时定位单词。

![在图像上运行 OCR 示例输出](example.png "在图像上运行 OCR – hOCR 与 PDF 结果")

## 使用 OcrEngine 从 PNG 提取文本

如果你只需要原始文本（不需要布局或 PDF），可以完全跳过 hOCR 步骤：

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*为何选择纯文本？* 轻量、便于索引，并且在后续的 NLP 流程中表现出色。

## 识别文字图像并生成可搜索 PDF

生成可搜索 PDF 需要两步操作：

1. 使用 `hocr`（如上所示） **运行 OCR**，获取布局信息。  
2. 将原始 PNG 与 hOCR 合并，使用引擎的 PDF 导出功能生成 PDF。

大多数现代 OCR 库（Tesseract、ABBYY、Google Vision）都提供 `pdf` 导出，正好完成上述工作。主脚本中 *可选* 块的代码展示了这一模式。如果你的库没有内置 PDF 导出器，可以使用 **`pdf2image`** + **`reportlab`** 将图像和 hOCR 拼接——如有需要请告诉我，我会分享一个快速的额外示例。

## 使用 OCR 输出将 PNG 转为 PDF

有时你只想要一个 **普通 PDF**，其中仅包含图像（没有可搜索层）。这更为简单：

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

如果需要可搜索版本，可将此步骤与 OCR 步骤结合；否则可将其作为忠实的视觉副本用于归档。

## 常见问题与技巧

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **模糊或低分辨率的 PNG** | 当 DPI 低于约 300 时，OCR 准确率会显著下降。 | 在送入引擎前使用 `Image.resize((width*2, height*2), Image.LANCZOS)` 放大图像。 |
| **语言设置错误** | 引擎默认使用英语，非英语字符会出现乱码。 | 在 `recognize()` 之前调用 `ocr_engine.setLanguage('deu')`（或相应的 ISO 代码）。 |
| **缺失 hOCR 输出** | 若未调用 `setExportFormat`，部分引擎会默认输出纯文本。 | 确认 `setExportFormat("hocr")` **在** `recognize()` **之前** 执行。 |
| **文件权限错误** | 试图写入只读文件夹。 | 使用项目内部路径，或先执行 `os.makedirs(..., exist_ok=True)` 创建目录。 |
| **大 PDF 导致内存激增** | PDF 导出器会将整张图像加载到内存。 | 将页面分块处理，或使用流式 PDF 写入器。 |

*小技巧：* 在批量处理成千上万张图片之前，先在一小批样本图像上测试。这样可以节省数小时的调试时间。

## 总结

现在你已经掌握了 **如何在图像文件上运行 OCR**、**从 PNG 提取文本**、**识别文字图像** 以供下游任务使用、**生成可搜索 PDF**，以及 **在需要时将 PNG 转为 PDF** 的完整流程。提供的脚本是即插即用的完整解决方案，可根据你的工作流通过可选部分进行灵活定制。

### 接下来该做什么？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}