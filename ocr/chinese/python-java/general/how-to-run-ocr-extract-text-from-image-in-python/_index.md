---
category: general
date: 2026-03-26
description: 如何对 PNG 文件进行 OCR 并使用自定义词典提取图像文本，以提升 OCR 准确率。学习快速加载图像进行 OCR。
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: zh
og_description: 如何对 PNG 文件运行 OCR 并使用自定义词典提取图像文本，以提升 OCR 准确率。一步步指南。
og_title: 如何运行 OCR – 在 Python 中从图像提取文本
tags:
- OCR
- Python
- Image Processing
title: 如何运行 OCR——在 Python 中从图像提取文本
url: /zh/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中运行 OCR – 从图像中提取文本

有没有想过 **如何运行 OCR** 在扫描的发票或截图上，并获得干净、可搜索的文本？你并不孤单。在许多项目中，瓶颈往往只是为 OCR 加载图像，然后诱导引擎理解特定领域的词汇。  

在本教程中，我们将逐步演示一个完整、可直接运行的示例，**从图像文件中提取文本**，展示如何 **从 PNG 资源中识别文本**，并演示使用自定义词典和特殊字符来 **提升 OCR 准确率** 的技巧。完成后，你将拥有一个可直接放入任何 Python 代码库的独立脚本。

## 你需要的环境

- Python 3.8+（代码使用类型提示，但在更早的 3.x 版本上也能运行）
- 针对你所使用的 OCR 引擎的 `ocr` 库（通过 `pip install ocr‑engine` 安装——请替换为实际的包名）
- 要处理的图像文件（`input.png`）
- 可选：包含领域特定词汇的纯文本文件（`invoice_terms.txt`），每行一个词

无需繁重的外部依赖，也不需要云 API 密钥，只需本地 OCR 引擎。

---

## 步骤 1：安装并导入 OCR 库

首先，确保已安装 OCR 包。如果你使用的是假设的 `ocr-engine` 包，运行以下命令：

```bash
pip install ocr-engine
```

现在导入你需要的类：

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **小技巧：** 如果你使用虚拟环境，请在安装前激活它，以保持全局 Python 环境的整洁。

## 步骤 2：创建 OCR 引擎实例

创建引擎对象是所有 OCR 任务的入口。可以把它看作在软件中打开扫描仪硬件。

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

为什么这很重要：引擎保存了语言包、识别模式以及后续将要附加的自定义资源等配置。没有它，你就无法 **load image for OCR** 或运行识别流水线。

## 步骤 3：加载要识别的图像

这里我们实际执行 **load image for OCR**。`Imaging.Image.load()` 方法读取文件并将其转换为引擎期望的内部位图格式。

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

如果是 JPEG 或 TIFF，同样的方法也适用——只需更改扩展名。引擎会自动检测格式。

> **特殊情况：** 非常大的图像（超过 5 MP）可能导致内存激增。如果遇到性能问题，考虑在加载前使用 Pillow 进行下采样。

## 步骤 4：提供自定义词典以提升准确率

大多数 OCR 引擎都附带通用语言模型。对于发票、收据或法律文件，常会出现漏识的词汇。提供自定义词表可以告诉引擎“这些词是合法的，请视为正确”。

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

典型的条目可能是：

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

添加这些条目可以显著提升 **improve OCR accuracy** 指标——尤其是对非 ASCII 符号。

## 步骤 5：添加默认集合未覆盖的特殊字符

如果你的领域使用欧元符号 (€) 或斯堪的纳维亚字母 Ø 等符号，可以显式添加它们：

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

引擎将在识别阶段将这些字形视为有效，从而降低出现“乱码”输出的概率。

## 步骤 6：运行 OCR 过程并获取文本

最后，调用识别器并获取纯文本结果。`recognize()` 调用返回一个丰富的对象；对于大多数用例，我们只需要原始字符串。

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**预期输出**（为简洁起见已截断）：

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

如果输出出现乱码，请再次确认自定义词典和特殊字符已正确加载。

---

## 可视化概览

![如何运行 OCR 图示](ocr-workflow.png){alt="如何运行 OCR 图示"}

上图展示了从加载图像到获取干净文本的流程，并突出显示了可以注入自定义词典和字符集的位置。

---

## 常见问题与注意事项

### 这在多页 PDF 上有效吗？

是的——只需将每页转换为 PNG（使用 `pdf2image` 或类似工具），并依次传入同一个 `ocr_engine` 实例。引擎会独立处理每张图像，返回一个字符串列表，你可以将其拼接。

### 如果图像被旋转了怎么办？

大多数现代 OCR 引擎会自动检测方向，但你也可以使用以下方式强制旋转：

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### 如何处理非英语语言？

在加载图像前切换语言模型：

```python
ocr_engine.set_language("de")  # German
```

确保已安装相应的语言包。

---

## 完整脚本 – 可直接复制粘贴

下面是完整程序，替换占位路径后即可运行。

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

使用以下方式运行：

```bash
python run_ocr.py
```

你应该会在控制台看到提取的文本。随后可以将其写入文件、写入数据库，或传递给下游的 NLP 流程。

---

## 回顾与后续步骤

我们已经介绍了在 PNG 上 **how to run OCR**，如何 **extract text from image**，并展示了在使用词典和自定义字符 **improving OCR accuracy** 的同时 **recognize text from PNG** 的实用方法。  

接下来，可以考虑：

- **批量处理：**遍历图像目录。
- **后处理：**使用正则提取发票号或日期。
- **集成：**将脚本挂接到 Flask API，实现按需 OCR 服务。

如果你对更高级的主题感兴趣，可以查看使用 OpenCV 预处理的 **load image for OCR** 教程，或深入了解基于深度学习的 OCR 模型，如带 LSTM 层的 Tesseract 4+。

---

### 持续实验！

尝试将 `invoice_terms.txt` 替换为医学术语列表，添加希腊字符，或给引擎喂入低分辨率照片，观察准确率的极限。你动手实验得越多，就越能理解预处理、自定义词汇和引擎设置之间的权衡。

祝编码愉快，愿你的 OCR 结果始终清晰！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}