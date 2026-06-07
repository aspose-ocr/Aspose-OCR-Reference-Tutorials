---
category: general
date: 2026-06-06
description: 如何使用 Python 对图像进行 OCR 预处理。学习使用 Otsu 方法二值化图像，如何校正扫描文档的倾斜，以及提升德文文本的 OCR
  准确率。
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: zh
og_description: 如何在 Python 中对图像进行 OCR 预处理。本教程展示了使用 Otsu 方法二值化图像、如何校正扫描文档的倾斜，以及如何提升德语图像的
  OCR 准确率。
og_title: 如何为OCR预处理图像——完整Python指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: 如何为 OCR 预处理图像——完整 Python 指南
url: /zh/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何为 OCR 预处理图像 – 完整 Python 指南

有没有想过 **how to preprocess images for OCR**，让文本清晰可辨？你并非唯一。扫描文档——尤其是嘈杂的德文页面——对任何 OCR 引擎来说都是噩梦。好消息是？只需几个聪明的预处理步骤，就能把模糊、斑点的扫描件变成干净、机器可读的图像。

在本教程中，我们将通过一个实用示例演示使用 Python 的 **how to preprocess images for OCR**。你将学习 **binarize image using Otsu**、**how to deskew scanned documents**，以及整体上 **how to improve OCR accuracy**，当你需要 **extract text from German image** 文件时。没有废话，只有可直接复制粘贴的工作脚本。

## 你需要的准备

- **Python 3.9+**（任何近期版本均可）
- 一个提供 `OcrEngine` 类的 OCR 库——演示中我们假设使用通用的 `ocr` 包。使用 `pip install ocr-lib` 安装。
- 一个嘈杂的德文扫描件（`noisy_german_scan.tif`），用于测试。
- 对 Python 函数的基本了解（如果你写过 `def`，就足够了）。

> **技巧提示：** 如果你使用其他 OCR SDK（例如通过 `pytesseract` 的 Tesseract），概念保持不变——只需调整方法名称。

## 解决方案概览

1. **创建 OCR 引擎实例。**  
2. **将识别语言设置为德语。**  
3. **构建自定义预处理流水线**，包括去倾斜、去噪、二值化（Otsu）和对比度拉伸。  
4. **将流水线附加到引擎**，使每张图像自动经过处理。  
5. **运行 OCR** 对嘈杂的德文扫描件进行识别。  
6. **打印提取的文本** 以验证结果。

下面我们逐步拆解每一步，解释 **why** 它重要，并展示你需要的完整代码。

![如何为 OCR 预处理图像示例](image.png "如何为 OCR 预处理图像示例")

## 步骤 1：创建 OCR 引擎实例

首先——没有引擎，什么也不会发生。`OcrEngine` 对象是协调后续所有处理的入口点。

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Why this matters:* 初始化引擎会设置内部资源（如语言模型），并为后续附加自定义流水线提供干净的起点。

## 步骤 2：将识别语言设置为德语

OCR 的准确性高度依赖语言。告知引擎预期为德语后，会激活正确的字符集和语言模型。

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

如果跳过此步骤，引擎可能默认使用英语，导致误识别变音符（ä, ö, ü）和 ß 字符——这是处理德文扫描件时常见的陷阱。

## 步骤 3：构建自定义预处理流水线

这是 **how to preprocess images for OCR** 的核心。我们将串联四个转换：

| 转换 | 作用 | 帮助原因 |
|------|------|----------|
| **Deskew** | 将图像旋转回水平（最大 5°） | 扫描很少完全对齐；去倾斜可消除导致字符分割混乱的倾斜。 |
| **Denoise** | 降低随机斑点（强度 0.7） | 噪声会产生错误的边缘，OCR 引擎可能将其误识为字符。 |
| **Binarize (Otsu)** | 使用 Otsu 方法转换为黑白二值图 | 干净的二值图为引擎提供前景（文本）与背景之间的鲜明对比。 |
| **Contrast Stretch** | 扩展动态范围 | 提高细弱笔画的可读性，尤其是旧文档。 |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### 如何对扫描文档去倾斜

`deskew` 调用即是对 **how to deskew scanned documents** 的具体实现。内部通过 Hough 变换估计主文本行角度并将图像旋转回正。如果文档旋转超过 5°，可以提升 `max_angle`，但要注意过度旋转产生的伪影。

### 使用 Otsu 进行图像二值化

`binarize(method="otsu")` 这一行直接回答了 **binarize image using otsu** 的查询。Otsu 算法计算出最小化类内方差的阈值，非常适合具有双峰直方图（深色文本与浅色背景）的文档。

## 步骤 4：将流水线附加到引擎

现在我们指示 OCR 引擎对每个输入图像运行我们刚构建的流水线。

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Why this matters:* 若不注册，引擎将直接处理原始扫描，忽略我们配置的所有清理步骤。此步骤通过一致地应用相同的预处理，确保 **how to improve OCR accuracy**。

## 步骤 5：从嘈杂的德文扫描件识别文本

是时候把所有内容组合起来了。我们向引擎提供嘈杂的德文图像，让它完成繁重的工作。

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

如果你对性能感兴趣，可以对调用进行计时：

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## 步骤 6：输出识别的文本

最后，我们打印提取的字符串。这是对 **extract text from german image** 的直接回答。

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### 预期输出

假设示例扫描包含句子 “Die schnelle braune Füchsin springt über den faulen Hund.”，你应看到类似如下的输出：

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

如果输出仍包含乱码，请考虑调整 `denoise` 强度或增加 `max_angle` 以进行去倾斜。

## 常见陷阱及解决方法

- **缺少语言模型：** 忘记调用 `set_recognition_language(Language.GERMAN)` 常导致缺失变音符。请再次检查该调用。
- **去噪过度：** 强度高于 0.9 可能抹去细小笔画，尤其是旧字体。大多数情况下保持在 0.5‑0.7。
- **文件格式错误：** 某些 OCR 引擎无法处理多页 TIFF。如果有多页文档，请先拆分为单页文件。
- **流水线顺序：** 所示顺序（deskew → denoise → binarize → contrast）是有意为之。先二值化再去噪会固化噪声；请始终先去噪。

## 扩展流水线（下一步？）

既然已经有了坚实的基线，你可能想要：

- **添加形态学开运算** 来清除细小斑点（`.morph_open(kernel=3)`）。
- **集成语言模型** 进行后处理校正（`ocr_engine.apply_spellcheck()`）。
- **使用 `concurrent.futures` 并行批处理** 大规模数据集。

所有这些都是自然的扩展，在保持 **how to preprocess images for OCR** 核心思想的同时，进一步提升 **how to improve OCR accuracy**。

## 结论

我们已经完整介绍了 **how to preprocess images for OCR** 的全过程：创建引擎、设置德语、构建包含 **binarize image using Otsu**、**how to deskew scanned documents** 的流水线，最终以更高的置信度 **extract text from german image**。遵循上述六个步骤，你会看到识别质量显著提升——不再需要无尽的手动校正。

使用自己的扫描件运行脚本，尝试不同参数，让结果说话。对某个特定的预处理调整有疑问？留下评论，我们一起深入探讨。

祝编码愉快，愿你的 OCR 永远精准！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.OCR 进行语言选择的 C# 提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [如何在 OCR 图像识别中设置阈值](/ocr/english/net/ocr-settings/set-threshold-value/)
- [如何 OCR 图像 – 在 OCR 图像识别中对图像执行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}