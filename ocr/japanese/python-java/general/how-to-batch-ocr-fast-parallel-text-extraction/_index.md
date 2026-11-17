---
category: general
date: 2026-03-26
description: Python を使って効率的に OCR をバッチ処理する方法 — 画像や PDF からテキストを抽出し、並列処理で OCR 変換を学ぶ。
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: ja
og_description: 効率的にバッチ OCR を行う方法—画像からテキストを抽出し、PDF の OCR 変換と Python を使用したバッチ OCR 処理のステップバイステップガイド
og_title: バッチOCRの方法：高速並列テキスト抽出
tags:
- OCR
- Python
- Parallel Computing
title: バッチOCRの方法：高速並列テキスト抽出
url: /ja/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# バッチ OCR の方法：高速並列テキスト抽出

スキャンしたページやスクリーンショット、PDF が何十枚もあるときに、**バッチ OCR のやり方**を考えたことはありませんか？ あなただけではありません—多くの開発者が同じ壁にぶつかります。ファイルを1つずつ処理するのは痛いほどのボトルネックになります。

良いニュースは、少数のワーカースレッドを立ち上げ、すべてのファイルを投入すれば、OCR エンジンがバッチを並列に処理してくれることです。このチュートリアルでは、**画像からテキストを抽出**し、**PDF OCR 変換**を実行し、**並列 OCR 処理**を活用して高速化する、完全な実行可能サンプルを順に解説します。

> **得られるもの**  
> * PNG、TIFF、PDF、JPG ファイルの混在リストを一括で処理する、完全に機能する Python スクリプト。  
> * スレッドプールが I/O バウンドの OCR タスクを高速化する理由の理解。  
> * エラー処理、大きな PDF、カスタムスレッド数に関するヒント。  

## 前提条件

本題に入る前に、以下が揃っていることを確認してください。

| 要件 | 理由 |
|------|------|
| Python 3.8+ | モダンな構文と `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | `OcrBatchProcessor` と結果オブジェクトを提供 |
| サンプルファイル（PNG、TIFF、PDF、JPG）数点 | **画像からテキストを抽出** の動作を見るため |
| スレッドの基本的な知識（任意） | 役立ちますが必須ではありません |

まだ `ocr` パッケージをインストールしていない場合は、次を実行してください：

```bash
pip install ocr-lib   # replace with the actual package name
```

環境が整ったので、問題を分解してみましょう。

## ステップ 1: ヘルパーをインポートし、バッチプロセッサをインスタンス化

最初に必要なのは、すべての OCR ジョブを収集する場所です。`OcrBatchProcessor` クラスはまさにそれを行い、作業項目をキューに入れ、`Future` オブジェクトのリストを返します。

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: `as_completed` をインポートすることで、最も遅いファイルを待つことなく、完了したジョブにすぐに反応できます。これは **バッチ OCR 処理** の核心です。

## ステップ 2: 並列実行のためにワーカープールを調整

デフォルトではプロセッサは単一スレッドを使用するため、バッチ化の目的が失われます。ここでは明示的に 4 つのワーカーを指定します—CPU コア数に合わせてこの数を増やしても構いません。

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: OCR のような I/O バウンドタスクでは、`CPU cores * 2` を超えると効果が薄れがちです。いくつかの値をテストして最適なポイントを見つけてください。

## ステップ 3: OCR したいすべてのファイルをキューに入れる

ここでは画像と PDF ファイルの混在セットを追加します。`add` メソッドは単にパスを記録するだけで、実際の処理はバッチを送信するまで開始されません。

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

フォルダー全体を処理したい場合は、簡単な `glob` ループで対応できます：

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## ステップ 4: ジョブを起動し、Future を収集

`submit_all` を呼び出すと、プロセッサに実行許可が出ます。`Future` オブジェクトのリストが返されます—これは後で結果が入るプレースホルダーと考えてください。

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

この時点で OCR エンジンはバックグラウンドで動作し、各スレッドがファイルを処理しています。

## ステップ 5: 完了したらすぐに結果を取得

`as_completed` を使用すると、送信順ではなく完了順に Future を反復処理できます。これにより、特に PDF がシンプルな PNG よりも長くかかる場合でも、スクリプトの応答性が保たれます。

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**期待される出力**（簡略化）:

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

各ブロックは元ファイルのプレーンテキスト表現に対応しています。**PDF OCR 変換** を行う場合、テキストには OCR エンジンが各ページから解読できたすべてが含まれます。

## エッジケースと一般的な落とし穴の対処

| 状況 | 注意点 | 簡易対策 |
|------|--------|----------|
| 破損した画像 | `future.result()` が `OSError` を送出 | `try/except` でラップ (上記コード参照) |
| 非常に大きな PDF（> 100 MB） | メモリ圧迫、スレッドが遅くなる | `thread_count` を適度に増やすか、まず PDF を章ごとに分割 |
| 混在言語の文書 | デフォルトの OCR モデルが誤検出する可能性 | ライブラリがサポートしていれば、`OcrBatchProcessor` に言語ヒントを渡す |
| レイアウトを保持する必要がある | プレーンな `get_text()` では列が失われる | `ocr_result.get_hocr()` など、レイアウト対応のメソッドを使用 |

### プロチップ: ファイルタイプに基づくカスタムスレッド数

作業の大半が PDF であることが分かっている場合、PDF 用に多めのスレッドを割り当て、tiny PNG には少なめに割り当てることができます。いくつかのライブラリではジョブごとに `priority` を渡すことができます；それができない場合は、画像用と PDF 用の 2 つのバッチを作成し、同時に実行できます。

## ビジュアル概要（オプション）

![バッチ OCR ワークフローダイアグラム](https://example.com/ocr-workflow.png "バッチ OCR ワークフロー")

*この図は、ファイル検出 → バッチ作成 → 並列実行 → 結果集約のフローを示しています。*

## コピー＆ペースト可能な完全スクリプト

以下は `.py` ファイルにそのまま貼り付けられる完全なプログラムです。上記のすべてのスニペットに加えて、ディレクトリ内の対応ファイルを自動的に検出する小さなヘルパーが含まれています。

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

`batch_ocr.py` として保存し、スキャン画像が入ったフォルダーを指定すると、コンソールに抽出テキストが次々と表示されます。  

### なぜこれが機能するのか

* **Thread pool** – OCR は主にディスク I/O と外部エンジン呼び出しを待つため、複数のスレッドで CPU を有効活用できます。  
* **`as_completed`** – 結果が準備でき次第取得できるため、UI フィードバックやストリーミングパイプラインに最適です。  
* **Error isolation** – 1 つの不良ファイルがバッチ全体を失敗させることはなく、`try/except` ブロックで失敗を分離します。  

## 結論

要するに、Python の `concurrent.futures` とバッチ処理をサポートする OCR ライブラリを組み合わせて **バッチ OCR のやり方** が分かりました。適度なスレッドプールを設定し、すべての対応ファイルをキューに入れ、完了したら結果を取得することで、信頼性を損なうことなく高速な **並列 OCR 処理** を実現できます。  

ここからは次のようなことが可能です：

* 出力を検索インデックスにフックして、ドキュメントを素早く検索できるようにする。  
* スクリプトを拡張し、各結果を元ファイルと同じ場所に `.txt` ファイルとして書き出す。  
* OCR ライブラリが非同期 API を提供している場合、組み込みのスレッドプールを `asyncio` に置き換える。  

実験を続けてください—Tesseract、Azure Cognitive Services、Google Vision などに入れ替えても同じパターンが適用できるはずです。OCR を楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}