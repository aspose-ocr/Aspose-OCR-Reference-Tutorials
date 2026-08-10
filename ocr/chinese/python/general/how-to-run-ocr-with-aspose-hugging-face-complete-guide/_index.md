---
category: general
date: 2026-04-29
description: 了解如何对扫描件运行 OCR，自动使用 Hugging Face 模型，并在几分钟内使用 Aspose OCR 识别扫描件中的文本。
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: zh
og_description: 如何使用 Aspose OCR 对扫描件进行 OCR，自动下载 Hugging Face 模型，并获得干净且带标点的文本。
og_title: 如何使用 Aspose 与 Hugging Face 进行 OCR – 完整指南
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: 如何使用 Aspose 与 Hugging Face 进行 OCR – 完整指南
url: /zh/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 与 Hugging Face 运行 OCR – 完整指南

是否曾想过 **如何在一堆扫描文档上运行 OCR**，却不想花费数小时去调参？你并不孤单。在许多项目中，开发者需要 **快速识别扫描文本**，但常常在模型下载和后处理上卡壳。

好消息：本教程提供了一个开箱即用的解决方案，**使用 Hugging Face 模型**，自动下载，并添加标点，使输出看起来像人类撰写。完成后，你将拥有一个脚本，能够处理文件夹中的每张图片，并在每个扫描文件旁生成干净的 `.txt` 文件。

## 你需要准备的环境

- Python 3.8+（代码使用 f‑strings，旧版本不兼容）
- `aspose-ocr` 包（通过 `pip install aspose-ocr` 安装）
- 首次下载模型时需要网络连接  
- 一个存放图像扫描件的文件夹（`.png`、`.jpg` 或 `.tif`）

就这些——无需额外二进制文件，无需手动模型配置。让我们开始吧。

![运行 OCR 示例](https://example.com/ocr-demo.png "运行 OCR 示例")

## 第一步：导入 Aspose OCR 类并设置环境

我们首先从 Aspose OCR 库中导入所需的类。提前导入所有内容可以让脚本保持整洁，也便于快速发现缺失的依赖。

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*为什么重要*：`OcrEngine` 承担核心识别工作，而 `AsposeAI` 让我们能够接入大型语言模型进行更智能的后处理。如果缺少导入，后面的代码根本无法编译——一定要记得这一步。

## 第二步：配置支持 GPU 的 Hugging Face 模型  

现在告诉 Aspose 从哪里获取模型，以及有多少层将在 GPU 上运行。`allow_auto_download="true"` 标志会为你 **自动下载模型**。

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **小技巧**：如果没有 GPU，设置 `gpu_layers=0`。模型会回退到 CPU，速度会慢一些，但仍能正常工作。

### 为什么选择 Hugging Face 模型？

Hugging Face 提供了海量即用的 LLM。指向 `Qwen/Qwen2.5-3B-Instruct-GGUF`，即可获得一个体积小、指令微调的模型，能够添加标点、纠正空格，甚至修正轻微的 OCR 错误。这正是 **使用 Hugging Face 模型** 的实际价值所在。

## 第三步：初始化 AI 引擎并启用标点后处理  

AI 引擎不仅用于聊天——这里我们挂载一个 *标点添加器*，对原始 OCR 输出进行清理。

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*发生了什么*？`set_post_processor` 调用注册了内置的后处理器，在 OCR 引擎完成后运行。它会在适当的位置插入逗号、句号和大写字母，使最终文本更易阅读。

## 第四步：创建 OCR 引擎并关联 AI 引擎  

将 AI 引擎与 OCR 引擎连接后，我们得到一个既能识别字符又能润色结果的统一对象。

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

如果跳过此步骤，OCR 仍能工作，但会失去标点提升——输出将会是一连串没有间隔的词语。

## 第五步：处理文件夹中的每张图片  

下面是本教程的核心。我们遍历文件夹中的每张图片，执行 OCR，应用后处理器，并将清理后的文本写入同名的 `.txt` 文件。

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### 预期结果

运行脚本后会打印类似如下信息：

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

每行会显示置信度分数（快速健康检查），并生成 `invoice_001.png.txt`、`receipt_2024.tif.txt` 等文件，里面包含已加标点、可读性强的文本。

### 边缘情况与变体

- **非英文扫描**：将 `hugging_face_repo_id` 切换为多语言模型（例如 `microsoft/Multilingual-LLM-GGUF`）。
- **大批量处理**：将循环包装在 `concurrent.futures.ThreadPoolExecutor` 中实现并行处理，但需注意 GPU 内存限制。
- **自定义后处理**：如果需要领域特定的清理（如去除发票号码），可将 `"punctuation_adder"` 替换为自己的脚本。

## 第六步：清理资源  

任务完成后，释放资源可以防止内存泄漏，尤其在长时间运行的服务中尤为重要。

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

忽视此步骤可能导致 GPU 内存残留，进而影响后续运行。

## 小结：端到端运行 OCR 的完整流程  

仅用几行代码，我们展示了 **如何在文件夹的扫描件上运行 OCR**，**使用首次自动下载的 Hugging Face 模型**，并 **在识别文本时自动添加标点**。完整脚本已准备好复制粘贴，修改路径后即可执行。

## 后续步骤与相关主题  

- **批量后处理**：探索 `ocr_engine.run_batch_postprocessor` 以实现更快的批量处理。  
- **替代模型**：如果需要语音转文字，可尝试 `openai/whisper` 系列模型。  
- **与数据库集成**：将提取的文本存入 SQLite 或 Elasticsearch，实现可搜索的文档档案。  

尽情实验——更换模型、调节 `gpu_layers`，或添加自定义后处理器。Aspose OCR 与 Hugging Face 模型中心的组合，为任何文档数字化项目提供了灵活且强大的基础。

---

*祝编码愉快！如果遇到问题，欢迎在下方留言或查阅 Aspose OCR 文档获取更深入的配置选项。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}