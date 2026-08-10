---
category: general
date: 2026-06-06
description: Python を使って画像の OCR を実行し、信頼度スコアを確認します。信頼度の低い単語をフィルタリングする方法、しきい値の設定、エッジケースの処理方法を学びます。
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: ja
og_description: Pythonで画像にOCRを実行し、信頼度レベルを確認して低信頼度の単語をフィルタリングします。このチュートリアルでは、完全な実行可能な例を順を追って解説します。
og_title: Pythonで画像のOCRを実行する ― 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像のOCRを実行する – 完全ステップバイステップガイド
url: /ja/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像のOCRを実行する – 完全ステップバイステップガイド

画像ファイルに対して **run OCR on image** を実行したいと思ったことはありませんか？しかし、信頼できるテキストを取得する方法が分からないこともあるでしょう。あなたは一人ではありません—抽出された単語が不安定に見え、confidenceスコアが謎のままになる壁に、多くの開発者がぶつかっています。

このガイドでは、実用的な解決策にすぐに取り掛かります。**run OCR on image** の方法、全体の confidence を読み取り、手動で確認が必要になる低 confidence の単語を抽出する方法を紹介します。最後まで読むと、再利用可能なスクリプトが手に入り、各行がなぜ重要か理解でき、プロジェクトに合わせて confidence の閾値を調整する方法が分かります。

## このチュートリアルでカバーする内容

- 堅牢な OCR エンジンの選択（ここでは **EasyOCR**、人気の Python OCR ライブラリを使用します）  
- すべての OCR 結果が返す `confidence` 属性の解釈  
- カスタム **OCR confidence threshold** による単語のフィルタリング  
- バッチ処理や **pytesseract** などの代替エンジンへの拡張  

OCR の事前経験は不要です。Python の基本的な知識と動作環境（Python 3.9+ 推奨）があれば始められます。

ぼやけたスクリーンショットをクリーンで検索可能なテキストに変換する準備はできましたか？さあ、始めましょう。

---

## ## Pythonで画像のOCRを実行する方法

チュートリアルの核心は、すでに見たコードと同様の 3 ステップスニペットです。以下で各行を分解し、理由を説明し、コピー＆ペーストで使える完全なスクリプトを提供します。

### ステップ 1: OCRエンジンのインストールとインポート

まず、OCR ライブラリが利用可能であることを確認します。**EasyOCR** は多くの言語に対してすぐに使える上、単語ごとに confidence スコアを提供します。

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* 多様なデータセットで学習されたディープラーニングモデルをバンドルしているため、特に品質が混在した画像では、従来の Tesseract エンジンよりも高い confidence 値が得られることが多いです。

> **Pro tip:** 制約のある環境（例: 小さな Docker コンテナ）で作業している場合、`pytesseract` の方が軽量ですが、EasyOCR が提供する最新の精度の一部は失われます。

### ステップ 2: 画像に対して OCR を実行する

ここで実際に **run OCR on image** を行います。元の例の `recognize_image` メソッドは EasyOCR の `readtext` 呼び出しに置き換えられ、`(bbox, text, confidence)` のタプルのリストが返ります。

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

`ocr_results` の各エントリは次のようになります:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

3 番目の要素（例では `0.92`）が 0 から 1 の範囲の confidence スコアです。

### ステップ 3: 全体の confidence を要約する

以前のスニペットが単一の `confidence` 属性を出力したのとは異なり、EasyOCR は単語ごとに confidence を提供します。全体像を把握するために、これらを平均します:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* 迅速なヘルスチェックが可能になります。たとえば全体の confidence が 70 % 未満であれば、画像の照明改善や前処理などが必要になる可能性が高いです。

### ステップ 4: 低 confidence の単語を一覧表示

ここが「confidence が所定の閾値以下の単語をリストアップする」要件に直接応える部分です。デフォルトで **OCR confidence threshold** を 0.80（80 %）に設定しますが、必要に応じて調整できます。

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

このループは基準に達しなかった各単語とそのパーセンテージ confidence を出力します。これは元の `for recognized_word in recognition_result.words` ループと同等ですが、EasyOCR の出力形式に合わせて動作します。

---

## ## OCR confidence スコアの理解

confidence は魔法の数値ではなく、特定の文字起こしに対するモデルの確信度の推定です。覚えておくべきポイントをいくつか紹介します。

| 状況 | 典型的な信頼度 | 対策 |
|-----------|-------------------|------------|
| 明瞭で高解像度のスキャン | 0.95 – 1.00 | 追加作業不要 |
| わずかなぼやけや不均一な照明 | 0.80 – 0.94 | 軽度の前処理（コントラスト強化）を検討 |
| 大きなノイズや回転したテキスト | < 0.70 | 画像前処理（デスキュー、ノイズ除去）または別の OCR エンジンに切り替え |

> **Watch out:** 手書きの筆記体など、一部の言語は自然に低いスコアを出すことがあります。閾値はそれに合わせて調整してください。

### Edge Cases & Variations

1. **Batch Processing** – 大量の **run OCR on image** ファイルを処理する必要がある場合、上記ロジックをディレクトリを走査するループでラップします。  
2. **Multiple Languages** – `easyocr.Reader` に `['en', 'fr']` のようなリストを渡すと、エンジンは両方の言語を検出します。  
3. **Alternative Engines** – **pytesseract** を試したいですか？リーダーブロックを次のように置き換えます:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   その後、文字単位の confidence を単語単位に集計する必要があります。少し手間はかかりますが実現可能です。

4. **Pre‑processing Tricks** – OpenCV フィルタ（`cv2.threshold`, `cv2.GaussianBlur`）を適用すると、ノイズの多いスキャンでも confidence を向上させられます。

---

## ## 完全版・すぐに実行できるスクリプト

以下はプロジェクトにそのまま組み込める Python ファイルです。`ocr_report.py` として保存し、`python ocr_report.py` を実行してください。画像パスは実際のファイルを指すように設定してください。

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**期待される出力**（数値は環境により異なります）:

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

すべての単語が 80 % の基準をクリアすれば、代わりに「All words meet the confidence threshold.」というフレンドリーなメッセージが表示されます。

---

## ## Frequently Asked Questions (FAQ)

**Q: Does this work with PDFs?**  
A: 直接は対応していません。まず `pdf2image` などで各 PDF ページを画像に変換し、PNG/JPEG をスクリプトに渡してください。

**Q: My confidence numbers are all low—what can I do?**  
A: 画像前処理を試みてください。コントラストを上げる、背景ノイズを除去する、画像を水平に回転させるなど。EasyOCR では `contrast_ths` パラメータも調整可能です。

**Q: Can I export the results to CSV?**  
A: もちろんです。低 confidence ループの後で、`ocr_results` を `csv.DictWriter` に書き出し、各行に `text`、`confidence`、バウンディングボックス座標を含めれば完了です。

**Q: Is there a GPU‑accelerated version?**  
A: EasyOCR は、互換性のある GPU と PyTorch がインストールされていれば自動的に CUDA を使用します。スクリプト実行前に `torch.cuda.is_available()` で確認してください。

---

## Conclusion

私たちは Python を使って **run OCR on image** を実行し、全体の confidence を検査し、手動レビューが必要な低 confidence の単語を抽出しました。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}