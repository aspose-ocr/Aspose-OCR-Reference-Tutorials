---
category: general
date: 2026-08-12
description: Python と Aspose AI を使用して画像の OCR を実行し、画像からテキストを抽出し、スペルチェックのポストプロセッサで OCR
  精度を向上させる。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: ja
lastmod: 2026-08-12
og_description: Pythonで画像にOCRを実行し、画像からテキストを即座に抽出し、Aspose AIのポストプロセッシングでOCR精度を向上させます。
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Pythonで画像のOCRを実行する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Pythonで画像のOCRを実行する – ステップバイステップガイド
url: /ja/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像にOCRを実行する – ステップバイステップガイド

画像ファイルに対して **OCR を実行** したい場合、このガイドはワークフロー全体を解説します。**画像からテキストを抽出** し、**OCR テキストの補正** を適用し、数行のコードだけで **OCR の精度を向上** させる方法を学びます。

スキャンした文書、領収書、スクリーンショットなどはノイズが多くなりがちです。スペルチェックのポストプロセッサを組み合わせることで、生の OCR 出力を別ツールに切り替えることなく、クリーンで検索可能なコンテンツに変換できます。このチュートリアルでは、画像の読み込みから補正結果の表示まで、必要なすべてを網羅しています。

## 前提条件

開始する前に、以下を確認してください。

* Python 3.9 以上がインストールされていること。
* Aspose.OCR と Aspose.AI の Python パッケージ（または同等のオープンソースラッパー）にアクセスできること。
* 既知のディレクトリに配置したサンプル画像（例: `sample.png`）があること。
* Python の関数やオブジェクト指向コードに基本的に慣れていること。

必要なライブラリは pip でインストールできます。

```bash
pip install aspose-ocr aspose-ai
```

> **プロのコツ:** 依存関係を分離するために仮想環境 (`python -m venv .venv`) を使用しましょう。

## Step 1: OCR エンジンインスタンスの作成

最初のステップは `OcrEngine` オブジェクトを作成することです。このオブジェクトは OCR エンジンの設定をカプセル化し、画像処理や認識のメソッドを提供します。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

エンジンを一度作成して複数の画像で再利用すると、起動オーバーヘッドが削減され、セッション全体で設定が一貫します。

## Step 2: OCR 用に画像を読み込む

認識を行う前に、エンジンは解析対象の画像を知る必要があります。`load_image` メソッドはファイルパスまたはバイナリストリームを受け取ります。

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **なぜ重要か:** 画像を正しく読み込むことが正確な OCR の基盤です。解像度が高い画像（300 dpi 以上）を使用すると、エンジンが文字をより明瞭に識別できるため、**OCR の精度が向上** します。

## Step 3: 画像からテキストを抽出 – 基本認識の実行

画像がロードされたら、`recognize()` を呼び出して結果オブジェクトを取得します。結果には生テキスト、信頼度スコア、必要に応じて各単語のバウンディングボックスが含まれます。

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

この時点で **画像に OCR を実行** し、生の文字列を抽出できました。ただし、低品質のスキャンでは誤字が含まれることがあります。

## Step 4: OCR テキスト補正 – ポストプロセッシングのスペルチェッカーを組み込む

Aspose AI は柔軟なポストプロセッシングパイプラインを提供します。カスタムスペルチェッカーを差し込むことで、典型的な OCR エラー（例: “l” と “1”、 “O” と “0”）を修正できます。

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**スペルチェッカーの仕組み:** `MySpellChecker` は `process(text: str) -> str` メソッドを実装する必要があります。内部では `pyspellchecker` や `symspellpy` といったライブラリを使用し、辞書で検証された代替語に置き換えることができます。

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Step 5: 元の OCR テキストと補正後テキストを表示

最後に、生テキストと補正後テキストを比較します。これにより、**OCR テキスト補正** が実際に **OCR の精度を向上** させたかを検証できます。

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### 期待される出力

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

補正された行では、スペルチェッカーが一般的な OCR 誤認識（`Th1s` → `This`、`s4mpl3` → `simple`、`rec3pt` → `receipt`、`som3` → `some`、`err0rs` → `errors`）を置き換えていることが分かります。

## Step 6: OCR 精度向上 – ベストプラクティスチェックリスト

ポストプロセッシングだけでなく、OCR エンジン自体のベースライン品質を高める方法もあります。

| チェックリスト項目 | 効果の理由 |
|----------------|--------------|
| **高解像度画像を使用（≥300 dpi）** | ピクセル情報が増えることで文字の曖昧さが減少します。 |
| **カラー画像をグレースケールに変換** | エンジンを混乱させる色ノイズを除去します。 |
| **画像のデスキュー（傾き補正）を適用** | 傾いた文字列を水平化し、改行エラーを防ぎます。 |
| **言語/ロケールを明示的に設定** | 認識器が正しい文字セットを選択しやすくなります。 |
| **言語モデルを有効化（ライブラリがサポートしている場合）** | 文脈を考慮した予測が可能になり、さらに **OCR の精度が向上** します。 |

これらの前処理は Pillow や OpenCV を使って画像を `ocr_engine` に渡す前に実装できます。

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## 完全に実行可能なスクリプト

すべてを統合した以下のスクリプトを `run_ocr.py` という名前で保存し、実行できます。

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

スクリプトを実行すると、元のテキストと補正後のテキストが出力され、**画像に OCR を実行**、**画像からテキストを抽出**、そして **OCR テキスト補正** を通じて **OCR の精度を向上** させたことが確認できます。

## まとめ

Python で **画像に OCR を実行** し、生テキストを抽出し、ポストプロセッシングのスペルチェッカーでクリーンな結果を得る方法が理解できました。**OCR 精度向上** のチェックリストを活用すれば、領収書、請求書、身分証明書、その他のスキャン文書にもこのワークフローを適用できます。

### 次にやること

* 多言語 OCR 用の **言語別辞書** を調査する。
* パイプラインをデータベースや検索インデックス（例: Elasticsearch）と統合し、抽出テキストを検索可能にする。
* シンプルなスペルチェッカーを、ニューラル言語モデル（例: GPT 系統の補正）に置き換えて、さらに高精度を目指す。

画像前処理手法、ポストプロセッサ、代替 OCR エンジンなどを自由に試してみてください。コアパターン—**画像に OCR を実行 → 画像からテキストを抽出 → OCR テキスト補正 → OCR の精度を向上**—は変わらないので、あらゆる文書デジタル化プロジェクトの堅牢な基盤となります。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [画像をテキストに変換: Aspose OCR (Python) を使用して画像からテキストを抽出](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Aspose OCRで画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキストを抽出 – Aspose.OCR for .NET を使用したOCR最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}