---
category: general
date: 2026-03-26
description: 学习如何对图像进行去倾斜、识别图像中的文本，并构建图像预处理流水线，以去除扫描噪声并将扫描图像转换为文本。
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: zh
og_description: 如何纠正图像倾斜并将倾斜的扫描件转换为可搜索的文本。请按照本指南识别图像中的文字，去除扫描噪声，并将扫描图像转换为文本。
og_title: 如何校正图像倾斜 – 步骤式 OCR 指南
tags:
- OCR
- image-processing
- Python
title: 如何纠正图像倾斜 – 包含 OCR 的完整指南
url: /zh/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何去倾斜图像 – 完整的 OCR 指南

是否曾经想过**如何去倾斜图像**从廉价扫描仪得到的图像？你并不孤单。歪斜的页面看起来不专业，更重要的是，倾斜会导致任何尝试**从图像中识别文本**的 OCR 引擎出错。  

在本教程中，我们将逐步演示完整的 **图像预处理流水线**，它会去倾斜、二值化并去噪扫描图像，然后交给 OCR 引擎，使您能够 **将扫描图像转换为文本**，过程轻松无忧。没有魔法，仅使用原生 Python 和一个完成繁重工作的轻量库。

## 您需要的环境

- Python 3.9+（代码在 3.10 及以上版本也可运行）
- `ocr` 包（通过 `pip install ocr‑toolkit` 安装 – 替换为您实际使用的库名）
- 一张明显倾斜的扫描 JPEG 或 PNG（例如 `skewed_scan.jpg`）
- 对每个预处理步骤为何重要有一点好奇心

就是这样。除非您以后想深入研究，否则无需像 OpenCV 这样的大型依赖。

## 步骤 1：加载扫描图像

首先需要将文件读取到内存中。此步骤简单却至关重要——如果路径错误，后续所有操作都会崩溃。

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **为什么？**  
> 加载图像后我们得到一个可操作的对象，`ocr.ImagePreprocessor` 可以对其进行处理。跳过此步骤会使流水线无法获取实际像素数据。

## 如何去倾斜图像并为 OCR 做准备

现在我们已经拥有图像，接下来将其校正。`deskew()` 方法会估计倾斜角度并将图片旋转回水平。

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **专业提示：** 如果您的扫描仅略有倾斜（≤ 3°），默认算法通常非常准确。对于极端角度，可能需要调整内部参数——请查看库文档中的 `max_angle`。

## 二值化图像 – 转为黑白

OCR 引擎喜欢高对比度的输入。将图片转换为二值（黑白）表示可以去除细微的灰度，从而避免字符识别混淆。

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **发生了什么？**  
> 像素值大于 128 的会变为白色，其他全部变为黑色。如果扫描图像异常暗或亮，请调整阈值。

## 在 OCR 前去除扫描噪声

即使是完美去倾斜的图像也可能包含斑点、灰尘或压缩伪影。这些小斑点是任何 OCR 引擎的克星。

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **为什么要去噪？**  
> 噪声会产生错误的边缘，OCR 引擎可能将其误识为字符。小半径适用于大多数扫描；对于颗粒感强的文档可适当增大。

## 应用图像预处理流水线

所有配置已就绪——现在在原始图像上运行流水线。

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **结果：** `processed_image` 是已清理、校正且高对比度的位图，准备进行文本提取。

## 使用 OCR 引擎从图像中识别文本

是时候真正读取文本了。我们初始化 OCR 引擎，将处理好的图像输入，并请求原始字符串。

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **预期输出**（示例）：

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

如果出现乱码，请再次检查去倾斜步骤或尝试不同的 `threshold` 值。

## 构建图像预处理流水线 – 完整脚本

将所有内容整合在一起，以下是一个可直接放入 `.py` 文件并运行的完整脚本：

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **提示：** 如果计划批量处理多个文件，可将整个过程封装在函数中（`def ocr_from_file(path): …`）。

## 常见问题与边缘情况

- **如果图像已经是正向的怎么办？**  
  `deskew()` 方法会检测到接近零的角度并保持图像不变，因此可以安全地对每个文件运行该方法。

- **我的扫描是彩色的——应该保留吗？**  
  对于大多数 OCR 任务，颜色并无价值。二值化会去除颜色，加快处理速度并降低内存占用。

- **我可以链式使用多个预处理步骤吗？**  
  完全可以。`ImagePreprocessor` 类专为流水线设计；在调用 `apply()` 之前，你可以添加 `sharpen()`、`contrast_enhance()` 或自定义过滤器。

- **OCR 输出中出现多余换行——如何解决？**  
  使用 `text.replace("\n", " ").strip()` 对字符串进行后处理，或使用更高级的版面分析库，如 Tesseract 的 `--psm` 模式。

## 后续步骤

既然您已经了解**如何去倾斜图像**并拥有完整的**图像预处理流水线**，可以进一步探索：

- 将**从图像中识别文本**集成到 Flask API，以实现即时文档上传。
- 使用流水线**去除扫描噪声**，处理需要保存的历史文档。
- 扩展至批量处理数千页，并使用 `pdfminer` 或 `PyMuPDF` 输出可搜索的 PDF。

欢迎尝试不同的阈值、去噪半径，甚至在需要多语言支持时将 OCR 后端换成 Tesseract。基本原理保持不变：校正、清理，然后读取。

---

*编码愉快！如果遇到问题，请在下方留言——我很乐意帮助您微调流水线。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}