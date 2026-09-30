---
category: general
date: 2026-02-22
description: OCRテキストの抽出方法と、AIによる後処理でOCR精度を向上させる方法を学びましょう。ステップバイステップの例で、Pythonを使ってOCRテキストを簡単にクリーンアップできます。
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: ja
og_description: シンプルなPythonワークフローとAIポストプロセッシングを活用して、OCRテキストの抽出、OCR精度の向上、そしてOCRテキストのクリーンアップ方法を学びましょう。
og_title: OCRテキストの抽出方法 – ステップバイステップガイド
tags:
- OCR
- AI
- Python
title: OCRテキストの抽出方法 – 完全ガイド
url: /ja/python/general/how-to-extract-ocr-text-complete-guide/
---

.

Now produce final translated content with same structure.

Make sure to keep blank lines as needed.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRテキストの抽出方法 – 完全プログラミングチュートリアル

スキャンした文書から **OCRを抽出する方法** について考えたことはありますか？ あなただけではありません。実際のプロジェクトでは、OCRエンジンの生データが乱れた段落のように見え、クリーニングが面倒に感じられます。  

良いニュースは？このガイドに従うことで、構造化されたOCRデータを取得し、AIポストプロセッサを実行し、**クリーンなOCRテキスト** を得て、下流の分析にすぐ使えるようになります。また、**OCR精度を向上させる** テクニックにも触れますので、結果が最初から信頼できるようになります。

次の数分で、必要なものすべてをカバーします：必須ライブラリ、実行可能な完全スクリプト、そして一般的な落とし穴を回避するためのヒントです。「ドキュメントを参照」などの曖昧なショートカットはありません—コピー＆ペーストしてすぐに実行できる、完全に自己完結したソリューションだけを提供します。

## 必要なもの

- Python 3.9+（コードは型ヒントを使用していますが、古い3.xバージョンでも動作します）
- 構造化された結果を返すことができるOCRエンジン（例：`pytesseract` を使用した Tesseract と `--psm 1` フラグ、またはブロック/行メタデータを提供する商用API）
- AIポストプロセッシングモデル – この例ではシンプルな関数でモックしますが、OpenAI の `gpt‑4o-mini`、Claude、またはテキストを受け取りクリーンな出力を返す任意のLLMに差し替えることができます
- テスト用のサンプル画像（PNG/JPG）の数行

これらが揃っているなら、さっそく始めましょう。

## OCRの抽出方法 – 初期取得

最初のステップはOCRエンジンを呼び出し、プレーンな文字列ではなく **構造化表現** を要求することです。構造化された結果はブロック、行、単語の境界を保持するため、後のクリーニングが格段に楽になります。

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

> **Why this matters:** ブロックと行を保持することで、段落の開始位置を推測する必要がなくなります。`recognize_structured` 関数は、後でAIモデルに入力できるクリーンな階層構造を提供します。

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

スニペットを実行すると、OCRエンジンが見た通りの最初の行がそのまま出力されます。ここにはしばしば “0cr” のように “OCR” と誤認識された文字が含まれます。

## AIポストプロセッシングでOCR精度を向上させる

生の構造化出力が得られたので、AIポストプロセッサに渡しましょう。目的は、一般的なミスを修正し、句読点を正規化し、必要に応じて行を再セグメント化することで **OCR精度を向上させる** ことです。

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

> **Pro tip:** LLMのサブスクリプションがない場合は、呼び出しをローカルトランスフォーマー（例：`sentence‑transformers` とファインチューニングされた補正モデル）やルールベースのアプローチに置き換えることができます。重要な考え方は、AIが各行を個別に見ることで、通常は **OCRテキストをクリーンに** するのに十分だということです。

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

これで、はるかにクリーンな文が表示されるはずです—誤字が修正され、余分なスペースが削除され、句読点が整えられます。

## より良い結果のためのOCRテキストのクリーニング

AIによる補正後でも、最終的なサニタイズステップを適用したい場合があります：非ASCII文字を除去し、改行を統一し、複数のスペースを縮小します。この追加処理により、出力はNLPやデータベースへの取り込みなどの下流タスクにすぐ使える状態になります。

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

`final_cleanup` 関数は、検索インデックス、言語モデル、または CSV エクスポートに直接入力できるプレーンな文字列を返します。ブロック境界を保持したままなので、段落構造が保たれます。

## エッジケースと想定シナリオ

- **Multi‑column layouts:** ソースに列がある場合、OCRエンジンは行を交互に出力することがあります。TSV出力から列座標を検出し、AIに送る前に行を再順序付けできます。
- **Non‑Latin scripts:** 中国語やアラビア語などの言語の場合、LLMのプロンプトを言語固有の補正を要求するように切り替えるか、そのスクリプトに特化したファインチューニング済みモデルを使用します。
- **Large documents:** 各行を個別に送信すると遅くなる可能性があります。行をバッチ化（例：リクエストあたり10行）し、LLMにクリーンな行のリストを返させます。トークン制限に注意してください。
- **Missing blocks:** 一部のOCRエンジンは単語のフラットリストしか返さないことがあります。その場合、`line_num` が似ている単語をグループ化して行を再構築できます。

## 完全動作例

すべてを統合した、エンドツーエンドで実行できる単一ファイルをご紹介します。プレースホルダーはご自身のAPIキーと画像パスに置き換えてください。

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