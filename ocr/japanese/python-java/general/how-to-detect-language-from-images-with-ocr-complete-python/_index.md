---
category: general
date: 2026-06-22
description: Pythonで画像から言語を検出し、OCRを使ってテキストを抽出する方法を学びましょう。自動言語検出とテキスト抽出をカバーしたステップバイステップのチュートリアルです。
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: ja
og_description: 画像からOCRで言語を検出する方法は？このガイドでは、PythonでOCRを使用して言語を検出し、テキストを抽出する手順をステップバイステップで示します。
og_title: OCRで画像から言語を検出する方法 – 完全なPythonウォークスルー
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCRで画像から言語を検出する方法 – 完全なPythonガイド
url: /ja/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から言語を検出する OCR 完全ガイド（Python）

画像を開かずに **言語を検出** したいと思ったことはありませんか？ あなただけではありません。レシートスキャナーや多言語文書アーカイブ、シンプルな写真からテキストへの変換アプリなど、さまざまなプロジェクトでテキストがどの言語に属しているかを把握してから処理を進める必要があります。

このチュートリアルでは、画像から **言語を検出** し、実際の文字を抽出する実践的なエンドツーエンドの例を順を追って解説します。最後まで読めば、数行の Python コードを実行し、任意の対応画像を指定するだけで検出された言語 *と* 抽出されたテキストの両方を取得できるようになります。余計な説明は省き、すぐにコピー＆ペーストできる明快な解決策をご提供します。

## 学べること

- Python で軽量な OCR ライブラリをインストール・設定する方法  
- OCR エンジンを初期化し、自動言語検出を有効にする方法  
- 画像（対応フォーマット任意）を読み込み、OCR を実行する手順  
- 検出された言語と抽出されたテキストを取得する方法  
- 未対応フォーマットや曖昧な言語結果など、一般的な落とし穴への対処法  

多言語文書で **OCR をどう使うか** と悩んだことがある方に最適なガイドです。

---

## 前提条件

作業を始める前に、以下が環境に揃っていることを確認してください。

| 必要条件 | 理由 |
|-------------|----------------|
| Python 3.9 以上 | 使用する OCR パッケージは最新のインタプリタを対象としています。 |
| `pip`（Python パッケージマネージャ） | OCR ライブラリのインストールに必要です。 |
| テキストが含まれるサンプル画像（例：`sample-multilang.png`） | 実際にテストできる具体的な素材が必要です。 |
| 任意：仮想環境（`venv` または `conda`） | 依存関係を整理し、バージョン衝突を防げます。 |

> **プロのコツ:** 仮想環境内で作業する場合は、OCR パッケージをインストールする前に環境をアクティベートして、グローバルな Python を汚染しないようにしましょう。

---

## 手順 1: OCR ライブラリのインストール

本チュートリアルでは、コードスニペットに示した API と同等の仮想パッケージ `ocr` を使用します。実際のプロジェクトでは `pytesseract`、`easyocr`、または自動言語検出をサポートする任意のライブラリに置き換えて構いません。

```bash
pip install ocr
```

> **注意:** パッケージは軽量（< 5 MB）で、Windows、macOS、Linux すべてで動作します。権限エラーが出た場合はコマンドに `--user` を付加してください。

---

## 手順 2: OCR エンジンの初期化 – 言語検出の準備

ライブラリの準備ができたら、OCR エンジンのインスタンスを作成します。これが実際に画像を走査し、言語を判別するオブジェクトです。

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

なぜエンジンから始めるのか？ エンジンは OCR システムの「脳」に相当し、設定情報や言語モデルの読み込み、裏側での重い処理を管理します。最初に初期化しておくことで、後続の画像読み込みなどの呼び出しが適切なコンテキストで実行されます。

---

## 手順 3: 画像を読み込み自動言語検出を有効化

次に画像をエンジンに渡します。同時に *自動言語検出* フラグをオンにし、OCR エンジンに言語を推測させます。

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **自動検出を有効にする理由**  
> 多くの OCR ライブラリはデフォルトで英語（English）を使用します。文書にフランス語や日本語など別のスクリプトが含まれている場合、この設定がなければエンジンはそれらを見逃してしまいます。`set_auto_detect_language(True)` を有効にすると、エンジンはビットマップを走査し、文字形状統計を比較して最も適切な言語モデルを選択します。

---

## 手順 4: OCR の実行 – 画像からテキストを抽出

画像がロードされ、言語検出が有効になったら、実際の OCR は単一メソッド呼び出しで完了します。

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

`recognize()` メソッドは内部で次の 2 つの処理を行います。

1. **言語検出:** 画像上で軽量分類器を走らせ、言語コード（例：`en`、`fr`、`es`）を決定します。  
2. **テキスト抽出:** 選択された言語固有モデルを用いて文字を Unicode 文字列に変換します。

この 2 つが同時に実行されるため、結果はすべて `result` オブジェクトに格納されます。

---

## 手順 5: 検出された言語と抽出テキストの取得・表示

最後に、`result` オブジェクトから言語コードと生テキストを取り出し、コンソールに出力します。

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### 期待される出力例

`sample-multilang.png` にフランス語テキストが含まれている場合、次のような出力が得られるでしょう。

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

画像が曖昧だったり複数言語が混在している場合、エンジンは最も自信のある言語を返します。さらに詳細が必要な場合は、ほとんどのライブラリが提供する `get_confidence()` メソッドで信頼度スコアを取得できます（高度なユースケース向け）。

---

## 一般的なエッジケースの対処法

### 1. 未対応画像フォーマット

OCR ライブラリが認識しない TIFF ファイルを読み込もうとすると、`ocr.ImageStream.from_file()` が `OcrUnsupportedFormatError` を送出します。以下のように try/except でラップしてください。

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. 低解像度画像

解像度が約 300 dpi 未満になると OCR の精度は急激に低下します。精度が悪いと感じたら、Pillow で前処理を行うことを検討してください。

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. 画像内に複数言語が混在

画像に複数言語が含まれる場合、自動検出は支配的な言語を選びます。すべての言語を取得したい場合は自動検出をオフにし、エンジンに言語リストを手動で渡します。

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

この設定にすると、OCR は各言語モデルを順に適用し、テキストブロックごとに最適なマッチを返します。

---

## 完全スクリプト – すべての手順を統合

以下は、ここまで解説した内容をすべて組み込んだ実行可能な Python スクリプトです。`detect_language_ocr.py` という名前で保存し、`python detect_language_ocr.py` と実行してください。

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**実行すると** 言語コードと抽出テキストが即座に表示されます。これが **画像から言語を検出** し、**テキストを抽出** する一連の手順です。

---

## 次のステップと関連トピック

- **精度向上:** `opencv-python` を使ったしきい値処理やノイズ除去などの前処理を試す。  
- **バッチ処理:** フォルダ内の多数画像をループで処理できるようスクリプトを拡張。  
- **NLP との統合:** 抽出テキストを `langdetect` などの言語判定ライブラリに渡し、二重チェックを実装。  
- **他の OCR エンジンの探索:** `pytesseract` は細かい制御が可能、`easyocr` は 80 以上の言語を即座にサポート。  

これらのテーマはすべて「画像から言語を検出」「画像からテキストを抽出」「OCR の使い方」「テキスト抽出方法」といったキーワードに直結しており、基礎を固めた後にさらにスキルを広げられます。

---

## 結論

本稿では **画像から言語を検出** する方法をコード例と共に詳述し、各ステップの意図を解説しました。OCR エンジンを初期化し、画像をロードし、自動言語検出を有効化、最後に `recognize()` を呼び出すだけで、言語識別子と抽出テキストの両方をシンプルに取得できます。

このロジックをレシートスキャンサービス、多言語チャットボット、デスクトップユーティリティなど、さまざまなアプリケーションに組み込んでみてください。基本的な考え方は変わりません—OCR エンジンに重い処理を任せ、得られた結果を自由に活用するだけです。

質問やエッジケースに関する相談、面白い活用例があればぜひコメントで共有してください。コーディングを楽しみながら、画像を検索可能なテキストへと変換しましょう！

![画像から言語を検出する方法](ocr-demo.png "Python OCR を使用して画像から言語を検出する様子を示すスクリーンショット")


## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連テーマを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Aspose OCR で画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR を使用した C# の画像テキスト抽出と語彙選択](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [AspOCR の使い方：.NET 向け画像前処理 OCR フィルタ](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}