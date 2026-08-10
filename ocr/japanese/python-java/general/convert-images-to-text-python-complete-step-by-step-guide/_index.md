---
category: general
date: 2026-05-31
description: バルク画像からテキストへの変換スクリプトを使って、Pythonで画像をテキストに変換する方法を学びましょう。Aspose.OCRを利用すれば、スキャンした画像から数分でテキストを認識できます。
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: ja
og_description: 画像を即座にPythonでテキストに変換します。このガイドでは、画像の一括テキスト変換と、Aspose.OCR を使用したスキャン画像からのテキスト認識方法を紹介します。
og_title: 画像をテキストに変換する Python – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: 画像をテキストに変換する Python – 完全ステップバイステップガイド
url: /ja/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像をテキストに変換する Python – 完全ステップバイステップガイド

何十ものライブラリを探さずに **convert images to text python** を行う方法を考えたことはありますか？ あなただけではありません。古いレシートをデジタル化したり、スキャンした請求書からデータを抽出したり、PDF の検索可能なアーカイブを構築したりする場合、画像をプレーンテキストファイルに変換する作業は多くの開発者にとって日常的な課題です。

このチュートリアルでは、スキャン画像からテキストを認識し、各結果を個別の `.txt` ファイルとして保存し、Python の数行だけで実行できる **bulk image to text conversion** パイプラインを解説します。 obscure APIs を探す必要はありません—Aspose.OCR が重い処理を担い、設定方法を詳しく示します。

## 学べること

- Aspose.OCR for Python パッケージのインストールと設定方法。  
- `BatchOcrEngine` を使用して **convert images to text python** を実行するための正確なコード。  
- サポートされていない形式や破損したファイルなど、一般的な落とし穴への対処法のヒント。  
- **recognize text from scanned images** ステップが実際に成功したかを検証する方法。  

このガイドの最後までに、数千枚の画像を一括で処理できる実行可能なスクリプトが手に入り、あらゆるバッチ処理シナリオに最適です。

## 前提条件

- マシンに Python 3.8+ がインストールされていること。  
- テキストに変換したい画像ファイル（PNG、JPEG、TIFF など）のフォルダー。  
- 有効な Aspose Cloud アカウントまたは無料トライアルライセンス（テストには無料プランで十分）。  

これらが揃ったら、さっそく始めましょう。

---

## ステップ 1 – Python 環境のセットアップ

OCR コードを書く前に、クリーンな仮想環境内で作業していることを確認してください。これにより依存関係が分離され、バージョンの衝突を防げます。

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **Pro tip:** プロジェクトディレクトリを整理整頓しましょう—`ocr_project` というサブフォルダーを作成し、スクリプトをそこに置きます。これにより後でパス処理が楽になります。

## ステップ 2 – Aspose.OCR for Python のインストール

Aspose.OCR は商用ライブラリですが、PyPI から取得できる無料の NuGet 形式の wheel が同梱されています。アクティブな仮想環境内で以下のコマンドを実行してください：

```bash
pip install aspose-ocr
```

権限エラーが出た場合は `--user` フラグを付けるか、`sudo`（Linux/macOS のみ）でコマンドを実行してください。インストール後は次のような表示が出ます：

```
Successfully installed aspose-ocr-23.9.0
```

> **Why Aspose?** 多くのオープンソース OCR ツールとは異なり、Aspose.OCR は **bulk image to text conversion** を標準でサポートし、追加設定なしで幅広い画像形式を処理します。また、`BatchOcrEngine` クラスを提供しており、“convert images to text python” タスクをワンラインで実行できます。

## ステップ 3 – Batch OCR で画像をテキストに変換する Python

それではチュートリアルの核心です。以下は完全に実行可能なスクリプトで、次のことを行います：

1. OCR エンジンのクラスをインポートします。  
2. `BatchOcrEngine` のインスタンスを作成します。  
3. エンジンに画像の入力フォルダーを指定します。  
4. 抽出されたテキストファイルを出力フォルダーに書き込むよう指示します。  
5. `recognize()` メソッドを呼び出し、**recognize text from scanned images** を1つずつ実行します。  

以下の内容をプロジェクトフォルダー内に `batch_ocr.py` として保存してください：

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### 動作概要

- **`BatchOcrEngine`** は通常の `OcrEngine` をラップし、フォルダー単位のオーケストレーションを追加します。大量に **convert images to text python** を行いたいときに最適です。  
- `input_folder` プロパティはエンジンにソース画像の場所を指示します。ディレクトリを自動的にスキャンし、サポートされているすべてのファイルタイプをキューに入れます。  
- `output_folder` プロパティは各 `.txt` ファイルの保存先を決定します。エンジンは元のファイル名をそのまま使用するため、`receipt1.png` は `receipt1.txt` になります。  
- `recognize()` を呼び出すと、各画像を読み込み OCR を実行し結果を書き込む内部ループが開始されます。すべてのファイルが処理されるまでメソッドはブロックするため、後続の処理（例：出力フォルダーを zip にする）を簡単に連結できます。  

#### 期待される出力

スクリプトを実行すると：

```bash
python batch_ocr.py
```

次のように表示されます：

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

`output_texts` フォルダー内に、各画像に対応するプレーンテキストファイルが作成されます。テキストエディタで開くと、元の印刷テキストにかなり近い生の OCR 結果が確認できます。

## ステップ 4 – 結果の検証とエラー処理

最高の OCR エンジンでも、低解像度のスキャンや大きく歪んだページでは失敗することがあります。出力を簡易的にチェックし、失敗をログに記録する簡単な方法をご紹介します。

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

> **Why add this?**  
- エンジンが空文字列を静かに出力したケース（読めない画像でよく発生）を捕捉します。  
- 問題のあるファイルのリストを取得できるため、手動で確認したり、`OcrEngine.preprocess` オプションを変更して再実行できます。  

### エッジケースと調整

| Situation | Suggested Fix |
|-----------|----------------|
| Images are rotated 90° | Set `batch_engine.ocr_engine.rotation_correction = True`. |
| Mixed languages (English + French) | Use `batch_engine.ocr_engine.language = "eng+fra"` before `recognize()`. |
| Huge PDFs converted to images first | Split PDFs into single‑page images, then feed the folder to the batch engine. |
| Memory errors on very large batches | Process smaller sub‑folders sequentially, or increase `batch_engine.max_memory_usage`. |

## ステップ 5 – ワークフロー全体の自動化（オプション）

この変換を毎晩実行したい場合は、スクリプトをシンプルなシェルまたは Windows バッチファイルでラップし、`cron`（Linux/macOS）またはタスクスケジューラ（Windows）でスケジュールします。Unix 系システム向けの最小限の `run_ocr.sh` は以下の通りです：

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

実行可能にして（`chmod +x run_ocr.sh`）cron エントリを追加します：

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

これにより毎日午前 2 時に変換が実行され、出力は後で確認できるようにログに残ります。

---

## 結論

Aspose.OCR の `BatchOcrEngine` を使用して **convert images to text python** を行う、実証済みの本番環境対応手法が手に入りました。スクリプトは **bulk image to text conversion** を処理し、各結果を個別ファイルに優雅に書き込み、**recognize text from scanned images** が正しく行われたことを検証する手順も含んでいます。

ここからは：

- OCR 設定（言語パック、デスキュー、ノイズ除去）を試す。  
- 生成されたテキストを Elasticsearch などの検索インデックスに流し込み、即時全文検索を実現。  
- このパイプラインを PDF 変換ツールと組み合わせ、スキャン PDF を一括処理。  

質問や特定のファイルタイプで問題が発生した場合は、下のコメントで教えてください。一緒にトラブルシュートしましょう。コーディングを楽しんで、OCR が高速かつエラーなしで動作しますように！

## 次に学ぶべきこと

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}