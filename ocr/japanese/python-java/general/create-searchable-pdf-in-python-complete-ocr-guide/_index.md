---
category: general
date: 2026-06-22
description: OCR を使用して Python で検索可能な PDF を作成 – 画像を PDF に変換し、テキストを認識し、ワークフローを自動化する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: ja
og_description: OCR を使用して Python で検索可能な PDF を作成します。画像を PDF に変換し、テキストを認識し、ドキュメント処理を自動化するステップバイステップのチュートリアルをご覧ください。
og_title: Pythonで検索可能なPDFを作成する – 完全OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Pythonで検索可能なPDFを作成 – 完全OCRガイド
url: /ja/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで検索可能なPDFを作成 – 完全OCRガイド

スキャンした契約書から **検索可能なPDF** を作成したいと思ったことはありませんか？でもどこから始めればいいか分からない…という方は多いです。ビットマップ画像をテキスト検索可能なドキュメントに変換しようとしたときに、最初に壁にぶつかる開発者は多数います。良いニュースは、ほんの小さなPythonスクリプトを使えば **画像をPDFに変換** でき、OCRエンジンがすべての単語を認識し、完全に検索可能なファイルを作成できるということです。

このチュートリアルでは、適切なライブラリのインストールからマルチページ文書といったエッジケースの処理まで、全工程を順に解説します。最後まで読むと **ocr image to pdf**、**recognize text pdf** ができるようになり、ワークフローを大規模な自動化パイプラインに組み込むことができます。

## 必要なもの

本題に入る前に、以下がマシンに揃っていることを確認してください。

| 要件 | 重要な理由 |
|------|------------|
| Python 3.8 以降 | モダンな構文とより良い型ヒントが利用可能 |
| `ocr` Python package (or any compatible OCR SDK) | `OcrEngine`、`ImageStream`、PDF出力を提供 |
| A scanned image (JPEG, PNG, or TIFF) | 変換対象となるソース画像 |
| Write access to a folder for the output PDF | 生成されたファイルを保存できるようにするため |

まだSDKをインストールしていない場合は、以下を実行してください：

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **プロのコツ:** 仮想環境（`python -m venv .venv`）を使用して依存関係を整理しましょう。

## ワークフローの概要

1. **OCRエンジンインスタンスを作成** – 認識の中枢です。  
2. **画像をロード** して処理対象にします。  
3. **エンジンを設定** して、プレーンテキストではなく検索可能なPDFを出力させます。  
4. **メモリ内ストリームを準備** して、PDFバイト列を保持します。  
5. **認識を実行** – エンジンが画像を読み取り、テキストを抽出し、PDFを書き出します。  
6. **PDFをディスクに保存** して、任意のビューアで開けるようにします。

これがコード6行で完結する全体像です。それぞれのステップを詳しく見ていきましょう。

---

## 検索可能なPDFを作成 – ステップバイステップ Python OCR チュートリアル

### ステップ 1: OCRエンジンの初期化

最初に行うのは `OcrEngine` オブジェクトを生成することです。画像を読み取る準備ができたスキャナをオンにするイメージです。

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **なぜ重要か:** エンジンをインスタンス化すると内部バッファが確保され、言語データがロードされます。このステップを省略すると、後で画像を設定しようとした際に `NoneType` エラーが発生します。

### ステップ 2: 変換したい画像をロード

次に、エンジンに画像ストリームを渡します。`ImageStream.from_file` ヘルパーはファイルを読み込み、OCRエンジンが理解できる形式にラップします。

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **エッジケース:** ソースがマルチページTIFFの場合は、代わりに `ocr.MultiPageImageStream.from_file` を使用してください。エンジンは各ページを自動的に別々のPDFページとして扱います。

### ステップ 3: エンジンに検索可能なPDFを出力させる

デフォルトでは多くのOCR SDKはプレーンテキストを出力します。出力形式をPDFに切り替えることで、視覚的な画像と検索可能なテキストの両方を持つファイルが生成されます。

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **内部で何が起きているか:** エンジンはビットマップの背後に見えないテキストレイヤーを埋め込むため、ネイティブPDFと同様に単語検索が可能になります。

### ステップ 4: PDFデータ用のメモリ内ストリームを準備

ディスクに直接書き込む代わりに、`MemoryStream` にPDFを捕捉します。これによりI/Oが高速になり、必要に応じてバイト列を別の場所（例: S3へのアップロード）へパイプできます。

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### ステップ 5: 認識を実行し、PDFを書き出す

いよいよ本格的な処理が行われます。`recognize` 呼び出しは画像を読み取り、OCRを実行し、検索可能なPDFを `pdf_stream` にストリームします。

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **一般的な落とし穴:** `engine.recognize` の呼び出しを忘れると `pdf_stream` が空になり、保存しようとすると `ValueError` が発生します。データが生成されたか確認したい場合は必ず `pdf_stream.length` をチェックしてください。

### ステップ 6: 生成したPDFをファイルに保存

最後に、メモリストリームからバイト列をディスクに書き出します。生成されたファイルはAdobe Reader、Preview、または全文検索が可能な任意のPDFビューアで開くことができます。

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **期待される結果:** PDFを開き、`Ctrl+F` を押して、元のスキャンに含まれる単語を入力すると、ビューアが即座にハイライトします。これが **検索可能なPDF** の特徴です。

---

## 画像をPDFに変換 – ベストな結果のための設定調整

OCRなしで単に **画像をPDFに変換** することが目的であれば、ステップ 3 を省略し、出力形式を `ocr.OutputFormat.IMAGE_PDF` に設定できます。エンジンはビットマップを隠しテキストレイヤーなしでPDFページとして埋め込みます。

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

検索可能性が不要で、視覚的に忠実なコピーが必要な場合（例: OCRが不要なアーカイブ目的）にこのモードを使用してください。

---

## テキストPDFを認識 – 言語パックとDPI制御の追加

堅牢な **テキストPDF認識** を実現するために、以下のオプション調整を検討してください：

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **なぜDPIを調整するか:** 高解像度にするとOCRエンジンが解析できるピクセル数が増え、低品質なスキャンでの誤認識が減少します。

---

## Python OCR PDF – 大規模パイプラインへの統合

数行で **python ocr pdf** ができるようになったので、このロジックをFlask APIに組み込むことを想像してみてください：

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

この小さなエンドポイントにより、クライアントは画像をPOSTし、即座に **検索可能なPDF** を受け取れます。SaaSの文書処理サービスに最適です。

---

## **ocr image to pdf** 時の一般的な落とし穴

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| PDFページが空白 | 画像がロードされていない（`engine.set_image` が誤ったパスで呼び出された） | パスを確認し、`os.path.abspath` を使用してください |
| 検索可能なテキストがない | 出力形式が依然として `IMAGE_PDF` に設定されている | `set_output_format(ocr.OutputFormat.PDF)` を明示的に呼び出す |
| 文字化け | 誤った言語パックが使用されている | `settings.set_language("eng")` で正しい言語をロードする |
| 大きなファイルで処理が遅い | 高解像度画像でデフォルトDPI（72）を使用している | DPIを300に上げるか、ページを個別にバッチ処理する |

---

## 完全に実行可能な例（コピー＆ペースト可能）

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

スクリプトを実行し、生成されたPDFを開いて、元のスキャンに含まれることが分かっている単語で検索してみてください。すべてがうまくいったなら、Pythonで **create searchable pdf** をマスターしたことになります。

---

## 結論

PythonのOCRライブラリを使用して **検索可能なPDF** を作成するために必要なすべての手順、すなわちエンジンの初期化、画像のロード、PDF出力の設定、結果のストリーミング、そして最終的なディスクへの保存を網羅しました。また、**画像をPDFに変換** する方法や、** 

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [PDFテキストの認識 – Aspose.OCR for JavaでのOCR操作](/ocr/english/java/ocr-operations/)
- [.NETでPDFをOCRする方法 – Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [画像をPDFに変換 C# – マルチページOCR結果を保存](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}