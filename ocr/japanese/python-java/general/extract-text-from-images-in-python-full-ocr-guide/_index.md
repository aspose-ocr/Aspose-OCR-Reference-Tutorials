---
category: general
date: 2026-06-19
description: Python OCR を使用して画像からテキストを抽出します。自動言語検出、並列処理、バッチ認識を簡潔なチュートリアルで学びましょう。
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: ja
og_description: Python OCRで画像からテキストを抽出します。このガイドでは、自動言語検出、並列処理、バッチ認識を1つのチュートリアルで紹介しています。
og_title: Pythonで画像からテキストを抽出する – 完全OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像からテキストを抽出する – 完全OCRガイド
url: /ja/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像からテキストを抽出 – 完全OCRガイド

画像の文字を手で入力せずに **画像からテキストを抽出** できたらと思ったことはありませんか？ あなただけではありません。古いレシートをデジタル化したり、検索可能な文書アーカイブを構築したり、単にクールなAIトリックで遊んだりする場合でも、画像から文字を取り出す能力は、今日のPython開発者にとって必須のスキルです。

このチュートリアルでは、人気のOCRエンジンを使って **画像からテキストを抽出** する、実行可能な完全なサンプルを順に解説します。自動言語検出、速度向上のための並列処理、バッチ画像認識をカバーし、数十ファイルを数秒で処理できるようにします。必要な内容ですか？ それでは始めましょう。

## 学べること

- `ocr.OcrEngine` で OCR エンジンをインスタンス化する方法
- **自動言語検出** を有効にして、エンジンが自動で適切な言語を選択する方法
- カスタムスレッドプールで **並列処理 OCR** を設定する方法
- ファイルリストに対して **バッチ画像認識** を実行する方法
- 各画像の認識結果テキストを出力し、保存やインデックス作成に利用できる形で表示する方法

外部ドキュメントは不要です。必要なものはすべてここにあり、`ocr` パッケージ（`pip install ocr` でインストール）だけで動作します。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

1. Python 3.8 以降がインストールされていること。
2. `ocr` パッケージ（`pip install ocr`）。
3. 処理したい PNG（または JPG）画像が入ったフォルダー。
4. Python の関数とループに関する基本的な知識。

以上です—重い依存関係も GPU も不要で、純粋な Python だけです。

![画像からテキストを抽出する例](https://example.com/ocr-demo.png "画像からテキストを抽出する出力のスクリーンショット")

*Alt text: 画像からテキストを抽出するデモスクリーンショット*

## Step 1 – OCR エンジンのセットアップ（Primary Keyword in Action）

まず最初に OCR エンジンのインスタンスを作成します。`ocr.OcrEngine()` は操作の中枢で、文字・行・段落を読む方法を知っています。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

なぜ明示的にエンジンが必要なのか？ **ocr.OcrEngine の使用** により、言語設定やスレッド管理などを細かく制御できるからです。ワンライナーのヘルパーに比べ、**画像からテキストを抽出** する最も柔軟な方法です。

## Step 2 – エンジンに自動言語検出を任せる

多くの OCR ライブラリは対象言語を手動で指定する必要があります。単一言語のプロジェクトでは問題ありませんが、混在言語のバッチ処理では面倒です。幸い、`ocr` パッケージは **自動言語検出** をサポートしています。

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

`engine.language` に `ocr.Language.Auto` を設定すると、エンジンは各画像を解析して適切な言語モデルを自動で選択します。この一行で、国際文書を扱う際の手動設定作業を何時間も削減できます。

## Step 3 – 並列処理 OCR で速度アップ

CPU コアが4つ以上あるなら、活用しませんか？ エンジンはスレッドプールを立ち上げ、複数画像を同時に処理できます。ここが **並列処理 OCR** の威力です。

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

マシンに合わせて `4` の数値は自由に調整してください。スレッド数を増やすほどバッチ実行は速くなりますが、各スレッドはメモリを消費するので、環境に合ったバランスを見つけましょう。

## Step 4 – 処理したい画像を集める

次にファイルパスのリストが必要です。手動で作成したり、CSV から読み込んだり、`glob` を使ったりできます。ここでは簡潔さのためにハードコードした短いリストを示します。

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

`YOUR_DIRECTORY` を実際のパスに置き換えてください。数十ファイルがある場合は、`glob.glob("*.png")` で一括取得できます。

## Step 5 – バッチ画像認識を実行

チュートリアルの核心です。`files` に含まれるすべての画像を処理し、結果オブジェクトのリストを返す単一呼び出しです。これが **バッチ画像認識** 機能で、大規模 OCR を実用的にします。

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

内部では、先ほど設定した4つのワーカースレッドに各ファイルが分配され、同時に自動言語検出も行われます。メソッドは、認識されたテキストとメタデータを保持した要素のリストを返します。

## Step 6 – 抽出したテキストを出力（または保存）

最後に結果をループしてテキストを出力します。実際のプロジェクトではデータベースや CSV に書き込むことが多いですが、ここではシンプルにコンソールへ表示します。

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**期待される出力**（簡略化）:

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

各ブロックはファイル名と OCR で取得した文字列を示します。画像に複数言語が混在している場合は、前述の **自動言語検出** ステップのおかげで適切な文字が表示されます。

## プロのコツ & よくある落とし穴

- **画像品質が重要** – ぼやけた画像やコントラストが低い画像はゴミデータになります。必要に応じて OpenCV（`cv2.threshold`、`cv2.resize`）で前処理してください。
- **スレッド数 vs I/O** – 画像が遅いネットワークドライブ上にある場合、スレッドを増やしても効果が薄いことがあります。`top` や `Task Manager` で CPU 使用率を監視しましょう。
- **Unicode の取り扱い** – `result.text` は Unicode 文字列です。ファイルに書き込む際は `encoding="utf-8"` で開き、`UnicodeEncodeError` を回避してください。
- **メモリ使用量** – 大きな PDF を処理すると RAM を大量に消費します。`MemoryError` が出たらスレッドプールサイズを減らすか、画像を小さなチャンクに分割して処理してください。

## 完全動作スクリプト

以下は、ここまで説明したすべての手順を組み込んだ、コピー＆ペースト可能なスクリプトです。`batch_ocr.py` として保存し、`python batch_ocr.py` を実行してください。

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

実行例:

```bash
python batch_ocr.py ./my_images 4
```

各画像に対して整形されたテキストブロックが表示され、**画像からテキストを抽出** がスケールで可能であることが証明されます。

## 次にやるべきこと

Python で **画像からテキストを抽出** する基本をマスターしたら、以下のテーマを検討してみてください。

- **ポストプロセッシング**: 正規表現や自然言語処理ライブラリで OCR 出力をクリーンアップ
- **PDF 変換**: 抽出した文字列を PDF ジェネレータに渡し、検索可能な PDF を作成
- **クラウド OCR サービス**: オンプレミスの `ocr` 結果を Google Vision や Azure OCR と比較し、エッジケースの精度を検証
- **GUI フロントエンド**: 小さな Flask や FastAPI アプリを作り、ユーザーが画像をアップロードして即座にテキストを取得できるようにする

これらすべてが、今回構築した **Python OCR ライブラリ** の基盤と、ここで使った **並列処理 OCR** のテクニックから恩恵を受けます。

---

*Happy coding! If you hit any snags, drop a comment below—I'm always up for troubleshooting OCR quirks.*

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、独自プロジェクトで代替実装を試したりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}