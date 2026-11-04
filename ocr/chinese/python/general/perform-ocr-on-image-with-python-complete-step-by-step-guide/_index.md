---
category: general
date: 2026-07-05
description: 使用 Python 对图像进行 OCR。学习如何将图像转换为文本（Python），加载图像进行 OCR，并在几分钟内从图像中提取西里尔文文本。
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: zh
og_description: 在 Python 中对图像进行 OCR。本文指南展示了如何使用 Python 将图像转换为文本，加载图像进行 OCR，并快速提取图像中的西里尔文字。
og_title: 使用 Python 对图像进行 OCR – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: 使用 Python 对图像进行 OCR – 完整的逐步指南
url: /zh/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 对图像执行 OCR – 完整分步指南

是否曾想过如何在不将图像文件交给第三方服务的情况下 **perform OCR on image**？你并不孤单。在许多项目中——护照扫描仪、收据数字化或档案工具——从图片中获取原始文本是第一道难关。  

在本教程中，我们将演示一个实用示例，展示 **converts image to text python** 风格的用法，教你如何 **load image for OCR**，以及最终使用开源 `aocr` 库 **extract Cyrillic text from image**。结束时，你将能够 **recognize Cyrillic text** 于任何图片。

> **你将收获：** 一个可直接运行的脚本、每一步的清晰解释，以及处理常见陷阱（如模糊扫描或意外字体）的技巧。无需外部 API，仅使用纯 Python。

---

## 前置条件

- 已安装 Python 3.8 或更高版本。
- 你熟悉的终端或命令提示符。
- `aocr` 包（可通过 `pip install aocr` 安装）。
- 包含西里尔字符的图像文件（例如，扫描的俄文护照）。  

如果这些听起来陌生，请不要慌——我们将在后续简要覆盖每一点。

---

## 第一步：Perform OCR on Image – 设置环境

我们首先需要一个干净的 Python 环境来容纳 OCR 库。使用虚拟环境可以隔离依赖并防止版本冲突。

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**为什么？**  
专用环境可确保 `aocr` 包及其本机二进制文件不会干扰其他项目。它还能让可复现性变得轻而易举——其他人可以克隆你的仓库并运行相同的 `pip install -r requirements.txt` 命令。

> **专业提示：** 使用 `pip freeze > requirements.txt` 冻结依赖，这样你始终清楚使用了哪些版本。

---

## 第二步：Load Image for OCR – 导入并准备文件

库已准备好后，我们需要 **load image for OCR**。`aocr.Image.from_file` 方法支持大多数常见格式（PNG、JPEG、TIFF）。下面演示如何使用：

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**这段代码在做什么？**  
`aocr.Image.from_file` 读取二进制数据，解码并存入 OCR 引擎可识别的对象。如果文件未找到，Python 会抛出 `FileNotFoundError`，你可以在后续捕获以实现优雅的错误处理。

> **边缘情况：** 某些扫描仪会输出多页 TIFF。在这种情况下，需要先拆分页面——`aocr` 提供了 `Image.from_tiff_pages()` 来实现。

---

## 第三步：Configure the OCR Engine – 强制西里尔文字识别

默认情况下，许多 OCR 引擎会尝试猜测语言，这会导致非拉丁文字出现乱码。为了可靠地 **recognize Cyrillic text**，我们显式将语言设为 “cyrillic”。

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**为什么强制语言？**  
西里尔字符在视觉上与拉丁字母相似（例如 “A” 与 “А”）。让引擎预期西里尔文字可以显著降低误识别，尤其是在低分辨率扫描时。

---

## 第四步：Perform OCR on Image – 运行识别

图像已加载且引擎已调校后，我们终于 **perform OCR on image**。`recognize` 方法返回一个 `OcrResult` 对象，包含提取的文本和置信度分数。

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` 提供了什么？**  
- `text`：识别字符的纯字符串。  
- `confidence`：一个 0‑1 之间的浮点数，表示整体置信度。  
- `lines`：如果需要细粒度控制，则为行对象的列表。

> **常见问题：** *如果文字是倒置的怎么办？*  
> `aocr` 可以自动旋转图像；只需在调用 `recognize` 前设置 `ocr_engine.auto_rotate = True` 即可。

---

## 第五步：Convert Image to Text Python – 后处理输出

原始字符串可能包含多余的空白或换行符。为了 **convert image to text python** 风格，我们将通过几步简单的清理来处理：

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**为什么要这么做？**  
清理后的输出更易于输入下游流水线——无论是存入数据库、喂给翻译 API，还是使用正则搜索护照号码。

---

## 第六步：Extract Cyrillic Text from Image – 综合示例

让我们把所有内容封装成一个可复用函数。这使得 **extract Cyrillic text from image** 在你的项目中只需一行代码即可实现。

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**预期结果（示例）：**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

如果图像清晰且字体与 OCR 模型匹配，你将获得几乎完美的转录。

---

## 故障排查与技巧

| 问题 | 可能原因 | 解决方案 |
|-------|--------------|-----|
| 字符乱码 | 语言设置错误 | 确保 `ocr_engine.language = "cyrillic"` |
| 输出为空 | 图像过暗或分辨率低 | 使用 `opencv` 预处理以提升对比度 |
| 方向错误 | 图像旋转了 90° | 设置 `ocr_engine.auto_rotate = True` |
| 性能慢 | 大图像（>5 MP） | 在识别前使用 `aocr.Image.resize(width=1024)` 调整大小 |

![展示 Python 代码从护照扫描中提取西里尔文字的示例](ocr_example.png "perform OCR on image 示例")

*Alt 文本：“perform OCR on image 示例，展示 Python 代码从护照扫描中提取西里尔文字。”*

---

## 结论

我们刚刚使用纯 Python **performed OCR on image** 文件，学习了如何 **load image for OCR**，强制引擎 **recognize Cyrillic text**，并最终使用整洁的辅助函数 **extract Cyrillic text from image**。整个流水线——从安装 `aocr` 到清理结果——只需几十行代码，可直接嵌入任何需要 **convert image to text python** 风格的项目中。

## 接下来做什么？

- **批量处理：** 遍历扫描文件夹并将结果存入 SQLite。
- **语言检测：** 将 `langdetect` 与 `aocr` 结合，实现西里尔文和拉丁文的自动切换。
- **高级预处理：** 使用 `opencv` 对图像进行去倾斜、去噪或二值化，以提升准确率。
- **与 FastAPI 集成：** 将 `extract_cyrillic_text` 函数暴露为 Web 应用的 REST 接口。

随意尝试——将语言切换为 “latin” 以处理英文护照，或完全换用其他 OCR 后端。概念保持不变，代码足够灵活以适配各种情况。

祝编码愉快，愿你的图像始终清晰可读！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 分步指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [将图像转换为文本 – 从 URL 执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [使用 Aspose.OCR 的语言选择提取图像文本（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}