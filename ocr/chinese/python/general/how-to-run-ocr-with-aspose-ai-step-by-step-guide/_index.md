---
category: general
date: 2026-02-09
description: 如何使用 Aspose AI 和 Hugging Face 模型运行 OCR —— 学习下载 Hugging Face 模型、纠正 OCR
  错误并释放 GPU 内存。
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: zh
og_description: 在第一段中解释了如何使用 Aspose AI 运行 OCR——了解如何下载 Hugging Face 模型、纠正 OCR 错误并释放
  GPU 内存。
og_title: 如何使用 Aspose AI 运行 OCR – 完整指南
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: 如何使用 Aspose AI 进行 OCR – 步骤指南
url: /zh/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose AI 运行 OCR – 完整指南

Ever wondered **how to run OCR** on a scanned invoice and get perfectly clean numbers without spending hours fixing typos? You're not alone. In many real‑world projects the raw text that comes out of a classic OCR engine still contains stray characters, broken currency symbols, or garbled digits—especially when the source image is noisy.  

The good news is that you can hook an LLM up to Aspose OCR, download a Hugging Face model on‑the‑fly, and let the AI polish the output for you. In this tutorial we’ll walk through the whole pipeline, from pulling the model (yes, we’ll show you how to **download hugging face model** automatically) to freeing up GPU resources when you’re done. By the end you’ll have a reproducible script that **corrects OCR errors**, runs fast on a modest GPU, and cleans up after itself so you don’t waste memory.

## 您将学到的内容

- Configure Aspose AI to fetch a **Qwen2.5‑3B‑Instruct‑GGUF** model from Hugging Face.
- Run the standard Aspose OCR engine on an image file.
- Use a custom LLM prompt that keeps numbers and currency symbols intact.
- Release GPU memory with the built‑in **free gpu memory** routine.
- Tweak the workflow for edge cases like multi‑page PDFs or low‑end GPUs.

> **前提条件** – Python 3.9+、`aspose-ocr` 包、首次模型下载需要网络、以及至少 4 GB VRAM 的 GPU（可选但推荐）。如果没有 GPU，脚本会自动回退到 CPU 运行剩余层。

---

## 如何运行 OCR 并提升结果

下面是完整的、可直接运行的 Python 脚本。将其保存为 `ocr_with_ai.py` 并将占位路径替换为你自己的文件路径。

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **专业提示**：`gpu_layers` 参数可以让你决定有多少 transformer 层在 GPU 上运行。如果出现显存不足错误，降低该数值，其余层将在 CPU 上执行——随后仍可使用 `ai.free_resources()` **free gpu memory**。

### 预期输出

在示例发票上运行脚本会得到类似以下内容：

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

可以看到 AI 将 `$1O0.00` 中的 “O” 正确纠正为零，同时保留了美元符号。这正是对金融文档 **correct OCR errors** 的核心。

---

## 下载 Hugging Face 模型 – 背后发生了什么？

当你将 `allow_auto_download="true"` 设置为 true 时，Aspose AI 包装器会检查 `directory_model_path`。如果模型文件不存在，它会访问 Hugging Face Hub，拉取 **int8‑quantized** 版本的 `Qwen2.5‑3B‑Instruct‑GGUF`，并将其存储在本地。此一次性下载通常在 2 GB 以下，即使在容量有限的 SSD 上也能轻松容纳。

> **为什么使用 int8？** 将模型量化为 8 位可以显著降低内存占用——这在你希望在处理后 **free gpu memory** 时尤为关键。精度会有极小的下降，但对 OCR 文本的后处理影响可以忽略不计。

如果你更愿意自行托管模型，只需将 `.gguf` 文件放入 `YOUR_DIRECTORY/Models`，Aspose 将直接加载，无需再次访问网络。

---

## 如何释放 GPU – 最佳实践

在许多工作站上，GPU 资源是共享的。脚本结束后仍保留张量会导致后续任务出现 “CUDA out of memory” 错误。`ai.free_resources()` 调用会执行三件事：

1. **释放底层 transformer** – 所有驻留在 GPU 上的权重被释放。
2. **清理 PyTorch 缓存** – 内部调用 `torch.cuda.empty_cache()`。
3. **删除临时文件** – 下载过程中产生的磁盘缓存会被移除。

如果你在同一环境中还使用其他 PyTorch 任务，也可以手动调用 `torch.cuda.empty_cache()`，但内置方法通常已经足够。

---

## 步骤详解（含二级关键词）

### 自动下载 Hugging Face 模型

`AsposeAIModelConfig` 构造函数已经封装了与 Hugging Face API 的交互细节。只需确保第一次运行脚本时能够访问互联网。之后模型会保存在 `YOUR_DIRECTORY/Models`，后续运行即可瞬间启动。

### 推理后释放 GPU 显存

如果你在长时间运行的服务（例如 Flask API）中使用此功能，请在每次请求结束后调用 `ai.free_resources()`。这可以防止内存泄漏，确保下一个请求能够顺利复用同一块 GPU。

### 使用自定义 Prompt 修正 OCR 错误

我们的 `financial_prompt` 函数返回一个仅包含 `prompt` 键的字典。你可以根据任何业务领域自行定制：

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

只需在 `ai.set_post_processor(...)` 中替换函数名，即可得到针对医疗记录的 **correct OCR errors** 流程。

### 在多页 PDF 上运行 OCR

Aspose OCR 本身就支持直接处理 PDF：

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

获取原始字符串后，同一 LLM 后处理器会逐页清理文本，无需额外代码。

### 没有 GPU 时如何释放 GPU（即使没有 GPU）

即便在仅 CPU 的机器上，调用 `ai.free_resources()` 也不会产生副作用。它仅会清理内部缓存，从而释放 RAM。因此 **how to free gpu** 的建议在任何环境下都适用：使用后务必清理。

---

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **GPU 显存不足** | `gpu_layers` 对你的显卡来说设置过高 | 将 `gpu_layers` 降至 10 或 5，其余层在 CPU 上运行 |
| **模型始终无法下载** | 企业防火墙阻止了对 huggingface.co 的 HTTPS 访问 | 在其他网络环境手动下载模型，然后将 `directory_model_path` 指向本地文件夹 |
| **数字被破坏** | Prompt 未明确要求保留数字 | 在 Prompt 中加入 “preserve all numeric values and currency symbols exactly as they appear” |
| **`free_resources` 抛出异常** | 使用了旧版 Aspose OCR | 更新至最新 `aspose-ocr` 包 (pip install --upgrade aspose-ocr) |

---

## 完整示例回顾

下面再次提供完整脚本，并附带逐行解释的注释，方便日后参考：

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## 结论

我们已经完整演示了 **how to run OCR** 与 Aspose 的结合方式，如何按需下载 Hugging Face 模型，如何编写 Prompt 以 **correct OCR errors**，以及如何 **free gpu memory** 让工作站保持响应。整个工作流仅需一个独立的 Python 文件——无需额外脚本、无需手动模型管理，也不会留下残留的 GPU 分配。

下一步？尝试将 `financial_prompt` 替换为一个

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}