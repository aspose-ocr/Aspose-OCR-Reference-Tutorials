---
category: general
date: 2026-06-25
description: Pythonのaocrライブラリで画像からテキストを抽出 – バッチOCRを学び、認識モードを印刷用に設定し、AIポストプロセッサを追加。
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: ja
og_description: Pythonのaocrライブラリを使用して画像からテキストを抽出します。このチュートリアルでは、バッチOCR、印刷文字認識モード、そしてオプションのAIポストプロセッサを紹介します。
og_title: Pythonで画像からテキストを抽出する – 完全なaocrバッチガイド
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Pythonでaocr OCRバッチを使用して画像からテキストを抽出
url: /ja/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonでaocr OCRバッチを使用して画像からテキストを抽出する

画像から**テキストを抽出**したいけれど、細かい手順が多くて圧倒されていませんか？ あなただけではありません。スキャンしたフォームのデジタル化、レシートからのデータ抽出、検索可能なアーカイブの構築など、スケールで信頼できるOCR結果を得ることは、急な坂道を登るように感じられることがあります。

良いニュースは、**aocr ライブラリ**を使えば、ほんの数行のコードでフル**Python OCR バッチ**を立ち上げられることです。このガイドでは、OCR バッチの作成、フォルダー内のすべての対応画像の読み込み、適切な**recognition mode printed**の選択、そして精度向上のための**AI ポストプロセッサ**の添付方法を順を追って説明します。最後まで読めば、画像からテキストを抽出し、ファイルごとの取得文字数を表示する実行可能なスクリプトが手に入ります。

## 学べること

- `aocr` パッケージのインストールとインポート方法
- 数千ファイルを自動処理する `OcrBatch` の設定方法
- 印刷文書に最適な認識モードの選択方法
- (任意) ノイズの多い結果をクリーンアップする AI ポストプロセッサの組み込み方
- 各ファイルパスと抽出テキストの長さを表示する方法
- 未対応フォーマットや空白ページなどのエッジケースへの対処法

### 前提条件

- Python 3.8 以上がインストールされていること  
- Python スクリプトの基本的な知識（ループ、インポートなど）  
- スキャン画像が格納されたフォルダー (PNG, JPG, TIFF など) が用意されていること  

これらが揃っていれば、外部サービスは不要ですぐに始められます。

## Step 1: aocr ライブラリのインストール

まずは `aocr` パッケージを PyPI から取得します。標準ライブラリには含まれていないので、以下のコマンドでインストールしてください。

```bash
pip install aocr
```

> **プロのコツ:** `python -m venv .venv` で仮想環境を作成し、依存関係を分離しておくと安心です。  

インストールが完了したら、コアクラスをインポートできます。

```python
# core imports
import aocr
```

## Step 2: OCR バッチインスタンスの作成

`OcrBatch` はディレクトリを走査し、画像ファイルをすべて管理する仕事の中心です。画像を OCR エンジンに流し込むコンベアベルトと考えてください。

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

この時点ではバッチは空ですが、次のステップで画像を追加します。

## Step 3: フォルダー内のすべての対応画像を再帰的に追加

クライアントごとや月ごとにサブフォルダーがあるような階層構造を想定しています。`add_folder` メソッドがツリーをたどり、読み取り可能なすべての画像を自動で取り込みます。

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

`"YOUR_DIRECTORY/scanned_forms/"` を実際のパスに置き換えてください。この呼び出し後、`ocr_batch.file_paths` には絶対パスのリストが格納され、バッチは処理対象アイテム数を把握します。

## Step 4: 印刷テキスト用の認識モードを選択

`aocr` エンジンは複数のモード（handwritten, printed, mixed）をサポートしています。今回はクリアな印刷フォームを対象にするので、モードを設定します。この小さなフラグが、手書き文字用の重いヒューリスティックをスキップさせるため、精度を大幅に向上させます。

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **重要ポイント:** 印刷テキストはベースラインと文字形状が一定なので、OCR モデルはよりタイトな文字辞書を適用できます。モードを「auto」のままにすると、低解像度スキャンで余計なノイズが混入する可能性があります。

## Step 5: (任意) AI ポストプロセッサの添付

スキャンがぼやけている、コントラストが低い、特殊フォントが使われている場合は、AI ポストプロセッサで生の OCR 出力をクリーンアップできます。`set_ai_postprocessor` メソッドは `process(text: str) -> str` インターフェースを実装したオブジェクトを受け取ります。

以下は架空の `SimpleCleaner` クラスを使った最小例です。実際には HuggingFace のトランスフォーマーやカスタム言語モデル、ルールベースのスペルチェッカーなどを差し込めます。

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

このステップを省略すると、バッチは生の OCR 文字列をそのまま返します。

## Step 6: バッチ全体で OCR を実行し結果を収集

いよいよ本格的な処理です。`run` メソッドはすべてのファイルをループし、OCR エンジンを実行し、オプションの AI ポストプロセッサを通して、画像ごとに文字列のリストを返します。

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

メソッドは純粋な Python のリストを返すので、他のコレクションと同様に扱えます。CSV に書き出したり、データベースに保存したり自由に利用可能です。

## Step 7: 各ファイルパスと抽出テキストの長さを表示

簡易的なサニティチェックとして、各ファイルから抽出された文字数を出力します。ページが空白だったり OCR が失敗した場合は `0` が表示されます。

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

典型的な出力例:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

`0` が出たファイルはすぐに要チェック（破損している、画像でないなど）と判断できます。

## 共通エッジケースの対処

### 1. 未対応ファイルタイプ

`aocr` はデコードできないファイルを黙ってスキップします。PDF や BMP が混在している疑いがある場合は、事前にフィルタリングしましょう。

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. 大規模バッチとメモリ消費

高解像度スキャンを数千件処理するとメモリ使用量が急増します。チャンク単位で処理することで緩和できます。

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. 空白ページや低コントラストページ

文字数が 10 未満の場合は手動レビュー用にフラグを立てると便利です。

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## 完全動作サンプル

すべてをまとめたスクリプトです。コピーしてすぐに実行できます。`batch_ocr.py` という名前で保存してください。

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**期待される出力**（抜粋）:

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

実行コマンド:

```bash
python batch_ocr.py
```

正しく設定されていれば、すべての画像について抽出文字数が表示されます。

## よくある質問

**Q: PDF でも動作しますか？**  
A: 標準では対応していません。`aocr` はラスタ画像のみ扱えるので、事前に `pdf2image` などで PNG/TIFF に変換してください。

**Q: 認識モードを手書きに変更できますか？**  
A: もちろんです。`aocr.RecognitionMode.PRINTED` を `aocr.RecognitionMode.HANDWRITTEN` に置き換えるだけです。処理は遅くなりますが、手書きノートでの精度は向上します。

**Q: 多言語対応は可能ですか？**  
A: ライブラリには言語パックが同梱されています。目的の言語モジュールをインストール（例: フランス語は `pip install aocr-lang-fr`）し、実行前に `ocr_batch.language = "fr"` を設定してください。

## 次のステップと関連トピック

- **並列処理:** `concurrent.futures.ThreadPoolExecutor` でバッチ実行をラップし、複数 CPU コアを活用する  
- **結果の保存:** `ocr_results` を CSV や SQLite に書き出して downstream 分析に利用する  
- **クラウド AI との統合:** `SimpleCleaner` を HuggingFace のトランスフォーマーモデルに差し替えて最先端のスペル補正を実装する  
- **aocr のファインチューニング:** カスタムフォントセットがある場合は `aocr.Trainer` を使って印刷モードの精度を向上させる  

---

以上です。これで堅牢な OCR バッチ処理の基礎が身につきました。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}