---
category: general
date: 2026-03-28
description: PythonでPDFのOCRをすばやく学びましょう。このガイドでは、PDFからテキストを抽出する方法、PDFのテキストを認識する方法、そしてスキャンしたPDFをAspose
  OCRを使用してテキストに変換する方法を示します。
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: ja
og_description: PythonでPDFのOCRをマスターしよう。PDFからテキストを抽出し、文字を認識し、スキャンしたPDFを数分でテキストに変換します。
og_title: PythonでPDFをOCRする方法 – 完全ガイド
tags:
- PDF
- OCR
- Python
- Aspose
title: PythonでPDFをOCRする方法 – ステップバイステップガイド
url: /ja/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFをOCRする方法 – ステップバイステップガイド

PDFファイルがページの画像だけの場合、**PDFをOCRする方法**を疑問に思ったことはありませんか？ あなただけではありません。このチュートリアルでは、PDFファイルをOCRし、PDFからテキストを抽出し、スキャンされたPDFを検索可能なテキストに変換する正確な手順を、シンプルなPythonコードだけで解説します。

Aspose OCRライブラリのインストールから各ページの認識テキストを取得するまで、すべてをカバーします。最後までに、**PythonでPDFをOCRする**、**PDFからテキストを抽出する**、そして**スキャンされたPDFをテキストに変換する**ことができ、散在するドキュメントを探し回る必要はありません。余計な説明はなく、実用的で実行可能なサンプルをそのままコピー＆ペーストできます。

## 必要なもの

* Python 3.8+（最新の安定版が最適です）  
* Aspose OCR for Python のライセンスまたは無料トライアルキー – Asposeのウェブサイトから取得できます。  
* 処理したいスキャン済みPDF（ここでは `input.pdf` と呼びます）。  

すでに揃っているなら、素晴らしいです—さっそく始めましょう。まだの場合は、パッケージのインストールは簡単で、手順をご紹介します。

## PDFをOCRする方法 – 環境設定

最初に行うべきことは、Aspose OCRモジュールをマシンに導入することです。パッケージ名は `aspose-ocr` で、pipを使ってインストールできます：

```bash
pip install aspose-ocr
```

> **プロのコツ:** 仮想環境（`python -m venv venv`）を使用すると、依存関係が整理された状態を保てます。

パッケージがインストールされたら、インポートしてOCRエンジンを起動する準備が整います。これは、後で構築するすべての **ocr pdf with python** ワークフローの基盤となります。

## PythonでPDFをOCRする – Aspose OCR のインポート

ライブラリが利用可能になったので、スクリプトに取り込みましょう。また、エンジンを *direct PDF mode* に設定します。これにより、Asposeは各ページを画像に変換せず、PDFバイトを直接ファイルから読み取ります。

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

`PdfMode.DIRECT` を使用する理由は何ですか？ 余分なラスタライズ処理を省くことで、処理が高速化され、元のレイアウトが保持されます—特に **recognize text from PDF** を正確に行う必要がある場合に便利です。

## PDFからテキストを認識する – エンジンの実行

エンジンの準備ができたら、スキャンしたファイルを指定します。`recognize_from_pdf` メソッドがすべての重い処理を行い、各ページを解析し、OCRアルゴリズムを実行し、`Page` オブジェクトのコレクションを含む `OcrResult` オブジェクトを返します。

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

暗号化されたPDFでも動作するか気になる場合—はい、`recognize_from_pdf` を呼び出す前に `ocr_engine.password = "secret"` でパスワードを設定すれば動作します。多くのチュートリアルが省略しがちなエッジケースですが、実務のパイプラインでは有用です。

## PDFからテキストを抽出する – ページ結果へのアクセス

`ocr_result.pages` リストはページごとに1つのエントリを保持します。各 `Page` オブジェクトは、スキャンされたページのプレーンテキスト表現を含む `.text` 属性を持ちます。ループで結果を出力し、抽出された内容を確認しましょう。

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

スクリプトを実行すると、以下のような出力が得られます：

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

この出力は、Aspose OCR を使用して **PDFからテキストを抽出** し、**PDFからテキストを認識** に成功したことを示しています。これで文字列をデータベースや検索インデックス、あるいは downstream の NLP パイプラインに流し込むことができます。

![OCR PDF の例](placeholder-image.png "OCR PDF の例")

*画像の代替テキスト:* **OCR PDF の例** – ページごとの認識テキストのコンソール出力を示しています。

## スキャンされたPDFをテキストに変換する – 出力の保存

多くの開発者はコンソールにテキストを表示するだけでなく、永続的なファイルが必要です。以下は、各ページのテキストを別々の `.txt` ファイルに書き出す小さなヘルパーで、実質的に `output` フォルダーに **スキャンされたPDFをテキストに変換** します。

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

スクリプトが完了すると、整理されたディレクトリが作成されます：

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

これで **スキャンされたPDFをテキストに変換** が完了し、これらのファイルを検索、分析、あるいは単純な `grep` などの downstream プロセスに投入できます。

## よくある質問とエッジケース

**PDFに画像と実際のテキストが混在している場合はどうすればいいですか？**  
Aspose OCR はすべてを認識しようとしますが、選択可能なテキストがすでに含まれているページでは OCR を無効にすることで処理を高速化できます。`ocr_engine.auto_detect_page_orientation = True` を設定し、既知のテキストがあるページについては `ocr_engine.recognize_from_pdf(..., detect_text=False)` を呼び出してください。

**言語モデルを制御できますか？**  
もちろんです。`recognize_from_pdf` を呼び出す前に `ocr_engine.language = aocr.Language.English`（またはサポートされている任意の言語）を設定してください。これにより、英語以外の文書の精度が向上します。

**非常に大きなPDF（100ページ以上）をどう処理すればいいですか？**  
チャンク単位で処理します。`recognize_from_pdf` メソッドは `page_range` 引数を受け取ります。例: `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`。範囲ごとにループしてメモリ使用量を抑えます。

## 完全な動作例

すべてをまとめると、`ocr_pdf.py` というファイルに保存して実行できる単一スクリプトは以下の通りです：

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

次のコマンドで実行します：

```bash
python ocr_pdf.py
```

各ページのテキストと保存された `.txt` ファイルの場所がコンソールに出力されるはずです。

## 結論

Python を使用した **PDFのOCR方法** を解説し、**ocr pdf with python** のクリーンな手法を示し、**PDFからテキストを抽出** する方法を紹介し、**recognize text from PDF** の仕組みを説明し、最後に **スキャンされたPDFをテキストに変換** できる実用的なスニペットを提供しました。全体のプロセスは以下のようにまとめられます

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}