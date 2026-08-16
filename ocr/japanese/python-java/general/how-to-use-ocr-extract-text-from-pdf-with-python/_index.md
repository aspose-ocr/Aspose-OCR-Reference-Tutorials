---
category: general
date: 2026-04-26
description: スキャンしたPDFにOCRを使用し、テキストを抽出し、PDFにOCRを実行し、数ステップで検索可能なファイルに変換する方法。
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: ja
og_description: PythonでOCRを使用する方法：PDFからテキストを抽出し、PDFにOCRを実行し、スキャンしたPDFを検索可能な文書に変換する方法を学びましょう。
og_title: OCRの使い方 – PDFからテキストを抽出するクイックガイド
tags:
- OCR
- Python
- PDF
- Text Extraction
title: OCRの使い方 – PythonでPDFからテキストを抽出する
url: /ja/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR の使い方 – Python で PDF からテキストを抽出する

スキャンされた契約書、領収書、または電子書籍からテキストを抽出するために **OCR の使い方** を疑問に思ったことはありませんか？ あなただけではありません。実際のプロジェクトでは、受け取る PDF が単なる画像であることが多く、OCR がなければ内容を検索したり、インデックス付けしたり、分析したりすることができません。

このチュートリアルでは、**OCR の使い方**、**PDF からテキストを抽出する方法**、そしてスキャンした PDF を検索可能なドキュメントに **変換する** 必要性を示す、完全に実行可能なサンプルを順に解説します。また、OCR エンジンが各ページを正確に認識できるように **PDF を画像として読み込む** 微妙なテクニックも取り上げます。

> **クイックプレビュー:** 最後まで実行すれば、マルチページ PDF を読み込み、各ページに OCR を実行し、認識されたテキストを出力するスクリプトが手に入ります – 外部サービスは不要です。

## 必要なもの

- Python 3.9+（最新バージョンであれば問題ありません）
- `aocr` パッケージ（または `OcrEngine` と `Image.load` を提供する互換 OCR ライブラリ）
- 処理したいスキャン済み PDF ファイル（例: `contract.pdf`）
- ほどほどの RAM（100 ページの PDF あたり約 200 MB が目安）

OCR ライブラリがまだインストールされていない場合は、以下を実行してください。

```bash
pip install aocr
```

> **プロのコツ:** 仮想環境を使用して依存関係を整理しましょう。

## Step 1: Load PDF as Image – The First Piece of the Puzzle

OCR を実行する前に、PDF を画像として表現する必要があります。ここで副キーワード **load pdf as image** が登場します。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Why this matters:* `aocr.Image.load` は内部で各 PDF ページをビットマップにラスタライズし、OCR エンジンが理解できる形式に変換します。このステップを省いて生の PDF を渡すと、エンジンはベクターデータではなくピクセルデータを期待しているためエラーを返します。

> **注意:** パスは絶対でも相対でも構いません。ファイルが読み取り可能であることを確認してください。そうでなければ `FileNotFoundError` が発生します。

## Step 2: Run OCR on PDF – Turning Pixels into Characters

PDF が画像として扱えるようになったので、いよいよ **run OCR on PDF** が可能です。以下のスニペットはすべてのページを一括で処理します。

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*What’s happening under the hood?* `process_all_pages` はラスタライズされたページを順に走査し、OCR モデルを適用して、ページごとの結果オブジェクトのリストを返します。各結果には認識テキスト、信頼度スコア、バウンディングボックス（必要に応じて）が含まれます。

## Step 3: Extract Text from PDF – Pulling the Strings Out

OCR 結果が得られたら、プレーンテキストの抽出は非常に簡単です。ページをイテレートして出力を表示し、**extract text from pdf** という副キーワードを実演します。

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Expected output** (truncated for brevity):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

テキストを単一の文字列にしたい場合は、単に結合すれば OK です。

```python
full_text = "\n".join(r.text for r in page_results)
```

これで OCR を使って **PDF からテキストを抽出** できました。

## Step 4: Convert Scanned PDF – Making It Searchable

Elasticsearch や SharePoint などの多くの下流ツールは、プレーンテキストのダンプではなく検索可能な PDF を期待します。OCR の出力を元の PDF に埋め込むことで、実質的に **convert scanned PDF** して検索可能なバージョンを作れます。

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Why bother?* 検索可能な PDF は元のレイアウトや画像を保持しつつ、テキスト選択やインデックス作成が可能になるため、ヒトにもマシンにもメリットがあります。

## Common Pitfalls & Edge Cases

### Multi‑Page PDFs Larger Than Memory

PDF が数百ページに及ぶ場合、一度にすべてを読み込むと RAM が不足することがあります。`aocr` ライブラリは遅延読み込みをサポートしています。

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

その後、ページを一つずつ処理します。

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Low‑Quality Scans

ぼやけた画像やコントラストが低いスキャンでは OCR の精度が大幅に低下します。エンジンに渡す前に前処理を検討してください。

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Language Support

デフォルトではエンジンは英語を想定しています。別言語で **run OCR on PDF** したい場合は、言語コードを設定します。

```python
ocr_engine.language = "spa"  # Spanish
```

対応する言語モデルがインストールされていることを確認してください。

## Full Working Example

すべてを統合した、`ocr_pdf.py` というファイルに保存してすぐに実行できる自己完結型スクリプトです。

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

以下のように実行します。

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

コンソールにテキストが表示され、`-o` オプションを指定した場合は元ファイルの横に検索可能な PDF が生成されます。

## Pro Tips & Best Practices

- **Batch processing:** 数十個の PDF を扱う際は、上記ロジックをループで包み、各ファイルの成功／失敗をログに残しましょう。
- **Confidence filtering:** 各 `page_result` には信頼度メトリックが含まれます。信頼度が低いページは除外または手動レビュー用にフラグを立ててください。
- **Parallelism:** CPU にコアが複数ある場合は、`concurrent.futures` を使ってページを並列処理すると効率的です – ただしメモリ使用量に注意しましょう。
- **Version lock:** `aocr` API は変化する可能性があります。`requirements.txt` でバージョンを固定（例: `aocr==2.3.1`）して、破壊的変更を回避してください。

## Conclusion

**OCR の使い方** を通じて **PDF からテキストを抽出**、**PDF に OCR を実行**、**PDF を画像として読み込む**、さらには **スキャンした PDF を検索可能に変換** する方法を解説しました。コードは完全で、説明は *何を* と *なぜ* の両方をカバーしています。これで画像ベースの PDF を扱うあらゆるプロジェクトで再利用できるパターンが手に入りました。

次は何をしますか？ 抽出したテキストを自然言語処理パイプラインに流し込んだり、Elasticsearch で検索可能な PDF をインデックスしたり、Tesseract や Azure Computer Vision など別の OCR バックエンドを試したりしてみましょう。可能性は無限大、ツールはすでに手元にあります。

Happy coding, and may your PDFs always be searchable! 

![OCR の使い方例](/images/ocr_workflow.png "OCR の使い方")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}