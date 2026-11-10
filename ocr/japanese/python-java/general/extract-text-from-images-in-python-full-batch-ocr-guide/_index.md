---
category: general
date: 2026-06-19
description: シンプルなOCRエンジンを使ってPythonで画像からテキストを抽出します。スキャンした画像をテキストに変換する方法、画像からテキストを認識する方法、そしてPythonで画像ファイルを効率的に一覧表示する方法を学びましょう。
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: ja
og_description: 軽量なOCRエンジンを使用して、Pythonで画像からテキストを抽出します。このガイドでは、スキャンした画像をテキストに変換し、画像からテキストを認識し、Pythonで画像ファイルを一覧表示する方法を数ステップで紹介します。
og_title: Pythonで画像からテキストを抽出する – 完全バッチOCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Pythonで画像からテキストを抽出する – 完全バッチOCRガイド
url: /ja/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像からテキストを抽出 – 完全バッチOCRガイド

画像から**テキストを抽出**したいけど、どこから始めればいいか分からないことはありませんか？開発者はスキャンしたPDF、撮影したレシート、スクリーンショットなどを検索可能なテキストに変換する課題に日々直面しています。このチュートリアルでは、**スキャン画像をテキストに変換**し、画像からテキストを認識し、さらに**list image files python**スタイルで画像ファイルを列挙する、実行可能な完全なサンプルを順を追って解説します。最後まで読めば、フォルダ全体を一括で処理できる再利用可能なスクリプトが手に入ります。

必要なライブラリ、各ステップの重要性、エッジケースの扱い、トラブルシューティングまで網羅しています。外部ドキュメントを追いかける必要はありません。以下のコードは自己完結しており、解説は「どうやって」だけでなく「なぜ」も説明しています。お気に入りのIDEを開いて、さっそく始めましょう。

---

## 作成するもの

- OCRエンジンを初期化する（例として `ocr` パッケージを使用）。
- ディレクトリを走査し、**list image files python**スタイルで PNG、JPG、TIFF をフィルタリングして列挙。
- 見つかったすべての画像に対して**バッチ OCR**を実行。
- 各ファイルの抽出テキストを明示的にラベル付けして出力。

> **プロのコツ:** `ocr` ライブラリがインストールされていない場合は、`pytesseract` に差し替えてもほぼ同じロジックで動作します。

---

## 前提条件

- Python 3.8+（スクリプトは f‑string と型ヒントを使用）。
- `OcrEngine` と `recognize_batch` を提供する OCR ライブラリ。ここでは架空の `ocr` パッケージを例にしていますが、実際のライブラリでも同様のパターンが使えます。
- 処理したい画像ファイルが入っているフォルダ（`.png`、`.jpg`、`.tif`）。

---

## Step 1 – 必要なモジュールのインストールとインポート

まず、OCR パッケージが利用可能か確認してください。実際のライブラリ（例: `pytesseract`）を使う場合はインポート文を置き換えます。

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **重要性:** `os` をインポートするとクロスプラットフォームのパス操作が可能になり、`typing.List` は IDE の補完や将来の拡張性に役立ちます。

---

## Step 2 – **Extract Text from Images**: OCR エンジンの初期化

エンジンを作成することが OCR 作業の第一歩です。言語は自動検出に設定し、混在言語の文書にも対応できるようにします。

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **解説:** エンジン生成を関数に切り出すことでコードをモジュール化しています。後で DPI や OCR モードを変更したい場合は、この関数だけを修正すれば済みます。

---

## Step 3 – **List Image Files Python**: ディレクトリからファイルを取得

次に、処理対象となるすべての画像を見つける必要があります。以下のリスト内包表記は一般的な **list image files python** パターンを模倣しています。

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **エッジケース処理:** この関数はサブフォルダを無視します（必要なら再帰処理を追加可能）し、隠しファイルは自動的に除外されます。隠しファイルは通常、サポート対象の拡張子で終わらないためです。

---

## Step 4 – **Convert Scanned Images to Text**: バッチ OCR の実行

多くの OCR ライブラリはバッチメソッドを提供しており、1枚ずつ処理するよりもはるかに高速です。以下が呼び出し例です。

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **なぜバッチ処理か？** すべての画像を一度に送ることで、OCR モデルのロードオーバーヘッドが削減され、CPU/GPU の利用効率が向上します。

---

## Step 5 – **Recognize Text from Pictures**: 結果の表示

最後に、ファイル名と OCR 結果をペアにしてイテレートし、各画像ごとに見やすいヘッダーを出力します。

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **ヒント:** `strip()` は OCR が付与しがちな前後の空白を除去します。

---

## 完全スクリプト – すべてをまとめる

以下が実行可能な完全プログラムです。`batch_ocr.py` として保存し、`python batch_ocr.py <your_folder>` で実行してください。

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### 期待される出力

フォルダに `invoice1.png` と `receipt.jpg` があると仮定すると、次のような出力が得られます。

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

各ブロックは明確にラベル付けされているため、データベースへの保存など、下流処理がシンプルになります。

---

## よくある落とし穴の対処法

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **No text appears** | OCR の言語が検出されない、または画像のコントラストが低すぎる。 | 言語を強制指定（`engine.language = ocr.Language.English`）するか、画像のコントラストを上げて前処理する。 |
| **Memory error on large batches** | エンジンがすべての画像を一度に読み込もうとする。 | `image_files` をチャンクに分割（例: `batch_size = 20`）し、`recognize_batch` を複数回呼び出す。 |
| **Unsupported file format** | `.gif` や `.bmp` を追加した。 | `supported_exts` タプルに拡張子を追加するか、事前に PNG/JPG に変換する。 |
| **Unicode garbling** | OCR がバイト列を返している。 | OCR ライブラリが Unicode を出力するように設定（必要なら `result.text.decode('utf‑8')`）する。 |

---

## ワークフローの拡張

**画像からテキストを抽出**できたので、次のステップを検討してください。

- **CSV へのエクスポート** – ファイル名と抽出テキストをスプレッドシートに書き出し、分析に活用。
- **並列処理** – `concurrent.futures.ThreadPoolExecutor` を使って複数バッチを同時に処理。
- **クラウド OCR との統合** – ローカルエンジンを Google Vision や Azure OCR に置き換えて、複雑なレイアウトでも高精度に。
- **画像前処理の追加** – Pillow や OpenCV で画像の傾き補正、ノイズ除去、二値化を行い、OCR 精度を向上。

これらのアイデアはすべて、ここで構築したコア関数をそのまま利用できるため、ゼロから始める必要はありません。

---

## 結論

Python で **画像からテキストを抽出**するための完全なソリューションを一通り解説しました。**list image files python** から **recognize text from pictures**、そして **convert scanned images to text** までをバッチ処理で実装し、シンプルながら拡張性の高いスクリプトが完成しました。領収書のデジタル化、検索可能なアーカイブ構築、データ抽出パイプラインの構築など、さまざまなプロジェクトの土台として活用できます。

ぜひ実行してみて、前処理を調整しながら OCR 精度の向上を体感してください。問題が発生したら「よくある落とし穴」表を参照すれば、ほとんどのケースは小さな設定変更で解決できます。

次のチャレンジはどうですか？`pdf2image` を使って PDF を画像に変換し、同じパイプラインに流し込んでみましょう。OCR と Python の豊富なエコシステムを組み合わせれば、可能性は無限です。

Happy coding, and may your text be ever legible!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}