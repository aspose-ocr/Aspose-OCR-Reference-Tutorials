---
category: general
date: 2026-03-26
description: 创建 ROI 多边形以在选定区域运行 OCR。了解如何定义多个区域、注册它们，并使用 Python OCR 引擎提取文本。
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: zh
og_description: 创建 ROI 多边形并使用 Python 引擎对选定区域进行 OCR。包含完整代码、解释和技巧。
og_title: 创建感兴趣区域多边形 – 对选定区域进行快速 OCR
tags:
- OCR
- Python
- Image Processing
title: 创建感兴趣区域多边形 – 选定区域 OCR 的分步指南
url: /zh/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 ROI 多边形 – 选定区域 OCR 完整教程

是否曾需要 **创建 ROI 多边形**，以便只对图像中重要的部分进行 OCR？比如扫描收据时只关心总额，或表单中只需要读取签名字段。在这些情况下，**ocr on selected area** 能节省时间并提升准确率。  

在本指南中，我们将逐步演示完整流程：从定义两个多边形、在 OCR 引擎中注册它们，到一次性获取识别文本。阅读完毕后，你将拥有可直接运行的脚本，并深入理解为何聚焦感兴趣区域如此重要。

## 你将学到

- 如何使用常见 OCR 库 **创建 ROI 多边形** 对象。  
- 单一区域与多区域定义的区别。  
- 如何将这些区域注册到引擎，以实现 `ocr on selected area`。  
- 预期输出以及常见问题的排查方法（如 ROI 重叠、结果为空）。

### 前置条件

- 已安装 Python 3.8+。  
- 一个提供 `Polygon`、`Point` 和 `add_region_of_interest` 方法的 OCR 库（示例使用虚构的 `ocr` 模块；请替换为实际 SDK，如 Tesseract‑Python 包装器或 EasyOCR）。  
- 一张示例图片文件（`sample.png`），其中包含下文坐标对应的文字。

> **小贴士：** 若使用真实库，请确保图像加载时使用相同的坐标系（左上角为原点，X 向右递增，Y 向下递增）。

---  

## 步骤 1：导入 OCR 模块并加载图片  

首先，将 OCR 包导入作用域并读取待处理的图像。  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*为什么重要：* 引擎需要图像数据才能附加任何 **ROI 多边形**。有些库也支持后续传入图像，但提前初始化可以让工作流更整洁。

## 步骤 2：定义第一个 ROI 多边形  

现在创建第一个感兴趣区域。可以把它想象成在表头周围画一个矩形。  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*说明：*  
- `ocr.Point(x, y)` 使用像素坐标。  
- 点的列表按顺时针顺序排列，这是大多数引擎的默认要求。  
- 你可以添加任意数量的点来构成不规则形状；矩形只是其中一种特殊情况。

## 步骤 3：定义额外的 ROI 多边形（可选）  

不必局限于一个区域。下面的第二个多边形用于捕获页面下方的签名字段。  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*为何要添加更多？* 对多个区域执行 **ocr on selected area** 能在一次调用中提取不同的数据块，速度远快于对每个切片单独裁剪并处理。

## 步骤 4：在 OCR 引擎中注册 ROI  

多边形准备好后，告诉引擎哪些区域需要检查。  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*重要提示：* 某些 SDK 在为同一引擎处理新图像前，需要先调用 `clear_regions()` 方法以清除已有区域。

## 步骤 5：运行 OCR 并获取文本  

最后，触发识别。引擎只会在我们刚添加的多边形内部搜索。  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**预期输出**（假设 `sample.png` 在第一个 ROI 中包含 “Invoice Total: $123.45”，在第二个 ROI 中包含 “Signature: John Doe”）：

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

如果输出为空，请再次确认坐标实际覆盖了文字，并且图像分辨率与坐标系匹配。

## 边缘情况与常见陷阱  

| 情况                                   | 需要注意的点                                   | 解决方案 / 变通方法                              |
|----------------------------------------|------------------------------------------------|------------------------------------------------|
| **ROI 重叠**                            | 文本可能被返回两次。                           | 保持多边形不相交或对输出进行去重。               |
| **ROI 超出图像边界**                    | 引擎可能报错或返回空。                         | 将坐标限制在 `0 ≤ x < width`、`0 ≤ y < height` 范围内。 |
| **ROI 过小**                            | 像素不足导致 OCR 准确率下降。                 | 将多边形向外扩展几像素，或先对图像进行放大。     |
| **非矩形形状**                          | 部分引擎仅支持凸多边形。                       | 将复杂形状拆分为多个凸 ROI。                   |
| **图像尺寸变化**                        | 硬编码坐标会失效。                             | 根据图像尺寸计算 ROI（例如使用百分比）。        |

## 完整可运行示例  

下面是完整脚本，复制粘贴后即可运行（请将 `ocr` 替换为实际使用的库）。  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

使用 `python ocr_roi_example.py` 运行，你应当能看到两个定义区域中提取的字符串。

## 后续步骤  

- **动态 ROI 生成：** 与其手动写坐标，不如使用图像处理（如 OpenCV 轮廓检测）自动定位表格或字段。  
- **后处理：** 去除空白、使用正则表达式，或将数字转换为合适的数据类型。  
- **批量处理：** 遍历文件夹中的图片，如果布局一致，可复用相同的 ROI 定义。  

如果你对更复杂文档的 **ocr on selected area** 感兴趣——比如多页 PDF 或扫描表单——可以研究支持逐页 ROI 注册的库。

---  

### 可视化概览  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="创建 ROI 多边形示例，展示两个选定区域"}

该图展示了两个矩形（蓝色和绿色）在底层图像上的映射，明确标示了 OCR 引擎将读取的区域。

---  

## 结论  

我们已经 **创建了 ROI 多边形** 对象，将其注册到 OCR 引擎，并在干净、可复现的脚本中实现了 `ocr on selected area`。通过限制引擎只处理感兴趣的区域，你可以缩短处理时间、提升准确率，并让后续数据处理更加简便。  

尝试使用自己的图片——调整坐标、添加更多多边形，或将输出接入数据库。掌握基于区域的 OCR 后，可能性无限。  

有问题或想分享有趣的使用案例？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}