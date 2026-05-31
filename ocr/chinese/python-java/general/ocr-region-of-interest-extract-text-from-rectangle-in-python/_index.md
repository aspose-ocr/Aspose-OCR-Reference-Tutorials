---
category: general
date: 2026-05-31
description: 了解如何使用 OCR 感兴趣区域加载图像进行 OCR，并从矩形中提取文本，完美适用于识别发票上的金额。
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: zh
og_description: 掌握 OCR 感兴趣区域，加载图像进行 OCR，从矩形中提取文本，并在单个教程中识别发票文本。
og_title: OCR感兴趣区域 – Python逐步指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR感兴趣区域 – 在Python中从矩形提取文本
url: /zh/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 感兴趣区域 – 在 Python 中从矩形提取文本

有没有想过如何 **ocr region of interest** 扫描发票的特定部分，而不必将整页输入引擎？你并不是第一个盯着模糊收据并思考“如何提取位于右下角的金额？”的人。好消息是，你可以告诉 OCR 库确切的查找位置，从而显著提升速度和准确性。

在本指南中，我们将通过一个完整、可运行的示例，展示如何 **load image for OCR**、定义 **region of interest**，然后 **extract text from rectangle**，最终 **recognize text from invoice**，并回答经典的“如何提取金额”问题。没有模糊的引用——只有具体的代码、清晰的解释，以及一些你希望早些知道的专业技巧。

---

## 你将构建的内容

通过本教程的学习，你将拥有一个小型的 Python 脚本，能够：

1. 从磁盘加载发票图像。  
2. 标记总金额所在的矩形 ROI。  
3. 仅在该 ROI 内运行 OCR。  
4. 打印清理后的金额字符串。  

所有这些都适用于任何支持 ROI 的 OCR 库——这里我们使用一个虚构但具代表性的 `SimpleOCR` 包，它模拟了 Tesseract 或 EasyOCR 等流行工具。随意替换它；概念保持不变。

---

## 前置条件

- 已安装 Python 3.8+（`python --version` 应显示 ≥3.8）。  
- 可通过 pip 安装的 OCR 包（例如 `pip install simpleocr`）。  
- 放置在可引用文件夹中的发票图像（PNG 或 JPEG）。  
- 对 Python 函数和类有基本了解（无需高级技巧）。

如果你已经具备这些，太好了——让我们开始吧。如果没有，先获取图像；其余步骤与实际文件内容无关。

---

## 步骤 1：加载用于 OCR 的图像

任何 OCR 工作流的第一步都是需要一个位图作为读取来源。大多数库提供一个接受文件路径的简单 `load_image` 方法。下面是使用我们的 `SimpleOCR` 引擎的做法：

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **专业提示：** 使用绝对路径或 `os.path.join`，以避免在从不同工作目录运行脚本时出现 “file not found” 的意外。

---

## 步骤 2：定义 OCR 感兴趣区域

我们不让引擎扫描整页，而是明确告诉它金额所在的*确切*位置。这一步是 **ocr region of interest**，是实现可靠提取的关键，尤其当文档包含嘈杂的页眉或页脚时。

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

为什么是这些数字？`x` 和 `y` 是相对于左上角的像素偏移，而 `width` 和 `height` 描述了框的尺寸。如果不确定，可以在任意编辑器中打开图像，启用标尺并记录坐标。许多 IDE 甚至在悬停时显示光标位置。

---

## 步骤 3：从矩形提取文本

现在 ROI 已设置，我们让引擎 **recognize text from invoice**，但仅限于我们刚刚添加的矩形。该调用返回一个结果对象，通常包含原始字符串、置信度分数，有时还有边界框。

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

在内部，`recognize()` 会遍历每个 ROI，裁剪相应区域，运行 OCR 模型，并将结果拼接起来。这就是为什么定义一个紧凑的 **extract text from rectangle** 区域可以为批处理作业节省数秒的原因。

---

## 步骤 4：如何提取金额 – 清理输出

OCR 并非完美；你经常会得到多余的空格、换行，甚至误读的字符（比如 “S” 与 “5”）。快速使用 `strip()` 加上一个小正则表达式通常即可处理货币值。

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **为何重要：** 如果你打算将金额写入数据库或支付网关，需要一个可预测的格式。去除空白并过滤非数字字符可以防止后续错误。

---

## 步骤 5：识别发票文本 – 完整脚本

将所有步骤整合在一起，下面是完整的可直接运行的脚本。将其保存为 `extract_amount.py` 并执行 `python extract_amount.py`。

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### 预期输出

```
Amount: 1,245.67
```

如果 ROI 对齐不正确，你可能会看到类似 `Amount: 1245.6S` 的输出——注意多余的 “S”。调整矩形坐标并重新运行，直至输出整洁。

---

## 常见陷阱与边缘情况

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI 太小** | 金额文本被裁剪，导致识别不完整。 | 将 `width`/`height` 扩大约 10‑20 % 并重新测试。 |
| **DPI 不正确** | 低分辨率扫描（≤150 dpi）降低 OCR 准确度。 | 在加载前将图像重新采样至 300 dpi，或让扫描仪使用更高 DPI。 |
| **多种货币** | 正则表达式匹配到第一个数字组，可能是发票号。 | 优化正则，使其在数字前查找货币符号（`$`, `€`, `£`）。 |
| **发票旋转** | OCR 引擎假设文本是正向的，旋转的页面会导致识别失败。 | 在添加 ROI 前使用旋转校正（`ocr_engine.rotate(90)`）。 |
| **背景噪声** | 阴影或印章会干扰模型。 | 使用简单阈值预处理（`cv2.threshold`）或去噪滤波。 |

提前处理这些边缘情况可以为你节省后续数小时的调试时间。

---

## 实际项目的专业技巧

- **批量处理：**遍历发票文件夹，动态计算 ROI（例如基于模板检测），并将结果存入 CSV。  
- **模板匹配：**如果处理多种发票布局，维护一个 `template_id → ROI coordinates` 的 JSON 映射。根据快速布局分类器切换 ROI。  
- **并行执行：**使用 `concurrent.futures.ThreadPoolExecutor` 并发运行多个 OCR 实例——适用于高吞吐量的后台流水线。  
- **置信度过滤：**大多数 OCR 结果包含置信度分数。丢弃低于阈值（如 85 %）的结果，并标记为手动复审。

---

## 结论

我们已经覆盖了实现 **ocr region of interest**、**load image for OCR**、**extract text from rectangle**，以及最终 **recognize text from invoice**，以回答经典的 **how to extract amount** 问题所需的全部内容。该脚本简洁但足够灵活，可适配不同的文档格式、语言和 OCR 后端。

既然你已经掌握了基础，考虑扩展工作流：添加条形码扫描、集成 PDF 解析器，或将提取的金额推送到会计 API。无限可能，而通过明确定义的 ROI，你始终能获得更快、更清晰的结果。

如果遇到问题，请在下方留言——祝你 OCR 愉快！

![OCR 感兴趣区域示例](https://example.com/ocr_roi_example.png "OCR 感兴趣区域示例")

## 接下来你应该学习什么？

- [通过在 OCR 中准备矩形来提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [使用 Aspose.OCR 检测区域模式在 Java 中提取图像文本](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [提取图像文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}