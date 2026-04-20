---
category: general
date: 2026-03-18
description: Python と Aspose OCR を使用して PNG からテキストを抽出します。OCR 用に画像を読み込む方法、複数ファイルで OCR
  を実行する方法、そして並列画像認識によるバッチ OCR を実現する方法を学びましょう。
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: ja
og_description: PythonでAspose OCRを使用してPNGからテキストを抽出します。このチュートリアルでは、OCR用に画像を読み込む方法、複数ファイルのOCRを処理する方法、そして並列画像認識を利用したバッチOCR画像の実行方法を示します。
og_title: PNGからテキストを抽出 – 並列OCRガイド
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: PNGからテキストを抽出 – バッチ画像認識のための並列OCRガイド
url: /ja/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを抽出 – バッチ画像認識のための並列OCRガイド

PNGファイルから**PNGからテキストを抽出**したいと思ったことはありませんか？しかし、1枚の画像の処理に時間がかかりすぎて行き詰まったことはありませんか？あなたは一人ではありません。実際のプロジェクトでは、請求書スキャナ、レシートデジタライザ、アーカイブツールなどを考えてみてください。速度が重要で、PNGを1枚ずつ処理するだけでは間に合いません。  

このガイドでは、**loads image for OCR** を行い、**ocr multiple files** を **batch OCR images** 方式で実行し、Python の `threading` モジュールを使った **parallel image recognition** を活用する、完全な実行可能ソリューションを順に解説します。最後まで読めば、PNG を任意の数だけ、数秒でテキスト抽出できるスクリプトが手に入ります。

## 必要なもの

- Python 3.8 以上（示した構文は 3.10+ でも動作します）。  
- Aspose OCR for Java/​Python パッケージ（`aspose-ocr`）。`pip` でインストールできます。  
- 処理したい PNG ファイルが数個入ったフォルダー。  
- 適度な量の RAM—各スレッドは小さな OCR エンジンインスタンスを保持するため、ノートパソコンでも数十のワーカーを起動できます。

外部サービスもクラウドキーも不明な設定ファイルも不要です。コピー＆ペーストして実行できる純粋な Python コードだけです。

## なぜ PNG からテキストを並列で抽出するのか？

PNG の処理は CPU バウンドです。OCR エンジンはピクセルデータを解析する一連の画像分析アルゴリズムを実行します。10 枚、20 枚、あるいは 100 枚の画像がある場合、総実行時間は基本的に各個別実行時間の合計になります。  

各ファイルごとにスレッドを生成することで、OS にこれらの CPU 集中型ジョブを同時にスケジュールさせます。マルチコアマシンでは、実行時間が半分、場合によっては 4 分の 1 にまで短縮されることがあります。トレードオフとしてメモリ使用量がやや増加しますが、ほとんどのバッチジョブでは速度向上の価値があります。

> **Pro tip:** 画像が数百メガバイトに及ぶ場合は、`threading` の代わりに `concurrent.futures.ProcessPoolExecutor` の使用を検討してください。プロセスは GIL に束縛された CPython インタプリタ上で真の並列性を提供しますが、若干のオーバーヘッドが増えます。

## ステップ 1: Aspose OCR for Python をインストール

まずは OCR ライブラリをシステムにインストールしましょう。

```bash
pip install aspose-ocr
```

この1行で最新の Aspose OCR バイナリと Python バインディングが取得されます。権限エラーが出た場合は `--user` を付けるか、仮想環境を使用してみてください。

## ステップ 2: OCR 用に画像をロード – ワーカ関数

ここでは、各スレッドで実行されるコアルーチンを定義します。**loads image for OCR** を行い、認識を実行し、抽出されたテキストのプレビューを出力します。

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

注意すべき点は以下です：

- **Why a new `OcrEngine` per thread?** エンジンは内部バッファを保持しているため、インスタンスを共有すると競合状態や文字化けが発生します。  
- **Why strip newlines?** コンソールにログ出力する際に行を整えるためです。  
- **Error handling?** 本番環境では本体を `try/except` で囲み、ファイルにログを取るなどの処理を行います—これは後ほど説明します。

## ステップ 3: 処理したい PNG ファイルをリスト化

リストをハードコードすることもできますが、より柔軟なのはディレクトリをスキャンする方法です。以下では分かりやすさのために手動で 3 ファイルを列挙しています。パスはご自身のフォルダーに合わせて置き換えてください。

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

自動検出を好む場合は次のようにします：

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

この小さな調整により、毎回ソースコードを変更せずに **extract text from PNG** ファイルを一括で抽出できます。

## ステップ 4: ocr multiple files と batch OCR images を設定

ここでは各画像ごとにスレッドを作成します。これが **batch OCR images** パターンの核心です。

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

リスト内包表記によりコードが簡潔になり、各 `Thread` オブジェクトはターゲット関数とその引数（`image_path`）を保持します。  

> **Side note:** Python の `threading` モジュールはネイティブ OS スレッドを使用するため、4 コアのラップトップでは通常最大で 4 つのスレッドが同時に実行され、残りはコアが空くたびにスケジュールされます。

## ステップ 5: 並列画像認識を実行

ワーカーの起動はシンプルです。リストをイテレートして `start()` を呼び出し、その後 `join()` で全スレッドの完了を待ちます。

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

スクリプトが終了すると、次のような行が表示されます：

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

この出力は各 PNG が処理されたことを示し、抽出されたテキストはさらに処理（例：データベースへの保存や NLP パイプラインへの入力）に利用できます。

## ステップ 6: 結果を検証し、エッジケースに対処

### 空結果のチェック

画像がノイズが多すぎる、または OCR エンジンが文字を検出できないことがあります。簡単なサニティチェックを行うことで、下流のエラーを防げます。

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### 同時スレッド数の制限

小規模な VM で実行する場合、数百のスレッドを生成するとスケジューラが圧倒される可能性があります。セマフォで同時実行数を上限設定できます：

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### 結果をファイルに保存

出力をコンソールに表示する代わりに、ファイル名と抽出テキストを含む CSV が欲しいかもしれません：

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

レースコンディションを防ぐため、スレッド関数の外側で CSV を **一度だけ** 開き、`csv` モジュールの writer はシンプルな書き込みに対してスレッドセーフであることを確認してください。

## 完全な動作例

すべてをまとめると、`batch_ocr.py` というファイルに貼り付けて実行できる単一スクリプトは以下の通りです：

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}