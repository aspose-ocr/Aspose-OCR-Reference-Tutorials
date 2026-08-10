---
category: general
date: 2026-06-28
description: Pythonで自動回転、二値化、ノイズ除去を行いOCR用に画像を前処理します。OCRエンジンを使用して構造化されたJSON出力を取得します。
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: ja
og_description: Pythonで自動回転、二値化、ノイズ除去を行い画像をOCR用に前処理します。OCRエンジンを使って構造化されたJSONを抽出する方法を学びましょう。
og_title: OCR用画像前処理 – 完全Pythonガイド
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR用画像前処理 – 完全Pythonガイド
url: /ja/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像前処理 – 完全 Python ガイド

画像を **preprocess image for OCR** して、エンジンが実際に見える文字を読めるようにしたいと思ったことはありませんか？ あなたは一人ではありません。多くの開発者が、スキャンした文書が文字化けしている壁にぶつかります。朗報は、いくつかの適切な手順—自動回転、二値化、ノイズ除去—で、乱れた写真をクリーンで機械が読めるテキストに変えることができるということです。

このチュートリアルでは、画像をクリーニングし、整然とした JSON ファイルを返す **Python** ワークフローを順に解説します。最後まで読むと、OCR 用に画像を自動回転させる方法、OCR 用画像の二値化を適用する方法、そして **OCR engine Python** インスタンスに渡す前に OCR 画像データのノイズ除去を行う方法が分かります。

## 必要なもの

作業を始める前に、以下がマシンにインストールされていることを確認してください。

- Python 3.9+（最近のバージョンならどれでも可）
- 画像処理用 `Pillow`（`pip install pillow`）
- OCR エンジンをラップする架空のユーティリティライブラリ `ocrutil`（`pip install ocrutil`）
- サンプルの傾いた画像（`skewed.jpg`）を参照できるフォルダーに配置

以上です—重厚なフレームワークも GPU も不要です。純粋な Python と便利なライブラリだけで完結します。

## Step 1: Load Your Image – Preparing for OCR

まず最初に、パイプライン全体で扱える画像オブジェクトを取得します。

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*このステップが重要な理由:* Pillow で画像を読み込むことで、後で二値化を行う際に必要な元のピクセルデータをすべて保持できます。低品質のローダーを使うと、OCR の精度がすでに損なわれる恐れがあります。

## Step 2: Auto‑rotate the Image for OCR (auto rotate image OCR)

スマートフォンで撮影した写真は、傾いていたり逆さまだったりすることが多いです。`ocrutil.auto_rotate` ヘルパーはテキストのベースラインを検出し、画像を自動で回転させます。

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*プロのコツ:* 文書が常に正立していることが分かっている場合はこのステップを省略できますが、実務では “auto rotate image OCR” が手作業の手間を大幅に削減します。

## Step 3: Preprocess Image for OCR – Binarization + Denoising

ここが本題です： **preprocess image for OCR**。最も効果的な 2 つのテクニックは次の通りです。

1. **二値化** – 画像を純粋な白黒に変換し、文字のエッジを際立たせます。  
2. **ノイズ除去** – OCR エンジンが文字と勘違いしやすい斑点を取り除きます。

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

このステップの後に画像を確認すると（例: `img.show()`）、背景とのコントラストがはっきりと上がっているはずです。これこそが優れた OCR エンジンが欲しがる状態です。

## Step 4: Set Up the OCR Engine (OCR engine Python)

クリアな画像が手に入ったら、OCR エンジンを初期化します。`ocrutil.OcrEngine` クラスは、Tesseract などのオープンソース OCR バックエンドをラップし、使いやすい Python API を提供します。

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*この処理の意図:* 前処理済み画像を **OCR engine Python** オブジェクトに渡すことで、エンジンが提供できる最高品質のデータで動作し、精度が直接向上します。

## Step 5: Plain‑text Recognition (Optional but Handy)

時には生のテキストだけが欲しいこともあります。このステップはオプションです。チュートリアルの主目的は構造化出力ですが、簡易的な検証には便利です。

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

元の文書に近い文字列が出力されますが、レイアウト情報は失われています。文字化けしている場合は、前処理パラメータを調整してください。

## Step 6: Extract Structured Data and Save as JSON (OCR structured JSON output)

最新の OCR エンジンはレイアウト情報（テーブル、カラム、フォームフィールド）も返すことができます。`engine.recognize_structured()` がそれを実現し、結果を整然とした JSON ファイルにダンプします。

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

JSON の一部は次のようになります。

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*得られるもの:* データベース、API、レポートツールにそのまま投入できる機械可読形式です。手作業でのコピペは不要です。

## Bonus: Visual Confirmation (Image with Alt Text)

以下は前後のパイプライン結果を比較したスナップショットです。コントラストが上がり、ノイズが消えていることが確認できます。

![OCR 用画像前処理 – オリジナル vs クリーン](/images/ocr_preprocess_example.png){: .align-center alt="preprocess image for OCR example"}

*興味がある方へ:* `ocrutil.preprocess` を自作の OpenCV 処理に置き換えても、同じ **preprocess image for OCR** の考え方（しきい値 → フィルタ → エンジン投入）で進められます。

## Common Pitfalls & How to Avoid Them

- **過度な二値化:** しきい値が高すぎると薄い文字が消えてしまいます。文字が抜けている場合は `ocrutil.preprocess` のしきい値を下げてください。  
- **DPI が不適切:** OCR エンジンは印刷物で約 300 dpi を想定しています。低解像度の場合は、前処理前に拡大を検討してください。  
- **自動回転を省く:** 5 度程度の傾きでも行検出が失敗します。 “auto rotate image OCR” はコストが低く、後々のデバッグ時間を大幅に削減します。

## Extending the Workflow

ベースができたら、次のような拡張が考えられます。

1. **言語パックを追加**（`engine.set_language('eng+spa')`）して多言語文書に対応。  
2. **Pandas と統合**して JSON のテーブルを DataFrame に変換し、分析に活用。  
3. **バッチ処理**を実装し、フォルダー内の画像をループで処理して結果をマスタ JSON に追記。

これらすべては、エンジンを呼び出す前に **preprocess image for OCR** を行うというコアアイデアに基づいています。

## Conclusion

Python で **preprocess image for OCR** を実装し、自動回転、二値化、ノイズ除去を行い、最終的に **OCR engine Python** にクリーンな画像を渡してプレーンテキストとリッチな **OCR structured JSON output** を取得する方法を学びました。この手順を踏むことで認識率が大幅に向上し、下流処理にすぐ使えるデータが手に入ります。

次のステップとして、組み込みの `ocrutil.preprocess` をカスタム OpenCV パイプラインに差し替えてみたり、さまざまな二値化手法を試したり、JSON をレポートダッシュボードに流し込んでみてください。可能性は無限大です。ここで築いた基盤が、画像品質に関する同じ問題に再び躓くことを防いでくれるでしょう。

Happy coding, and may your OCR results be ever crisp!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}