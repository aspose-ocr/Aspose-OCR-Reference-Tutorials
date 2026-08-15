---
category: general
date: 2026-03-28
description: 如何在 Python 中对 ROI 进行 OCR – 学习如何设置预处理选项，以从特定图像区域准确提取文本。
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: zh
og_description: 如何在Python中对ROI进行OCR – 本指南展示了如何设置预处理，以实现对定义图像区域的可靠文本提取。
og_title: 如何在Python中对ROI进行OCR——如何设置预处理
tags:
- OCR
- Python
- Aspose
title: 如何在Python中对ROI进行OCR – 如何设置预处理
url: /zh/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中 OCR ROI – 如何设置预处理

是否曾想过 **如何在嘈杂的发票图像中 OCR ROI**，而不必将整页加载到内存中？你并不是唯一有此困扰的人。在许多真实项目中，我们只需要少数几个字段——客户姓名、地址、总额——因此扫描整份文档显得多余。

好消息是？使用 Aspose OCR，你可以明确告诉引擎 **在哪里查找**，甚至先对图像进行清理。在本教程中，我们将演示 **如何设置预处理** 选项，定义感兴趣区域（ROI），并仅用几行 Python 代码提取干净的文本。

阅读完本指南后，你将拥有一个可直接运行的脚本，能够从任意发票、收据或表单中提取特定块。无需额外工具，只需 Aspose OCR 和一点 Python 逻辑。

---

## 你需要准备的内容

- **Python 3.8+**（代码在任何近期版本上均可运行）  
- **Aspose OCR for Python via .NET** – 使用 `pip install aspose-ocr` 安装  
- 一个示例图像（例如 `invoice.png`），放在可引用的文件夹中  
- 对 Python 函数和面向对象语法的基本了解  

如果这些都已经准备好，太好了——直接进入代码部分吧。

---

![如何 OCR ROI 示例图](ocr-roi.png "如何 OCR ROI 示例")

*Alt text: 展示发票图像上 ROI 框的如何 OCR ROI 示意图*

---

## 第一步 – 初始化 OCR 引擎（如何 OCR ROI）

在告诉引擎 **在哪里** 查找之前，需要先创建 OCR 处理器的实例。该对象保存所有配置并执行识别过程。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*为什么重要*：`OcrEngine` 类封装了繁重的工作（字体检测、版面分析等）。创建单个引擎可以避免对每张图像重新初始化重资源，从而保持性能敏捷。

---

## 第二步 – 加载源图像（如何 OCR ROI）

Aspose Storage 让加载图像变得轻而易举。指向文件路径，即可得到一个准备好处理的 `Image` 对象。

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*提示*：如果使用流（例如通过 Web API 上传的图像），可以将 `BytesIO` 对象传给 `Image.load`，而不是文件路径。

---

## 第三步 – 定义感兴趣区域（ROIs）

现在我们回答核心问题 **如何 OCR ROI**：告诉引擎包含我们关心数据的精确矩形。每个 ROI 由左上角坐标 (`x`, `y`) 和尺寸 (`width`, `height`) 定义。

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*为什么使用 ROI？*  
- **速度** – 引擎跳过图像中无关的部分。  
- **准确性** – 聚焦小区域后，其他噪声不会干扰识别器。  
- **灵活性** – 可以根据需要添加任意数量的 ROI；引擎会按相同顺序返回结果列表。

---

## 第四步 – 如何设置预处理以提升 OCR 准确度

直接从扫描仪或手机获取的图像常常存在倾斜、对比度低或光照不均等问题。Aspose OCR 提供 `PreprocessingOptions` 对象，让你在识别前启用常见的修复功能。

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*这有什么帮助*：  
- **Deskew** 去除导致字符形状模糊的倾斜。  
- **Binarize** 降低颜色噪声，生成干净的二值图像。  
- **Contrast** 放大微弱笔画，特别适用于褪色的收据。

可以尝试打开或关闭这些标志，观察输出是否变化。这正是 **如何有效设置预处理** 的精神所在。

---

## 第五步 – 仅在已定义的 ROI 内执行 OCR

当引擎、图像、ROI 与预处理都准备就绪后，调用 `recognize`。该方法返回一个 `OcrResult` 对象，其中包含 `regions` 集合——每个条目对应我们提供的 ROI 顺序。

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*内部原理*：引擎会裁剪每个 ROI，应用预处理管道，然后在清理后的片段上运行识别模型。因为我们传入的是列表，结果保持相同顺序，后处理变得直观。

---

## 第六步 – 读取并使用提取的文本（如何 OCR ROI）

最后，遍历 `regions` 列表并打印或存储识别出的字符串。`Region` 对象公开的 `text` 属性即为 Unicode 结果。

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**预期输出（示例）**：

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

如果文本出现乱码，请重新检查 **如何设置预处理**：可能需要提升 `contrast`，或对彩色徽标关闭 `binarize`。

---

## 常见陷阱与专业提示

| 问题 | 产生原因 | 解决方案（如何设置预处理） |
|------|----------|---------------------------|
| 倾斜的文字变成乱码 | `deskew` 未启用或图像旋转角度过大 | 设置 `preprocessing_options.deskew = True` |
| 数字变成点或杂散标记 | 对比度低或二值化过度 | 降低 `contrast`（如 `1.2`）或将 `binarize = False` |
| ROI 坐标偏移几像素 | DPI 不同或扫描仪缩放 | 使用工具（如 Paint.NET）精确测量像素位置，或为每个 ROI 增加少量边距（`+5` 像素） |
| 某区域返回空结果 | ROI 超出图像边界 | 验证图像尺寸：`source_image.width`, `source_image.height` |

---

## 扩展方案（如何在不同场景下 OCR ROI）

- **动态 ROI**：如果发票布局多变，可先进行快速全页 OCR，定位关键字（如 “Customer:”, “Address:”），随后动态计算 ROI。  
- **批量处理**：将上述步骤封装为函数，对文件夹中的图像循环处理。记得复用同一个 `ocr_engine` 实例，以降低内存占用。  
- **导出为 JSON**：与其直接打印，不如构建字典并使用 `json.dumps` 导出；这让后续集成（例如向 ERP 系统供稿）变得轻而易举。

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## 结论

现在你已经拥有一个完整、可运行的示例，展示了 **如何在 Python 中 OCR ROI**，并掌握了 **如何设置预处理** 以获得最佳准确度。通过将引擎限制在感兴趣的矩形并事先清理图像，你可以获得更快、更干净的结果——这对发票自动化、表单数字化或任何只需页面局部信息的场景都极为适用。

准备好进一步探索了吗？尝试为不同文档类型调整 ROI 坐标，或实验 `sharpen`、`noise_reduction` 等额外预处理标志。Aspose OCR 的灵活性让你几乎可以针对任何图像质量定制流水线。

如果遇到问题，请检查控制台输出是否有空区域，并重新审视预处理设置。祝编码愉快，愿你的 OCR 永远精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}