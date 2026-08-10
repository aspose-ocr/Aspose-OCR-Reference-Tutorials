---
category: general
date: 2026-05-03
description: 使用 Aspose OCR 即时提取图像中的文本。学习如何定义感兴趣区域、加载图像进行 OCR，并在几分钟内从发票中提取文本。
draft: false
keywords:
- extract text from image
- define region of interest
- load image for ocr
- extract text from invoice
- process image with ocr
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本。本指南展示如何定义感兴趣区域、加载图像进行 OCR，以及高效地从发票中提取文本。
og_title: 使用 Aspose OCR 从图像中提取文本 – 完整教程
tags:
- ocr
- python
- image-processing
title: 使用 Aspose OCR 从图像中提取文本 – 步骤指南
url: /zh/python-java/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像中提取文本 – 步骤指南

需要 **快速从图像中提取文本** 吗？你并不孤单——开发者经常要应对噪声扫描件、收据和发票。在本教程中，我们将完整演示一个解决方案，既展示如何 *从图像中提取文本*，又演示如何 **定义感兴趣区域 (ROI)**、**加载图像进行 OCR**，以及如何从发票中提取所需的精确行。

我们将覆盖从安装 Aspose OCR 库到处理旋转页面等边缘情况的全部内容。完成后，你将拥有一个可直接运行的脚本，只需一次调用即可提取目标文本——无需手动裁剪。

## 你将学到

- 如何使用 Aspose 的 Python API **加载图像进行 OCR**。  
- 最佳的 **定义感兴趣区域 (ROI)** 方法，只处理图片中重要的部分。  
- 如何 **从发票中提取文本** 字段，而不必读取整页。  
- 高效 **处理图像与 OCR** 的技巧，避免常见陷阱。  

**先决条件** – 最近的 Python 3.9+ 环境、有效的 Aspose OCR 许可证文件，以及一张图像（例如发票 PNG）。不需要其他外部工具。

---

## 第一步 – 初始化 OCR 引擎（基础设置）

在 **处理图像与 OCR** 之前，需要一个持有许可证的引擎实例。这一步至关重要，因为未授权的引擎只能返回有限的结果集。

```python
import aspose.ocr as ocr  # Make sure you installed aspose-ocr via pip

# Create the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with your actual .lic file location
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

*为什么重要*：`OcrEngine` 对象是库的核心；它管理语言模型、图像预处理和授权。提前设置许可证可确保获得完整的准确度且不会出现水印。

---

## 第二步 – 加载图像进行 OCR

引擎准备好后，我们需要 **加载图像进行 OCR**。Aspose 支持多种格式（PNG、JPEG、TIFF），但使用 `Image.from_file` 能保证图像被正确解码。

```python
# Load the target image – change the path to point at your invoice file
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.from_file(image_path)
```

> **专业提示**：将图像文件保持在 5 MB 以下可获得最快的处理速度。更大的文件可以在 OCR 前使用 `image.resize(width, height)` 进行降采样。

---

## 第三步 – 定义感兴趣区域 (ROI)

大多数发票包含大量无关文字——地址块、页脚等。通过 **定义感兴趣区域**，我们告诉引擎只在金额或日期所在的位置进行识别，从而提升速度和准确度。

```python
# Define ROI: (x, y, width, height) in pixels
# Adjust these numbers based on the layout of your specific invoice
roi = ocr.Rectangle(150, 300, 400, 120)
```

*工作原理*：`Rectangle` 类在虚拟上裁剪图像；OCR 引擎永远不会看到矩形之外的像素，因此 ROI 之外的噪声会被忽略。

---

## 第四步 – 识别 ROI 内的文本

在引擎、图像和 ROI 都准备好后，我们终于可以 **从图像中提取文本**。`recognize` 方法返回一个 `OcrResult` 对象，包含检测到的字符串和置信度分数。

```python
# Perform OCR only within the defined ROI
ocr_result = ocr_engine.recognize(image, roi=roi)

# Print the raw extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

**预期输出**（典型发票合计行示例）：

```
Text inside ROI:
Total Amount: $1,245.67
```

如果 ROI 定位正确，你将只看到所需的那一行——没有其他内容。

---

## 第五步 – 完整可运行示例（复制粘贴即用）

下面是把前面所有步骤串联起来的完整脚本。将其保存为 `extract_invoice_roi.py` 并运行 `python extract_invoice_roi.py`。

```python
# extract_invoice_roi.py
import aspose.ocr as ocr

def main():
    # 1️⃣ Initialize OCR engine and apply license
    ocr_engine = ocr.OcrEngine()
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image you want to process
    image = ocr.Image.from_file("YOUR_DIRECTORY/invoice.png")

    # 3️⃣ Define the region of interest (ROI) – rectangle where the text lives
    roi = ocr.Rectangle(150, 300, 400, 120)   # (x, y, width, height)

    # 4️⃣ Recognize text only inside the ROI
    ocr_result = ocr_engine.recognize(image, roi=roi)

    # 5️⃣ Display the extracted text
    print("Text inside ROI:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

运行脚本后，你应该在控制台看到目标行的输出。如果得到空字符串，请再次检查 ROI 坐标——偏差几像素就可能导致文本被完全排除。

---

## 第六步 – 常见变体与边缘情况

### a) 不同的发票布局  
不同供应商的发票往往会把合计金额框放在不同位置。要在多种布局下 **处理图像与 OCR**，可以考虑：

- **多个 ROI**：依次使用多个矩形运行引擎，并挑选置信度最高的结果。  
- **动态 ROI 检测**：使用轻量级图像处理库（如 OpenCV）先定位 “Total” 标签，然后相对计算 ROI。

### b) 旋转或倾斜的图像  
如果扫描件倾斜，在识别前调用 `image.rotate(angle)`：

```python
image = image.rotate(2.5)  # Rotate 2.5 degrees clockwise
```

Aspose OCR 也提供自动去倾斜功能，但手动旋转可以让你获得更精细的控制。

### c) 非拉丁字符  
默认语言模型是英语。要 **从发票中提取文本**（其他语言），请在识别前设置语言：

```python
ocr_engine.language = ocr.Language.French  # Example for French invoices
```

### d) 大型 PDF  
处理多页 PDF 时，先将每页提取为图像（Aspose PDF → Image），然后对每页使用相同的 ROI 逻辑。

---

## 第七步 – 性能技巧与专业提示

- **缓存引擎**：在循环中反复创建 `OcrEngine` 会拖慢速度。实例化一次后重复使用。  
- **批量处理**：如果有数十份发票，可将 OCR 调用包装在 `ThreadPoolExecutor` 中，实现 I/O‑bound 并行。  
- **置信度检查**：`ocr_result.confidence` 返回 0 到 1 之间的浮点数。将低于 0.85 的结果视为失败，并回退到更大的 ROI 或人工复核。  

> **注意**：ROI 设得过小可能会截断字符，导致输出乱码。务必先在少量样本发票上测试后再大规模使用。

---

## 结论

现在，你已经掌握了使用 Aspose OCR **从图像中提取文本** 的完整、可投入生产的方法，涵盖 **定义感兴趣区域**、**加载图像进行 OCR**，以及可靠 **从发票中提取文本** 的技巧。通过将 OCR 限制在紧凑的 ROI 内，你可以同时提升速度和准确度——这对于批量处理成千上万张收据尤为理想。

准备好下一步了吗？尝试将此脚本集成到 Flask API 中，让你的 Web 应用能够上传发票并即时返回合计金额。或者实验多个 ROI，一次性提取日期、发票号和供应商名称。可能性无限，只要掌握了这里的基础，你就能应对任何 OCR 挑战。

祝编码愉快，愿你的提取文本始终干净整洁！  

![Workflow diagram showing how to extract text from image using Aspose OCR](workflow.png){: .center-image alt="使用 Aspose OCR 从图像中提取文本的工作流"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}