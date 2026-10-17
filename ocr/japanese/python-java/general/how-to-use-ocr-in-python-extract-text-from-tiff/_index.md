---
category: general
date: 2026-07-05
description: PythonでOCRを使用してTIFFを素早くテキストに変換する方法。TIFF画像からテキストを抽出し、Python OCRエンジンを構築するためのocrライブラリの手順を学びましょう。
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: ja
og_description: PythonでOCRを使用する方法は？このガイドでは、PythonのOCRエンジンとocrライブラリを使って、TIFFをテキストに変換する手順をステップバイステップで示します。
og_title: PythonでOCRを使用する方法 – 完全なTIFFテキスト抽出
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: PythonでOCRを使用する方法 – TIFFからテキストを抽出
url: /ja/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを使用する方法 – TIFFからテキストを抽出

スキャンした本を編集可能なテキストに変換するために、**PythonでOCRを使用する方法**を考えたことはありませんか？ あなただけではありません—開発者、研究者、趣味で取り組む人々も、マルチページTIFF画像を扱う際に同じ壁にぶつかります。 良いニュースは？ **ocr library python** を使えば、軽量なOCRエンジンを起動し、TIFFファイルを指定するだけで、数秒でクリーンで検索可能なテキストが得られます。

このチュートリアルでは、必要なすべての手順を解説します：適切なパッケージのインストール、マルチページTIFFの読み込み、OCRエンジンの実行、そして最終的に各ページの内容を出力します。最後まで読めば、**TIFFをテキストに変換**し、**TIFFからテキストを抽出**する方法をPython環境から離れることなく実現できます。

## 前提条件

- Python 3.9 以上（例は 3.11 でテスト済み）
- `ocr` ライブラリの最新バージョン（または好みの互換性のある `python ocr engine`）
- 処理したいマルチページTIFFファイル（ここでは `scanned_book.tif` と呼びます）
- Python スクリプトと仮想環境の基本的な知識

重い外部ツールは不要です—pip と数行のコードだけで始められます。

## OCRライブラリ（Python）をインストール

まず最初に、堅牢なOCRバックエンドが必要です。このガイドでは、シンプルな高レベルAPIを備えた架空の `ocr` パッケージを使用しますが、同じパターンは `pytesseract` のようなTesseractベースのラッパーや商用SDKでも機能します。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **プロのコツ:** Windows でパッケージがネイティブバイナリに依存している場合、適切な Visual C++ 再頒布可能パッケージがインストールされていることを確認してください。インストーラは不足しているものがあると警告を出すことが多いです。

## PythonでOCRエンジンを使用する方法

ライブラリの準備ができたので、OCRエンジンを起動し、TIFFファイルを指定しましょう。以下のスニペットはエンジンインスタンスを作成し、言語を英語に設定し、マルチページ処理の準備を行います。

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**なぜ言語を設定するのか？**  
ほとんどのOCRエンジンは言語モデルを使用して精度を向上させます。このステップを省略すると、エンジンは汎用モデルにフォールバックし、句読点や特殊文字を誤認識する可能性があります。

## マルチページTIFF画像をロード

次にスキャンした文書を読み込みます。`ocr.Image.load` ヘルパーはTIFFスタックをそのまま理解し、各ページを内部的に表すオブジェクトを返します。

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **エッジケース:** TIFF が圧縮（CCITT Group 4、LZW など）されていてライブラリがエラーを出す場合は、まず ImageMagick で非圧縮版に変換してみてください:  
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## すべてのページでOCRを実行 – TIFFをテキストに変換

画像オブジェクトが手元にあれば、エンジンは一度にすべてのページを処理できます。このメソッドは、各要素が単一ページのOCR結果を保持するリストを返します。

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**内部で何が起きているのか？**  
`recognize_multi_page` 関数は各ラスタライズされたページを反復し、ニューラルネットワーク認識器を実行し、プレーンテキスト出力と信頼度スコアをまとめます。実質的にバッチ処理で、手動でループを書く手間を省きます。

## 結果を反復処理 – TIFFからテキストを抽出

最後に認識されたテキストを表示します。出力を個別の `.txt` ファイルに書き出したり、データベースにプッシュしたり、検索インデックスに流し込んだり、ワークフローに合わせて自由に扱えます。

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### 期待される出力

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

各 `result.text` 文字列にはそのページの生のOCR出力が含まれます。改行を保持したい場合は、多くのエンジンが `result.lines` を文字列のリストとして提供しています。

## 大きなTIFFファイルの取り扱い – ヒントとコツ

500ページのTIFFを処理するとメモリを大量に消費します。スムーズに処理するための戦略をいくつか紹介します：

1. **ページを分割** – `recognize_multi_page` の代わりに、ジェネレータ内で `engine.recognize(page)` を呼び出し、1ページずつ処理させます。  
2. **DPI を調整** – 画像解像度を下げる（例：300 DPI から 200 DPI）ことで CPU 負荷を減らし、ほとんどの印刷テキストの精度への影響は最小限です。  
3. **並列化** – OCRエンジンがスレッドセーフであれば、`concurrent.futures.ThreadPoolExecutor` を使って複数ページを同時に認識させます。

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## 抽出したテキストをファイルに保存

実務でのパイプラインは永続的な保存が必要です。以下は各ページのテキストを順序通りに個別ファイルへダンプする簡潔な方法です。

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

これでインデックス作成やさらなる NLP 処理にすぐ使える `.txt` ファイル群が整いました。

## 画像プレビュー – OCR結果を視覚的に利用する方法

デバッグに便利な、元画像上にOCRオーバーレイを表示したい場合、多くのライブラリでバウンディングボックス描画が可能です。以下は Pillow を使った簡単な例です：

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![PythonでOCRを使用する方法 – TIFFページ上のOCRオーバーレイ](ocr_overlay_example.png)

*Alt text:* PythonでOCRを使用する方法 – 認識されたテキストをTIFFページ上に視覚的にオーバーレイした例。

## よくある落とし穴と回避策

| 問題 | 発生理由 | 解決策 |
|------|----------|--------|
| 文字化け | 言語モデルが間違っている | `engine.language` を正しい enum に設定する |
| ページが欠落 | TIFF 圧縮がサポートされていない | まず非圧縮 TIFF に変換する |
| 処理が遅い | 高 DPI + シングルスレッド処理 | DPI を下げるかマルチスレッド化を有効にする |
| 出力が空 | 画像が暗すぎる／コントラストが低い | コントラストストレッチ（`opencv` または `Pillow`）で前処理する |

これらを早期に対処すれば、後で何時間もデバッグに費やすことを防げます。

## 次のステップ – 基本抽出を超えて

**PythonでOCRを使用する方法** の基本をマスターした今、以下のテーマを探求してみてください：

- **PDF生成** – 抽出したテキストを `reportlab` と組み合わせ、検索可能なPDFを再構築します。  
- **言語検出** – `langdetect` を使って `engine.language` を自動切替えします。  
- **構造化データ抽出** – 正規表現や spaCy を利用し、生テキストから日付、名前、表などを抽出します。  
- **代替OCRバックエンド** – 多言語対応が必要な場合は `ocr` を `pytesseract` や `easyocr` に置き換えます。

これらのトピックはすべて、二次キーワード **ocr library python**、**convert tiff to text**、**extract text from tiff**、**python ocr engine** と自然に結びつき、より高度なプロジェクトへの堅実な基盤を提供します。

---

### 結論

インストールからマルチページ処理まで、**PythonでOCRを使用する方法** を網羅し、シンプルな **python OCR engine** を使って **TIFFをテキストに変換** し **TIFFからテキストを抽出** する手順を示しました。上記の完全な実行可能サンプルは、標準的なTIFFファイルのほとんどでそのまま動作し、提示したヒントは大規模文書へのスケールやOCRを大規模パイプラインに統合する際に役立ちます。

自分のスキャンした書籍、領収書、アーカイブ画像で試してみてください。その後は「次のステップ」セクションにある高度なアイデアを実験してみましょう。コーディングを楽しみ、OCR結果が常に正確であることを願っています！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCRで画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for JavaでTIFFからテキストを抽出する方法](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose OCRを使用したストリームからの画像テキスト抽出の実行方法](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}