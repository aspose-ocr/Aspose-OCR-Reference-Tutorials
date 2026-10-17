---
category: general
date: 2026-04-26
description: 如何对扫描表单进行 OCR，学习如何预处理图像以降低噪声，并快速从图像中提取文本。
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: zh
og_description: 如何对扫描文档进行 OCR，预处理图像，降低噪声，并高效提取文本。
og_title: 如何运行 OCR 并预处理图像 — 快速指南
tags:
- OCR
- image processing
- Python
title: 如何运行 OCR 并预处理图像——从扫描表单中提取文本
url: /zh/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何运行 OCR – 提取图像中文本的完整指南

是否曾好奇 **如何运行 OCR** 在一张凌乱的扫描表单上并获得干净、可搜索的文本？你并不是唯一有此疑问的人。在许多真实项目中，原始图像充满斑点、光照不均以及其他导致开箱即用的 OCR 失效的怪异情况。

好消息是？只需几行 Python 代码和一个智能的预处理管道，你就能显著提升识别准确率，**降低噪声**，并提取出所需的精确文字。在本教程中，我们将逐步演示从加载图片到打印最终字符串的每一步，让你获得一段可直接用于发票、收据或任何扫描文档的即用代码片段。

## 你将构建的内容

- 一个与底层 OCR 库通信的 `OcrEngine` 实例。  
- 一个 **二值化** 图像并应用 **中值模糊** 来平滑斑点的预处理链。  
- 一个简单的 `process()` 调用，返回包含 `text` 属性的对象，即提取的字符串。  

完成后，你将拥有一个自包含的脚本，能够对任意图像文件运行并立即在控制台中看到提取的文本。

## 前置条件

- Python 3.9+（此处使用的语法对应最新稳定版）。  
- 虚构的 `aocr` 包——可以把它视为 Tesseract 或任何现代 OCR 引擎的轻量包装器。使用 `pip install aocr` 安装。  
- 一个放置在可引用文件夹中的扫描图像（`scanned_form.jpg`）。  

如果你使用的是实际的 OCR 库，如 `pytesseract`，只需将 `OcrEngine` 替换为相应的类——其他代码保持不变。

![](how-to-run-ocr-example.png "如何运行 OCR 示例，展示扫描表单及提取的文本")

*Alt text: 如何在扫描文档上运行 OCR 并查看提取的文本。*

---

## 步骤 1：如何运行 OCR – 初始化引擎

在引擎能够读取任何内容之前，我们需要创建一个实例。把 `OcrEngine` 当作后续解释视觉数据的大脑。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **为何重要：** 实例化引擎会设置内部模型、加载语言包并准备运行时环境。跳过此步骤通常会在后续调用 `process()` 时导致 `NoneType` 错误。

---

## 步骤 2：如何预处理图像 – 加载你的扫描表单

大脑准备就绪后，我们将图片喂给它。该图像可以是 `aocr.Image` 支持的任意格式。

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **专业提示：** 开发阶段使用绝对路径，可避免脚本在不同工作目录下运行时出现 “文件未找到” 的意外。

---

## 步骤 3：如何降低噪声 – 应用二值化 & 中值模糊

原始扫描常常包含杂散点、背景不均或淡淡的阴影。两种经典技巧——**二值化** 和 **中值模糊**——能够在不牺牲字符边缘的前提下清理图像。

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### 深入了解

- **二值化**：`threshold=180` 的数值告诉算法：“亮度高于 180 的像素设为白色，其余设为黑色”。如果你的扫描过暗或过亮，可相应调整此数值。  
- **中值模糊**：半径为 `2` 表示滤波器查看一个 5×5 像素窗口，并用中值替换中心像素。这样既能平滑孤立的斑点，又能保持字母笔画的完整。

> **边缘情况：** 若文档中有彩色高亮，简单的二值阈值可能会将其抹掉。此时可考虑使用 `aocr.ImageFilters.adaptive_threshold()`——它会在图像局部自适应阈值。

---

## 步骤 4：如何提取文本 – 运行 OCR 过程

手握干净的图像后，终于让引擎施展魔法。

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **内部发生了什么？** 引擎在像素矩阵上运行神经网络（或传统模式匹配器），将每个识别出的字形转换为 Unicode 字符，并将其组装成行和段落。

---

## 步骤 5：如何提取文本 – 打印结果

`ocr_result` 对象提供了一个便利的 `text` 属性。让我们看看得到了什么。

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### 预期输出

如果扫描表单包含：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

你应该会看到类似如下的输出：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

注意，预处理步骤消除了之前把 “Amount” 误识为 “Am0unt” 的杂散点。这正是 **在 OCR 前降低噪声** 的威力所在。

---

## 常见陷阱与解决方案

| 症状 | 可能原因 | 快速解决方案 |
|------|----------|--------------|
| 字符乱码（例如 “@#%”） | 图像过暗或过亮 | 调整 `binarize()` 中的 `threshold`；尝试 `adaptive_threshold`。 |
| 缺失单词 | 噪声仍然存在 | 增大 `median_blur` 的 `radius`，或添加 `gaussian_blur` 滤镜。 |
| 语言错误（例如英文字符变成中文） | 加载了错误的语言包 | 在创建 `OcrEngine()` 时传入 `language="eng"`（如果库支持）。 |
| 大文件处理慢 | 分辨率过高 | 在二值化前先下采样图像：`aocr.ImageFilters.resize(width=1200)`。 |

---

## 进一步探索 – 后续步骤与相关主题

- **批量处理**：将上述逻辑封装在循环中，自动处理数十个文件。  
- **结构化输出**：对 `ocr_result.text` 使用正则表达式提取日期、金额等字段。  
- **替代库**：将 `aocr` 替换为 `pytesseract`——仅在引擎初始化步骤更改代码。  
- **PDF 图像预处理**：将每页 PDF 转为图像后，套用相同的管道。  

这些扩展可以让你把解决方案从单个表单扩展到企业级文档摄取流水线。

---

## 结论

我们已经从头到尾完整演示了 **如何运行 OCR**，展示了 **如何预处理图像** 以 **降低噪声**，并演示了 **如何从图像中提取文本** 的可复现脚本。关键要点是：几种简单的滤镜——二值化和中值模糊——即可将嘈杂的扫描件转化为可靠的数据来源，为你节省大量手动清理时间。

尝试使用自己的文档运行脚本，调节阈值，观察准确率提升。当你准备好后，可探索批量处理或将输出集成到数据库，实现可搜索的档案。祝编码愉快，愿你的 OCR 永远精准无误！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}