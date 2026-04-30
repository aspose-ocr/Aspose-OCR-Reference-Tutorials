---
category: general
date: 2026-04-29
description: Aspose OCR を使用して Python で PDF からテキストを抽出します。バッチ OCR PDF 処理を学び、スキャンされた
  PDF のテキストを変換し、信頼度の低いページを処理します。
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: ja
og_description: Aspose OCR を使用して Python で PDF からテキストを抽出します。このガイドでは、バッチ OCR PDF 処理、スキャンされた
  PDF のテキスト変換、低信頼度結果の処理方法を示します。
og_title: PDFからテキストを抽出 – PythonでPDFをOCR
tags:
- OCR
- Python
- PDF processing
title: PDFからテキストを抽出 – PythonでPDFをOCR
url: /ja/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFからテキストを抽出 – PythonでOCR PDF

PDFから**テキストを抽出**したいが、ファイルが単なるスキャン画像だったことはありませんか？ あなた一人ではありません—多くの開発者がPDFを検索可能なデータに変換しようとしてこの壁にぶつかります。良いニュースは、Aspose OCR for Python を使えば、数行のコードでスキャンしたPDFのテキストを変換でき、さらに**バッチOCR PDF処理**を数十ファイルに対して実行できることです。

このチュートリアルでは、ライブラリのセットアップ、単一PDFでのOCR実行、バッチへのスケーリング、そして低信頼度ページの処理（手動レビューが必要なときが分かるように）という全体のワークフローを順に解説します。最後まで読むと、任意のスキャンPDFからテキストを抽出できる実行可能なスクリプトが手に入り、各ステップの背景も理解できるようになります。

## 必要なもの

Before we dive in, make sure you have:

- Python 3.8 以上（コードはf文字列を使用しているため、3.6以降でも動作しますが、3.8以上を推奨します）
- Aspose OCR for Python のライセンスまたは無料トライアルキー（Aspose のウェブサイトから取得できます）
- 処理したいスキャンPDFが1つ以上入っているフォルダー
- 生成される *.txt* レポート用の適度なディスク容量

以上です—重い外部依存関係は不要で、OpenCVの操作も必要ありません。Aspose OCR エンジンが重い処理をすべて担ってくれます。

## 環境設定

まず、PyPI から Aspose OCR パッケージをインストールします。

```bash
pip install aspose-ocr
```

ライセンスファイル（`Aspose.OCR.lic`）を持っている場合は、プロジェクトのルートに配置し、以下のように有効化します。

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **プロのコツ:** ライセンスファイルはバージョン管理に含めないでください。`.gitignore` に追加して、誤って公開されるのを防ぎましょう。

## 単一PDFでのOCR実行

それでは、単一のスキャンPDFからテキストを抽出しましょう。主な手順は次の通りです。

1. `OcrEngine` のインスタンスを作成します。
2. 対象のPDFファイルを指定します。
3. 各ページの `OcrResult` を取得します。
4. プレーンテキストの出力をディスクに書き込みます。
5. エンジンを破棄してネイティブリソースを解放します。

以下が完全な実行可能スクリプトです。

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**実行結果の例:** 各ページでスクリプトは `Page 1: confidence 97.45%` のように出力します。信頼度が80 %未満のページがあると、警告が表示され、OCR が文字を見逃した可能性があることが分かります。

### なぜこれが機能するのか

- **`OcrEngine`** はネイティブな Aspose OCR ライブラリへのゲートウェイで、画像前処理から文字認識まで全てを処理します。
- **`extract_from_pdf`** は各PDFページを自動的にラスタライズするため、PDF を画像に変換する手間が不要です。
- **信頼度スコア** を利用すれば品質チェックを自動化できます。正確さが重要な法務や医療文書の処理に特に有用です。

## PythonでバッチOCR PDF処理

実務では複数のファイルを扱うことがほとんどです。単一ファイル用スクリプトを拡張し、ディレクトリ内を走査して各PDFを処理し、結果を対応するサブフォルダーに保存する **バッチOCR PDF処理** パイプラインを作りましょう。

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### これが役立つ理由

- **スケーラビリティ:** 関数はフォルダーを一度走査し、各PDFごとに専用の出力サブフォルダーを作成します。多数の文書がある場合でも整理された状態を保てます。
- **再利用性:** `ocr_pdf_file` は純粋関数なので、他のスクリプト（例: Webサービス）から呼び出すことができます。
- **エラーハンドリング:** 入力フォルダーが空の場合、スクリプトは親切なメッセージを表示し、無音の失敗を防ぎます。

## スキャンPDFテキストの変換 – エッジケースの処理

上記のコードは**ほとんどのPDF**で動作しますが、いくつかの特殊ケースに遭遇することがあります。

| 状況 | 発生理由 | 対策 |
|-----------|----------------|-----------------|
| **暗号化PDF** | PDFがパスワードで保護されています。 | `extract_from_pdf(pdf_path, password="yourPwd")` にパスワードを渡してください。 |
| **多言語文書** | Aspose OCR のデフォルト言語は英語です。 | スペイン語の場合は `ocr_engine.language = "spa"` と設定するか、混在言語の場合はリストで指定してください。 |
| **非常に大きなPDF（>500ページ）** | 各ページがRAMに読み込まれるため、メモリ使用量が急増します。 | `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` などでPDFを分割して処理し、ループさせます。 |
| **スキャン品質が低い** | DPIが低い、またはノイズが多いと信頼度が低下します。 | `engine.image_preprocessing = True` で前処理を行うか、`engine.dpi = 300` でDPIを上げてください。 |

> **注意:** 画像前処理を有効にすると CPU 時間が顕著に増加します。夜間バッチを実行する場合は、十分な時間を確保するか、別のワーカーを立ち上げてください。

## 出力の検証

スクリプトが完了すると、以下のようなフォルダー構造が作成されます。

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

任意の `.txt` ファイルを開くと、元のスキャン内容を反映したクリーンな UTF‑8 エンコードのテキストが表示されます。文字化けが見られる場合は、PDF の言語設定を再確認し、マシンに適切なフォントパックがインストールされているか確認してください。

## リソースのクリーンアップ

Aspose OCR はネイティブ DLL に依存しているため、完了後に `engine.dispose()` を呼び出すことが重要です。この手順を忘れると、特に長時間実行するバッチジョブでメモリリークが発生する可能性があります。

```python
# Always the last line of your script
engine.dispose()
```

## 完全なエンドツーエンド例

すべてをまとめると、以下は単一の

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}