---
category: general
date: 2026-01-12
description: OCR を迅速かつ正確に実行する方法。ドキュメントで OCR を実行し、TIFF からテキストを抽出し、OCR 用に画像を読み込み、Python
  で OCR 言語を設定する方法を学びます。
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: ja
og_description: PythonでOCRを実行する方法。このチュートリアルでは、ドキュメントでOCRを実行し、TIFFからテキストを抽出し、OCR用に画像を読み込み、OCR言語を設定する方法を示します。
og_title: TIFFドキュメントでOCRを実行する方法 – 完全ガイド
tags:
- OCR
- Python
- Image Processing
title: TIFFドキュメントでOCRを実行する方法 – ステップバイステップガイド
url: /ja/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFFドキュメントでOCRを実行する方法 – 完全ガイド

スキャンしたTIFFファイルで **OCRを実行する方法** を、適切なライブラリを探すのに何時間も費やさずに知りたくありませんか？ あなたは一人ではありません。特にパフォーマンスや言語設定が重要になるとき、TIFF画像からテキストを抽出しようとして壁にぶつかる開発者は多いです。

このチュートリアルでは、OCRパッケージのインストール、画像のロード、OCR言語の設定、最終的に **ドキュメント上でOCRを実行** してクリーンなテキストを取得するまでのすべての手順を解説します。最後まで読めば、任意のプロジェクトにすぐ組み込める実行可能なスクリプトが手に入ります。

> **プロのコツ:** 例では汎用的な `ocr` モジュールを使用していますが、同じ概念は Tesseract、EasyOCR、または Python API を提供する最新の OCR エンジンすべてに当てはまります。

---

## 必要なもの

- Python 3.8+（最近のバージョンならどれでも可）
- `OcrEngine` クラスを提供する OCR ライブラリ（サンプルでは架空の `ocr` パッケージを使用しています。実際に使用するものに置き換えてください）
- 処理したいマルチページ TIFF ファイル（ここでは `big_document.tif` と呼びます）
- スレッド数を設定する場合は、少なくとも 4 コアを持つマシン

外部サービスやクラウドキーは不要です。ローカルで数秒で動作するコードだけです。

---

![TIFFドキュメントでOCRを実行する例](/images/ocr-example.png "TIFFドキュメントでOCRを実行する方法")

*画像代替テキスト: TIFFドキュメントでOCRを実行する例 – 抽出されたテキストのプレビュー。*

---

## Step 1: OCR ライブラリのインストールとインポート

まず最初に、ライブラリをマシンにインストールします。ほとんどの OCR パッケージは PyPI にあるので、シンプルな `pip install` で完了します。

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

次に必要なクラスをインポートします。Tesseract を使用する場合はインポート行が異なりますが、残りのコードは同じです。

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*なぜ重要か:* 正しいシンボルを早めにインポートしておくことで、後で名前空間の衝突を防ぎ、スクリプトの可読性が向上します。

---

## Step 2: OCR エンジンの作成と設定（OCR 言語の設定）

エンジンの設定は **OCR 言語を設定** して正確な認識を行うポイントです。デフォルトは英語ですが、1 行でフランス語、ドイツ語、あるいは多言語モードに切り替えられます。

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **なぜ 4 スレッドか？** 現代のノートパソコンは少なくとも 4 コアを搭載していることが多く、スレッド数を制限することで OCR プロセスがマシン全体を占有するのを防げます。特に共有サーバー上でスクリプトを実行する場合に有用です。

別の言語が必要な場合は、`ocr.Language.ENGLISH` を `ocr.Language.FRENCH`、`ocr.Language.SPANISH` などに置き換えるだけです。

---

## Step 3: OCR 用画像のロード（Load Image for OCR）

ここで **OCR 用画像をロード** します。`Image.load` メソッドは TIFF ファイルをメモリに読み込み、マルチページドキュメントを自動的に処理します。

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*エッジケース:* ファイルが非常に大きい場合、RAM が不足することがあります。その場合は、`Image.load_page(page_number)`（ライブラリがサポートしていれば）でページごとにロードすることを検討してください。

---

## Step 4: ドキュメント上で OCR を実行

エンジンが準備でき、画像がロードされたら、いよいよ **ドキュメント上で OCR を実行** します。`process` メソッドが重い処理を行い、結果オブジェクトを返します。

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

内部ではエンジンが画像をテキストブロックに分割し、認識モデルを走らせ、結果を結合しています。呼び出しはブロッキングで、スクリプトは TIFF 全体が処理されるまで待機します——バッチジョブに最適です。

---

## Step 5: TIFF からテキストを抽出し出力を検証

最後に、結果オブジェクトの `text` 属性にアクセスして **TIFF からテキストを抽出** します。簡易的なサニティチェックとして最初の 200 文字を表示してみましょう。

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**期待される出力（例）:**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

全文が必要な場合は単に `ocr_result.text` を使用してください。下流処理のために `.txt` ファイルに書き出すこともできます。

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## 完全動作サンプル

すべてをまとめた、すぐに実行できるスクリプトです。プレースホルダーのパッケージ名は実際にインストールしたものに置き換えてください。

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

スクリプトの実行は次のコマンドで行います。

```bash
python ocr_tiff_example.py
```

コンソールにプレビューが表示され、`extracted_text.txt` という名前のファイルに全文が保存されます。

---

## よくある質問とエッジケース

- **TIFF に複数ページが含まれる場合は？**  
  多くの OCR エンジンは各ページを内部的に別々の画像として扱います。`ocr_result.text` にはページ間に改行が入ります。ページ単位で処理したい場合は `Image.load_page(page_number)` を使って反復処理してください。

- **TIFF の代わりに PNG や JPEG を処理できるか？**  
  もちろん可能です。`Image.load` メソッドは Pillow や基盤ライブラリがサポートするフォーマットならほぼすべて受け付けます。ファイル拡張子を変更するだけで OK です。

- **テキストが文字化けしている——言語設定を変えるべきか？**  
  はい。**OCR 言語の設定** は英語以外の文書にとって重要です。対象言語のパックがインストールされていることを確認してください（例: フランス語なら `tesseract‑lang‑fra`）。

- **メモリが足りなくなる場合は？**  
  `set_memory_limit` を下げるか、ページ単位で処理してください。一部のエンジンは認識前に画像を縮小するオプションも提供しています。

---

## 結論

以上で、Python を使って **TIFF ファイルで OCR を実行する方法** に関する簡潔で実用的なガイドは完了です。ライブラリのインストール、エンジンの設定（**OCR 言語の設定** を含む）、**OCR 用画像のロード**、**ドキュメント上で OCR を実行**、そして最終的に **TIFF からテキストを抽出** までを網羅しました。

ぜひ色々試してみてください：スレッド数を調整したり、言語を切り替えたり、OCR の出力を自然言語処理パイプラインに流し込んだり。基本をマスターすれば、可能性は無限に広がります。

質問があれば下のコメント欄にどうぞ。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}