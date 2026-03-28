---
category: general
date: 2026-03-28
description: PythonでAspose OCRを使用してTIFFファイルからテキストを抽出します。TIFFを迅速かつ確実にテキストへ変換する方法を学びましょう。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: ja
og_description: PythonでAspose OCRを使用してTIFFファイルからテキストを抽出します。このガイドでは、TIFFをテキストに変換する手順をステップバイステップで示します。
og_title: TIFFからテキストを抽出 – 完全なPythonガイド
tags:
- OCR
- Python
- Aspose
title: TIFFからテキストを抽出する – 完全なPythonガイド
url: /ja/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF からテキストを抽出する – 完全な Python ガイド

Python プロジェクトで **TIFF からテキストを抽出** する必要がありますか？このガイドでは、Aspose OCR ライブラリを使用して **TIFF をテキストに変換** する方法を示し、初心者でも実行できるように解説します。  

マルチページ TIFF を見つめて、手動で入力せずに文字を取り出す方法を考えたことがあるなら、ここが正しい場所です。パッケージのインストールから、暗号化ファイルのようなエッジケースの処理まで、全工程を順に説明するので、重要な機能開発に集中できます。

## 学べること

このチュートリアルで学べること：

* Aspose OCR for Python のセットアップ方法。
* マルチページ TIFF のすべてのページを読み取るために必要な正確なコード。
* フォントが欠如している、ページが破損しているなどの一般的な落とし穴への対処方法。
* 大規模に **TIFF からテキストを抽出** する際の精度とパフォーマンスを向上させるヒント。

最後まで読めば、任意の TIFF をプレーンテキストに変換できるスクリプトが手に入り、インデックス作成や検索、下流の NLP パイプラインへの投入がすぐに可能になります。

### 前提条件

* Python 3.8 以上（ライブラリは 3.7 以降をサポート）。
* 有効な Aspose OCR ライセンス—または無料トライアルで開始できます（コードは評価モードで動作しますが、出力に透かしが入ります）。
* Python の仮想環境に関する基本的な知識（任意ですが推奨）。

---

## ステップ 1 – Aspose OCR パッケージのインストール

まず最初に、`aspose-ocr` パッケージが必要です。PyPI にホストされているので、シンプルな `pip` インストールで完了します。

```bash
pip install aspose-ocr
```

> **Pro tip:** 依存関係を分離するために仮想環境（`python -m venv venv`）を使用しましょう。他のプロジェクトとのバージョン競合を防げます。

> **Why this matters:** パッケージをインストールすると、実際に重い処理を行うネイティブ OCR エンジンのバイナリが取得されます。これが無いと `recognize_from_tiff` メソッドが存在せず、`ImportError` が発生します。

---

## ステップ 2 – ライブラリのインポートと OCR エンジンの作成

ライブラリがマシンに入ったら、インポートして `OcrEngine` を起動します。このオブジェクトが画像データを処理する主役です。

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*`OcrEngine` クラスは言語、解像度、前処理オプションなど、すべての OCR 設定をカプセル化します。後で精度向上のためにいくつか調整します。*

---

## ステップ 3 – マルチページ TIFF ファイルへのパス指定

読み取りたい TIFF へのパスが必要です。ライブラリは絶対パスでも相対パスでも動作しますが、スクリプトが別の作業ディレクトリから実行されたときの予期せぬ挙動を防ぐために絶対パスを推奨します。

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **Common mistake:** Windows でバックスラッシュをエスケープし忘れる（`C:\\Images\\file.tif`）。生文字列（`r"C:\Images\file.tif"`）またはスラッシュ（`/`）を使うと手間が省けます。

---

## ステップ 4 – すべてのページからテキストを認識

チュートリアルの核心です：`recognize_from_tiff` を呼び出します。このメソッドは `OcrResult` オブジェクトのリストを返し、ページごとに個別にイテレートできます。

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**Why this works:** Aspose OCR は内部で TIFF を構成フレームに分割し、各フレームに OCR エンジンを適用して結果をまとめます。Pillow や ImageMagick で手動でページ分割するよりはるかに信頼性が高いです。

---

## ステップ 5 – 結果をイテレートしてテキストを出力

最後に、`OcrResult` リストをループし、抽出したテキストを表示（または保存）します。ワークフローに合わせて各ページを個別の `.txt` ファイルに書き出すことも可能です。

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**Expected output** (truncated for brevity):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **Edge case handling:** ページに認識可能なテキストが全く無い場合、`page_result.text` は空文字列になります。そのようなページは後で手動レビューできるようにログに残すと良いでしょう。

---

## ボーナス – 精度向上のための OCR 設定調整

デフォルト設定だけでは不十分なことがあります。特に低解像度のスキャンや特殊フォントの場合は以下の設定を調整してください。

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*これらのオプションは任意ですが、文字化けした出力とクリーンで検索可能な文字列の差を生むことが多いです。*

---

## よくある落とし穴と回避策

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| すべてのページで出力が空 | ファイルパスが間違っている、または TIFF 圧縮形式が非対応 | パスを確認し、TIFF がサポートされている圧縮（例: LZW、PackBits）を使用しているか確認 |
| 文字化け（例: �） | 言語設定が間違っている、またはフォントファイルが欠如 | `ocr_engine.language` を正しいロケールに設定し、必要なフォントを OS にインストール |
| 大容量 TIFF の処理が遅い | デフォルトのシングルスレッドモード | ライブラリが対応していれば `ocr_engine.recognize_from_tiff(..., parallel=True)` を使用 |
| ライセンス警告 | トライアル版をライセンスファイルなしで使用 | `aocr.License().set_license("Aspose.OCR.lic")` でライセンスキーを設定 |

---

## 完全スクリプト – すぐに実行可能

以下は、上記のすべての手順とオプションの調整を組み込んだ、自己完結型スクリプトです。`extract_tiff_text.py` という名前で保存し、`python extract_tiff_text.py` を実行してください。

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**Running the script**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

実行すると各ページのコンソールプレビューと、`output` フォルダ内に `page_1.txt`、`page_2.txt` などが生成されます。

---

## 結論

Python と Aspose OCR を使って **TIFF からテキストを抽出** するために必要なすべてを網羅しました。パッケージのインストールからマルチページ文書の処理、精度向上の設定調整、結果の保存まで、全工程が手元に揃いました。  

本番パイプラインで **TIFF をテキストに変換** したい場合は、ファイルをバッチ処理し、OCR 呼び出しを並列化し、Elasticsearch のような検索可能なインデックスに出力を保存することを検討してください。冒険心がある方は、他言語（`aocr.Language.Spanish`）を試したり、OCR 結果をスペルチェックライブラリに通してノイズを除去するのも面白いでしょう。

スケーリング、ライセンス、クラウドストレージとの統合に関する質問があれば、下のコメント欄にどうぞ。ハッピーコーディング！

---

![TIFF ファイルから抽出されたテキストへの OCR フローを示す図](https://example.com/placeholder-image.png "Python を使用した TIFF からテキスト抽出")

*画像の代替テキスト: Python を使用した TIFF からテキスト抽出*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}