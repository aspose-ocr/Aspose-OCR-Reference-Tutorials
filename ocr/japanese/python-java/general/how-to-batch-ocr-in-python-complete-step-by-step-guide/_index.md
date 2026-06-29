---
category: general
date: 2026-06-28
description: Python を使用したバッチ OCR の方法。複数の画像を OCR し、PNG からテキストを抽出し、画像をテキストに変換する完全な Python
  OCR チュートリアルを学びましょう。
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: ja
og_description: PythonでバッチOCRを行う方法は最初の文で説明しています。このPython OCRチュートリアルに従って、PNGファイルからテキストを効率的に抽出しましょう。
og_title: PythonでバッチOCRを行う方法 – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: PythonでバッチOCRを実行する方法 – 完全ステップバイステップガイド
url: /ja/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python でバッチ OCR を実行する方法 – 完全ステップバイステップガイド

スキャンしたページの山を **バッチ OCR** したいのに、UI をブロックしてしまうループを書きたくない、と思ったことはありませんか？ あなたは一人ではありません。PNG ファイルを 1 枚ずつ処理するのは、1 枚あたり数秒かかることもあり、まるで絵の具が乾くのを待つように感じられます。  

このチュートリアルでは、**複数画像を同時に OCR** し、**PNG からテキストを抽出** し、**画像をテキストに変換** する、モダンな Python OCR エンジンを使ったクリーンでノンブロッキングな方法を紹介します。最後まで読めば、どんなプロジェクトにもすぐに組み込める実行可能スクリプトが手に入ります – 手軽な *python ocr tutorial* から本番レベルのバッチジョブまで対応可能です。

## 作成するもの

- OCR エンジンを初期化し、言語を Latin（または必要な言語）に設定する。  
- 画像パスのリスト（例では PNG）をエンジンに渡す。  
- バッチ操作を起動し、Future 風のオブジェクトを取得する。  
- スレッドプールで結果を同時取得し、メインスレッドはフリーに保つ。  
- 各ページの認識テキストを整形して出力する。

特別な魔法はなく、純粋な Python とサードパーティ OCR ライブラリ（ここでは説明用に架空の `pyocr` パッケージを使用）だけです。  

**前提条件**  
- Python 3.8+ がインストールされていること。  
- Python の関数と `concurrent.futures` の基本が分かっていること。  
- `OcrEngine` クラスを提供する OCR ライブラリが利用可能であること（例：`pip install pyocr`）。  

これらが揃っていない場合は、今すぐ入手してください – 思ったより簡単です。

---

## Python でバッチ OCR を実行する – コアコンセプト

コードに入る前に、各ステップの「なぜ」を確認しましょう。

1. **言語を設定する理由は？**  
   エンジンが期待する文字種を把握していると、OCR の精度は飛躍的に向上します。Latin は英語、フランス語、スペイン語などに適しています。必要に応じて `Language.Japanese` や `Language.Arabic` に切り替えてください。

2. **バッチ操作を使う理由は？**  
   バッチ呼び出しにより、エンジンは内部でスレッドや GPU 加速を利用して作業をスケジュールできます。ハンドル（オブジェクト）を取得できるので、各画像の処理中にブロックされません。

3. **ThreadPoolExecutor を使う理由は？**  
   取得した Future オブジェクトは *遅延実行* です – 結果を要求したときに初めて処理が始まります。`getAll` にスレッドプールを渡すことで、各ページのテキスト取得を並列化し、全体の実行時間を大幅に短縮できます。

4. **結果を enumerate する理由は？**  
   結果の順序は入力パスの順序と一致するため、ページ番号を安全に付与できます。

これらの「なぜ」を理解すれば、他のライブラリや大規模データセットにもパターンを応用しやすくなります。

---

## Step 1: 必要パッケージのインストールとインポート

まず OCR ライブラリがインストールされていることを確認します。例では汎用的な `pyocr` パッケージを使用していますが、実際に使うライブラリ（例：`pytesseract`、`easyocr`）に置き換えてください。

```bash
pip install pyocr
```

次に必要なモジュールをインポートします。

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **プロのコツ:** `pathlib` の `Path` を使うと、スクリプトが OS 非依存になり、可読性が向上します。

---

## Step 2: OCR エンジンの作成と語彙設定

エンジンの作成はシンプルです。このデモでは Latin にロックします。

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

`setLanguage` 呼び出しはエンジンによっては省略可能ですが、習慣として入れておくと良いでしょう。対象文字セットを限定することで、速度と精度の両方が向上します。

---

## Step 3: 処理対象画像ファイルのリスト化（PNG からテキストを抽出）

変換したい PNG ファイルをすべて集めます。`Path.glob` を使うと、スクリプトを書き換えずにフォルダ全体を対象にできます。

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **なぜ重要か:** リストをソートしておくことで、後で結果とページ番号を正確に対応付けられます。

---

## Step 4: バッチ OCR 操作の開始（画像をテキストに変換）

リストをエンジンに渡します。メソッドは後で取得できる Future 風のコンテナを返します。

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

内部ではエンジンが独自のワーカースレッドや GPU パイプラインを起動しているかもしれません。重要なのは、`batch_future` というハンドルが取得できることです。

---

## Step 5: 結果を同時取得（OCR Multiple Images）

ここが本格的な *バッチ* 処理です。`ThreadPoolExecutor` を `getAll` に渡すことで、各ページのテキスト取得が個別スレッドで行われます。

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

`max_workers` は CPU コア数や OCR ライブラリの推奨に合わせて調整してください。ワーカーを増やせば必ず速くなるわけではありません – CPU 使用率を監視しましょう。

---

## Step 6: 認識結果の出力（Python OCR Tutorial Finale）

最後に各ページのテキストを出力します。`Result` オブジェクトの `getText()` を呼び出します – ライブラリによってメソッド名が異なる場合は適宜変更してください。

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**期待される出力例（サンプル）**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

画像が失敗した場合、多くのエンジンは空文字列を返すか例外をスローします。`try/except` でループを包むと、エッジケースを優雅に処理できます。

---

## 完全版スクリプト – すぐに実行可能

以下が完結した自己完結型スクリプトです。`batch_ocr.py` という名前で保存し、`YOUR_DIRECTORY` を適切に設定したうえで `python batch_ocr.py` を実行してください。

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

保存して実行すれば、コンソールに抽出されたテキストが次々と表示されます。シンプルで高速、しかも完全に非同期です。

---

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **出力がない** – 空文字列 | 画像がノイズ過多でテキストが検出できなかった | 前処理で二値化、デスケュー、DPI 増加などを行う |
| **`FileNotFoundError`** | ディレクトリパスが間違っている、または PNG が存在しない | `YOUR_DIRECTORY` を再確認し、拡張子が `.png` であることを確認 |
| **CPU 使用率が高すぎる** | `max_workers` をマシンに対して大きく設定しすぎた | `max_workers` を減らすか、GPU が利用可能なら有効化 |
| **Unicode が乱れる** | エンジンが別言語で動作している | バッチ OCR 前に `engine.setLanguage(Language.Latin)`（または適切な言語）を呼び出す |

早期に対処すれば、デバッグに費やす時間を大幅に削減できます。

---

## チュートリアルの拡張 – 次のステップ

- **他フォーマットの OCR**（JPEG、TIFF） – `glob` パターンを変更するだけです。  
- **抽出したテキストを検索インデックス**（例：Elasticsearch）に投入する。  
- **画像からテキストへ変換**し、`reportlab` や `PyPDF2` で PDF を生成する。  
- **マシン間で並列化**する場合は `multiprocessing` や Celery のようなタスクキューを活用し、超大規模データセットに対応する。  

これらはすべて、今回の **python ocr tutorial** を土台に自然に拡張できます。

---

## 結論

PNG ファイルのコレクションに対して **バッチ OCR** を実行する方法を順を追って解説し、バッチ指向 API の威力とスレッドプールを用いた **PNG からテキストを抽出** のテクニックを示しました。上記のスクリプトは本番環境でも使えるレベルです。言語設定を変えたり、`pyocr` を `pytesseract` に差し替えてみても、パターンは変わりません。質問や面白い活用例があればコメントで教えてください。  

*Happy coding!*

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能や代替実装アプローチを自分のプロジェクトでマスターできます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}