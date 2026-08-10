---
category: general
date: 2026-05-31
description: OCRの関心領域（ROI）を使用して画像を読み込み、矩形からテキストを抽出する方法を学びましょう。請求書の金額認識に最適です。
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: ja
og_description: OCRの対象領域をマスターし、画像をOCRに読み込んで矩形からテキストを抽出し、請求書のテキストを認識する単一のチュートリアル。
og_title: OCR関心領域 – ステップバイステップ Python ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCRの関心領域 – Pythonで矩形からテキストを抽出
url: /ja/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR領域（Region of Interest） – Pythonで矩形からテキストを抽出

スキャンした請求書の特定の部分だけを **ocr region of interest** したいと思ったことはありませんか？ページ全体をエンジンに渡さずに、ぼやけたレシートを見ながら「右下にある金額をどうやって抽出すればいいんだろう？」と考えているのはあなただけではありません。朗報です。OCRライブラリに正確に「ここを見る」よう指示すれば、速度も精度も大幅に向上します。

このガイドでは、**load image for OCR**、**region of interest** の定義、そして **extract text from rectangle** を実演する、実行可能な完全なサンプルを順を追って解説します。最終的に **recognize text from invoice** し、古典的な「金額を抽出する方法」への答えを導き出します。曖昧な説明はありません—具体的なコード、明快な解説、そして早く知っておきたかったプロのコツを提供します。

---

## What You’ll Build

このチュートリアルの最後までに、以下の機能を持つ小さな Python スクリプトが完成します。

1. ディスクから請求書画像を読み込む。  
2. 合計金額が記載されている矩形 ROI をマークする。  
3. その ROI 内だけで OCR を実行する。  
4. 整形された金額文字列を出力する。  

これらは ROI をサポートする任意の OCR ライブラリで動作します—ここでは、Tesseract や EasyOCR などの代表的なツールを模倣した架空の `SimpleOCR` パッケージを使用します。別のライブラリに差し替えても概念は変わりません。

---

## Prerequisites

- Python 3.8+ がインストール済み（`python --version` で ≥3.8 が表示されること）。  
- pip でインストール可能な OCR パッケージ（例：`pip install simpleocr`）。  
- 請求書画像（PNG または JPEG）を参照できるフォルダーに配置。  
- Python の関数・クラスに関する基本的な知識（特別な知識は不要）。

上記がすでに揃っていれば、さっそく始めましょう。まだの場合はまず画像を用意してください。残りの手順はファイル内容に依存しません。

---

## Step 1: Load Image for OCR

OCR ワークフローの最初のステップは、読み取るビットマップを用意することです。多くのライブラリはファイルパスを受け取るシンプルな `load_image` メソッドを提供しています。以下は `SimpleOCR` エンジンでの実装例です。

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** スクリプトを別ディレクトリから実行する際の “file not found” エラーを防ぐため、絶対パスまたは `os.path.join` を使用しましょう。

---

## Step 2: Define OCR Region of Interest

エンジンにページ全体を走査させる代わりに、金額が存在する正確な位置を指定します。これが **ocr region of interest** のステップであり、ヘッダーやフッターがノイズになる文書でも信頼性の高い抽出を実現する鍵です。

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

なぜその数値なのか？`x` と `y` は左上隅からのピクセルオフセット、`width` と `height` は矩形のサイズを表します。分からない場合は任意の画像エディタで定規を表示し、座標をメモしてください。多くの IDE ではカーソル位置をホバーで表示できます。

---

## Step 3: Extract Text from Rectangle

ROI が設定できたら、エンジンに **recognize text from invoice** を依頼しますが、先ほど追加した矩形に限定します。呼び出しは通常、生文字列、信頼度スコア、場合によってはバウンディングボックスを含む結果オブジェクトを返します。

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

内部では、`recognize()` が各 ROI を走査し、該当領域を切り取り、OCR モデルを実行し、結果を結合します。したがって、**extract text from rectangle** の領域を絞ることで、バッチ処理の時間を数秒短縮できます。

---

## Step 4: How to Extract Amount – Clean the Output

OCR は完璧ではなく、余分な空白や改行、文字の誤認識（例： “S” と “5”）が出やすいです。`strip()` と小さな正規表現で金額形式を整えるのが一般的です。

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** 金額をデータベースや決済ゲートウェイに渡す場合、予測可能なフォーマットが必要です。空白除去と数値以外の文字フィルタリングで下流エラーを防げます。

---

## Step 5: Recognize Text from Invoice – Full Script

すべてをまとめた完全なスクリプトです。`extract_amount.py` として保存し、`python extract_amount.py` で実行してください。

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

```
Amount: 1,245.67
```

ROI がずれていると `Amount: 1245.6S` のように余計な文字が混入します。矩形座標を調整し、出力がきれいになるまで再実行してください。

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI too small** | 金額テキストが切り取られ、認識が不完全になる。 | `width`/`height` を約10‑20 % 拡大して再テスト。 |
| **Incorrect DPI** | 低解像度スキャン（≤150 dpi）で OCR 精度が低下。 | 読み込む前に画像を 300 dpi にリサンプリング、またはスキャナ設定を上げる。 |
| **Multiple currencies** | 正規表現が最初の数値グループを取得し、請求書番号になることがある。 | 通貨記号（`$`, `€`, `£`）を数字の前に探すよう正規表現を改良。 |
| **Rotated invoices** | OCR エンジンは正立テキストを前提としているため、回転ページは認識できない。 | ROI 設定前に `ocr_engine.rotate(90)` で回転補正を実施。 |
| **Noise in background** | 影やスタンプがモデルを混乱させる。 | `cv2.threshold` で閾値処理、またはデノイズフィルタを適用。 |

これらのケースに早めに対処すれば、後々のデバッグ時間を大幅に削減できます。

---

## Pro Tips for Real‑World Projects

- **Batch Processing:** 請求書フォルダーをループし、テンプレート検出に基づいて ROI を動的に算出、結果を CSV に保存。  
- **Template Matching:** 複数の請求書レイアウトを扱う場合、`template_id → ROI coordinates` の JSON マップを保持し、レイアウト分類器で ROI を切り替える。  
- **Parallel Execution:** `concurrent.futures.ThreadPoolExecutor` を使って OCR インスタンスを並列実行。大量のバックオフィスパイプラインに最適。  
- **Confidence Filtering:** 多くの OCR 結果は信頼度スコアを含む。閾値（例：85 %）未満は除外し、手動レビューへフラグ付け。

---

## Conclusion

**ocr region of interest**、**load image for OCR**、**extract text from rectangle**、そして **recognize text from invoice** のすべての手順を網羅し、古典的な **how to extract amount** の疑問に答える方法を解説しました。スクリプトはコンパクトながら、さまざまな文書形式・言語・OCR バックエンドに柔軟に対応できます。

基本をマスターしたら、バーコードスキャンの追加、PDF パーサーとの統合、会計 API への金額送信など、ワークフローを拡張してみてください。ROI を明確に定義すれば、常に高速でクリーンな結果が得られます。

問題があればコメントで教えてください—Happy OCRing!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## What Should You Learn Next?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}