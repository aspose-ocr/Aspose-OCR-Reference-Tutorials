---
category: general
date: 2026-01-12
description: OCR を高速に実行し、画像をテキストに変換する方法。特殊文字の認識、画像からのテキスト抽出、OCR 用の画像読み込みを、完全な Python
  の例で学びましょう。
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: ja
og_description: PythonでOCRを実行し、画像をテキストに変換し、特殊文字を認識する方法。画像からテキストを抽出する実践的なガイドをご覧ください。
og_title: PythonでOCRを実行する方法 – 完全チュートリアル
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRを実行する方法 – ステップバイステップガイド
url: /ja/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で OCR を実行する方法 – ステップバイステップガイド

スクリーンショットにラテン文字とキリル文字が混在している場合、**OCR を実行**したことがありますか？ あなたは一人ではありません。領収書のデジタル化、多言語文書のインデックス作成、検索可能なアーカイブ構築など、さまざまなプロジェクトで**Python で OCR を実行**する方法はすぐに重要な課題となります。

このチュートリアルでは、**画像をテキストに変換**し、**特殊文字を認識**し、**画像からテキストを抽出**するシンプルな Python ライブラリを使った、実行可能な完全サンプルを順を追って解説します。最後まで読めば、画像を OCR にかけ、多言語コンテンツを処理し、結果を出力するスクリプトがすぐに使えるようになります。

## 必要なもの

本格的に始める前に、以下の前提条件を確認してください。

- Python 3.8 以上がインストールされていること。  
- `ocr` パッケージ（または互換性のある OCR ライブラリ）を `pip install ocr` でインストールしてあること。  
- ラテン文字とキリル文字の両方が含まれる画像ファイル（`multilingual.png`）を用意してあること。  
- 基本的なテキストエディタまたは IDE（VS Code、PyCharm、あるいはシンプルなメモ帳）  

`ocr` パッケージが入手できない場合は、`pytesseract` に置き換えても構いません。その場合は数行の変更だけで済み、基本的な概念は同じです。

## Step 1: OCR ライブラリのインストールとインポート

まずは OCR エンジンを準備します。ライブラリをインポートし、エンジンインスタンスを作成し、多言語サポート用に設定します。

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**ポイント:**  
エンジンを作成することが基礎です。これがないと後で**画像を OCR にかける**ことができません。言語パックを有効にすれば、 “Ŀ”、 “Ҕ”、 “Ǣ” といった文字も正しく認識できます。このステップを省くと、ラテン文字以外が文字化けしてしまいます。

## Step 2: 多言語テキストを含む画像を読み込む

次に、処理したい画像ファイルをエンジンに渡します。パスは絶対でも相対でも構いませんが、読み取り可能であることを確認してください。

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![OCR の実行例](/images/ocr-example.png "多言語画像で OCR を実行する例")

**ポイント:**  
`load_image` 呼び出しはピクセルデータをメモリに読み込み、OCR アルゴリズムの入力として準備します。画像が大きい場合、エンジンは自動的にダウンサンプリングすることがあります。高解像度スキャンが必要な場合は、後述の `engine.set_max_resolution(3000)` で調整できます。

## Step 3: 認識プロセスを実行する

エンジンが準備でき、画像がロードされたら、いよいよテキスト抽出を行います。

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**ポイント:**  
`recognize()` は裏で重いニューラルネットワークを走らせます。戻り値は生テキスト、信頼度スコア、必要に応じてバウンディングボックスなどを保持したオブジェクトです。

## Step 4: 認識結果のテキストを出力する

エンジンが見つけた内容を確認しましょう。ここではコンソールに出力しますが、ファイルやデータベースに書き込むことも可能です。

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### 期待される出力

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

このような結果が得られたら、**画像をテキストに変換**し、**特殊文字を認識**できています。おめでとうございます。

## よくある落とし穴への対処

シンプルなスクリプトでも、いくつかの問題に直面することがあります。以下は私自身の経験から得た実践的なヒントです。

### 1. 言語パックが不足している

キリル文字が `?` で表示される場合は、言語パックがインストールされているか確認してください。多くの OCR エンジンでは、対応する `.traineddata` ファイルをダウンロードし、エンジンの `tessdata` フォルダに配置する必要があります。

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. 画像品質が低い

ぼやけた画像やコントラストが低い画像は信頼度が下がります。OpenCV で前処理すると効果的です。

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. 大容量ファイルとメモリ使用量

10 MB 程度の写真を処理するとメモリが急増することがあります。`engine.set_max_image_size(2000)` で解像度上限を設定するか、画像をタイルに分割して個別に OCR を実行してください。

### 4. バウンディングボックスの取得

各単語の位置をハイライトしたい場合（UI オーバーレイなどに便利）、`result.boxes` にアクセスします。

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## フルスクリプト – ワンクリック実行

すべてをまとめた単一ファイルを `python ocr_demo.py` として実行できます。エラーハンドリング、オプションの前処理、コメントを含んでいます。

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

実行コマンド:

```bash
python ocr_demo.py path/to/multilingual.png
```

先ほどの出力と同じ結果が表示されれば、**画像からテキストを抽出**できたことが確認できます。

## まとめ

Python で **OCR を実行**する手順を、ライブラリのインストールから画像の読み込み、多言語コンテンツの認識、一般的なエッジケースへの対処まで一通り解説しました。このガイドに従えば、**画像をテキストに変換**し、**特殊文字を認識**し、**画像からテキストを抽出**するコードを自分のプロジェクトにすぐ組み込めます。手作業の文字起こしはもう不要です。

次のステップは？

- 言語パックを追加する（例: `spa` でスペイン語）。  
- 結果を JSON にエクスポートして downstream 処理に活用する。  
- OCR 処理を Flask API に組み込み、他サービスから呼び出せるようにする。  

問題が発生したら、各 OCR ライブラリのコミュニティが活発です。 “ocr library language pack installation” で検索するか、下のコメント欄に質問を残してください。コーディングを楽しみながら、画像を検索可能なテキストに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}