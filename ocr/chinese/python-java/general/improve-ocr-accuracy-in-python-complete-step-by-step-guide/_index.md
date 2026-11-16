---
category: general
date: 2026-05-31
description: 通过使用 Python 对图像进行预处理，提高 OCR 的准确性。学习如何从图像文件中提取文本，识别 PNG 中的文字，并提升识别效果。
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: zh
og_description: 通过对文本进行图像预处理，在 Python 中提升 OCR 准确率。按照本指南轻松从图像文件中提取文本并识别 PNG 中的文字。
og_title: 在Python中提升OCR准确率 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: 在 Python 中提升 OCR 准确率 – 完整的逐步指南
url: /zh/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 提升 Python 中 OCR 准确率 – 完整分步指南

是否曾尝试 **提升 OCR 准确率**，却得到一堆乱码？你并不孤单。大多数开发者在原始图像噪声大、倾斜或对比度低时都会碰壁。好消息是：只需几招预处理技巧，就能把模糊的截图变成干净、机器可读的文本。

在本教程中，我们将通过一个真实案例 **对图像进行 OCR 预处理**，运行识别引擎，最后 **从图像中提取文本**——具体以 PNG 为例。完成后，你将掌握如何 **从 PNG 中识别文本**，并拥有一段可在任意项目中直接使用的代码片段。

## 你将学到

- 为什么图像预处理对 OCR 引擎至关重要  
- 哪些预处理模式（去噪、去倾斜）能带来最大提升  
- 如何在 Python 中配置 `OcrEngine` 实例  
- 完整可运行的脚本，**从图像文件中提取文本**  
- 处理旋转扫描或低分辨率图片等边缘情况的技巧  

无需除 OCR SDK 之外的外部库，但你需要 Python 3.8+ 和一张待读取的 PNG 图像。

---

![提升 Python 中 OCR 准确率的步骤示意图](image.png "提升 OCR 准确率工作流")

*Alt text: 展示预处理和识别步骤的提升 OCR 准确率工作流示意图。*

## 前置条件

- 已安装 Python 3.8 或更高版本  
- 可使用提供 `OcrEngine`、`OcrEngineSettings` 与 `ImagePreprocessMode` 的 OCR SDK（下面的代码使用通用 API；如有需要请替换为你的供应商类）  
- 将 PNG 图像（`input.png`）放在可引用的文件夹中  

如果你使用虚拟环境，请立即激活——不需要花哨操作，只需 `python -m venv venv && source venv/bin/activate`。

---

## 步骤 1：创建 OCR 引擎实例 – 开始提升 OCR 准确率

首先需要一个 OCR 引擎对象。它相当于大脑，后续会读取像素并输出字符。

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

为什么重要：没有引擎就无法进行任何预处理，原始图像会直接喂给识别器——这通常是准确率最差的情况。

---

## 步骤 2：加载目标 PNG – 为从 PNG 中识别文本做好准备

现在告诉引擎要处理的文件。PNG 是无损格式，天然比 JPEG 多了一点优势。

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

如果图像位于其他位置，只需调整路径即可。引擎支持任何受支持的格式，但 PNG 往往能保留字符边缘的细节。

---

## 步骤 3：配置预处理 – 为 OCR 预处理图像

魔法就在这里。我们创建一个设置对象，开启去噪以去除斑点，并打开去倾斜，使倾斜的文字自动校正。

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### 为什么同时使用去噪 + 去倾斜？

- **去噪**：随机像素噪声会干扰模式匹配算法。去除噪声后字母更清晰。  
- **去倾斜**：即使是 2 度的倾斜也会显著降低置信度分数。去倾斜会对齐基线，让识别器更可靠地匹配字体。

如果你的图像特别暗，可以尝试额外的标志（例如 `ImagePreprocessMode.CONTRAST_ENHANCE`）。SDK 文档通常会列出所有可用模式。

---

## 步骤 4：将设置应用到引擎 – 把预处理绑定到 OCR

将设置对象分配给引擎，这样下一次识别时就会使用我们刚定义的转换。

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

如果跳过此步骤，引擎会回退到默认（通常是“无预处理”），导致 **OCR 准确率下降**。

---

## 步骤 5：运行识别过程 – 从图像中提取文本

所有准备就绪后，终于可以让引擎工作了。此调用是同步的，返回一个包含识别字符串的结果对象。

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

在幕后，引擎会：

1. 将 PNG 加载到内存  
2. 根据我们的设置执行去噪和去倾斜  
3. 运行神经网络或经典模式匹配器  
4. 将输出封装进 `recognition_result`

---

## 步骤 6：输出识别文本 – 验证提升效果

打印提取的字符串。在真实应用中，你可能会把它写入文件、数据库，或传递给其他服务。

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### 预期输出

如果图像中包含句子 “Hello, OCR World!” 应该会看到：

```
Hello, OCR World!
```

可以看到文本干净整洁——没有杂散符号或破碎字符。这正是 **图像预处理用于文本** 的效果。

---

## 专业技巧 & 边缘情况

| 场景 | 调整方式 | 原因 |
|-----------|----------------|-----|
| 非常低分辨率的 PNG (≤ 72 dpi) | 如有可用，添加 `ImagePreprocessMode.SUPER_RESOLUTION` | 上采样可以为识别器提供更多像素 |
| 文本旋转 > 5° | 增大去倾斜容差或在喂给引擎前使用 `Pillow` 手动旋转 | 极端角度有时会绕过自动去倾斜 |
| 背景图案繁杂 | 启用 `ImagePreprocessMode.BACKGROUND_REMOVAL` | 去除非文本杂乱，防止误读 |
| 多语言文档 | 设置 `ocr_engine.language = "eng+spa"`（或类似） | 引擎选择正确的字符集，提高整体准确率 |

记住，**提升 OCR 准确率** 并非一刀切；你可能需要针对特定数据集反复调试预处理标志。

---

## 完整脚本 – 直接复制粘贴

下面是完整、可运行的示例，涵盖了我们讨论的每一步。将其保存为 `improve_ocr_accuracy.py`，然后使用 `python improve_ocr_accuracy.py` 执行。

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

运行后观察控制台，你会立即看到 **从图像中提取文本** 的结果。如果输出不理想，按 “专业技巧” 表中的说明调整 `preprocess_mode` 标志。

---

## 结论

我们刚刚演示了使用 Python **提升 OCR 准确率** 的实用配方。通过创建 `OcrEngine`、加载 PNG、**为 OCR 预处理图像**，以及最终 **从 PNG 中识别文本**，即使源图像并不完美，也能可靠地 **从图像文件中提取文本**。

接下来可以尝试将一批图像放入循环处理、将每个结果存入 CSV，或实验对比度增强等额外预处理模式。相同的模式同样适用于 PDF、扫描收据或手写笔记——只需更换输入并相应调整设置。

对特定图像类型有疑问，或想了解如何将其集成到 Web 服务中？欢迎留言，我们一起探讨。祝编码愉快，愿你的 OCR 结果永远晶莹剔透！

## 接下来该学习什么？

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}