---
category: general
date: 2026-03-18
description: PythonでAspose OCRを使用して画像からテキストを抽出し、スキャン画像のテキストを編集可能な文字列に変換する方法を学びましょう。ステップバイステップのコードが含まれています。
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: ja
og_description: PythonでAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、数行のコードでスキャン画像のテキストを変換する方法を示します。
og_title: Aspose OCR を使用した画像からのテキスト抽出 – Python ガイド
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCRで画像からテキストを抽出する – Pythonガイド
url: /ja/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト抽出 – Python ガイド

画像から **テキストを抽出** したいことはありませんか？でも、どこから始めればいいか分からない…という開発者は多いです。スキャンした PDF、ノイズの多いスクリーンショット、写真で撮ったレシートを検索可能で編集可能な文字列に変換するのは、常に頭を悩ませる作業です。

朗報です！Aspose OCR for Python を使えば、IDE を離れることなく **スキャン画像のテキストを一括変換** できます。このチュートリアルでは、完全に実行可能なサンプルを通して、手順ごとの意味と注意点を詳しく解説します。

## 学べること

- Python 環境に Aspose OCR ライブラリをセットアップする方法  
- 画像ファイル（PNG、JPG、TIFF など）のリストを作成する方法  
- 1 回のメソッド呼び出しでバッチ OCR を実行する方法  
- 各ファイルの抽出テキストを取得・表示する方法  
- 未対応フォーマットや大容量ファイルのメモリ使用量といった一般的な落とし穴への対処法  

このチュートリアルを終える頃には、**画像からテキストを抽出** できる再利用可能なスクリプトが手に入り、データ入力の自動化、文書のインデックス作成、下流の NLP パイプラインへのデータ供給などに活用できます。

---

![画像からテキストを抽出する例](/images/ocr-extract-text.png "画像からテキストを抽出")

*画像の代替テキスト: “Aspose OCR を使用した Python での画像からテキスト抽出”*

## 前提条件

- Python 3.8 以上（コードは f‑strings を使用）  
- 有効な Aspose OCR for Python ライセンスまたは無料トライアルキー  
- ローカルに保存された画像（PNG、JPG、TIFF など、任意の組み合わせ）  

既に仮想環境がある場合はそのままで構いません。まだの場合は、以下で作成してください。

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

これで SDK のインストール準備が整いました。

## 手順 1: Aspose OCR SDK をインストール

Aspose は OCR エンジンを PyPI 経由で配布しているため、`pip` コマンド一つで完了します。

```bash
pip install aspose-ocr
```

> **プロのヒント:** 後々の予期せぬ破壊的変更を防ぐため、バージョンを固定（例: `aspose-ocr==22.12`）しておくと安心です。

## 手順 2: OCR エンジンのクラスをインポート

操作の中心になるクラスは `OcrEngine` です。スクリプトの冒頭でインポートしましょう。

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *この重要性:* 必要なものだけをインポートすることで、起動時間を短縮できます。特に後で大規模アプリに組み込む場合に効果的です。

## 手順 3: 処理対象の画像ファイルを定義

スキャンしたいすべての画像へのフルパスを Python のリストに格納します。`YOUR_DIRECTORY` は実際のフォルダパスに置き換えてください。

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **エッジケース:** ファイルが数百に上る場合は、`glob.glob('*.png')` などでプログラム的にリストを生成し、手動編集を避けましょう。

## 手順 4: すべての画像に対して OCR を一括実行

Aspose OCR には便利な `processMultiple` メソッドがあり、各入力ファイルに対する `OcrResult` オブジェクトのリストを返します。

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *なぜバッチ処理か？* 画像を 1 枚ずつ送ると、エンジンの初期化やネイティブライブラリのロードといった余計なオーバーヘッドが発生します。バッチ呼び出しにより CPU の負荷が抑えられ、全体の処理速度が向上します。

### エラーを優雅に処理する

画像が読めない（破損ファイル、未対応フォーマット）場合、`processMultiple` は例外をスローします。スクリプトが停止しないよう、`try/except` でラップしましょう。

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## 手順 5: 各ファイルの抽出テキストを出力

結果を走査し、`OcrResult` と元のファイル名を対応付けます。`getText()` メソッドが認識文字列を返します。

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### 期待される出力

3 枚のシンプルなスクリーンショットでスクリプトを実行すると、次のような出力になることがあります。

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

画像に認識可能な文字が全くない場合は空文字列が出力されます。エラーにはなりませんので、手動レビューが必要かどうかを判定できます。

## ボーナス: OCR 精度の微調整

Aspose OCR では、以下のようなオプション設定で精度を向上させることができます。

| 設定 | 機能概要 | 使用シーン |
|------|----------|------------|
| `ocr_engine.setLanguage('eng')` | 英語モデルを強制（誤検出を減少） | 主に英語文書 |
| `ocr_engine.setResolution(300)` | 低 DPI スキャンの精度向上 | 200 dpi 未満のスキャン |
| `ocr_engine.setPageSegMode('single_block')` | 画像全体を 1 ブロックのテキストとして扱う | シンプルなレシートや ID カード |

`ocr_engine` を生成した直後に以下を追加してください。

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## よくある落とし穴と回避策

1. **大容量 TIFF スタック** – マルチページ TIFF を一括で読み込むと、RAM が数ギガバイトに達することがあります。`processMultiple` に渡す前に、単ページ画像に分割しましょう。  
2. **非ラテン文字** – Cyrillic、Arabic、Chinese などの文字が含まれる画像から **テキストを抽出** したい場合は、言語コードをそれぞれ `'rus'`、`'ara'`、`'chi_sim'` に変更してください。  
3. **ファイルパスにスペースが含まれる** – Windows のスペース付きパスは `FileNotFoundError` の原因になることがあります。各パスを raw 文字列（例: `r"C:\My Folder\image.png"`）で囲むか、`os.path.abspath` を利用しましょう。  

事前にこれらに対処しておくと、実行時の暗号化されたエラーメッセージに悩まされることがなくなります。

---

## 完全動作サンプル

以下は `batch_ocr.py` というファイル名で保存できる、完全版スクリプトです。先ほど説明したベストプラクティスがすべて組み込まれています。

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

保存後、仮想環境を有効化して次のコマンドを実行してください。

```bash
python batch_ocr.py
```

コンソールに抽出された文字列が表示されます。これをデータベースに保存したり、自然言語モデルに渡したりするのは自由です。

---

## 結論

本ガイドでは、Aspose OCR for Python を用いて **画像からテキストを抽出** する方法を、インストールからバッチ処理、エラーハンドリングまで網羅的に解説しました。スクリプトはコンパクトで実用的、かつ拡張しやすい構造になっているため、スキャン画像のテキストを CSV に変換したり、検索インデックスに流し込んだり、単純にデータ入力を自動化したりと、さまざまなユースケースに応用できます。

次のステップとしては、OCR パイプラインを PDF マージツールと組み合わせて検索可能な PDF を生成したり、クラウドストレージのトリガーに結び付けてアップロードされたスキャンを即座に処理したりしてみてください。可能性は無限大です。ぜひこの土台を活用して、さらに高度なソリューションを構築してください。

質問や改善アイデアがあれば、下のコメント欄にどうぞ。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}