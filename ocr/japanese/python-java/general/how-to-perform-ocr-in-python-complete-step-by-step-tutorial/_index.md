---
category: general
date: 2026-03-26
description: PythonでOCRを実行し、画像ファイルからテキストを認識する方法を学びましょう。このガイドでは、PNGからテキストを抽出し、画像を素早くテキストに変換する手順を示します。
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: ja
og_description: PythonでOCRを実行する方法は？このガイドに従って画像からテキストを認識し、PNGからテキストを抽出し、トライアルライセンスで画像をテキストに変換しましょう。
og_title: PythonでOCRを実行する方法 – 完全チュートリアル
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRを実行する方法 – 完全ステップバイステップチュートリアル
url: /ja/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを実行する方法 – 完全ステップバイステップチュートリアル  

スマートフォンで撮影した画像で **OCRを実行する方法** を知りたくなったことはありませんか？ あなたは一人ではありません—世界中の開発者が、複雑なネイティブライブラリと格闘せずに画像ファイルからテキストを認識する信頼できる方法を必要としています。  

このチュートリアルでは、軽量な Python ラッパーを使用して **OCRを実行する方法**、**画像からテキストを認識**、そして **PNGからテキストを抽出** するハンズオン例を順に解説します。最後まで読むと、数行のコードで **画像をテキストに変換** できるようになり、ビルトインのトライアルモードを使用するためライセンスに関する頭痛も回避できます。

## 学習できること  

* OCR エンジンのトライアルライセンスを設定する方法（ファイルパスは不要）。  
* **画像からテキストを認識** するための正確な呼び出し順序。  
* **PNGからテキストを抽出** する方法と、フォントが欠如している場合などの一般的な落とし穴への対処法。  
* トライアルから本番ライセンスへ移行する際のスケーリングに関するヒント。  

**前提条件** – Python 3.8 以上と `ocr` パッケージ（`pip install ocr` でインストール可能）が必要です。その他の外部ツールは不要です。

---  

![OCR実行例](https://example.com/ocr-demo.png "PythonでOCRを実行 – 認識されたテキストが表示")  

*画像の代替テキスト: PythonでOCRを実行 – サンプル出力*  

## Step 1 – トライアルライセンスを有効化（ファイルパス不要）  

エンジンが何かを読み取る前に、有効なライセンスが必要です。トライアルモードは実験や小規模プロジェクトに最適です。

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* ライセンスオブジェクトは OCR ライブラリに対しサンドボックスで動作していることを伝えます。このステップを省略すると、`recognize()` を呼び出した瞬間に `LicenseError` が発生します。  

**Pro tip:** 有料ライセンスに切り替える際は、上記の2行を `ocr.License("path/to/your/license.key").apply()` に置き換えてください。

## Step 2 – OCR エンジンインスタンスを作成  

トライアルが有効になったので、メインエンジンをインスタンス化します。これは画像を見て文字がどこにあるかを判断する「脳」のようなものです。

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* `OcrEngine` は言語パックや DPI 設定などの構成情報を保持します。後から調整可能ですが、デフォルト設定でほとんどの英語のみの PNG に対しては問題なく動作します。

## Step 3 – 処理したい PNG を読み込む  

ここで **画像からテキストを認識** します。`ocr.Imaging.Image.load()` メソッドは PNG、JPEG、BMP、その他いくつかのフォーマットをサポートしています。

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* PNG がインデックスカラー（スクリーンショットで一般的）の場合、ローダーは自動的に 24 ビット RGB バッファへ変換します。この変換は若干のパフォーマンス低下を招くことがありますが、正確な OCR 結果を保証します。

## Step 4 – OCR を実行してテキストを取得  

最後にエンジンに処理を指示し、プレーンテキストの結果を取得します。

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Expected output**（「Hello World」だけが書かれたシンプルな画像の例）:

```
Hello World
```

画像に複数行が含まれる場合、出力は改行を保持するため、CSV パーサーや NLP パイプラインなどの下流プロセスにそのまま渡すことが容易です。

## Optional: 精度向上のための微調整  

* **Language packs:** `ocr_engine.set_language("eng")`（デフォルト）またはフランス語の場合は `"fra"`。  
* **DPI scaling:** `ocr_engine.set_dpi(300)` は低解像度スキャンの結果を改善できます。  
* **Pre‑processing:** `set_image` の前にバイナリ閾値 (`ocr.Imaging.Image.threshold()`) を適用すると、ノイズの多い背景でもテキストがクリアに抽出されやすくなります。

これらの調整は、簡易デモから 1 日数百ファイルを処理する本格的な **ocr tutorial python** に移行する際に有用です。

## Full Script – コピー＆ペースト用の完成スクリプト  

以下は上記すべての手順を組み合わせた、実行可能な完全スクリプトです。`run_ocr.py` として保存し、`YOUR_DIRECTORY/sample1.png` を自分の PNG のパスに置き換えてください。

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

コマンドラインから実行します:

```bash
python run_ocr.py
```

コンソールに抽出されたテキストが表示されます。空文字列が返ってきた場合は、画像に明瞭で高コントラストなテキストが含まれているか、トライアルライセンスがエラーなく適用されたかを再確認してください。

## Common Questions & Gotchas  

* **「JPEG でも動作しますか？」** – はい。`load()` メソッドはフォーマットを自動検出するため、コードを変更せずに PNG から JPEG に差し替えられます。  
* **「画像が回転している場合は？」** – エンジンは向きを自動検出しますが、最高の結果を得るには `set_image` の前に `input_image.rotate(90)` で事前に回転させても構いません。  
* **「ループで複数画像を処理できますか？」** – できます。`for` ループ内にロードと `recognize()` 呼び出しを移動すれば、同じ `ocr_engine` インスタンスを再利用でき、わずかなオーバーヘッド削減につながります。  

## Next Steps – デモから本番へ  

今や **OCRを実行する方法** が分かったので、以下のトピックを検討してください:

* **バッチ処理** – このスクリプトと `os.listdir()` を組み合わせて、**PNGからテキストを抽出** する作業を一括で行う。  
* **PDF との統合** – `pdf2image` を使って PDF ページを PNG に変換し、同じパイプラインに流し込む。  
* **ポストプロセッシング** – 正規表現やファジーマッチングを適用して、一般的な OCR 誤認（例: “0” と “O”）をクリーンアップする。  

これらはすべて **画像をテキストに変換** というコアアイデアに基づいており、OCR ワークフローの有用性を大幅に拡張します。

---  

### TL;DR  

Python で **OCRを実行する方法** に必要なすべてを網羅しました：トライアルライセンスの有効化、エンジンの作成、PNG のロード、認識の実行、結果の出力。数行のコードで **画像からテキストを認識**、**PNGからテキストを抽出**、そして **画像をテキストに変換** でき、あらゆる下流アプリケーションに活用できます。  

ぜひ試してみて、DPI や言語設定を調整しながらエンジンに任せてみてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}