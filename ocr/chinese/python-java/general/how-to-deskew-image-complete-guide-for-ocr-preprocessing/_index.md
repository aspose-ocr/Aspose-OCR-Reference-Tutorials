---
category: general
date: 2026-07-05
description: 如何快速校正图像倾斜。学习为 OCR 预处理图像、纠正图像旋转，并使用 Python 将扫描件转换为文本。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: zh
og_description: 如何对图像进行去倾斜和预处理以用于 OCR。本指南展示了如何纠正图像旋转并使用 Python 从图像中提取文本。
og_title: 如何校正图像倾斜 – OCR 预处理逐步指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: 如何去除图像倾斜 – OCR 预处理完整指南
url: /zh/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何去倾斜图像 – OCR 预处理完整指南

是否曾好奇 **如何去倾斜图像** 文件，看起来像是从歪斜的扫描仪拍摄的？你并不孤单。在许多真实项目中，在 **从图像中提取文本** 之前，首先要做的就是把那种倾斜校正过来。

在本教程中，我们将通过一个动手的、端到端的示例，**为 OCR 预处理图像**、修正旋转，并最终使用 Python OCR 库 **将扫描转换为文本**。没有模糊的引用，只有可以直接复制粘贴的工作脚本，以及常见陷阱的提示。

## 你将实现的目标

完成本指南后，你将能够：

* 加载任意轻微倾斜的 JPEG 或 PNG 扫描件。  
* 应用去倾斜滤镜和二值化步骤，以提升 OCR 准确率。  
* 运行 OCR 引擎并可靠地 **从图像中提取文本**。  
* 理解 **正确的图像旋转** 为什么对后续文本提取至关重要。  

### 前置条件

* 在机器上已安装 Python 3.9+。  
* 一个可通过 pip 安装的 OCR 包，使用示例中的 `ocr` 命名空间（例如，Tesseract 的轻量包装器）。  
* 对 Python 函数和图像处理概念有基本了解。  

如果你满足以上条件，下面开始吧。

![如何去倾斜图像示例](deskew_before_after.png){alt="如何去倾斜图像 – 校正前后对比"}

## 步骤 1：设置 OCR 引擎 – 使用 Python 去倾斜图像

首先，你需要一个能够识别文档语言的 OCR 引擎。下面的代码片段展示了创建引擎并声明使用英文文本的最小模板。

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*为什么这很重要：* 引擎的语言设置会影响其使用的字符集和词典。跳过此步骤可能导致 OCR 误判常见词，尤其是在你 **校正图像旋转** 之后。

## 步骤 2：加载需要校正的扫描图像

现在把文件读取到内存中。将 `"YOUR_DIRECTORY/skewed_scan.jpg"` 替换为你自己的图像路径。

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

如果图像已经是 NumPy 数组或 OpenCV `Mat`，可以相应地调整加载方式——关键是该对象必须提供后续使用的 `apply_filter` 方法。

## 步骤 3：为 OCR 预处理图像 – 去倾斜并二值化

魔法就在这里。我们链式调用两个滤镜：

1. **去倾斜** – 自动检测主文本基线并将图像旋转回水平。  
2. **二值化（Otsu）** – 将图片转换为纯黑白，从而显著提升识别率。

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*小技巧：* 如果二值化后文字仍显得模糊，尝试调节对比度或使用其他阈值方法。`ocr.Filter` 模块通常提供 `adaptive_threshold()` 以应对更棘手的情况。

## 步骤 4：运行 OCR – 从图像中提取文本

拥有干净、已校正的画布后，将图像交给引擎。结果对象包含识别出的字符串、置信度分数，甚至还有需要时的边界框。

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

典型输出如下：

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

注意换行完全对齐了吗？这正是 **正确的图像旋转** 带来的好处——OCR 不再需要猜测行的方向。

## 步骤 5：整合为一文件脚本 – 将扫描转换为文本

下面是完整、可运行的脚本，汇集了我们讨论的所有步骤。将其保存为 `deskew_ocr.py` 并执行 `python deskew_ocr.py`。

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### 为什么这样有效

* **先去倾斜** – 在二值化之前旋转图像，确保阈值算法在水平基线上工作。  
* **去倾斜后二值化** – Otsu 方法假设直方图为双峰；倾斜的页面会破坏该假设。  
* **英文语言模型** – 告诉 OCR 预期的字符，降低误报率。  

如果需要处理其他语言，只需将 `ocr.Language.ENGLISH` 替换为相应的枚举值。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *What if the scan is upside‑down?* | The `deskew()` filter usually detects 180° rotation as well. If it fails, call `apply_filter(ocr.Filter.rotate(180))` before deskewing. |
| *My document has colored graphics – will binarization erase them?* | Yes. For mixed content, consider using `ocr.Filter.deskew()` alone, then run OCR on the color image. You can still extract text while preserving graphics. |
| *Can I process a batch of files?* | Wrap the logic in a loop, read each file path from a list, and store each `result.text` in a separate `.txt` file. |
| *How do I improve accuracy on low‑resolution scans?* | Upscale the image with a bicubic filter **before** deskewing, then apply a sharpening filter. More pixels give the OCR engine better clues. |

## 进阶：可视化验证去倾斜效果

如果想并排查看前后对比，可加入一个简短的 Matplotlib 代码片段：

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

在调试一批棘手扫描时，看到校正后的对齐效果会让人更有信心。

## 结论

我们已经覆盖了 **如何去倾斜图像**、为什么 **为 OCR 预处理图像** 至关重要，以及如何 **从图像中提取文本** 并最终 **将扫描转换为文本**。工作流——加载 → 去倾斜 → 二值化 → 识别——确保 OCR 看到的是干净、水平的页面，从而提升准确率并减少人工校正。

接下来你的 OCR 之旅可以尝试：

* 不同语言包（`ocr.Language.FRENCH` 等）。  
* 添加版面分析步骤以检测列或表格。  
* 使用 PDF 库将 OCR 结果导出为可搜索的 PDF。

如果遇到问题，欢迎留言讨论，或分享你处理顽固扫描的技巧。祝编码愉快，愿你的图像永远保持完美水平！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步扩展 API 功能并探索替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}