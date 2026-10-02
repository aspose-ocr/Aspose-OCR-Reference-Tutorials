---
category: general
date: 2026-01-12
description: 如何使用 Aspose OCR 和轻量级 Hugging Face 模型对发票图像进行 OCR 并提取文本。学习下载模型、纠正 OCR 错误以及在图像上执行
  OCR。
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: zh
og_description: 如何对发票图像进行 OCR，提取文本，并使用 Hugging Face LLM 修复错误。请遵循本完整指南，获得完美结果。
og_title: 如何在发票图片上运行 OCR – 完整教程
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: 如何对发票图片进行 OCR – 完整的分步指南
url: /zh/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在发票图像上运行 OCR – 完整分步指南

是否曾想过 **如何在扫描的发票上运行 OCR** 并获得干净、可搜索的文本，而无需花费数小时进行清理？你并不是唯一有此困惑的人。在许多真实项目中，原始 OCR 输出充斥着误识别——比如把 “0” 识别成 “O”、把 “1” 识别成 “l”，甚至整段文字乱码。好消息是？只需几行 Python 代码，你不仅可以 **perform OCR on image** 文件，还能使用 Hugging Face 的轻量模型自动 **correct OCR errors**。

在本教程中，我们将逐步讲解你需要了解的所有内容：从加载发票图像、提取原始文本、下载量化模型，到打磨结果，使你获得可直接用于后续处理的完美转录。完成后，你将能够在单个可重复使用的脚本中 **extract text from invoice** PDF 或 PNG 文件。

## 前置条件与环境设置

在深入之前，请确保你具备以下条件：

| 需求 | 重要原因 |
|-------------|----------------|
| Python 3.9+ | 现代语法和类型提示 |
| `aspose-ocr` package | 提供示例中使用的 `ocr.OcrEngine` |
| `aspose-ai` package | 提供 `AsposeAI` 后处理器 |
| Access to a GPU (optional) | 加速 LLM 层；否则 CPU 也能正常工作 |
| Internet connection (first run) | 需要自动 **download Hugging Face model** |

你可以使用以下方式安装所需库：

```bash
pip install aspose-ocr aspose-ai
```

> **专业提示：** 如果计划在 GPU 上运行 LLM，请安装带有 CUDA 支持的 `torch`（`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`）。

环境准备就绪后，让我们进入代码部分。

---

## 第一步 – 初始化 OCR 引擎并加载发票图像

首先，你需要创建 Aspose OCR 引擎的实例，并指向要处理的文件。此步骤是 **how to run OCR** 在任何图像上的基础。

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **为什么重要：** `load_image` 支持 PNG、JPEG、TIFF，甚至 PDF 页面，使你能够 **perform OCR on image** 数据，无论格式如何。

---

## 第二步 – 运行基础 OCR 以捕获原始文本

图像加载后，引擎可以生成原始转录。该输出通常噪声较多，这也是我们随后进行纠正步骤的原因。

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

典型的原始输出可能如下所示：

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

注意到应该是字母 “O” 的位置出现了数字零 (`0`) 吗？这正是我们稍后要修正的错误类型。

---

## 第三步 – 使用轻量 LLM 配置 AI 后处理器

现在我们引入一个 **download Hugging Face model**，它足够小，可在普通硬件上运行，却又足以理解发票语言。示例使用 Qwen 2.5 3B‑Instruct GGUF 模型，量化为 `int8`，占用极小的内存。

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

**为什么选择此模型？** `int8` 量化将文件大小压缩至约 1.2 GB，使其在大多数笔记本电脑上可行。GPU 层可加速推理，但当未检测到 GPU 时，代码会优雅地回退到 CPU。

---

## 第四步 – 对原始 OCR 结果进行基于 LLM 的纠正

模型准备好后，我们将原始文本输入后处理器。LLM 将重写转录，修复常见 OCR 错误并规范数字。

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

预期的清理后输出：

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

你可以看到数字零已恢复为字母 “O”，且 “Am0unt” 已变为 “Amount”。这正是 **correct OCR errors** 的自动核心。

---

## 第五步 – 释放资源并清理

大型语言模型可能占用 GPU 内存，因此在完成后释放资源是良好实践。

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

如果计划批量处理大量发票，你可以保持模型加载状态，仅在脚本结束时释放。

---

## 完整工作示例

将所有内容整合在一起，下面是一段可以直接保存为 `.py` 文件并运行的脚本：

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

运行脚本后应产生与前面 “AI‑corrected” 区块相似的输出。随意将图像路径替换为其他发票或收据，以批量 **extract text from invoice** 文件。

---

## 常见问题与边缘情况

### 如果没有 GPU 怎么办？

`gpu_layers` 参数是可选的。将其设为 `0` 或省略，模型将完全在 CPU 上运行。预期推理速度较慢——在现代笔记本上每页约 2–3 秒。

### 我的发票是多页 PDF，如何处理？

将每页转换为单独的图像（例如使用 `pdf2image`），并在同一脚本中循环处理各页。OCR 引擎可以独立处理每张图像，LLM 将纠正每段文本。

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### 在防火墙后模型下载失败怎么办？

手动从 Hugging Face 模型中心下载模型，解压到本地文件夹，并将 `hugging_face_repo_id` 指向本地路径：

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### 纠正的准确率如何？

对于典型的英文发票，LLM 能修正超过 95 % 的常见 OCR 误识别。复杂的手写备注仍可能需要人工审查。

---

## 生产环境使用技巧与窍门

- **批量处理：** 将步骤 2‑4 包装成函数并传入文件路径列表。复用同一个 `AsposeAI` 实例以避免重新加载模型。
- **日志记录：** 用 Python 的 `logging` 模块替换 `print`，以捕获原始和纠正后的输出用于审计追踪。
- **错误处理：** 用 `try/except` 块包裹 OCR 调用。如果图像处理失败，记录文件名并继续。
- **性能调优：** 尝试不同的 `gpu_layers`。在 GPU 上使用更多层可加速推理，但会增加显存占用。

---

## 结论

我们已经从头到尾讲解了 **how to run OCR** 在发票图像上的完整流程，展示了如何 **perform OCR on image**、**download Hugging Face model**，以及自动 **correct OCR errors**。完整脚本演示了一个实用工作流，可直接嵌入任何基于 Python 的自动化流水线。

下一步？尝试扩展流水线，使用正则表达式在纠正后的文本中 **extract key fields**（发票号、日期、总额），或将清理后的输出写入数据库以实现可搜索记录。如果需要其他语言或领域的知识，也可以尝试 Hugging Face 的其他轻量 LLM。

祝编码愉快，愿你的 OCR 结果始终清晰如水！

![在发票图像上运行 OCR 的示例](ocr_invoice_example.png "在发票上运行 OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}