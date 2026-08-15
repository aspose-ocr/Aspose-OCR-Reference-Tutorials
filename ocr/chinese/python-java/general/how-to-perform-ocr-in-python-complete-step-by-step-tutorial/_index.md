---
category: general
date: 2026-03-26
description: 学习如何在 Python 中进行 OCR 并识别图像文件中的文本。本指南展示了如何快速从 PNG 中提取文本并将图像转换为文本。
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: zh
og_description: 如何在 Python 中执行 OCR？请按照本指南识别图像中的文字，从 PNG 中提取文本，并使用试用许可证将图像转换为文本。
og_title: 如何在 Python 中进行 OCR – 完整教程
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中进行 OCR – 完整的逐步教程
url: /zh/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中执行 OCR – 完整分步教程  

有没有想过 **如何对手机刚拍的图片进行 OCR**？你并不孤单——全球的开发者都需要一种可靠的方式，从图像文件中识别文字，而不必与复杂的本地库纠缠。  

在本教程中，我们将通过一个实战示例，展示 **如何执行 OCR**、**从图像中识别文字**，以及 **从 PNG 中提取文本**，使用轻量级的 Python 包装器。完成后，你只需几行代码即可 **将图像转换为文本**，而且无需担心授权问题，因为我们将使用内置的试用模式。

## 你将学到  

* 如何为 OCR 引擎设置试用许可证（无需文件路径）。  
* 调用 **从图像中识别文字** 对象的完整顺序。  
* 如何 **从 PNG 中提取文本** 并处理常见的字体缺失等陷阱。  
* 在从试用版迁移到正式版许可证时的扩展技巧。  

**先决条件** – 需要 Python 3.8+ 和 `ocr` 包（可通过 `pip install ocr` 安装）。不需要其他外部工具。

---  

![how to perform OCR example](https://example.com/ocr-demo.png "how to perform OCR in Python – recognized text displayed")  

*图片替代文字：在 Python 中执行 OCR – 示例输出*  

## 第一步 – 激活试用许可证（无需文件路径）  

在引擎能够读取任何内容之前，需要一个有效的许可证。试用模式非常适合实验和小型项目。

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*为什么重要：* 许可证对象告诉 OCR 库你正在沙箱环境中运行。如果跳过此步骤，调用 `recognize()` 时引擎会抛出 `LicenseError`。  

**小贴士：** 当你切换到付费许可证时，将上面的两行代码替换为 `ocr.License("path/to/your/license.key").apply()`。

## 第二步 – 创建 OCR 引擎实例  

试用许可证激活后，我们实例化主引擎。可以把它看作会查看图像并决定字符位置的“大脑”。

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*为什么重要：* `OcrEngine` 保存语言包、DPI 等配置信息。你可以稍后进行微调，但默认设置已能满足大多数仅含英文的 PNG。

## 第三步 – 加载要处理的 PNG  

这里就是 **从图像中识别文字** 的地方。`ocr.Imaging.Image.load()` 方法支持 PNG、JPEG、BMP 等多种格式。

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*边缘情况：* 如果你的 PNG 使用索引调色板（截图常见），加载器会自动将其转换为 24 位 RGB 缓冲区。此转换会带来轻微的性能开销，但能保证 OCR 结果的准确性。

## 第四步 – 运行 OCR 并获取文本  

最后，让引擎执行识别，然后提取纯文本结果。

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**预期输出**（示例：包含 “Hello World” 的简单图像）：

```
Hello World
```

如果图像包含多行，输出会保留换行符，便于后续处理，如 CSV 解析器或 NLP 流水线。

## 可选：微调以提升准确率  

* **语言包：** `ocr_engine.set_language("eng")`（默认）或 `"fra"`（法语）。  
* **DPI 缩放：** `ocr_engine.set_dpi(300)` 可改善低分辨率扫描的识别效果。  
* **预处理：** 在 `set_image` 前使用二值阈值 `ocr.Imaging.Image.threshold()` 往往能在噪声背景下得到更干净的文本。

这些调整在你从快速演示转向生产级 **ocr tutorial python**、每日处理数百文件时尤为有用。

## 完整脚本 – 直接复制粘贴使用  

下面是整合上述所有步骤的可运行脚本。将其保存为 `run_ocr.py`，并将 `YOUR_DIRECTORY/sample1.png` 替换为你自己的 PNG 路径。

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

在命令行运行：

```bash
python run_ocr.py
```

你应该会在控制台看到提取的文本。如果得到空字符串，请检查图像是否确实包含清晰的高对比度文字，以及试用许可证是否成功应用。

## 常见问题与陷阱  

* **“JPEG 能用吗？”** – 完全可以。`load()` 方法会自动检测格式，你可以直接把 PNG 换成 JPEG 而无需修改代码。  
* **“图像如果被旋转了怎么办？”** – 引擎可以自动检测方向，但为了获得最佳效果，你可以在 `set_image` 前使用 `input_image.rotate(90)` 进行预旋转。  
* **“能在循环中处理多张图片吗？”** – 能。只需将加载和 `recognize()` 调用放入 `for` 循环；同一个 `ocr_engine` 实例可以重复使用，能略微减少开销。  

## 后续步骤 – 从演示到生产  

既然你已经掌握 **如何执行 OCR**，可以进一步探索以下主题：

* **批量处理** – 将此脚本与 `os.listdir()` 结合，**批量提取 PNG 文本**。  
* **与 PDF 集成** – 使用 `pdf2image` 将 PDF 页面转换为 PNG，再喂入同一流水线。  
* **后处理** – 使用正则或模糊匹配清理常见的 OCR 误识（例如 “0” 与 “O” 的混淆）。  

这些都基于 **将图像转换为文本** 的核心思路，能够大幅提升 OCR 工作流的实用性。

---  

### TL;DR  

我们已经覆盖了在 Python 中 **如何执行 OCR** 所需的全部步骤：激活试用许可证、创建引擎、加载 PNG、运行识别并打印结果。只需几行代码，你就可以 **从图像中识别文字**、**从 PNG 中提取文本**，以及 **将图像转换为文本**，供后续任何应用使用。  

尝试一下，调节 DPI 或语言设置，让引擎为你完成繁重的工作。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}