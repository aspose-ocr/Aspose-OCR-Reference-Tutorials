---
category: general
date: 2026-06-25
description: 学习如何在 Python 中进行 OCR，发现加载图像进行 OCR 的最佳方式，然后通过 Aspose AI 后处理提升准确率。
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: zh
og_description: 如何在 Python 中执行 OCR？请按照本指南加载用于 OCR 的图像，运行基本识别，并使用 Aspose AI 后处理提升结果。
og_title: 如何在 Python 中进行 OCR – 完整的 Aspose OCR 与 AI 教程
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: 如何在 Python 中执行 OCR – 完整的 Aspose OCR 与 AI 指南
url: /zh/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中执行 OCR – 完整的 Aspose OCR 与 AI 指南

是否曾好奇 **如何在 Python 中执行 OCR** 而不必与底层图像技巧纠缠？你并不孤单。在本教程中，我们将演示如何加载用于 OCR 的图像、进行纯文本提取，然后使用 Aspose 的 AI 后处理器对输出进行润色。完成后，你将拥有一个即用即走的脚本，能够将嘈杂的扫描件转换为干净、可搜索的文本——无需额外服务。

我们将覆盖从安装 SDK 到在长时间运行的应用中释放资源的全部内容。如果你曾尝试 **load image for OCR** 却得到一堆乱码，这篇指南就是解药。你会看到将传统 OCR 与语言模型结合后，产生的结果看起来就像人手工输入的一样。

## 前置条件

在开始之前，请确保你拥有：

- Python 3.9 或更高版本（代码使用类型提示，旧版解释器不支持）
- 有效的 Aspose OCR 许可证或免费试用版（社区版可用于评估）
- 如果想加速 AI 模型，至少 4 GB VRAM 的 GPU（可选，但更好）
- 一张示例图像，例如 `sample_invoice.png`，放置在可引用的位置

如果这些听起来陌生，请不要慌——安装 SDK 只需一行命令，GPU 设置也可以稍后关闭。

## 第一步：安装 Aspose OCR 与依赖

打开终端并运行：

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

第一个包为你提供 `aspose.ocr`，第二个添加 AI 后处理实用工具。两者都是纯 Python wheel，无需自行编译任何东西。

## 第二步：加载用于 OCR 的图像并初始化引擎

现在我们将使用 Aspose 的 `OcrEngine` **load image for OCR**。把它想象成把一张纸交给一位非常勤奋的职员，让他读取每一个字符。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **为什么这很重要：** `load_image` 调用是文件系统与 OCR 引擎之间的桥梁。如果路径错误，你会在任何识别开始之前就收到 `FileNotFoundError`。务必仔细检查目录分隔符，尤其是在 Windows 与 macOS/Linux 之间。

## 第三步：设置 Aspose AI 后处理器

Aspose AI 可以从 Hugging Face 下载语言模型，缓存到本地，并在你的 GPU（或 CPU）上进行推理。下面我们配置一个轻量级的 30 亿参数模型，能够在大多数现代笔记本电脑上运行。

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **提示：** 如果你使用的是仅 CPU 机器，请将 `gpu_layers = 0`。模型仍然可以运行，只是稍慢一些。`int8` 量化保持了极小的内存占用，同时保留了大部分模型精度。

## 第四步：注册自定义后处理器

AI 模型需要一个提示词来告诉它该做什么。这里我们让它充当 OCR 校对员，修正拼写错误、合并被拆开的单词并去除杂质。

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **为什么要使用自定义处理器？** 默认的后处理器可能会添加你不需要的额外解释或格式。通过提供我们自己的函数，输出将严格是清理后的文本，这对于后续的索引或数据库存储非常完美。

## 第五步：运行 AI 增强的 OCR 流程

现在我们将原始 OCR 输出送入 AI 层。引擎会调用我们的 `correction_processor`，进而与语言模型交互。

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

你应该会看到明显的改进：缺失的字符被恢复，常见的 OCR 误读如 “0” 与 “O” 被纠正，换行也变得更合理。

## 第六步：清理 – 释放资源

如果你计划在 Web 服务或长期运行的守护进程中使用此代码，释放 GPU 内存至关重要。忘记调用 `free_resources` 可能会在几百次请求后导致 “out‑of‑memory” 崩溃。

```python
ocr_ai.free_resources()
```

就这样——你的完整 OCR 流水线已经可以投入生产使用。

## 完整脚本回顾

下面是完整、可运行的示例。将其复制粘贴到名为 `ocr_with_ai.py` 的文件中，调整图像路径，然后运行 `python ocr_with_ai.py`。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### 预期输出

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

注意 “Inv0ice” 被纠正为 “Invoice”，金额后面的多余 “O” 消失了。这就是 AI 的魔法。

## 常见问题与边缘情况

### 如果没有 GPU 怎么办？

将 `model_config.gpu_layers = 0`，并可选地将 `model_config.context_size` 提升至 2048，以获得更好的 CPU 性能。模型运行会更慢，但仍能得到相同质量的纠正。

### 我的图像被旋转了——`load_image` 能处理吗？

Aspose OCR 会自动检测方向，但对于极度倾斜的扫描，你可能需要使用 Pillow 预先旋转：

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### 如何处理文件夹中的多个文件？

将整个流水线包装在 `for` 循环中，并将每个 `enhanced_text` 存入列表或直接写入 CSV。记得在循环结束后 **一次** 调用 `ocr_ai.free_resources()`，而不是在每个文件后调用——反复重新初始化模型会浪费资源。

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### 我可以更换语言模型吗？

完全可以。只需将 `model_config.hugging_face_repo_id` 更改为 Hugging Face 上任何兼容 GGUF 的模型（例如 `Meta/Llama-3.2-1B-Instruct-GGUF`）。保持量化设置与硬件相匹配即可。

## 专业技巧与陷阱

- **专业提示：** 将 `temperature=0.0` 设置为确定性的纠正。较高的温度可能会引入创意但不正确的更改。
- **注意：** 极长的文档（> 5000 字符）。示例中模型的上下文窗口限制为 1024 个 token；在发送给 AI 前请将文本拆分为段落。
- **安全提示：** 如果在受监管的环境中运行，请确保模型下载 URL 已列入白名单。`allow_auto_download` 标志可以

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [如何使用 AspOCR：针对 .NET 的图像 OCR 过滤器预处理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [使用 Aspose.OCR 的语言选择在 C# 中提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}