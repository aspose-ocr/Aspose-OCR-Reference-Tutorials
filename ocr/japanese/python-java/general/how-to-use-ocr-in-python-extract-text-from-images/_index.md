---
category: general
date: 2026-06-16
description: PythonでOCRを使用してPNGなどの画像ファイルからテキストを抽出する方法。Aspose OCRを使った画像からテキストへのステップバイステップ変換を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: ja
og_description: PythonでOCRを使用して画像からテキストを抽出する方法。このガイドでは、Aspose OCRを使ってPNGファイルを検索可能なテキストに変換する手順を案内します。
og_title: PythonでOCRを使用する方法 – 画像からテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: PythonでOCRを使用する方法 – 画像からテキストを抽出する
url: /ja/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを使用する方法 – 画像からテキストを抽出する

Pythonプロジェクトで**OCRの使い方**を疑問に思ったことはありませんか？ あなただけではありません。レシートスキャナーや文書アーカイバーを作る場合でも、スクリーンショットを編集可能なテキストに変換したいだけの場合でも、**画像からテキストを抽出**する機能は画期的です。

このチュートリアルでは、Aspose OCRライブラリのインストールからPNGファイルからテキストを読み取るまでの全工程を解説します。数行のコードで**画像をテキストに変換**できるようになります。最後まで読むと、**PNGからテキストを読み取る**方法や、マルチ言語コンテンツを自動的に処理する方法が正確に分かります。

> **Pro tip:** Aspose OCRの自動言語検出により、事前に言語を推測する必要がなくなります—旅行アプリに最適です。

## 必要なもの

- Python 3.8+（最新の安定版で問題ありません）
- Aspose OCRの有効なライセンスファイル（`Aspose.OCR.lic`）。無料トライアルはテストに使用できますが、正式なライセンスを取得すれば評価制限が解除されます。
- `pip`でインストールしたAspose OCRパッケージ：

```bash
pip install aspose-ocr
```

- 処理したい画像ファイル—デモとして`sample-multi-lang.png`を使用します。

これらの前提条件を揃えておくことで、作業がスムーズに進み、後で「module not found」のエラーが出ることを防げます。

![PythonでOCRを使用するワークフロー](https://example.com/ocr-workflow.png "PythonでOCRを使用する方法 – ステップバイステップのイラスト")

*画像の代替テキスト: PythonでOCRを使用して画像からテキストを抽出する方法を示す図。*

## ステップ 1: Aspose OCR ライセンスを適用する（アプリケーションごとに一度だけ必要）

本格的なOCRプロジェクトが最初に行うことはライセンスをロードすることです。これがないと、Asposeは警告を出し、処理できるページ数に制限がかかります。

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Why this matters:** ライセンスを事前にロードすることで、**ocr image to text python** エンジンが最大速度でウォーターマークなしで動作します。変換を開始する前にプレミアム機能のロックを解除するイメージです。

## ステップ 2: OCRエンジンを作成し、自動言語検出を有効にする

ここでコアエンジンのインスタンスを作成します。画像に英語、スペイン語、中国語、またはそれらの混在が含まれるか分からない場合、`language_auto_detect` を有効にすることが重要です。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

もし事前に言語が分かっている場合は、`ocr_engine.language = "English"`（またはサポートされているISOコード）を設定すれば少し高速化できます。しかし、汎用的な「PNGからテキストを読み取る」ユーティリティでは、自動検出が最も安全です。

## ステップ 3: 処理したい画像をロードする

Aspose OCRはPNG、JPEG、BMP、TIFFなどさまざまな形式に対応しています。ここでは複数言語を含むPNGファイルをロードしてみましょう。

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Edge case:** 画像が非常に大きい（数メガバイト以上）場合、パフォーマンス向上のためにまず縮小した方が良いかもしれません。そのためにAsposeは `ocr_image.resize(width, height)` を提供しています。

## ステップ 4: OCR認識を実行する

すべてが設定されたら、実際のテキスト抽出は1つのメソッド呼び出しで行えます。結果オブジェクトは認識されたテキストと検出された言語の両方を提供します。

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

内部では、Asposeは高度なニューラルネットワークとパターンマッチングアルゴリズムを使用して各ピクセルクラスタを文字に変換します。重い処理はすべてネイティブコードで行われるため、低スペックのハードウェアでも**高速で正確なOCR**が得られます。

## ステップ 5: 検出された言語と認識されたテキストを表示する

最後に、取得した結果を出力しましょう。`detected_language` プロパティはAsposeが推測した言語を示し、`text` には全文が含まれます。

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### 期待される出力

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

英語と日本語の両方を含む画像でスクリプトを実行すると、言語が自動的に切り替わるのが確認できます—先ほど有効にした自動検出機能のおかげです。

## よくある落とし穴の対処法

### 1. ライセンスが見つからない

`License file not found` のようなエラーが出た場合、`set_license` に渡したパスを再確認してください。Windowsでのエスケープ文字の問題を防ぐために、生文字列（`r"...`）を使用すると便利です。

### 2. 空の出力

`ocr_result.text` が空になるのは、画像がノイズが多すぎるかテキストが薄すぎることが原因です。画像のコントラストを上げてみてください：

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. 言語検出が間違っている

自動検出が誤った言語を選んだ場合、特定の言語を強制できます：

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## 例の拡張: 複数のPNGファイルをバッチ処理する

フォルダー全体の画像を**画像をテキストに変換**したいことが多く、単一ファイルだけでなくバッチ処理が必要です。以下はディレクトリ内のすべてのPNGを処理する簡単なループです：

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

このスニペットは、ドキュメントデジタル化パイプラインでよくある大量の**画像からテキストを抽出**する実用的な方法を示しています。

## 完全な動作スクリプト

すべてをまとめると、以下の単一ファイルをエンドツーエンドで実行できます：

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

`ocr_demo.py` として保存し、`python ocr_demo.py` を実行すると、コンソールに言語とテキストが表示されます。

## 結論

Pythonで**OCRの使い方**を最初から最後まで解説し、**画像からテキストを抽出**し、**PNGからテキストを読み取る**、そして一般的にAsposeの強力なエンジンを使って**画像をテキストに変換**する方法を示しました。ライセンスをロードし、自動言語検出を有効にし、画像を `OcrEngine` に渡すだけで、数秒でクリーンで検索可能なテキストが得られます。

次は何をすべきでしょうか？ AsposeをTesseractなどのオープンソース代替に置き換えて精度を比較したり、PDF入力を試したり、OCRステップをFlask APIに統合してリアルタイム画像処理を実装したりしてみてください。**ocr image to text python** の基本をマスターすれば、可能性は無限です。

フォントの扱い、パフォーマンスのスケーリング、ライセンスに関する質問があれば、下にコメントを残してください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に基づく関連トピックをカバーしています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCRで画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキストを抽出 – Aspose.OCR for .NETによるOCR最適化](/ocr/english/net/ocr-optimization/)
- [Aspose.OCRを使用した言語選択付き画像テキスト抽出（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}