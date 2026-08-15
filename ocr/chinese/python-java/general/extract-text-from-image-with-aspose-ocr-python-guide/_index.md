---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 在 Python 中提取图像文本——学习如何识别 PNG 中的文字，将图像转换为文本（Python），以及快速加载图像进行
  OCR。
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to text python
- load image for ocr
- read text from scanned image
language: zh
og_description: 使用 Aspose OCR 在 Python 中提取图像文本。本教程展示如何识别 PNG 中的文字、将图像转换为文本（Python），以及加载图像进行
  OCR。
og_title: 使用 Aspose OCR 从图像提取文本 – Python 指南
tags:
- OCR
- Python
- Aspose
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – Python 指南
url: /zh/python-java/general/extract-text-from-image-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 提取图像文本 – Python 指南

是否曾需要 **从图像中提取文本**，却不确定哪个库能在 PNG 扫描件上提供可靠的结果？你并不孤单——许多开发者在处理扫描的 PDF 或收据照片时都会遇到这个难题。好消息是：使用 Aspose OCR for Python，你可以识别 PNG 文件中的文本、以 Python 方式将图像转换为文本，并且只需几行代码即可加载图像进行 OCR。

在本教程中，我们将演示一个完整、可运行的示例，准确展示如何使用 Aspose OCR **从图像中提取文本**。你将看到如何加载图像、启用自动语言检测、运行 OCR 引擎，最后读取检测到的语言和提取的文本。完成后，你即可将此代码嵌入任何需要读取扫描图像文件中文本的项目中。

## 你将学到

- 如何使用 Aspose Storage **加载图像进行 OCR**。
- 如何 **从 PNG 中识别文本** 并自动检测其语言。
- 如何 **以 Python 方式将图像转换为文本**，无需处理底层字节缓冲区。
- 处理多页 PDF、常见陷阱以及边缘案例的技巧。
- 预期输出以及快速验证提取是否成功的方法。

### 前置条件

- 已在机器上安装 Python 3.8 或更高版本。
- 拥有 Aspose OCR for Python 许可证（或免费试用密钥）——可从 Aspose 官网获取。
- 通过 `pip install aspose-ocr aspose-storage` 安装 `aspose-ocr` 与 `aspose-storage` 包。
- 准备一张 PNG 或其他受支持的图像文件供处理。

现在，让我们开始吧。

## 步骤 1：加载图像进行 OCR

在 OCR 引擎能够工作之前，需要先获取图像对象。Aspose Storage 让这一步变得轻而易举。

```python
# Step 1: Import required Aspose modules
import aspose.ocr as aocr
import aspose.storage as storage

# Step 1.1: Define the path to your image file
input_image_path = "YOUR_DIRECTORY/input_image.png"

# Step 1.2: Load the image – Aspose supports PNG, JPEG, BMP, TIFF, etc.
# The Image class abstracts away file‑system handling.
image = storage.Image.load(input_image_path)
```

*为什么重要：* 使用 `storage.Image.load` 可以抽象掉格式特有的细节，这样你就可以 **从 png 中识别文本** 或 JPEG，而无需编写自定义加载器。如果文件未找到，Aspose 会抛出明确的 `FileNotFoundError`，你可以捕获它以实现优雅的回退。

> **专业提示：** 为获得最佳性能，请将图像大小控制在 5 MB 以下。对于更大的文件，可在 OCR 前使用 `image.resize()` 进行降采样。

## 步骤 2：初始化 OCR 引擎并启用语言检测

Aspose OCR 附带功能强大的 `OcrEngine`，能够自动检测文本的语言。开启此功能通常能提升多语言文档的识别准确度。

```python
# Step 2: Initialise the OCR engine
ocr_engine = aocr.OcrEngine()

# Step 2.1: Enable automatic language detection (AUTO mode)
ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO
```

*为什么重要：* 当你以 **Python 方式将图像转换为文本** 时，语言信息非常关键，因为它会影响识别时使用的字符集和词典。AUTO 模式让引擎自行选择最佳匹配，无论是英语、西班牙语还是中文。

## 步骤 3：从 PNG 中识别文本并提取结果

现在正式进入核心工作。`recognize` 方法会运行 OCR 流程并返回一个丰富的结果对象。

```python
# Step 3: Run OCR on the loaded image
ocr_result = ocr_engine.recognize(image)

# Step 3.1: Pull out the detected language and the plain text
detected_lang = ocr_result.detected_language
extracted_text = ocr_result.text
```

如果只需要原始字符串，`ocr_result.text` 已经可以直接使用。`detected_language` 属性会返回 ISO‑639‑1 代码（例如 `"en"` 代表英语）。

> **边缘情况：** 对于严重损坏的扫描件，引擎可能返回空字符串。此时可考虑在将图像交给 Aspose 之前，使用 Pillow 等库进行预处理（提升对比度、去倾斜）。

## 步骤 4：展示结果 – 预期输出

让我们打印结果，以便验证一切正常。

```python
# Step 4: Show the detection results
print(f"Detected language: {detected_lang}")
print("Extracted text:")
print(extracted_text)
```

### 示例输出

```
Detected language: en
Extracted text:
Invoice #12345
Date: 2026‑03‑01
Total: $1,250.00
Thank you for your business!
```

如果看到类似的内容，恭喜你——已经成功使用 Aspose OCR **从图像中提取文本**！如果输出乱码，请再次确认图像质量是否足够（打印文本建议至少 300 dpi）。

## 步骤 5：高级技巧 – 处理多页 PDF 与扫描文档

虽然基本流程适用于单个 PNG，但实际场景常常涉及多页 PDF 或 TIFF 堆叠。

1. **将 PDF 页面转换为图像** – Aspose PDF 可将每页渲染为 PNG，然后将其喂入 OCR 循环。
2. **批量处理** – 遍历扫描图像目录，将结果累积到列表或写入 CSV。
3. **自定义语言选择** – 如果文档始终为法语，可将 `ocr_engine.language_detection = aocr.LanguageDetectionMode.FRENCH` 以提升速度。

```python
# Example: Batch processing a folder of PNGs
import os

folder = "scans/"
texts = []
for file_name in os.listdir(folder):
    if file_name.lower().endswith(".png"):
        img = storage.Image.load(os.path.join(folder, file_name))
        result = ocr_engine.recognize(img)
        texts.append({"file": file_name,
                      "lang": result.detected_language,
                      "text": result.text})
```

现在你拥有一个可以使用 `json` 或 `pandas` 导出的实用集合。

## 步骤 6：常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 输出为空 | 图像分辨率过低或压缩过度 | 将分辨率提升至 ≥300 dpi，使用 Pillow 锐化 |
| 语言检测错误 | 页面混合多语言 | 手动将 `language_detection` 设置为特定语言，或对每页单独处理 |
| 大批量处理时内存错误 | 同时加载大量高分辨率图像 | 逐张处理，或在每次迭代后调用 `gc.collect()` |
| 出现异常字符 | OCR 字典不支持的字体 | 若处理阿拉伯文或印地文等复杂脚本，启用 `ocr_engine.enable_complex_script` |

## 完整可运行脚本

下面是完整脚本，可直接复制到名为 `extract_text.py` 的文件中。将 `YOUR_DIRECTORY/input_image.png` 替换为实际的图像路径。

```python
# extract_text.py
# Complete example: extract text from image with Aspose OCR (Python)

import aspose.ocr as aocr
import aspose.storage as storage

def main():
    # 1️⃣ Load the image
    input_image_path = "YOUR_DIRECTORY/input_image.png"
    try:
        image = storage.Image.load(input_image_path)
    except Exception as e:
        print(f"❗ Unable to load image: {e}")
        return

    # 2️⃣ Initialise OCR engine and enable auto language detection
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO

    # 3️⃣ Run OCR
    try:
        ocr_result = ocr_engine.recognize(image)
    except Exception as e:
        print(f"❗ OCR failed: {e}")
        return

    # 4️⃣ Output results
    print(f"Detected language: {ocr_result.detected_language}")
    print("Extracted text:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

运行方式：

```bash
python extract_text.py
```

你应该会在控制台看到检测到的语言以及随后打印的提取文本。

## 结论

现在，你已经掌握了如何在 Python 中使用 Aspose OCR **从图像中提取文本**，从文件加载到显示识别结果的完整流程。此端到端解决方案让你能够 **从 png 中识别文本**、**以 Python 方式将图像转换为文本**，并在任何自动化流水线中轻松 **加载图像进行 OCR**。

下一步？尝试将一批扫描收据喂入脚本，导出结果为 CSV，或将 OCR 步骤集成到更大的文档处理工作流中（例如自动填充数据库）。如果你想将扫描的 PDF 转换为可搜索文档，可进一步探索 Aspose PDF——这是处理 **从扫描图像中读取文本** 的 PDF 时的自然延伸。

祝编码愉快，欢迎尝试不同的语言设置、图像预处理技巧，甚至将 Aspose OCR 与 Tesseract 结合使用形成混合方案。如遇到任何问题，欢迎在下方留言——我们一起排查解决！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}