---
category: general
date: 2026-06-28
description: Aspose OCR for Python を使用して画像からテキストを認識し、OCR を実行する方法を学びます。OCR 言語の設定手順と信頼度スコアの抽出が含まれています。
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: ja
og_description: PythonでAspose OCRを使用して画像からテキストを認識します。このガイドでは、OCR言語の設定方法、画像でのOCR実行方法、そして信頼度の取得方法を示します。
og_title: 画像からテキストを認識する – 完全なPython OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Aspose OCRで画像からテキストを認識する – 完全Pythonガイド
url: /ja/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト認識 – 完全な Python ガイド

画像からテキストを **recognize text from image** したいと思ったことはありませんか？しかし、速度と精度の両方を兼ね備えたライブラリがどれか分からない…という方は多いです。ドキュメント自動化の世界では、**perform OCR on image** が日常的な要件です。領収書のデジタル化、パスポートのスキャン、あるいは多言語サインからのデータ抽出など、シーンはさまざまです。

このチュートリアルでは、Aspose OCR for Python を使って **recognize text from image** を実際に行うハンズオン例を紹介し、**how to set OCR language** についても解説します。最終的に、全文テキスト、行ごとの信頼度、単語ごとのバウンディングボックスを出力するスクリプトが完成します。

## 必要な環境

- **Python 3.8+**（最新バージョンで動作します）
- **Aspose.OCR for Python via Java** パッケージ – `pip install aspose-ocr` でインストール
- テキスト抽出対象の画像ファイル（例: `mixed_script.png`）
- 基本的な IDE またはエディタ – VS Code、PyCharm、あるいはシンプルなテキストエディタで構いません

重い依存関係やネイティブバイナリのコンパイルは不要です。pip でインストールするだけで準備完了です。

## Step 1: OCR エンジンのインストールとインポート

まずはライブラリをマシンに導入し、必要なクラスをインポートしましょう。

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Pro tip:** 社内プロキシ環境下にいる場合は、pip コマンドに `--proxy` フラグを付与してください。後々のトラブルを防げます。

## Step 2: エンジンの作成と **how to set OCR language**

`OcrEngine` インスタンスの生成はコンストラクタを呼び出すだけです。しかし、エンジンに期待する言語を伝えることで本格的な力が発揮されます。ここが **how to set OCR language** のポイントです。

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

なぜ重要かというと、OCR アルゴリズムは言語固有の文字モデルを使用します。正しい言語を設定することで、特に似た形状の文字（例: ラテン文字の “0” と “O”、キリル文字の “О”）の認識精度が大幅に向上します。

## Step 3: **perform OCR on image** – テキストの認識

画像パスをエンジンに渡し、魔法のように処理させます。メソッドは `RecognitionResult` オブジェクトを返し、必要な情報がすべて格納されています。

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

ファイルが見つからない場合は Aspose が `FileNotFoundError` をスローします。実運用では `try/except` でラップして、例外がサービス全体を停止させないようにしましょう。

## Step 4: 完全な認識テキストの出力

最も一般的な要求は「テキストを教えて」だけです。`getText()` メソッドは検出されたすべての行を連結し、単一の文字列として返します。

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

出力例:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

これが **recognize text from image** のコアです。1 行でエンジンが解読した全テキストを取得できます。

## Step 5: (任意) 各行の信頼度を表示

信頼度スコアを確認すれば、結果の信頼性を評価できます。たとえば 0.70 未満の行は人手での確認が必要かもしれません。

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

典型的な出力例:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Step 6: (任意) 各単語のバウンディングボックス取得 – UI ハイライトに最適

ユーザーが単語をクリックして OCR データを表示できるビューアを作る場合、バウンディングボックス座標は非常に有用です。

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

サンプル出力:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

座標は元画像に対するピクセル単位なので、キャンバス上に直接オーバーレイできます。

## 完全動作スクリプト

以上をまとめた、すぐに実行できるスクリプトです。`YOUR_DIRECTORY/mixed_script.png` を実際の画像パスに置き換えてください。

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

実行コマンド:

```bash
python ocr_demo.py
```

コンソールに抽出された全文テキスト、信頼度スコア、バウンディングボックスが表示されます。

## よくある質問とエッジケース

### 画像に複数言語が混在している場合は？

Aspose OCR はマルチランゲージ検出をサポートしていますが、**combined language flag** を渡す必要があります。例としてラテン文字とキリル文字の両方を認識させる場合:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

パイプ (`|`) 演算子で列挙型を結合します。これにより、**perform OCR on image** を多言語シナリオでも実現できます。

### 低解像度画像の精度を上げるには？

- **前処理**: コントラストを上げる、二値化する、または Pillow などでアップスケールする。
- **正しい DPI を設定**: 画像メタデータがある場合は Aspose がそれを尊重します。
- **適切な言語を設定**: 言語を具体的に指定すればするほど、モデルの性能が向上します。

### 画像の特定領域だけを抽出したい？

可能です。`recognizeRegion` メソッド（基本例には未掲載）を使用し、関心領域を表す矩形オブジェクトを渡します。テーブルや特定ブロックだけを抽出したいときに便利です。

## まとめ

本稿では、Aspose OCR for Python を使って **recognize text from image** を行う一連の手順を解説しました。**perform OCR on image** の実装方法、**OCR language** の正しい設定、そして信頼度スコアや単語レベルのバウンディングボックス取得まで網羅しています。

次のステップとしては:

- 他言語 (`Language.Arabic`, `Language.Japanese` など) を試す
- スクリプトを Flask/Django の Web サービスに組み込み、OCR API として提供する
- バウンディングボックスデータをフロントエンドのキャンバスに統合し、ユーザーがテキストをハイライトできるようにする

デジタル化すべき文書が増えるほど、活用の幅は広がります。難しい画像で詰まったらコメントで教えてください。一緒に解決しましょう。Happy coding!

![recognize text from image example](/images/ocr_example.png "recognize text from image – Aspose OCR output")

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}