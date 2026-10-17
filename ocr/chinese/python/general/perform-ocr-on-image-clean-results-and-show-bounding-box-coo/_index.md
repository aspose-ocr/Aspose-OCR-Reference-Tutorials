---
category: general
date: 2026-03-28
description: 对图像执行 OCR 并获取带有边界框坐标的干净文本。学习如何提取 OCR、清理 OCR，并一步步显示结果。
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: zh
og_description: 对图像进行 OCR 识别，清理输出，并在简明教程中显示边界框坐标。
og_title: 对图像进行 OCR – 干净的结果和边界框
tags:
- OCR
- Computer Vision
- Python
title: 对图像进行 OCR – 清理结果并显示边界框坐标
url: /zh/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 对图像执行 OCR – 清理结果并显示边界框坐标

是否曾需要 **对图像执行 OCR**，却总是得到杂乱的文本并且不确定每个单词在图片中的位置？你并不孤单。在许多项目中——发票数字化、收据扫描或简单的文本提取——获取原始 OCR 输出只是第一道障碍。好消息是？你可以清理这些输出，并立即看到每个区域的边界框坐标，而无需编写大量样板代码。

在本指南中，我们将逐步演示 **如何提取 OCR**，运行 **如何清理 OCR** 的后处理器，最后 **显示每个清理后区域的边界框坐标**。完成后，你将拥有一个可直接运行的脚本，将模糊的照片转换为整洁、结构化的文本，准备好进行后续处理。

## 你需要准备的内容

- Python 3.9+（下面的语法在 3.8 及以上版本均可运行）
- 支持 `recognize(..., return_structured=True)` 的 OCR 引擎——例如本文代码片段中使用的虚构 `engine` 库。请将其替换为 Tesseract、EasyOCR 或任何返回区域数据的 SDK。
- 对 Python 函数和循环有基本了解
- 一张你想要扫描的图像文件（PNG、JPG 等）

> **专业提示：** 如果使用 Tesseract，`pytesseract.image_to_data` 已经提供了边界框。你可以将其结果包装成一个小适配器，以模拟下文展示的 `engine.recognize` API。

---

![对图像执行 OCR 示例](image-placeholder.png "对图像执行 OCR 示例")

*Alt text: 展示如何对图像执行 OCR 并可视化边界框坐标的示意图*

## 第一步 – 对图像执行 OCR 并获取结构化区域

首先，让 OCR 引擎返回的不仅是纯文本，而是一个结构化的文本区域列表。该列表包含原始字符串以及包围它的矩形。

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**为什么这很重要：**  
仅请求纯文本会丢失空间位置信息。结构化数据让你后续能够 **显示边界框坐标**、将文本与表格对齐，或将精确位置提供给下游模型。

## 第二步 – 使用后处理器清理 OCR 输出

OCR 引擎擅长识别字符，但常会留下多余空格、换行符或误识别的符号。后处理器会对文本进行规范化，修正常见 OCR 错误，并去除多余空白。

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

如果你自行实现清理器，可以考虑：

- 删除非 ASCII 字符（`re.sub(r'[^\x00-\x7F]+',' ', text)`）
- 将多个空格合并为单个空格
- 使用 `pyspellchecker` 等拼写检查器纠正常见拼写错误

**为什么你应该在意：**  
整洁的字符串使搜索、索引以及后续的 NLP 流程更加可靠。换句话说，**如何清理 OCR** 往往决定了数据集是可用还是让人头疼。

## 第三步 – 为每个清理后的区域显示边界框坐标

文本整理完毕后，我们遍历每个区域，打印其矩形以及清理后的字符串。这一步就是最终 **显示边界框坐标** 的地方。

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**示例输出**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

现在，你可以将这些坐标传入绘图库（例如 OpenCV）在原图上绘制框，或将其存入数据库以供后续查询。

## 完整、可直接运行的脚本

下面是把上述三步整合在一起的完整程序。请将占位的 `engine` 调用替换为你实际使用的 OCR SDK。

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### 如何运行

```bash
python perform_ocr.py sample_invoice.jpg
```

你应该会看到一系列边界框与清理后文本的对应列表，正如上面的示例输出所示。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| **What if the OCR engine doesn’t support `return_structured`?** | Write a thin wrapper that converts the engine’s raw output (usually a list of words with coordinates) into objects with `text` and `bounding_box` attributes. |
| **Can I get confidence scores?** | Many SDKs expose a confidence metric per region. Append it to the print statement: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **How to handle rotated text?** | Pre‑process the image with OpenCV’s `cv2.minAreaRect` to deskew before calling `recognize`. |
| **What if I need the output in JSON?** | Serialize `processed_result.regions` with `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Is there a way to visualize the boxes?** | Use OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` inside the loop, then `cv2.imwrite("annotated.jpg", img)`. |

## 小结

你刚刚学习了 **如何对图像执行 OCR**、清理原始输出，并 **显示每个区域的边界框坐标**。这套三步流程——识别 → 后处理 → 遍历——是一个可复用的模式，能够轻松嵌入任何需要可靠文本提取的 Python 项目。

### 接下来可以做什么？

- **探索不同的 OCR 后端**（Tesseract、EasyOCR、Google Vision），比较准确率。
- **与数据库集成**，将区域数据存储用于可搜索的档案。
- **添加语言检测**，为每个区域路由到合适的拼写检查器。
- **在原图上叠加框** 进行可视化验证（参见上面的 OpenCV 代码片段）。

如果遇到奇怪的情况，请记住，最大的收益来自稳固的后处理步骤；干净的字符串远比原始字符堆更易于后续操作。

祝编码愉快，愿你的 OCR 流程始终保持整洁！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}