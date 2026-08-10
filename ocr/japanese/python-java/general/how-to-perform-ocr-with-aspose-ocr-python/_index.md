---
category: general
date: 2026-06-25
description: Aspose OCR PythonでOCRを実行する方法 – 画像OCRの読み込み、画像OCRの処理、JSON結果の抽出を数分で学びましょう。
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: ja
og_description: Aspose OCR PythonでOCRを実行する方法。このガイドに従って画像OCRを読み込み、画像OCRを処理し、JSON出力を簡単に解析しましょう。
og_title: Aspose OCR PythonでOCRを実行する方法
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Aspose OCR PythonでOCRを実行する方法
url: /ja/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR PythonでOCRを実行する方法

Pythonを使ってレシートや請求書、スキャンしたドキュメントで **OCRを実行する方法** を疑問に思ったことはありませんか？ あなただけではありません。実際のプロジェクトでは、画像からテキストを抽出することが、Automation、Analytics、またはアーカイブへの第一歩となります。  

良いニュースは？ **Aspose OCR Python** を使えば、画像OCRのロード、画像OCRの処理、そして整ったJSONペイロードを数行のコードで取得できます。以下では、完全な実行可能スクリプトと、各ステップの背後にある理由を示すので、コードがそのようになっている *なぜ* を本当に理解できます。

## このチュートリアルでカバーする内容

- PythonでAspose OCRエンジンを設定する  
- **Load image OCR** を正しく行い、TIFF、PNG、JPEGなどの一般的なフォーマットを処理する  
- **Process image OCR** を実行し、結果をJSONに変換する  
- JSONを解析して有用な情報（単語、信頼度スコアなど）を取得する  
- トラブルシューティング、エッジケースの処理、次のステップのアイデアに関するヒント  

Asposeの事前経験は不要です。動作するPython 3環境と、読み取りたい画像ファイルがあれば始められます。

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| Python 3.8+ | Aspose OCRのwheelは最新のインタプリタを対象としています |
| `aspose-ocr` package (`pip install aspose-ocr`) | 重い処理を実行するコアライブラリです |
| A sample image (e.g., `receipt.tif`) | エンジンに入力するものが必要です |
| Basic `json` knowledge | OCR出力をPythonのdictにパースします |

> **プロのコツ:** Windowsを使用している場合、パッケージをインストールする際は管理者としてコマンドプロンプトを実行し、権限に関する問題を回避してください。

---

## Aspose OCR PythonでOCRを実行する方法

以下は **完全なスクリプト** で、`ocr_demo.py` というファイルにコピー＆ペーストできます。インポートから最終出力まで全てが含まれているので、すぐに実行できます。

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### 期待される出力

`python ocr_demo.py` を実行すると（画像が存在し読み取り可能であることを前提に）、以下のような出力が表示されます：

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

正確な内容は元画像により異なりますが、`"words"` 配列が存在することで **process image OCR** が成功したことが確認できます。

---

## Load Image OCR – ヒントと一般的な落とし穴

1. **File format matters** – TIFFはスキャン文書に最適ですが、スクリーンショットにはPNG、写真にはJPEGがしばしば適しています。  
2. **Resolution** – Aspose OCRは300 dpi以上で最良のパフォーマンスを発揮します。信頼度スコアが低い場合は、ロード前に画像をアップサンプリングすることを検討してください。  
3. **Multi‑page files** – TIFFに複数ページが含まれる場合、`image = ocr.Image.load(path)` はスタックを返します。`for page in image.pages:` でイテレートし、各ページに対して `engine.recognize(page)` を呼び出すことができます。

> **このステップが重要な理由:** 画像を正しくロードすることで、OCRエンジンがクリーンなピクセルデータを受け取ります。破損したりサポートされていない形式は `engine.recognize` が例外をスローし、パイプラインが停止します。

---

## Process Image OCR – 高度なオプション

Aspose OCRは `OcrEngine` オブジェクト上でいくつかのプロパティを提供します：

| プロパティ | 使用例 |
|------------|--------|
| `engine.language = ocr.Language.English` | 画像に混在したスクリプトがある場合に英語を強制する |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | 高速だが精度は低め。クイックプレビューに適する |
| `engine.auto_rotate = True` | 回転したページを自動的に修正する（レシートに便利） |

これらはステップ 3の前に設定でき、**process image OCR** フェーズを微調整できます。例：

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## Aspose OCR Pythonの出力を理解する

JSONペイロードは予測可能なスキーマに従います：

- **pages** – 各ページの寸法と回転情報を持つページオブジェクトのリスト。  
- **lines** – 同じベースラインを共有する単語のグループ。段落の再構築に有用です。  
- **words** – `text`、`confidence`、座標を持つ `rectangle` を含む個別の単語オブジェクト。  
- **language** – 検出された言語コード（例: "en"）。  
- **confidence** – 文書全体の総合信頼度。  

この構造を理解すれば、必要な情報を正確に抽出できます。例えば、信頼度 < 0.9 の単語（OCRエラーの可能性がある）をすべて取得するには、次のように追加できます：

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## エッジケースとその対処方法

| 状況 | 推奨される対処法 |
|------|--------------------|
| **Empty result** (no words) | 画像品質を確認し、正しい言語が設定されていることを確認し、必要に応じてDPIを上げてください。 |
| **Multi‑page PDFs** | `pdf2image` などを使用してPDFページを画像に変換し、各ページをOCRエンジンに入力します。 |
| **Non‑Latin scripts** | `engine.add_language(ocr.Language.ChineseSimplified)` で追加の言語パックをインストールします。 |
| **Large files** | チャンク単位で処理し、同じ `OcrEngine` インスタンスを再利用して過剰なメモリ割り当てを防ぎます。 |

---

## 完全な動作例（すべてのステップを統合）

以下は Jupyter ノートブックやスクリプトに貼り付け可能なコンパクト版です。エラーハンドリング、オプション設定を含み、整ったサマリーを出力します。

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

これを実行すると、先ほどと同じ簡潔な出力が得られます、

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCRで画像からテキストを抽出する – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像認識でJSON結果を取得するためのAspose OCRの使用方法](/ocr/english/net/text-recognition/get-result-as-json/)
- [Aspose OCRを使用したストリームからの画像テキスト抽出の実行方法](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}