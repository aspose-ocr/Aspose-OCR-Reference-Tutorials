---
category: general
date: 2026-06-22
description: 使用 Python 从图像获取边界框坐标。学习如何在几分钟内使用 Aspose OCR 和 JSON 解析从图像中提取文本。
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: zh
og_description: 使用 Python 从图像获取边界框坐标。本指南展示了如何使用 Aspose OCR 在 Python 中提取图像文本并解析布局数据。
og_title: 在Python中获取OCR的边界框坐标 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: 在 Python 中从 OCR 获取边界框坐标 – 完整指南
url: /zh/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 OCR 中获取 Python 的边界框坐标 – 完整指南

是否曾经需要为扫描的发票中的每个单词**获取边界框坐标**，但不知从何入手？你并不是唯一遇到这种情况的人。在许多自动化项目中，你必须在图像上定位文本以进行高亮、编辑或输入到下游分析中。好消息是？只需几行 Python 和 Aspose.OCR，你就可以一次性获取文本**以及**其精确位置。

在本教程中，我们将通过一个实战示例，展示如何以**extract text from image python**的方式提取文本，然后深入 JSON 布局数据以提取这些边界框。没有冗余，只有可运行的脚本、每一步重要性的解释以及避免常见陷阱的提示。

---

## 您将构建的内容

通过本指南的学习，您将拥有一个可直接运行的 Python 脚本，能够：

1. 将图像（例如发票 PNG）加载到 Aspose OCR 中。
2. 配置引擎以输出 JSON 布局信息。
3. 将 JSON 解析为 Python 字典。
4. 遍历每个识别出的单词，打印其文本**以及**边界框坐标。

您还将看到如何将代码适配到多页 PDF、不同图像格式以及自定义坐标系。

### 前提条件

- 在机器上已安装 Python 3.8+。  
- 拥有有效的 Aspose.OCR for Python 许可证或免费试用版（库在没有许可证的情况下仍可工作，但会添加水印）。  
- `pip install aspose-ocr`（PyPI 上的包名）。  
- 将名为 `invoice.png` 的示例图像放置在可引用的文件夹中。

就是这样——无需重量级框架，也不需要外部服务。让我们开始吧。

---

## 步骤 1：安装并导入所需库

首先，确保 Aspose OCR 包和内置的 `json` 模块可用。`json` 模块随 Python 自带，因此我们只需安装 Aspose。

```bash
pip install aspose-ocr
```

Now import them in your script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **为什么这很重要：**导入 `aspose.ocr` 可让您使用高性能 OCR 引擎，而 `json` 则可以将原始布局字符串转换为原生 Python 字典，便于遍历。

---

## 步骤 2：创建 OCR 引擎并加载图像

引擎是该过程的核心。您实例化它，然后指向要扫描的图像。

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **专业提示：**将 `"YOUR_DIRECTORY/invoice.png"` 替换为指向实际文件的绝对或相对路径。如果未找到文件，Aspose 将抛出 `FileNotFoundError`，请仔细检查拼写。

---

## 步骤 3：配置引擎以输出 JSON 布局数据

Aspose OCR 可以返回纯文本、仅 OCR 的 JSON，或包含单词、行甚至单个字符坐标的完整布局 JSON。要**获取边界框坐标**，我们需要布局 JSON。

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **为什么使用 JSON？**JSON 与语言无关、易于阅读，并且可以干净地映射到 Python 字典。布局 JSON 包含一个 `"words"` 数组，每个条目保存文本以及一个包含八个数字的 `boundingBox` 数组（四个角点）。

---

## 步骤 4：运行识别并获取原始 JSON 字符串

现在我们实际运行 OCR。`recognize()` 方法返回一个 `OcrResult` 对象，我们可以从中提取 JSON 字符串。

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

If you print `layout_json` you’ll see something like:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **边缘情况：**如果 OCR 引擎无法检测到任何文本，某些图像可能会产生空的 `"words"` 数组。此时，请在继续之前检查图像质量（对比度、分辨率）。

---

## 步骤 5：将 JSON 解析为 Python 字典

使用原生 Python 结构比处理字符串要容易得多。使用 `json.loads()` 函数将字符串转换。

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

现在 `layout_data["words"]` 是一个字典列表，每个字典代表一个单词及其边界框。

---

## 步骤 6：遍历单词并**获取边界框坐标**

以下是本教程的核心：遍历每个单词，提取文本并打印坐标。这正是我们**获取边界框坐标**的地方。

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Sample output** (your numbers will differ based on the image):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **为什么使用八点格式？**四个角点（左上、右上、右下、左下）即使文本倾斜也能绘制出单词的多边形。如果只需要简单的矩形，可以计算 `x_min = min(x1, x2, x3, x4)`，`y_min = min(y1, y2, y3, y4)`，`width = max(x…) - x_min`，以及 `height = max(y…) - y_min`。

---

## 可选增强

### 1. 将边界框转换为简单矩形

如果下游工具期望 `(x, y, width, height)` 而不是八点，请添加一个辅助函数：

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. 处理多页 PDF

Aspose OCR 可以接受 PDF 流。将图像加载行替换为：

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

对每页调用 `set_page_number`，收集每页的坐标。

### 3. 可视化边界框

如果想在原始图像上看到绘制的框，请使用 Pillow：

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

现在您会看到每个识别单词周围的红色轮廓——非常适合调试或 UI 覆盖。

---

## 常见问题与注意事项

- **如果 JSON 很大怎么办？** 对于大型文档，考虑流式处理 JSON 或逐页处理，以降低内存使用。
- **为什么有些单词缺失？** 低对比度或手写文本常会导致 OCR 引擎识别失败。在将图像提供给 Aspose 前进行预处理（提升对比度、二值化）。
- **能获取字符级别的坐标吗？** 可以——设置 `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` 即可收到包含各自 `boundingBox` 的 `"characters"` 数组。
- **坐标系是从零开始吗？** 完全是。 (0, 0) 位于图像的左上角。

---

## 完整脚本 – 可直接复制运行

下面是完整的可运行示例，整合了所有步骤。将其保存为 `extract_bboxes.py` 并执行 `python extract_bboxes.py`。

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何在图像识别中使用 Aspose OCR 获取 JSON 结果](/ocr/english/net/text-recognition/get-result-as-json/)
- [通过准备矩形在 OCR 中提取图像文本](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}