---
category: general
date: 2026-04-26
description: 使用 AsposeAI OCR 后处理快速掩码信用卡号码。通过一步步教程了解 PCI 合规、正则表达式掩码和数据清理。
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: zh
og_description: 使用 AsposeAI 在 OCR 结果中掩码信用卡号码。本教程涵盖 PCI 合规、正则表达式掩码和数据清理。
og_title: 掩码信用卡号码 – 完整的 Python OCR 后处理指南
tags:
- OCR
- Python
- security
title: 在 OCR 输出中掩码信用卡号码 – 完整 Python 指南
url: /zh/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 掩码信用卡号码 – 完整 Python 指南

是否曾需要在直接来自 OCR 引擎的文本中 **掩码信用卡号码**？你并不是唯一遇到这种情况的人。在受监管的行业中，暴露完整的 PAN（Primary Account Number）会让你在 PCI 合规审计中陷入麻烦。好消息是？只需几行 Python 代码和 AsposeAI 的后处理钩子，你就可以自动隐藏中间的八位数字，确保安全。

在本教程中，我们将演示一个真实场景：对收据图片进行 OCR，然后应用自定义 **OCR 后处理** 函数对任何 PCI 数据进行清理。完成后，你将拥有一个可复用的代码片段，能够直接嵌入任何 AsposeAI 工作流，并提供一系列处理边缘情况和扩展方案的实用技巧。

## 你将学习

- 如何使用 **AsposeAI** 注册自定义后处理器。
- 为什么 **正则表达式掩码** 方法既快速又可靠。
- 与数据清理相关的 **PCI 合规** 基础知识。
- 如何扩展模式以支持多种卡片格式或国际卡号。
- 预期输出以及如何验证掩码是否生效。

> **先决条件** – 你需要一个可用的 Python 3 环境，已安装 Aspose.AI for OCR 包（`pip install aspose-ocr`），以及一张包含信用卡号码的示例图片（例如 `receipt.png`）。不需要其他外部服务。

---

## 步骤 1：定义一个掩码信用卡号码的后处理器

解决方案的核心是一个小函数，它接收 OCR 结果，执行 **正则表达式掩码** 逻辑，并返回清理后的文本。

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**为什么这样有效：**  
- 正则 `(\d{4})\d{8}(\d{4})` 精确匹配 16 位连续数字，这是 Visa、MasterCard 等常见卡片的格式。  
- 通过捕获前四位和后四位（`\1` 和 `\2`），我们在保留足够调试信息的同时，遵守 **PCI 合规** 中禁止存储完整 PAN 的规定。  
- 替换模式 `\1****\2` 隐藏敏感的中间八位数字，将 `1234567812345678` 变为 `1234****5678`。

> **专业提示：** 如果需要支持 15 位的美国运通卡号，可添加第二个模式，例如 `r'(\d{4})\d{6}(\d{5})'`，并顺序执行两次替换。

---

## 步骤 2：初始化 AsposeAI 引擎

在我们能够挂载后处理器之前，需要先创建 OCR 引擎实例。AsposeAI 捆绑了 OCR 模型并提供了简易的自定义处理 API。

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**为何在此初始化？**  
一次性创建 `AsposeAI` 对象并在多张图片间复用，可降低开销。引擎还会缓存语言模型，加速后续调用——在批量扫描收据时尤为便利。

---

## 步骤 3：注册自定义掩码函数

AsposeAI 提供 `set_post_processor` 方法，允许你接入任意可调用对象。我们将 `mask_pci` 函数连同可选的设置字典（此处为空）一起传入。

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**内部发生了什么？**  
当稍后调用 `run_postprocessor` 时，AsposeAI 会把原始 OCR 结果交给 `mask_pci`。该函数接收一个轻量对象（`data`），其中包含识别出的文本，返回一个新的字符串。此设计保持核心 OCR 不受影响，同时让你在单一位置强制执行 **数据清理** 策略。

---

## 步骤 4：对收据图片运行 OCR

现在引擎已经知道如何清理输出，我们把图片喂进去。为简化教程，假设你已经拥有配置好语言和分辨率的 `engine` 对象。

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**提示：** 如果还没有预配置对象，可以使用以下方式创建：

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` 调用返回一个对象，其 `text` 属性保存原始、未掩码的字符串。

---

## 步骤 5：应用已注册的后处理器

拿到原始 OCR 数据后，我们将其交给 AI 实例。引擎会自动运行我们之前注册的 `mask_pci` 函数。

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**为何使用 `run_postprocessor` 而不是手动调用函数？**  
这样可以保持工作流的一致性，尤其当你拥有多个后处理器（例如拼写检查、语言检测）时。AsposeAI 会按照注册顺序排队执行，确保输出可预测。

---

## 步骤 6：验证清理后的输出

最后，打印清理后的文本并确认所有信用卡号码已被正确掩码。

```python
print(final_result.text)
```

**预期输出**（摘录）：

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

如果收据中没有卡号，文本保持不变——无需掩码，也无需担心。

---

## 处理边缘情况和常见变体

### 文档中出现多个卡号
如果收据包含多个 PAN（例如会员卡加付款卡），正则会全局匹配，自动掩码所有匹配项，无需额外代码。

### 非标准格式
OCR 有时会插入空格或短横线（`1234 5678 1234 5678` 或 `1234-5678-1234-5678`）。可扩展模式以忽略这些字符：

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

新增的 `[ -]?` 允许在数字块之间出现可选的空格或连字符。

### 国际卡号
对于某些地区使用的 19 位 PAN，可将模式放宽为：

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

只需记住，**PCI 合规** 仍要求对中间位进行掩码，无论长度如何。

### 记录掩码值（可选）
如果需要审计日志，可通过 `custom_settings` 传入标志并调整函数：

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

随后使用以下方式注册：

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## 完整可运行示例（复制粘贴即用）

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

在包含 `4111111111111111` 的收据上运行此脚本，将得到：

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

这就是完整的流水线——从原始 OCR 到 **数据清理**，全部用几行简洁的 Python 实现。

---

## 结论

我们已经演示了如何使用 AsposeAI 的后处理钩子、简洁的正则表达式以及一系列 **PCI 合规** 的最佳实践，在 OCR 结果中 **掩码信用卡号码**。该方案完全自包含，适用于任何 OCR 引擎可读取的图像，并可扩展以覆盖更复杂的卡片格式或日志需求。

准备好下一步了吗？尝试将此掩码与 **数据库插入** 逻辑结合，仅存储后四位作参考，或集成 **批处理器**，在夜间扫描整个收据文件夹。你也可以探索其他 **OCR 后处理** 任务，如地址标准化或语言检测——它们都遵循我们这里使用的相同模式。

对边缘情况、性能或如何将代码迁移到其他 OCR 库有疑问？在下方留言，让我们继续讨论。祝编码愉快，保持安全！

![掩码信用卡号码在 OCR 流程中的工作示意图](https://example.com/images/ocr-mask-flow.png "OCR 后处理掩码流程图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}