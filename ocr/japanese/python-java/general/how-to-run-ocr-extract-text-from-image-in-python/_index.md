---
category: general
date: 2026-03-26
description: PNGファイルに対してOCRを実行し、カスタム辞書を使用して画像からテキストを抽出し、OCR精度を向上させる方法。OCR用に画像を素早く読み込む方法を学びましょう。
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: ja
og_description: PNGファイルでOCRを実行し、カスタム辞書を使用して画像からテキストを抽出し、OCR精度を向上させる方法。ステップバイステップガイド。
og_title: OCRの実行方法 – Pythonで画像からテキストを抽出する
tags:
- OCR
- Python
- Image Processing
title: OCRの実行方法 – Pythonで画像からテキストを抽出する
url: /ja/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR の実行方法 – Python で画像からテキストを抽出する

スキャンした請求書やスクリーンショットで **OCR の実行方法** を考えたことがありますか？きれいで検索可能なテキストを取得したいですよね。あなたは一人ではありません。多くのプロジェクトでボトルネックになるのは、単に画像を OCR 用に読み込んで、エンジンにドメイン固有の単語を理解させることです。

このチュートリアルでは、**画像からテキストを抽出** する完全な実行可能サンプルを順に解説し、**PNG からテキストを認識** する方法を示し、さらにカスタム辞書や特殊文字を使って **OCR の精度を向上** させるコツも紹介します。最後まで読むと、任意の Python コードベースに組み込める自己完結型スクリプトが手に入ります。

## 必要なもの

- Python 3.8+（コードは型ヒントを使用していますが、以前の 3.x バージョンでも動作します）
- ターゲットとする OCR エンジンに同梱されている `ocr` ライブラリ（`pip install ocr‑engine` でインストールしてください – 実際のパッケージ名に置き換えてください）
- 処理したい画像ファイル（`input.png`）
- 任意: ドメイン固有の単語を1行ずつ記載したプレーンテキストファイル（`invoice_terms.txt`）

重い外部依存関係も、クラウド API キーも不要で、ローカルの OCR エンジンだけです。

---

## ステップ 1: OCR ライブラリのインストールとインポート

まず、OCR パッケージがインストールされていることを確認してください。仮想的な `ocr-engine` パッケージを使用している場合、次のコマンドを実行します：

```bash
pip install ocr-engine
```

次に、必要なクラスをインポートします：

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **プロのコツ:** 仮想環境を使用している場合、インストール前に環境をアクティブにして、グローバルな Python を汚染しないようにしましょう。

## ステップ 2: OCR エンジンインスタンスの作成

エンジンオブジェクトを作成することは、すべての OCR タスクのエントリーポイントです。ソフトウェア上でスキャナハードウェアをオンにするイメージです。

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

これが重要な理由: エンジンは言語パックや認識モード、後で追加するカスタムリソースなどの設定を保持します。これがなければ、**OCR 用に画像を読み込む** ことも認識パイプラインを実行することもできません。

## ステップ 3: 認識したい画像を読み込む

ここでは実際に **OCR 用に画像を読み込む** ことを行います。`Imaging.Image.load()` メソッドはファイルを読み取り、エンジンが期待する内部ビットマップ形式に変換します。

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

JPEG や TIFF でも同じメソッドが使えます—拡張子を変更するだけです。エンジンは自動的にフォーマットを検出します。

> **エッジケース:** 非常に大きな画像（5 MP 超）はメモリ使用量が急増することがあります。パフォーマンスに問題が出た場合は、読み込む前に Pillow で縮小することを検討してください。

## ステップ 4: カスタム辞書を提供して精度を向上させる

多くの OCR エンジンは汎用的な言語モデルを搭載しています。請求書、領収書、法的文書などでは、しばしば単語が抜け落ちます。カスタム単語リストを提供することで、エンジンに「これらの用語は正当であり、正しいものとして扱う」よう指示できます。

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

典型的なエントリは次のようになります:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

これらを追加すると、**OCR の精度向上** 指標が劇的に改善されます—特に非 ASCII 記号に対して効果的です。

## ステップ 5: デフォルトセットに含まれない特殊文字を追加する

ドメインでユーロ記号 (€) やスカンジナビア文字 Ø のような記号を使用する場合、明示的に追加できます:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

エンジンは認識フェーズでこれらのグリフを有効とみなし、「ゴミ」出力になる可能性を減らします。

## ステップ 6: OCR プロセスを実行しテキストを取得する

最後に、認識器を呼び出してプレーンテキストの結果を取得します。`recognize()` 呼び出しはリッチなオブジェクトを返しますが、ほとんどのユースケースでは生の文字列だけが必要です。

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**期待される出力**（簡略化）:

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

出力が文字化けしている場合は、カスタム辞書と特殊文字が正しくロードされているか再確認してください。

---

## ビジュアル概要

![how to run OCR diagram](ocr-workflow.png){alt="OCR の実行フロー図"}

上の図は、画像の読み込みからクリーンなテキスト取得までのフローを示し、カスタム辞書や文字セットを挿入できるポイントをハイライトしています。

---

## よくある質問と落とし穴

### マルチページ PDF でも動作しますか？

はい—各ページを PNG に変換（`pdf2image` などを使用）し、同じ `ocr_engine` インスタンスに順次渡すだけです。エンジンは各画像を独立して処理するため、連結可能な文字列のリストが得られます。

### 画像が回転している場合は？

最新の OCR エンジンはほとんどが向きを自動検出しますが、次のように強制的に回転させることもできます:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### 英語以外の言語を扱うには？

画像を読み込む前に言語モデルを切り替えます:

```python
ocr_engine.set_language("de")  # German
```

対応する言語パックがインストールされていることを確認してください。

---

## 完全スクリプト – コピー＆ペースト用

以下は全体のプログラムです。プレースホルダーのパスを置き換えればすぐに実行できます。

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

次のコマンドで実行します:

```bash
python run_ocr.py
```

コンソールに抽出されたテキストが表示されるはずです。その後、ファイルに書き出したり、データベースに投入したり、下流の NLP パイプラインに渡したりできます。

---

## まとめと次のステップ

PNG に対して **OCR の実行方法**、**画像からテキストを抽出** する方法、そして辞書やカスタム文字を用いて **OCR の精度を向上** させながら **PNG からテキストを認識** する実践的な手法をカバーしました。

次に、以下を検討してください:

- **バッチ処理:** 画像ディレクトリをループ処理する。
- **後処理:** 正規表現を使って請求書番号や日付を抽出する。
- **統合:** スクリプトを Flask API に組み込み、オンデマンドの OCR サービスを提供する。

より高度なトピックに興味がある場合は、OpenCV 前処理を用いた **OCR 用に画像を読み込む** チュートリアルや、LSTM 層を備えた Tesseract 4+ などのディープラーニングベースの OCR モデルを調べてみてください。

---

### 実験を続けよう！

`invoice_terms.txt` を医療用語リストに差し替えたり、ギリシャ文字を追加したり、低解像度の写真をエンジンに入力して精度がどこまで伸びるか試してみてください。試行回数が増えるほど、前処理、カスタム語彙、エンジン設定間のトレードオフを深く理解できるようになります。

コーディングを楽しんで、OCR の結果が常に鮮明でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}