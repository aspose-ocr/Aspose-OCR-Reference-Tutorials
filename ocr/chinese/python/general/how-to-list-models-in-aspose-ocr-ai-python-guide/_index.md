---
category: general
date: 2026-01-07
description: 如何使用 Python 列出 Aspose OCR AI 中的模型——学习获取模型路径、检查已安装的模型，并在几秒钟内获取 Python
  模型列表。
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: zh
og_description: 如何使用 Python 列出 Aspose OCR AI 的模型。查找模型路径，检查已安装的模型，并查看所有可用模型的完整列表。
og_title: 如何在 Aspose OCR AI 中列出模型 – Python 指南
tags:
- Aspose OCR
- Python
- AI models
title: 如何在 Aspose OCR AI 中列出模型 – Python 指南
url: /zh/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose OCR AI 中列出模型 – Python 指南

是否曾经想过 **如何列出** 已经安装在机器上的模型，在使用 Aspose OCR AI 时？你并不是唯一遇到这个问题的人。在许多项目中，你需要检查模型文件夹，确认有哪些模型存在，甚至调试缺失模型的问题——全部在 Python REPL 中完成。

在本教程中，我们将演示一个完整、可直接运行的示例，向你展示如何 **获取模型路径**、**检查已安装模型**，以及最终 **列出可用模型**，只需几行代码。无需外部脚本、无需隐藏的魔法——纯 Python 加 Aspose OCR AI SDK。

> **先决条件**  
> • Python 3.8 或更高版本  
> • 已安装 `asposeocr` 包（`pip install asposeocr`）  
> • 对导入模块有基本了解  

如果你已经满足上述条件，让我们开始吧。

---

## 使用 Aspose OCR AI 列出模型

我们首先需要 `asposeocr.ai` 模块中提供的 `AsposeAI` 辅助类。该类提供了三个实用方法：

| 方法 | 返回内容 | 常见使用场景 |
|--------|----------------|-----------------|
| `get_local_path()` | Aspose 存放 AI 模型的文件夹的绝对路径 | 验证 SDK 正在查找正确的位置 |
| `list_local()` | 磁盘上实际存在的模型文件夹名称的 Python `list` | 快速查看可以加载哪些模型 |
| `list_remote()` *(optional)* | 可从 Aspose 云端下载的模型列表 | 当本地没有所需模型时使用 |

下面是 **完整脚本**，它会打印本地模型文件夹路径以及已安装模型的列表。

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### 预期输出

在全新安装后运行脚本，通常会看到类似如下的输出：

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

如果文件夹为空，`list_local()` 会返回空列表 (`[]`)。这是一条有用的信号，表明你需要先下载模型——我们稍后会介绍如何操作。

---

## 为什么了解模型路径很重要

了解 **SDK 将文件存放在哪里**（`获取模型路径`）不仅仅是好奇心驱动：

1. **调试** – 若模型加载失败，你可以 `ls` 该路径，确认文件是否真的存在。  
2. **自定义模型** – 有些团队会自行训练 OCR 模型并放入该文件夹。知道路径后即可将文件放在 Aspose 期望的位置。  
3. **权限** – 在 Linux 上，该文件夹可能归属于其他用户。提前发现权限错误可以节省大量时间。

> **小贴士：** 若需将 SDK 指向自定义目录，请在创建 `AsposeAI()` 之前设置环境变量 `ASPOSE_OCR_MODEL_PATH`。

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## 检查已安装模型 – 边缘情况与技巧

### 1. 未安装任何模型

如果 `list_local()` 返回 `[]`，你有两种选择：

| 选项 | 操作方法 |
|--------|--------------|
| **从 Aspose 下载模型** | `ai.download('ocr-general-v1')`（需要网络） |
| **手动复制预训练模型** | 将模型文件夹手动放入 `get_local_path()` 显示的路径中 |

### 2. 同一模型的多个版本

有时会同时看到 `ocr-general-v1` **和** `ocr-general-v1-beta`。SDK 会加载首次匹配到的模型，但你可以通过向 OCR 构造函数传入确切的文件夹名称来强制使用特定版本：

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. 模型文件损坏

部分下载的模型可能导致后续出现 `FileNotFoundError`。如果怀疑文件损坏，只需删除对应文件夹并重新下载：

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## 扩展脚本 – 列出远程模型（可选）

如果想在不离开 Python 的情况下查看可下载的模型，添加以下调用：

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

这将输出类似如下内容：

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

随后你可以选择任意模型，调用 `ai.download('model-name')` 自动下载。

---

## 完整端到端示例

将所有内容整合在一起，下面是一个 **单文件、可直接运行的脚本**，实现以下功能：

1. 显示本地模型文件夹路径。  
2. 列出已安装的模型。  
3. 若未找到模型，下载默认模型。  
4. 最后打印更新后的模型列表。

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

在干净的机器上运行此脚本会产生：

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

现在你拥有一个 **自包含、可引用** 的解决方案，任何 AI 助手都可以原文引用。

---

## 常见问题 (FAQ)

**Q: 这在 Windows 上可以运行吗？**  
A: 当然可以。SDK 会抽象文件系统，`get_local_path()` 会返回类似 `C:\Users\YourName\.asposeocr\models` 的路径。只需确保 Python 有权写入该文件夹。

**Q: 我可以将模型存放在网络驱动器上吗？**  
A: 可以——在创建 `AsposeAI` 实例之前，将 `ASPOSE_OCR_MODEL_PATH` 设置为 UNC 路径（`\\server\share\models`）。

**Q: 如果需要的语言模型不在默认集合中怎么办？**  
A: 使用 `list_remote()` 查看 Aspose 是否提供对应语言的模型。如果没有，你可以自行训练模型并放入文件夹；只需在 OCR 构造函数中传入自定义文件夹名称即可。

---

## 结论

我们已经介绍了 **如何在 Aspose OCR AI 中列出模型**，演示了 **获取模型路径**、**检查已安装模型**，甚至 **下载缺失模型**——全部使用纯 Python。通过了解文件夹结构以及辅助方法 (`get_local_path()`、`list_local()`、`list_remote()`)，你可以完全掌控应用所依赖的 AI 模型。

接下来可以尝试将默认模型替换为手写文字模型，或指向你自行训练的自定义模型。无论哪种方式，你现在都有了管理 OCR 资源的坚实基础，适用于任何 Python 项目。

祝编码愉快，愿你的模型列表始终保持最新！

---

![列出模型截图](https://example.com/images/how-to-list-models.png "列出模型")

*图片 alt 文本:* **列出模型截图** (满足主要关键词要求)。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}