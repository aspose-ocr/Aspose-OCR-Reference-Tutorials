---
category: general
date: 2026-04-26
description: OCR を迅速かつ確実に作成する方法。画像からテキストを抽出し、OCR 用に画像を読み込み、カスタム辞書を使用して PNG に対して OCR
  を実行する方法を学びます。
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: ja
og_description: PythonでOCRを作成し、画像からテキストを抽出する方法。このガイドでは、OCR用に画像を読み込む方法、PNGでOCRを実行する方法、カスタム辞書の使用方法を示します。
og_title: PythonでOCRを作成する方法 – 高速テキスト抽出
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRを作成する方法 – 画像からテキストを抽出
url: /ja/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを作成する方法 – ステップバイステップガイド

スキャンしたPDFやスクリーンショット、手書きのメモを読み取れる **OCRの作り方** を疑問に思ったことはありませんか？ あなただけではありません。実際のプロジェクトでは *画像からテキストを抽出* する必要がありますが、既成のエンジンはドメイン固有の単語でつまずくことが多いです。

このチュートリアルでは、OCR用に画像を読み込み、カスタム辞書を適用し、最終的に **PNGファイルでOCRを実行** する完全な実行可能例をご紹介します。最後まで読むと、任意の画像からテキストを抽出し、エンジンを自分の用語に合わせてカスタマイズできるようになります。

## このチュートリアルでカバーする内容

* 小さくても強力な `aocr` パッケージ（または互換性のあるライブラリ）をインストールする。  
* `aspocorp` や `licensekey` のような用語が認識されるように **カスタム辞書** を設定する。  
* PNG、JPEG、またはスキャンしたPDFページなど、**OCR用に画像を読み込む**。  
* OCRプロセスを実行し、結果を出力する。  

外部ドキュメントへのリンクはなく、今日すぐにコピー＆ペーストして実行できる自己完結型のソリューションです。

### 前提条件

* Python 3.8 以上（コードは f‑string を使用）。  
* コマンドラインの基本的な知識 – `pip install` コマンドを数回入力します。  
* 参照できる場所に配置した画像ファイル（例では `technical_doc.png`）。

上記の3項目を満たしていれば、すぐに始められます。

---

## ステップ1: OCRライブラリのインストール

まず、プログラム可能な設定オブジェクトをサポートするOCRエンジンが必要です。`aocr` パッケージはネイティブOCRエンジンの軽量ラッパーで、デモに適しています。

```bash
# Install the library (run once)
pip install aocr
```

> **プロのコツ:** Windowsでコンパイルエラーが出た場合は、事前ビルド済みのホイールが含まれる `pip install aocr‑binary` を試してください。

### なぜこのライブラリをインストールするのか？

`aocr` は `config` オブジェクトへの直接アクセスを提供し、そこに **カスタム辞書** を注入できます。これがニッチな語彙の精度向上の秘訣です。

---

## ステップ2: OCRエンジンインスタンスの作成とカスタム辞書の追加

ここでエンジンを起動し、既知として扱う単語を指定します。

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### カスタム辞書が重要な理由

標準的なOCRモデルは汎用コーパスで訓練されています。モデルが “aspocorp” を見ると “aspo corp” に分割したり、文字を抜き落としたりすることがあります。カスタムリストを提供することで、認識器を必要な正確なスペルにバイアスさせ、後処理の手間を大幅に削減します。

---

## ステップ3: 処理したい画像の読み込み

ここで **OCR用に画像を読み込む** ことを行います。`Image.load` メソッドはパス文字列を受け取り、ファイルタイプを自動的に判別します。

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **エッジケース:** ソースが複数ページのPDFの場合、まず各ページをPNGに変換（例: `pdf2image` 使用）し、エンジンに1ページずつ渡してください。

### 画像品質向上のヒント

* 解像度は最低でも300 dpiに保つ。  
* 画像が正しい向きであることを確認し、必要なら `Pillow` で回転させる。  
* カラースキャンはグレースケールに変換してノイズを減らす。

---

## ステップ4: PNGファイルでOCRプロセスを実行

エンジンの設定と画像の読み込みが完了したら、最終的に **PNGでOCRを実行** します。

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()` 呼び出しは、認識されたテキスト、信頼度スコア、各単語のバウンディングボックスを含むオブジェクトを返します。

---

## ステップ5: 認識テキストの出力

エンジンが見つけた内容を確認する最も簡単な方法は、`text` 属性を出力することです。

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### 期待される出力

`technical_doc.png` に文 *“The Aspocorp licensekey expires on 2025‑12‑31.”* が含まれている場合、コンソールには次のように表示されます:

```
The Aspocorp licensekey expires on 2025-12-31.
```

カスタム辞書がブランド名をそのまま保持していることに注目してください。標準のOCRでは文字化けしていた可能性があります。

---

## 完全動作例（コピー＆ペースト準備完了）

以下は全スクリプトで、`run_ocr.py` として保存できます。プレースホルダーのパスを画像の場所に置き換えるだけです。

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

ターミナルから実行してください:

```bash
python run_ocr.py
```

先ほどの例と同様に、抽出されたテキストがコンソールに表示されるはずです。

---

## よくある質問 (FAQ)

| Question | Answer |
|----------|--------|
| **スキャンしたPDFからテキストを抽出できますか？** | はい。各ページをまずPNG（またはTIFF）に変換し、同じスクリプトに画像を渡してください。 |
| **画像がPNGではなくJPEGの場合はどうしますか？** | `Image.load` メソッドはJPEG、BMP、TIFF、PNGを標準でサポートしています。ファイル拡張子を変更するだけです。 |
| **コントラストが低いスキャンの精度を上げるには？** | `Pillow` で前処理 – コントラストを上げ、二値化を適用するか、`opencv` で傾きを補正してください。 |
| **各単語の信頼度スコアを取得する方法はありますか？** | `ocr_result` には `words` が含まれており、各単語は `confidence` 属性を持つので反復処理できます。 |
| **ヘッドレスサーバーで実行できますか？** | もちろんです。`aocr` はGUI依存がなく、CIパイプラインに最適です。 |

---

## 次のステップと関連トピック

**OCRの作り方** と **画像からテキストを抽出** できるようになったので、以下を検討してください:

* **前処理技術** – `load image for OCR` は最初のステップに過ぎません。`opencv` を使ってノイズ除去やシャープ化を行いましょう。  
* **バッチ処理** – PNGディレクトリをループして検索可能なアーカイブを生成します。  
* **多言語サポート** – フランス語やドイツ語の文書を読む必要がある場合、エンジンに言語パックを追加します。  
* **Elasticsearchとの統合** – 抽出したテキストをインデックス化し、スキャン資産全体の全文検索を可能にします。  

これらの拡張はすべて、先ほど説明したコアパターン上に構築されているため、移行はスムーズです。

---

## まとめ

数分で、特にPNGファイルに対して信頼性の高い **OCRの作り方** と **画像からテキストを抽出** する方法を解説し、**OCR用に画像を読み込む**、**カスタム辞書を適用する**、そして **PNGでOCRを実行** する手順を外部サービスなしで示しました。

スクリプトを試し、辞書を自分の専門用語に合わせて調整すれば、あらゆる文書デジタル化プロジェクトの堅実な基盤が手に入ります。

問題が発生した場合は下にコメントを残してください—喜んでサポートします。また、成功事例を共有することを忘れずに。コミュニティは実例から最も学びます。

**書類の自動化を始めませんか？** コードを取得し、適応させて、今日からピクセルを検索可能なテキストに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}