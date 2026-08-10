---
category: general
date: 2026-06-25
description: 使用 aocr 库快速获取 OCR 支持的字符。了解如何列出 OCR 字符、设置语言以及在 Python 中调试 OCR 引擎。
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: zh
og_description: 使用 aocr 获取 OCR 支持的字符。本指南展示如何列出 OCR 字符、选择语言以及在 Python 中处理边缘情况。
og_title: 在 Python 中获取 OCR 支持的字符 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: 在 Python 中获取 OCR 支持的字符 – 完整指南
url: /zh/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取 Python 中 OCR 支持的字符 – 完整指南

有没有想过在玩转 OCR 引擎时，**获取特定语言的 OCR 支持字符**？你并不孤单。无论是构建收据扫描器还是多语言文档解析器，准确了解引擎能够识别哪些字形都是救命稻草。在本教程中，我们将完整演示整个过程——安装库、配置语言，最后列出这些字符——让你在几分钟内调试并微调 OCR 流程。

我们将使用 **aocr** 库，这是一款轻量级的 Python OCR 引擎，能够轻松查询语言能力。阅读完本指南后，你将能够 **列出 OCR 字符**、在 **支持的 OCR 语言** 之间切换，甚至在生产环境出现问题前发现覆盖盲区。

---

## 前置条件

在开始之前，请确保你拥有：

* Python 3.8 或更高（aocr 包已不再支持 3.7）
* 能联网的终端或命令提示符
* 基本的 Python 脚本使用经验（只要会写 `print()` 就可以）

没有繁重的外部依赖——只需 `aocr` pip 包。

---

## 安装 aocr 库（OCR Engine Python）

首先需要一个可用的 **OCR engine Python** 环境。aocr 包已发布在 PyPI，只需一条 pip 命令即可完成：

```bash
pip install aocr
```

如果你使用虚拟环境（强烈推荐），请先激活它：

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **小技巧：** 固定版本号（`pip install aocr==1.2.4`）可以避免后续意外的 API 变更。

---

## 选择语言（Supported OCR Languages）

aocr 附带少量内置语言包。每个语言包定义了引擎可以识别的 Unicode 码点集合。要查询这些包，需要在引擎实例上设置 `language` 属性。

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

你可以将 `aocr.Language.ENGLISH` 替换为其他枚举值（`FRENCH`、`GERMAN` 等）。如果尝试赋予未打包的语言，aocr 会抛出 `ValueError`。因此，先检查 **supported OCR languages** 列表是个好习惯：

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## 获取字符集合（Get OCR Supported Characters）

下面进入教程核心：实际 **获取 OCR 支持的字符**。引擎提供了一个便利方法 `get_supported_characters()`，返回单字符字符串的列表。

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

在内部，aocr 会读取随语言包一起提供的 JSON 文件，并将每个 Unicode 码点转换为 Python 字符串。结果是确定性的，也就是说在相同语言版本下每次运行脚本都会得到相同的列表。

---

## 显示支持的字符数量

了解数量可以快速评估覆盖范围。对于英语，通常会看到几千个字符（包括标点和数字）。

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()` 调用是 O(1) 的，因为 Python 在内部保存了列表长度，即使是大字母表也不会带来性能惩罚。

---

## 预览前 100 个支持字符

快速的可视化检查可以帮助你确认引擎是否包含所需符号（比如欧元符号或智能引号）。我们打印前一百个字符：

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join` 操作会把切片合并成单个字符串，比直接打印 Python 列表更易阅读。

---

## 完整脚本 – 所有步骤汇总

下面是完整、可运行的示例，涵盖所有步骤。将其保存为 `list_supported_chars.py`，然后在终端执行 `python list_supported_chars.py`。

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**预期输出（为简洁起见已截断）：**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

具体字符数量可能会因 aocr 版本略有差异，但你始终会看到一个包含常用标点的长字母表。

---

## 处理边缘情况

### 语言包缺失怎么办？

如果请求的语言未打包，`aocr.Language` 中将不存在对应枚举，会触发 `AttributeError`。可以通过简单检查来防御：

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### 空字符列表

某些小众语言在底层训练数据不完整时可能返回空列表。此时可以回退到默认语言（例如 English）或抛出警告：

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode 正规化

列表中可能包含组合字符（例如 “é” 以 `e` + 急音符的形式出现）。如果下游处理期望预组合字形，请执行正规化步骤：

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## 实战项目的专业技巧

* **缓存字符列表** – 若要处理成千上万张图片，在每次迭代中调用 `get_supported_characters()` 会产生不必要的开销。将列表存放在模块级变量或序列化为 JSON 供后续复用。
* **跨语言校验** – 当一个应用支持多语言时，取字符集合的交集以找到公共子集。这有助于设计在不同语言环境下保持一致的 UI 元素。
* **调试 OCR 失败** – 若引擎误分类某个字形，可将该字符与 `list_supported_chars` 的输出对比。若缺失，即发现覆盖盲区，可能需要自定义训练步骤。
* **结合自定义字体** – aocr 尊重 Unicode 范围，但渲染质量受字体影响。请使用生产环境中实际使用的字体测试支持字符，以免出现意外。

---

## 常见问题

**Q: 这在 aocr 2.x 版本上可用吗？**  
A: 可以，`get_supported_characters()` 方法在 1.x 与 2.x 中保持稳定。唯一变化是语言枚举已迁移至 `aocr.languages`。

**Q: 我能获取每个字符的 Unicode 码点吗？**  
A: 完全可以。使用列表推导式配合 `ord(ch)`：

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: 那阿拉伯语等从右到左的脚本怎么办？**  
A: aocr 包含 `ARABIC` 枚举。字符列表会包含阿拉伯字形，但在下游 UI 中可能需要启用 RTL 渲染。

---

## 结论

现在，你已经掌握了使用 aocr 库在 Python 中 **获取 OCR 支持字符** 的方法，了解了如何在 **supported OCR languages** 之间切换，并认识到 **列出 OCR 字符** 对构建稳健的文本识别流水线有多重要。借助完整脚本和上述技巧，你可以快速验证语言覆盖范围、调试缺失字形，并构建更智能的 OCR 驱动应用。

准备好下一步了吗？尝试将此字符列表与自定义词表过滤器结合，或使用其他 OCR 引擎（Tesseract、EasyOCR）进行对比实验。探索得越多，你的 OCR 解决方案就会越强大。

祝编码愉快，愿你的字符集永远完整！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步深入。每篇资源都提供完整可运行的代码示例以及逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}