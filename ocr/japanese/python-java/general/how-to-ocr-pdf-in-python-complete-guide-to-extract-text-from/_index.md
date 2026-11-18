---
category: general
date: 2026-06-22
description: PythonでPDFファイルをOCRし、PDFからテキストを抽出し、ストリームベースのアプローチでPDFをテキストに変換する方法を学びましょう。スキャンしたPDFを処理するためのシンプルな手順です。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: ja
og_description: PythonでPDFファイルをOCRする方法は？このガイドに従ってPDFからテキストを抽出し、PDFをテキストに変換し、ストリームを使用してスキャンされたPDFを処理しましょう。
og_title: PythonでPDFをOCRする方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: PythonでPDFをOCRする方法 – PDFからテキストを抽出する完全ガイド
url: /ja/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFをOCRする方法 – PDFからテキストを抽出する完全ガイド

重厚なデスクトップツールに悩まされずに **PDFをOCRする方法** を考えたことはありませんか？ あなただけではありません。実務のプロジェクト—たとえば請求書の自動化やアーカイブスキャンのデジタル化—では、スキャンしたPDFを検索可能で編集可能なテキストに変換する信頼できる方法が必要です。

このチュートリアルでは、軽量な Python OCR エンジンを使用して **PDFからテキストを抽出** するクリーンなエンドツーエンドの例を順に解説します。最後まで読めば、**PDFをテキストに変換** する方法、**ストリームからPDFをロード** する方法、そして **スキャンしたPDFを処理** する方法が正確に分かります。魔法はありません、今日すぐプロジェクトに組み込めるシンプルな Python コードだけです。

## 学べること

- PDF入力を理解できるPython OCRライブラリのインストールと設定。  
- PDF認識モードを有効にし、出力形式をプレーンテキストに設定。  
- ファイルストリームからマルチページPDFをロード（いわゆる “load pdf from stream” パターン）。  
- すべてのページに対してOCRを実行し、テキストコンテンツを取得。  
- 結果を出力または保存し、下流処理に利用。

**前提条件**  
- Python 3.8+ がマシンにインストールされていること。  
- pip と仮想環境の基本的な知識。  
- スキャンしたPDFファイル（例では `multipage.pdf` と命名）を既知のディレクトリに配置。

これらのいずれかが馴染みがない場合でも心配はいりません—各ステップは平易な言葉で説明し、必要な正確なコマンドを提供します。

---

## ステップ 1: OCRエンジンのインストール (how to OCR PDF)

まず最初に、PDF入力を扱える OCR エンジンが必要です。このガイドでは仮想の `ocr` パッケージを使用します（API は一般的な商用 SDK を模倣していますが、同様のパターンは Tesseract‑OCR、ABBYY、Google Vision でも適切にラップすれば機能します）。

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **プロのコツ:** Windows で権限エラーが出た場合は `pip install --user ocr` を試してください。

パッケージがインストールされたら、スクリプトでインポートしエンジンインスタンスを作成できます—これが **PDFをOCRする方法** の核心です。

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` オブジェクトは、後で調整する言語、DPI、そして最も重要な PDF モードなど、すべての設定を保持します。

## ステップ 2: PDF認識を有効にし出力形式を選択 (extract text from PDF)

デフォルトでは多くの OCR SDK が画像を入力と想定しています。エンジンにストリームを PDF として扱わせるために、PDF 認識フラグを有効にし、プレーンテキスト出力を要求します。

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

出力形式を指定する理由は何ですか？ 一部のエンジンは隠しテキスト層付き PDF、検索可能な PDF、あるいはバウンディングボックス付き JSON を返すことがあります。ほとんどのデータ抽出パイプラインでは、**PDFからテキストを抽出** してプレーン文字列にするのが最もクリーンな下流フォーマットです。

## ステップ 3: ストリームからPDFをロード (load PDF from stream)

ストリームから PDF をロードするパターンはメモリ効率が高く、ファイル全体を一度に RAM に読み込むことを回避できます。特に大容量のマルチページ文書を扱う際に便利です。

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **ファイルが S3 や別のクラウドバケットにある場合は？**  
> `from_file` をバイトバッファを受け取るメソッド（例: `ImageStream.from_bytes(s3_object.read())`）に置き換えるだけです。パイプラインの残りは同一です。

## ステップ 4: すべてのページでOCRを実行 (process scanned PDF)

いよいよ本格的な処理が始まります。エンジンは各ページを順に走査し、認識エンジンを実行してページオブジェクトのリストを返します—各オブジェクトはテキストコンテンツを公開します。

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

内部では、OCR ライブラリが各 PDF ページをデコードし、設定された DPI でラスタライズし、ビットマップをニューラルネットワークモデルに渡します。結果は抽出可能な `Page` オブジェクトのコレクションです。

## ステップ 5: 認識テキストを取得・表示 (convert PDF to text)

最後に、返されたページをループして認識されたテキストを出力します。これが **PDFをテキストに変換** が実際に行われる瞬間です。

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### 期待される出力

`multipage.pdf` に 3 ページのスキャンが含まれている場合、以下のような出力が得られます：

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

ページ間のクリーンな区切りに注目してください—各ページのテキストをデータベースに保存したり、下流の NLP モデルに供給したりする際に便利です。

## 共通エッジケースの処理

### 1. 画像とテキスト層が混在した PDF
Word からエクスポートされたように、既に隠しテキスト層を持つ PDF があります。OCR エンジンに **既存のテキストを無視** させて画像を再処理したい場合は、次のように設定します：

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. メモリ制限を超える大容量ファイル
ギガバイト級の PDF を扱うときは、チャンク単位で処理することを検討してください：

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. 言語とフォントのサポート
スキャン文書がフランス語や特殊文字を含む場合は、使用する言語モデルをエンジンに指示します：

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## 完全スクリプト – 実行可能

以下はすべての要素を結びつけた完全な実行例です。`ocr_pdf.py` として保存し、`python ocr_pdf.py` を実行してください。

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**スクリプトを実行** すると、各ページのテキストがコンソールに出力され、上記「期待される出力」セクションと同様になります。ここから出力をファイルにリダイレクトすることも可能です：

```bash
python ocr_pdf.py > extracted_text.txt
```

## 結論

ここまでで、Python で **PDFをOCRする方法** を最初から最後まで網羅しました。エンジンの設定、ストリーム経由でのドキュメント読み込み、各認識ページのイテレーションにより、**PDFからテキストを抽出**、**PDFをテキストに変換**、そして **スキャンしたPDFを処理** できるようになりました。このアプローチは、2 ページの小さな請求書から数百ページに及ぶ大規模アーカイブまでスケールします。

次は何をしますか？ 抽出した文字列を検索インデックス、言語モデル要約、またはデータ検証パイプラインに流し込んでみましょう。JSON 形式で出力して位置メタデータを保持すれば、より高度な文書分析にも応用できます。

暗号化された PDF の取り扱いやクラウドストレージとの統合について質問がありますか？ コメントで教えてください—ハッピーコーディング！

![OCR PDF ワークフローを示す図 – PDFをOCRする方法、ストリームからPDFをロード、ページを認識、テキストを抽出](ocr-pdf-workflow.png "PDFをOCRするワークフロー図")

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose.OCR を使用した .NET での PDF OCR 方法](/ocr/english/net/text-recognition/recognize-pdf/)
- [Aspose.OCR for .NET を使用した画像からのテキスト抽出方法](/ocr/english/net/text-recognition/get-recognition-result/)
- [Aspose.OCR for .NET を使用した ZIP アーカイブからのテキスト抽出方法](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}