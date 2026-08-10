---
category: general
date: 2026-06-28
description: 在 Python 中对图像进行 OCR 预处理，包括自动旋转、二值化和去噪。使用 OCR 引擎获取结构化的 JSON 输出。
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: zh
og_description: 使用 Python 对图像进行 OCR 预处理，包括自动旋转、二值化和去噪。学习使用 OCR 引擎提取结构化 JSON。
og_title: OCR图像预处理——完整Python指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR 图像预处理——完整 Python 指南
url: /zh/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 预处理图像用于 OCR – 完整 Python 指南

是否曾想过如何 **预处理图像用于 OCR**，让引擎真正读取你看到的内容？你并不孤单——大多数开发者在扫描文档出现乱码时都会遇到同样的难题。好消息是，只需几个关键步骤——自动旋转、二值化和去噪——就能把杂乱的照片变成干净、机器可读的文本。

在本教程中，我们将演示一个 **Python** 工作流，不仅清理图像，还会返回结构化的 JSON 文件。完成后，你将会掌握如何为 OCR 自动旋转图像、进行图像二值化以及在将图像送入 **OCR engine Python** 实例前进行去噪。

## 你需要准备的环境

在开始之前，请确保你的机器上已具备以下条件：

- Python 3.9+（任意近期版本均可）
- `Pillow` 用于图像处理（`pip install pillow`）
- `ocrutil` – 一个虚构的封装 OCR 引擎的工具库（通过 `pip install ocrutil` 安装）
- 一张倾斜的示例图片（`skewed.jpg`），放在可引用的文件夹中

就这些——无需重量级框架，也不需要 GPU 加持。只要普通的 Python 加上几个实用库即可。

## 第一步：加载图像 – 为 OCR 做准备

首先，我们需要一个图像对象，以便后续流水线处理。

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*为什么这一步很重要：* 使用 Pillow 加载图像可以保留所有原始像素数据，这在后续进行二值化时至关重要。跳过此步骤或使用低质量加载器可能已经破坏了 OCR 的准确性。

## 第二步：为 OCR 自动旋转图像（auto rotate image OCR）

用手机拍摄的照片常常倾斜甚至倒置。`ocrutil.auto_rotate` 辅助函数会检测文字基线并相应地旋转图像。

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*小技巧：* 如果你的文档始终是正立的，可以跳过此步骤，但在实际场景中，“auto rotate image OCR” 能帮你省去大量手动校正的工作。

## 第三步：预处理图像用于 OCR – 二值化 + 去噪

现在进入核心环节：**预处理图像用于 OCR**。最有效的两招是：

1. **二值化** – 将图片转换为纯黑白，强化字符边缘。
2. **去噪** – 去除可能被 OCR 误认成字形的斑点。

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

如果在此步骤后查看图像（例如 `img.show()`），你会注意到背景与前景的对比度大幅提升——这正是优秀 OCR 引擎所渴求的。

## 第四步：设置 OCR 引擎（OCR engine Python）

手握干净的图像后，我们实例化 OCR 引擎。`ocrutil.OcrEngine` 类封装了流行的开源 OCR 后端（如 Tesseract），并提供友好的 Python API。

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*这么做的原因：* 将预处理后的图像传递给 **OCR engine Python** 对象，确保引擎使用你能提供的最高质量数据，从而直接提升识别准确率。

## 第五步：纯文本识别（可选但实用）

有时你只需要原始文本。此步骤为可选，因为本教程的主要目标是结构化输出，但它对于快速检查非常有帮助。

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

你会得到一段看起来与原始文档相似的字符串，只是没有任何布局信息。如果文字出现乱码，请返回并微调预处理参数。

## 第六步：提取结构化数据并保存为 JSON（OCR structured JSON output）

现代 OCR 引擎的真正威力在于返回布局信息——表格、列甚至表单字段。`engine.recognize_structured()` 正是完成此任务的函数，我们会把结果导出为整洁的 JSON 文件。

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

JSON 片段可能如下所示：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*这能为你提供什么：* 机器可读的表示形式，可直接导入数据库、API 或报表工具——再也不需要手动复制粘贴。

## 额外内容：可视化确认（带 Alt 文本的图像）

下面展示了预处理流水线的前后对比快照。注意对比度的提升以及噪声的消失。

![预处理图像用于 OCR – 原始 vs 清理后](/images/ocr_preprocess_example.png){: .align-center alt="预处理图像用于 OCR 示例"}

*如果你感兴趣：* 将 `ocrutil.preprocess` 替换为自己的 OpenCV 实现，仍然遵循相同的 **预处理图像用于 OCR** 思路——阈值化、滤波，然后送入引擎。

## 常见陷阱及规避方法

- **二值化过度：** 阈值设得太高会抹掉淡弱字符。如果出现缺字现象，请降低 `ocrutil.preprocess` 中的阈值。
- **DPI 错误：** OCR 引擎默认约 300 dpi 的打印材料分辨率。如果图像分辨率过低，考虑在预处理前进行放大。
- **跳过自动旋转：** 即使是 5 度的倾斜也会影响行检测。 “auto rotate image OCR” 步骤成本低，却能省去后期大量调试时间。

## 扩展工作流

有了稳固的基础后，你可能想进一步：

1. **添加语言包**（`engine.set_language('eng+spa')`）以处理多语言文档。  
2. **与 Pandas 集成**，将 JSON 表格转为 DataFrame 进行分析。  
3. **批量处理**，遍历文件夹中的图像并将结果追加到主 JSON 文件中。

所有这些扩展仍然依赖核心理念：在调用引擎之前 **预处理图像用于 OCR**。

## 结论

你已经学会了如何在 Python 中 **预处理图像用于 OCR**——自动旋转、二值化、去噪，最后将干净的图片交给 **OCR engine Python**，输出纯文本和丰富的 **OCR structured JSON output**。遵循这些步骤，你将显著提升识别率，并获得可直接用于下游处理的数据。

准备好升级了吗？尝试用自定义的 OpenCV 流水线替代内置的 `ocrutil.preprocess`，实验不同的二值化技术，或将 JSON 导入报表仪表盘。只要有坚实的基础，你再也不会因图像质量问题而卡壳。

祝编码愉快，愿你的 OCR 结果始终清晰锐利！


## 接下来该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助你在已有技巧的基础上进一步深化。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并探索替代实现方案。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}