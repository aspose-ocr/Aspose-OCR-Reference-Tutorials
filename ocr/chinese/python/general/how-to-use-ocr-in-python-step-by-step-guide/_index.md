---
category: general
date: 2026-08-12
description: 如何在 Python 中使用 OCR 识别图像中的文本，提取文本，将图像转换为文本，并使用 AI 后处理清理 OCR 文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: zh
lastmod: 2026-08-12
og_description: 如何在 Python 中使用 OCR 将图片转换为可编辑文本。学习从图像中识别文本、提取文本、将图像转换为文本，并使用 AI 清理
  OCR 文本。
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: 如何在 Python 中使用 OCR – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: 如何在 Python 中使用 OCR – 步骤指南
url: /zh/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 OCR – 步骤指南

如果你需要 **how to use OCR** 将扫描文档或截图转换为可编辑文本，本教程提供了完整的 Python 解决方案。你将学习如何从图像中识别文本、提取文本、将图像转换为文本，并使用轻量级 AI 后处理器清理 OCR 文本。

本指南涵盖了从安装所需库到处理低质量图像的全部内容，让你能够在任何自动化流水线中集成 OCR，而无需猜测缺少了哪一步。

## 你将构建的内容

阅读完本文后，你将拥有一个单独的 Python 脚本，能够：

1. 加载图像文件（PNG、JPEG 或 TIFF）。  
2. 使用 OCR 引擎识别图像中的文本。  
3. 使用 AI 驱动的后处理器改进原始输出。  
4. 将清理后的文本打印到控制台。

无需外部服务——所有操作均在本地运行，适用于离线环境或对隐私要求高的项目。

## 前置条件

- Python 3.9 或更高版本。  
- `pytesseract` 与 `Pillow` 库（`pip install pytesseract pillow`）。  
- 已安装 Tesseract‑OCR 二进制文件，并已将其加入系统 `PATH`。  
- 对 Python 中函数的基本了解。  

如果你已经具备上述条件，可以直接跳到第一个代码块。

## 如何在 Python 中使用 OCR

**how to use OCR** 的核心是初始化 OCR 引擎并向其提供图像。本教程使用 `pytesseract`，它是开源 Tesseract 引擎的轻量包装。

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **为什么这一步重要** – Tesseract 需要干净、方向正确的图像。使用 Pillow 可以在 OCR 运行前对图像数据进行标准化，从而提升后续 **recognize text from image** 操作的准确性。

## Recognize text from image

现在我们调用 `pytesseract.image_to_string` 来提取原始字符串。这就是经典的 “recognize text from image” 调用。

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **为什么要把函数单独拆分** – 将 OCR 步骤隔离后，你可以在以后轻松切换引擎（例如改用 EasyOCR），而无需修改流水线的其他部分。同时也便于单元测试。

## Extract text from image and improve quality

原始 OCR 输出常常包含换行符、杂散字符或误识别的单词。AI 后处理器可以自动清理这些伪影。下面是一个使用 `transformers` 库在本地运行小型语言模型的最小示例。如果你愿意，也可以替换为任何专有服务。

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **为什么 AI 后处理器有帮助** – 传统 OCR 引擎擅长字符识别，但在布局和噪声处理上表现不足。语言模型能够理解上下文，从而把 “Th1s 1s 4 test.” 转换为 “This is a test.” 这一步直接满足 **clean up OCR text** 的需求。

## Convert image to text – full script

将所有内容组合起来，就得到一个 **convert image to text** 的端到端短脚本。

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### 预期输出

使用示例图像（`sample.png`）运行脚本可能得到：

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

可以看到 AI 后处理器纠正了误读字符并去除了多余的换行。这展示了完整的 **extract text from image** 工作流，并体现了清理 OCR 文本的优势。

## 处理常见边缘情况

| 情况                                   | 推荐的调整方案                                                                   |
|----------------------------------------|---------------------------------------------------------------------------------|
| 低对比度图像                           | 在 OCR 前使用 `ImageEnhance` 将图像转换为灰度并提升对比度。                     |
| 多语言文档                             | 将逗号分隔的语言列表传递给 `lang`（例如 `lang='eng+fra'`）。                    |
| 超大图像（> 2000 px）                  | 使用 `img.thumbnail((2000, 2000))` 降采样，以加快 Tesseract 处理速度。          |
| 缺少 Tesseract 二进制文件               | 确认 `pytesseract.pytesseract.tesseract_cmd` 指向可执行文件的正确路径。        |
| AI 后处理器运行缓慢                     | 使用更小的模型（如 `t5-small`）或在 GPU 上运行后处理器。                      |

> **专业提示**：如示例所示，在模块导入时缓存 AI 模型对象（`_ai_postprocessor`），可避免每次调用都重新加载模型，从而在处理大量图像时显著降低延迟。

## 替代方案

- **EasyOCR**：纯 Python OCR 库，支持 80 多种语言，无需外部二进制文件。如果你更倾向于仅使用 pip 安装的方案，可将 `ocr_recognize` 替换为 `EasyOCR.Reader`。  
- **云 OCR API**：Google Cloud Vision、Azure Computer Vision 或 Amazon Textract 在处理复杂布局时精度更高，但需要网络访问并产生费用。  
- **自定义后处理**：若需确定性的清理，可使用正则表达式（`re.sub`）修复常见模式（例如去除连字符换行），无需 AI 模型。

## 总结

现在你已经掌握了 **how to use OCR** 在 Python 中实现 **recognize text from image**、**extract text from image**、**convert image to text**，并使用 AI 后处理器 **clean up OCR text**。完整脚本展示了可投入生产的流水线，你可以在此基础上添加更多预处理（降噪、去倾斜）或下游操作（保存到数据库、写入搜索索引）。

### 后续步骤

- 尝试不同的 AI 模型（如 `gpt‑2`、`flan‑ul2`），找出最适合你领域的清理效果。  
- 使用 Flask 或 FastAPI 将流水线集成到 Web 服务中，打造按需 OCR 接口。  
- 探索批量处理：遍历图像目录，将每个清理后的输出写入对应的 `.txt` 文件。

欢迎根据你的具体工作流调整代码，让干净、可搜索的文本为你的应用下一阶段提供动力。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}