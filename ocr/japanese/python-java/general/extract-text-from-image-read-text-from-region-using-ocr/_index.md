---
category: general
date: 2026-07-05
description: Python OCR を使用して画像からテキストを抽出します。OCR 用に画像を読み込む方法、領域からテキストを読み取る方法、数行のコードで請求書からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: ja
og_description: Python OCRで画像からテキストを抽出します。このガイドでは、OCR用に画像を読み込む方法、領域からテキストを読み取る方法、そして請求書からテキストを迅速に抽出する方法を示します。
og_title: 画像からテキストを抽出 – OCRで領域のテキストを読み取る
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 画像からテキストを抽出 – OCRで領域のテキストを読み取る
url: /ja/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – OCRで領域からテキストを読み取る

画像から **テキストを抽出** したいことはありますか、しかし重要なのは特定の部分だけ—たとえば請求書の合計金額のような場合です。あなただけではありません。実際のプロジェクトでは、画像全体を解析するのではなく **領域からテキストを読み取る** 必要があることが多いです。幸い、数行の Python で OCR 用に画像を読み込み、関心領域（ROI）を定義し、必要な文字だけを抽出できます。

このチュートリアルでは、**OCR 用に画像を読み込む** 方法、ROI を設定する方法、そして最終的に **請求書からテキストを抽出** する方法を示す、完全で実行可能な例を順に解説します。最後まで読むと、領域ベースの認識をサポートする任意の一般的な OCR ライブラリで動作する、すぐに使えるスニペットが手に入ります。

---

## 必要なもの

- Python 3.8+（コードは 3.10 でも動作します）  
- `OcrEngine` クラスを提供する OCR パッケージ（デモでは架空の `ocr` モジュールを使用します；`pytesseract`、`easyocr`、または ROI をサポートする任意のライブラリに置き換えてください）  
- サンプル画像（例：`invoice.png`）で、はっきりとした印刷テキストが含まれているもの  
- Python の関数やクラスに関する基本的な知識（ディープラーニングの知識は不要）

これらがすでに揃っているなら、素晴らしいです—さっそく始めましょう。まだの場合は、python.org から最新の Python を入手し、`pip install your-ocr-lib` で OCR パッケージをインストールしてください。

![画像からテキストを抽出する例](extract-text-from-image.png "画像からテキストを抽出 – 領域ベース OCR デモ")

*上の画像は、**画像からテキストを抽出** する対象となる領域（赤い矩形）を示しています。*

## ステップ 1: OCR ライブラリのインストールとインポート

まず、OCR ライブラリが環境にインストールされていることを確認してください。以下のインポートパターンは、`OcrEngine` クラスを提供するほとんどのパッケージで機能します。

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **プロのコツ:** `pytesseract` を使用する場合、Tesseract のバイナリを別途インストールし、`pytesseract.pytesseract.tesseract_cmd` にそのパスを設定する必要があります。

## ステップ 2: OCR エンジンの作成と言語設定

エンジンの作成は簡単ですが、言語を指定することで精度が大幅に向上します。特に数字や英単語を含む請求書の場合は効果的です。

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

なぜこのようにするのでしょうか？ OCR エンジンは言語モデルを使用して文字を予測します。英語を期待するように設定することで、例えば “0” を “O” と誤認識するような偽陽性を減らすことができます。

## ステップ 3: OCR 用に画像を読み込む

ここで実際に **OCR 用に画像を読み込む** ことになります。ほとんどのライブラリはファイルパスまたは Pillow の画像オブジェクトを受け取ります。ここでは簡単のため、ライブラリの組み込みローダーを使用します。

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

パスが正しいディレクトリを指していることを確認してください。スクリプトが別の作業ディレクトリから実行される場合に相対パスを忘れるというミスがよくあります。

## ステップ 4: 関心領域（ROI）の定義

ROI の定義は **領域からテキストを読み取る** の核心です。請求書の合計金額が記載された部分を矩形で囲むイメージです。

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` と `top` は矩形の左上隅の X 座標と Y 座標を表します。  
- `width` と `height` はボックスのサイズを設定します。  
- ピクセル座標を表示できる画像ビューアを使って、さまざまな値を試すことができます。

> **ROI が重要な理由:** ページ全体に OCR を実行すると CPU サイクルが無駄になり、無関係なテキストや表、グラフィックからノイズが入ることがよくあります。領域に絞ることで、よりクリーンな結果と高速な処理が得られます。

## ステップ 5: 指定した領域で OCR を実行する

すべての準備が整ったので、最後に **画像からテキストを抽出** します—ただし、定義した ROI 内だけです。

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` メソッドは、通常、生の文字列、信頼度スコア、場合によっては各単語のバウンディングボックスを含むオブジェクトを返します。今回の目的ではプレーンテキストだけが必要です。

## ステップ 6: 抽出したテキストを出力する

結果をプリントして確認しましょう。このステップは実際のシナリオで **請求書からテキストを抽出** することを示しています。

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### 期待される出力

```
Text inside ROI:
Total Amount: $1,245.67
```

請求書のレイアウトが異なる場合、矩形内にあるテキストが表示されます—たとえば請求書番号、日付、または PO 番号などです。

## ステップ 7: 再利用可能な関数にまとめる（オプション）

複数の請求書で再利用できるように、ロジックを関数にまとめます。これにより **領域での OCR** を汎用ユーティリティとして示すこともできます。

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

これで任意の請求書に対して関数を呼び出すことができます。

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## よくある落とし穴と回避策

| 問題点 | 発生原因 | 対策 |
|-------|----------|------|
| **空白出力** | ROI が実際にテキストをカバーしていない（座標が間違っている） | 画像エディタでピクセル値を再確認し、視覚的デバッグオーバーレイを追加する。 |
| **文字化け** | 画像解像度が低い、またはコントラストが悪い | 画像を前処理する：グレースケールに変換し、閾値処理（`cv2.threshold`）を適用する。 |
| **言語設定ミス** | エンジンが必要な文字セットを含まない言語をデフォルトにしている | `ocr_engine.language` を `ENGLISH` または適切なロケールに明示的に設定する。 |
| **パフォーマンス低下** | 大きな画像に対して OCR を繰り返し実行している | 読み込む前に画像をリサイズするか、最初に切り抜いて ROI のみを処理する。 |

## 例の拡張: 複数の ROI

請求書に複数の項目が必要になることがあります—たとえば合計金額と請求日両方の **請求書からテキストを抽出**。矩形のリストをループ処理できます：

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

このパターンによりコードがすっきりし、後から領域を追加しやすくなります。

## 結論

ここでは、Python OCR を使用して **画像からテキストを抽出** する完全なエンドツーエンドのワークフローを、特定の領域に焦点を当てて解説しました。**OCR 用に画像を読み込み**、**関心領域** を定義し、エンジンを呼び出すことで、確実に **領域からテキストを読み取る** ことができます—請求書の合計金額やレシートの日付、その他任意の局所データを抽出するのに最適です。  

自由に試してみてください

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose OCR を使用した画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキストを抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)
- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}