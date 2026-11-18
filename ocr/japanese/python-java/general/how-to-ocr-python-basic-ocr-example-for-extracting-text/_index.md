---
category: general
date: 2026-04-26
description: 'PythonでOCRの方法: 基本的なOCR例を使って画像からテキストを抽出し、TIFFファイルをPythonで読み取る方法を学びます。すぐに実行できるコードが含まれています。'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: ja
og_description: PythonでOCRを行う方法：画像からテキストを抽出し、PythonでTIFFファイルを読み取り、スキャンした画像のテキストをシンプルで実行可能なスクリプトで変換するステップバイステップガイド。
og_title: PythonでOCRを行う方法 – テキスト抽出の基本OCR例
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRする方法 – テキスト抽出の基本OCR例
url: /ja/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – テキスト抽出のための基本 OCR 例

スキャンした TIFF が机の上にあるとき、**how to ocr python** が気になったことはありませんか？ 画像ファイルの山を見ながら「この中の文字をどうやって取り出すんだろう？」と考えているのはあなただけではありません。良いニュースは、適切なライブラリといくつかのシンプルな手順さえあれば、画像をプレーンテキストに変換するのはとても簡単だということです。

このチュートリアルでは、TIFF ファイルを読み込み、テキストを抽出し、コンソールに出力する **基本 OCR 例** を順を追って解説します。最後まで読めば、**画像からテキストを抽出**する方法、TIFF 形式特有の注意点、そして **スキャンした画像テキストを変換** する際に調整すべきポイントがすべて分かります。隠された魔法はありません—今日すぐにコピー＆ペーストして実行できるシンプルな Python です。

## What You’ll Need

始める前に、以下を用意してください。

- Python 3.9+ がインストール済み（最新の安定版がベストです）。
- pip でインストールできる OCR ライブラリ。本ガイドでは、Tesseract などの人気ツールを模倣した架空の `aocr` パッケージを使用します。後で `pytesseract` や `easyocr` に置き換えることも可能です。
- 処理したい TIFF 画像 – `input.tiff` という名前で、コードで参照するフォルダーに配置してください。
- コマンドラインの基本的な操作に慣れていること（パッケージをインストールする程度）。

以上です。重い依存関係や Docker コンテナは不要、数行のコードだけです。

## Step 1 – Install and Import Dependencies (how to ocr python)

まず OCR パッケージを取得します。ターミナルを開いて次のコマンドを実行してください。

```bash
pip install aocr
```

実際のライブラリを使いたい場合は、`aocr` を `pytesseract` に置き換え、Tesseract エンジンを別途インストールしてください。

次に必要なモジュールをインポートします。`pathlib` の `Path` クラスは、OS を問わずファイルパスを扱うのに便利です。

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*なぜ `Path` を使うのか？* スラッシュ（`/` と `\`）の違いを抽象化し、ディレクトリ結合を OS に依存せずに行えるためです。この小さな工夫が、後で CI サーバーにスクリプトを移す際の頭痛の種を減らしてくれます。

## Step 2 – Create the OCR Engine Instance (basic ocr example)

次に OCR エンジンのインスタンスを作成します。`OcrEngine` は画像を読み取り文字列を出力する「脳」のようなものです。

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

多くの OCR ライブラリはここで言語、DPI、信頼度閾値などを調整できます。この **basic OCR example** ではデフォルト設定のまま進めますが、後で多言語文書を扱う場合は `ocr_engine.config` を確認してください。

## Step 3 – Load Your TIFF Image (read tiff file python)

ここが **read tiff file python** の出番です。TIFF はマルチページになることがありますが、`Image.load` はデフォルトで最初のページだけを取得します—単一ページのスキャンには最適です。

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

`"YOUR_DIRECTORY"` を `input.tiff` が置かれている実際のフォルダーに置き換えてください。スクリプトの実行ディレクトリが不明な場合は、`Path.cwd()` が現在の作業ディレクトリを表示してくれるので、パスのデバッグに便利です。

## Step 4 – Run the OCR Process (extract text from image)

いよいよ本番です。`process()` を呼び出すと画像が OCR パイプラインに流れ、結果オブジェクトが返ります。

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

内部ではエンジンが画像をグレースケールに変換したり、しきい値処理を行ったりしてからニューラルネットワークに渡しています。これらのステップはライブラリが自動で処理してくれるので、開発者が意識する必要はありません。

## Step 5 – Print the Recognized Text (convert scanned image text)

最後にテキストを出力します。実際のプロジェクトではファイルやデータベースに保存することが多いですが、例示のためにコンソールへ出力しています。

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

スクリプトを実行すると、次のような出力が得られるはずです。

```
Hello, world!
This is a sample scanned document.
```

出力が文字化けしている場合は、元画像が鮮明かどうか、OCR の言語設定がテキストと合っているかを再確認してください。

## Full Working Script

以上をすべて組み合わせた、実行可能な完全スクリプトは以下の通りです。

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

**スキャンした画像テキストを検索可能な PDF** に変換したい場合は、`ocr_result.text` を `reportlab` などの PDF ジェネレータに渡すと良いでしょう—ただしそれは別のチュートリアルになります。

## Common Pitfalls & Pro Tips

- **低解像度スキャン**: OCR は 150 DPI 未満では精度が落ちます。画像がぼやけている場合は Pillow の `Image.open(...).resize(...)` でアップサンプリングしてください。
- **複数ページ**: マルチページ TIFF の場合は `Image.load_multi_page()`（ライブラリが対応していれば）でページを順に処理し、結果を結合します。
- **言語サポート**: 多くのエンジンはデフォルトで英語です。例としてスペイン語を扱う場合は `ocr_engine.language = "spa"` と設定します。
- **空白文字の処理**: OCR は余計な改行を入れがちです。`str.splitlines()` や正規表現でクリーンアップしましょう。
- **パフォーマンス**: 大量処理を行う際は、ファイルごとに新しい `OcrEngine` を作るのではなく、1つのインスタンスを再利用してください。

## Extending the Example

単一画像で **how to ocr python** をマスターしたら、次のステップに挑戦してみてください。

1. **バッチ処理** – ディレクトリ内の TIFF をループで走査し、各結果を `.txt` ファイルに書き出す。
2. **Pandas との統合** – 抽出したテキストとメタデータを組み合わせて、迅速な分析を可能にする。
3. **ハイブリッドアプローチ** – OCR と `spaCy` などの NLP ライブラリを組み合わせ、スキャンした請求書から名前・日付・金額といったエンティティを抽出する。
4. **代替ファイル形式** – `Image.load` を `Image.from_bytes` に置き換えて、API やデータベースから取得した画像を直接処理する。

これらすべては **extract text from image** と **convert scanned image text** の基本概念に基づいており、機械が理解できる形に変換する土台となります。

## Conclusion

本稿では、**how to ocr python**、**read tiff file python**、そして **extract text from image** を数行のコードで実現する **basic OCR example** を丁寧に解説しました。スクリプトは自己完結型でエラーハンドリングも含み、結果を直接コンソールに出力します。これをベースに、OCR バックエンドの差し替えや前処理の調整、下流ワークフローへの接続など、さまざまな応用が可能です。

質問やエッジケース、言語パック、パフォーマンスチューニングに関する疑問があれば、ぜひコメントで教えてください。Happy coding!

![how to ocr python example](/images/ocr-python-example.png "how to ocr python スクリプト出力のスクリーンショット")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}