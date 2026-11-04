---
category: general
date: 2026-06-06
description: Aspose OCR Cloud を使用した PDF の OCR 方法。PDF からテキストを抽出し、PDF ページを PNG に変換し、Python
  で PDF ページ画像を保存する方法を学びます。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: ja
og_description: Aspose OCR Cloud を使用して PDF を OCR する方法。このガイドでは、プレーンテキスト PDF の抽出、PDF
  ページを PNG に変換、PDF ページ画像の保存方法を示します。
og_title: Aspose OCR CloudでPDFをOCRする方法 – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Aspose OCR CloudでPDFをOCRする方法 – 完全ガイド
url: /ja/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR CloudでPDFをOCRする方法 – 完全ガイド

重いデスクトップツールと格闘せずに **PDFをOCRする方法** を考えたことはありませんか？ あなたは一人ではありません—スキャンした文書からテキストを素早くプログラム的に抽出する必要がある開発者は多く、この壁にぶつかります。良いニュースは、Aspose OCR Cloudを使えば **PDFからテキストを抽出** でき、各ページをPNGに変換し、さらには **PDFページ画像を保存** して後で利用することも、きれいなPythonスクリプトだけで実現できます。

このチュートリアルでは、SDKのインストール、エンジンのライセンス設定、マルチページPDFの認識から、プレーンテキストの抽出、ページのPNG変換、画像のディスクへの永続化まで、必要なすべての手順を解説します。最後まで読めば、**PDFをOCRする方法** の機能を必要とする任意のプロジェクトに組み込める再利用可能なスニペットが手に入ります。

## What You’ll Need

- **Python 3.8+**（コードは3.10以降でも動作します）  
- Aspose OCR Cloud アカウント – 無料トライアルのライセンスファイル（`Aspose.OCR.lic`）が取得できます  
- `asposeocrcloud` パッケージ（`pip install asposeocrcloud`）  
- 処理したいスキャン済みのマルチページPDF  

## How to OCR PDF – Setup and License

OCR メソッドを呼び出す前に、SDK に自分が誰かを知らせる必要があります。Aspose は軽量なライセンスファイルを使用し、スクリプトからアクセス可能な場所に配置します。

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro tip:* ライセンス手順を省略すると、SDK は動作しますが出力画像に小さな透かしが埋め込まれます。実運用には適しません。

## Step 2: Install the Aspose OCR Cloud Python SDK

ターミナルを開き、以下を実行します：

```bash
pip install asposeocrcloud
```

このパッケージは必要な依存関係（requests、pillow など）をすべて自動で取得するため、別途探す必要はありません。

## Step 3: Create an OCR Engine and Choose a Language

エンジンは処理の中心です。Aspose がサポートする任意の言語を指定できます。英語はほとんどの場合で機能します。

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

言語を設定する理由は、OCR エンジンが言語固有の辞書を使用して精度を向上させるためです。フランス語のPDFを処理する場合は、`ENGLISH` を `FRENCH` に置き換えるだけです。

## Step 4: Point to Your Multi‑Page PDF

エンジンに処理したいファイルへのフルパスを指定します。相対パスでも、スクリプトの作業ディレクトリから解決できれば問題ありません。

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

ファイルが読み取り可能であることを確認してください。そうでない場合は `FileNotFoundError` が発生します。

## Step 5: Run OCR – You Get a List of Results

`recognize_pdf` を呼び出すと、元のPDFの各ページに対応する要素が含まれるリストが返されます。

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

各 `OcrResult` には便利なプロパティが2つあります：

* `text` – ページのプレーンテキスト表現（**extract plain text pdf** に最適）  
* `image` – レンダリングされたページの Pillow `Image` オブジェクト（**convert pdf page png** に最適）

## Step 6: Extract Text from PDF and Convert Pages to PNG

ここでは結果をループし、抽出したテキストを出力し、各ページの PNG バージョンを保存します。

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Expected Console Output

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

`page_1.png`、`page_2.png` … が `YOUR_DIRECTORY` に生成されます。これらは下流の画像処理パイプラインに渡せるラスタライズされたページ画像です。

## Step 7: Save PDF Page Images (Optional Post‑Processing)

画像だけが必要でテキストが不要な場合は `print(res.text)` 行を省略できます。逆にテキストを別々の `.txt` ファイルに保存したい場合は、以下のように小さな書き出しを追加するだけです：

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

この小さな追加により、**PDFページ画像を保存**しつつ抽出したコンテンツを永続化するのがいかに簡単かが分かります。

## Full Working Example

すべてをまとめると、`ocr_pdf.py` にコピー＆ペーストできる完全なスクリプトは以下の通りです：

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

以下のコマンドで実行します：

```bash
python ocr_pdf.py
```

各ページのテキストがコンソールに出力され、PNG ファイルが一連で生成されるはずです。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}