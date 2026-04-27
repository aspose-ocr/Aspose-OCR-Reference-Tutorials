---
category: general
date: 2026-04-26
description: 如何使用 Python 从图像中提取 OCR —— 一个 Python OCR 示例，展示如何加载图像进行 OCR 并从收据中提取文本。
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: zh
og_description: 如何使用 Python 从图像中提取 OCR。学习一个 Python OCR 示例，加载图像进行 OCR，并在几分钟内从收据中提取文本。
og_title: 如何在 Python 中提取 OCR – 完整指南
tags:
- OCR
- Python
- Image Processing
title: 如何在 Python 中提取 OCR – 步骤教程
url: /zh/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中提取 OCR – 完整指南

Ever wondered **how to extract ocr** from a blurry receipt or a scanned invoice? You're not the only one—developers constantly hit the wall when they need clean, machine‑readable text from images. The good news? With just a few lines of Python you can turn a picture of a receipt into high‑confidence, searchable text.

在本教程中，我们将演示一个 **python ocr example**，展示 **how to load image for ocr**，运行引擎，并仅保留置信度达到 85 % 的字符。完成后，你将能够 **extract text from receipt** 图像，而无需在文档中搜索或猜测 API 参数。

## 所需环境

- Python 3.9 或更高版本（我们使用的语法在 3.8+ 也可工作）
- `aocr` 包（或任何提供 `OcrEngine` 类的 OCR 库）。使用以下方式安装：

```bash
pip install aocr
```

- 示例收据图像（`receipt.png`），放在可引用的文件夹中。
- 文本编辑器或 IDE——VS Code、PyCharm，甚至是简单的 notebook 都可以。

就这么简单。无需重量级框架、外部服务，仅仅是纯 Python。

![高置信度 OCR 结果 – 如何从收据中提取 OCR](/images/ocr-high-confidence.png)

*图片说明：使用 Python OCR 从收据中提取 OCR*

## 步骤 1 – 创建 OCR 引擎实例 (how to extract ocr)

我们首先要启动一个 OCR 引擎。可以把它想象成读取像素的“大脑”。

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** 实例化 `OcrEngine` 会得到一个全新的配置对象。之后你可以调整语言模型、DPI 设置或预处理步骤——全部无需修改核心处理循环。

## 步骤 2 – 加载用于 OCR 的图像

接下来我们将引擎指向要分析的图像。这就是 **load image for ocr** 关键字发挥作用的地方。

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** 如果你的图像位于不同的目录，请使用 `os.path.join` 构建跨平台的路径。

**Why load the image this way?** `Image.load` 辅助函数会将文件读取为引擎可理解的格式，自动处理常见格式（PNG、JPEG、TIFF）。跳过此步骤或直接提供原始字节会抛出 `ValueError`。

## 步骤 3 – 运行 OCR 过程

现在我们真正运行 OCR。`process` 方法返回一个丰富的结果对象，包含识别的符号、置信度分数和边界框。

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** 在大多数库中，它包括：

- `text`：原始的拼接字符串。
- `symbol_confidences`：`(char, confidence)` 元组的列表。
- `boxes`：每个字符的坐标（用于可视化调试）。

获取每个字符的置信度对于下一步至关重要。

## 步骤 4 – 仅保留高置信度符号 (≥ 85 %)

收据常常有污渍、淡印或背景噪声。通过过滤低置信度符号，我们可以显著提升后续解析的效果。

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** 实际经验表明，约 0.85 的阈值在大多数印刷收据上能够平衡召回率和精确率。如果发现数字缺失，可降低阈值；如果出现乱码，则提高阈值。

## 步骤 5 – 输出高置信度提取文本

最后，我们打印（或保存）已清理的字符串。这就是我们 **extract text from receipt** 工作流的核心。

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

典型的输出如下：

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

现在你可以将该字符串输入到 CSV 写入器、数据库或任何后续分析管道中。

## 完整、可直接运行的脚本

下面是完整的代码片段，你可以复制粘贴到 `ocr_receipt.py` 并立即运行。

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

保存文件，确保 `receipt.png` 存在，然后执行：

```bash
python ocr_receipt.py
```

你应该会在控制台看到已清理的收据文本。

## 边缘情况与应对方案

| Situation | Suggested Fix |
|-----------|----------------|
| **整体置信度非常低** | 对图像进行预处理：提升对比度、转换为灰度，或使用去噪滤波器（`cv2.GaussianBlur`）。 |
| **非拉丁字符** | 向 `OcrEngine` 传入语言模型（例如 `ocr_engine.language = "spa"` 表示西班牙语）。 |
| **单张图像中包含多张收据** | 对整张图像运行 OCR，然后使用检测 `\n\n+`（双换行）的正则表达式拆分结果。 |
| **同时需要原始 OCR 文本** | 保留 `ocr_result.text` 与过滤后的版本一起用于调试。 |

## 常见陷阱（以及如何避免）

- **忘记安装库** – 在导入之前必须成功执行 `pip install aocr`。
- **在 Windows 上使用错误的路径分隔符**（`\` 与 `/`），请使用 `os.path.join`。
- **硬编码置信度阈值** 而未进行测试 —— 首先在几张收据上进行快速的可视化检查。
- **忽略 Unicode 正规化** —— 某些收据包含特殊的破折号字符；如果计划存储输出，请运行 `unicodedata.normalize('NFKC', text)`。

## 下一步 – 超越基础

既然你已经了解了如何从单张收据中 **how to extract ocr** 数据，接下来可能想要：

1. **批量处理收据文件夹** – 循环遍历所有 PNG/JPG 文件，并将每个结果写入 CSV。
2. **与数据库集成** – 将 `high_confidence_text` 存入 SQLite，以便快速查询。
3. **应用自然语言解析** – 使用正则或 `dateutil` 提取日期、总额和税额。
4. **尝试其他库** – 如果需要多语言支持或更高精度，可使用 `pytesseract`、`easyocr` 或云服务（Google Vision、Azure OCR）。

上述每个主题自然都包含我们的次要关键词：*python ocr example*、*extract text from receipt*、*load image for ocr* 和 *how to use OCR*。

## 结论

我们刚刚完整演示了一个 **python ocr example**，展示了如何 **how to extract ocr** 收据图像中的文本，过滤低置信度符号，并输出干净的结果。步骤简洁，代码独立，方法足够灵活，可适配更大的项目。

使用自己的收据尝试一下，调整置信度阈值，然后扩展到批量处理。如果遇到奇怪的情况——比如淡淡的徽标或不常见的字体——请记住上面的边缘情况提示。祝编码愉快，愿你的 OCR 流程始终精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}