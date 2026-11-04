---
category: general
date: 2026-06-06
description: PythonでPDFをOCRし、PDFからテキストを抽出し、スキャンしたPDFのテキストを変換し、数行のコードでOCR言語を変更する方法。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: ja
og_description: PythonでPDFをOCRする方法：PDFからテキストを抽出し、スキャンしたPDFのテキストを変換し、OCR言語を簡単に変更できる実践的ガイド。
og_title: PythonでPDFをOCRする方法 – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: PythonでPDFをOCRする方法 – 完全ステップバイステップガイド
url: /ja/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFをOCRする方法 – 完全ステップバイステップガイド

高価なSaaSツールに払わずに **PDFをOCRする方法** を知りたくありませんか？ あなたは一人ではありません。古い本をデジタル化したり、請求書からデータを抽出したり、スキャンしたレポートから検索可能なテキストが必要だったりする場合、PythonでPDF OCRをマスターすれば手作業のコピーに費やす時間を大幅に削減できます。

このチュートリアルでは、**PDFからテキストを抽出** する簡潔で動作する例を順に解説し、**スキャンしたPDFテキストを編集可能な文字列に変換** する方法、さらに文書が英語でない場合に **OCR言語を変更** する方法も示します。最後まで読めば、どのプロジェクトにもすぐに組み込める再利用可能なスニペットが手に入ります。

## 前提条件とセットアップ

始める前に以下を用意してください。

- Python 3.8+ がインストール済み（コードは 3.9、3.10、以降でも動作します）
- `ocr` パッケージ（`OcrEngine` クラスを提供）※ `pip install ocr-lib` でインストールできます（実際に使用しているパッケージ名に置き換えてください）
- 処理したい PDF ファイル；デモでは `high_res_book.pdf` を `YOUR_DIRECTORY` フォルダーに置きます

仮想環境を使用している場合（強く推奨）、まずそれをアクティベートしてください：

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **プロのコツ:** 後でパス関連のトラブルを防ぐため、PDF ファイルは専用の `data/` ディレクトリに置いておくと便利です。

## Step 1: OCR エンジンインスタンスの作成（How to OCR PDF – Initialization）

**PDFに対してOCRを実行** したいときに最初に行うべきことは、エンジンをインスタンス化することです。エンジンは各ページを読み取り、文字形状を解釈し、プレーンテキストを返す「脳」のようなものです。

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

なぜ重要かというと、エンジンがなければ言語設定やレンダリングオプション、PDF の取り扱いに関するコンテキストがありません。`OcrEngine` オブジェクトはこれらのデフォルトを保持し、後から調整できるようにします。

## Step 2: 認識言語の設定（Change OCR Language）

多くの OCR ライブラリはデフォルトで英語ですが、文書がフランス語、ドイツ語、あるいは日本語の場合はどうでしょうか？ 言語を変更するのは `set_recognition_language` を呼び出すだけです。これにより **OCR言語の変更** 要件を満たし、精度が向上します。

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **この設定が必要になる理由:** 多言語アーカイブには混在した言語のページが含まれることが多いです。実行時に言語を切り替えることで「ß」や「ñ」などの文字が誤認識されるのを防げます。

## Step 3: PDF レンダリングオプションの構成（Convert Scanned PDF Text Effectively）

スキャンした PDF を扱う際、解像度とカラーモードは OCR の品質に大きく影響します。300 DPI のグレースケールはほとんどの文書にとって最適なバランスで、ディテールを十分に捉えつつメモリ使用量も抑えられます。

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

チェーン形式の呼び出しは見た目が派手ですが、同じオプションオブジェクトを返す流暢な API に過ぎません。カラー画像（例：カラー図表）が必要な場合は `"grayscale"` を `"color"` に置き換えてください。

## Step 4: PDF を認識し、最初のページのテキストを取得（Extract Text from PDF）

ここが **PDFに対してOCRを実行** する核心部分です。エンジンにファイルパスを渡し、認識されたテキストを取得します。メソッドはページ結果のリストを返し、各結果は `text` 属性を持ちます。

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

文書全体が必要な場合は `results` をイテレートします：

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### PDF が暗号化されている場合は？

一部の PDF はパスワードで保護されています。その場合は `recognize_pdf` にパスワードを渡すだけです：

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

エンジンは OCR を実行する前にオンザフライで復号化するので、追加の手順は不要です。

## Step 5: 抽出テキストの後処理（Fine‑Tuning Extract Text from PDF）

生の OCR 出力には改行や余分なスペース、時折の誤認識文字が含まれがちです。簡単なクリーンアップルーチンを実行すれば、抽出した文字列を検索インデックスやデータベース保存、その他の下流処理にすぐ使える形に整えられます。

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

これで **PDFからテキストを抽出** でき、任意の NLP パイプラインや検索エンジン、あるいはシンプルな `open(...).write()` 操作に渡すことができます。

## Bonus: 複数 PDF のバッチ処理（Scaling Perform OCR on PDF）

スキャンした PDF が多数ある場合は、ロジックをループで包みます：

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

このスニペットは **PDFに対してOCRを実行** するバルク処理の方法を示しており、デジタル化プロジェクトでよく求められるニーズに応えます。

## Expected Output

単ページの例（Step 4）を実行すると、次のような出力がコンソールに表示されます：

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

複数ページの書籍を処理した場合、各ページのクリーンテキストがコンソールに表示され、バッチスクリプトは各 PDF の横に `.txt` ファイルを生成します。

## Common Pitfalls & How to Avoid Them

| Issue | Symptoms | Fix |
|-------|----------|-----|
| Low‑resolution source PDF | 文字化け、単語欠落 | DPI を上げる（`set_dpi(400)` 以上） |
| Wrong language set | 多数の不明シンボル、特にアクセント文字が誤認識 | `engine.set_recognition_language(ocr.Language.FRENCH)` など適切な enum を使用 |
| Large PDF causing memory error | `MemoryError` または数ページ後のクラッシュ | ページをチャンクで処理（`engine.recognize_pdf(..., max_pages=10)`） |
| Missing fonts in the PDF | 特定ページで空出力 | PDF が実際にラスタ画像を含んでいるか確認。ベクタのみの場合は別の処理が必要 |

## Image Illustration

以下はワークフローの簡易ビジュアルです。代替テキストは SEO を意識して作成しています。

![how to ocr pdf workflow diagram showing engine initialization, language setting, rendering options, recognition, and text extraction](/images/ocr-workflow.png)

*この図はコード実行に必須ではありませんが、視覚的に各ステップの位置付けを理解したい学習者に役立ちます。*

## Conclusion

Python で **PDFに対してOCRを実行** する方法を、エンジン作成、**OCR言語の変更**、**スキャンしたPDFテキストの変換**、そして最終的な **PDFからテキストを抽出** まで一通り解説しました。完全に実行可能なサンプルはどのプロジェクトにもすぐに組み込め、オプションのバッチスクリプトでソリューションをスケールさせる方法も示しました。

次に試したいこと：

- 言語リストをループして **PDFに対してOCRを実行** する多言語アーカイブ対応
- 抽出テキストを Elasticsearch に統合し全文検索を実現
- OCR で生成したテキストレイヤーを元のファイルに埋め込み、検索可能な PDF を作成（多くのライブラリは `save_as_searchable_pdf` メソッドを提供）

自由に実験し、DPI 設定を調整したり、別の OCR バックエンドに切り替えたりしてみてください。基本は変わりませんので、これでしっかりとした土台ができました。

Happy coding, and may your scanned documents finally become searchable!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}