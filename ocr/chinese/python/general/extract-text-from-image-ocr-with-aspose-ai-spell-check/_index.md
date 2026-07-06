---
category: general
date: 2026-05-03
description: 使用 Aspose OCR 和 AI 拼写检查从图像中提取文本。学习如何对图像进行 OCR、加载图像进行 OCR、识别发票中的文本并释放
  GPU 资源。
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: zh
og_description: 使用 Aspose OCR 和 AI 拼写检查从图像中提取文本。一步步指南，涵盖如何对图像进行 OCR、加载图像进行 OCR，以及释放
  GPU 资源。
og_title: 从图像提取文本 – 完整的 OCR 与拼写检查指南
tags:
- OCR
- Aspose
- AI
- Python
title: 从图像中提取文本 – Aspose AI 拼写检查的 OCR
url: /zh/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像提取文本 – 完整 OCR 与拼写检查指南

是否曾需要 **从图像提取文本**，却不确定哪个库既快又准？你并不孤单。在许多真实项目中——比如发票处理、收据数字化或合同扫描——从图片中获取干净、可搜索的文本是第一道难关。

好消息是，Aspose OCR 搭配轻量级 Aspose AI 模型，只需几行 Python 代码即可完成这项工作。在本教程中，我们将演示 **如何 OCR 图像**、正确加载图片、运行内置的拼写检查后处理器，最后 **释放 GPU 资源**，让你的应用保持内存友好。

阅读完本指南后，你将能够 **识别发票图像中的文本**，自动纠正常见的 OCR 错误，并为下一个批次保持 GPU 清洁。

---

## 你需要准备的环境

- Python 3.9 或更高（代码使用类型提示，但在更早的 3.x 版本也可运行）
- `aspose-ocr` 与 `aspose-ai` 包（通过 `pip install aspose-ocr aspose-ai` 安装）
- 可选的 CUDA‑enabled GPU；如果未检测到 GPU，脚本会回退到 CPU
- 示例图片，例如 `sample_invoice.png`，放在可引用的文件夹中

无需大型机器学习框架，也不需要庞大的模型下载——只需一个小巧的 Q4‑K‑M 量化模型，能够轻松适配大多数 GPU。

---

## 第一步：初始化 OCR 引擎 – extract text from image

首先创建一个 `OcrEngine` 实例，并指定期望的语言。这里我们选择 English 并请求纯文本输出，这对后续处理最为理想。

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**为什么重要：** 设置语言可以缩小字符集范围，提高识别准确度。纯文本模式会去除布局信息，正好适用于只想 **从图像提取文本** 的场景。

---

## 第二步：加载图像进行 OCR – how to OCR image

接下来将实际图片喂给引擎。`Image.load` 辅助函数支持常见格式（PNG、JPEG、TIFF），并抽象了文件 I/O 的细节。

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**提示：** 如果源图片尺寸较大，建议在送入引擎前先进行缩放；较小的分辨率可以降低 GPU 内存占用，而不会显著影响识别质量。

---

## 第三步：配置 Aspose AI 模型 – recognize text from invoice

Aspose AI 附带一个小型 GGUF 模型，可自动下载。示例使用 `Qwen2.5‑3B‑Instruct‑GGUF` 仓库，量化为 `q4_k_m`。我们还指示运行时在 GPU 上分配 20 层，以在速度和显存之间取得平衡。

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**内部原理：** 量化模型在磁盘上约为 1.5 GB，仅为全精度模型的一小部分，但仍能捕捉足够的语言细微差别，以标记常见的 OCR 拼写错误。

---

## 第四步：初始化 AsposeAI 并挂载拼写检查后处理器

Aspose AI 包含现成的拼写检查后处理器。将其挂载后，所有 OCR 结果都会自动清理。

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**为什么使用后处理器？** OCR 引擎常把 “Invoice” 误读为 “Invo1ce”，或把 “Total” 误读为 “T0tal”。拼写检查会在原始字符串上运行轻量语言模型，自动纠正这些错误，无需自行编写字典。

---

## 第五步：在 OCR 结果上运行拼写检查后处理器

所有配置就绪后，只需一次调用即可得到校正后的文本。我们同时打印原始文本和清理后的文本，方便对比改进效果。

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

发票的典型输出可能如下所示：

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

可以看到 “Invo1ce” 已被正确纠正为 “Invoice”。这正是内置 AI 拼写检查的威力所在。

---

## 第六步：安全释放 GPU 资源 – release gpu resources safely

如果你在长时间运行的服务中使用（例如每分钟处理数十张发票的 Web API），必须在每个批次后释放 GPU 上下文。否则会出现内存泄漏，最终导致 “CUDA out of memory” 错误。

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**专业技巧：** 将 `free_resources()` 放在 `finally` 块或上下文管理器中，以确保即使出现异常也能执行释放操作。

---

## 完整示例代码

将上述所有片段组合在一起，即可得到一个可直接放入任意项目的独立脚本。

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

保存文件，修改图片路径，然后运行 `python extract_text_from_image.py`。你应该会在控制台看到已清理的发票文本。

---

## 常见问题解答 (FAQ)

**Q: 这在仅有 CPU 的机器上能运行吗？**  
A: 完全可以。如果未检测到 GPU，Aspose AI 会回退到 CPU 执行，虽然速度会慢一些。你也可以通过设置 `model_cfg.gpu_layers = 0` 强制使用 CPU。

**Q: 如果我的发票使用的不是英文怎么办？**  
A: 将 `ocr_engine.language` 改为相应的枚举值（例如 `aocr.Language.Spanish`）。拼写检查模型支持多语言，但使用针对特定语言的模型可能会得到更好效果。

**Q: 能否在循环中处理多张图片？**  
A: 能。只需将加载、识别和后处理步骤放入 `for` 循环中。若复用同一 AI 实例，记得在循环结束后或每个批次后调用 `ocr_ai.free_resources()`。

**Q: 模型下载大小是多少？**  
A: 量化的 `q4_k_m` 版本约为 1.5 GB。首次运行后会被缓存，后续执行几乎是瞬时的。

---

## 结论

本教程展示了如何使用 Aspose OCR **从图像提取文本**、配置小型 AI 模型、应用拼写检查后处理器，并安全 **释放 GPU 资源**。整个工作流覆盖了从加载图片到清理资源的全部步骤，为 **recognize text from invoice** 场景提供了可靠的流水线。

下一步？尝试将拼写检查替换为自定义的实体抽取模型

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}