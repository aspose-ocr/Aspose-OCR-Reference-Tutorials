---
category: general
date: 2026-06-19
description: Python の OCR ライブラリを使用して画像で OCR を実行します。画像からテキストを検出し、JPEG からテキストを認識し、スキャンした画像からテキストを効率的に抽出する方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: ja
og_description: Pythonで画像のOCRを実行し、スキャンしたファイルからテキストを抽出します。このガイドでは、画像の読み込み、傾き補正、テキスト認識をステップバイステップで解説します。
og_title: Pythonで画像のOCRを実行する – 完全テキスト抽出ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Pythonで画像のOCRを実行する – 完全テキスト抽出ガイド
url: /ja/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で画像の OCR を実行する – 完全テキスト抽出ガイド

画像ファイルに対して **OCR を実行** したいけど、コードが暗号のようで壁にぶつかっていませんか？ あなただけではありません。スキャンした領収書の山を検索可能な PDF に変換したり、データサイエンスプロジェクトのために JPEG からキャプションを抽出したりする際、JPEG などのフォーマットからテキストを認識できることは、今日の開発者にとって必須スキルです。

このチュートリアルでは、**画像からテキストを検出** し、**スキャン画像からテキストを抽出** し、さらに **OCR 用に画像をロード** する方法を、数行のコードで実演する完全な実行可能サンプルを順を追って解説します。最後まで読めば、インポート忘れや「ドキュメント参照」的な曖昧さのない、実運用可能なスニペットを自分のプロジェクトにすぐ組み込めます。

## 作成するもの

- OCR エンジンを作成し、auto‑deskew を有効化し、JPEG（または任意のサポート形式）をロードして認識結果を出力する小さな Python スクリプト  
- 各設定が **なぜ** 必要かを説明する解説（**どうやって** だけでなく）  
- マルチページ PDF、非英語言語、ぼやけたスキャンなどの一般的な落とし穴への対処法

### 前提条件

- Python 3.8+ がインストール済み（例では `pip install ocr-lib` で入手できる `ocr` パッケージを使用しています – 実際のライブラリ名に置き換えてください）  
- Python の関数と仮想環境に関する基本的な知識  
- 処理したい画像ファイル（JPEG、PNG、TIFF）。ここでは `skewed_page.jpg` を例として使用します

> **プロのコツ:** Windows 環境で OCR ライブラリをインストールする際は、権限の問題を回避するためにターミナルを管理者として実行してください。

---

## Perform OCR on Image – Setup and Configuration

最初に必要なのは、クリーンな OCR エンジンインスタンスです。これは処理全体の「脳」に相当し、適切に構成しなければ、どんなに鮮明な画像でも意味不明な文字列が返ってきます。

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**重要性:**  
`engine.language` を設定すると、OCR エンジンが期待する文字セットが絞り込まれ、精度が大幅に向上します。この設定を省略すると、エンジンは推測に頼り、単純な単語すら誤認識しがちです。

---

## Enable Automatic Deskew – Fix Tilted Scans

スキャンしたページはほとんどが完全に平坦ではありません。わずかな傾きでも文字の分割が乱れ、「Hello」が「H3llo」になることがあります。`auto_deskew` フラグはこの処理を自動で行います。

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**エッジケース:** 画像がすでに真っ直ぐであることが分かっている場合、デスクューを無効にすると数ミリ秒の処理時間短縮が期待できます – 大量ページをバッチ処理する際に有用です。

---

## Load Image for OCR – Supporting JPEG, PNG, TIFF

ここで実際に **OCR 用に画像をロード** します。`ocr.Image.load` メソッドは柔軟で、サポートされているラスタ形式へのパスを受け取ります。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **このステップが重要な理由:** ライブラリはファイルを内部ビットマップに読み込み、必要に応じてカラースペース変換を行います。生のバイトストリームを直接渡すと `FileNotFoundError` が発生するか、最悪の場合空の結果が黙って返ります。

**JPEG からテキストを認識** したい場合は、拡張子が `.jpeg` または `.jpg` であることを確認してください。同じ呼び出しで PNG（`.png`）や TIFF（`.tif`）も問題なく扱えます。

---

## Perform OCR on Image – Running the Engine

エンジンが準備でき、画像がメモリ上にある状態で、いよいよ **画像に対して OCR を実行** します。この一行で前処理、セグメンテーション、分類、テキスト組み立てが行われます。

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**内部で何が起きているか?**  
- デスクューが有効なら変換を適用  
- ニューラルネットワークまたは Tesseract バックエンドで文字を識別  
- 文字を単語・行に結合し、リッチな `result` オブジェクトを返す

---

## Extract Text from Scanned Image – Output the Results

最後に **スキャン画像からテキストを抽出** し、結果を表示します。`result.text` 属性にプレーンテキストが格納されています。

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

典型的な出力例:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

OCR エンジンが文字を検出できなかった場合、`result.text` は空文字列になります。その際は画像品質を再確認するか、`engine.confidence_threshold`（ライブラリがサポートしていれば）を調整してください。

---

## Handling Common Variations

### Recognize Text from JPEG vs PNG

両形式ともサポートされていますが、JPEG の圧縮アーティファクトがエンジンを混乱させることがあります。誤認識が頻発する場合は、まず JPEG を PNG に変換してみてください。

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Detect Text from Image with Multiple Languages

文書に英語とスペイン語が混在している場合は、多言語モードを設定します。

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

これにより、認識時に両方のアルファベットが考慮されます。

### Extract Text from Scanned PDFs

PDF の場合は、まず各ページを画像にラスタライズする必要があります。`pdf2image` などのライブラリを使えば簡単です。

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Full Working Example

以下は `ocr_demo.py` にコピペできる完全なスクリプトです。エラーハンドリングと実行時間測定用の小さなヘルパーが含まれています。

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**期待される出力**（クリアなスキャンを想定）:

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Frequently Asked Questions

**Q: ヘッドレスサーバーで実行できますか？**  
A: もちろんです。ライブラリは GUI がなくても動作します。サーバーに必要なネイティブバイナリ（例: Tesseract）をインストールしておくだけです。

**Q: 画像がぼやけている場合は？**  
A: `engine.recognize` の前にシャープ化フィルタを追加すると効果的です。多くの OCR ライブラリは `image_preprocessing.sharpen = True` を提供しているか、OpenCV の `cv2.GaussianBlur` を逆に使うことで実装できます。

**Q: バッチ処理はサポートされていますか？**  
A: はい。ファイルパスのリストに対して `perform_ocr` をループで呼び出すだけで対応できます。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}