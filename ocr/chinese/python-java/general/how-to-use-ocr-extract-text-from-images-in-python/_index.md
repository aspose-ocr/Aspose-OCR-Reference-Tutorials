---
category: general
date: 2026-03-18
description: 如何使用 OCR 从图像中提取文本——快速指南，教你识别 PNG 文件中的文字并加载图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: zh
og_description: 如何使用 OCR 从图像中提取文本——学习从 PNG 识别文本，加载图像进行 OCR，并使用简单的 Python 脚本提取文本。
og_title: 如何使用 OCR：在 Python 中从图像提取文本
tags:
- OCR
- Python
- Image Processing
title: 如何使用 OCR：在 Python 中从图像提取文本
url: /zh/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR：在 Python 中从图像提取文本

有没有想过在手头有一张杂乱的截图或扫描的收据时，**如何使用 OCR**？你并不孤单——开发者经常需要从图片中提取可读文本，尤其是来自移动应用或网页上传的 PNG。 在本教程中，我们将演示一个完整、可运行的示例，向你展示如何 **从图像文件中提取文本**、**从 PNG 资产中识别文本**，甚至只用几行 Python **加载图像进行 OCR**。

我们将涵盖从安装合适的库到处理多语言文档的全部内容，届时你将准确了解如何 *从任意图像中提取文本*。没有模糊的引用，只有清晰的逐步解决方案，您可以复制粘贴并直接运行。

## 您将学到的内容

在接下来的几节中我们将：

1. 搭建一个轻量级的 OCR 引擎（无需大型依赖）。  
2. 将图像文件——特别是 PNG——加载到引擎中。  
3. 启用自动语言检测，使引擎能够处理多语言内容。  
4. 运行识别过程并获取纯文本结果。  
5. 为缺失文件或不支持的格式等边缘情况微调工作流。

如果你对基础 Python 已经熟悉，完全可以上手。无需事先的 OCR 经验，快速浏览一下库的文档也会有帮助。

---

![在 PNG 图像上使用 OCR 的方法](placeholder.png "在 PNG 图像上使用 OCR 的方法 – 分步指南")

## 如何使用 OCR – 加载图像并识别文本 {#how-to-use-ocr}

### 步骤 1：安装 OCR 库

首先，你需要一个提供 `OcrEngine` 类的 Python 包。为了本教程的目的，我们将使用虚构但具有示例性的 **SimpleOCR** 包，你可以通过 pip 安装它：

```bash
pip install simple-ocr
```

> **专业提示：** 如果你在虚拟环境中工作（强烈推荐），请在运行安装命令前激活它。这可以保持项目依赖的整洁。

### 步骤 2：导入引擎并创建实例

创建引擎就像调用构造函数一样简单。把引擎想象成后续处理你提供的图像的“大脑”。

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

为什么每次都要创建新实例？因为需要隔离。全新的引擎保证之前运行留下的状态不会污染当前的识别，这在批量处理大量文件时尤为关键。

### 步骤 3：加载要处理的图像

现在我们实际 **加载图像进行 OCR**。`setImageFromFile` 方法接受任意光栅图像的路径；这里我们指向名为 `mixed_doc.png` 的 PNG。

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

如果文件未找到，`SimpleOCR` 会抛出明确的 `FileNotFoundError`。你可以捕获它并提供友好的错误提示：

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### 步骤 4：启用自动语言检测

大多数现代 OCR 引擎都自带语言包。通过传入 `"multilingual"`，我们告诉引擎自动嗅探文本并选择合适的语言模型。这在你的 PNG 包含英文和西班牙文混合时尤其方便。

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

如果你事先知道语言，可以将 `"multilingual"` 替换为具体的语言代码，例如 `"eng"` 或 `"spa"`，以加快处理速度。

### 步骤 5：运行识别过程

真正的工作在这里完成。`recognize()` 会扫描图像、进行分割、运行神经网络，并在内部构建文本缓冲区。

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

在幕后，引擎会执行：

- **预处理**（去倾斜、二值化）  
- **版面分析**（检测列、表格）  
- **字符分类**（使用深度学习模型）  

所有这些都已抽象化，这也是只需要一行代码的原因。

### 步骤 6：获取并打印识别结果

最后，我们获取结果对象并提取纯字符串。这就是实际 **从图像中提取文本** 的环节。

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**预期输出**（为简洁起见已截断）：

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

如果图像中没有可识别的字符，`text` 将是空字符串。你可以对此进行防护：

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## 从图像提取文本 – 处理常见边缘情况

### 一个文件中包含多种语言

当文档混合多语言时，`"multilingual"` 设置通常能正常工作。但如果出现误识别，你可以手动指定回退语言列表：

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### 非 PNG 格式

虽然我们的重点是 **从 PNG 识别文本**，`SimpleOCR` 也支持 JPEG、BMP 和 TIFF。只需在 `setImageFromFile` 中更改文件扩展名。对于 TIFF 堆栈，可能需要指定具体页码：

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### 大文件与内存使用

如果你在处理千兆像素的扫描件，考虑在 OCR 前先缩放图像：

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

缩放可以降低内存压力，同时保留足够的细节以实现准确识别。

### 调试加载失败

有时图像肉眼看起来正常，但内部已损坏。启用详细日志以查看引擎实际读取的内容：

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## 完整、可直接运行的脚本

下面是把所有步骤组合在一起的完整程序。将其复制到名为 `ocr_demo.py` 的文件中，修改 `YOUR_DIRECTORY` 占位符，然后运行 `python ocr_demo.py`。

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

运行此脚本后，应该会输出 `mixed_doc.png` 中内容的纯文本版本。随意将文件换成其他图片——**如何提取文本**的方式保持不变。

---

## 结论

我们刚刚演示了在 Python 中 **如何使用 OCR** 来 **从图像文件中提取文本**，特别聚焦于 **从 PNG 资产中识别文本** 以及实际的 **加载图像进行 OCR** 步骤。上面的代码片段是一个自包含的解决方案：安装包、提供文件、启用多语言检测、运行引擎并获取结果。

接下来你可以：

- 将脚本集成到接受用户上传的 Web 服务中。  
- 批量处理转换为 PNG 的 PDF 文件夹。  
- 添加后处理（例如正则清理、拼写检查）以提升准确率。

记住，OCR 的质量取决于图像清晰度、合适的语言包，有时还需要一点预处理——所以多尝试吧。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}