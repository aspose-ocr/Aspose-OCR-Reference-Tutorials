---
category: general
date: 2026-06-22
description: Python で数行のコードだけで画像の OCR を実行します。OCR 用に画像を読み込む方法、PNG からテキストを認識する方法、そして
  OCR エンジンを効率的に使用する方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: ja
og_description: Pythonで画像のOCRを迅速に実行します。このチュートリアルでは、OCR用に画像を読み込む方法、PNGからテキストを認識する方法、そして信頼性の高いOCRエンジンの使用方法を示します。
og_title: Pythonで画像のOCRを実行する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像のOCRを実行する – 完全ガイド
url: /ja/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像のOCRを実行する – 完全ガイド

画像ファイルに対して **perform OCR on image** したいと思ったことはありませんか？最初の一行でつまずいてしまうこともあるでしょう。今回の解説では、**load image for OCR** の方法、軽量な **OCR engine** のセットアップ、そして **recognize text from PNG** を数行のコマンドだけで実現する手順を詳しくお見せします。

ライブラリのインストールから、数字と大文字だけを残すホワイトリストの調整まで、すべてカバーします。最後には、どのプロジェクトにもすぐに組み込める実行可能なスクリプトが手に入ります—余計な説明は一切ありません。

## 学べること

- Pythonで **OCR engine** をプログラムから利用する方法  
- ローカルフォルダから **load image for OCR** する正確な手順  
- カスタム文字セットに認識を制限する理由と方法  
- **recognize text from PNG** して結果を安全に扱う方法  

**前提条件:** Python 3.7+ がインストールされていること、慣れたターミナルが使えること、そして読み取りたい画像（例: `serial-number.png`）が用意されていること。OCR の経験は不要です。

---

## Perform OCR on Image – OCRエンジンの初期化

最初に行うべきことは OCR エンジンのインスタンスを作成することです。エンジンはピクセルを解析し文字に変換する「脳」の役割を果たします。

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*なぜ重要か:* エンジンがなければ画像を処理できません。`OcrEngine` クラスは前処理、セグメンテーション、文字分類といった重い処理をすべてひとつのオブジェクトにまとめ、再利用可能にします。

---

## Load Image for OCR – PNG ファイルを提供

エンジンが用意できたら、読み取りたい画像を渡す必要があります。ライブラリは `ImageStream` オブジェクトを受け取りますが、これはファイルパスから直接作成できます。

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*プロのコツ:* 画像は高コントラスト（白背景に黒文字）にし、圧縮アーティファクトは避けましょう。これらは OCR アルゴリズムの精度を下げる原因になります。

---

## Restrict Characters – 数字と大文字のホワイトリスト設定

多くの場合、対象はシリアル番号のように限定された文字集合（例: A‑Z と 0‑9）だけです。ホワイトリストを設定すると、エンジンはそれ以外の文字を無視し、認識精度が大幅に向上します。

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*内部で何が起きているか？* エンジンは最終分類段階の前に、ホワイトリストに含まれないグリフを除去するフィルタを構築します。画像にノイズや装飾文字が混在している場合に特に有効です。

---

## Recognize Text from PNG – OCR プロセスの実行

エンジンの準備と画像のロードが完了したら、いよいよ **perform OCR on image** です。`recognize()` 呼び出しが全パイプラインを走らせ、結果オブジェクトを返します。

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

パフォーマンスが気になる場合、300 × 200 px の PNG であればモダンなノートパソコン上で数百ミリ秒程度で完了します。

---

## Output and Verify – 認識結果の取得

最後のステップは結果オブジェクトからプレーンテキストを抽出することです。ホワイトリストにマッチしなかった文字は自動的に除外され、後続処理に使えるクリーンな文字列が得られます。

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*典型的な出力例:* `AB12C3D4E5`（画像にこのシリアル番号が正確に含まれている場合）。  
出力が空だったり文字化けしたりしたら、画像の品質とホワイトリストを再確認してください。よくある落とし穴は、必要な文字をホワイトリストから抜かしてしまうことです。

---

## Edge Cases & Common Gotchas

| 状況 | 確認すべきこと | 推奨される対策 |
|-----------|---------------|---------------|
| **ファイルが見つからない** | パスのタイプミスやファイル欠損 | `set_image` を呼ぶ前に `os.path.abspath` でフルパスを確認 |
| **コントラストが低い画像** | 文字が背景と混ざっている | `Pillow` や `OpenCV` で簡易的な閾値処理を施す |
| **予期しない文字が出る** | ホワイトリストが厳しすぎる | 欠けている文字をホワイトリスト文字列に追加 |
| **画像が大きすぎる** | 認識が遅い | 幅を最大 1024 px にリサイズ。品質は概ね維持される |

---

## Full Script – 実行可能な完全スクリプト

以下はすべての要素を結合した自己完結型スクリプトです。`ocr_demo.py` として保存し、`YOUR_DIRECTORY` を実際のフォルダに置き換えてから `python ocr_demo.py` を実行してください。

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*期待されるコンソール出力*（PNG に `SN12345` が含まれている場合）:

```
Recognized text: SN12345
```

---

## Conclusion

これで、Python で **perform OCR on image** ファイルを **load image for OCR** から **recognize text from PNG** まで、カスタマイズ可能な **OCR engine** を使ってクリーンな結果を取得する手順がすべて分かりました。シンプルで拡張性が高く、ほとんどのシリアル番号スタイルのスキャンにすぐに利用できます。

次は何をすべきか？ホワイトリストを小文字に変えてみる、JPEG や BMP など別フォーマットで実験する、あるいはバッチ処理パイプラインに組み込むなど、エンジン → 画像 → 設定 → 認識 → 出力というパターンはほぼすべての OCR タスクに応用できます。

質問や、うまく認識できない画像があれば下のコメント欄へどうぞ。Happy coding!

![Diagram illustrating the steps to perform OCR on image using Python](https://example.com/ocr-flow.png "Diagram showing how to perform OCR on image with a Python OCR engine")


## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}