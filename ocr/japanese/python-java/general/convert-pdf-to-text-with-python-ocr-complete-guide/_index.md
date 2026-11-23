---
category: general
date: 2026-07-05
description: Python OCR を使用して PDF をテキストに変換します。PDF からテキストを抽出する方法、バッチ OCR 処理の実行方法、OCR
  用に PDF を読み込む方法を、簡単な手順で学びましょう。
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: ja
og_description: PDFをすばやくテキストに変換します。このチュートリアルでは、PDFからテキストを抽出し、バッチOCR処理を実行し、Pythonを使ってスキャンされたPDFファイルを認識する方法を示します。
og_title: Python OCRでPDFをテキストに変換する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Python OCRでPDFをテキストに変換する – 完全ガイド
url: /ja/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR で PDF をテキストに変換する – 完全ガイド

PDF を **テキストに変換** したいと考えたことはありませんか？スキャンされた契約書や請求書、研究論文が山ほどあり、インデックス作成や分析のためにプレーンテキストが必要な場合に最適です。数行の Python コードで重い作業を自動化できます。

このチュートリアルでは、 **PDF をテキストに変換** するだけでなく、 **PDF からテキストを抽出** する方法、 **バッチ OCR 処理** の設定方法、そして **OCR 用に PDF をロード** する正しい手順を実演します。最後まで読めば、スキャンされた PDF ページを一括で **認識** できる実行可能スクリプトが手に入ります。

## 学べること

- Python OCR ライブラリのインストールと設定（例として汎用的な `ocr` パッケージを使用）  
- 複数ページの PDF をロードし、OCR エンジンに渡す方法  
- 結果をイテレートしてテキストを表示または保存する方法  
- 大容量ファイル、暗号化 PDF、混在言語文書などの一般的なエッジケースへの対処法  

重い GUI ツールや手作業のコピーは不要です。CI パイプラインやデスクトップユーティリティにそのまま組み込める純粋なコードだけです。

![Python OCR で PDF をテキストに変換](https://example.com/images/convert-pdf-to-text.png "Python OCR で PDF をテキストに変換")

## 前提条件

作業を始める前に以下を用意してください。

| 要件 | 理由 |
|------|------|
| Python 3.9+ | 最新構文、型ヒント、パフォーマンス向上のため |
| `ocr` ライブラリ（または Tesseract ラッパー） | サンプルで使用する `OcrEngine`、`Language`、`Image` クラスを提供 |
| 複数ページのスキャン PDF（例：`contract.pdf`） | **OCR 用に PDF をロード** する対象ファイル |
| 基本的なコマンドライン操作の知識 | パッケージインストールやスクリプト実行に必要 |

Tesseract を使用する場合は OS のパッケージマネージャでインストールします（Linux の `apt-get install tesseract-ocr`、macOS の `brew install tesseract`）。その後、Python ラッパーを追加します。

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## 手順 1: OCR エンジンを作成し認識言語を設定

まず OCR エンジンのインスタンスを作ります。言語を英語に設定するのが一般的なデフォルトですが、後から他のサポート言語に切り替えることも可能です。

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**ポイント:** エンジンはピクセルデータを解釈する脳です。`engine.language` を明示的に設定することで、各ページで言語検出を行うオーバーヘッドを回避でき、 **バッチ OCR 処理** の速度が大幅に向上します。

## 手順 2: OCR 用に PDF ドキュメントをロード

次に PDF をメモリに読み込みます。`ocr.Image.load` メソッドはファイルパスを受け取り、エンジンが理解できるオブジェクトを返します。

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**プロ tip:** PDF がパスワード保護されている場合、多くのライブラリは `password` 引数を受け付けます。早めに処理しておくと、後で「ファイルを開けません」という不明瞭なエラーを防げます。

## 手順 3: すべてのページで OCR を実行 – 1 回の呼び出しでスキャン PDF を認識

ページごとに OCR を実行すると時間がかかります。`recognize_multi_page` メソッドは内部で **バッチ OCR 処理** を行い、可能な限りマルチスレッドで処理します。

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**内部で何が起きているか:** エンジンは各ページを基盤の OCR エンジン（例：Tesseract）にストリームし、テキストを収集して `OcrResult` にラップします。この手法は I/O オーバーヘッドを削減し、後で **PDF からテキストを抽出** する際にシンプルなインターフェースを提供します。

## 手順 4: 結果をイテレートして認識テキストを出力

最後に各 `OcrResult` をループし、テキストを表示します。ページごとに別々の `.txt` ファイルに書き出したり、すべてを結合して単一文書にしたりすることも可能です。

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**enumerate を使う理由:** `enumerate(..., start=1)` により人間が読みやすいページ番号が得られ、後で元の PDF の特定セクションを参照する際に便利です。

### 期待される出力

3 ページの契約書に対してスクリプトを実行すると、次のような出力が得られます。

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

ページに認識可能なテキストが無い場合、対応する `result.text` は空文字列になります。これにより、空白ページや画像のみのページを簡単に特定できます。

## 大容量 PDF とメモリ制約への対処

500 ページ規模の PDF を一括でロードすると RAM が枯渇する恐れがあります。以下の 2 つの戦略をご紹介します。

1. **チャンクロード** – ライブラリによってはページ範囲を指定してロードできます:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **ディスクへのストリーミング** – 各ページのテキストをメモリに保持せず、直接ファイルに書き出します。

どちらの手法も **PDF をテキストに変換** ワークフローをスケーラブルに保ちます。

## エラーとエッジケースの処理

- **暗号化 PDF** – `Image.load` にパスワードを渡す:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **混在言語** – ページごとに言語を切り替える:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **低解像度スキャン** – `Pillow` などでコントラストを上げる前処理を行うと、 **スキャン PDF を認識** するステップの精度が劇的に向上します。

## 完全スクリプト: 1 回の実行で PDF をテキストに変換

以下は全体をまとめた実行可能スクリプトです。`pdf_to_text.py` として保存し、`python pdf_to_text.py` で実行してください。

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**スクリプト実行後**、`output` フォルダが作成され、`page_1.txt`、`page_2.txt` … といったファイルが生成されます。これにより、 **PDF からテキストを抽出** する作業が構造化された形で完了します。

## ソリューションのテスト

1. **サニティチェック** – 生成された `.txt` ファイルを開き、先頭数行が元文書のヘッダーと一致するか確認します。  
2. **パフォーマンステスト** – `time` コマンドで 100 ページの PDF に対する実行時間を測定します。期待以上に時間がかかる場合は、ライブラリのマルチスレッドフラグ（例：`engine.set_threads(4)`）を有効にしてください。  
3. **品質保証** – OCR 出力と手入力した抜粋を diff ツールで比較し、クリーンなスキャンの場合は文字精度 95 % 以上を目指します。

## 次のステップと関連トピック

- **精度向上**: `engine.dpi = 300` を試す、または OCR 前に画像前処理（デスケュー、ノイズ除去）を実施。  
- **検索可能 PDF**: `PyPDF2` や `pdfplumber` などの PDF ライブラリで抽出テキストを元 PDF に埋め込み、検索可能にする。  
- **自然言語処理**: 抽出テキストを spaCy や NLTK に渡し、エンティティ抽出、感情分析、キーワードタグ付けを実施。  
- **自動化パイプライン**: `watchdog` と組み合わせ、フォルダを監視して新規ファイルが追加されるたびに **PDF をテキストに変換** する仕組みを構築。

これらのパターンを習得すれば、次のようなことが可能になります。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、実装例とステップバイステップの解説が含まれており、API の追加機能や代替実装アプローチを自分のプロジェクトで活用できるようになります。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}