---
category: general
date: 2026-02-22
description: 了解如何列出缓存的模型并快速显示您机器上的缓存目录。包括查看缓存文件夹和管理本地 AI 模型存储的步骤。
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: zh
og_description: 了解如何列出缓存模型、显示缓存目录以及查看缓存文件夹，只需几个简单步骤。附带完整的 Python 示例。
og_title: 列出已缓存模型 – 查看缓存目录的快速指南
tags:
- AI
- caching
- Python
- development
title: 列出已缓存的模型 – 如何查看缓存文件夹并显示缓存目录
url: /zh/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 列出缓存模型 – 快速查看缓存目录指南

是否曾想过在工作站上 **列出缓存模型** 而不必在晦涩的文件夹中翻找？你并不是唯一的遇到这种情况的人。许多开发者在需要确认哪些 AI 模型已经本地存储时会卡住，尤其是磁盘空间紧张时。好消息是？只需几行代码，你就可以 **列出缓存模型** 并 **显示缓存目录**，完整可视化你的缓存文件夹。

在本教程中，我们将逐步演示一个自包含的 Python 脚本，正好实现上述功能。完成后，你将会知道如何查看缓存文件夹，了解不同操作系统下缓存的存放位置，甚至看到一个整齐打印的已下载模型列表。无需外部文档，无需猜测——只要清晰的代码和解释，立即复制粘贴使用。

## 你将学到

- 如何初始化一个提供缓存工具的 AI 客户端（或存根）。  
- **列出缓存模型** 与 **显示缓存目录** 的确切命令。  
- 缓存在 Windows、macOS 和 Linux 上的存放位置，方便手动导航。  
- 处理空缓存或自定义缓存路径等边缘情况的技巧。  

**前置条件** – 需要 Python 3.8+，以及一个可通过 pip 安装的实现了 `list_local()`、`get_local_path()`，可选的 `clear_local()` 的 AI 客户端。如果还没有，可使用示例中的模拟 `YourAIClient` 类，随后替换为真实 SDK（如 `openai`、`huggingface_hub` 等）。

准备好了吗？让我们开始吧。

## 第一步：设置 AI 客户端（或模拟对象）

如果你已经有客户端对象，可跳过此块。否则，创建一个小型的替代对象来模拟缓存接口。这样即使没有真实 SDK，脚本也能运行。

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **专业提示：** 如果已有真实客户端（例如 `from huggingface_hub import HfApi`），只需将 `YourAIClient()` 调用替换为 `HfApi()`，并确保 `list_local` 与 `get_local_path` 方法存在或已相应包装。

## 第二步：**列出缓存模型** – 检索并显示

客户端准备好后，我们可以让它枚举本地已知的所有模型。这就是 **列出缓存模型** 操作的核心。

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**预期输出**（使用步骤 1 中的示例数据）：

```
Cached models:
 - model_1
 - model_2
 - model_3
```

如果缓存为空，你将只看到：

```
Cached models:
```

这行空白提示表示尚未存储任何内容——在编写清理脚本时非常实用。

## 第三步：**显示缓存目录** – 缓存到底在哪里？

知道路径往往是解决问题的一半。不同操作系统的默认缓存位置各不相同，有些 SDK 还能通过环境变量覆盖。下面的代码片段会打印绝对路径，方便你 `cd` 进去或在文件资源管理器中打开。

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**在类 Unix 系统上的典型输出：**

```
Cache directory: /home/youruser/.ai_cache
```

在 Windows 上可能看到类似：

```
Cache directory: C:\Users\YourUser\.ai_cache
```

现在，你已经掌握了在任何平台 **查看缓存文件夹** 的方法。

## 第四步：整合为单个可运行脚本

以下是完整、可直接运行的程序，融合了上述三步。将其保存为 `view_ai_cache.py`，然后执行 `python view_ai_cache.py`。

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

运行后，你将立即看到缓存模型列表 **以及** 缓存目录的位置。

## 边缘情况与变体

| 情况 | 处理办法 |
|-----------|------------|
| **缓存为空** | 脚本会打印 “Cached models:” 但没有条目。可添加条件警告：`if not models: print("⚠️ No models cached yet.")` |
| **自定义缓存路径** | 在创建客户端时传入路径：`YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`。`get_local_path()` 调用将反映该自定义位置。 |
| **权限错误** | 在受限机器上，客户端可能抛出 `PermissionError`。将初始化包装在 `try/except` 中，并回退到用户可写目录。 |
| **使用真实 SDK** | 将 `YourAIClient` 替换为实际的客户端类，并确保方法名称匹配。许多 SDK 直接暴露 `cache_dir` 属性，可直接读取。 |

## 管理缓存的专业技巧

- **定期清理：** 如果经常下载大型模型，可安排 cron 任务，在确认不再需要后调用 `shutil.rmtree(ai.get_local_path())`。  
- **磁盘使用监控：** 在 Linux/macOS 上使用 `du -sh $(ai.get_local_path())`，或在 PowerShell 中使用 `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum`，随时掌握大小。  
- **版本化文件夹：** 某些客户端会为每个模型版本创建子文件夹。当你 **列出缓存模型** 时，会看到每个版本作为单独条目——利用此特性清理旧版本。  

## 可视化概览

![列出缓存模型截图](https://example.com/images/list-cached-models.png "列出缓存模型 – 控制台输出显示模型名称和缓存路径")

*Alt text:* *列出缓存模型 – 控制台输出显示已缓存模型名称以及缓存目录路径。*

## 结论

我们已经覆盖了 **列出缓存模型**、**显示缓存目录**，以及一般 **查看缓存文件夹** 的全部要点。简短的脚本展示了完整、可运行的解决方案，解释了每一步的意义，并提供了实际使用的技巧。

接下来，你可以探索 **如何以编程方式清除缓存**，或将这些调用集成到更大的部署流水线中，以在启动推理任务前验证模型可用性。无论哪种方式，你现在都具备了自信管理本地 AI 模型存储的基础。

对特定 AI SDK 有疑问吗？在下方留言吧，祝你缓存愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}