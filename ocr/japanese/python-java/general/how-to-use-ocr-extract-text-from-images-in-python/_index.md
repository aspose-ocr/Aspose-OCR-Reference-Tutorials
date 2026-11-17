---
category: general
date: 2026-03-18
description: 画像からテキストを抽出するOCRの使い方 – PNGファイルのテキスト認識とOCR用画像の読み込みに関するクイックガイド
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: ja
og_description: OCRを使用して画像からテキストを抽出する方法 – PNGからテキストを認識し、OCR用に画像を読み込み、シンプルなPythonスクリプトでテキストを抽出する方法を学びましょう。
og_title: OCRの使い方：Pythonで画像からテキストを抽出する
tags:
- OCR
- Python
- Image Processing
title: OCRの使い方：Pythonで画像からテキストを抽出する
url: /ja/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR の使い方: Python で画像からテキストを抽出する

スクリーンショットが乱雑だったり、スキャンしたレシートがあったりして **OCR の使い方** が気になったことはありませんか？ あなたは一人ではありません。開発者はモバイルアプリやウェブアップロードから来る PNG などの画像から可読テキストを取り出す必要があります。このチュートリアルでは、**画像からテキストを抽出** し、**PNG からテキストを認識** し、さらに **OCR 用に画像をロード** する方法を、数行の Python だけで実行できる完全なサンプルを順を追って解説します。

必要なライブラリのインストールから多言語文書の取り扱いまで網羅しますので、最後まで読めばどんな画像でもエンジンに投げ込んで *テキストを抽出する方法* が分かります。曖昧な説明はなく、コピー＆ペーストしてすぐに走らせられる明確なステップバイステップの解決策を提供します。

## 学べること

次のセクションで行うことは以下の通りです。

1. 軽量な OCR エンジンをセットアップ（重い依存関係は不要）。  
2. 画像ファイル、特に PNG をエンジンにロード。  
3. 自動言語検出を有効にし、多言語コンテンツに対応。  
4. 認識プロセスを実行し、プレーンテキスト結果を取得。  
5. ファイルが見つからない、サポート外フォーマットなどのエッジケースに対処。

基本的な Python が扱える方ならすぐに始められます。OCR の事前知識は不要ですが、ライブラリのドキュメントをざっと見るとさらに理解が深まります。

---

![PNG 画像で OCR を使用する方法](placeholder.png "PNG 画像で OCR を使用する方法 – ステップバイステップガイド")

## OCR の使い方 – 画像をロードしてテキストを認識する {#how-to-use-ocr}

### 手順 1: OCR ライブラリをインストール

まず最初に、`OcrEngine` クラスを提供する Python パッケージが必要です。このチュートリアルでは、架空ですが分かりやすい **SimpleOCR** パッケージを使用します。pip でインストールできます。

```bash
pip install simple-ocr
```

> **プロのコツ:** 仮想環境（強く推奨）で作業している場合は、インストールコマンドを実行する前に環境をアクティブにしてください。これによりプロジェクトの依存関係が整理されます。

### 手順 2: エンジンをインポートしてインスタンスを作成

エンジンの作成はコンストラクタを呼び出すだけです。エンジンは後で画像を処理する「脳」のようなものです。

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

なぜ毎回新しいインスタンスを作るのか？ それは **分離** のためです。新しいエンジンは前回の実行から残った状態が現在の認識に影響しないことを保証し、バッチ処理時に重要です。

### 手順 3: 処理したい画像をロード

ここで実際に **OCR 用に画像をロード** します。`setImageFromFile` メソッドは任意のラスタ画像へのパスを受け取り、ここでは `mixed_doc.png` という PNG を指定します。

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

ファイルが見つからない場合、`SimpleOCR` は明確な `FileNotFoundError` を投げます。以下のようにキャッチしてフレンドリーなエラーメッセージを出すことができます。

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### 手順 4: 自動言語検出を有効化

最新の OCR エンジンは言語パックを同梱しています。`"multilingual"` を渡すことで、エンジンはテキストを嗅ぎ取り自動で適切な言語モデルを選択します。たとえば PNG に英語とスペイン語が混在している場合に便利です。

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

事前に言語が分かっている場合は、`"multilingual"` を `"eng"` や `"spa"` といった特定のロケールに置き換えることで処理速度を向上させられます。

### 手順 5: 認識プロセスを実行

ここが本番です。`recognize()` が画像をスキャンし、セグメンテーションを行い、ニューラルネットを走らせ、内部でテキストバッファを構築します。

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

内部でエンジンが行うこと:

- **前処理**（デスキュー、二値化）  
- **レイアウト解析**（列やテーブルの検出）  
- **文字分類**（ディープラーニングモデル使用）  

これらはすべて抽象化されているため、コードはたった一行で済みます。

### 手順 6: 認識結果のテキストを取得して表示

最後に結果オブジェクトを取得し、プレーン文字列を抽出します。ここが実際に **画像からテキストを抽出** する部分です。

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**期待される出力**（簡略化）:

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

画像に認識可能な文字が全く含まれない場合、`text` は空文字列になります。その場合に備えて以下のようにガードできます。

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## 画像からテキストを抽出 – よくあるエッジケースの対処

### 1 ファイル内で複数言語を扱う場合

文書に複数言語が混在しているときは、通常 `"multilingual"` 設定でうまくいきます。しかし、認識ミスが目立つ場合はフォールバックリストを手動で指定できます。

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### 2 PNG 以外のフォーマット

**PNG からテキストを認識** に焦点を当てていますが、`SimpleOCR` は JPEG、BMP、TIFF も受け付けます。`setImageFromFile` の拡張子を変更するだけです。TIFF スタックの場合は特定のページを選択する必要があります。

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### 3 大容量ファイルとメモリ使用量

ギガピクセル級のスキャンを処理する場合は、OCR 前にリサイズを検討してください。

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

リサイズすることでメモリ負荷を減らしつつ、認識に十分なディテールは保持できます。

### 4 ロード失敗のデバッグ

目視では問題なさそうでも内部で破損している画像があります。詳細ログを有効にしてエンジンが何を見ているか確認しましょう。

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## 完全版・実行可能スクリプト

以下は全体をまとめたプログラムです。`ocr_demo.py` という名前で保存し、`YOUR_DIRECTORY` プレースホルダーを適切に置き換えてから `python ocr_demo.py` を実行してください。

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

このスクリプトを走らせると、`mixed_doc.png` の中身がプレーンテキストとして出力されます。別の画像に差し替えても **テキスト抽出の方法** は同じです。

---

## まとめ

ここまでで、Python で **OCR の使い方** を学び、**画像からテキストを抽出** する方法、特に **PNG からテキストを認識** する手順と **OCR 用に画像をロード** する実践的な流れを体験しました。上記スニペットは自己完結型のソリューションです: パッケージをインストールし、ファイルを渡し、多言語検出を有効にし、エンジンを走らせ、結果を取得するだけです。

ここからは次のような応用が考えられます:

- ユーザーアップロードを受け付ける Web サービスにスクリプトを組み込む。  
- PNG に変換した PDF フォルダをバッチ処理する。  
- 正規表現によるクレンジングやスペルチェックなどの後処理を追加して精度を向上させる。

OCR の品質は画像の鮮明さ、適切な言語パック、時には前処理に依存します。ぜひ実験してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}