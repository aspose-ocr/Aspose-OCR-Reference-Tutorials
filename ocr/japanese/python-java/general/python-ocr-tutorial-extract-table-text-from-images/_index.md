---
category: general
date: 2026-01-12
description: Python OCRチュートリアル：画像からテーブルのテキストを抽出する方法を紹介します。画像からテーブルを読み取り、Aspose OCRを使用して選択したテキストを抽出する方法を学びましょう。
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: ja
og_description: 画像からテーブルテキストを抽出し、画像からテーブルを読み取り、Aspose OCRを使用して選択したテキストを抽出する方法を教えるPython
  OCRチュートリアル。
og_title: Python OCRチュートリアル：画像から表のテキストを抽出
tags:
- OCR
- Python
- AsposeOCR
title: Python OCRチュートリアル：画像から表のテキストを抽出
url: /ja/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR チュートリアル：画像からテーブルテキストを抽出する

スキャンしたフォームからテーブルを抽出する方法を実際に示す **python ocr tutorial** が欲しかったことはありませんか？ あなただけではありません。ほとんどのチュートリアルは汎用的なテキスト抽出で止まり、欲しいデータのきれいなグリッドをどのように分離すれば良いか分からないままです。

このガイドでは、実際のシナリオとして画像からテーブルを読み取り、必要な選択テキストだけを抽出し、最終的に結果を出力する手順を解説します。その過程で **how to extract table** データを確実に取得するコツも紹介するので、毎回ゼロから作り直す必要はありません。

## 学べること

- Aspose OCR for Python のセットアップ方法。
- テーブルを含む矩形領域の定義方法。
- **extract table text** と **read table from image** の正確な手順。
- 複数言語や不規則なテーブルレイアウトへの対処法のヒント。
- すぐにプロジェクトに組み込める、完全で実行可能なスクリプト。

**前提条件**  
- Python 3.8 以上。  
- OCR の基本概念に関する基礎知識（深い専門知識は不要）。  
- 明瞭なテーブルを含む PNG または JPEG 画像（ここでは `form_with_table.png` と呼びます）。  

これらが揃っていれば、さっそく始めましょう—余計な説明は省き、実践的なコードだけです。

![python ocr tutorial example of table region](table_region_example.png){alt="テーブル領域を示す python ocr tutorial の例"}

## ステップ 1: Aspose OCR のインストールとインポート

まず最初に、Aspose OCR ライブラリが必要です。パッケージは PyPI にあるので、`pip` コマンド一つでインストールできます。

```bash
pip install aspose-ocr
```

次に、必要なモジュールとヘルパーをインポートします。

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* 依存関係は `requirements.txt` にまとめておきましょう。環境の再現が簡単になります。

## ステップ 2: OCR エンジンの初期化（Python OCR Tutorial Core）

エンジンの作成は、どの **python ocr tutorial** においても中心的な作業です。ここではデフォルト言語を英語に設定していますが、後から変更可能です。

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

言語を設定する理由は何ですか？ エンジンが期待する文字種を把握していると、OCR の精度は劇的に向上します。多言語フォームを扱う場合は、言語のリストを設定するか、領域ごとに上書きできます（後述）。

## ステップ 3: 画像の読み込み

Aspose OCR は一般的な画像形式に対応しています。ファイルパスを指定すれば、処理可能な `Image` オブジェクトが取得できます。

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Edge case:* 5 MB を超える大きな画像は処理が遅くなることがあります。パフォーマンスが問題になる場合は、OCR 前にリサイズや圧縮を検討してください。

## ステップ 4: テーブル領域の定義（Read Table from Image）

ここが楽しい部分です：エンジンにテーブルがどこにあるかを指示します。`OcrRegion` に `Rectangle`（x, y, width, height）を渡します。座標はピクセル単位なので、多少の試行錯誤が必要です。

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

領域を使う理由は何ですか？ OCR をテーブル領域に限定することで **extract selected text** が高速化し、周囲のラベルやグラフィックからのノイズを回避できます。また、エンジンが均一なレイアウトに集中できるため、精度も向上します。

## ステップ 5: 定義した領域で OCR を実行

領域を設定したら、`process_region` を呼び出します。このメソッドは生テキスト、信頼度スコア、必要に応じてバウンディングボックスを含む `OcrResult` オブジェクトを返します。

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

複数のテーブルを抽出したい場合は、異なる矩形でステップ 4‑5 を繰り返すだけです。

## ステップ 6: 抽出したテーブルテキストの出力

最後に、テーブルのテキスト表現を出力（または保存）します。Aspose OCR は行区切りが行に合わせて配置されたプレーンテキストを返すため、後処理がシンプルです。

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**期待される出力**（例）:

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

この文字列を `csv` パーサーや pandas の DataFrame、あるいは任意の下流分析パイプラインに渡すことができます。

## 完全な動作例

すべてをまとめた、すぐに実行できるスクリプトです。`YOUR_DIRECTORY/form_with_table.png` を実際の画像パスに置き換えてください。

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

`python extract_table.py` でスクリプトを実行します。すべてが正しく設定されていれば、コンソールにテーブルが表示されます。

## よくある質問とエッジケースの対処

**テーブルが完全に矩形でない場合はどうすればいいですか？**  
テーブルを複数の重複領域に分割するか、全体をカバーする大きめの矩形を使用してからテキストを後処理（例：改行で分割）してください。

**特定の列だけを抽出できますか？**  
フルテーブルテキストを取得した後、Python の `csv` や `pandas` を使って必要な列だけを抽出します。OCR の段階では矩形内のすべてが取得されます。

**英語以外のテーブルを扱うにはどうすればいいですか？**  
`ocr_engine.language`（または `region.language`）に適切な列挙子を設定します。例：`ocr.Language.FRENCH`、または `ocr.Language.ENGLISH | ocr.Language.SPANISH` のように複数言語を組み合わせられます。

**各セルのバウンディングボックスを取得する方法はありますか？**  
Aspose OCR は `region_result.words` を返し、各単語にバウンディングボックスが含まれます。これらをグリッドにマッピングすれば、セル単位の位置情報を取得できます。高度なレイアウト解析に有用です。

## 精度向上のためのヒント

- 画像をクリーニングする：OCR にかける前に二値化やコントラスト強化を行いましょう。Pillow などのライブラリが役立ちます。  
- 圧縮アーティファクトを避ける：可能であればスキャンは PNG で保存しましょう。  
- DPI に注意：300 dpi が最適です。低い DPI は文字欠損の原因になります。  
- 矩形サイズを試す：やや大きめの矩形にすると、テーブルに属する余分な文字も捕捉しやすくなります。  

## 次のステップ

この **python ocr tutorial** で **how to extract table** の基礎をマスターしたので、次は以下に挑戦してみましょう：

- 抽出したテキストを Python の `csv` モジュールで CSV ファイルに変換する。  
- データを **pandas** の DataFrame に投入して分析する。  
- 手書きフォームを OCR で読み取る（別のエンジンや追加トレーニングが必要）。  
- シンプルな `for` ループで数十枚のスキャンフォームをバッチ処理する自動化。  

これらの拡張はすべて、本チュートリアルで扱ったコア概念に基づいているため、スケールアップもスムーズに行えます。

*ハッピーコーディング！問題があれば下にコメントを残してください—抽出の微調整を喜んでお手伝いします。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}