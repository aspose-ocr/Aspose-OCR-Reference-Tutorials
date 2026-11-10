---
category: general
date: 2026-03-28
description: Aspose OCR Cloud を使用した Python OCR チュートリアルです。Python で画像からテキストを抽出する方法を示します。OCR
  用に画像を読み込み、数分で画像をプレーンテキストに変換する方法を学びましょう。
draft: false
keywords:
- python ocr tutorial
- extract text image python
- ocr image to text
- load image for ocr
- convert image plain text
language: ja
og_description: Python OCRチュートリアルでは、OCR用に画像を読み込む方法と、Aspose OCR Cloudを使用して画像のプレーンテキストに変換する方法を解説しています。完全なコードとヒントを入手してください。
og_title: Python OCRチュートリアル – 画像からテキストを抽出する
tags:
- OCR
- Python
- Image Processing
title: Python OCRチュートリアル – 画像からテキストを抽出
url: /ja/python/general/python-ocr-tutorial-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR チュートリアル – 画像からテキストを抽出する

散らかった領収書の写真をきれいで検索可能なテキストに変換したいと思ったことはありませんか？ あなただけではありません。私の経験では、最大の障壁は OCR エンジン自体ではなく、画像を正しい形式に変換し、問題なくプレーンテキストを取り出すことです。

この **python ocr tutorial** では、OCR 用に画像をロードし、認識を実行し、最終的に画像のプレーンテキストを Python の文字列に変換して保存や分析ができるようになるまでのすべての手順を案内します。最後まで読めば、**extract text image python** スタイルでテキストを抽出でき、開始するために有料ライセンスは不要です。

## 学べること

- Aspose OCR Cloud SDK for Python のインストールとインポート方法。  
- **load image for OCR** 用の正確なコード（PNG、JPEG、TIFF、PDF など）。  
- **ocr image to text** 変換を実行するエンジンの呼び出し方。  
- マルチページ PDF や低解像度スキャンなど、一般的なエッジケースへの対処法。  
- 出力を検証する方法と、テキストが乱れた場合の対処法。

### 前提条件

- Python 3.8+ がマシンにインストールされていること。  
- 無料の Aspose Cloud アカウント（トライアルはライセンス不要で動作）。  
- pip と仮想環境の基本的な知識—特別なことは不要です。

> **Pro tip:** すでに virtualenv を使用している場合は、今すぐ有効化してください。依存関係が整理され、バージョン衝突を防げます。

![Python OCR チュートリアルのスクリーンショット（認識されたテキストが表示）](path/to/ocr_example.png "Python OCR チュートリアル – 抽出されたプレーンテキスト表示")

## Step 1 – Install the Aspose OCR Cloud SDK

まず最初に、Aspose の OCR サービスと通信するライブラリが必要です。ターミナルを開いて次のコマンドを実行してください。

```bash
pip install asposeocrcloud
```

この単一コマンドで最新の SDK（現在のバージョンは 23.12）を取得できます。パッケージには必要なものがすべて含まれており、追加の画像処理ライブラリは不要です。

## Step 2 – Initialise the OCR Engine (Primary Keyword in Action)

SDK の準備ができたので、**python ocr tutorial** エンジンを起動できます。トライアル版ではライセンスキーは不要なので、シンプルに開始できます。

```python
import asposeocrcloud as ocr

# Initialise the OCR engine – no licence needed for trial use
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** エンジンを一度だけ初期化すれば、以降の呼び出しが高速になります。画像ごとにオブジェクトを再作成すると、ネットワーク往復が無駄になります。

## Step 3 – Load Image for OCR

ここで **load image for OCR** キーワードが活躍します。SDK の `Image.load` メソッドはファイルパスまたは URL を受け取り、形式（PNG、JPEG、TIFF、PDF など）を自動的に検出します。サンプルの領収書をロードしてみましょう。

```python
# Step 3: Load the input image (PNG, JPEG, TIFF, PDF …)
input_image = ocr.Image.load(r"YOUR_DIRECTORY/receipt.png")
```

マルチページ PDF を扱う場合は、PDF ファイルを指定するだけで、SDK が内部的に各ページを個別の画像として処理します。

## Step 4 – Perform OCR Image to Text Conversion

画像がメモリ上にある状態で、実際の OCR はワンラインで完了します。`recognize` メソッドはプレーンテキスト、信頼度スコア、必要に応じてバウンディングボックスを含む `OcrResult` オブジェクトを返します。

```python
# Step 4: Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)
```

> **Edge case:** 300 dpi 未満の低解像度画像の場合は、先に画像を拡大した方が良いかもしれません。SDK には `Resize` ヘルパーがありますが、ほとんどの領収書ではデフォルトで問題ありません。

## Step 5 – Convert Image Plain Text to a Usable String

最後のピースは、結果オブジェクトからプレーンテキストを抽出することです。これが **convert image plain text** ステップで、OCR のバイナリデータを印刷・保存・他システムへの入力に使える文字列に変換します。

```python
# Step 5: Output the recognised plain text
print("Plain OCR:")
print(ocr_result.text)
```

スクリプトを実行すると、次のような出力が得られるはずです。

```
Plain OCR:
Starbucks Coffee
Date: 2026/03/27
Total: $4.75
Thank you!
```

この出力は通常の Python 文字列となり、CSV エクスポート、データベースへの挿入、自然言語処理などにすぐ利用できます。

## Handling Common Pitfalls

### 1. Blank or Noisy Images

`ocr_result.text` が空の場合は、画像品質を再確認してください。簡単な対策として前処理ステップを追加できます。

```python
# Simple preprocessing – convert to grayscale and increase contrast
processed = input_image.to_grayscale().adjust_contrast(1.2)
ocr_result = ocr_engine.recognize(processed)
```

### 2. Multi‑Page PDFs

PDF を入力すると、`recognize` は各ページごとの結果を返します。以下のようにループ処理してください。

```python
pdf_image = ocr.Image.load("document.pdf")
pages = pdf_image.pages  # collection of page images

for i, page in enumerate(pages, start=1):
    result = ocr_engine.recognize(page)
    print(f"--- Page {i} ---")
    print(result.text)
```

### 3. Language Support

Aspose OCR は 60 以上の言語に対応しています。言語を切り替えるには、`recognize` を呼び出す前に `language` プロパティを設定します。

```python
ocr_engine.language = "fr"  # French
ocr_result = ocr_engine.recognize(input_image)
```

## Full Working Example

すべてをまとめた、インストールからエッジケース処理まで網羅したコピー＆ペースト可能な完全スクリプトをご紹介します。

```python
# -*- coding: utf-8 -*-
"""
Python OCR tutorial – complete example using Aspose OCR Cloud.
Demonstrates loading an image, performing OCR, and handling multi‑page PDFs.
"""

import asposeocrcloud as ocr
import os

def ocr_file(filepath: str, language: str = "en"):
    """
    Perform OCR on a given file (image or PDF) and return plain text.
    """
    # Initialise engine (trial licence)
    engine = ocr.OcrEngine()
    engine.language = language

    # Load the file – SDK auto‑detects format
    image = ocr.Image.load(filepath)

    # If it's a PDF, iterate over pages
    if image.is_pdf:
        all_text = []
        for page in image.pages:
            result = engine.recognize(page)
            all_text.append(result.text)
        return "\n".join(all_text)

    # Single‑image case
    result = engine.recognize(image)
    return result.text


if __name__ == "__main__":
    # Example usage – replace with your own path
    sample_path = os.path.join("YOUR_DIRECTORY", "receipt.png")

    if not os.path.exists(sample_path):
        raise FileNotFoundError(f"File not found: {sample_path}")

    extracted = ocr_file(sample_path)
    print("=== Extracted Text ===")
    print(extracted)
```

スクリプトを実行します（`python ocr_demo.py`）と、コンソールに **ocr image to text** の出力が表示されます。

## Recap – What We Covered

- **Aspose OCR Cloud** SDK をインストール（`pip install asposeocrcloud`）。  
- ライセンス不要で **Initialised the OCR engine**（トライアルに最適）。  
- PNG、JPEG、PDF など、**load image for OCR** の方法を実演。  
- **ocr image to text** 変換と **converted image plain text** を実行し、使える Python 文字列に変換。  
- 低解像度スキャン、マルチページ PDF、言語選択といった一般的な落とし穴に対処。

## Next Steps & Related Topics

**python ocr tutorial** をマスターした今、次のテーマを検討してみてください。

- 大量の領収書フォルダーをバッチ処理する **Extract text image python**。  
- OCR 出力を **pandas** と組み合わせてデータ分析に活用（`df = pd.read_csv(StringIO(extracted))`）。  
- インターネット接続が不安定な場合の代替手段として **Tesseract OCR** を使用。  
- **spaCy** で事後処理し、日付、金額、店舗名などのエンティティを抽出。

自由に実験してください：異なる画像形式を試す、コントラストを調整する、言語を切り替えるなど。OCR の領域は広く、今回習得したスキルはあらゆる文書自動化プロジェクトの堅実な基盤となります。

Happy coding, and may your text always be readable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}