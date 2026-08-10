---
category: general
date: 2026-06-25
description: Python を使用して OCR 用に画像を前処理し、スキャンした文書からテキストを認識します。フルコード付きのステップバイステップチュートリアル。
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: ja
og_description: PythonでOCR用に画像を前処理し、スキャンした文書からテキストを認識します。詳細で実行可能なチュートリアルをご覧ください。
og_title: PythonでOCR用画像前処理 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRのための画像前処理 – 完全ガイド
url: /ja/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCR用画像前処理 – 完全ガイド

**OCR用画像前処理** を行って、テキストをきれいで信頼性の高い形で取得したいと思ったことはありませんか？ あなただけではありません—スキャンしたページが歪んでいたり、コントラストがばらばらだったりすると、ほとんどの開発者が同じ壁にぶつかります。朗報は、数行の Python でその混乱を整列させ、画像を二値化し、鮮明で検索可能なテキストを手に入れられることです。

このチュートリアルでは、**OCR用画像前処理** と **スキャンした文書からテキストを認識** する正確な手順を、一般的な OCR ライブラリを使って解説します。最後まで読むと、すぐに実行できるスクリプトが手に入り、各設定がなぜ重要かを理解し、難しいケースに合わせて調整できるようになります。

## 必要なもの

- Python 3.8 以降（コードは 3.10+ でも動作します）
- `OcrEngine`、`ImagePreProcessingOptions`、`Image` クラスを提供する OCR パッケージ（例として本稿で使用している架空の `ocr` モジュール）
- 多少傾いている、またはコントラストが低いスキャン画像または撮影画像
- お好きな IDE もしくはシンプルなターミナル—重い GUI は不要です

以上です。余計なバイナリや Docker の設定は不要です。さっそく始めましょう。

## OCR用画像前処理 – ステップバイステップ

以下はコアワークフローを 5 つの明確な段階に分けたものです。各段階には **なぜ** 行うのか、正確な **コード**、そして裏で何が起きているかを示す簡単な **説明** が含まれます。

### Step 1: OCR エンジンインスタンスの作成

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:*  
`OcrEngine` オブジェクトは処理全体の頭脳です。言語パックや信頼度閾値、そして何よりも画像前処理フラグといった設定を保持します。最初にインスタンス化することで、後続のトリックを有効にするためのクリーンな状態が得られます。

### Step 2: 自動デスキューと二値化を有効化

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Why this matters:*  
- **Deskewing（デスキュー）** は画像を回転させ、テキスト行を水平にします。ベースラインが数度以上傾いていると OCR エンジンは苦戦します。  
- **Binarization（二値化）** は画像を純粋な白黒に変換し、文字分類器を混乱させる背景ノイズを除去します。  
多くの最新ライブラリではこれらのオプションは *自動* ですが、明示的にオンにする必要があります。

> **Pro tip:** 画像がすでに完全に整列している場合は、`auto_deskew=False` に設定して処理時間を数ミリ秒削減できます。

### Step 3: 処理したい歪んだ画像を読み込む

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Why this matters:*  
`Image.load` メソッドはファイルをメモリに読み込み、OCR エンジンが理解できるオブジェクトにラップします。また DPI などのメタデータも取得し、デスキューのデフォルトスケーリング係数に影響を与えることがあります。

> **Edge case:** 画像がマルチページ TIFF の場合は、各ページをイテレートするか `ocr.MultiPageImage.load` のようなヘルパーを使用してください。前処理設定はすべてのページに同じように適用されます。

### Step 4: 前処理済み画像で OCR を実行

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Why this matters:*  
この時点でエンジンは先ほど有効にしたデスキューと二値化のステップを適用し、クリーンなビットマップ上でニューラルネットワーク（または従来の Tesseract スタイルパイプライン）を走らせます。返される `result` オブジェクトには通常、プレーンテキスト、信頼度スコア、場合によっては各単語の位置情報が含まれます。

> **What if the text is still garbled?**  
画像解像度を確認してください：OCR は 300 dpi 以上で最も効果的に動作します。元画像がそれ以下の場合は、読み込む前にアップスケールするか、元のスキャンを提供元に依頼しましょう。

### Step 5: 認識結果テキストの出力

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Why this matters:*  
`result.text` はエンジンが読み取れたすべてのテキストを文字列として表したものです。デバッグ時にすぐに表示できるのは便利です。実際のアプリでは `.txt` ファイルやデータベースに書き込んだり、下流の NLP パイプラインに渡したりすることが多いでしょう。

---

## スキャン文書からテキストを認識 – 基本を超えて

基本パイプラインが動作したら、実際の環境で **スキャン文書からテキストを認識** する際に遭遇しやすいバリエーションをいくつか見ていきましょう。

### 1. 複数言語の扱い

文書に英語とフランス語が混在している場合は、Step 1 の前にエンジンを設定します：

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

ほとんどの OCR エンジンは ISO‑639‑2 コードを受け付けます。追加の言語パックを読み込むと若干のオーバーヘッドは発生しますが、多言語ページの精度は劇的に向上します。

### 2. 二値化閾値の微調整

自動二値化は多くの場合で機能しますが、古いコピーはカスタム閾値が必要です：

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

背景が消えるが文字が消えないように、120〜220 の範囲で値を試してみてください。

### 3. レイアウト情報の抽出

単なるテキストだけでなく、各段落がページ上のどこにあるか知りたいことがあります。多くのエンジンは `result.blocks` コレクションを提供しています：

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

テーブルの再構築や列順の保持に非常に役立ちます。

### 4. ファイルバッチ処理

スキャンした PDF を JPEG に変換したフォルダがある場合は、全体の流れをループで包みます：

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

ループは同じ `engine` インスタンスを再利用するため、ファイルごとにインスタンスを作り直すよりも効率的です。

### 5. 低解像度スキャンへの対処

解像度が 150 dpi 未満の画像は文字がぼやけがちです。簡単な対策は、OCR エンジンに渡す前に高品質アルゴリズムでアップスケールすることです：

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

アップスケールでディテールが魔法のように増えるわけではありませんが、二値化ステップがより鮮明なエッジで動作し、多少の改善が期待できます。

---

## 期待される出力

中程度に傾き、300 dpi のスキャン画像で元の 5 ステップスクリプトを実行すると、次のような出力が得られるはずです：

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

文字化けが見られる場合は、前処理フラグ、画像解像度、言語設定を再確認してください。

---

## 結論

Python を使って **OCR用画像前処理** と **スキャン文書からテキストを認識** するために必要なすべてを網羅しました。新しいエンジンインスタンスを作成し、自動デスキューと二値化を有効化し、歪んだ画像を読み込み、認識を実行し、クリーンなテキストを出力しました。その過程で多言語対応、手動閾値調整、レイアウト抽出、バッチ処理、低解像度対策も紹介しました。

自分のスキャン（レシートの山、手書きフォーム、古い新聞の切り抜きなど）でスクリプトを試してみてください。慣れたら PDF 生成や検索インデックスへの投入など、さらに機能を拡張してみましょう。可能性は無限です。

**次のチャレンジに備えましたか？** *「Extract Tables from Scanned PDFs with Python」* と *「Train Custom OCR Models with TensorFlow」* のチュートリアルをチェックして、ドキュメント自動化ツールボックスを拡充してください。

Happy coding, and may your OCR always be crisp!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}