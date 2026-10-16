---
category: general
date: 2026-06-19
description: Python OCR を使用して画像から検索可能な PDF を作成します。OCR を PDF に変換し、画像からテキストを抽出し、画像上で
  OCR を迅速に実行する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: ja
og_description: Python OCRで画像から検索可能なPDFを作成する。このガイドでは、OCRをPDFに変換する方法、画像からテキストを抽出する方法、そして画像に対してOCRを実行する方法を示します。
og_title: Pythonで検索可能なPDFを作成 – 完全プログラミング解説
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Pythonで検索可能なPDFを作成する – 完全ステップバイステップガイド
url: /ja/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで検索可能なPDFを作成する – 完全ステップバイステップガイド

スキャンしたレシートから **searchable PDF** を作成したいと思ったことはありませんか？でも、どこから始めればいいか分からない…という方は多いです。テキストの画像を実際に検索できる PDF に変換しようとしたときに、最初に壁にぶつかる開発者は多数います。

このチュートリアルでは、**画像に対して OCR を実行**し、その OCR 結果を **searchable PDF** に変換し、さらに必要に応じて生テキストを抽出する実用的な解決策を順を追って解説します。余計な説明は省き、すぐにプロジェクトにコピペできる動作例を提供します。

## 学べること

- Python で軽量な OCR エンジンをセットアップする方法  
- **OCR を PDF に変換**して検索可能なドキュメントとして保存する手順  
- **画像からテキストを抽出**して下流処理に利用する方法  
- 画像の向きや大容量ファイルなど、よくある落とし穴への対処法  
- 実際に動作する完全なスクリプト（自分のユースケースに合わせてカスタマイズ可能）

### 前提条件

- Python 3.8+ がインストールされていること  
- pip と仮想環境の基本的な使い方が分かっていること（任意ですが推奨）  
- 明瞭で機械可読なテキストを含む画像ファイル（PNG、JPEG など）  

上記が揃っていれば、さっそく始めましょう。

## Step 1: 必要なライブラリをインストール

先ほどのコードスニペットでは架空の `ocr` パッケージを使用しましたが、実際のライブラリとしては **EasyOCR**、**pytesseract**、**pdfminer.six** などが利用できます。このガイドでは、純粋な Python 実装で多言語対応かつ便利な PDF 変換ヘルパーを持つ **EasyOCR** を使用します。

```bash
pip install easyocr pillow
```

> **プロのコツ:** 仮想環境内でインストールすると依存関係が整理しやすくなります（`python -m venv venv && source venv/bin/activate`）。

## Step 2: OCR エンジンを初期化 – 画像に対して OCR を実行

ライブラリの準備ができたら、OCR エンジンを作成し、英語テキスト用に設定します。ここが **画像に対して OCR を実行**する最初のステップです。

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

なぜ専用のリーダーオブジェクトが必要かというと、EasyOCR は言語モデルを事前にロードするため、複数画像に対して同じ `reader` を再利用する方が毎回再初期化するよりもはるかに効率的です。

## Step 3: 画像を読み込む – 画像からテキストを抽出

画像をメモリに読み込みます。この段階ではまだ **画像からテキストを抽出** する準備だけです。

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

画像が逆さまだったり歪んでいる場合は、OCR エンジンに渡す前に Pillow の `rotate` や `transpose` メソッドで補正するとよいでしょう。簡単な目視確認だけでもデバッグ時間を大幅に削減できます。

## Step 4: OCR エンジンを実行し結果を取得

ここがプロセスの核心です。画像を OCR エンジンに渡し、構造化されたデータを受け取ります。

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

`detail=1` フラグを付けるとバウンディングボックスが取得でき、後で **OCR を PDF に変換**する際に必要になります。文字列だけが欲しい場合は `detail=0` に設定してください。

## Step 5: OCR 結果を検索可能な PDF に変換 – OCR を PDF に変換

EasyOCR には直接 PDF を書き出す機能はありませんが、Pillow と `reportlab`、そして軽量な `fpdf2` を組み合わせて自前で PDF を作成できます。ここでは画像を表示レイヤーとして貼り付け、見えないテキストを重ねる手法を取ります。

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

何が起きたかというと、スキャン画像を可視レイヤーとして配置し、その上に白いテキスト（背景と同色）で認識した文字列を書き込んでいます。検索ツールは隠れたテキスト層を読むため、見た目は変わらず **searchable** な PDF が完成します。

## Step 6: PDF バイト列を取得 – 画像を PDF に変換

PDF をディスクに直接書き出す代わりに、メモリ上でバイト列として取得したい場合は以下のようにします。

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

この一行で、典型的な **convert image to PDF** ワークフロー（画像 → OCR → テキストオーバーレイ → PDF ストリーム生成）を実演しています。

## Step 7: 結果を確認 – 簡易チェック

スクリプト実行後、`receipt_searchable.pdf` を任意の PDF ビューアで開き、検索ボックス（Ctrl + F）でレシートに含まれる単語を入力してみてください。正しい位置にジャンプすれば **searchable pdf を作成**できています！

検索が機能しない場合は、以下を再確認してください。

1. OCR の信頼度スコア（`conf` 値）。低いと画像がぼやけている可能性があります。  
2. バウンディングボックスの座標 – EasyOCR が異なる向きで報告することがあります。  
3. PDF ビューアが「画像のみ」モードになっていないか（稀ですが、一部のビューアにその設定があります）。

## 完全動作スクリプト

すべてをまとめた、すぐに実行できる Python ファイルは以下の通りです。

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

`searchable_pdf.py` という名前で保存し、`YOUR_DIRECTORY` のプレースホルダーを実際のパスに置き換えてから実行してください。

```bash
python searchable_pdf.py
```

実行すると確認メッセージが表示され、フォルダ内に新しい **searchable PDF** が生成されます。

## よくある質問とエッジケース

**画像がカラーの場合はどうすれば？**  
EasyOCR はグレースケール・カラーどちらでも動作しますが、ノイズが多いスキャンでは `pil_image.convert("L")` でグレースケール化すると精度が向上することがあります。

**マルチページ PDF に対応できるか？**  
可能です。各ページ画像に対して同じ OCR 手順を実行し、同一の `FPDF` オブジェクトに `self.add_page()` でページを追加していきます。

**テキスト層を白文字ではなく、実際の「テキスト下画像」レイヤーにしたい**  
アクセシビリティが必要な場合は、`pdfminer` や `pikepdf` を使って隠しテキスト層を PDF タグ付きで埋め込む方法があります。高度な手法ですが、基本は「背景画像 + テキストオーバーレイ」という考え方は変わりません。

**OCR の信頼度が低い場合は？**  
信頼度が低い単語を除外することができます。

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## まとめ – 達成したこと

レシートの画像から **画像に対して OCR を実行**し、認識文字列を抽出、最終的に **searchable pdf** を作成しました。プロセス全体で **OCR を PDF に変換**、**画像からテキストを抽出**、**画像を PDF に変換**、**画像に対して OCR を実行**という二次キーワードをすべて網羅していますので、同様のプロジェクトで再利用できるツールボックスが手に入りました。

### 次のステップ

- `easyocr.Reader(['en', 'es'])` のように ISO コードを追加して他言語に挑戦する。  
- 完全オフラインが必要な場合は Tesseract に置き換えても、パイプラインは同じです。  
- OCR の信頼度を可視化（画像にバウンディングボックスを描画）して、問題のあるスキャンをデバッグする。  

何か独自の工夫があればコメントで共有してください。フォークも大歓迎です。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれているので、API の追加機能習得や別実装アプローチの探索に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}