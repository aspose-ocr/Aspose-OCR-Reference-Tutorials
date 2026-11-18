---
category: general
date: 2026-06-25
description: 使用 Python OCR 从图像中提取文本。学习如何加载图像进行 OCR、在 Python 中执行 OCR，以及将收据转换为 JSON，只需几个简单步骤。
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: zh
og_description: 使用 Python OCR 从图像中提取文本。本教程将指导您加载用于 OCR 的图像、在 Python 中执行 OCR，以及将收据转换为
  JSON。
og_title: 在 Python 中从图像提取文本 – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: 在 Python 中从图像提取文本 – 完整 OCR 指南
url: /zh/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 从图像中提取文本 – 完整 OCR 指南

是否曾需要**从图像中提取文本**但不知从何入手？在本教程中，我们将向您演示如何**加载图像进行 OCR**、**在 Python 中执行 OCR**以及**将收据转换为 JSON**——只需几行代码即可实现。

如果您曾构建过收据扫描应用、费用追踪器，或只是想自动化数据录入，您会明白掌握此流程为何能改变游戏规则。完成后，您将拥有一个可运行的脚本，读取收据图片并输出干净的 JSON 负载，供下游服务使用。

## 您将学到的内容

1. **Create an OCR engine instance** – 所有识别工作的入口点。  
2. **Load an image for OCR** – 告诉引擎读取哪个文件。  
3. **Choose the export format** – JSON 或 XML，我们将选择 JSON，因为它更易于使用。  
4. **Run the recognition** – 实际在 Python 中执行 OCR。  
5. **Print or store the result** – 将收据转换为 JSON 并查看输出。

不需要任何 OCR 先前经验；只需一个基本的 Python 环境和一张图像文件（收据、传单或任何您需要的）。

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="使用 Python OCR 提取图像文本的流程图"}

## 从图像中提取文本 – 步骤式 Python OCR

下面是完整的可直接运行的脚本。您可以将其复制粘贴到名为 `receipt_ocr.py` 的文件中，然后运行 `python receipt_ocr.py`。

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### 为什么这样有效

- **Engine instance** – `aocr.OcrEngine()` 封装了所有繁重的工作（模型加载、预处理等）。  
- **Loading the image** – `engine.load_image()` 明确告知库要分析的位图；您可以提供 JPEG、PNG，甚至多页 PDF。  
- **Export format** – 将 `engine.export_format` 设置为 `aocr.ExportFormat.JSON` 可使结果成为结构化字符串，完美匹配期待 JSON 的 API。  
- **Recognition call** – `engine.recognize()` 在后台运行神经网络推理；它返回包含检测到的文本块、置信度分数和布局信息的 JSON 字符串。  

---

## 使用 aocr 加载 OCR 图像

如果您在想图像是否需要特殊预处理，简短的答案是**不**——`aocr` 会自动处理大多数常见情况（对比度调整、去倾斜）。不过，您可以通过以下方式提升准确率：

- 确保图像分辨率至少为 300 dpi。  
- 裁剪掉无关的边框。  
- 在输入前转换为灰度（可选，`engine.load_image()` 会为您完成）。

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* 如果收据噪声较多，上述额外步骤可以显著提升 **perform OCR in Python** 的准确性。

---

## 选择导出格式并将收据转换为 JSON

您可能会问：“为什么不直接获取纯文本？”因为 JSON 保留了层次结构（行、单词、边界框），这使得后续映射诸如*总金额*或*日期*等字段更加容易。

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

运行脚本时，`json_result` 将类似如下（为简洁起见已裁剪）：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

现在您拥有一个 **convert receipt to JSON** 的负载，可直接输入数据库、REST 接口或机器学习模型。

---

## 运行识别并获取结果

最后一步——实际执行 OCR——只需调用 `recognize()`。在后台，库会：

1. 将图像送入预训练的卷积网络。  
2. 将网络输出解码为可读字符。  
3. 将所有内容打包为选定的格式（本例中为 JSON）。

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

如果您需要将输出保存而不是打印，只需写入文件：

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* 某些收据包含非 ASCII 字符（例如 “€”）。请确保如上所示使用 UTF‑8 编码打开文件，以避免出现乱码。

---

## 完整工作示例（所有步骤合并在一个脚本中）

将所有内容整合在一起，以下是可端到端运行的最终脚本：

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

使用以下方式运行：

```bash
python receipt_ocr.py
```

您应该会看到确认行，并且在同一文件夹中生成一个包含结构化数据的 `receipt_output.json` 文件。

---

## 结论

现在您已经了解如何使用 Python **从图像中提取文本**、如何 **加载图像进行 OCR**、如何 **在 Python 中执行 OCR**，以及如何 **将收据转换为 JSON** 以供下游使用。此端到端流程轻量，仅需 `aocr` 包，即可嵌入任何自动化流水线。

接下来做什么？尝试将导出格式切换为 XML，实验不同的图像预处理技术，或构建一个小型 Flask API，接受上传的收据并即时返回 JSON 负载。一旦掌握基础，可能性无限。

有问题或遇到困难？在下方留言，祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 提取图像文本 – 步骤式指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [提取图像文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 从图像中提取表格](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}