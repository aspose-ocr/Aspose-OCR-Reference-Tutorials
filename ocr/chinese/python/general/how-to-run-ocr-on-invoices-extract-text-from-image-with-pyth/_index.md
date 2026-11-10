---
category: general
date: 2026-01-07
description: 如何运行 OCR 并从图像中提取发票文本。学习提升 OCR 准确率、加载图像进行 OCR，以及高效处理发票 OCR。
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: zh
og_description: 一步步教你在发票上运行 OCR。提取图像中的文本，提高 OCR 准确率，并使用 Aspose AI 加载图像进行 OCR。
og_title: 如何对发票进行 OCR – 完整的 Python 指南
tags:
- OCR
- Python
- Image Processing
title: 如何在发票上进行 OCR – 使用 Python 从图像中提取文本
url: /zh/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在发票上运行 OCR – 使用 Python 从图像中提取文本

是否曾想过 **如何在扫描的发票上运行 OCR** 并获得干净、可搜索的文本？你并不孤单。许多开发者在原始 OCR 输出充斥拼写错误、断裂的换行以及缺失标点时卡住了。本文将演示一个全栈解决方案，不仅 **从图像中提取文本**，还能通过 Aspose AI 模型的后处理 **提升 OCR 准确率**。

你将看到如何 **加载图像进行 OCR**、运行内置引擎，然后应用轻量级拼写检查，使结果可直接用于下游分析。完成后，你将拥有一个可复用的脚本，能够轻松嵌入任何发票处理流水线。

> **你需要准备的内容**  
> * Python 3.9 或更高版本  
> * `aspose-ocr` 与 `aspose-ai` 包（通过 `pip` 安装）  
> * 一张发票图像（PNG、JPEG 或 TIFF）——本文示例使用 `sample_invoice.png`  
> * 可选：至少 4 GB VRAM 的 GPU，以加速模型推理（脚本在 CPU 上也可运行）

---

## 步骤 1：安装必需的包并准备环境

在 **加载图像进行 OCR** 之前，需要确保所需库已就绪。Aspose OCR 引擎自带一个简易的 Python 包装器，而 AI 后处理器依赖 Hugging Face 量化模型。

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **小贴士：** 若计划使用 GPU 加速，请安装带 CUDA 支持的 `torch`（`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`）。

---

## 步骤 2：加载发票图像

加载图像非常直接，但值得说明为何要将路径写成原始字符串 (`r"..."`)。这可以避免 Windows 路径中的转义字符导致的意外错误。

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*为什么重要：* 使用 `ocr.Image.load` 可确保图像在加载时已进行二值化、去倾斜等预处理，这些都是 Aspose 的最佳默认设置，能够在任何 AI 操作之前 **提升 OCR 准确率**。

---

## 步骤 3：运行内置 OCR 引擎

现在我们真正 **运行 OCR** 并捕获原始文本。此步骤展示了普通 OCR 运行时的典型输出——往往充斥换行混乱和偶发的拼写错误。

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**典型原始输出**（为简洁起见已截断）：

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

你可能会注意到 “Invoice” 被识别为 “Invo1ce”，或是标点缺失。这时 AI 后处理器就派上用场了。

---

## 步骤 4：配置 Aspose AI 模型

我们将使用的 AI 模型是 **Qwen2.5‑3B‑Instruct‑GGUF**，这是一款轻量级指令微调 LLM，能够在中等 GPU 上流畅运行。下面的配置告诉 Aspose 从何处获取模型、在 GPU 上保留多少层以及处理长段落所需的上下文大小。

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **为何这样配置？**  
> * `gpu_layers=30` 在速度与显存之间取得平衡——大部分推理在 GPU 上完成，剩余层留在 CPU，避免 OOM 错误。  
> * `context_size=4096` 确保模型一次性看到整张发票，防止重要字段被截断。

---

## 步骤 5：创建简易拼写检查后处理器

我们将在一个名为 `simple_spell_check` 的小函数中封装 AI 调用。提示语故意简短：“Correct spelling and punctuation:” 后接原始 OCR 文本。模型会返回已清理的版本。

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**工作原理：** `ai.run_prompt` 将提示发送给本地加载的 LLM，模型返回一个包含纠正后拼写、正确标点以及更自然换行布局的单字符串。

---

## 步骤 6：对原始 OCR 文本应用后处理器

现在魔法出现了。我们把原始 OCR 输出喂给后处理器，并打印增强后的结果。

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**示例增强输出**：

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

可以看到 “Invoice” 的拼写已纠正，冒号使用恰当，换行保持一致——这正是可靠下游解析所需的格式。

---

## 步骤 7：清理资源

OCR 引擎和 AI 模型都会分配本地资源。长时间运行的服务中，使用完毕后释放它们是良好实践。

```python
ai.free_resources()
engine.dispose()
```

---

## 完整脚本 – 直接复制使用

下面是完整、可直接运行的脚本。将其保存为 `invoice_ocr.py`，将 `YOUR_DIRECTORY` 替换为存放发票图像的文件夹路径，然后使用 `python invoice_ocr.py` 执行。

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

运行脚本后，你将看到嘈杂的原始 OCR 输出以及经过 **提升 OCR 准确率** 的清晰版本并排展示。

---

## 常见问题与边缘情况

### 1. 我的发票图像是多页 PDF？

Aspose OCR 能直接加载 PDF 页面。将图像加载行替换为：

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

遍历 `page_index` 即可顺序处理每一页。

### 2. 我的 GPU 显存不足——可以只用 CPU 吗？

完全可以。在 `AsposeAIModelConfig` 中将 `gpu_layers=0`。模型将全程在 CPU 上运行，速度会慢一些，但对低配硬件更安全。

### 3. 如何处理非英文发票？

将模型仓库 ID 替换为对应语言的模型，例如 `"mistralai/Mistral-7B-Instruct-v0.2"` 以获得多语言支持。其余管道保持不变。

### 4. 能否链式使用多个后处理器（例如格式化日期、提取总额）？

可以。`ai.set_post_processor` 接受一个可调用列表。例如：

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

输出将先进行拼写检查，随后提取总额等信息。

---

## 性能技巧与最佳实践

| 技巧 | 作用说明 |
|-----|----------|
| **批量处理多张发票** – 将它们放入列表并在循环中处理。 | 减少 Python 解释器开销，让 AI 模型保持热状态。 |
| **缓存模型** – 在 Web 服务中避免重复调用 `initialize`。 | 模型加载约需 30 秒，缓存后可实现瞬时响应。 |
| **在 OCR 前将大图缩放至 1500 px 宽**。 | 更小的图像加速 OCR 与 AI 推理，且不显著影响准确率。 |
| **生产环境将 `allow_auto_download="false"`** – 随部署一起打包模型。 | 确保启动时间可预期，避免网络波动。 |

---

## 结论

我们已经完整演示了 **如何在发票上运行 OCR**，从加载图像到使用 AI 驱动的拼写检查提升结果。遵循这些步骤，你可以可靠地 **从图像中提取文本**、**提升 OCR 准确率**，并在任何基于 Python 的工作流中无缝 **处理发票 OCR**。

不妨尝试不同的发票版式——手写收据或扫描合同均可。相同的流水线只需微调即可适配，证明结构良好的 OCR + AI 组合是任何文档自动化项目的多功能利器。

如果本指南对你有帮助，欢迎分享给团队成员或给托管 Aspose 包的仓库点星。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}