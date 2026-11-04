---
category: general
date: 2026-03-28
description: Aspose OCR を Python で使用して PNG からテキストを素早く抽出します。高性能な結果を得るために、並列画像認識 Python
  を活用したスキャンページのテキスト変換方法を学びましょう。
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: ja
og_description: Aspose OCR を Python で使用して PNG からテキストを高速に抽出します。このガイドでは、並列画像認識を活用したスキャンページのテキスト変換方法を示し、高速な結果を実現します。
og_title: PNGからテキストを抽出 – Pythonで高速並列OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: PNGからテキストを抽出 – Python と Aspose を使用した高速並列 OCR
url: /ja/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを抽出 – Pythonで高速並列OCR

PNGファイルから **テキストを抽出** したいけれど、シングルスレッドのOCRが極端に遅く感じたことはありませんか？ あなただけではありません。スキャンした領収書の山をデジタル化したり、講義スライドを検索可能なPDFに変換したりする際、ボトルネックはほとんどの場合OCRステップです。

このチュートリアルでは、Aspose OCR の非同期バッチモードと Python の `ThreadPoolExecutor` を組み合わせた **並列でスキャンページのテキストを変換** する、すぐに実行できる完全なソリューションをご紹介します。最後まで読めば、**画像テキストを python スタイルで認識** し、単純なループで処理する場合に比べて数十倍速く多数の画像を処理できるようになります。

> **得られるもの**  
> * PNG画像を同時にテキスト抽出する完全なスクリプト。  
> * 非同期バッチモードが高速化につながる仕組みの理解。  
> * 大規模なワークロードへスケールさせるためのヒント。

## 必要なもの

| 前提条件 | 理由 |
|--------------|--------|
| Python 3.9+ | モダンな構文と型ヒント。 |
| `aspose-ocr` と `aspose-storage` パッケージ | OCRエンジンと画像ローダーを提供します。 |
| PNGファイルのフォルダー（例：スキャンしたページ） | 処理したい元データです。 |
| Pythonの並行処理の基本知識 | 役立ちますが必須ではありません。すべて説明します。 |

Aspose ライブラリは以下でインストールできます:

```bash
pip install aspose-ocr aspose-storage
```

> **プロのコツ:** パッケージは常に最新に保ちましょう（`pip list --outdated`）ことで、最新のパフォーマンス改善を享受できます。

## ステップ1: Aspose OCRエンジンを非同期バッチモードで初期化する

最初に `OcrEngine` インスタンスを作成し、**非同期バッチモード** に切り替えます。このモードは内部で認識リクエストをキューイングし、Pythonスレッドをブロックせずに複数画像を同時に処理できるようにします。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*なぜ非同期なのか？*  
同期モードで `recognize` を呼び出すと、画像の処理が完了するまで呼び出し元がブロックされます。非同期モードでは、現在の画像がデコード中でも次の画像の処理を開始でき、I/O と CPU の作業が重なります。

## ステップ2: 処理したいPNGファイルを一覧化する

ここでは画像のコレクションを定義します。実際のプロジェクトでは `glob.glob("*.png")` のように動的に生成することもできますが、例示をシンプルに保つために明示的にリスト化しています。

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **注:** `YOUR_DIRECTORY` を実際の PNG スキャンが保存されているパスに置き換えてください。数百ファイルある場合は `os.listdir` と拡張子フィルタ（`.png`）を組み合わせると便利です。

## ステップ3: 画像をロードしテキストを返すヘルパー関数を書く

このヘルパーは **Aspose Storage** を介してファイルをロードし、OCRエンジンに渡す 2 ステップの処理を抽象化します。簡単な docstring を付けることで関数が自己文書化され、将来の保守が楽になります。

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*なぜ別関数にするのか？*  
スレッドプールのコードをすっきり保ち、他の場所（例: Flask エンドポイント）でもロジックを再利用できます。また、I/O を分離することでデバッグが容易になり、特定のファイルが失敗した場合は例外トレースにファイル名が表示されます。

## ステップ4: ThreadPoolExecutorで並列画像認識を実行する

ここで `ThreadPoolExecutor` を導入します。デフォルトでは 4 ワーカーを起動しますが、CPU コア数や画像セットのサイズに合わせて `max_workers` を調整してください。

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### これがPythonで並列画像認識を実現する仕組み

* **ThreadPoolExecutor** は各スレッドが `recognize_image` を呼び出すワーカースレッドプールを作成します。  
* OCR エンジンが非同期バッチモードにあるため、各スレッドはエンジンに仕事を渡したまま応答性を保てます。  
* `as_completed` は完了した順に Future を返すので、結果が出たらすぐに取得でき、大量バッチのストリーミングに最適です。

> **一般的な落とし穴:** `max_workers=1` にすると並列化の意味がなくなります。8 コアマシンでは `max_workers=8` が最高スループットになることが多いですが、ハードウェアに合わせて数値を試してみてください。

## ステップ5: 出力を検証し、エッジケースに対処する

スクリプトを実行すると、各 PNG のテキストがファイル名でプレフィックスされた形で表示されます:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

画像が破損している、または未対応フォーマットの場合は `except` ブロックがエラーメッセージを出力し、バッチ全体がクラッシュすることはありません。

### ソリューションの拡張

| シナリオ | 推奨の調整 |
|----------|-----------------|
| **数千ページ** | `ProcessPoolExecutor` に切り替えて複数 CPU プロセスを活用するか、リストを分割して順次バッチ処理する。 |
| **異なる画像フォーマット（JPG、TIFF）** | `storage.Image.load` メソッドはフォーマットを自動検出するので、ファイルを `input_images` に追加するだけで OK。 |
| **結果を保存する必要がある** | `else` ブロック内で `text` を `.txt` ファイルに書き込むか、データベースに挿入します。 |
| **パフォーマンス監視** | `recognize_image` をタイマー（`time.perf_counter`）でラップし、ファイルごとの処理時間をログに記録します。 |

## 完全な動作例（コピー＆ペースト可能）

以下が `parallel_ocr.py` というファイルにそのまま貼り付けられる、完成形スクリプトです。抜けはありません—必要なものはすべてここにあります。

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

ファイルを保存し、`YOUR_DIRECTORY` プレースホルダーを調整して実行してください:

```bash
python parallel_ocr.py
```

コンソールに各 PNG の抽出テキストが表示され、前述の例と同じ結果が得られるはずです。

## 結論

Aspose OCR の非同期バッチモードと Python の `ThreadPoolExecutor` を組み合わせることで、**PNGからテキストを効率的に抽出** できることを実証しました。このスクリプトはスキャンページのテキストを並列で変換し、**画像テキストを python スタイルで認識** するスケーラブルな方法を提供します。

さらに踏み込むなら、次のようなことに挑戦してみてください：

* 結果を検索可能な SQLite データベースに保存する。  
* OCR 前に OpenCV で画像前処理（デスクュー、ノイズ除去）を行う。  
* Flask や FastAPI のエンドポイントとしてスクリプトをマイクロサービス化する。

高性能 OCR の鍵は、エンジン自体の速さだけでなく、仕事をどれだけ効果的に並列化してエンジンに供給できるかにあります。このパターンを使えば、コード変更は最小限で数十、場合によっては数百の PNG スキャンを処理できます。

Happy coding, and may your PDFs always be searchable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}