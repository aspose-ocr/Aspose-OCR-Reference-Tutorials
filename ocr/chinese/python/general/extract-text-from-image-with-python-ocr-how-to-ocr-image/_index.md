---
category: general
date: 2026-05-31
description: 使用 Python 的 aocr 库从图像中提取文本。学习如何对图像进行 OCR、加载用于 OCR 的图像，并仅用几行代码识别特殊字符。
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: zh
og_description: 使用 Python 的 aocr 库从图像中提取文本。本指南展示了如何对图像进行 OCR、加载用于 OCR 的图像，以及快速识别特殊字符。
og_title: 使用 Python OCR 从图像中提取文本 – 如何进行图像 OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 使用 Python OCR 从图像提取文本 – 如何对图像进行 OCR
url: /zh/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python OCR 从图像提取文本 – 如何进行 OCR

是否曾经需要**从图像中提取文本**，但不确定哪个库能够处理诸如 “Ł”、 “Ž” 或 “ß” 之类的特殊符号？你并不孤单。在许多真实项目中——比如扫描收据、多语言标识或历史文档——**识别特殊字符**的能力可能决定数据集是可用还是无路可走。

好消息是？只需几行 Python 代码和轻量级的 **aocr** 包，你就可以将任何图片转换为可搜索的文本。下面你会看到一个完整、可直接运行的脚本，以及每一步背后的 *原因*，这样你不仅仅是复制粘贴，还能真正理解发生了什么。

## 本教程涵盖内容

- 安装并导入 **aocr** 库  
- 加载用于 OCR 的图像（包括常见陷阱）  
- 运行引擎以**将图像转换为文本**  
- 打印结果并处理特殊字符输出  
- 扩展基本流程以支持多语言和错误处理  

通过本指南，你将能够**从图像中提取文本**，支持任何语言，并且了解在默认设置不足时如何微调流程。

## 前置条件

| 需求 | 为什么重要 |
|------|------------|
| Python 3.8+ | aocr 依赖现代类型特性 |
| `pip` access | 用于安装库 |
| 示例图像（例如 `multilingual.png`） | 我们将使用它展示特殊字符 |
| 对虚拟环境的基本了解（可选） | 保持依赖整洁 |

无需像 Tesseract 那样的沉重外部工具——**aocr** 捆绑了一个开箱即用的快速神经引擎。

---

## 步骤 1：安装 aocr 库

首先，打开终端（或 IDE 的控制台）并运行：

```bash
pip install aocr
```

*小技巧：* 如果你在管理多个项目，建议先创建一个虚拟环境：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

这样可以将 OCR 依赖与系统的其他部分隔离——我发现这能省去很多后期的麻烦。

---

## 步骤 2：加载用于 OCR 的图像

现在包已经准备好，我们需要**加载图像用于 OCR**。`OcrEngine` 类期望一个文件路径，请确保图像存在且可读取。

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **为什么重要：**  
> - `load_image` 会快速检查文件是否存在以及是否为支持的格式。  
> - 使用原始字符串 (`r"..."`) 可以避免 Windows 路径中的转义字符错误。  
> - 如果图像非常大，aocr 会自动降采样以保持内存使用合理。  

如果出现 `FileNotFoundError`，请再次确认路径，并确保文件扩展名为 PNG、JPEG 或 BMP 之一。

---

## 步骤 3：执行 OCR – 将图像转换为文本

图像已加载到内存后，下一步调用实际上会**识别特殊字符**并生成 Unicode 字符串。

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

在幕后，aocr 运行一个轻量级的卷积‑循环网络，已在多语言数据集上训练。这就是为什么你会看到西里尔字母、扩展拉丁字母，甚至一些罕见字形能够正确显示。

---

## 步骤 4：显示提取的文本

最后，让我们打印结果。输出将包含引擎能够识别的每一个字符，包括那些恼人的变音符号。

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**示例输出**（实际结果取决于图像内容）：

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*图像示例：*  
![从图像提取文本示例输出](https://example.com/ocr-output.png "从图像提取文本示例输出")

> **注意：** `print` 调用在现代 Python 中默认使用 UTF‑8 编码，因此在大多数终端中你应该能正确看到特殊字符。如果出现乱码，请将控制台设置为 UTF‑8，或使用 `encoding='utf-8'` 将字符串写入文件。

---

## 步骤 5：处理边缘情况与常见陷阱

### 5.1 低分辨率图像

如果图像低于 150 dpi，OCR 准确率可能会大幅下降。一个快速的解决办法是先放大再交给 aocr：

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 语言检测不正确

aocr 会自动检测语言，但你可以强制指定特定脚本以获得更好结果：

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

支持的语言代码包括 `eng`、`deu`、`fra`、`rus`、`spa` 等。

### 5.3 噪声和背景图案

噪声背景会干扰模型。可使用 OpenCV 进行二值化预处理：

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## 完整脚本 – 一键解决方案

下面是**完整、可运行的示例**，将所有步骤串联起来。将其保存为 `ocr_demo.py` 并执行 `python ocr_demo.py`。

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

运行方式如下：

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

你应该会在控制台看到提取的字符，证明你已经成功**从图像中提取文本**并**识别特殊字符**。

---

## 常见问题

**Q: 这能用于 PDF 吗？**  
A: 不能直接。请先将 PDF 页面转换为图像（例如使用 `pdf2image`），然后将每张图像喂给 aocr。

**Q: aocr 与 Tesseract 的速度相比如何？**  
A: 对于典型的 300 dpi 扫描，aocr 在现代笔记本上处理一页约需 ~0.3 秒——大约是默认设置下的 Tesseract 的两倍。

**Q: 能批量处理文件夹中的图像吗？**  
A: 完全可以。将 `main` 函数包装在 `Path(folder).glob("*.png")` 循环中，并将结果收集到 CSV 中。

---

## 结论

你现在拥有一个完整、端到端的工作流，使用 Python 的 aocr 库**从图像中提取文本**。从加载文件到打印 Unicode 输出，每一步都已解释，方便你将其迁移到自己的项目中——无论是构建收据扫描服务还是多语言文档归档。

接下来，可以进一步探索以下相关主题：

- **将图像转换为文本** 用于 PDF（使用 `pdf2image` + OCR）  
- **识别手写笔记中的特殊字符**（尝试 `ocr_engine.set_dpi(600)`）  
- **在 Web API 中加载图像用于 OCR**（Flask + aocr）  

动手试一试，调节语言设置，让你的数据瞬间可搜索。有什么问题或酷炫的使用案例？在下方留言——祝编码愉快！

## 接下来该学习什么？

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR 通过语言选择在 C# 中提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose.OCR for .NET 优化图像文本提取](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}