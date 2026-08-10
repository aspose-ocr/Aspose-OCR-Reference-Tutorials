---
category: general
date: 2026-06-16
description: IDカードからスペイン語テキストを抽出するために、OCRの関心領域（ROI）を定義します。OCR用に画像を読み込む方法と、ROIを効率的に指定する方法を学びましょう。
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: ja
og_description: OCRでIDカードからスペイン語テキストを抽出するための関心領域を定義します。画像の読み込みとROIの指定に関するステップバイステップガイド。
og_title: OCRにおける関心領域の定義 – 完全なPythonチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCRで関心領域を定義する – 完全なPythonチュートリアル
url: /ja/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR における関心領域の定義 – 完全な Python チュートリアル

画像の中で実際に必要な部分だけを読み取るために **define region of interest in OCR** を行う方法を考えたことはありますか？このチュートリアルでは、その手順を詳しく解説し、さらに **load image for OCR** の方法と、Python の数行で ID カードからスペイン語テキストを抽出する方法をご紹介します。  

ノイズの多いスキャン画像を見て「名前フィールドだけをきれいに取得できる方法があるはずだ」と思ったことがあるなら、ここがその場所です。最後まで読めば、背景の雑音に邪魔されずに必要な ID カードのテキストを取得できるようになります。

## 学べること

- OCR を実行する前に **define region of interest** を定義すべき理由。  
- 人気のある Python OCR ラッパーを使用して **load image for OCR** を行う正確な手順。  
- ピクセル座標で **how to specify ROI** を指定する方法。  
- ソース言語がスペイン語の場合でも、**extract id card text** を確実に取得する方法。  
- 回転したカードや低コントラストのスキャンなど、エッジケースを処理するためのヒント。  

OCR の事前知識は不要です――Python 3 環境とテストしたい ID カードの JPEG があれば始められます。

---

![Define region of interest illustration](placeholder.png){alt="関心領域の例：IDカード画像上にハイライトされた矩形を示す"}

## ステップ 1: OCR ライブラリのインストールとインポート

まず最初に、先ほどのスニペットと同様に `OcrEngine` クラスを提供するライブラリが必要です。このガイドでは架空の `ocr` パッケージを使用しますが、同じ概念は `pytesseract`、`easyocr`、または言語と ROI を設定できる任意のラッパーにも当てはまります。

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* `pytesseract` を使用している場合、`Rectangle` クラスはシンプルなタプル `(left, top, width, height)` に置き換わります。フローの残りは同一です。

## ステップ 2: OCR 用画像のロード

ここで **load image for OCR** を行います。エンジンは `ocr.Image` オブジェクトを期待するので、ID カードが保存されているファイルを指し示します。パスは絶対パスでもスクリプトの作業ディレクトリからの相対パスでも構いません。

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

画像が非常に大きい場合は、まずリサイズすることを検討してください。OCR エンジンは幅 1500 px 未満の画像でより高速に動作します。

## ステップ 3: ROI の指定方法（関心領域の定義）

チュートリアルの核心です: **how to specify ROI**。関心領域は単に「このピクセル範囲だけを見てください」と OCR エンジンに指示する矩形です。ID カードの名前フィールドの周りに箱を描くイメージです。

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

なぜその数値なのか？サンプル画像では名前が左端から約 120 px、上端から 80 px の位置にあります。処理するカードのレイアウトに合わせて調整してください。  

*Edge case:* カードが 90° 回転している場合は `width` と `height` を入れ替え、`left`/`top` をそれに合わせて調整するか、Pillow で事前に画像を回転させてからエンジンに渡してください。

## ステップ 4: ROI 内で OCR を実行

ROI が定義されると、エンジンは矩形外の領域を無視します。これにより処理速度が向上するだけでなく、背景グラフィックによる誤検出も減少します。

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` 呼び出しは、認識されたテキスト、信頼度スコア、各単語のバウンディングボックスを保持するオブジェクトを返します。

## ステップ 5: ID カードテキストの抽出（スペイン語出力の検証）

最後に、ROI の結果から **extract id card text** を行い、コンソールに出力します。事前に言語を Spanish に設定しているため、OCR エンジンは「ñ」や「á」などのアクセント文字に対応した辞書を使用し、精度が向上します。

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### 期待される出力

```
ROI text: JUAN PÉREZ GARCÍA
```

文字化けが発生した場合は、画像が本当にスペイン語であること、そして OCR ライブラリの言語データファイルが正しくインストールされていることを再確認してください。

## よくある落とし穴と回避方法

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| 空文字列が返される | ROI がテキストと交差していない | 画像ビューアで座標を確認。利用可能なら `engine.debug_draw_roi()` を使用。 |
| 大量のゴミ文字 | 言語パックが間違っている | スペイン語の言語データを再インストールするか、`ocr.Language.AUTO` に切り替える。 |
| 信頼度が低い | 画像がぼやけている、またはコントラストが低い | OpenCV で前処理 – `cv2.GaussianBlur` と `cv2.threshold` を適用。 |
| ROI を設定しているのに OCR が画像全体で実行される | 古いライブラリバージョンを使用している | 最新の `ocr` パッケージにアップグレード。古いバージョンは ROI を無視していた。 |

## 例の拡張: 複数の ROI

場合によっては複数のフィールド（例: 名前と ID 番号）を取得したいことがあります。パターンは同じです: `engine.region_of_interest` を変更し、再度 `recognize()` を呼び出します。

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

ライブラリがサポートしていれば、矩形のリストをバッチ処理でき、OCR エンジンへの往復回数を削減できます。

## 完全な動作スクリプト

すべてを統合した、**defines region of interest**、**loads image for OCR**、そして ID カードから **extracts Spanish text** する実行可能スクリプトを示します。

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

スクリプトを実行すると、コンソールに名前が表示されます。矩形の値を入れ替えて他のフィールドを対象にすれば、あらゆる ID カードタイプの文書に再利用できるユーティリティが完成します。

## 次のステップ

- **バッチ処理:** ID カードのフォルダーをループし、抽出した名前を CSV ファイルに保存する。  
- **言語検出:** ユーザーが動的に言語を選択できるようにする。`ocr.Language.AUTO` が便利。  
- **後処理:** 正規表現パターンを適用して一般的な OCR のミスを修正する（例: 名前に出現する “0” を “O” に置換）。  

**define region of interest** の習得により、特にスペイン語文書を扱う際に、**extract id card text** を迅速かつ正確に行う強力な手段が手に入りました。

---

### TL;DR

**define region of interest in OCR**、**load image for OCR**、そして **how to specify ROI** を使って ID カードから **extract spanish text image** を行う方法を示しました。完全な例は 1 分未満で実行でき、座標を少し調整すれば任意のレイアウトに適応可能です。ぜひ試して矩形を調整し、レーザーのように OCR を集中させてみてください。

コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Aspose.OCR を使用した言語選択付き C# で画像テキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像からテキストを抽出 – .NET 用 Aspose.OCR の OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}