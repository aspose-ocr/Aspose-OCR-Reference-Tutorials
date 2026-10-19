---
category: general
date: 2026-03-26
description: 画像からテキストを素早く認識するには、OCR用に画像を読み込む方法と特定領域からデータを抽出する方法を学びましょう。この実践的なガイドに従ってください。
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: ja
og_description: Pythonで画像からテキストを認識するには、OCR用に画像を読み込み、関心領域を設定し、クリーンなテキストを抽出します。全体のワークフローを学びましょう。
og_title: 画像からテキストを認識する – 完全なPython OCRチュートリアル
tags:
- OCR
- Python
- Image Processing
title: 画像からテキストを認識する – ステップバイステップ Python OCR チュートリアル
url: /ja/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する – 完全な Python OCR チュートリアル

画像から **テキストを認識** したいけれど、どこから始めればいいか分からないことはありませんか？スキャンしたフォームやレシート、スクリーンショットがあり、特定のボックス内の文字だけが欲しいときに便利です。数行の Python で画像を OCR 用に読み込み、単一領域にフォーカスし、必要なテキストを取得できます—手動でコピーする必要はありません。

このチュートリアルでは、画像の読み込み、関心領域（ROI）の定義、OCR エンジンの実行、結果の出力までの全プロセスを順に解説します。最後まで読めば、画像の特定部分からテキストを抽出するコードを任意のプロジェクトに組み込めるようになります。重厚な画像処理パイプラインは不要です。シンプルで読みやすいコードがすぐに使えます。

## 前提条件

- Python 3.8+ がインストールされていること  
- `ocr` パッケージ（または互換性のある OCR ライブラリ） – `pip install ocr-lib` でインストール（実際に使用するパッケージ名に置き換えてください）  
- 読み取り対象のフォームが含まれる PNG/JPEG 画像  
- Python の関数やクラスに関する基本的な知識  

これらに慣れているなら、すぐに次へ進んで構いません。まだの場合は、コーヒーを一杯用意して上記項目を確認してください。以降の手順はそれらが整っている前提で説明します。

## Step 1: OCR エンジンインスタンスの作成 – 「画像からテキストを認識」コア

最初に必要なのは、OCR エンジンとやり取りできるオブジェクトです。これは後で **画像からテキストを認識** する脳みそとなります。

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **なぜ重要か:** エンジンを一度初期化すれば、言語パックなどの設定を複数画像で再利用でき、パフォーマンスが向上しコードもすっきりします。

## Step 2: OCR 用に画像を読み込む – メモリへ画像を取り込む

次に実際に **画像を OCR 用に読み込む** 作業です。ライブラリが提供する便利な static メソッドでファイルを読み取り、エンジンが理解できるオブジェクトを返します。

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **プロのコツ:** 画像が大きい場合は、読み込む前にリサイズを検討してください。小さな画像は OCR の速度を上げ、ほとんどの印刷文字で精度を損なわずに処理できます。

## Step 3: OCR の関心領域（ROI）を定義する

ページ全体を処理する必要はなく、ユーザーが入力した特定のボックスだけが欲しいことが多いです。**OCR の関心領域** を定義すると、エンジンはそれ以外を無視し、ノイズが減り処理が高速化します。

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **ROI に注目すべき理由:**  
> - **速度:** ピクセル数が減るのでスキャンが速くなる。  
> - **精度:** ROI 外の背景グラフィックが文字認識を妨げない。  
> - **シンプルさ:** 必要なフィールドに対応するクリーンな文字列が得られる。

## Step 4: OCR プロセスを実行 – 本番の瞬間

設定がすべて整ったら、定義した ROI 内で **画像からテキストを認識** します。

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

エンジンが複数領域に対応している場合、`ocr_result` はリストになりますが、ここでは単一 ROI なので `get_text()` メソッドを持つシンプルなオブジェクトです。

## Step 5: テキストを抽出して表示 – 最終出力を取得

結果オブジェクトから文字列を取り出し、画面に表示します。ここで得た出力をデータベースや CSV、その他のロジックに渡すことができます。

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**期待される出力**（例: 記入された名前フィールド）:

```
Text inside ROI:
 John Doe
```

OCR エンジンが余分な空白や改行を返す場合は、`.strip()` や正規表現でクリーンアップしてください。

## よくあるエッジケースの対処法

| 状況                                   | 対応策                                                                      |
|----------------------------------------|-----------------------------------------------------------------------------|
| **低解像度画像**                       | 読み込む前に `Pillow` の `Image.resize` で拡大。                           |
| **傾いた・回転したテキスト**           | `ocr.Imaging.Image.rotate` で回転補正を適用。                               |
| **複数言語**                           | エンジンに言語パックを設定: `ocr_engine.set_language('eng+spa')`.          |
| **ROI が未定義**                       | `add_region_of_interest` を省略すれば、エンジンは画像全体を処理。          |
| **予期しない文字（例: カンマ）**       | 文字列を後処理: `extracted_text.replace(',', '')`.                         |

これらのヒントで、**画像を OCR 用に読み込む** パイプラインは、元データが完璧でなくても頑丈に動作します。

## 完全動作サンプル – コピー＆ペーストで実行

以下は `.py` ファイルに貼り付けてそのまま実行できるスクリプトです。インポート、エラーハンドリング、画像の存在確認ヘルパーまで網羅しています。

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

このスクリプトを実行すると、ROI から抽出されたクリーンな文字列が出力され、すぐに利用できるデータが得られます。

## 結論

これで **画像からテキストを認識** する一連の流れが把握できました。まず **画像を OCR 用に読み込む**、次に正確な **OCR 関心領域（ROI）** を定義し、最後にクリーンなテキストを抽出します。この手法は上記のような Python OCR ライブラリで共通して利用でき、複数 ROI や異なる言語、前処理ステップへも簡単に拡張可能です。

次に試したいこと:

- **OCR 用画像前処理**（閾値処理、ノイズ除去）でスキャンの精度を向上させる。  
- **ROI から抽出したテキスト** を pandas の DataFrame に格納し、バルクデータ分析を行う。  
- 大規模・高信頼性が必要な場合は、Google Vision や Azure Computer Vision といったクラウド OCR サービスに切り替える。

座標を自分のフォームに合わせて調整し、オートメーションの効果を体感してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}