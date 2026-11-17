---
category: general
date: 2026-03-26
description: Python OCRチュートリアル：画像からテキストを抽出し、OCR用に画像を読み込み、Aspose OCRを使ってレシートのテキストを数ステップで認識する方法を学ぶ。
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: ja
og_description: Python OCRチュートリアル：画像からテキストをすばやく抽出し、OCR用に画像を読み込み、Aspise OCRでレシートのテキストを認識する方法。
og_title: Python OCRチュートリアル – 画像からテキストを抽出
tags:
- OCR
- Aspose
- Python
title: Python OCRチュートリアル – Asposeで画像からテキストを抽出
url: /ja/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR チュートリアル – Aspose を使用した画像からテキストを抽出

ぼんやりしたレシートやスキャンしたフォームから、カスタム正規表現を書いて何時間も費やすことなくテキストを抽出する方法を考えたことはありませんか？ あなたは一人ではありません。この **python ocr tutorial** では、OCR 用の画像を読み込む方法、Python で OCR を実行する方法、そして最終的に Aspose OCR ライブラリを使用してレシートファイルからテキストを認識する手順を解説します。  

このガイドが終わる頃には、サポートされている任意の画像形式を読み取り、テキストコンテンツを抽出し、コンソールに出力するすぐに実行できるスクリプトが手に入ります。外部サービスや API キーは不要で、純粋な Python と強力な OCR エンジンだけです。  

## 必要なもの

- Python 3.8 以上（コードは型ヒントを使用しているため、最新のインタプリタが最適です）
- `asposeocrjava` パッケージを `pip install aspose-ocr` でインストール
- サンプル画像 – 例として典型的な店舗レシートを含む `receipt_noisy.jpg`
- (オプション) 依存関係を整理するための仮想環境

これらの項目がすべて揃っていれば、すぐにコードに進みましょう。  

## 手順 1: Aspose OCR クラスのインストールとインポート

まず、Aspose OCR パッケージが利用可能であることを確認してください。その後、必要なクラスをインポートします。

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Why this matters:** 必要なシンボルだけをインポートすることで名前空間がすっきりし、インタプリタに実際に使用するライブラリの部分を示すことができます。また、後続のコード行が短くなり、チュートリアルが追いやすくなります。

> **Pro tip:** Jupyter ノートブックを使用している場合、インストール行の先頭に `!` を付けてセル内で実行してください。

## 手順 2: OCR エンジンの作成と Deep‑Learning モードの有効化

Aspose には複数のエンジンモードがあります。実際のレシートの多くでは、特にノイズの多いスキャンに対して、Deep‑Learning モデルが最も高い精度を提供します。

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Why deep‑learning?** 従来のルールベース OCR は低コントラストや歪んだ文字でつまずくことがあります。何百万ものグリフで訓練された Deep‑learning モデルは変化により適応しやすく、スマートフォンで撮影したレシートに対して *perform OCR in Python* する際にまさに必要なものです。

## 手順 3: OCR 用画像のロード

ここで実際に **load image for OCR** を行います。Aspose.Imaging は PNG、JPEG、BMP、TIFF などをサポートしているため、事実上どんなドキュメント画像でも指定できます。

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Common pitfall:** エンジンに画像を設定し忘れると、実行時に `NullReferenceException` が発生します。ファイルをロードした後は必ず `set_image` を呼び出してください。

## 手順 4: OCR の実行とテキスト抽出

エンジンの準備が整い画像が添付されたので、いよいよ **perform OCR in Python** を実行し、テキスト結果を取得できます。

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

`recognize()` メソッドは `OcrResult` オブジェクトを返し、生テキストだけでなく信頼度スコア、バウンディングボックス、言語情報も含みます。簡単な **extract text from image** のユースケースでは `get_text()` だけが必要です。

## 手順 5: 認識テキストの表示

エンジンがレシートから実際に読み取った内容を見てみましょう。

```python
print("Recognized text:\n", recognized_text)
```

典型的な出力は次のようになります：

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

出力に文字化けが含まれる場合は、OCR エンジンにロードする前に画像の前処理（例: コントラストの向上やデスキュー フィルタの適用）を検討してください。Aspose.Imaging は連結可能な画像強化ツールのフルスイートを提供しています。

## エッジケースの処理と精度向上のヒント

### 1. 極度にノイズの多いレシートへの対処

レシートが大きく汚れている場合、`OcrEngineMode.HIGH_SPEED` モードに切り替えて高速（ただし精度は低め）で処理し、クリーンアップした画像で `DEEP_LEARNING` を再度実行すると良いでしょう。

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. 言語の指定

デフォルトでは Aspose が言語を自動検出しようとします。英語のレシートの場合は以下のように固定できます：

```python
ocr_engine.set_language("eng")
```

### 3. メモリ管理

ループで多数の画像を処理する際は、リソースを明示的に解放してください：

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR 結果をファイルに保存

後で分析するために抽出したテキストを永続化したい場合があります。

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## 完全な動作例

以下はすべてを結びつけた完全なスクリプトです。`receipt_ocr.py` という名前のファイルにコピー＆ペーストし、画像パスを調整して `python receipt_ocr.py` を実行してください。

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

スクリプトを実行すると、コンソールにレシートの内容が表示され、同じデータを含む `receipt_output.txt` が作成されます。

![Python OCR チュートリアル – サンプルレシート出力](https://example.com/receipt_output.png "python ocr チュートリアル例")

*画像の代替テキスト:* **python ocr tutorial – サンプルレシート出力**

## まとめと次のステップ

ここでは **python ocr tutorial** を通じて、**load image for OCR**、**perform OCR in Python**、そして最終的に Aspose を使用して **recognize text from receipt** ファイルを認識する方法を解説しました。主なポイントは次のとおりです：

- 正しいエンジンモードを選択する（精度のために deep‑learning）
- `recognize()` を呼び出す前に必ず画像を添付する
- `OcrResult` オブジェクトを使用してクリーンなテキストを取得し、必要に応じて保存または処理する

次は何をすべきでしょうか？低コントラストのスキャンを改善するために Aspose Imaging フィルタを連結したり、スクリプトを Flask API に統合してウェブフォームからレシートをアップロードできるようにしたりしてみてください。また、会計自動化のために OCR データを CSV にエクスポートすることも検討できます。

マルチページ PDF やラテン文字以外のスクリプトの取り扱いについて質問がありますか？コメントを残してください—喜んでお手伝いします！

**Ready to level up your document automation?** コードを取得し、さまざまな画像で実験して、OCR エンジンに重い作業を任せましょう。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}