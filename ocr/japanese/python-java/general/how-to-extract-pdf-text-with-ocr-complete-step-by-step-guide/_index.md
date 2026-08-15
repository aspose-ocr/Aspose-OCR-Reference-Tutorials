---
category: general
date: 2026-03-26
description: OCRを使用してPDFテキストを抽出する方法。PDFを画像として読み込み、PDFテキストを認識し、シンプルなPython例でPDFからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: ja
og_description: OCR を使用して PDF のテキストを抽出する方法。このガイドでは、PDF を画像として読み込み、PDF のテキストを認識し、Python
  で PDF からテキストを抽出する方法を示します。
og_title: OCRでPDFテキストを抽出する方法 – 完全チュートリアル
tags:
- OCR
- Python
- PDF processing
title: OCRでPDFテキストを抽出する方法 – 完全ステップバイステップガイド
url: /ja/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRでPDFテキストを抽出する方法 – 完全ステップバイステップガイド

実際にはスキャン画像だけの **PDFを抽出する方法** を考えたことがありますか？同じ壁にぶつかる開発者は多いです。検索可能なコンテンツが必要なのに、画像だけのPDFしかないというケースです。朗報です！数行のコードと堅実なOCRライブラリさえあれば、画像PDFを瞬時にプレーンテキストに変換できます。  

このチュートリアルでは、**OCRの使い方** を通じてPDFを画像として読み込み、PDFテキストを認識し、最終的に **PDFからテキストを抽出する** 方法を解説します。最後まで読むと、実行可能なスクリプト、各ステップの明確な説明、そして一般的な落とし穴を回避するためのヒントが手に入ります。

## 必要なもの

- Python 3.9 以上（コードは3.10+でも動作します）  
- `ocr` Python パッケージ（または `OcrEngine`、`OcrEngineMode`、`Imaging.Image` を提供する互換性のあるOCRライブラリ）  
- 処理したいマルチページPDF（デモでは `multi_page.pdf` と呼びます）  
- 仮想環境の基本的な知識（任意ですが推奨）

> **プロのコツ:** Windows を使用している場合は Anaconda Prompt を、macOS/Linux では `python -m venv venv && source venv/bin/activate` で仮想環境を作成すると便利です。

## Step 1: OCR ライブラリをインストール

まず、PyPI から OCR パッケージを取得します。以下の例は、コードスニペットに示した API を模倣した架空の `ocr` パッケージを使用していますが、実際のライブラリ（例: `pytesseract` + `pdf2image`）も同様のパターンです。

```bash
pip install ocr
```

別のエンジンを使用する場合は、`ocr` を適切な名前に置き換えてください（例: `pip install pytesseract pdf2image`）。

## Step 2: OCR エンジンを初期化

エンジンインスタンスの作成は **PDFを抽出する方法** の基礎です。エンジンは各PDFページ内のピクセルを解釈する脳のようなものです。

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **重要ポイント:** `set_engine_mode` で速度と精度のトレードオフが可能です。`DEFAULT` はバランスの取れた選択肢です。より高精度が必要な場合は、ライブラリがサポートしていれば `HIGH_ACCURACY` に切り替えてください。

## Step 3: PDF を画像オブジェクトとしてロード

OCR は画像上で動作し、PDF コンテナ上では動作しません。そのため、まず PDF を画像表現に変換する必要があります。`Imaging.Image.load` メソッドはマルチページPDFを自動的に処理します。

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **エッジケース:** ライブラリによっては単一ページ画像しか受け付けないものがあります。その場合は `pdf2image.convert_from_path` を使って各ページをループ処理します。今回の `load` 呼び出しはそれを抽象化しており、**PDFを画像としてロード** がワンライナーで済みます。

## Step 4: すべてのページでテキストを認識

ここからが **PDFテキストを認識する** 本番です。エンジンは各ページを走査し、ページごとの結果オブジェクトのリストを返します。

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

各 `page_result` には `get_text()`（プレーンテキスト）や `get_confidence()`（任意の品質指標）といったメソッドが含まれます。  

> **ヒント:** 最初の1ページだけが必要な場合は、マルチページヘルパーの代わりに `recognize(pdf_image[0])` を呼び出してください。

## Step 5: 結果を反復処理し、抽出テキストを出力

最後に、結果をループして各ページのテキストを出力します。これで **PDFからテキストを抽出する** ワークフローが完了です。

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### 期待される出力

`multi_page.pdf` に「Hello」「World」「Python」の3ページが含まれている場合、次のように表示されます。

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

これで PDF は完全に検索可能になり、テキストは下流処理（インデックス作成、感情分析など）にすぐ使える状態です。

## Step 6: よくある落とし穴の対処法

| 問題 | 発生理由 | 簡単な対策 |
|------|----------|------------|
| **出力が空** | PDF ページが低 DPI でスキャンされ、文字が判別できない | OCR 前に画像を拡大: `pdf_image = pdf_image.resize(300)`（300 DPI が目安） |
| **文字化け** | ラテン文字以外の言語は言語パックが必要 | 適切な言語モデルをロード: `ocr_engine.load_language('spa')`（スペイン語の場合） |
| **巨大PDFでメモリ不足** | すべてのページを同時にロードすると RAM を大量消費 | ページをバッチ処理: `for img in pdf_image.split(batch=10): …`（疑似コード） |
| **処理が遅い** | 大規模ドキュメントで `DEFAULT` を使用すると遅くなる | `FAST` モードに切り替えるか、`concurrent.futures` で並列実行 |

## ボーナス: 抽出テキストをファイルに保存

実務ではテキストを永続化する必要があります。以下はすべてを `output.txt` に書き込む小さなヘルパーです。

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

これで `output.txt` を検索エンジン、データベース、任意の NLP モデルに投入できます。

## すべてをまとめた完全スクリプト

以下が実行可能なフルプログラムです。コピー＆ペーストして、ファイルパスを調整すればすぐに使えます。

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

実行方法:

```bash
python extract_pdf_ocr.py
```

各ページの内容がコンソールに表示され、`extracted_text.txt` が作成されたことが確認できます。

## 結論

画像のみのPDFからテキストを抽出する **方法** を、OCRエンジンのインストールからマルチページ結果の処理、出力の保存まで網羅しました。これで **OCRの使い方**、**PDFを画像としてロード**、そして **PDFテキストを認識** する手順が確実に身につきました。  

次のステップは？ デフォルトエンジンモードを高精度設定に変えてみる、マルチリンガルPDF向けに言語パックを試す、あるいは抽出テキストを Elasticsearch のような全文検索インデックスに流し込むなどです。テキスト抽出の基本をマスターすれば、PDFファイルからの情報活用は無限に広がります。

---

![PDF抽出例](images/ocr_flowchart.png){alt="PDF抽出ワークフローダイアグラム"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}