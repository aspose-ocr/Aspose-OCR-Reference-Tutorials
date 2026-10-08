---
category: general
date: 2026-02-22
description: 学习如何提取 OCR 文本并通过 AI 后处理提升 OCR 准确率。使用一步步示例，在 Python 中轻松清理 OCR 文本。
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: zh
og_description: 了解如何使用简单的 Python 工作流和 AI 后处理来提取 OCR 文本、提升 OCR 准确率并清理 OCR 文本。
og_title: 如何提取 OCR 文本 – 步骤指南
tags:
- OCR
- AI
- Python
title: 如何提取 OCR 文本——完整指南
url: /zh/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何提取 OCR 文本 – 完整编程教程

是否曾好奇 **如何从扫描文档中提取 OCR**，却不想得到一堆错别字和断行？你并不孤单。在许多实际项目中，OCR 引擎的原始输出往往是一段乱七八糟的文字，清理起来像是做家务。

好消息是？只要按照本指南操作，你就能看到一种实用的方法来获取结构化的 OCR 数据，运行 AI 后处理，并得到 **干净的 OCR 文本**，可直接用于后续分析。我们还会涉及 **提升 OCR 准确率** 的技巧，让结果一次就可靠。

接下来几分钟，我们将覆盖所有必备内容：所需库、完整可运行的脚本，以及避免常见坑的提示。没有模糊的 “参考文档” 走捷径——只有完整、可复制粘贴直接运行的自包含解决方案。

## 你需要准备的东西

- Python 3.9+（代码使用类型提示，但在旧的 3.x 版本也能运行）
- 能返回结构化结果的 OCR 引擎（例如使用 `pytesseract` 并加上 `--psm 1` 参数的 Tesseract，或提供块/行元数据的商业 API）
- 一个 AI 后处理模型——本示例中我们用一个简单函数来模拟，你可以替换为 OpenAI 的 `gpt‑4o-mini`、Claude，或任何接受文本并返回清理后输出的 LLM
- 几张用于测试的示例图片（PNG/JPG）

如果这些都准备好了，下面开始吧。

## 如何提取 OCR – 初始获取

第一步是调用 OCR 引擎，并让它返回 **结构化表示** 而不是纯字符串。结构化结果会保留块、行和词的边界，这让后续清理工作轻松很多。

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **为什么这很重要：** 通过保留块和行，我们避免了必须猜测段落起始位置。`recognize_structured` 函数为我们提供了一个干净的层次结构，后续可以直接喂给 AI 模型。

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

运行该代码片段会打印出 OCR 引擎看到的第一行，通常会出现像 “0cr” 这种误识别，而不是正确的 “OCR”。

## 使用 AI 后处理提升 OCR 准确率

现在我们已经拿到原始结构化输出，接下来把它交给 AI 后处理器。目标是通过纠正常见错误、规范标点，甚至在需要时重新分段，来 **提升 OCR 准确率**。

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **小技巧：** 如果没有 LLM 订阅，可以用本地 transformer（例如 `sentence‑transformers` 加上微调的纠错模型）或甚至基于规则的方法来替代调用。关键在于 AI 能逐行查看，这通常足以 **清理 OCR 文本**。

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

此时你应该能看到更干净的句子——错别字已被替换，额外空格去除，标点也已修正。

## 为更好结果清理 OCR 文本

即使经过 AI 校正，你可能仍想再做一次最终的清理：去除非 ASCII 字符、统一换行符、合并多个空格。这个额外的步骤确保输出可以直接用于 NLP、数据库导入等下游任务。

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

`final_cleanup` 函数会返回一个纯字符串，你可以直接喂给搜索索引、语言模型或导出为 CSV。由于我们保留了块边界，段落结构得以保持。

## 边缘情况与应对方案

- **多列布局：** 如果源文件是多列的，OCR 引擎可能会交叉输出行。可以从 TSV 输出中检测列坐标，并在发送给 AI 前重新排序行。
- **非拉丁文字：** 对于中文、阿拉伯语等语言，需将 LLM 的提示改为请求特定语言的纠错，或使用针对该脚本微调的模型。
- **大文档：** 单行逐个发送会很慢。可以批量发送（例如每次 10 行），让 LLM 返回一组已清理的行。记得遵守 token 限制。
- **缺失块信息：** 有些 OCR 引擎只返回平铺的词列表。此时可以通过相同的 `line_num` 将词归组为行，从而重建结构。

## 完整可运行示例

把所有步骤整合在一起，下面是一个可以端到端运行的单文件示例。请将占位符替换为你自己的 API 密钥和图片路径。

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}