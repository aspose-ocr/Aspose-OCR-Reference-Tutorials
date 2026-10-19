---
category: general
date: 2026-03-18
description: Aspose OCR を使用して、スキャンしたファイルから検索可能な PDF を作成します。スキャンした PDF の変換、PDF からのテキスト抽出、テキスト
  PDF の認識方法をすばやく学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: ja
og_description: 検索可能なPDFを即座に作成します。このガイドに従って、スキャンしたPDFを変換し、PDFからテキストを抽出し、Aspose OCR
  を使用してテキストを認識してください。
og_title: 検索可能なPDFを作成 – Aspose OCRでステップバイステップ
tags:
- OCR
- PDF
- Aspose
- Python
title: 検索可能なPDFを作成 – Aspose OCRでスキャンPDFを変換
url: /ja/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能な PDF の作成 – ステップバイステップガイド  

スキャンしたページの山から **create searchable PDF** を作成する必要があったことはありませんか？ しかし、どこから始めればいいか分からないこともあるでしょう。あなたは一人ではありません—最初のスキャンがサーバーに届いたとき、多くの開発者が同じ壁にぶつかります。  

良いニュースは、Aspose OCR を使えば、ほんの数行のコードで **convert scanned pdf** ができ、検証のために **extract text from pdf** が可能で、さらにリアルタイムで **recognize text pdf** も行えることです。このチュートリアルでは、ライブラリのインストールから完全な検索可能ドキュメントの保存まで、全プロセスを順に解説し、**convert image pdf** のエッジケースを扱うためのいくつかのヒントも紹介します。

## 達成できること  

このガイドの最後までに、以下ができるようになります：

* スキャンした PDF（または画像のみの PDF）を Aspose OCR に読み込む。  
* エンジンに処理するページを指定する – 必要なページだけを処理したいときに便利です。  
* OCR 結果を元のファイルに埋め込み、出力を真の **searchable PDF** にする。  
* ページ数を出力して操作を検証し、必要に応じて抽出したテキストをダンプする。  

外部サービスや隠されたマジックは不要です—純粋に Python と Aspose の API だけです。

## 前提条件  

* Python 3.8 以上。  
* `aspose-ocr` パッケージ – `pip install aspose-ocr` でインストール。  
* スキャンした PDF ファイル（または画像のみを含む PDF）。  
* Python スクリプトの基本的な知識。  

これらがすでに揃っているなら、素晴らしい—さっそく始めましょう。

<img src="searchable-pdf-workflow.png" alt="検索可能な PDF ワークフロー">  

（OCR パイプラインの図 – コードには不要ですが、視覚的学習者に役立ちます。）

## ステップ 1 – OCR エンジンの初期化  

まず最初に、`OcrEngine` インスタンスが必要です。これは、すべてのピクセルを読み取り、Unicode 文字に変換する脳のようなものです。

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Why this matters:** エンジンがなければオプションを設定したり認識を実行したりできません。早めに初期化しておくことで、後でカスタム辞書を添付する場所も確保できます。

## ステップ 2 – ソース PDF の読み込み  

Aspose OCR は PDF を直接読み取れるため、各ページを自分でラスタライズする必要はありません。エンジンにファイルを指すだけです。

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Pro tip:* PDF が巨大な場合、ストリームから読み込むことでディスク上のファイルロックを回避することを検討してください。

## ステップ 3 – PDF 認識オプションの設定  

ここで二次キーワードが活きてきます。エンジンに特定のページだけ **convert scanned pdf** させ、認識されたテキストを埋め込んだり、元の画像をそのまま残すこともできます。

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Why this matters:**  
* `setEmbedRecognisedText(True)` は、ラスタ PDF を **searchable PDF** に変える鍵です。  
* `setPageRange` は **convert image pdf** を選択的に行うのに役立ちます—大きな文書で数ページだけ OCR が必要な場合に便利です。  
* テキスト抽出を有効にすると、後でビューアを開かずに **extract text from pdf** が可能になります。

## ステップ 4 – オプションをエンジンに添付  

オプションをエンジンにバインドします。このステップは見落としがちですが、スキップするとエンジンはデフォルト設定で動作し（検索可能テキストがありません）

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## ステップ 5 – 選択したページで OCR を実行  

すべてが接続されたら、実際の認識は単一のメソッド呼び出しです。

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

マルチメガバイトの文書を処理する場合、`OcrException` を捕捉し問題のページをログに記録するために、try/except ブロックで囲むことを検討してください。

## ステップ 6 – 結果の検証  

簡単な妥当性チェックとして、エンジンが処理したと考えるページ数を出力します。さらに、**extract text from pdf** が必要な場合は生テキストを取得できます。

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Why you care:** ページ数が表示されることで `setPageRange` が機能したことが確認でき、抽出されたテキストの抜粋が OCR が実際に文字を認識したことを証明します。

## ステップ 7 – 検索可能な PDF を保存  

最後に、出力をディスクに書き戻します。`ImageFormats.PDF` 定数は、Aspose にファイルを PDF のまま保持させ、検索可能なテキストが付加された状態にします。

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

生成されたファイルを任意の PDF リーダーで開き、テキスト検索を試してみてください—これで **created searchable pdf** が完了です！

## エッジケースの一般的な処理  

### ソースが *画像のみ* PDF の場合  

入力 PDF が画像のみ（テキスト層がない）場合でも、同じコードが機能します—`setEmbedRecognisedText(True)` が有効なままであることを確認してください。精度向上のために DPI を上げることも検討してください：

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### 複数言語への対応  

Aspose OCR は言語パックをサポートしています。`recognize()` を呼び出す前に言語をロードします：

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### 大規模文書  

500ページのスキャン PDF の処理はメモリ集約的になる可能性があります。ジョブを分割しましょう：

1. `setPageRange(start, end)` でページ範囲をループする。  
2. 各チャンクを一時的な検索可能 PDF として保存する。  
3. `PdfMerger`（別の Aspose コンポーネント）でチャンクをマージする。

## 完全な動作例（すべてのステップをまとめて）

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

このスクリプトを実行すると、Adobe Reader、Chrome、または任意の PDF ビューアで開き、単語を即座に検索できる **searchable PDF** が得られます。

## 結論  

これで、Aspose OCR を使用して **create searchable PDF** ファイルを作成するための完全なエンドツーエンドソリューションが手に入りました。ソースの読み込み、**convert scanned pdf** のオプション設定、テキストの抽出と検証、そして最終的に検索可能な結果を保存するまで、すべてのステップが網羅されています。  

次に、ソースが JPEG の連続で PDF にパックされた **convert image pdf** のシナリオを探求したり、多言語文書の精度向上のために言語固有の OCR を深掘りしたりしたいかもしれません。いずれにせよ、パターンは同じです：オプションを設定し、`recognize()` を実行し、保存する。  

自由に実験してください—ページ範囲を変更したり、DPI を調整したり、カスタム辞書を組み込んだり。問題が発生したら、下にコメントを残すか、Aspose の公式ドキュメントで最新の API のニュアンスを確認してください。OCR を楽しんでください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}