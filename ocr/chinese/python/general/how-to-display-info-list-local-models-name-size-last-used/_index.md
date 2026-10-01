---
category: general
date: 2026-01-12
description: 学习如何通过列出本地模型、显示模型名称、大小和最近使用时间戳，在清晰的 Python 示例中展示 AsposeAI 的信息。
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: zh
og_description: 如何显示 AsposeAI 的信息：列出本地模型，显示模型名称、大小和最近使用时间戳，并提供完整的 Python 演练。
og_title: 如何显示信息 – 列出本地模型、名称、大小、最近使用时间
tags:
- AsposeAI
- Python
- Model Management
title: 如何显示信息——列出本地模型、名称、大小、最近使用
url: /zh/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何显示信息 – 列出本地模型、名称、大小、最近使用时间

是否曾想过 **如何显示** 来自 AsposeAI 安装的信息，而不必翻阅日志或 UI？你并非唯一的疑问。在许多数据科学流水线中，第一件事就是快速查看机器上有哪些模型，它们的名称、大小以及最近一次使用的时间。

这正是我们要讲的内容：一个简洁、端到端的 Python 代码片段，**列出本地模型**，随后 **显示模型名称**、**展示模型大小**，以及 **显示最近使用时间**。不依赖外部库，没有隐藏的魔法——只使用你已经拥有的 AsposeAI 客户端。

完成本教程后，你可以将代码直接嵌入任意脚本，运行后即可立即得到本地缓存模型的整齐表格。它非常适合环境的健康检查、构建监控仪表盘，或仅仅满足对磁盘上隐藏内容的好奇心。

## 前置条件

- Python 3.8 或更高（示例使用 f‑strings，需 3.6 以上）
- 已安装 `asposeai` 包（`pip install asposeai`）
- 有效的 AsposeAI 许可证或试用密钥（客户端会从环境变量或配置文件中读取凭证）

如果这些都已准备就绪，太好了——让我们开始吧。

## 步骤 1：如何显示信息 – 初始化 AsposeAI 客户端

在 **列出本地模型** 之前，我们需要一个能够与 AsposeAI 运行时通信的客户端对象。这一步是基础；没有它，其余代码会抛出 `NameError`。

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*为什么这很重要*：初始化客户端会与本地推理引擎建立会话，加载必要的本地库。它还会验证你的许可证是否有效，避免在后续查询模型时出现晦涩错误。

> **专业提示**：如果在 CI 服务器上运行，请在环境变量中设置 `ASPOSEAI_LICENSE`，这样客户端即可在没有交互提示的情况下启动。

## 步骤 2：列出本地模型 – 获取可用模型

客户端准备就绪后，我们可以 **列出本地模型**。`list_local()` 方法返回一个对象集合，每个对象都暴露 `name`、`size_mb` 和 `last_used` 等属性。

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*内部工作原理*：`list_local()` 会扫描 AsposeAI 缓存模型文件的目录（默认 `~/.asposeai/models`），并构建轻量级的元数据对象。因为它只读取一个小的 JSON 清单，而不加载模型权重，所以速度很快。

如果你想确认某个模型是否已经缓存，这个调用是最快的方式。

## 步骤 3：显示模型名称、展示模型大小以及显示最近使用时间

拿到模型列表后，我们最终通过遍历集合并打印每个属性来 **显示信息**。这一步同时 **显示模型名称**、**展示模型大小**，以及 **显示最近使用时间**，全部在一行中整齐呈现。

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**预期输出**（时间戳会因环境而异）：

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*为何采用这种格式*：短横线（`–`）用于分隔字段，提高可读性，标题行让控制台输出更易扫描。如果后续需要机器可读的格式（CSV、JSON），只需将 `print` 替换为 `writer.writerow` 或 `json.dump` 即可。

### 处理边缘情况

- **没有缓存模型** – `list_local()` 返回空列表。循环将直接跳过，只留下标题行。你可以添加一个保护：

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **属性缺失** – 在极少数情况下清单可能损坏。访问 `model_info.last_used` 可能会抛出 `AttributeError`。如果预期会出现此类问题，请在 `print` 周围使用 `try/except`。

- **模型目录过大** – 若模型数量达数百个，考虑对输出进行分页，或改为写入文件而非直接打印到控制台。

## 可视化摘要（可选）

如果你更喜欢直观的视觉提示，下面的示意图展示了从客户端初始化到最终显示的完整流程。

![Diagram showing how to display info from AsposeAI client](/images/how-to-display-info.png "how to display info diagram")

*替代文字*：**如何显示信息** – AsposeAI 客户端初始化、模型列出以及信息显示的示意图。

## 完整可运行脚本

将所有内容组合在一起，下面是完整的、可直接运行的脚本：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

将其保存为 `list_models.py`，赋予可执行权限（`chmod +x list_models.py`），然后运行：

```bash
./list_models.py
```

你将看到前面演示的整齐列表。

## 结论

我们已经完整演示了 **如何显示信息**：通过 **列出本地模型**，随后 **显示模型名称**、**展示模型大小**，以及 **显示最近使用时间**。该方法轻量、仅依赖标准的 `asposeai` 包，可随时嵌入任何自动化流水线或调试会话。

接下来你可以：

- 将输出导出为 CSV 以便在电子表格中分析（使用 `csv` 模块）。
- 将时间戳送入监控仪表盘，以便对长期未使用的模型触发警报。
- 将此脚本与 `aspose_ai.download()` 结合，自动刷新长时间未使用的模型。

请记住，对模型清单的清晰可见性可以节省时间，减少存储冗余，并保持 AI 服务平稳运行。试着运行脚本，按需调整格式，让它成为你工具箱中的常备利器。

祝编码愉快，愿你的模型始终保持新鲜！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}