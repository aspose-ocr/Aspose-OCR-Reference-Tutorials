---
category: general
date: 2026-04-26
description: 使用 Aspose OCR 在 Python 中从图像提取文本。了解如何提取文本、将图像转换为文本，以及加载图像进行 OCR，并支持多语言。
draft: false
keywords:
- extract text from image
- how to extract text
- convert image to text
- load image for ocr
- multilingual ocr python
language: zh
og_description: 即时从图像中提取文本。本指南展示了如何提取文本、将图像转换为文本，以及使用 Aspose OCR 在 Python 中加载图像进行
  OCR。
og_title: 使用 Python 从图像提取文本 – 完整多语言 OCR 教程
tags:
- OCR
- Python
- Aspose
title: 使用 Python 从图像中提取文本 – 多语言 OCR 指南
url: /zh/python-java/general/extract-text-from-image-with-python-multilingual-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 提取图像文本 – 多语言 OCR 指南

是否曾需要**从图像中提取文本**却不确定哪个库能处理混合语言的页面？你并不孤单。在许多实际应用中——比如发票处理、社交媒体监控或多语言文档归档——你会遇到同时包含拉丁字母和西里尔字母的图片。

好消息是？使用 Aspose OCR for Python，你可以**提取文本**、**将图像转换为文本**，并**加载图像进行 OCR**，只需几行代码，且引擎会自动检测语言。在本教程中，我们将演示一个完整、可运行的示例，解释每一步的意义，并覆盖你在实践中可能遇到的几个边缘情况。

> **你将收获**  
> * 一个可直接运行的脚本，能够从混合语言的 PNG 中提取文本。  
> * 如何在 Python 中配置多语言 OCR 的理解。  
> * 处理大文件、不同图像格式以及调试常见陷阱的技巧。  

## 前置条件

- Python 3.8 或更高（代码使用 f‑strings）。  
- 已安装 `asposeocr` 包（`pip install asposeocr`）。  
- 一张包含多种文字脚本的图像文件（例如 `mixed_lang.png`）。  
- 对 Python 导入和面向对象 API 有基本了解。  

没有繁重的依赖，没有外部服务——只需一次 pip 安装，即可开始。

---

## 第 1 步 – 安装并导入 Aspose OCR 库  

在我们能够**加载图像进行 OCR**之前，需要先获取库本身。该包自带核心 OCR 引擎和轻量级图像加载器。

```python
# Install the package (run once in your environment)
# pip install asposeocr

# Import the required classes
import asposeocr as aocr
from asposeocr import OcrEngine, OcrConfig, Language
```

*为什么重要*：导入特定类可以保持命名空间整洁，使后续代码更清晰。如果只导入 `asposeocr`，则每次调用都需要加前缀（`aocr.OcrEngine()`），代码会显得冗长。

---

## 第 2 步 – 创建 OCR 引擎并启用多语言检测  

Aspose OCR 能自动猜测图像中出现的语言。将 `Language.AUTO` 设置为覆盖拉丁文、西里尔文、阿拉伯文等多种语言。

```python
# Initialize the OCR engine
ocr_engine = OcrEngine()

# Enable automatic language detection (covers Latin, Cyrillic, etc.)
ocr_engine.config.language = Language.AUTO
```

*小贴士*：如果事先知道语言集合，可以使用 `Language.ENGLISH` 或 `Language.RUSSIAN` 来获得轻微的性能提升。但对于真正的混合文档，`AUTO` 是最安全的选择。

---

## 第 3 步 – 加载要处理的图像  

这里我们**加载图像进行 OCR**。Aspose 支持 PNG、JPEG、BMP、TIFF，甚至将 PDF 页面视作图像加载。

```python
# Path to the image containing mixed‑language text
image_file_path = "YOUR_DIRECTORY/mixed_lang.png"

# Load the image into the OCR engine
ocr_engine.image = aocr.Image.load(image_file_path)
```

> **提示**：如果图像大于 2 MB，建议事先进行缩放。大图会增加内存占用并减慢检测步骤。

---

## 第 4 步 – 运行 OCR 过程并获取结果  

调用 `process()` 完成核心工作：文本检测、版面分析以及语言解码。

```python
# Execute the OCR operation
ocr_result = ocr_engine.process()
```

返回的 `ocr_result` 对象包含多个有用属性：

| 属性 | 描述 |
|----------|-------------|
| `text`   | 识别出的纯文本字符串（最常用）。 |
| `confidence` | 整体置信度分数（0‑100）。 |
| `lines`  | 包含位置信息的 `OcrLine` 对象列表（对 PDF 很有帮助）。 |

---

## 第 5 步 – 显示提取的文本  

最后，我们打印输出。在实际应用中，你可能会将其写入数据库或传递给翻译 API。

```python
print("Recognized Text:")
print(ocr_result.text)
```

**预期输出**（混合语言图像示例）：

```
Recognized Text:
Hello world!
Привет мир!
```

如果出现乱码，请确认图像未损坏且使用的是最新版本的 `asposeocr`（撰写时为 v23.7）。

---

## 第 6 步 – 完整脚本，可直接复制粘贴  

将所有步骤整合在一起，消除“代码从哪开始”的困惑。将此文件保存为 `multilingual_ocr.py` 并在命令行运行。

```python
# multilingual_ocr.py
# -------------------------------------------------
# Complete example: extract text from image (multilingual)
# -------------------------------------------------

import asposeocr as aocr
from asposeocr import OcrEngine, Language

def extract_text(image_path: str) -> str:
    """
    Loads an image, runs Aspose OCR with auto language detection,
    and returns the recognized text.
    """
    engine = OcrEngine()
    engine.config.language = Language.AUTO
    engine.image = aocr.Image.load(image_path)
    result = engine.process()
    return result.text

if __name__ == "__main__":
    # Adjust this path to point at your own image file
    img_path = "YOUR_DIRECTORY/mixed_lang.png"
    text = extract_text(img_path)
    print("Recognized Text:")
    print(text)
```

运行方式：

```bash
python multilingual_ocr.py
```

你应该会在控制台看到提取的字符串。这就是使用少量代码**将图像转换为文本**的全部过程。

---

## 常见问题与边缘情况处理  

### 如果图像中包含手写文字怎么办？  
Aspose OCR 针对印刷体文本进行优化。手写文字通常需要专用模型（如 Azure Read 或 Google Vision）。你仍可尝试 `Language.AUTO`，但置信度可能较低。

### 如何提升噪声扫描的准确率？  
1. 预处理图像（二值化、去噪）。  
2. 将 DPI 提升至至少 300 ppi 再送入引擎。  
3. 若图像倾斜，显式设置 `ocr_engine.config.deskew = True`。

```python
ocr_engine.config.deskew = True
```

### 能否直接从 PDF 提取文本，而无需先转换为图像？  
可以——Aspose OCR 能直接打开 PDF 页面：

```python
ocr_engine.image = aocr.Image.load("document.pdf", page_number=1)
```

只需记住，每页在内部仍被视作图像处理，因此同样的质量考虑仍然适用。

---

## 结论  

现在，你已经掌握了使用 Aspose OCR 在 Python 中**从图像提取文本**的完整端到端方案，并支持多语言。该脚本演示了如何**加载图像进行 OCR**、**将图像转换为文本**，以及如何处理最常见的陷阱。

接下来，你可以：

- 将该函数集成到接受用户上传的 Web 服务中。  
- 将提取的文本与语言检测库结合，以路由到合适的翻译引擎。  
- 试验 `ocr_engine.config` 选项（如 `max_recognition_time`、`text_orientation`）以微调性能。

祝编码愉快，愿你的 OCR 流程始终精准！

---  

![Screenshot of extracted multilingual text – extract text from image example](image-placeholder.png "extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}