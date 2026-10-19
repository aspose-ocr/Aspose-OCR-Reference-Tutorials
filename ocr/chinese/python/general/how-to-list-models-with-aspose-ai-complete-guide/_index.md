---
category: general
date: 2026-07-05
description: 如何使用 Aspose AI 列出模型、启用自动下载，并在 Python 中下载 Hugging Face 模型。请按照本分步教程设置缓存，立即开始使用
  Aspose AI。
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: zh
og_description: 如何使用 Aspose AI 列出模型、启用自动下载并下载 Hugging Face 模型。学习在几分钟内设置缓存并使用 Aspose
  AI。
og_title: 如何使用 Aspose AI 列出模型——完整教程
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: 如何使用 Aspose AI 列出模型 – 完整指南
url: /zh/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose AI 列出模型 – 完整指南

当你开始在 Python 中尝试大型语言模型时，**如何使用 Aspose AI 列出模型**这个问题会随之而来。在本教程中，我们将演示如何启用 **auto download**、配置本地缓存，并直接从 Hugging Face 拉取模型——这样你就可以无需手动寻找文件即可快速上手。

如果你曾经想过 *“如何使用 Aspose 进行 OCR 驱动的 AI？”* 或者 *“设置模型文件缓存的最简方法是什么？”*，那么你来对地方了。到最后，你将拥有一个完整的脚本，能够列出本地存储的每个模型，自动下载缺失的模型，并准确显示文件在磁盘上的位置。

---

## 你需要的条件

在开始之前，请确保你拥有：

- Python 3.9 或更高（库使用需要近期解释器的类型提示）
- `pip` 用于安装 **Aspose OCR** 包 (`aocr`).  
  ```bash
  pip install aocr
  ```
- 首次从 Hugging Face 下载所需的互联网连接。
- 用于保存模型缓存的文件夹（例如 `./model_cache`）。

就这些——不需要额外的 Docker 容器，也不需要除干净的 Python 安装之外的重量级虚拟环境。

---

## ## 如何使用 Aspose AI 列出模型

本指南的核心是能够 **列出** Aspose AI 本地缓存的模型。一旦缓存设置完成，库就可以枚举它所知道的所有内容，让调试和版本控制变得轻而易举。

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**为什么这样有效：**  
- `AsposeAI()` 创建与底层推理引擎通信的高级入口点。  
- `AsposeAIModelConfig()` 包含所有可调参数；将 `allow_auto_download` 设置为 `"true"` 告诉库自动从指定的仓库获取缺失文件。  
- `directory_model_path` 是 *缓存目录*——所有下载的二进制文件所在的位置。  
- `initialize()` 应用配置，如果缓存为空则执行首次下载。  
- 最后，`list_local()` 扫描缓存文件夹并返回模型标识符的 Python 列表，我们将其打印出来。

### 预期输出（首次运行）

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

如果你再次运行脚本，库将跳过下载，直接列出已经存在的模型，证明 **如何设置缓存** 在后续运行中真的能节省时间。

---

## ## 为缺失模型启用自动下载

在多个项目中使用多个模型时，手动从 Hugging Face 拉取每个模型会非常繁琐。通过启用自动下载，Aspose AI 会自行完成繁重的工作。

```python
cfg.allow_auto_download = "true"
```

> **专业提示：** 在开发或 CI 环境中 **仅** 将 `allow_auto_download` 保持为 `"true"`。在生产环境中，你可能希望锁定缓存，以避免意外的网络流量。

如果以后决定关闭它，只需在再次调用 `initialize()` 之前将该标志设为 `"false"` 即可。

---

## ## 动态下载 Hugging Face 模型

下面这行代码

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

告诉 Aspose AI 从哪个远程仓库拉取模型。库支持任何提供 GGUF 文件的公开 Hugging Face 模型。想换模型？只需替换仓库 ID：

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

运行脚本时，Aspose AI 会检查缓存：

- **如果模型已存在**，则立即加载。  
- **如果不存在**，自动下载标志会触发下载，将文件存储在 `directory_model_path` 下，并立即注册供使用。

这种方式消除了许多教程强制的 “先下载后运行” 两步流程。

---

## ## 列出模型后如何使用 Aspose AI

列出模型只是第一步。确认模型已存在后，你就可以开始推理：

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**为什么这很重要：**  
- `run_inference()` 抽象了分词、批处理和 GPU 处理。  
- 通过传入从 `list_local()` 获得的 *模型名称*，确保推理调用匹配磁盘上的确切文件。

---

## ## 为多个项目设置缓存位置

如果你在多个项目之间切换，可能希望每个项目拥有自己的缓存文件夹。`directory_model_path` 字段只是普通字符串，你可以动态构建它：

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

现在每个项目都会得到一个独立的子文件夹（`./model_cache/sentiment_analysis`），避免版本冲突，并且清理工作也更简单。

---

## ## 常见陷阱及规避方法

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| **`PermissionError` 在访问缓存时** | 缓存文件夹被其他用户拥有（共享服务器上常见） | 手动创建文件夹并设置适当权限：`mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **模型未出现在 `list_local()` 中** | `allow_auto_download` 设置为 `"false"` 且模型尚未缓存 | 临时打开该标志，运行一次后如需可再关闭 |
| **意外的模型版本** | 两个不同的仓库使用相同名称但文件不同 | 固定确切的仓库 ID（包括标签/提交），或在首次成功拉取后通过禁用 auto‑download 锁定缓存 |
| **内存不足错误** | 在 RAM/VRAM 不足的机器上使用大型 GGUF 文件 | 使用更小的模型（例如 `Qwen2.5-1.5B`）或将 `cfg.device = "cpu"` 设置为强制 CPU 推理 |

---

## ## 完整脚本（可复制粘贴）

下面是整合了上述所有概念的完整可运行示例。将其保存为 `list_models_demo.py` 并使用 `python list_models_demo.py` 执行。

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**运行它** 将产生与前面示例类似的输出，随后是模型给出的简洁答案。随意替换提示内容——这是在 **如何列出模型** 之后最快速验证模型是否真正可用的方法。

---

## ## 总结

我们已经覆盖了使用 Aspose AI **如何列出模型** 所需的全部内容，从启用 **auto download** 到配置持久 **缓存**，以及按需拉取 **Hugging Face 模型**。关键要点：

1. 创建 `AsposeAI` 对象和 `AsposeAIModelConfig`。  
2. 将 `allow_auto_download = "true"` 并将 `directory_model_path` 指向你控制的文件夹。  
3. 初始化 AI，然后调用 `list_local()` 查看缓存的具体内容。  
4. 使用列出的模型名称进行推理，即可构建真实世界的应用。

---

## 接下来该做什么？

- **尝试不同的模型** – 将 `cfg.hugging_face_repo_id` 替换为其他仓库，观察列表变化。  
- **微调缓存**  

## 接下来你应该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并在项目中探索替代实现方式，每篇都包含完整可运行的代码示例和逐步解释。

- [如何在 Aspose.OCR for .NET 中使用列表批量 OCR 图像](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [如何在 Java 中设置 Aspose OCR 许可证并验证](/ocr/english/java/ocr-basics/set-license/)
- [如何使用 Aspose.OCR for .NET 从图像中提取文本](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}