---
category: general
date: 2026-07-05
description: 画像の傾きを素早く補正する方法。OCRのための画像前処理、画像の回転補正、そしてPythonでスキャンをテキストに変換する方法を学びましょう。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: ja
og_description: 画像の傾きを補正し、OCR用に前処理する方法。このガイドでは、画像の回転を修正し、Pythonを使用して画像からテキストを抽出する手順を示します。
og_title: 画像の傾き補正方法 – ステップバイステップ OCR 前処理
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: 画像の傾き補正方法 – OCR前処理の完全ガイド
url: /ja/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 – OCR 前処理の完全ガイド

Ever wondered **how to deskew image** files that look like they were taken from a crooked scanner?  You’re not the only one.  In many real‑world projects the first thing you have to do before you can **extract text from image** is straighten that wobble.  

このチュートリアルでは、**OCR 用画像前処理** を行い、回転を修正し、最終的に Python OCR ライブラリを使用して **スキャンをテキストに変換** するハンズオンのエンドツーエンド例を解説します。曖昧な説明はなく、コピー＆ペーストできる動作スクリプトと、よくある落とし穴に関するヒントを提供します。  

## 本チュートリアルで得られること

* 少し傾いたスキャンした JPEG または PNG を読み込む。  
* デスクエンジフィルタと二値化ステップを適用して OCR の精度を向上させる。  
* OCR エンジンを実行し、**画像からテキストを抽出** を確実に行う。  
* 下流のテキスト抽出において **正しい画像回転** が重要な理由を理解する。  

### 前提条件

* マシンに Python 3.9 以上がインストールされていること。  
* `ocr` 名前空間を模倣した pip でインストール可能な OCR パッケージ（例: Tesseract の薄いラッパー）。  
* Python の関数と画像処理の概念に関する基本的な知識。  

これらが揃っていれば、さっそく始めましょう。

![how to deskew image example](deskew_before_after.png){alt="画像の傾き補正 – 補正前後"}

## ステップ 1: OCR エンジンのセットアップ – Python で画像の傾き補正を行う

まず最初に、ドキュメントの言語を理解できる OCR エンジンが必要です。以下のスニペットは、エンジンを作成し、英語テキストを扱うことを指定する最小限のボイラープレートを示しています。

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Why this matters:* エンジンの言語設定は使用する文字セットと辞書に影響します。このステップを省略すると、特に **画像回転を正しく補正** した後で、OCR が一般的な単語を誤認識する可能性があります。

## ステップ 2: 直したいスキャン画像を読み込む

ここでファイルをメモリに読み込みます。`"YOUR_DIRECTORY/skewed_scan.jpg"` をご自身の画像へのパスに置き換えてください。

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

画像がすでに NumPy 配列や OpenCV の `Mat` である場合は、ローダーをそれに合わせて調整できます。重要なのは、後で使用する `apply_filter` メソッドをオブジェクトが持っていることです。

## ステップ 3: OCR 用画像前処理 – デスクエンジと二値化

ここが魔法の場所です。2 つのフィルタを連結します：

1. **Deskew** – 画像内の支配的なテキストベースラインを自動検出し、画像を水平に戻すように回転させます。  
2. **Binarize (Otsu)** – 画像を純粋な白黒に変換し、認識率を劇的に向上させます。

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tip:* 二値化後にテキストがまだぼやけて見える場合は、コントラストを調整するか、別の閾値処理手法を試してください。`ocr.Filter` モジュールには、より厳しいケース向けに `adaptive_threshold()` が含まれていることが多いです。

## ステップ 4: OCR を実行 – 画像からテキストを抽出

クリーンでまっすぐに補正されたキャンバスをエンジンに渡します。結果オブジェクトには認識された文字列、信頼度スコア、必要に応じてバウンディングボックスも含まれます。

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

典型的な出力例は次のようになります：

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

改行が完璧に揃っているのが分かりますか？ これは **正しい画像回転** の利点で、OCR が行の向きを推測する必要がなくなります。

## ステップ 5: すべてをまとめる – スキャンをテキストに変換する単一ファイルスクリプト

以下は、これまで説明したすべての要素を組み合わせた完全な実行可能スクリプトです。`deskew_ocr.py` として保存し、`python deskew_ocr.py` を実行してください。

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### なぜこれが機能するのか

- **Deskew first** – 二値化の前に画像を回転させることで、閾値アルゴリズムが水平な画像で動作します。  
- **Binarize after deskew** – Otsu 法は二峰性ヒストグラムを前提としますが、傾いたページではこの前提が崩れます。  
- **English language model** – OCR に期待すべき文字を伝え、偽陽性を減らします。

他の言語に対応する場合は、`ocr.Language.ENGLISH` を該当する enum に置き換えるだけです。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| *スキャンが逆さまの場合はどうしますか？* | `deskew()` フィルタは通常 180° の回転も検出します。失敗した場合は、デスクエンジ前に `apply_filter(ocr.Filter.rotate(180))` を呼び出してください。 |
| *文書にカラーグラフィックが含まれています – 二値化で消えてしまいますか？* | はい。混在コンテンツの場合は、`ocr.Filter.deskew()` のみを使用し、カラー画像のまま OCR を実行することを検討してください。グラフィックを保持しながらテキストは抽出できます。 |
| *複数ファイルをバッチ処理できますか？* | ロジックをループで包み、リストから各ファイルパスを読み取り、各 `result.text` を別々の `.txt` ファイルに保存します。 |
| *低解像度スキャンの精度を上げるには？* | デスクエンジ前にバイキュービックフィルタで画像を拡大し、その後シャープフィルタを適用します。ピクセル数が増えることで OCR エンジンにより多くの手がかりが提供されます。 |

## ボーナス: デスクエンジの視覚的検証

ビフォーアフターを横並びで確認したい場合は、簡単な Matplotlib スニペットを追加してください：

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## 結論

本稿では **画像の傾き補正方法**、**OCR 用画像前処理** が重要である理由、そして **画像からテキストを抽出** して最終的に **スキャンをテキストに変換** する方法を解説しました。ワークフロー（load → deskew → binarize → recognize）は、OCR がクリーンでまっすぐなページを認識できるようにし、精度向上と手動修正の削減につながります。

次に OCR の旅で挑戦すべきは？ 以下を試してみてください：

- 異なる言語パック（`ocr.Language.FRENCH` など）。  
- レイアウト解析ステップを追加して、列やテーブルを検出する。  
- PDF ライブラリを使用して OCR 結果を検索可能な PDF にエクスポートする。

問題が発生したら遠慮なくコメントを残すか、特に頑固なスキャンを処理するための独自の工夫を共有してください。コーディングを楽しんで、画像が常に完璧に水平でありますように！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースは、完全な動作コード例とステップバイステップの解説を含み、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [AspOCR の使い方: .NET 用画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR を使用した C# の画像テキスト抽出（言語選択）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像の OCR 方法 – OCR 画像認識で画像に OCR を実行](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}