---
category: general
date: 2026-06-25
description: PythonでPNGからテキストを認識する：OCRエンジンを作成するステップバイステップガイド、技術文書にOCRを実行し、技術文書画像からテキストを抽出する。
draft: false
keywords:
- recognize text from png
- ocr image to text python
- create OCR engine python
- extract text from technical document image
- run OCR on technical document
language: ja
og_description: PythonでPNG画像からテキストを認識します。OCRエンジンの作成方法、技術文書にOCRを実行して画像からテキストを抽出する手順を学びましょう。
og_title: PythonでPNG画像からテキストを認識する – 完全OCRエンジンチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  headline: Recognize Text from PNG in Python – Complete OCR Engine Guide
  type: TechArticle
- description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  name: Recognize Text from PNG in Python – Complete OCR Engine Guide
  steps:
  - name: Low‑Resolution Images
    text: 'If the PNG originates from a scanned fax, you might be dealing with 72
      dpi. OCR accuracy drops dramatically below 150 dpi. A quick fix is to upscale
      the image using a bicubic algorithm before recognition:'
  - name: Rotated Pages
    text: 'Technical manuals sometimes come scanned at an angle. The engine can auto‑deskew,
      but you can also pre‑rotate:'
  - name: Multi‑Page Documents
    text: 'When you need to **run OCR on technical document** PDFs that have been
      exported to PNG per page, wrap the logic in a loop:'
  - name: Language Selection
    text: 'Aspose OCR defaults to English, but you can switch to other languages (e.g.,
      German) by loading the appropriate language pack:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: PythonでPNGからテキストを認識する – 完全OCRエンジンガイド
url: /ja/python-java/general/recognize-text-from-png-in-python-complete-ocr-engine-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを認識する Python – 完全なOCRエンジンガイド

PNGファイルから**テキストを認識**したいことはありませんか？どのPythonライブラリを選べば良いか迷っていませんか？あなたは一人ではありません。スキャンしたマニュアルをデジタル化したり、製品ラベルからシリアル番号を抽出したり、技術文書画像からデータを取り出したりする場合、信頼できるOCRパイプラインは手作業でのコピーペーストに費やす時間を大幅に削減できます。

このチュートリアルでは、**OCRエンジン python を作成**し、PNGを入力として**技術文書画像からテキストを抽出**するハンズオン例をステップバイステップで解説します。最後まで実施すれば、品質がさまざまな**技術文書に対して OCR を実行**する方法が分かり、次のプロジェクトで使える再利用可能なスクリプトが手に入ります。

## 学べること

- Python OCR ライブラリのインストールとセットアップ（Aspose OCR を使用しますが、手順はほとんどの最新 OCR パッケージに共通です）。  
- **OCRエンジン python** のインスタンスを作成し、ドメイン固有用語のカスタム辞書を設定。  
- PNG画像を読み込み、OCR を実行して**png からテキストを認識**する方法。  
- 低解像度、回転ページ、ノイズの多い背景といった一般的な落とし穴への対処法。  
- スクリプトを拡張して複数の技術文書をバッチ処理。

> **前提条件** – Python 3.8+ がインストールされており、pip の基本操作が分かっていて、機械可読テキストを含む PNG 画像が用意できていること。OCR の事前知識は不要です。

---

## Step 1: Install the OCR Library (Create OCR Engine Python)

まずは実際に処理を行うライブラリが必要です。Aspose OCR for Python via .NET は商用オプションで、箱から出すだけで高精度を実現しますが、`pytesseract` のようなオープンソース代替でも同様のパターンが使えます。例を自己完結させるため、ここでは Aspose OCR を使用します。

```bash
pip install aspose-ocr
```

> **プロのコツ:** Windows で権限エラーが出た場合は、管理者権限で PowerShell を起動するか、コマンド末尾に `--user` を付けて実行してください。

インストールが完了したら、モジュールをインポートしてエンジンを起動します。

```python
import aspose.ocr as ocr
```

この 1 行のインポートで `OcrEngine` クラスにアクセスでき、**OCR エンジン python の作成**の基礎が整います。

## Step 2: Initialize the OCR Engine and Tune It (Run OCR on Technical Document)

次にエンジンをインスタンス化し、必要に応じてカスタム辞書を設定します。カスタム辞書は OCR が有効な単語として扱う語彙リストで、技術用語や製品コード、社内略語に最適です。

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: define a custom dictionary for domain‑specific terms
engine.custom_dictionary = [
    "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
]
```

なぜ辞書が必要か？たとえば「SKU‑12345」というコードが頻出する保守マニュアルをスキャンしたとします。辞書が無いと OCR は「S K U‑12345」や「SKU‑12345」と誤認識する可能性があります。`custom_dictionary` にこの語を追加すれば、**ocr image to text python** の精度が大幅に向上します。

## Step 3: Load the PNG Image (Extract Text from Technical Document Image)

続いて、**png からテキストを認識**したい画像を読み込みます。Aspose OCR は多数の画像形式に対応していますが、PNG はロスレス品質を保つ点で優れた選択肢です。

```python
# Step 3: Load the image file
image_path = "YOUR_DIRECTORY/technical_doc.png"
image = ocr.Image.load(image_path)
```

PNG が極端に大きい（例：スキャンした設計図）場合は、OCR 前に縮小してメモリ使用量を抑えることをおすすめします。

```python
# Optional downscale for huge images
max_dim = 2000  # pixels
if max(image.width, image.height) > max_dim:
    scale = max_dim / max(image.width, image.height)
    image = image.resize(int(image.width * scale), int(image.height * scale))
```

## Step 4: Perform the OCR (OCR Image to Text Python)

エンジンと画像の準備ができたら、実際の認識は以下の 1 行で完了します。

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize(image)
```

内部では `engine.recognize` が二値化、デスキュー、レイアウト解析といった前処理を順に実行し、クリーン化されたビットマップをニューラルネットワークに渡します。そのため、**技術文書に対して OCR を実行**する際にも、単純なスクリプトで高い成功率が得られます。

## Step 5: Output the Recognized Text (Recognize Text from PNG)

最後に抽出したテキストを出力します。ファイルに書き出したり、データベースに保存したり、 downstream の NLP パイプラインに渡したりすることも可能です。

```python
# Step 5: Output the recognized text
print("=== OCR Result ===")
print(result.text)
```

有効な PNG でスクリプトを実行すると、次のような出力が得られます。

```
=== OCR Result ===
Invoice #2026
Product: AsposeOCR SDK
SKU-12345
Total: $1,299.00
```

> **画像例**  
> ![recognize text from png output](images/ocr_result.png)  
> *Alt text:* *recognize text from png – コンソールに表示されたサンプル OCR 結果。*

このスクリーンショットは、カスタム辞書のおかげで製品コードが正しく保持されたクリーンな抽出結果を示しています。

---

## Deeper Dive: Handling Common Edge Cases

### Low‑Resolution Images

PNG がファックスのスキャンから来ていて 72 dpi しかない場合、150 dpi 未満では OCR 精度が大幅に低下します。認識前にバイキュービックアルゴリズムで画像を拡大すると効果的です。

```python
if image.dpi < 150:
    image = image.resize(image.width * 2, image.height * 2, interpolation=ocr.InterpolationMode.BICUBIC)
```

### Rotated Pages

技術マニュアルは角度が付いたままスキャンされることがあります。エンジンは自動デスキュー機能を持ちますが、事前に回転させても構いません。

```python
# Detect and correct rotation
angle = engine.auto_rotate(image)
if angle != 0:
    image = image.rotate(-angle)
```

### Multi‑Page Documents

**技術文書に対して OCR を実行**する PDF がページごとに PNG にエクスポートされている場合、以下のようにループで処理します。

```python
import glob

for png_path in sorted(glob.glob("pages/*.png")):
    img = ocr.Image.load(png_path)
    txt = engine.recognize(img).text
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write(f"--- Page {png_path} ---\n{txt}\n\n")
```

### Language Selection

Aspose OCR のデフォルトは英語ですが、言語パックを読み込むことで他言語（例：ドイツ語）に切り替えられます。

```python
engine.language = ocr.Language.German
```

多言語の表や仕様書が含まれる**技術文書画像からテキストを抽出**する際に便利です。

---

## Full Working Script

以下は全体をまとめた実行可能スクリプトです。`ocr_technical_doc.py` として保存し、`YOUR_DIRECTORY/technical_doc.png` を対象の PNG パスに置き換えてください。

```python
#!/usr/bin/env python3
"""
Full example: recognize text from png using Aspose OCR for Python.
Demonstrates creating OCR engine python, custom dictionary, and
handling common image issues.
"""

import os
import aspose.ocr as ocr

def configure_engine():
    """Create and configure the OCR engine."""
    engine = ocr.OcrEngine()
    # Custom dictionary improves recognition of domain‑specific terms
    engine.custom_dictionary = [
        "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
    ]
    return engine

def load_image(path):
    """Load PNG and apply optional preprocessing."""
    if not os.path.isfile(path):
        raise FileNotFoundError(f"Image not found: {path}")

    img = ocr.Image.load(path)

    # Downscale huge images
    max_dim = 2000
    if max(img.width, img.height) > max_dim:
        scale = max_dim / max(img.width, img.height)
        img = img.resize(int(img.width * scale), int(img.height * scale))

    # Upscale low‑dpi images
    if img.dpi < 150:
        img = img.resize(img.width * 2, img.height * 2,
                         interpolation=ocr.InterpolationMode.BICUBIC)

    # Auto‑deskew if needed
    angle = engine.auto_rotate(img)
    if angle != 0:
        img = img.rotate(-angle)

    return img

def run_ocr(engine, image):
    """Perform OCR and return the result object."""
    return engine.recognize(image)

def main():
    # ---- Step 1: Initialize OCR engine ----
    global engine
    engine = configure_engine()

    # ---- Step 2: Load the PNG image ----
    png_path = "YOUR_DIRECTORY/technical_doc.png"
    img = load_image(png_path)

    # ---- Step 3: Run OCR ----
    result = run_ocr(engine, img)

    # ----


## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を試したりする際に役立ちます。

- [Aspose OCR で画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose OCR を使用したストリームからの画像テキスト抽出方法](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [画像を URL から取得して OCR を実行 – Image to Text 変換](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}