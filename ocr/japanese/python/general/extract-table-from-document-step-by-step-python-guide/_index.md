---
category: general
date: 2026-01-02
description: Python を使用してドキュメントからテーブルを抽出します。PDF からテーブルを読み取り、テーブル行をクリーンで再利用可能なソリューションでイテレートする方法を学びましょう。
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: ja
og_description: Pythonで文書からテーブルを抽出する。このガイドでは、PDFからテーブルを読み取り、信頼できるエンジンでテーブルの行を反復処理する方法を示します。
og_title: ドキュメントからテーブルを抽出 – 完全なPythonチュートリアル
tags:
- Python
- PDF
- Data Extraction
title: ドキュメントから表を抽出する – ステップバイステップ Python ガイド
url: /ja/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ドキュメントからテーブルを抽出 – 完全 Python チュートリアル

テーブルを **ドキュメントから抽出** したいけど、どこから手を付ければいいか分からないことはありませんか？ 同じ壁にぶつかる開発者は多いです。PDF の中に隠れたテーブルデータを扱うときに特にそうです。このチュートリアルでは、**PDF からテーブルを読む** 方法と、**テーブル行をイテレート** してデータを好きな場所へ流す方法を実践的に解説します。

たとえば、請求書が多数あり、各請求書に明細テーブルがあるとします。その行を CSV に出力して downstream の分析に使いたい。この記事を読み終えると、まさにそれを実現する再利用可能なスニペットと、よくある落とし穴を回避するコツが手に入ります。

## 学べること

- レイアウトエンジンでドキュメントのレイアウトを検出する。  
- ポストプロセッサで生の検出結果を洗練させ、テーブル構造をきれいにする。  
- 検出したテーブルの各行をイテレートし、セル内容を出力（または保存）する。  

外部サービス不要、ブラックボックスも不要—ただの Python と、人気の OCR/レイアウトライブラリ（例: **pdfplumber**, **pdfminer.six**, または既に使っている商用 `engine`）だけです。`recognize_layout()` と `run_postprocessor()` を実装した `engine` オブジェクトがあれば、コードをそのまま貼り付けるだけで動きます。

> **プロのコツ:** 商用 SDK を使う場合は「テーブル検出」機能を必ず有効にしてください。そうしないと、生のレイアウトで結合セルが見逃されることがあります。

---

## 手順 1: テーブル構造を検出 – ドキュメントからテーブルを抽出

まず最初に必要なのは、ページ上のテーブルがどこにあるかを示す生のレイアウトです。多くの最新 PDF ライブラリは `recognize_layout()` のようなメソッドを提供し、ブロック・ライン・セルの階層構造を返します。

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**なぜ重要か:**  
生のレイアウトはすべてのテキスト要素の座標を提供しますが、ヘッダー・フッター・テーブル外の文字などノイズも含まれます。そこで次のステップでクリーンアップが必要になります。

> **よくある質問:** *PDF が複数ページある場合は？*  
> `recognize_layout()` は通常、ページオブジェクトのリストを返します。各ページをループし、同じポストプロセッシングロジックを適用してください。

---

## 手順 2: 検出結果を洗練 – PDF からテーブルを読む

`raw_layout` を取得したら、次はそれをきれいにします。ほとんどのエンジンは、断片化されたセルを結合し、不要なテキストを除去し、正しい `Table` オブジェクトを構築するポストプロセッサを提供しています。

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**必要な理由:**  
生のレイアウトでは、1 行が何十もの小さな断片として報告されることがあります。ポストプロセッサはそれらを論理的なセルにまとめ、後でイテレートしやすくします。

> **エッジケース:** 一部の PDF は目に見えない罫線を使用しています。行が抜けていると感じたら、エンジンに「見えない線を検出」フラグがあれば有効にしてください（利用可能な場合）。

---

## 手順 3: テーブル行をイテレート – テーブル行をイテレートする方法

クリーンな `enhanced_layout` が手に入ったら、データ抽出はとても簡単です。以下のコードは各行をループし、セルテキストをタブで結合（出力が整列しやすくなるため）して `print` しています。`print` を CSV ライターやデータベース挿入ロジックに置き換えるだけで応用できます。

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**期待される出力（例）:**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

タブ区切りではなく CSV が欲しい場合は、`"\t".join(...)` を `",".join(...)` に置き換えてファイルに書き出してください。

---

## 完全動作サンプル

全体をまとめた自己完結型スクリプトです。インポート文とエンジン初期化部分は、使用しているライブラリに合わせて調整してください。

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**差し替える箇所:**

- `initialize_engine(pdf_path)`: 使用するライブラリに合わせてエンジンインスタンスを作成。  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: メソッド名が異なる場合は正しい名前に置き換える。

`python extract_table.py invoice.pdf` で実行すると、タブ区切りのテーブルが標準出力に表示され、 downstream の処理にすぐ使えます。

---

## 画像イラスト

以下は検出パイプラインの概略図です。  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt text:* *extract table from document flow diagram*  

---

## FAQ とエッジケース

| 質問 | 回答 |
|----------|--------|
| **PDF に複数のテーブルがある場合は？** | `enhanced_layout.table` は最初に検出されたテーブルだけを保持することがあります。ライブラリがサポートしていれば `enhanced_layout.tables`（複数形）をループし、同じ行イテレーションロジックを各テーブルに適用してください。 |
| **結合セルはどう扱う？** | ポストプロセッサは通常、結合セルを個別エントリに展開します。展開されない場合はエンジンの `merge_cells` フラグを確認するか、座標に基づいて隣接セルを手動で結合してください。 |
| **スキャンした PDF からテーブルを抽出できる？** | 可能です。ただし、レイアウト検出の前に OCR が必要です。多くの SDK は OCR とレイアウト検出を一括で行う `recognize_layout()` を提供しています。 |
| **大量バッチ処理のパフォーマンスは？** | `concurrent.futures` などでページ単位やファイル単位の並列処理を行うと効果的です。重い部分は OCR なので、エンジンインスタンスはファイル間で再利用し、モデルの再ロードを避けましょう。 |
| **追加の依存関係は必要？** | `pdfplumber` を使う場合は `pip install pdfplumber` でインストールしてください。商用 SDK の場合はベンダーのインストールガイドに従ってください。 |

---

## 結論

今回は **ドキュメントからテーブルを抽出** する手順を、レイアウト検出 → 洗練 → 行イテレーションの流れで示しました。データウェアハウスへの投入、レポート作成、PDF→CSV 変換など、用途はさまざまですがパターンは変わりません：検出 → クリーン → イテレート。

次に試したいこと:

- 追加のスタイリング情報（フォント・色）を取得しながら **PDF からテーブルを読む**。  
- **pandas DataFrame** へ直接エクスポートして高度な分析に活用。  
- 同じパイプラインを逆に使い、**テーブルを書き戻す** 新しい PDF を生成。  

ぜひ自分の PDF でスクリプトを試し、静的テーブルをすぐに活用可能なデータへ変換してみてください。Happy extracting!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}