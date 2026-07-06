---
category: general
date: 2026-06-22
description: 学习如何使用 Python 中的 AI SDK 列出缓存的 AI 模型。包括获取模型缓存目录的步骤以及高效管理本地 AI 模型的方法。
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: zh
og_description: 使用 AI SDK 用 Python 列出已缓存的 AI 模型。按照本分步教程获取模型缓存目录并处理本地 AI 模型。
og_title: Python 中列出缓存的 AI 模型 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Python 中列出缓存的 AI 模型——完整指南
url: /zh/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中列出缓存的 AI 模型 – 完整指南

是否曾想过如何在工作站上 **列出缓存的 AI 模型**，而不必在晦涩的文件夹中翻找？你并不孤单。许多开发者在需要确认本地已经存储了哪些模型时会卡住，尤其是在带宽受限或离线部署的情况下。在本教程中，你将看到一种快速、无废话的方式来查询 AI SDK、打印缓存内容，并准确定位这些文件所在的位置。

我们还会涉及 **检索模型缓存目录**、处理空缓存以及在生产脚本中 **管理 AI 模型缓存** 的最佳实践。阅读完本教程后，你将拥有一个可直接嵌入任何 Python 项目的完整代码片段。

## 前置条件

在开始之前，请确保你已具备：

- 已安装 Python 3.8 或更高版本。
- 已通过 `pip install ai-sdk` 或组织内部仓库安装 AI SDK（`ai` 包）。
- 对在命令行运行脚本有基本了解。

无需额外的库，示例保持轻量且可移植。

---

## 列出缓存的 AI 模型 – 快速概览

首先需要导入 SDK 并调用其辅助函数。SDK 提供了两个便利的方法：

1. `ai.list_local()` – 返回已缓存模型标识符的 Python 列表。
2. `ai.get_local_path()` – 返回这些模型文件所在的绝对目录。

两个调用都是同步的，如果出错会抛出明确的 `AIError`，从而简化错误处理。

> **为何使用这些函数？**  
> 知晓确切的缓存模型集合可以避免不必要的下载、调试版本不匹配，并自动清理旧的制品。这是 **AI SDK Python** 工作流中的一个小环节，却能为你节省数小时的手动文件系统查找时间。

### 第 1 步：导入 AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*原因说明：* 导入包会注册底层 C 扩展并从环境中加载配置文件（如缓存路径）。如果跳过此步骤，一旦调用任何 SDK 函数就会抛出 `ModuleNotFoundError`。

### 第 2 步：列出所有缓存的模型

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**你将看到的结果：** 如果本地存有三个模型，输出可能如下：

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

如果缓存为空，则会得到一个空列表：

```
Cached models: []
```

> **小技巧：** 如果怀疑 SDK 未正确初始化，可将调用包装在 try/except 块中。

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### 第 3 步：检索模型缓存目录

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

在类 Unix 系统上的典型输出：

```
Model cache directory: /home/you/.cache/ai/models
```

在 Windows 上可能会看到类似 `C:\Users\you\AppData\Local\ai\models` 的路径。了解此路径在手动 **管理 AI 模型缓存** 时至关重要——例如清除旧版本或将文件复制到共享盘。

---

## 可视化概览

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Alt text:* 使用 AI SDK 在 Python 中 **列出缓存的 AI 模型** 的流程示意图。

---

## 处理边缘情况和常见陷阱

### 空缓存

如果 `ai.list_local()` 返回空列表，可能会怀疑 SDK 配置有误。请再次检查环境变量 `AI_CACHE_DIR`（或 SDK 的配置文件），确保其指向可写入的位置。

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### 权限问题

在访问 `ai.get_local_path()` 时，受限系统可能会抛出 `PermissionError`。通常的解决办法是以合适的用户权限运行脚本，或调整目录的 ACL 权限。

### 版本不匹配

有时缓存中存在旧版本模型，而代码请求的是新版本。SDK 会自动下载新版本，但你也可以通过检查列表中的版本标签提前发现此类情况：

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### 清理旧模型

如果需要释放空间，可以直接删除特定模型文件夹：

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

运行 `purge_model('bert-base-uncased')` 将移除该模型并释放磁盘空间。

---

## 可直接复制‑粘贴的完整脚本

下面是一段可直接运行的脚本，整合了所有步骤、基础错误处理，并输出友好的摘要。

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**预期输出（当缓存已填充时）：**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

使用 `python list_models.py` 运行脚本，即可瞬间了解磁盘上有哪些模型。

---

## 常见问答

**问：此方法适用于所有操作系统吗？**  
答：是的。SDK 会抽象掉 OS 特定路径，`ai.get_local_path()` 在 Linux、macOS 和 Windows 上均返回有效字符串。

**问：能否列出远程缓存中的模型？**  
答：内置的 `list_local()` 仅报告本地存储的制品。若需查询远程注册表，可使用 `ai.list_remote()`（前提是你的 SDK 版本提供该功能）。

**问：如果 SDK 包名不是 `ai`，该怎么办？**  
答：将导入行替换为实际的包名，例如 `import myai as ai`。后续调用保持不变，因为 API 合约在不同实现间是一致的。

---

## 结论

现在，你已经掌握了使用 **AI SDK Python** 库 **列出缓存的 AI 模型**、获取 **模型缓存目录**，以及清理旧文件的生产级方法。这些知识帮助你保持环境整洁，避免重复下载，并轻松调试版本问题。

准备好下一步了吗？尝试扩展脚本以自动下载缺失的模型，或将其集成到 CI 流水线中，在每次构建前验证缓存健康。探索 **管理 AI 模型缓存** 的策略，将让你的 AI 应用更快、更可靠。

祝编码愉快，愿你的缓存保持精简！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在本教程展示的技巧之上进一步提升。每个资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}