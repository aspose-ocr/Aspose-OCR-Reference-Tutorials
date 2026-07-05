---
category: general
date: 2026-07-05
description: 使用 Python 创建可搜索的 PDF。学习如何对扫描的 PNG 进行 OCR，转换扫描的图像 PDF，并在几分钟内生成可搜索的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: zh
og_description: 快速创建可搜索的 PDF。本指南展示如何对 PNG 进行 OCR、转换扫描的图像 PDF，并使用 Python 生成可搜索的 PDF。
og_title: 从扫描图像创建可搜索的 PDF – Python OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: 从扫描图像创建可搜索的 PDF – 完整的 Python OCR 指南
url: /zh/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从扫描图像创建可搜索 PDF – 完整 Python OCR 指南

是否曾想过 **从扫描图片创建可搜索 PDF** 而不必购买昂贵的软件？你并不孤单。在许多办公室，PDF 只是一张平面图像——难以搜索，无法复制粘贴，合规审计时更是噩梦。好消息是，只需几行 Python 代码，就能把静态 PNG 转换为完整的可搜索 PDF，过程比想象中更简单。

在本教程中，我们将完整演示一个 **OCR 识别示例**，涵盖从安装合适的库到写入最终 PDF 文件的全部步骤。完成后，你将清楚如何 **转换扫描图像 PDF**，如何以编程方式 **how to ocr pdf**，并拥有一个可在任何项目中直接使用的脚本。

## 你将学到

- 安装并配置 Python OCR 库（我们使用 `pytesseract` 和 `pdf2image`）。
- 初始化 OCR 引擎并设置语言。
- 加载扫描的 PNG（或任意图像）并运行 OCR。
- 将 OCR 结果转换为 **可搜索 PDF**（字节数组）并保存。
- 处理多页文档、不同语言以及常见陷阱的技巧。

不需要任何 OCR 经验——只要有可用的 Python 3 环境和一点好奇心即可。

---

## 创建可搜索 PDF – 概览

下面是我们将实现的步骤的高级流程图。  

![创建可搜索 PDF 工作流图](https://example.com/flowchart.png "创建可搜索 PDF 工作流图")

*Alt text: 创建可搜索 PDF 工作流图，展示引擎初始化、图像加载、OCR 识别、PDF 转换以及文件写入。*

---

## 步骤 1：初始化 OCR 引擎（how to ocr pdf）

为什么必须先初始化？OCR 引擎是将像素模式解释为字符的大脑。通过创建引擎实例并显式设置语言，我们告诉库期待哪种字母表，从而显著提升准确率。

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**专业提示：** 如果需要对多语言文档进行 OCR，请为 Tesseract 安装相应的语言包，并将类似 `"eng+spa"` 的列表传递给 `ocr_language`。

---

## 步骤 2：加载扫描图像（convert scanned image pdf）

接下来要把图像数据导入 Python。无论是单个 PNG 还是多页 TIFF，`PIL.Image` 类都能打开它。如果你是从已经包含扫描图像的 PDF 开始，`pdf2image` 会把每页转换为图像供我们使用。

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**为何重要：** 将图像加载为 Pillow 对象后，我们即可访问其原始像素数据，这是 OCR 引擎所必需的。直接使用原始字节会导致错误。

---

## 步骤 3：对图像执行 OCR 识别（ocr recognition example）

现在是有趣的部分——让引擎读取文本。`pytesseract.image_to_pdf_or_hocr` 返回一个已经包含不可见文本层的 PDF 字节流，这正是我们需要的 **可搜索 PDF**。

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**边缘情况：** 如果图像对比度低，考虑在 OCR 前先做简单的阈值处理：

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

这一步微小的预处理可以显著提升准确率。

---

## 步骤 4：将 PDF 字节写入文件（convert png searchable pdf）

OCR 库给我们的是一个字节数组——可以把它看作 PDF 文件的原始内容。现在只需把这些字节写入磁盘即可。

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**你会看到：** 在任意 PDF 阅读器中打开生成的文件，搜索原始图像中已知出现的词汇。高亮应直接跳到对应位置，证明不可见文本层已生效。

---

## 步骤 5：扩展到多页文档（convert scanned image pdf）

实际合同常常跨多页。要 **convert scanned image pdf** 包含多页的文件，只需遍历每页，进行 OCR，然后将生成的 PDF 合并。

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**为何要合并？** 每次调用 `image_to_pdf_or_hocr` 都会生成一个独立的 PDF。合并它们可确保最终文档保持原始页序。

---

## 常见陷阱及解决方案

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 打开 PDF 后无法搜索文本 | Tesseract 未识别到字符（输出为空） | 检查图像质量，提升 DPI，或进行预处理（对比度、二值化）。 |
| 出现乱码字符（如 �） | 语言包错误或缺少字体 | 安装正确的语言数据（`tesseract‑lang‑eng`），并确保 `ocr_language` 匹配。 |
| PDF 文件体积巨大（>10 MB 单页图像） | 使用无损 PNG 作为源；OCR 添加了全分辨率图像 | 在 OCR 前缩小图像 (`image.thumbnail((1240, 1754))` 适用于 A4)。 |
| 脚本在 Windows 上报 “tesseract.exe not found” | Tesseract 可执行文件未在 PATH 中 | 添加 `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"`（根据实际路径调整）。 |

---

## 完整、可直接运行的脚本

将所有内容整合后，下面是一个可以复制粘贴并直接运行的单文件脚本：

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

将其保存为 `create_searchable_pdf.py`，将占位符替换为真实路径，然后运行：

```bash
python create_searchable_pdf.py
```

你应该会看到


## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步使用 API 功能或探索替代实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}