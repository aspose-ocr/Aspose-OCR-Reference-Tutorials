---
category: general
date: 2026-03-18
description: 画像にOCRを実行してPNGからテキストを抽出し、検索可能なPDFを生成します。数分でテキスト画像の認識方法とPNGからPDFへの変換方法を学びましょう。
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: ja
og_description: PNG画像にOCRを実行してテキストを抽出し、文字画像を認識し、検索可能なPDFを生成します。ステップバイステップのガイドに従ってください。
og_title: 画像でOCRを実行 – PNGからテキストを素早く抽出
tags:
- OCR
- Python
- Image Processing
title: 画像でOCRを実行 – PNGからテキストをすばやく抽出
url: /ja/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行 – PNG からテキストをすばやく抽出

**画像で OCR を実行**したいけど、どこから始めればいいか分からないことはありませんか？たとえばスキャンした記事が `article.png` として保存されていて、単にプレーンテキストが欲しい、あるいはアーカイブ用に検索可能な PDF が必要、というケースです。どちらの場合でも、ここが正しい場所です。このチュートリアルでは PNG からテキストを抽出し、テキスト画像を認識し、さらにその PNG を検索可能な PDF に変換する方法を、数行のコードで実演します。

> **得られるもの:** PNG を読み込み OCR を実行し、hOCR 出力を保存し、必要に応じて検索可能な PDF を作成する、完全に実行可能なスクリプトです。インポート忘れや「ドキュメント参照」的な行き止まりはありません—今日からプロジェクトに組み込める自己完結型のソリューションです。

## 前提条件

以下を事前に用意してください：

- **Python 3.8+**（ここで使用している構文は最近のバージョンであればすべて動作します）
- 使用している **`ocr_engine`** ライブラリ（例では `OcrEngine` というクラスを想定しています。必要に応じて Tesseract、EasyOCR などに置き換えてください）
- 処理したい PNG 画像（例: 参照できるフォルダーに配置した `article.png`）
- 出力ディレクトリへの書き込み権限

Tesseract を内部で使用する場合は、以下でインストールしてください：

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

その後、Python ラッパーをインストールします：

```bash
pip install pytesseract Pillow
```

*Pro tip:* OCR ライブラリは常に最新に保ちましょう—新しい言語パックやパフォーマンス向上が頻繁にリリースされます。

## 画像で OCR を実行 – ステップバイステップガイド

以下が **完全なスクリプト** です。`run_ocr.py` というファイル名でコピー＆ペーストし、`python run_ocr.py` で実行してください。

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### スクリプトの内容を平易な日本語で説明

1. **Instantiate**（インスタンス化）して OCR エンジンを作成し、設定を制御できるようにします。
2. **Load**（読み込み）で PNG ファイル（`article.png`）をロードします。ファイルが存在しない場合は早期に終了し、後で `NoneType` エラーが出ることを防ぎます。
3. **Select**（選択）でエクスポート形式を `hocr` に設定します。この形式は元のレイアウト情報を保持し、後で画像を検索可能な PDF に変換する際に必須です。
4. **Run**（実行）で認識エンジンを走らせます。ここで本格的な処理が行われます。
5. **Write**（書き込み）で hOCR XML を `article.hocr` に保存します。これでテキストと座標情報を機械可読形式で取得できます。
6. *(Optional)* `"pdf"` に切り替えて、追加のステップで検索可能な PDF を生成します。

**期待される出力** は UTF‑8 エンコードされた `.hocr` ファイルで、以下のような内容になります（簡略化）：

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

PDF セクションのコメントアウトを外すと、`article_searchable.pdf` も生成されます。この PDF は任意のビューアで開き、**Ctrl + F** の検索ボックスで単語を即座に見つけることができます。

![画像で OCR を実行した例の出力](example.png "画像で OCR – hOCR と PDF の結果")

## OcrEngine を使って PNG からテキストを抽出する方法

レイアウトや PDF が不要で、純粋なテキストだけが欲しい場合は、hOCR のステップを完全にスキップできます：

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Why choose plain text?*（プレーンテキストを選ぶ理由） 軽量でインデックス作成に最適、そして下流の NLP パイプラインでも快適に扱えます。

## テキスト画像を認識し検索可能な PDF を生成する

検索可能な PDF の生成は二段階のプロセスです：

1. `hocr` で **Run OCR**（OCR を実行）し、レイアウト情報を取得します（上記と同様）。
2. エンジンの PDF エクスポート機能を使って、元の PNG と hOCR を組み合わせて PDF を作成します。

ほとんどの最新 OCR ライブラリ（Tesseract、ABBYY、Google Vision）には `pdf` エクスポートが用意されており、まさにこの操作を行います。メインスクリプトの *Optional* ブロックにあるコードがそのパターンです。もし使用しているライブラリに組み込みの PDF エクスポートが無い場合は、**`pdf2image`** と **`reportlab`** を組み合わせて画像と hOCR を結合できます—必要なら追加のサンプルを共有しますのでお知らせください。

## OCR 出力付きで PNG を PDF に変換する

場合によっては、検索可能レイヤーなしの **プレーン PDF**（画像だけを含む）だけが欲しいこともあります。その場合はさらにシンプルです：

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

検索可能版が必要なときは OCR ステップと組み合わせ、アーカイブ目的であればビジュアルレプリカとしてそのまま保存できます。

## よくある落とし穴とヒント

| 問題 | 発生原因 | 簡単な対処法 |
|------|----------|--------------|
| **ぼやけた、または低解像度の PNG** | OCR の精度は約 300 DPI 未満で急激に低下します。 | エンジンに渡す前に `Image.resize((width*2, height*2), Image.LANCZOS)` でアップスケールしてください。 |
| **言語設定が間違っている** | エンジンはデフォルトで英語になるため、非英語文字が文字化けします。 | `ocr_engine.setLanguage('deu')`（または該当する ISO コード）を `recognize()` の前に呼び出してください。 |
| **hOCR 出力が得られない** | `setExportFormat` を呼び出さないと、一部のエンジンはプレーンテキストをデフォルト出力します。 | `recognize()` の **前に** `setExportFormat("hocr")` が実行されているか確認してください。 |
| **ファイル権限エラー** | 読み取り専用フォルダーに書き込もうとしています。 | プロジェクト内の書き込み可能なパスを使用するか、先に `os.makedirs(..., exist_ok=True)` を実行してください。 |
| **大きな PDF がメモリを圧迫** | PDF エクスポーターが画像全体を RAM に保持します。 | ページをチャンク単位で処理するか、ストリーミング対応の PDF ライターを使用してください。 |

*Pro tip:* 大量バッチにする前に、まず小さなサンプル画像でテストしましょう。デバッグにかかる時間を大幅に削減できます。

## まとめ

これで **画像で OCR を実行**する方法、**PNG からテキストを抽出**する方法、**テキスト画像を認識**して下流タスクに活用する方法、**検索可能な PDF を生成**する方法、そして **PNG を PDF に変換**する方法がすべて分かりました。提供したスクリプトはコピー＆ペーストでそのまま動作する完全版で、オプションセクションを使えば出力を自分のワークフローに合わせて調整できます。

### 次は何をすべき？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}