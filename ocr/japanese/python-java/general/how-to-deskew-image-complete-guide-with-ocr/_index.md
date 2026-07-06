---
category: general
date: 2026-03-26
description: 画像の傾きを補正し、画像からテキストを認識し、スキャンのノイズを除去してスキャン画像をテキストに変換する画像前処理パイプラインの構築方法を学びましょう。
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: ja
og_description: 画像の傾きを補正し、歪んだスキャンを検索可能なテキストに変換する方法。このガイドに従って画像からテキストを認識し、スキャンのノイズを除去し、スキャン画像をテキストに変換しましょう。
og_title: 画像の傾き補正方法 – ステップバイステップ OCR ガイド
tags:
- OCR
- image-processing
- Python
title: 画像の傾き補正方法 – OCR 完全ガイド
url: /ja/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 – OCR 完全ガイド

安価なスキャナーから出力された画像の **how to deskew image** が気になったことはありませんか？ページが歪んでいると見た目がプロフェッショナルでなくなるだけでなく、傾きが原因で **recognize text from image** を試みる OCR エンジンが正しく動作しなくなります。

このチュートリアルでは、スキャン画像を傾き補正し、二値化し、ノイズ除去を行う **image preprocessing pipeline** を順に解説し、最終的に OCR エンジンに渡して **convert scanned image to text** を最小限の手間で実現する方法を紹介します。魔法は使いません、純粋な Python と重い処理を担う小さなライブラリだけです。

## 必要なもの

- Python 3.9+（コードは 3.10 以降でも動作します）
- `ocr` パッケージ（`pip install ocr‑toolkit` でインストール – 実際のライブラリ名に置き換えてください）
- 明らかに傾いているスキャン画像（例: `skewed_scan.jpg`）
- 各前処理ステップが何のためにあるかに対する少しの好奇心

以上です。OpenCV のような重い依存関係は不要です（後で深掘りしたい場合を除く）。

## Step 1: Load the Scanned Image

最初にファイルをメモリに読み込みます。このステップはシンプルですが重要です。パスが間違っていると以降すべてがクラッシュします。

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Why?**  
> 画像を読み込むことで、`ocr.ImagePreprocessor` が操作できるオブジェクトが得られます。このステップを省略すると、パイプラインは実際のピクセルデータを認識できません。

## How to Deskew Image and Prepare It for OCR

画像が手元にあるので、次は傾きを補正します。`deskew()` メソッドが傾き角度を推定し、画像を水平に戻します。

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** スキャンがわずかにずれているだけ（≤ 3°）の場合、デフォルトアルゴリズムで十分です。極端な角度の場合は内部パラメータを調整する必要があります – `max_angle` のドキュメントを確認してください。

## Binarize the Image – Make It Black‑and‑White

OCR エンジンは高コントラストの入力を好みます。画像を二値（白黒）に変換することで、文字認識を妨げる微妙な色調を除去します。

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **What’s happening?**  
> ピクセル値が 128 より明るい部分は白に、その他は黒に変換されます。スキャンが特に暗いまたは明るい場合はしきい値を調整してください。

## Remove Noise from Scan Before OCR

完璧に傾き補正された画像でも、斑点やほこり、圧縮アーティファクトが残ることがあります。これらの小さなブロブは OCR エンジンにとって大敵です。

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Why remove noise?**  
> ノイズは偽のエッジを生成し、OCR エンジンが文字と誤認識する原因になります。ほとんどのスキャンでは小さな半径で十分です。粒子が多い文書の場合は半径を上げてください。

## Apply the Image Preprocessing Pipeline

設定がすべて揃ったので、元画像に対してパイプラインを実行します。

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Result:** `processed_image` はクリーンで水平、高コントラストなビットマップとなり、テキスト抽出の準備が整います。

## Recognize Text from Image with OCR Engine

いよいよテキストを読み取ります。OCR エンジンを初期化し、加工した画像を渡して生の文字列を取得します。

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Expected output** (sample):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

文字化けが見られる場合は、傾き補正ステップを再確認するか、別の `threshold` 値で実験してください。

## Building an Image Preprocessing Pipeline – Full Script

すべてをまとめた、単一の実行可能スクリプトを以下に示します。`.py` ファイルに保存して実行できます。

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** 多数のファイルをバッチ処理する場合は、全体を関数（`def ocr_from_file(path): …`）でラップすると便利です。

## Common Questions & Edge Cases

- **画像がすでに正立している場合は？**  
  `deskew()` メソッドはほぼゼロの角度を検出すると画像をそのままにします。すべてのファイルに対して安全に実行できます。

- **スキャンがカラー画像なのですが、保持すべきですか？**  
  多くの OCR タスクではカラーは価値を提供しません。二値化でカラー情報は除去され、処理速度が向上しメモリ使用量も削減されます。

- **複数の前処理ステップをチェーンできますか？**  
  もちろんです。`ImagePreprocessor` クラスはパイプライン向けに設計されており、`sharpen()`、`contrast_enhance()`、またはカスタムフィルタを `apply()` 前に追加できます。

- **OCR 出力に不要な改行が入っている – どう対処する？**  
  `text.replace("\n", " ").strip()` で後処理するか、Tesseract の `--psm` モードなど高度なレイアウト解析ライブラリを利用してください。

## Next Steps

**how to deskew image** と **image preprocessing pipeline** の基礎が身についたので、次のような応用を検討できます。

- Flask API に **recognize text from image** を組み込み、ドキュメントのオンザフライアップロードを実現する。
- 歴史的文書の **remove noise from scan** にパイプラインを活用し、保存性を高める。
- 数千ページをバッチ処理し、`pdfminer` や `PyMuPDF` を使って検索可能な PDF を生成する。

しきい値やデノイズ半径を変えてみたり、必要に応じて OCR バックエンドを Tesseract に切り替えて多言語対応にするなど、自由に実験してください。基本は変わりません：傾き補正 → クリーンアップ → 読み取り。

---

*Happy coding! 問題が発生したら下のコメント欄に書き込んでください。パイプラインの微調整を喜んでお手伝いします。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}