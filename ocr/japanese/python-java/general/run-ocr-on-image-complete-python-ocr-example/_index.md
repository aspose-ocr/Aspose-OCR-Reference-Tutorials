---
category: general
date: 2026-03-18
description: Pythonで画像のOCRを素早く実行する。PNGからテキストを認識し、OCR用に画像を読み込み、画像から単語を抽出する手順をステップバイステップで学べます。
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: ja
og_description: Pythonを使って画像のOCRを実行します。このチュートリアルでは、PNGからテキストを認識し、OCR用に画像を読み込み、画像から単語を抽出する方法を、完全なコード例とともに紹介します。
og_title: 画像でOCRを実行 – Pythonガイド
tags:
- OCR
- Python
- Image Processing
title: 画像でOCRを実行 – 完全なPython OCR例
url: /ja/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行する – 完全な Python OCR 例

画像で **run OCR on image** が必要だったことはありますか？しかし、どこから始めればよいか分からないことも多いでしょう。あなたは一人ではありません。多くの開発者がスキャンした文書からテキスト抽出に取り組む際に同じ壁にぶつかります。このチュートリアルでは、**Python OCR example** を通じて、**recognize text from PNG** ファイル、**load image for OCR**、そして **extract words from image** を信頼度スコアと共に数行のコードで実行する方法を紹介します。

必要なライブラリ、エンジンの設定方法、各ステップの重要性、出力の形状など、必要な情報をすべてカバーします。最後まで読めば、このスニペットを自分のプロジェクトに貼り付けるだけで、任意の画像から即座にテキストを抽出できるようになります。余計な説明は省き、実用的で実行可能なソリューションを提供します。

## 必要なもの

- Python 3.8 以上がインストールされていること  
- `ocrengine` パッケージ（または `OcrEngine` クラスを提供する任意のライブラリ）。`pip install ocrengine` でインストールできます。`pytesseract` など別の OCR ライブラリを使用する場合は名前を調整してください。  
- 処理したい画像ファイル（PNG、JPG など）— 本ガイドでは `invoice.png` を使用します。  

![画像で OCR を実行する例（スキャンされた請求書）](/images/run-ocr-on-image.png)

*Alt text: 画像で OCR を実行する例 – スキャンされた請求書が処理中*

## Step 1 – OCR ライブラリのインストールとインポート

まず最初に、OCR エンジンを環境に導入し、インポートしましょう。仮想の `ocrengine` パッケージを使用している場合、インポートは次のようになります。

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Why this matters:** 正しいクラスをインポートすることで、後で呼び出す `setImageFromFile` や `recognize` といったメソッドにアクセスできます。このステップを省略すると、Python は `ModuleNotFoundError` を投げ、画像を読み込む前に止まってしまいます。

## Step 2 – OCR エンジンインスタンスの作成

ライブラリの準備ができたので、認識プロセスの設定と状態を保持するエンジンオブジェクトが必要です。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* 一部の OCR エンジンでは、この段階で言語モデルや DPI 設定を調整できます。基本的な **python OCR example** ではデフォルトで問題ありませんが、低解像度のスキャンを扱う場合はここで調整することを検討してください。

## Step 3 – 処理したい画像の読み込み

次の論理的なステップは **load image for OCR** です。エンジンに解析したい PNG（またはサポートされている任意の形式）のファイルパスを指定します。

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**What’s happening under the hood?** エンジンはピクセルデータを読み取り、認識アルゴリズムが理解できる形式に変換し、内部に保存します。ファイルパスが間違っていると `FileNotFoundError` が発生するので、画像が存在することを再確認してください。

## Step 4 – 認識アルゴリズムの実行

画像が読み込まれたら、ようやく **run OCR on image** を実行してテキストコンテンツを抽出します。

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

この時点でエンジンはビットマップをスキャンし、パターンマッチングを適用し、検出されたすべての単語、行、信頼度メトリックを含むオブジェクトを返します。

## Step 5 – 認識された単語を反復処理し、信頼度を表示

OCR ワークフローで最も有用な部分は、抽出された各トークンの **the confidence** を確認することです。エンジンが各単語にどれだけ自信を持っているかを示し、必要に応じて低信頼度の結果をフィルタリングできます。

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Expected output** (sample):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

これで **what words were extracted from the image** が正確に確認でき、各検出の信頼性が分かります。これはあらゆる **extract words from image** パイプラインの核心です。

## Handling Common Edge Cases

### 画像がグレースケールの場合は？

一部の OCR エンジンはカラー画像の方が性能が良いです。全体的に信頼度が低い場合は、エンジンに渡す前に PNG を高コントラストの白黒画像に変換してみてください。Pillow が役立ちます。

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### 複数言語への対応

文書に英語とスペイン語の両方が含まれる場合、マルチリンガルモデルを使用して **recognize text from PNG** したいでしょう。多くのエンジンでは初期化時に言語リストを設定できます。

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### 低信頼度単語のフィルタリング

場合によっては、信頼度が 90 % 以上の単語だけが必要になることがあります。簡単なフィルタは次のようになります。

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## 完全な実行可能スクリプト

すべてをまとめると、以下の単一スクリプトをコピー＆ペーストしてすぐに実行できます（PNG のパスを置き換えるだけです）。

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

実行方法:

```bash
python run_ocr_on_image.py
```

コンソールに単語リストと信頼度パーセンテージが、先ほどの例と同様に出力されます。

## よくある質問

**Does this work with JPG or TIFF files?**  
絶対に対応しています。`setImageFromFile` メソッドは基盤となるライブラリがデコードできる任意の形式を受け入れるため、JPG、TIFF、BMP などの **run OCR on image** ファイルでも使用できます。

**Can I process multiple images in a loop?**  
もちろんです。ファイルパスのリストに対して `for` ループで読み込みと認識のステップをラップしてください。ライブラリが画像ごとに新しいインスタンスを必要とする場合は、エンジンを再初期化することを忘れずに。

**What if I need the text in a single string instead of per‑word?**  
ほとんどの OCR 結果オブジェクトは、全文書を返す `getText()` メソッドを提供しています。例:

```python
full_text = ocr_result.getText()
print(full_text)
```

## 次のステップと関連トピック

**run OCR on image** の方法が分かったので、以下を検討してください：

- **Post‑processing**: 正規表現を使用して、請求書から抽出した日付、金額、ID などをクリーンアップします。  
- **Batch processing**: `os.listdir()` と組み合わせて、スキャンされた文書のフォルダ全体を処理します。  
- **Alternative libraries**: `pytesseract` は人気のあるオープンソースオプションです。ワークフローは似ているので、エンジン呼び出しを置き換えるだけです。  
- **Exporting results**: 抽出した単語と信頼度スコアを CSV に書き出し、下流の分析に利用します。

これらの拡張はすべて、ここで築いた基盤の上に直接構築され、未加工の OCR データを実用的な情報へと変換できます。

### TL;DR

簡潔な **python OCR example** を示し、**load image for OCR**、**run OCR on image**、**extract words from image** を信頼度と共に実演しました。完全なスクリプトはすぐに実行可能で、**recognize text from PNG**（または他の形式）が必要な任意のプロジェクトに適用できる知識が得られました。ぜひ試してみて、信頼度閾値を調整し、数分でアプリケーションをテキスト認識対応にしましょう。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}