---
category: general
date: 2026-05-31
description: Python OCR を使用してスキャン画像から検索可能な PDF を作成します。スキャン画像の PDF を変換し、TIFF を PDF
  に変換し、数分で OCR テキストレイヤーを追加する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: ja
og_description: 検索可能なPDFを即座に作成します。このガイドでは、OCRを実行し、スキャン画像PDFを変換し、単一のPythonスクリプトでOCRテキストレイヤーを追加する方法を示します。
og_title: Pythonで検索可能なPDFを作成する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Pythonで検索可能なPDFを作成する – ステップバイステップガイド
url: /ja/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで検索可能なPDFを作成 – ステップバイステップガイド

スキャンしたページから **検索可能なPDFを作成** する方法を、たくさんのツールを使い分けずに知りたくなったことはありませんか？ あなただけではありません。多くのオフィスワークフローでは、スキャンしたTIFFやJPEGが共有ドライブに置かれ、次の担当者が手作業でテキストをコピー＆ペーストしなければならず、面倒でエラーが起きやすく、時間が無駄になります。

このチュートリアルでは、**スキャン画像PDFを変換**、**TIFFをPDFに変換**、そして **OCRテキストレイヤーを追加** するクリーンでプログラム的なソリューションを順を追って解説します。最後まで実行すれば、OCRを走らせて隠しテキストを埋め込み、インデックス作成や検索、共有が自信を持ってできる検索可能なPDFを出力するスクリプトが手に入ります。

## 必要なもの

- Python 3.9+（最近のバージョンならどれでも可）
- `aspose-ocr` と `aspose-pdf` パッケージ（`pip install aspose-ocr aspose-pdf` でインストール）
- スキャン画像ファイル（`.tif`、`.png`、`.jpg`、または画像だけのPDFページ）
- ほどほどのRAM（OCRエンジンは軽量で、ノートパソコンでも問題なく動作）

> **プロのコツ:** Windows を使用している場合、管理者権限で PowerShell ウィンドウを開き、上記コマンドを実行するとパッケージ取得が最も簡単です。

```bash
pip install aspose-ocr aspose-pdf
```

前提条件が整ったので、コードに入りましょう。

## Step 1: OCRエンジンインスタンスの作成 – *create searchable pdf*

最初に行うのは OCR エンジンの起動です。ピクセルを読み取り文字に変換する「脳」のようなものと考えてください。

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **なぜ重要か:** エンジンを一度だけ初期化すればメモリ使用量が抑えられます。各ページごとに `OcrEngine()` をループ内で呼び出すと、すぐにリソースが枯渇します。

## Step 2: スキャン画像の読み込み – *convert tiff to pdf* & *convert scanned image pdf*

次に、処理したいファイルをエンジンに渡します。API は任意のラスタ画像を受け付けるので、TIFF でも JPEG でも同様に扱えます。

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

もし画像だけが埋め込まれた PDF を持っている場合でも、`load_image` を使用すれば Aspose が自動的に最初のページを抽出してくれます。

## Step 3: PDF保存オプションの設定 – *add OCR text layer*

ここで最終的な PDF の見た目を構成します。重要なフラグは `create_searchable_pdf` で、`True` に設定するとライブラリは視覚コンテンツと同じ位置に見えないテキストレイヤーを埋め込みます。

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **テキストレイヤーの働き:** 生成されたファイルを Adobe Reader で開きテキスト選択を試すと、隠れた文字が選択できるようになります。検索エンジンもインデックス化できるため、コンプライアンスやアーカイブに最適です。

## Step 4: OCR実行と保存 – *how to run OCR* in a single call

いよいよ魔法の瞬間です。1 回のメソッド呼び出しで認識エンジンが走り、検索可能な PDF がディスクに書き込まれます。

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` メソッドはステータスオブジェクトを返し、エラーを確認できますが、ほとんどのシンプルなシナリオでは上記の呼び出しだけで十分です。

### 期待される出力

スクリプト実行時に次のように表示されます:

```
PDF saved as searchable PDF.
```

`scanned_page_searchable.pdf` を開くと、テキストが選択でき、コピー＆ペーストが可能で、`Ctrl+F` 検索も動作します。これが **create searchable pdf** ワークフローの特徴です。

## 完全動作スクリプト

以下が完成した、すぐに実行できるスクリプトです。プレースホルダーのパスを実際のファイル位置に置き換えてください。

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

`create_searchable_pdf.py` として保存し、実行します:

```bash
python create_searchable_pdf.py
```

## よくある質問とエッジケース

### 1️⃣ マルチページ PDF を処理できますか？

はい。`ocr_engine.load_image("file.pdf")` を使用し、`ocr_engine.recognize(pdf_save_options, page_number)` で各ページをループ処理します。ライブラリは自動的にマルチページの検索可能 PDF を生成します。

### 2️⃣ ソースファイルが高解像度 TIFF（300 dpi 以上）の場合は？

DPI が高いほど OCR の精度は向上しますが、メモリ使用量も増えます。`MemoryError` が発生したら、まず画像をダウンサンプルしてください:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ OCR の言語を変更するには？

画像を読み込む前にエンジンの `language` プロパティを設定します:

```python
ocr_engine.language = "fra"   # French
```

サポートされている言語コードの完全一覧は Aspose のドキュメントにあります。

### 4️⃣ 元画像の品質を保持したい場合は？

`PdfSaveOptions` クラスの `compression` プロパティを使用します。`PdfCompression.None` に設定すると、ラスタデータが元のまま保存されます。

```python
pdf_save_options.compression = "None"
```

## 本番環境向けデプロイのヒント

- **バッチ処理:** コアロジックをファイルパスのリストを受け取る関数でラップし、成功・失敗を CSV に記録して監査証跡を残す。
- **並列処理:** `concurrent.futures.ThreadPoolExecutor` を使って複数コアで OCR を同時実行。ただし各スレッドは独自の `OcrEngine` インスタンスを持つ必要があります。
- **セキュリティ:** 機密文書を扱う場合はサンドボックス環境でスクリプトを実行し、処理後は一時ファイルを即座に削除してください。

## 結論

これで、スキャン画像から **検索可能なPDF** を作成する簡潔な Python スクリプトの手順が分かりました。OCR エンジンを初期化し、TIFF（または任意のラスタ）を読み込み、`PdfSaveOptions` を **add OCR text layer** に設定し、最後に `recognize` を呼び出すだけで、**convert scanned image pdf** と **convert TIFF to PDF** のパイプラインが単一の再現可能なコマンドになります。

次のステップは？ このスクリプトをファイルウォッチャーと組み合わせ、フォルダーに新しいスキャンがドロップされるたびに自動で検索可能にするか、あるいは異なる OCR 言語を試して多言語アーカイブに対応させるかです。OCR と PDF 生成を組み合わせれば、可能性は無限です。

**how to run OCR** に関して他の言語やフレームワークでの質問があれば、下のコメント欄にどうぞ。Happy coding!

![スキャン画像 → OCRエンジン → 検索可能なPDF（create searchable pdf）のフローを示す図](searchable-pdf-flow.png "検索可能なPDFフローダイアグラム")


## 次に学ぶべきことは？

- [Aspose.OCR を使用した .NET での PDF OCR 方法](/ocr/english/net/text-recognition/recognize-pdf/)
- [C# で画像を PDF に変換 – マルチページ OCR 結果の保存](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Aspose.OCR を使用した言語別画像テキスト OCR 方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}