---
category: general
date: 2026-01-12
description: OCRエンジンPythonを使用してPDFからテキストを抽出 – OCRでPDFを読み取り、OCR用に画像をロードし、構造化された結果を取得する方法を学びましょう。
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: ja
og_description: OCRエンジンPythonを使用してPDFからテキストを抽出します。このチュートリアルでは、OCRでPDFを読み取る方法、OCR用に画像をロードする方法、そして信頼性の高い結果を得るためにOCRエンジンPythonを使用する方法を示します。
og_title: PythonのOCRエンジンでPDFからテキストを抽出する – 完全ガイド
tags:
- OCR
- Python
- PDF
- Text Extraction
title: PythonのOCRエンジンでPDFからテキストを抽出する – ステップバイステップガイド
url: /ja/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFからテキストを抽出する OCRエンジン Python – 完全チュートリアル

PDFからテキストを抽出する必要があったことはありますか？しかしファイルがスキャン画像だけだった場合です。あなたは一人ではありません。多くの実務プロジェクトでは、受け取ったPDFに選択可能なテキストがなく、唯一の方法は **read PDF with OCR** です。  

このガイドでは、実用的なエンドツーエンドのソリューションを順を追って解説します。**load image for OCR** の方法、**OCR engine Python** の起動、そして下流パイプラインに流せる構造化テキストの抽出方法を正確に示します。曖昧な参照は一切なく、今日すぐにコピー＆ペーストできる完全な実行例をご提供します。

## What You’ll Learn

- 必要なPython OCRライブラリのインストールとインポート方法。  
- PDFファイルから **load image for OCR** する正確な手順。  
- エンジンの `recognize_structured()` メソッドを呼び出し、ブロック、行、単語をイテレートする方法。  
- 低信頼度の結果やマルチページPDFの取り扱いに関するヒント。  

このチュートリアルの最後までに、ページ数が1ページでも100ページでも、**extracts text from PDF** ドキュメントを確実に抽出できるスクリプトが手に入ります。

---

![OCRエンジンがPDFを処理し、構造化テキストを出力する様子を示す図。](images/ocr_flow.png "PDFからテキストを抽出する図")

*画像代替テキスト: OCR処理手順を示す PDFからテキストを抽出する図。*

## Prerequisites

- Python 3.9以上（コードはf‑stringsと型ヒントを使用しています）。  
- `OcrEngine` クラスを提供する pip でインストール可能な OCR パッケージ（例として架空の `pyocr` ライブラリ）。  
- ローカルに保存された処理対象のPDFファイル（例: `form.pdf`）。  

OCR ライブラリが不足している場合は、以下でインストールしてください。

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Step 1: Extract Text from PDF – Setting Up the OCR Engine

**read PDF with OCR** を実行する前に、エンジンインスタンスが必要です。エンジンは各ピクセルを見て、どの文字に相当するかを判断する「脳」のようなものです。

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** エンジンを一度初期化すれば、複数ファイルで言語パックを再利用でき、時間とメモリの両方を節約できます。

---

## Step 2: Load Image for OCR – Preparing Your PDF

PDF は生の画像ではないため、ライブラリは通常、最初のページ（またはすべてのページ）を OCR エンジンが理解できる画像に変換するヘルパーを提供します。

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** PDF に複数ページがある場合、多くの OCR ライブラリは `page=2` を指定したり、`engine.load_image(pdf_path, page=n)` をループで呼び出すことができます。大容量ドキュメントでは、メモリスパイクを防ぐためにページをバッチ処理することを検討してください。

---

## Step 3: Use OCR Engine Python – Recognizing Structured Text

ここで本格的な処理が行われます。`recognize_structured()` の呼び出しは、ブロック → 行 → 単語 の階層構造を返し、各要素には言語、信頼度、バウンディングボックスが付与されます。

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **What you get:**  
> - `structured_result.blocks` – 上位レベルのコンテナ（通常は段落や列）。  
> - 各ブロックは `lines` を含み、各行は `words` を含みます。  
> - 信頼度スコアを利用して、疑わしい結果をフィルタリングできます。

---

## Step 4: Iterate Over Results – Accessing Blocks, Lines, and Words

以下は、最も有用な情報をコンソールに出力するコンパクトなループ例です。JSON、CSV への書き出しやデータベースへの投入に拡張しても構いません。

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Expected Output

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Why you’ll love this:** 階層構造は人間がページを読む方式と同じなので、後でテーブルやカラムレイアウトを再構築するのが容易です。

---

## Step 5: Handling Edge Cases – Low Confidence & Multi‑Page PDFs

### Low‑Confidence Words

単語の信頼度が例えば `0.70` 未満に下がった場合、手動レビュー用にフラグを立てると良いでしょう。

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Processing All Pages

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** OCR ライブラリが毎回画像を再生成する場合、途中生成した PNG をキャッシュしておくと、大量バッチ処理時に数秒の短縮が期待できます。

---

## Full Working Script

すべてをまとめた単一ファイルは以下の通りです。すぐに実行可能です。

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

このファイルを `extract_pdf_ocr.py` として保存し、実行してください。

```bash
python extract_pdf_ocr.py
```

コンソールにブロックレベルの詳細が出力され、低信頼度の警告も表示されます。

---

## Conclusion

**extract text from PDF** を **OCR engine Python** で実現する、完全な本番レベルの手順をご紹介しました。ライブラリのインストールから **load image for OCR**、**read PDF with OCR**、そして構造化出力のイテレーションまで、あらゆるプロジェクトに応用できる再利用可能なスクリプトが手に入りました。

次に試すべきステップ:

- 階層構造を JSON にエクスポートし、下流の NLP パイプラインへ渡す。  
- 言語検出を組み込み、OCR モデルを動的に切り替える。  
- 複雑なレイアウトを含む PDF の前処理に `pdf2image` を統合する。  

マルチページの請求書バッチで試し、信頼度閾値を調整し、スキャンされた PDF を検索可能で編集可能なテキストに変換する速さを体感してください。問題があればコメントで教えてください—Happy OCRing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}