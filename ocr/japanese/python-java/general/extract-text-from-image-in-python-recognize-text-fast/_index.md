---
category: general
date: 2026-07-05
description: Python OCR を使用して画像からテキストを抽出します。画像からテキストを認識する方法、OCR 用に画像を読み込む方法、そして数行で
  OCR 言語を設定する方法を学びましょう。
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: ja
og_description: Python OCRで画像からテキストを抽出する。このガイドでは、画像からテキストを認識する方法、OCR用に画像を読み込む方法、PythonスタイルでOCRエンジンを作成する方法、そしてOCR言語を設定する方法を示します。
og_title: Pythonで画像からテキストを抽出 – テキストを高速に認識
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像からテキストを抽出 – テキストを高速に認識
url: /ja/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する Python – 高速テキスト認識

画像からテキストを**抽出**したいと思ったことはありますか？どのライブラリを選べば良いか分からない場合、外部ツールを使わずに*画像からテキストを認識する方法*を探していることでしょう。このチュートリアルでは、軽量な OCR エンジンを起動し、画像に向けてテキストを抽出します—それ以上でもそれ以下でもありません。

以下の手順を順に解説します：**create OCR engine python**、**set OCR language**、**load image for OCR**、非同期で認識を実行し、最後に結果を取得します。最後まで読むと、ドキュメントデジタライザーやミームを読むチャットボットなど、どんなプロジェクトにも組み込める自己完結型スクリプトが手に入ります。

## 必要なもの

- Python 3.8+（コードは 3.10 以降でも動作します）  
- `ocr` パッケージ（Tesseract の薄いラッパーです – `pip install ocr` またはお好みのフォークでインストール）  
- テキストが読める画像ファイル（`.jpg`、`.png` など）  
- 非同期部分のための少しの忍耐（すぐ終わります、約束）

以上です—重い依存関係もネイティブビルドも不要です。システムに Tesseract が既にインストールされていれば、`ocr` ラッパーが自動的に検出します。

## ステップ 1: OCR エンジンの作成 – 抽出の中心

まず最初に、基盤となる OCR エンジンとやり取りできるエンジンオブジェクトが必要です。後で画像を処理する「脳」と考えてください。

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Why this matters*（なぜ重要か）: エンジンがなければ言語設定や非同期機能のコンテキストがありません。`OcrEngine` クラスは Tesseract への低レベルなコマンドライン呼び出しを抽象化し、クリーンな Python API を提供します。

## ステップ 2: OCR 言語の設定 – エンジンに期待する言語を伝える

ドキュメントが英語の場合、デフォルトのままで構いませんが、明示的に設定するのがベストプラクティスです。これにより、他のロケール向けに **set OCR language** を設定する方法も示します。

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Pro tip**（プロのコツ）: 多言語 PDF の場合、`[ocr.Language.ENGLISH, ocr.Language.FRENCH]` のようなリストを渡すことができます。エンジンは自動的に両方の言語を試みます。

## ステップ 3: OCR 用画像のロード – 画像をメモリに取り込む

ここで実際に **load image for OCR** を行います。ラッパーは遅延ロードをサポートしており、エンジンが必要になるまでファイルは読み込まれません。

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Edge case*（エッジケース）: 画像が非常に大きい（5 MB 超）場合、認識を高速化するためにまずリサイズすることを検討してください。Pillow を使って次のようにできます:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## ステップ 4: 非同期認識の開始 – アプリをブロックしない

OCR の実行には数秒かかることがあります、特に大きなスキャンの場合は顕著です。`recognize_async` メソッドは後でポーリングできる future を返し、OCR がバックグラウンドで動作している間に **perform other work while OCR runs in the background** が可能です。

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

なぜ非同期か？Web サーバーでは、単一のリクエストがワーカープール全体を停止させたくありません。future オブジェクトは制御を提供し、非同期コードで `await` したり、結果が本当に必要なときだけブロックしたりできます。

## ステップ 5: 結果の取得 – 必要なときだけブロック

テキストが必要になったら `future.get()` を呼び出します。この呼び出しは **blocks only here** で、OCR が完了するまでプログラムの他の部分は応答し続けます。

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

`asyncio` ループ内にいる場合は、代わりに `await future` を使用できます – ラッパーは両方のスタイルをサポートしています。

## ステップ 6: 認識されたテキストの利用 – データが準備完了

`result` オブジェクトが取得できたので、プレーンな文字列を取り出すのは簡単です。ここではそれを出力し、ファイルに書き込む方法も示します。

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Expected output**（期待される出力） (簡略化):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

画像にテキストが含まれていない場合、`result.text` は空文字列になります—このケースは適切に処理してください。

## 完全動作例 – すべてのステップを1つのスクリプトで

以下に完全な実行可能プログラムを示します。コピーして貼り付け、`image_path` を調整すればすぐに使用できます。

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Note**（注意）: `"YOUR_DIRECTORY/large_document.jpg"` を実際の画像パスに置き換えてください。Tesseract がインストールされ `PATH` から参照できる限り、スクリプトは Windows、macOS、Linux で動作します。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| **Garbage characters**（文字化け） | 言語が間違っているか、言語データファイルが欠如している。 | `engine.language` がテキストと一致していること、対応する `.traineddata` ファイルが Tesseract の `tessdata` フォルダーに存在することを確認してください。 |
| **Slow performance on big images**（大画像での遅延） | OCR はピクセル数に比例して遅くなる。 | エンジンに渡す前にリサイズまたはダウンサンプルしてください（Pillow のコード参照）。 |
| **Future never resolves**（Future が解決しない） | 画像ファイルが破損または読めない。 | `future.get()` を try/except で囲み、認識前に `image.is_valid()` で検証してください。 |
| **Unicode loss**（Unicode の損失） |  |  |

## 次に学ぶべきことは？

以下のチュートリアルは本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースは完全なコード例とステップバイステップの解説を含み、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキストへ変換 – URL から画像に OCR を実行](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [画像からテキスト抽出 – .NET 用 Aspose OCR による OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}