---
category: general
date: 2026-06-06
description: 使用 Python 对图像进行 OCR 并查看置信度分数。了解如何过滤低置信度词汇、设置阈值以及处理边缘情况。
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: zh
og_description: 在 Python 中对图像进行 OCR，检查置信度水平，并过滤低置信度的词。本教程将带您完成一个完整的可运行示例。
og_title: 使用 Python 对图像进行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 使用 Python 对图像进行 OCR——完整的逐步指南
url: /zh/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 对图像进行 OCR – 完整分步指南

是否曾经需要 **run OCR on image** 文件，却不确定如何提取可靠的文本？你并不孤单——很多开发者在提取的文字模糊、置信度分数难以理解时都会卡住。

在本指南中，我们将直接展示可运行的解决方案：你将看到如何对图像进行 OCR、读取整体置信度，并挑选出可能需要人工复核的低置信度词。阅读完毕后，你将拥有可复用的脚本，了解每行代码的意义，并学会为自己的项目调整置信度阈值。

## 本教程涵盖内容

我们将完整演示工作流——从加载图像到打印出置信度低于 80 % 的词汇报告。过程中我们会讨论：

* 选择可靠的 OCR 引擎（我们使用 **EasyOCR**，一款流行的 Python OCR 库）  
* 解读每个 OCR 结果返回的 `confidence` 属性  
* 使用自定义 **OCR confidence threshold** 过滤词汇  
* 将脚本扩展为批处理或使用 **pytesseract** 等其他引擎  

无需任何 OCR 经验，只需具备基本的 Python 知识并拥有可用的运行环境（推荐 Python 3.9+）。

准备好把模糊的截图转换为干净、可搜索的文本了吗？让我们开始吧。

---

## ## How to Run OCR on Image with Python

本教程的核心是一段三步代码片段，与你之前看到的代码结构相同。下面我们将逐行拆解，解释原因，并提供完整的可直接复制运行的脚本。

### 步骤 1：安装并导入 OCR 引擎

首先，确保 OCR 库已安装。**EasyOCR** 开箱即用，支持多语言，并为每个词提供置信度分数。

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*为什么选 EasyOCR？* 它内置了经过多样化数据集训练的深度学习模型，通常比旧的 Tesseract 引擎在混合质量图像上得到更高的置信度。

> **小技巧：** 如果你运行在资源受限的环境（例如极小的 Docker 容器），`pytesseract` 可能更轻量，但会失去 EasyOCR 所提供的现代化准确性。

### 步骤 2：对图像执行 OCR

现在我们真正 **run OCR on image**。原示例中的 `recognize_image` 方法被 EasyOCR 的 `readtext` 调用取代，返回 `(bbox, text, confidence)` 元组的列表。

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

`ocr_results` 中的每个条目形如：

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

第三个元素（示例中的 `0.92`）即置信度分数，取值范围为 0 到 1。

### 步骤 3：汇总整体置信度

不同于之前只打印单个 `confidence` 属性的代码片段，EasyOCR 为每个词提供置信度。我们通过求平均值来获得整体感受：

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*为什么取平均？* 这能快速检查整体健康度——如果整体置信度低于 70 %，通常需要改进图像（如提升光照、预处理等）。

### 步骤 4：列出低置信度词汇

下面的代码直接实现了“列出置信度低于设定阈值的词”的需求。默认将 **OCR confidence threshold** 设为 0.80（80 %），你可以自行调整。

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

循环会打印每个未达标的词及其置信度百分比。这正是原始 `for recognized_word in recognition_result.words` 循环的等价实现，只是适配了 EasyOCR 的输出格式。

---

## ## Understanding OCR Confidence Scores

置信度并非神秘数字；它是模型对特定转录结果的自信程度估计。需要注意的要点如下：

| 场景 | 典型置信度 | 处理建议 |
|-----------|-------------------|------------|
| 清晰、高分辨率扫描 | 0.95 – 1.00 | 无需额外操作 |
| 略有模糊或光照不均 | 0.80 – 0.94 | 考虑轻度预处理（提升对比度） |
| 噪声严重、文字倾斜 | < 0.70 | 进行图像预处理（去倾斜、去噪）或切换 OCR 引擎 |

> **注意：** 某些语言（例如手写体）天然会得到较低分数，请相应调低阈值。

### 边缘情况与变体

1. **批量处理** – 若需 **run OCR on image** 多个文件，可将上述逻辑包装在遍历目录的循环中。  
2. **多语言支持** – 向 `easyocr.Reader` 传入 `['en', 'fr']` 等列表，引擎即可同时识别多种语言。  
3. **替代引擎** – 想尝试 **pytesseract**？将读取块替换为：

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   此时需要将字符级置信度聚合为词级置信度——工作量稍大但可实现。

4. **预处理技巧** – 使用 OpenCV 滤波（`cv2.threshold`, `cv2.GaussianBlur`）可提升噪声图像的置信度。  

---

## ## Full, Ready‑to‑Run Script

下面是完整的 Python 文件，直接复制到项目中即可使用。保存为 `ocr_report.py` 并运行 `python ocr_report.py`。请确保图像路径指向真实文件。

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**预期输出**（数值会因图像而异）：

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

如果所有词的置信度均超过 80 %，你将看到友好的 “All words meet the confidence threshold.” 提示。

---

## ## Frequently Asked Questions (FAQ)

**Q: 是否支持 PDF？**  
A: 不能直接处理。请先使用 `pdf2image` 等工具将每页 PDF 转为图像（PNG/JPEG），再交给本脚本。

**Q: 我的置信度全部很低，怎么办？**  
A: 尝试图像预处理：提升对比度、去除背景噪声或将图像旋转至水平基线。EasyOCR 还提供 `contrast_ths` 参数可调。

**Q: 能导出结果为 CSV 吗？**  
A: 完全可以。在低置信度循环后，使用 `csv.DictWriter` 将 `ocr_results` 写入 CSV，每行包含 `text`、`confidence` 与边界框坐标。

**Q: 有 GPU 加速版本吗？**  
A: EasyOCR 会在检测到兼容的 GPU 与已安装的 PyTorch 时自动使用 CUDA。运行前可通过 `torch.cuda.is_available()` 验证。

---

## Conclusion

我们已经使用 Python **run OCR on image**，检查了整体置信度，并筛选出需要人工复核的低置信度词汇。

## What Should You Learn Next?

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索其他实现方式：

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}