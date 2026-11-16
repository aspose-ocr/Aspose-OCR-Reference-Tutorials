---
category: general
date: 2026-02-22
description: 學習如何提取 OCR 文字，並透過 AI 後處理提升 OCR 準確度。使用 Python 以逐步範例輕鬆清理 OCR 文字。
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: zh-hant
og_description: 了解如何使用簡單的 Python 工作流程結合 AI 後處理，提取 OCR 文字、提升 OCR 準確度並清理 OCR 文字。
og_title: 如何提取 OCR 文字 – 步驟指南
tags:
- OCR
- AI
- Python
title: 如何提取 OCR 文字 – 完整指南
url: /zh-hant/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何提取 OCR 文字 – 完整程式教學

有沒有想過 **如何提取 OCR** 從掃描文件中，而不會得到一堆錯字和斷行的混亂？你並不孤單。在許多實務專案中，OCR 引擎的原始輸出常常像是一段雜亂的文字，清理起來像是件苦差事。  

好消息是？跟隨本指南，你將看到一種實用的方法來取得結構化的 OCR 資料、執行 AI 後處理，最終得到 **clean OCR text**，可直接用於後續分析。我們也會提及 **improve OCR accuracy** 的技巧，讓結果一次就可靠。  

接下來的幾分鐘，我們會涵蓋你所需的一切：必備函式庫、完整可執行的腳本，以及避免常見陷阱的技巧。沒有模糊的「請參閱文件」捷徑——只有完整、獨立的解決方案，你可以直接複製貼上並執行。

## 需要的條件

- Python 3.9+（程式碼使用型別提示，但在較舊的 3.x 版本亦可運作）
- 能夠回傳結構化結果的 OCR 引擎（例如使用 `pytesseract` 並加上 `--psm 1` 旗標的 Tesseract，或提供區塊/行中繼資料的商業 API）
- AI 後處理模型——本範例中我們以簡單函式模擬，但你可以改用 OpenAI 的 `gpt‑4o-mini`、Claude，或任何接受文字並回傳清理後輸出的 LLM
- 幾張樣本影像（PNG/JPG）以供測試

如果你已備妥，讓我們開始吧。

## 如何提取 OCR – 初始擷取

第一步是呼叫 OCR 引擎，要求它回傳 **structured representation**（結構化表示）而非純文字字串。結構化結果保留區塊、行與單字的邊界，使之後的清理工作變得更簡單。

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

> **為什麼這很重要：** 透過保留區塊與行，我們不必猜測段落的起始位置。`recognize_structured` 函式提供了乾淨的層級結構，之後可以餵入 AI 模型。

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

執行此程式碼片段會精確印出 OCR 引擎看到的第一行文字，通常會包含像是把 “OCR” 誤辨為 “0cr” 之類的錯誤。

## 使用 AI 後處理提升 OCR 準確度

現在我們已取得原始的結構化輸出，接下來交給 AI 後處理器。目標是透過修正常見錯誤、正規化標點符號，甚至在需要時重新分段，以 **improve OCR accuracy**（提升 OCR 準確度）。

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

> **專業提示：** 若沒有 LLM 訂閱，你可以改用本地 transformer（例如 `sentence‑transformers` 加上微調的校正模型）或甚至規則式方法。關鍵概念是 AI 會單獨處理每一行，通常已足以 **clean OCR text**（清理 OCR 文字）。

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

現在你應該會看到更乾淨的句子——錯字已被更正、額外空格移除，標點也已修正。

## 為更佳結果清理 OCR 文字

即使在 AI 校正之後，你仍可能想再執行一次最終的清理步驟：去除非 ASCII 字元、統一換行符號，並合併多個空格。這一步可確保輸出已可直接用於後續任務，如 NLP 或資料庫匯入。

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

`final_cleanup` 函式會回傳純文字字串，你可以直接餵入搜尋索引、語言模型或匯出為 CSV。由於我們保留了區塊邊界，段落結構得以維持。

## 邊緣情況與假設情境

- **多欄位版面：** 若來源文件有多欄，OCR 引擎可能會交錯行。你可以從 TSV 輸出偵測欄位座標，並在送給 AI 前重新排序行。
- **非拉丁文字腳本：** 針對中文、阿拉伯文等語言，請改變 LLM 的提示以要求特定語言的校正，或使用已在該腳本上微調的模型。
- **大型文件：** 單行逐一送出可能較慢。可將行批次處理（例如每次 10 行）讓 LLM 回傳清理過的行列表。記得遵守 token 限制。
- **缺少區塊資訊：** 有些 OCR 引擎只回傳平面的單字列表。此時可依 `line_num` 相近的單字分組，重新構建行。

## 完整可執行範例

將所有步驟整合起來，以下是一個可端對端執行的單一檔案。請將佔位符替換為你自己的 API 金鑰與影像路徑。

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