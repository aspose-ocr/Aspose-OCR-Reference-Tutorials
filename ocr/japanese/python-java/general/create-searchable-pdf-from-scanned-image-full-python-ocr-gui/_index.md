---
category: general
date: 2026-07-05
description: Pythonで検索可能なPDFを作成する。スキャンしたPNGのOCR方法、スキャン画像PDFの変換方法を学び、数分で検索可能なPDFを取得する。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: ja
og_description: 検索可能なPDFをすばやく作成できます。このガイドでは、PNGをOCRし、スキャン画像PDFを変換し、Pythonを使用して検索可能なPDFを生成する方法を示します。
og_title: スキャン画像から検索可能なPDFを作成 – Python OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: スキャン画像から検索可能なPDFを作成する – 完全なPython OCRガイド
url: /ja/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャン画像から検索可能なPDFを作成 – 完全なPython OCRガイド

高価なソフトウェアを購入せずに、スキャンした画像から **検索可能なPDF** を作成する方法を考えたことはありませんか？ あなたは一人ではありません。多くのオフィスでは、PDFが平坦な画像として届き、検索が困難で、コピー＆ペーストもできず、コンプライアンス監査の悪夢となっています。良いニュースは、数行のPythonコードでその静的なPNGを完全に検索可能なPDFに変換でき、プロセスは思ったよりも簡単だということです。

このチュートリアルでは、**OCR認識の完全な例** を順を追って解説します。適切なライブラリのインストールから最終的なPDFファイルの書き出しまで網羅します。最後まで読めば、**スキャン画像PDF** を **how to ocr pdf** でプログラム的に変換する方法が正確に分かり、どのプロジェクトにも組み込める再利用可能なスクリプトが手に入ります。

## 学べること

- Python OCRライブラリをインストールし設定する（`pytesseract` と `pdf2image` を使用）。
- OCRエンジンを初期化し、言語を設定する。
- スキャンしたPNG（または任意の画像）を読み込み、OCRを実行する。
- OCR結果を **検索可能なPDF**（バイト配列）に変換し、保存する。
- 複数ページのドキュメント、異なる言語、一般的な落とし穴への対処法。

OCRの経験は不要です—Python 3 が動作する環境と少しの好奇心があれば始められます。

---

## 検索可能なPDFの作成 – 概要

以下は実装するステップのハイレベルなフローチャートです。  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: エンジン初期化、画像読み込み、OCR認識、PDF変換、ファイル書き込みを示す検索可能なPDFワークフロー図。*

---

## ステップ 1: OCRエンジンの初期化 (how to ocr pdf)

なぜエンジンを初期化する必要があるのでしょうか？ OCRエンジンはピクセルパターンを文字として解釈する頭脳です。エンジンインスタンスを作成し、言語を明示的に設定することで、期待すべき文字セットをライブラリに伝え、精度が大幅に向上します。

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** 複数言語の文書をOCRしたい場合は、Tesseract用の対応言語パックをインストールし、`ocr_language` に `"eng+spa"` のようにリストで渡してください。

---

## ステップ 2: スキャン画像の読み込み (convert scanned image pdf)

次に必要なのは画像データをPythonに取り込むことです。単一のPNGでもマルチページTIFFでも、`PIL.Image` クラスで開くことができます。すでにスキャン画像が埋め込まれたPDFから始める場合は、`pdf2image` が各ページを画像に変換してくれます。

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Why this matters:** 画像をPillowオブジェクトとしてロードすると、生のピクセルデータにアクセスでき、OCRエンジンが必要とする情報を提供できます。生バイトを直接渡すとエラーになります。

---

## ステップ 3: 画像に対するOCR認識の実行 (ocr recognition example)

さあ楽しいパートです—エンジンにテキストを読ませます。`pytesseract.image_to_pdf_or_hocr` は、すでに不可視テキスト層を含むPDFバイトストリームを返します。これが **検索可能なPDF** に必要なものです。

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** 画像が低コントラストの場合は、OCR前にシンプルな閾値処理を適用すると効果的です：

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

この小さな前処理で精度が劇的に向上します。

---

## ステップ 4: PDFバイトをファイルに書き出す (convert png searchable pdf)

OCRライブラリがバイト配列を返します—PDFファイルの生データと考えてください。あとはそのバイトをディスクに書き込むだけです。

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** 任意のPDFビューアで生成されたファイルを開き、元画像に確実に存在する単語で検索してみてください。ハイライトが直接該当箇所にジャンプし、不可視テキスト層が機能していることが確認できます。

---

## ステップ 5: マルチページ文書への拡張 (convert scanned image pdf)

実務の契約書はしばしば複数ページにわたります。**スキャン画像pdf** ファイルを複数ページ処理するには、各ページをループでOCRし、生成されたPDFを連結します。

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Why merge?** `image_to_pdf_or_hocr` の各呼び出しは単独のPDFを生成します。これらを結合することで、最終文書が元のページ順序を保持します。

---

## よくある落とし穴と対処法

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| PDFを開いた後にテキストが検索できない | Tesseractが文字を検出できない（空の出力） | 画像品質を確認し、DPIを上げるか、前処理（コントラスト、二値化）を適用する。 |
| 文字化け（例: �） | 言語パックが間違っている、またはフォントが不足している | 正しい言語データ（`tesseract‑lang‑eng`）をインストールし、`ocr_language` が一致していることを確認する。 |
| PDFファイルサイズが巨大（1ページ画像で10 MB超） | ソースがロスレスPNGで、OCRがフル解像度画像を追加している | OCR前に画像を縮小する（A4用に `image.thumbnail((1240, 1754))` など）。 |
| Windowsで「tesseract.exeが見つかりません」とクラッシュ | TesseractバイナリがPATHに含まれていない | `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"`（パスは環境に合わせて調整）を追加する。 |

---

## 完全な実行可能スクリプト

すべてをまとめた単一ファイルをご紹介します。コピーしてそのまま実行できます。

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

`create_searchable_pdf.py` として保存し、プレースホルダーを実際のパスに置き換えて実行してください：

```bash
python create_searchable_pdf.py
```

実行すると

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加のAPI機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose.OCR を使用した .NET での PDF OCR 方法](/ocr/english/net/text-recognition/recognize-pdf/)
- [C# で画像を PDF に変換 – マルチページ OCR 結果の保存](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Java 用 Aspose.OCR で PDF 文書を OCR 認識](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}