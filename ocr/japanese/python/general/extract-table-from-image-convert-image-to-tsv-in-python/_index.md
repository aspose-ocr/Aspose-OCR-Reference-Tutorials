---
category: general
date: 2026-07-05
description: Python OCR を使用して画像から表を抽出する。表の抽出方法、画像を TSV に変換する方法、そして OCR 表画像の Python
  テクニックをマスターしよう。
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: ja
og_description: Python OCRで画像から表を抽出する。このガイドでは、表の抽出方法、画像をTSVに変換する方法、そしてOCR表画像用Pythonツールの使い方を示します。
og_title: 画像から表を抽出 – Pythonで画像をTSVに変換
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: 画像から表を抽出 – Pythonで画像をTSVに変換
url: /ja/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から表を抽出 – Pythonで画像をTSVに変換

画像から表を抽出する方法で、髪の毛を抜くほど悩んだことはありませんか？このチュートリアルでは、`aocr` ライブラリを使って画像から **表を抽出** し、そのデータを整然とした TSV ファイルに変換する手順を解説します。魔法ではなく、数行の Python と AI を活用した後処理だけです。

スキャンした請求書やスクリーンショットから表をコピー＆ペーストしようとして、文字化けした混乱した状態になったことがあるなら、OCR 主導のアプローチを習得すべき理由が分かるでしょう。最後まで読めば、任意の表画像を Python に渡すだけで、スプレッドシートやデータベースで使えるきれいなタブ区切り値（TSV）を取得できるようになります。

---

## 必要なもの

本格的に始める前に、以下の環境が整っていることを確認してください。

| 要件 | 重要な理由 |
|------|------------|
| Python 3.9+ | `aocr` パッケージは最新の Python ランタイムを対象としています。 |
| `aocr` library (`pip install aocr`) | OCR エンジンと使用する AI 後処理を提供します。 |
| An image file containing a table (PNG, JPG, etc.) | 抽出対象となる表を含む画像ファイル（PNG、JPG など） |
| Optional: a virtual environment | 依存関係を分離して管理できます—強く推奨します。 |

これらが揃っていれば、ガイドの途中で中断することがなくなります。

---

## 依存関係のインストール

まず、OCR ツールをインストールしましょう。ターミナルを開いて以下を実行してください。

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **プロのコツ:** 権限エラーが出た場合は、`pip install` コマンドに `--user` を付けるか、グローバルインストールには `pipx` を使用してください。

---

## ステップ 1 – OCR エンジンの初期化

エンジンはプロセスの中心です。各ピクセルを見て、どの文字がどこに属すべきかを判断する「脳」と考えてください。

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

なぜ単一関数を呼び出すのではなくエンジンをインスタンス化するのでしょうか？エンジンオブジェクトは後からカスタムの後処理を付加でき、出力を細かく制御できます—**ocr table image python** の精度が必要なときに不可欠です。

---

## ステップ 2 – AI 後処理の付加

`aocr` には軽量な AI 後処理が同梱されており、生の OCR 結果をセルの境界を保ちつつクリーンアップします。追加の引数は不要で、コードがすっきりします。

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

このステップを省略すると、生テキストは取得できますが、表の構造はノイズだらけになります—まるで各セルが謎のスプレッドシートのようです。後処理はテキストを元のグリッドに合わせる重い作業を担います。

---

## ステップ 3 – 表画像の読み込み

任意のパスから画像を読み込めますが、分かりやすさのためプレースホルダーのディレクトリを使用します。`"YOUR_DIRECTORY/invoice_table.png"` を実際のファイルパスに置き換えてください。

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **注:** `aocr.Image` は画像形式を自動検出し、カラーチャンネルを正規化します。そのため、ファイルがひどく劣化していない限り、事前処理は不要です。

---

## ステップ 4 –構造化 OCR の実行

エンジンは画像を走査し、生のテーブルオブジェクトを返します。このオブジェクトは行・列と各セルの生テキストを含みます。

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

`recognize_structured` を汎用的な `recognize` 呼び出しの代わりに使う理由は何ですか？構造化バージョンは行・列の境界を推測し、後で TSV に変換しやすいマトリックス状の結果を提供します。

---

## ステップ 5 – AI 後処理でデータをクリーンアップ

後処理を実行すると、生の出力が洗練されます：不要な文字を除去し、分割された断片を結合し、各セルのテキストが正しく揃っていることを保証します。

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

`processed_table.table` を確認すると、行のリストが見えます。各行は `Cell` オブジェクトのリストです。各 `Cell` にはクリーンされた文字列を保持する `.text` 属性があります。

---

## ステップ 6 – 表を TSV としてエクスポート

最終ステップは、処理済みデータをタブ区切り値（TSV）ファイルに変換することです—Excel や Google Sheets 用に **convert image to TSV** したいときに必要なものです。

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

スクリプトを実行すると、各行がコンソールに出力され（必要なら）、任意のスプレッドシートプログラムで開けるクリーンな TSV ファイルが書き込まれます。

### 簡易検証

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

以下のように、列が整然と揃っているはずです：

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

出力が乱れている場合は、画像の品質（鮮明さ、コントラスト）を再確認し、OCR エンジンの設定を調整してください—`engine.set_config(...)` で言語モデルや信頼度閾値を変更できます。

---

## 一般的なエッジケースの対処

| 状況 | 推奨対策 |
|------|----------|
| **傾いた画像** | `Pillow` (`Image.rotate`) を使用して事前に回転させ、`aocr` に渡す。 |
| **コントラストが低い** | `cv2.equalizeHist` を適用して可読性を向上させる。 |
| **結合されたセル** | 既知の区切り文字に基づいて TSV を後処理してセルを分割するか、利用可能なら `merge_cells=False` フラグを使用する。 |
| **複数ページの PDF** | `pdf2image` で各ページを画像に変換し、パイプラインをループで実行する。 |

これらの調整により、さまざまなソース素材でも **ocr table image python** ワークフローが堅牢に保たれます。

---

## 完全スクリプト – オールインワン ソリューション

以下は、説明したすべてのステップをまとめた、実行可能な完全スクリプトです。`extract_table.py` として保存し、`python extract_table.py` を実行してください。

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [.NET 用 Aspose.OCR を使用した画像から表を抽出する方法](/ocr/english/net/text-recognition/recognize-table/)
- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}