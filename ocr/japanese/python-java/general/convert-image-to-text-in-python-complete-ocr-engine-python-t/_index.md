---
category: general
date: 2026-07-05
description: Python OCRで画像をテキストに変換 – 画像からテキストを抽出し、JPGからテキストを認識する方法を示すステップバイステップのPython
  OCR例
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: ja
og_description: Python OCR を使用して画像をテキストに変換します。この Python OCR の例に従い、画像からテキストを抽出し、数分で
  JPG のテキストを認識できます。
og_title: Pythonで画像をテキストに変換 – 完全OCRエンジンガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: Pythonで画像をテキストに変換する – 完全OCRエンジンPythonチュートリアル
url: /ja/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像をテキストに変換 – 完全OCRエンジンチュートリアル

画像を**テキストに変換**したいけど、どのライブラリを信頼すべきか分からないことはありませんか？同じ壁にぶつかる開発者は多いです。スキャンしたレシートや看板の写真から文字を抽出しようとしたときに特にそうです。朗報です。PythonのOCRエコシステムは、この作業をほぼ手間なく実現できます。

この**python ocr example**では、実際のシナリオを通して解説します。JPEGにキリル文字が含まれており、**画像からテキストを抽出**したい場合です。最後まで読めば、**jpgからテキストを認識**する方法、各ステップの重要性、他の言語や画像形式にコードを適応させる方法が分かります。

## 必要なもの

作業を始める前に、以下を用意してください。

* Python 3.8+（最新の安定版がベスト）
* OCRパッケージをインストールできるインターネット接続
* テキストが含まれる画像ファイル（例: `cyrillic_sample.jpg`）
* 任意だけど便利: 依存関係を整理できる仮想環境

OSレベルの重い依存関係や特殊なビルドツールは不要です。pipコマンド数個と数行のコードで完了します。

## Step 1: OCRエンジンPythonパッケージをインストール

最初に行うべきことは、Pythonと相性の良いOCRエンジンを入手することです。このチュートリアルでは、実際のライブラリ（`pytesseract`や`easyocr`など）と同様のAPIを持つ架空の `ocr` パッケージを使用します。以下でインストールしてください。

```bash
pip install ocr
```

> **このステップが重要な理由:** パッケージをインストールすると、実際に重い処理を行うネイティブバイナリや言語データが取得されます。インストールを省略すると、`import ocr` の瞬間に `ImportError` が発生します。

## Step 2: モジュールをインポートし環境を設定

ライブラリが手元にあるので、必要なモジュールをインポートします。また、エンジンの内部動作を確認できるようにロギングを設定します。**画像からテキストを抽出**する際に、画像が完璧でない場合に役立ちます。

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **プロのコツ:** Jupyter notebook 内で作業している場合は、`logging.getLogger().setLevel(logging.DEBUG)` を設定すると、さらに詳細な情報が得られます。

## Step 3: OCRエンジンインスタンスを作成

エンジンの作成は、**ocr engine python** ワークフローの基礎です。暗い部屋の電気を点けるイメージで、これがないとパイプライン全体が何も見えません。

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **このステップが重要な理由:** `OcrEngine` オブジェクトは、言語パックや前処理オプション、ハードウェアアクセラレーションフラグなどの設定を保持します。後からこれらを変更すると、以降のすべての認識結果に影響します。

## Step 4: 正しい言語を選択 – キリル文字サポート

キリル文字（またはラテン文字以外）を扱う場合、エンジンにロードすべき言語モデルを指示する必要があります。指示しないと、文字化けや空文字列が返ってきます。

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **エッジケース:** エンジンによっては言語データを別途ダウンロードする必要があります。`LanguageDataNotFound` のようなエラーが出たら、`ocr.download_language('CYRILLIC')` を実行してから言語を設定してください。

## Step 5: 変換対象の画像を読み込む

ここで**画像をテキストに変換**が本格的に始まります。OCRエンジンは生のファイルパスではなく `Image` オブジェクトで動作するため、まず JPEG をラップします。

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **なぜ重要か:** 画像を読み込むことで、エンジンはサイズ、カラーデプス、DPI などを検査できます。これらのプロパティは、**jpgからテキストを認識**する精度に直結します。

## Step 6: テキストを認識 – Python OCR例の核心

いよいよエンジンに「ピクセルを文字に変換」させます。`recognize` メソッドは、抽出された文字列、信頼度スコア、バウンディングボックスを保持した結果オブジェクトを返します。

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **取得できるもの:** `ocr_result.text` は改行が保持された普通の Python 文字列です。単語レベルの位置情報が必要なら `ocr_result.boxes` を調べてください。

## Step 7: 認識結果を出力 – 変換成功を確認

**画像をテキストに変換**が正しく行われたか確認する最もシンプルな方法は、結果をコンソールに出力することです。実際のアプリケーションでは、データベースやテキストファイルに書き込むことが多いでしょう。

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### 期待される出力

`cyrillic_sample.jpg` に「Привет, мир!」というフレーズが含まれていると仮定すると、コンソールには次のように表示されます。

```
=== OCR OUTPUT ===
Привет, мир!
```

出力が空だったり意味不明だったりしたら、言語設定と画像品質を再確認してください。ぼやけた画像やコントラストが低い画像は、**画像からテキストを抽出**する結果が悪くなる典型的な原因です。

## よくある落とし穴の対処法

| 問題 | 発生理由 | 簡単な対策 |
|------|----------|------------|
| **空文字列** | 言語モデルがロードされていない、または画像が暗すぎる | `ocr_engine.language` がスクリプトに合っているか確認し、`ocr.Image.adjust_contrast()` でコントラストを上げる |
| **文字化け** | 言語が間違っている、または混在スクリプト | `ocr_engine.language = ocr.Language.MULTI` に設定するか、ラテン文字とキリル文字で2回実行する |
| **大量バッチで遅い** | エンジンが画像を順次処理している | マルチスレッド化: `ocr_engine.set_threads(4)` |
| **メモリリーク** | 画像リソースを解放していない | 認識後に `cyrillic_image.close()` を呼び出す |

> **プロのコツ:** バッチ処理時は、認識ループを `try/except` で囲み、たまに発生する `ocr.EngineError` を捕捉してジョブ全体が中断しないようにします。

## 例の拡張 – JPEGからPDFへ、キリル文字から多言語へ

**画像をテキストに変換**するパターンは、PNG、BMP、TIFF、さらにはスキャンしたPDF（ページを画像として抽出すれば可）にも適用できます。複数言語が混在する画像から**画像からテキストを抽出**したい場合は、言語リストを渡すだけです。

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

スマートフォンで撮影した高解像度写真を扱う場合は、前処理ステップを検討してください。

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

これらの調整により、普通の**python ocr example**が本番レベルのコードに変わります。

## 完全動作スクリプト

以下は、すべての要素を組み合わせた完成版スクリプトです。`convert_image_to_text.py` として保存し、`python convert_image_to_text.py` で実行してください。



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するテーマを深掘りします。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}