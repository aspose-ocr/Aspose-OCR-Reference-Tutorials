---
category: general
date: 2026-06-06
description: 使用 Aspose OCR 识别图像中的文本——学习如何加载图像进行 OCR，并在 Python 中使用 AI 后处理执行图像 OCR。
draft: false
keywords:
- recognize text from image
- perform ocr on image
- load image for ocr
language: zh
og_description: 快速识别图像中的文字。本指南展示了如何加载图像进行 OCR、在图像上执行 OCR，以及通过 AI 后处理提升结果。
og_title: 使用 Aspose OCR 与 AI 识别图像中的文本
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  headline: recognize text from image using Aspose OCR & AI
  type: TechArticle
- description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  name: recognize text from image using Aspose OCR & AI
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer - `asposeocr` package (`pip install asposeocr`) -
      An image file (e.g., `doc.png`) that contains printed or handwritten text -
      Optional: a GPU for faster LLM inference (the script works on CPU too)'
  - name: Install and import the required modules
    text: '```python # Install the library (run once in your environment) # pip install
      asposeocr'
  - name: Create the OCR engine and enable handwritten text recognition
    text: '```python # Initialise the OCR engine ocr_engine = ocr.OcrEngine()'
  - name: Load the image for OCR
    text: '```python # Point the engine at the file you want to process ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
      ```'
  - name: Run the raw OCR pass
    text: '```python # Execute the recognition pipeline and capture the raw result
      raw_result = ocr_engine.recognize() ```'
  - name: Configure the Aspose AI model for LLM post‑processing
    text: '```python ai_config = AsposeAIModelConfig( allow_auto_download="true",
      # Pull the model if missing hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
      hugging_face_quantization="int8", # Reduce RAM usage gpu_layers=20, # Use 20
      GPU layers if a GPU is present directory_model_path="YOUR_DIRECTORY/mo'
  - name: Initialise the AI processor and attach it as a post‑processor
    text: '```python # Instantiate the AI processor with the configuration above ai_processor
      = AsposeAI() ai_processor.initialize(ai_config)'
  - name: Run the post‑processor to enhance the OCR output
    text: '```python # Apply AI‑driven post‑processing enhanced_result = ocr_engine.run_postprocessor(raw_result)'
  - name: Release resources
    text: '```python # Free GPU/CPU memory held by the AI model ai_processor.free_resources()'
  type: HowTo
- questions:
  - answer: No. The script falls back to CPU, but inference will be slower.
    question: Do I need a GPU?
  - answer: Absolutely—just change `hugging_face_repo_id` and adjust `gpu_layers`
      accordingly.
    question: Can I use a different LLM?
  - answer: Resize it first (e.g., using Pillow) to keep memory usage reasonable.
    question: What if my image is huge?
  - answer: You can toggle `enable_handwritten_recognition` depending on your workload.
    question: Is handwritten recognition always on?
  type: FAQPage
tags:
- OCR
- Aspose
- Python
title: 使用 Aspose OCR 与 AI 识别图像中的文本
url: /zh/python/general/recognize-text-from-image-using-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 与 AI 识别图像中的文本

是否曾经需要从图像中识别文本，却不确定哪个库既快又准？你并不孤单。在本指南中，我们将完整演示一个端到端的示例，展示 **如何加载图像进行 OCR**、**如何在图像上执行 OCR**，并使用 Aspose 的 AI 后处理器对输出进行润色。完成后，你将拥有一个可直接运行的脚本，将 PNG 转换为干净、可搜索的文本。

## 你将学到的内容

我们将从安装 Aspose OCR 包到运行结束时释放资源全部覆盖。你会了解为何启用手写文本识别很重要，如何为后处理配置 Qwen 2.5 LLM，以及最终输出的样子。无需外部引用——只需复制、粘贴并运行。

### 前置条件

- Python 3.8 或更高版本  
- `asposeocr` 包（`pip install asposeocr`）  
- 包含印刷或手写文本的图像文件（例如 `doc.png`）  
- 可选：用于加速 LLM 推理的 GPU（脚本也可在 CPU 上运行）

---

## 从图像识别文本 – 步骤详解

在每个代码块下方，你会看到对我们执行该操作的 **原因** 的简短说明，而不仅仅是 **代码做了什么**。

### 步骤 1：安装并导入所需模块

```python
# Install the library (run once in your environment)
# pip install asposeocr

import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig
```

*为什么？* 导入 `asposeocr` 可获得 `OcrEngine` 类，而 `ai` 子模块提供基于 LLM 的后处理器，显著提升原始 OCR 输出。

### 步骤 2：创建 OCR 引擎并启用手写文本识别

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Turn on handwritten‑text support – useful for notes, signatures, etc.
ocr_engine.ocr_settings.enable_handwritten_recognition = True
```

启用手写识别会扩展引擎的字符集，这样在对包含印刷体和手写体混合的图像文件 **执行 OCR** 时，就不会丢失涂鸦。

### 步骤 3：加载图像进行 OCR

```python
# Point the engine at the file you want to process
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
```

`load_image` 调用即为 **加载图像进行 OCR** 的时刻；如果路径错误，引擎会抛出详细异常，帮助你避免后续难以理解的错误。

### 步骤 4：执行原始 OCR 过程

```python
# Execute the recognition pipeline and capture the raw result
raw_result = ocr_engine.recognize()
```

此时你会得到一个 `RecognitionResult` 对象，包含未过滤的文本、置信度分数和布局元数据。结果通常噪声较多——因此需要 AI 驱动的清理。

### 步骤 5：为 LLM 后处理配置 Aspose AI 模型

```python
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # Pull the model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Reduce RAM usage
    gpu_layers=20,                                  # Use 20 GPU layers if a GPU is present
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)
```

为什么要设置这些？  
- **auto‑download** 确保模型在首次运行时即可下载。  
- **int8 quantization** 大幅降低内存需求，且对精度影响不大。  
- **gpu_layers** 让你利用兼容的 GPU 加速推理。

### 步骤 6：初始化 AI 处理器并将其作为后处理器附加

```python
# Instantiate the AI processor with the configuration above
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)

# Hook the AI processor into the OCR engine
ocr_engine.set_post_processor(ai_processor, None)
```

附加处理器后，每次调用 `run_postprocessor` 时，LLM 都会纠正拼写、合并断开的单词，甚至推断缺失的标点。

### 步骤 7：运行后处理器以提升 OCR 输出

```python
# Apply AI‑driven post‑processing
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# Print the polished text
print(enhanced_result.text)
```

`enhanced_result.text` 通常比原始字符串更易读——可以把它看作既能纠错又能理解上下文的拼写检查器。

### 步骤 8：释放资源

```python
# Free GPU/CPU memory held by the AI model
ai_processor.free_resources()

# Dispose of the OCR engine to close file handles, etc.
ocr_engine.dispose()
```

在长期运行的服务中清理资源至关重要；否则会导致 GPU 内存泄漏，最终使应用崩溃。

---

## 你今天即可运行的完整脚本

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Initialise OCR engine with handwritten support
ocr_engine = ocr.OcrEngine()
ocr_engine.ocr_settings.enable_handwritten_recognition = True

# 2️⃣ Load the image you want to analyse
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")   # <-- replace with your path

# 3️⃣ Perform the basic OCR pass
raw_result = ocr_engine.recognize()

# 4️⃣ Set up the AI model for smarter output
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)

# 5️⃣ Initialise and attach the AI post‑processor
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)
ocr_engine.set_post_processor(ai_processor, None)

# 6️⃣ Enhance the OCR result with the LLM
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# 7️⃣ Show the final, cleaned‑up text
print("=== Enhanced OCR Output ===")
print(enhanced_result.text)

# 8️⃣ Clean up
ai_processor.free_resources()
ocr_engine.dispose()
```

**预期输出**（简单发票图像示例）：

```
=== Enhanced OCR Output ===
Invoice #12345
Date: 2024‑04‑01
Total Amount: $1,250.00
Thank you for your business!
```

请注意 AI 层将 “Inv0ice” 修正为 “Invoice”，并补全了缺失的标点。

---

## 常见问题（以及快速答案）

- **我需要 GPU 吗？** 不需要。脚本会回退到 CPU，但推理速度会更慢。  
- **我可以使用其他 LLM 吗？** 当然——只需更改 `hugging_face_repo_id` 并相应调整 `gpu_layers`。  
- **如果我的图像很大怎么办？** 首先对其进行缩放（例如使用 Pillow），以保持内存使用在合理范围。  
- **手写识别是否始终开启？** 你可以根据工作负载切换 `enable_handwritten_recognition`。

---

## 结论

现在你已经了解如何使用 Aspose OCR **识别图像中的文本**、如何 **加载图像进行 OCR**，以及如何通过 AI 增强的后处理 **在图像上执行 OCR**。上面的完整可运行示例为你在任何 Python 项目中集成 OCR 打下了坚实基础——无论是扫描收据、数字化合同，还是提取手写表单中的数据。

准备好下一步了吗？尝试将 Qwen 模型替换为更大的模型，实验不同的量化方案，或将多张图像串联进行批处理。可能性无限，而你刚编写的代码能够优雅地应对这些场景。

祝编码愉快，愿你的 OCR 结果始终清晰如晶！  

![展示增强 OCR 输出的 Python 控制台截图](/images/ocr_output.png){alt="展示如何使用 Aspose OCR 识别图像文本的截图"}

## 接下来你应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在所示技巧之上。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose OCR 从图像提取文本 – 步骤指南](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [将图像转换为文本 – 从 URL 执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [使用 Aspose.OCR 的语言选择提取图像文本（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}