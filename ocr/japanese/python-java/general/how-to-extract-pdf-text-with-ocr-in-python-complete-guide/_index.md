---
category: general
date: 2026-06-19
description: PythonでOCRを使用してPDFを抽出する方法 – PDFからテキストを抽出し、画像からテキストを認識し、OCRのPython例を含むステップバイステップチュートリアル。
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: ja
og_description: PythonでOCRを使用してPDFを抽出する方法。PDFからテキストを抽出し、画像から文字を認識し、完全なOCR Python例をご覧ください。
og_title: PythonでOCRを使ってPDFテキストを抽出する方法 – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: PythonでOCRを使ってPDFテキストを抽出する方法 – 完全ガイド
url: /ja/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを使用してPDFテキストを抽出する方法 – 完全ガイド

スキャン画像だけのPDFから**PDFを抽出する方法**を考えたことがありますか？ あなただけではありません。実際のプロジェクトでは、契約書、請求書、歴史的アーカイブなど、受け取ったPDFに選択可能なテキストがないことがよくあります。良いニュースは、数行のPythonコードで画像のみのページを検索可能で編集可能なテキストに変換できることです。

このチュートリアルでは、PDFを読み取り、最初のページを画像としてレンダリングし、OCRエンジンを使用して**PDFからテキストを抽出**する実用的な**OCR Python example**を順に解説します。最後まで読むと、**OCRでPDFを読む**方法、各ステップの重要性、マルチページ文書や異なる言語へのコードの適応方法が正確に分かります。

## 学べること

- 信頼できるOCRライブラリをPythonにインストールし設定する方法。  
- OCRに適した画像へPDFページを変換する方法。  
- **画像からテキストを認識**し、クリーンなUnicode文字列を取得する方法。  
- よくある落とし穴（低解像度PDF、回転ページ）と回避策。  
- スクリプトを拡張して複数ページやバッチ処理に対応させる方法。

**Prerequisites**: Python 3.8以上、pip、仮想環境の基本的な理解。OCRの事前経験は不要です—手順に従うだけです。

---

## ## PythonでOCRを使用してPDFテキストを抽出する方法

このH2ヘッダーは、検索エンジンが好む主要キーワードをちょうどそこに入れています。さっそくコードに入りましょう。

### Step 1 – 必要なパッケージをインストール

まず、OCRエンジンが必要です。以下の例では、Tesseract の薄いラッパーである人気の **ocr** パッケージを使用しています。別のバックエンドを好む場合でも、概念は同じです。

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** Linux では Tesseract バイナリも必要です: `sudo apt-get install tesseract-ocr`。macOS ユーザーは Homebrew で取得できます: `brew install tesseract`。

### Step 2 – OCRエンジンを初期化し言語を設定

エンジンを起動し、英字文字を対象にするよう指示します。`ocr.Language.English` を任意のサポート言語コードに置き換えることができます。

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Why this matters:** 言語を指定すると、エンジンが言語固有の辞書や文字モデルを適用できるため、精度が劇的に向上します。

### Step 3 – PDFページを画像として読み込む

OCR はラスタ画像で動作し、PDF オブジェクトでは動作しません。`ocr.Image.from_pdf` ヘルパーは選択したページをビットマップにレンダリングします。他のページを処理する場合は `page_number` を調整してください（0 ベースインデックス）。

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** PDF にベクターグラフィックが含まれている場合、鮮明なレンダリングが得られることがあります。低解像度スキャンの場合は DPI を上げてください: `ocr.Image.from_pdf(..., dpi=300)`。

### Step 4 – レンダリングされた画像からテキストを認識

ここが **ocr python example** の核心です。エンジンがビットマップを処理し、抽出された文字列を含むオブジェクトを返します。

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

`ocr_result.text` 属性にプレーンテキスト出力が格納され、可能な限り改行が保持されます。

### Step 5 – 抽出したテキストを表示または保存

最後に結果を出力します。実際のアプリケーションではファイルやデータベースに書き込むことが多いでしょう。

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

スクリプトを実行すると、次のような出力が表示されます:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

これが OCR を使用した **extract text from pdf** ワークフローの全体です。

---

## ## 画像からテキストを認識 – 精度調整

**画像からテキストを認識**（例: レシートの JPEG）のみが目的の場合、PDF 変換ステップをスキップできます:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips for better results:**

- **Pre‑process** 画像: グレースケールに変換し、しきい値処理やデスケューを行う。Pillow で簡単に実装可能です。  
- PDF レンダリング時に **DPI を上げる**: 高解像度ほど OCR エンジンに詳細が提供されます。  
- OCR エンジンのページ分割設定を有効にする: `ocr_engine.config = "--psm 6"`（均一ブロック用）。

---

## ## OCRでPDFを読む – 複数ページの処理

多くの契約書は数ページにわたります。各ページをループ処理するのは簡単です:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

この関数は **read PDF with OCR** を実行し、出力を連結して明確なページ区切りマーカーを挿入します。その後 `full_text` を検索インデックスに投入したり、`.txt` ファイルとして保存したりできます。

---

## ## よくある落とし穴と対策

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| 文字化け、`?` が多数 | 言語設定が間違っている、または言語データファイルが欠如している | 正しいTesseract言語パック（`tesseract-ocr-<lang>`）をインストールし、`ocr_engine.language` を設定する。 |
| 行が欠落または単語が切り捨てられる | DPIが低い（150未満） | PDFを300 DPI以上でレンダリングする（`dpi=300`）。 |
| テキストが回転または逆さま | スキャンページが正しくない向き | 認識前に `ocr.Image.deskew(page_image)` を使用する。 |
| 大きなPDFで処理が遅い | ページを単一スレッドで順次処理している | `concurrent.futures.ThreadPoolExecutor` で並列化する。 |

---

## ## OCR Python Example の拡張

- **Export to PDF/A**: 抽出後、`reportlab` や `pypdf2` を使ってテキストを検索可能な PDF に埋め込めます。  
- **Language detection**: OCR 出力に `langdetect` を使用し、`ocr_engine.language` を動的に切り替えます。  
- **Batch processing**: `os.listdir` でディレクトリを走査し、`extract_all_pages` をすべてのファイルに適用します。

---

## ## 期待される出力と検証

クリアな英語スキャンに対してスクリプトを実行すると、適切な句読点が付いたクリーンなテキストブロックが得られるはずです。検証手順:

1. 数行を元のスキャン画像と比較する。  
2. 簡単な単語数カウント (`len(ocr_result.text.split())`) を実行し、出力が空でないことを確認する。  
3. 必要に応じて `pyspellchecker` などのスペルチェッカーに結果を渡し、OCR エラーを検出する。

---

## Conclusion

従来のパースが失敗するケースで**PDFを抽出する方法**をカバーし、完全な **ocr python example** を実演し、**画像からテキストを認識** と **OCRでPDFを読む** を単一ページ・マルチページシナリオの両方で説明しました。上記のコードスニペットを使えば、スキャンされた PDF を検索可能で編集可能なテキストに変換でき、手動での再入力は不要です。

次のステップは？ 言語をスペイン語（`ocr.Language.Spanish`）に変更したり、画像前処理技術を試して精度を向上させたりしてください。ドキュメント管理システムを構築している場合は、抽出テキストを Elasticsearch にインデックス化して超高速検索を実現しましょう。

質問や変わった PDF に遭遇したらコメントを残してください。Happy coding!  

![PythonでOCRを使用してPDFを抽出する方法](image.png "PythonでOCRを使用してPDFを抽出する方法")


## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose OCRで画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDFテキストを認識 – Aspose.OCR for JavaによるOCR操作](/ocr/english/java/ocr-operations/)
- [Aspose.OCRを使用したC#での画像テキスト抽出（言語選択）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}