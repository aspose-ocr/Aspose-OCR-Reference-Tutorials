---
category: general
date: 2026-01-12
description: 使用 Python 快速对 PNG 文件进行 OCR。了解如何从图像和发票中提取文本，并使用 Aspose.OCR 加载图像进行 OCR。
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: zh
og_description: 即时对 PNG 进行 OCR。本指南展示了如何从图像和发票中提取文本、加载图像进行 OCR，并将结果保存为 JSON 和 CSV。
og_title: 在 PNG 上运行 OCR – 完整的 Python 教程
tags:
- OCR
- Python
- Image Processing
title: 在 PNG 上运行 OCR – 完整的 Python 图像文字提取指南
url: /zh/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PNG 上运行 OCR – 完整的 Python 指南，提取图像中的文本

是否曾需要 **在 PNG 上运行 OCR**，却不确定哪个库能提供干净、结构化的结果？你并不孤单。在许多真实项目中——比如发票自动化或收据扫描——第一步就是 **从图像中提取文本**，而 PNG 是常用格式，因为它保持无损质量。

在本教程中，我们将使用 Aspose.OCR Python 包进行动手示例。阅读完本指南后，你将了解如何 **加载图像进行 OCR**、提取每一行文本、将数据转换为整洁的 JSON 对象，甚至导出为 CSV 以供后续处理。没有冗余，只提供实用、可直接运行的解决方案。

## 你将学到

- 如何安装并导入 Aspose.OCR 库。  
- **在 PNG 上运行 OCR** 的完整步骤以及如何处理结果对象。  
- **从发票中提取文本** 的方法，并将输出格式化为 JSON 或 CSV。  
- 处理低对比度图像、多语言文档以及置信度分数的技巧。  
- 一个完整的、可直接复制粘贴并立即执行的代码示例。

> **先决条件：** Python 3.8+，并且对 pip 有基本了解。如果你从未使用过 Aspose，也无需担心——本指南涵盖了入门所需的一切。

---

## 第一步 – 安装 Aspose.OCR 并准备环境

在我们能够 **在 PNG 上运行 OCR** 之前，需要先在系统中安装该库。

```bash
pip install aspose-ocr
```

> **专业提示：** 使用虚拟环境 (`python -m venv venv`) 来隔离依赖。这可以避免在处理多个项目时出现版本冲突。

安装完成后，导入我们需要的模块：

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

这里我们引入 `asposeocr` 来完成核心工作，并使用内置的 `json` 库进行后续序列化。

---

## 第二步 – 创建 OCR 引擎并设置语言

OCR 引擎是实际读取像素的核心组件。对于大多数英文发票，你需要使用英文语言包：

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **为什么重要：** 指定语言会缩小字符集范围，从而提升准确率并加快处理速度。如果需要处理多语言发票，只需将 `ocr.Language.ENGLISH` 替换为相应的枚举即可。

---

## 第三步 – 加载图像进行 OCR

现在我们将 **加载图像进行 OCR**。`Image.load` 方法接受文件路径，支持 PNG、JPEG、BMP 等多种格式。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **边缘情况：** 如果 PNG 文件异常大（超过 5 MB），建议先进行缩放以控制内存使用。Pillow 可以用一行代码完成：

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## 第四步 – 在 PNG 上运行 OCR 并获取结果

引擎准备好、图像已加载后，就可以 **在 PNG 上运行 OCR** 并获取结构化结果了。

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` 对象包含一系列 `OcrRegion` 项目，每个项目都有识别出的文本和置信度分数（0‑100）。这正是你从 **发票中提取文本** 所需的细粒度数据。

---

## 第五步 – 将结果转换为 JSON 并美化输出

大多数下游系统都喜欢 JSON，因此我们将 OCR 输出转换为格式化的字符串。

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### 示例输出

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

请注意，每行都包含置信度指标——如果你计划自动 **从发票中提取文本**，可以据此过滤低置信度条目。

---

## 第六步 – 将 OCR 数据保存为 CSV（每行文本 + 置信度）

CSV 非常适合电子表格或快速数据导入。Aspose 提供了一行代码即可将所有内容导出为 CSV 文件。

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

生成的 CSV 将如下所示：

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

现在你可以在 Excel、Google Sheets 中打开，或将其导入数据库。

---

## 进阶 – 处理低置信度文本和多页 PDF

### 按置信度过滤

如果只想保留高置信度的行，可在写入前先过滤 JSON：

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### 多页文档

Aspose.OCR 会为多页 PNG 或 PDF 自动创建新的 `page` 条目。遍历 `ocr_data["pages"]` 即可处理所有页面——无需额外代码。

---

## 完整可运行示例

下面是你可以直接复制、粘贴并立即运行的 **完整脚本**。将 `YOUR_DIRECTORY` 替换为存放 PNG 文件的文件夹路径。

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

使用 `python run_ocr.py` 运行脚本，你将在控制台看到 JSON 输出，磁盘上生成 CSV 文件，并得到一个高置信度条目的过滤列表。

---

## 常见问题

**Q: 我可以用它来提取扫描收据的文本，而不是发票吗？**  
A: 当然可以。工作流完全相同——只需将 `image_path` 指向你的收据 PNG。如果收据使用其他语言，相应地切换 `engine.language` 即可。

**Q: 如果我的 PNG 包含旋转的文字怎么办？**  
A: Aspose.OCR 会自动检测方向，但对于顽固情况，你可以在将图像传给引擎之前使用 Pillow 手动旋转。

**Q: 使用 Aspose.OCR 是否需要付费许可证？**  
A: 该库提供带水印的免费评估模式。生产环境下需要购买许可证，可从 Aspose 官网获取。

---

## 结论

我们已经覆盖了使用 Python **在 PNG 上运行 OCR** 所需的全部内容：安装 SDK、加载图像、提取结构化文本，以及将结果保存为 JSON 或 CSV。无论你是想 **从图像中提取文本** 用于简单脚本，还是 **从发票中提取文本** 用于自动化会计流水线，上述步骤都为你提供了坚实、可投入生产的基础。

接下来，你可以进一步探索：

- 将 CSV 输出集成到数据库，实现批量发票存储。  
- 使用正则表达式进行后处理，提取日期、金额或税号。  
- 若发票中包含二维码，可使用 `ocr_engine.recognize_barcode` 功能进行识别。

尝试一下，调整置信度阈值，感受文档处理工作流的轻松流畅。还有其他问题或想分享的使用案例吗？欢迎在下方留言——祝你 OCR 顺利！

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}