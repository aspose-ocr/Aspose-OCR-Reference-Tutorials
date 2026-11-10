---
category: general
date: 2026-06-25
description: Python を使って PDF のテキストを OCR で抽出します。明確な Python OCR の例で PDF をテキストに変換する方法を学び、迅速に信頼できる結果を得ましょう。
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: ja
og_description: PythonでPDFテキストをOCR抽出。このガイドでは、PDFをテキストに変換し、マルチページ文書を簡単に処理できるPython
  OCRの例を紹介します。
og_title: PythonでPDFテキストをOCR抽出 – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: PythonでPDFテキストをOCR抽出する完全ステップバイステップガイド
url: /ja/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFテキストOCRを抽出 – 完全ステップバイステップガイド

PDFのテキストを **extract pdf text OCR** したいと思ったことはありませんか？でも、マルチページPDFを手間なく処理できるライブラリが分からずに困ったことは…？ あなただけではありません。実務では、法的契約書やスキャンされた請求書、アーカイブされたレポートなど、PDFからクリーンで検索可能なテキストを取得することが必須スキルです。

このチュートリアルでは、Aspose.OCR を使った **python ocr example** を通じて **convert pdf to text** を実現する方法をステップバイステップで解説します。最終的には、すべてのページのテキストを取得し、プレビューを表示し、全文を単一の `.txt` ファイルとして保存できるスクリプトが手に入ります。余計な説明は省き、すぐにコードベースに組み込める実践的な解決策をご提供します。

## 学べること

- Aspose OCR モジュールのインストールとインポート方法  
- OCR エンジンのインスタンスを作成し、マルチページPDFに対して **extract pdf text OCR** を実行する方法  
- 各ページの結果をイテレートし、プレビューを表示し、全文をディスクに書き出す方法  
- 空白ページや Unicode 文字など、よくある落とし穴への対処法  

> **前提条件:** Python 3.8+ がインストールされていること、pip の基本操作が分かること、処理したい PDF ファイルが用意されていること。OCR の事前知識は不要です。

---

![Extract PDF Text OCR workflow diagram](extract-pdf-text-ocr.png "Diagram of extract pdf text OCR process")

*Alt text: Diagram illustrating the extract pdf text OCR workflow in Python.*

## 手順 1: Aspose OCR for Python をインストール

コードを実行する前に、Aspose.OCR パッケージを入手する必要があります。PyPI で配布されているので、pip コマンド一つで完了します。

```bash
pip install aspose-ocr
```

> **プロのコツ:** 仮想環境内で作業している場合（強く推奨）、まず仮想環境を有効化して依存関係を分離してください。

## 手順 2: モジュールをインポートし OCR エンジンを作成

ライブラリが利用可能になったら、モジュールをインポートし `OcrEngine` を起動します。エンジンは文字認識やページレイアウトの処理、クリーンな Unicode 文字列の返却といった重い作業を担う「頭脳」です。

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **重要ポイント:** エンジンは一度だけインスタンス化し、ページ間で再利用する方がはるかに効率的です。ページごとに新しいエンジンを作成すると設定がばらばらになるリスクもあります。

## 手順 3: PDF の全ページを認識（マルチページ OCR）

Aspose.OCR の `recognize_multi_page` メソッドはファイルパスを受け取り、ページごとの `OcrResult` オブジェクトのリストを返します。これが **convert pdf to text** の中心処理です。

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **エッジケース:** PDF がパスワードで保護されている場合、`engine.set_password("your_password")` でパスワードを設定してから `recognize_multi_page` を呼び出す必要があります。

## 手順 4: 結果をイテレートしてプレビュー表示

簡単なプレビューで OCR が正しくテキストを取得できているか確認できます。各ページの先頭 200 文字を出力しますが、必要に応じてスライス幅は調整可能です。

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**サンプル出力**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

上記は抜粋です。全文は `page_result.text` に格納されています。

## 手順 5: すべてのページを単一のテキストファイルに結合（任意）

検索インデックス作成やデータ分析、単純なアーカイブなど、下流の多くのワークフローは単一の `.txt` ファイルを好みます。ページを連結して書き出しましょう。

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **この方法が有効な理由:** UTF‑8 で保存すれば、法律文書に頻出するアクセント付き文字や記号などの特殊文字が失われません。

## 手順 6: よくある落とし穴への対処

| 問題 | 症状 | 対策 |
|------|------|------|
| 出力が空白ページになる | `page_result.text` が空 | 元の PDF が実際にスキャン画像を含んでいるか確認。テキストベースの PDF であれば別の抽出ライブラリが必要です（例: PDF テキスト抽出ライブラリ）。 |
| 文字化け | 文字の代わりに奇妙な記号が表示 | OCR エンジンの言語設定を正しく行う: `engine.language = ocr.Language.English`（または対象言語）。 |
| 大きな PDF が時間がかかりすぎる | スクリプトが特定のページで止まっているように見える | マルチスレッド化を有効にする: `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`。 |
| 巨大ファイルでメモリエラー | `MemoryError` が発生 | PDF をチャンク（例: 50 ページずつ）に分割して処理するか、Python のメモリ上限を増やす。 |

## 完全スクリプト – すぐに実行可能

すべてをまとめた、`extract_pdf_text_ocr.py` という名前で保存できる自己完結型スクリプトです。

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

ターミナルから実行します:

```bash
python extract_pdf_text_ocr.py
```

ページプレビューがコンソールに表示され、続いて全文が保存されたことが確認できます。

## まとめ & 次のステップ

今回、**extract pdf text OCR** をシンプルな **python ocr example** で **convert pdf to text** する方法を実演しました。インストール、インポート、エンジン作成、`recognize_multi_page` 実行、プレビュー、保存という基本フローは、スキャンされた PDF の一般的な処理に最適です。

**次にやること:**  

- **精度の微調整:** `engine.recognize_multi_page(..., RecognizeOptions(...))` で DPI を変更したり、言語パックを利用したりして精度を上げる。  
- **後処理:** 余分な空白を除去したり、スペルチェックを走らせたり、テキストを自然言語処理パイプラインに流したりする。  
- **バッチ処理:** フォルダ内の複数 PDF をループ処理して検索可能なアーカイブを構築する。  

問題が発生した場合は、対象 PDF が実際にラスタ画像を含んでいるか再確認してください。OCR は画像上の文字にしか作用しません。テキストが埋め込まれた PDF であれば、`pdfminer.six` や `PyMuPDF` といったライブラリの使用を検討してください。

---

**Happy coding!** このガイドで **extract pdf text OCR** が実現できたら、コメントで結果を共有したり、Aspose OCR の GitHub ページで機能リクエストを投稿したりしてください。実験を続ければ、スキャン PDF を検索可能かつ編集可能なテキストに変換する堅牢なパイプラインがすぐに手に入ります。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用・拡張するための関連トピックです。各リソースには、ステップバイステップの解説と動作するコード例が含まれており、API の追加機能習得や代替実装アプローチの探索に役立ちます。

- [Aspose OCR で画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}