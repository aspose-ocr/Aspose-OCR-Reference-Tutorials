---
category: general
date: 2026-03-26
description: PythonでOCRを実行し、画像からテキストを簡単に抽出したり、スキャンからテキストを読み取ったり、請求書からテキストを抽出したりする方法を、シンプルなOcrEngineを使って学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: ja
og_description: PythonでOCRを実行する方法は？このガイドでは、画像からテキストを抽出し、スキャンからテキストを読み取り、数分で請求書からテキストを抽出する方法を示します。
og_title: PythonでOCRを実行する方法 – テキストを高速で抽出
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRを実行する方法 – テキストを高速に抽出
url: /ja/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを実行する方法 – テキストを高速抽出

スキャンしたレシートやぼやけたPDFで **OCRの実行方法** を疑問に思ったことはありませんか？ あなただけではありません。多くのプロジェクトで **画像からテキストを抽出** する必要が早い段階で出てきますが、従来の「すべて手入力」アプローチはスケールしません。  

このチュートリアルでは、**OCRの使い方** を示す完全で実行可能な例をご覧いただけます。スキャンからテキストを読み取り、請求書からデータを取得し、さらには自動傾き補正も処理します—すべてPython数行で実現できます。

## 学習内容

以下の内容を順に解説します：

* 必要な依存関係とインポートの正確な一覧。
* `OcrEngine` インスタンスの作成と設定方法。
* 同じエンジンを使用して **画像からテキストを抽出**、**スキャンからテキストを読み取る**、および **請求書からテキストを抽出** する方法。
* 一般的な落とし穴（言語設定ミス、ファイル欠如、大きな画像）とその回避策。
* OCRが成功したことを確認できる期待出力。

外部ドキュメントへのリンクは不要です—すべてが自己完結しているので、コードをコピー＆ペーストすればすぐに結果が確認できます。

## 前提条件

始める前に以下を確認してください：

* Python 3.8+ がインストールされていること（`ocr` パッケージは最新バージョンで動作します）。
* `ocr` ライブラリが利用可能であること（`pip install ocr‑engine` – 実際のパッケージ名が異なる場合は置き換えてください）。
* 処理したい画像ファイル – デモでは `YOUR_DIRECTORY` フォルダー内の `invoice.png` を使用します。

以上です。これらが揃っていれば、すぐに始められます。

## ステップ 1: OCRモジュールのインストールとインポート

まず最初に、OCRライブラリが必要です。まだインストールしていない場合は、ターミナルで以下のコマンドを実行してください：

```bash
pip install ocr-engine
```

次に、スクリプトでモジュールをインポートします。

```python
# Step 1: Import the OCR module
import ocr
```

> **プロのコツ:** 仮想環境を整理整頓しておくと、後で他の画像処理パッケージを追加した際のバージョン衝突を防げます。

## ステップ 2: OCRエンジンの作成と設定

エンジンの作成はコンストラクタを呼び出すだけで簡単ですが、真の力は正しく設定することにあります。言語を英語に設定し、自動傾き補正を有効にします。これは、スキャンした請求書が完全に整列していない場合に必須です。

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

`auto_skew` を有効にする理由は何ですか？ 多くのスキャナは数度の傾きがある画像を生成します。補正がなければエンジンは文字を見逃し、読みやすい請求書が読めない文字列になってしまいます。

## ステップ 3: 対象画像でOCRを実行する

ここで画像ファイルをエンジンに渡します。`recognize_image` メソッドは、生テキストと信頼度スコア（ライブラリが提供している場合）を保持するオブジェクトを返します。

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

**スキャンからテキストを読み取る** シナリオの場合は、パスをスキャンしたPDFをPNGまたはJPEGに変換したものに置き換えるだけです。同じ呼び出しは、基盤となるライブラリがサポートする任意の画像形式で機能します。

## ステップ 4: 抽出されたテキストの確認と利用

生のOCR出力を表示してみましょう。実際の請求書処理パイプラインでは、この文字列を解析して項目、合計、日付などを抽出するでしょうが、ここでは簡単に目視でOCRが成功したことを確認します。

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**期待出力（簡略化）:**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

出力が文字化けしている場合は、画像が鮮明かつ `engine.language` が文書の言語と一致しているか再確認してください。

## ステップ 5: 一般的なエッジケースの処理

### 大きな画像

5000 × 5000 ピクセルのスキャンを処理するとメモリを大量に消費します。対策として、エンジンに送る前に画像を縮小するのが手早い方法です：

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### 複数言語

画像に英語とスペイン語の両方が含まれる場合、**画像からテキストを抽出** するために言語リストを設定できます：

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

エンジンは両方の文字セットを認識しようとします。

### エラーハンドリング

ファイルが存在することを前提にしないでください。呼び出しを try‑except ブロックでラップし、親切なメッセージを提供します：

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## ビジュアルリファレンス

以下はデモで使用したサンプル請求書のスクリーンショットです。わずかな傾きに注目してください—まさに `auto_skew` が修正するポイントです。

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* 自動傾き補正を示す請求書画像でOCRを実行する様子

## 完全実行可能な例

すべてをまとめた、コマンドラインから実行できる単一スクリプトをご紹介します。インストール、設定、エラーハンドリング、抽出したテキストを `output.txt` というファイルに書き込むシンプルな後処理ステップが含まれています。

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

`python full_ocr_demo.py` を実行すると、抽出されたテキストがコンソールに表示され、`output.txt` に保存されます。そこから正規表現やCSVライター、その他 **請求書からテキストを抽出** の自動化に必要なロジックを適用できます。

## 結論

これで、Pythonで **OCRの実行方法** に対する確実なエンドツーエンドの解決策が手に入りました。`OcrEngine` を作成し、言語と傾き補正を設定し、いくつかの実用的なエッジケースに対処することで、散在するドキュメントを探さずに **画像からテキストを抽出**、**スキャンからテキストを読み取る**、そして **請求書からテキストを抽出** を信頼性高く行えます。

次は何をすべきでしょうか？ ファイルをバッチでループ処理したり、異なる言語を試したり、出力をPDF生成ライブラリに組み込んで検索可能なPDFを作成したりしてみてください。可能性は無限で、今回のコードは堅実な出発点です。

特定のファイル形式について質問がある、または信頼度閾値の調整が必要ですか？ 下にコメントを残してください—OCRパイプラインの微調整を喜んでお手伝いします！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}