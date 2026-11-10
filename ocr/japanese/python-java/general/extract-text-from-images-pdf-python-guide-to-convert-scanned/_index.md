---
category: general
date: 2026-06-06
description: Python OCR を使用して画像 PDF からテキストを抽出します。非同期バッチ認識でスキャンした文書を迅速にテキストに変換する方法を学びましょう。
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: ja
og_description: Pythonで画像PDFからテキストを抽出する。ステップバイステップのガイドで、非同期OCRを使用してスキャンした文書をテキストに変換する方法を示します。
og_title: 画像PDFからテキストを抽出 – Python OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 画像PDFからテキストを抽出 – スキャンした文書をテキストに変換するPythonガイド
url: /ja/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像PDFからテキスト抽出 – スキャンした文書をテキストに変換するPythonガイド

何度も **画像PDFからテキストを抽出** したくて、何時間も手入力するのに疲れたことはありませんか？このガイドでは、シンプルな非同期OCRワークフローを使って **スキャンした文書をテキストに変換** する方法をPythonで紹介します。  

スキャンしたPDFが山積みで「もっと速くできないか？」と思ったことがあるなら、ここがその答えです。コードを一行ずつ解説し、各部分がなぜ重要かを説明し、遭遇しうるいくつかのエッジケースも取り上げます。

## 学べること

- OCRエンジンを起動し、認識言語を設定する方法。  
- PNGとPDFを混在させたリストをバッチ認識器に渡す仕組み。  
- OCRジョブを非同期で実行し、アプリの応答性を保つ方法。  
- 結果を取得し、元ファイルと組み合わせて、きれいに出力する方法。  

**前提条件**: Python 3.8以上、`asyncio` または `concurrent.futures` の基本的な理解、そして例で使用しているような `OcrEngine` クラスを提供するOCRライブラリ（例: Aspose.OCR、Tesseractラッパー、またはカスタムラッパー）。重いセットアップは不要で、ライブラリをインストールすればすぐに使用できます。

![画像PDFからテキスト抽出](https://example.com/placeholder.png "OCR出力のスクリーンショット – 画像PDFからテキスト抽出")

## 画像PDFからテキスト抽出 – OCRエンジンの設定

最初に必要なのは、文書の言語に合わせて設定されたOCRエンジンのインスタンスです。ここではフランス語を使用しますが、任意のサポートされている言語に変更可能です。

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**なぜ重要か**: 言語を事前に設定することで精度が大幅に向上します。エンジンは言語固有の辞書と文字モデルを使用するため、誤った言語を指定すると文字化けした出力になることがよくあります。

## ファイルリストの準備 – 画像とPDFを同時に扱う

バッチ認識器はラスタ画像（`.png`、`.jpg`）とPDFコンテナの両方を処理できます。ファイルパスの普通のPythonリストを渡すだけです。

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**ヒント**: リストはフラットに保ちます。エンジンは内部で各PDFページを画像に展開してから認識します。ファイルが数千件ある場合は、メモリ使用量の急増を防ぐためにリストを小さなバッチに分割すると良いでしょう。

## 非同期バッチ認識の開始

メインスレッドをブロックせずに、OCRジョブをバックグラウンドで起動します。このメソッドは最終的に `OcrResult` オブジェクトのリストを保持する `Future` を返します。

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**動作概要**: エンジンは内部でスレッドプール（または実装に応じた非同期タスク）を生成します。これにより、重い処理が別スレッドで行われている間に、UIの更新やファイルの取得、進捗のロギングなど他の作業を続けられます。

## OCR実行中に有用な処理を行う

一般的なミスは、何もしないでFutureを頻繁にポーリングすることです。その代わりに、無関係な作業を実行できます。デモとして、ステータス行を出力するだけにします。

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Future完了後に結果を取得する

OCR出力を取得する準備ができたら、`concurrent.futures` の `as_completed` を使用します。このパターンは、1つでも複数でも機能します。

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**出力例**: 各ファイルパスの後に抽出されたプレーンテキストが表示されます。PDFの場合、`result.text` には全ページのテキストが結合された形で含まれます。

### 期待される出力（例）

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

文字が抜けている場合は、設定した言語が文書の言語と一致しているか再確認し、エンジンに渡す前に画像の前処理（傾き補正、コントラスト向上）を検討してください。

## エッジケースと一般的な落とし穴の対処

| 状況 | 対策 |
|-----------|------------|
| **混在言語** | まず言語検出を行い、言語ごとに別々のエンジンをインスタンス化します。 |
| **巨大PDF（> 100 MB）** | PDFをディスク上でページ単位に分割（例: `PyPDF2` 使用）し、個別エントリとして渡します。 |
| **非ラテン文字** | OCRライブラリに必要な言語パックが含まれていることを確認します。ライブラリによっては追加データファイルのダウンロードが必要です。 |
| **パフォーマンスボトルネック** | スレッドプールサイズを増やす（`engine.set_thread_pool_size(8)`）か、利用可能ならGPUアクセラレートバックエンドに切り替えます。 |
| **低解像度画像でテキスト欠損** | OpenCVで前処理（`cv2.resize`、`cv2.threshold`、`cv2.medianBlur`）を行い、可読性を向上させます。 |

## 完全動作例（コピー＆ペースト可能）

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

`extract_text_async.py` として保存し、`YOUR_DIRECTORY` をファイルがあるパスに置き換え、OCRパッケージをインストール（`pip install your-ocr-lib`）して、`python extract_text_async.py` を実行します。先ほど示したコンソール出力が表示されるはずです。

## 次のステップ – 基本抽出を超えて

- **ポストプロセッシング**: 余分な空白を除去し、Unicode正規化（`unicodedata.normalize`）やスペルチェッカーを実行してOCRノイズを除去します。  
- **構造化出力**: 結果をCSV、JSON、またはデータベースに直接エクスポートし、下流検索に利用します。  
- **並列バッチ**: 数百ファイルある場合は複数のFutureを立ち上げ、キューを使ってCPUを稼働させつつメモリ過負荷を防ぎます。  
- **ウェブフレームワークとの統合**: このスクリプトをFlaskやFastAPIのエンドポイントに組み込み、オンデマンドOCRサービスを提供します。

---

### TL;DR

これで、OCRを非同期で実行する最小限のPythonスクリプトを使って **画像PDFからテキストを抽出** し、プログラムを応答性のまま **スキャンした文書をテキストに変換** できるようになりました。言語設定やバッチサイズ、前処理のテクニックを試して、文字精度を最大限に引き出してください。

手書きノートのOCRやクラウドベースのサービスなど、独自の工夫があればぜひ共有してください。コメントを残して、楽しいコーディングを！

## 次に学ぶべきこと

以下のチュートリアルは本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [フォルダー上での OCR 操作を使用して画像からテキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR を使用した画像からのテキスト抽出 – 許可文字](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}