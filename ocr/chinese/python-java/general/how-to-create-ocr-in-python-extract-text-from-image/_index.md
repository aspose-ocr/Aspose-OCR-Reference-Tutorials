---
category: general
date: 2026-04-26
description: 如何快速可靠地创建 OCR。学习从图像中提取文本、加载用于 OCR 的图像，并使用自定义词典对 PNG 进行 OCR。
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: zh
og_description: 如何在 Python 中创建 OCR 并从图像中提取文本。本指南展示了如何加载用于 OCR 的图像、在 PNG 上运行 OCR，以及使用自定义词典。
og_title: 如何在 Python 中创建 OCR – 快速文本提取
tags:
- OCR
- Python
- Image Processing
title: 如何在Python中创建OCR – 从图像中提取文本
url: /zh/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中创建 OCR – 步骤指南

是否曾好奇 **如何创建 OCR** 来读取你的扫描 PDF、截图或手写笔记？你并不孤单。在许多实际项目中，我们需要 *从图像中提取文本*，但开箱即用的引擎往往在领域专有词汇上表现不佳。  

在本教程中，你将看到一个完整、可直接运行的示例：加载用于 OCR 的图像、应用自定义词典，最后 **在 PNG 文件上运行 OCR**。完成后，你将能够从任意图像中提取文本，并根据自己的术语对引擎进行适配。

## 本教程涵盖内容

我们将逐步演示你需要的每一步：

* 安装体积小巧却功能强大的 `aocr` 包（或任何兼容库）。  
* 配置 **自定义词典**，让 `aspocorp`、`licensekey` 等词汇被识别。  
* **加载用于 OCR 的图像**，支持 PNG、JPEG 或扫描的 PDF 页面。  
* 运行 OCR 过程并打印结果。  

无需外部文档链接，只需一个可复制粘贴、立即运行的完整解决方案。

### 前置条件

* Python 3.8 或更高（代码使用 f‑string）。  
* 基本的命令行使用经验——你需要输入几条 `pip install` 命令。  
* 一张图像文件（示例中的 `technical_doc.png`），放在可引用的位置。  

满足以上三点，即可开始。

---

## 第一步：安装 OCR 库

首先，需要一个支持可编程配置对象的 OCR 引擎。`aocr` 包是对原生 OCR 引擎的轻量封装，演示效果极佳。

```bash
# Install the library (run once)
pip install aocr
```

> **小技巧：** 如果你在 Windows 上遇到编译错误，尝试 `pip install aocr‑binary`，该包提供预编译的 wheel。

### 为什么要安装这个库？

`aocr` 让我们可以直接访问 `config` 对象，并注入 **自定义词典**。这正是提升特定词汇识别准确率的关键。

---

## 第二步：创建 OCR 引擎实例并添加自定义词典

现在启动引擎，并告诉它哪些词应该被视为已知。

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### 为什么自定义词典重要

标准 OCR 模型基于通用语料库训练。当模型遇到 “aspocorp” 时，可能会把它拆成 “aspo corp” 或直接漏掉字母。通过提供自定义列表，我们可以将识别器偏向我们需要的精确拼写，从而大幅降低后处理工作量。

---

## 第三步：加载待处理的图像

这里是 **加载用于 OCR 的图像** 的环节。`Image.load` 方法接受路径字符串，并自动判断文件类型。

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **特殊情况：** 如果你的源文件是多页 PDF，请先使用 `pdf2image` 等工具将每页转换为 PNG，再逐页喂入引擎。

### 提升图像质量的技巧

* 分辨率至少保持在 300 dpi。  
* 确保图像方向正确，必要时使用 `Pillow` 进行旋转。  
* 将彩色扫描转换为灰度，以降低噪声。

---

## 第四步：在 PNG 文件上运行 OCR 过程

在引擎配置完成、图像加载后，我们最终 **在 PNG 上运行 OCR**。

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()` 调用会返回一个对象，包含识别出的文本、置信度分数以及每个单词的边界框。

---

## 第五步：输出识别的文本

查看引擎结果的最简方式是打印 `text` 属性。

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### 预期输出

如果 `technical_doc.png` 中包含句子 *“The Aspocorp licensekey expires on 2025‑12‑31.”*，控制台应显示：

```
The Aspocorp licensekey expires on 2025-12-31.
```

可以看到自定义词典保留了品牌名称——这是普通 OCR 可能会弄乱的地方。

---

## 完整可运行示例（复制粘贴即用）

下面是完整脚本，保存为 `run_ocr.py` 即可。只需将占位路径替换为你的图像实际位置。

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

在终端运行：

```bash
python run_ocr.py
```

你将看到提取的文本打印在控制台，完全与前面的示例一致。

---

## 常见问题解答 (FAQ)

| Question | Answer |
|----------|--------|
| **Can I extract text from a scanned PDF?** | Yes. Convert each page to PNG (or TIFF) first, then feed the images to the same script. |
| **What if my image is a JPEG instead of PNG?** | The `Image.load` method supports JPEG, BMP, TIFF, and PNG out of the box. Just change the file extension. |
| **How do I improve accuracy on low‑contrast scans?** | Pre‑process with `Pillow` – increase contrast, apply binarization, or use `opencv` to deskew. |
| **Is there a way to get confidence scores for each word?** | `ocr_result` includes `words` – each word has a `confidence` attribute you can iterate over. |
| **Can I run this on a headless server?** | Absolutely. `aocr` has no GUI dependencies, making it perfect for CI pipelines. |

---

## 后续步骤与相关主题

既然已经掌握 **如何创建 OCR** 并 **从图像中提取文本**，可以进一步探索：

* **预处理技术** – `load image for OCR` 只是第一步，使用 `opencv` 去噪或锐化。  
* **批量处理** – 循环遍历 PNG 目录，生成可搜索的存档。  
* **多语言支持** – 如需读取法语或德语文档，可为引擎添加语言包。  
* **与 Elasticsearch 集成** – 将提取的文本索引，实现对扫描资产的全文检索。  

这些扩展都基于我们刚才的核心模式，迁移过程轻松无阻。

---

## 小结

短短几分钟，我们已经解答了 **如何创建 OCR**，并可靠地 **从图像文件中提取文本**（尤其是 PNG），演示了如何 **加载用于 OCR 的图像**、应用 **自定义词典**，以及 **在 PNG 上运行 OCR**，且无需任何外部服务。  

运行脚本，调整词典以匹配你的行业术语，你就拥有了文档数字化项目的坚实基础。  

如果遇到任何问题，欢迎在下方留言——我们乐意帮助。别忘了分享你的成功案例，社区最需要真实的实践经验。  

**准备好自动化你的文书工作了吗？** 获取代码，进行适配，从像素转化为可检索的文本，从今天开始！  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}