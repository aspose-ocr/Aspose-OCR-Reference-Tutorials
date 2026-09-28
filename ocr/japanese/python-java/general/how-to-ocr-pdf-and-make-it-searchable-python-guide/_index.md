---
category: general
date: 2026-01-12
description: PythonでPDFをOCRし、PDFをすばやく検索可能にする方法を学びましょう。スキャンしたPDFを変換し、テキストを抽出し、Aspose
  OCRを使用してPythonでスキャンPDFをOCRします。
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: ja
og_description: PythonでPDFをOCRする方法は？このステップバイステップのチュートリアルでは、スキャンしたPDFファイルを検索可能なPDFに変換し、Aspose
  OCRでテキストを抽出する方法を紹介します。
og_title: PDFをOCRして検索可能にする方法 – Pythonガイド
tags:
- OCR
- Python
- PDF processing
title: PDFをOCRして検索可能にする方法 – Pythonガイド
url: /ja/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF を OCR して検索可能にする方法 – Python ガイド

商用ソフトに高額な費用をかけずに **PDF を OCR** する方法を考えたことはありませんか？ あなただけではありません。スキャンした契約書や請求書、画像ベースの PDF を検索可能なドキュメントに変換しなければならないとき、多くの開発者が壁にぶつかります。良いニュースは、Python と Aspose OCR の数行のコードで、スキャンした PDF を変換し、テキスト PDF を抽出し、最終的に数分で PDF を検索可能にできることです。

このチュートリアルでは、ライブラリのインストール、言語設定、スキャンした PDF の処理、元の画像と隠れたテキスト層の両方を含む検索可能な PDF として結果を保存するまで、必要なすべての手順を解説します。最後まで読むと、任意のプロジェクトに組み込める再利用可能なスクリプトが手に入り、手動でのコピーペーストは不要です。

---

## 必要なもの

- **Python 3.8+**（コードは 3.9、3.10、以降でも動作します）
- 有効な **Aspose OCR for Python** ライセンス（無料トライアルでも実験可能）
- 検索可能にしたいスキャン済み PDF ファイル（例: `scanned_contract.pdf`）
- コマンドラインと仮想環境の基本的な知識（任意ですが推奨）

> **プロのコツ:** まだライセンスをお持ちでない場合は、Aspose のウェブサイトで 30 日間のトライアルにサインアップしてください。トライアル版は開発目的で完全に機能します。

## Aspose OCR を使用した PDF の OCR 方法 (Primary Keyword in H2)

最初のステップは、適切なパッケージを取得することです。Aspose OCR は、低レベルの画像処理の詳細を抽象化したクリーンでハイレベルな API を提供します。

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

パッケージがインストールされたら、スクリプトの作成を開始できます。

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **なぜ言語を設定するのか？**  
> OCR の精度は言語モデルに大きく依存します。エンジンに英語テキストを期待させることで、誤検出を減らし、処理速度を向上させます。

## ステップ 2: スキャンした PDF を検索可能な PDF に変換

エンジンの準備ができたら、スキャンしたドキュメントを指定します。`process_pdf` メソッドは、元の画像データと認識されたテキストの両方を含む `PdfResult` オブジェクトを返します。

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

大量の **スキャンした PDF** を変換する必要がある場合は、ディレクトリをループして各ファイルに対して `process_pdf` を呼び出すだけです。エンジンはマルチページ PDF を自動的に処理します。

## ステップ 3: 結果を検索可能な PDF として保存 (Make PDF Searchable)

パズルの最後のピースは、検索可能なバージョンを永続化することです。Aspose OCR ではこれがワンライナーで実現できます。

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

`contract_searchable.pdf` を任意の PDF ビューアで開くと、元のスキャン画像が表示されますが、OCR エンジンが認識した **任意の単語** を検索できるようになります。隠れたテキスト層は目には見えませんが、完全にインデックス可能です。

### 完全スクリプト – 実行準備完了

以下に完全な実行可能サンプルを示します。`make_searchable.py` という名前のファイルにコピー＆ペーストし、環境に合わせてパスを調整してください。

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**期待される出力:**  
スクリプトを実行すると確認メッセージが表示され、`contract_searchable.pdf` が作成されます。ファイルを開き、`Ctrl + F` で元のスキャン画像に含まれる任意の単語を入力すると、即座に一致がハイライトされます。

## よくある質問とエッジケース

### 1. PDF に複数の言語が含まれている場合は？

エンジンに言語のリストを渡すことができます：

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR は同一ページ内の両方の言語を認識しようとします。

### 2. 低解像度のスキャンをどう処理するか？

元画像が 150 dpi 未満の場合、OCR の精度が低下する可能性があります。`pdfimages` などのツールでページを抽出し、Pillow でアップスケールした後、`process_pdf` に高解像度画像を渡すと効果的です。

### 3. 検索可能な PDF を作成せずにプレーンテキストだけ抽出できますか？

もちろん可能です。`PdfResult` オブジェクトの `text` プロパティでテキストを取得できます：

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

この方法は、**テキスト PDF を抽出** したいケースに最適です。

### 4. PDF フォルダーをバッチ処理する方法はありますか？

はい、`ocr_to_searchable` 関数をシンプルなループでラップすれば実現できます：

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

これで **スキャンした pdf** を一括で変換できます。

## パフォーマンスのヒント

- **エンジンを再利用**: ファイルごとに新しい `OcrEngine` を作成するとオーバーヘッドが増えます。1 回インスタンス化して複数回呼び出すようにしましょう。
- **並列処理**: 大量バッチの場合は Python の `concurrent.futures.ThreadPoolExecutor` を検討してください。Aspose OCR は読み取り専用操作に対してスレッドセーフです。
- **メモリ管理**: 数百ページ規模の非常に大きな PDF を処理する場合、各ファイル処理後に `gc.collect()` を呼び出してメモリを解放すると効果的です。

## 結論

Python で **PDF を OCR** する方法、スキャンを **検索可能な PDF** に変換する方法、そして **テキスト PDF を抽出** する方法を網羅しました。Aspose OCR を使えば、マルチページ文書、複数言語、高精度認識を数行のコードで実現できます。

ぜひ自分の契約書、請求書、アーカイブされた研究論文で試してみてください。基本をマスターしたら、カスタム辞書、画像前処理、Elasticsearch などの全文検索インデックスへの統合といった高度な機能にも挑戦してみましょう。

**ocr scanned pdf python** に関する追加質問や、難しいスキャンのトラブルシューティングが必要な場合は、下のコメント欄に書き込んでください。ハッピーコーディング！

--- 

![how to ocr pdf example](image-placeholder.png){alt="PDF OCR の例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}