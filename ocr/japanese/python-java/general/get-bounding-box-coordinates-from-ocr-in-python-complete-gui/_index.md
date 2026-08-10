---
category: general
date: 2026-06-22
description: Python を使用して画像からバウンディングボックス座標を取得します。Aspose OCR と JSON パースを使って、数分で画像からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: ja
og_description: Python を使用して画像からバウンディングボックス座標を取得します。このガイドでは、Aspose OCR を使った Python
  での画像からのテキスト抽出とレイアウトデータの解析方法を示します。
og_title: PythonでOCRからバウンディングボックス座標を取得する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: PythonでOCRからバウンディングボックス座標を取得する完全ガイド
url: /ja/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRからバウンディングボックス座標を取得する – 完全ガイド

スキャンした請求書のすべての単語の **バウンディングボックス座標** を取得したいが、どこから始めればよいか分からないことはありませんか？ あなただけではありません。多くの自動化プロジェクトでは、画像上のテキストをハイライトしたり、マスクしたり、下流の分析に渡したりする必要があります。良いニュースは、数行の Python と Aspose.OCR を使えば、テキスト **と** その正確な位置を一度の処理で取得できることです。

このチュートリアルでは、**画像からテキストを抽出する** 方法をハンズオンで示し、JSON レイアウトデータを解析してバウンディングボックスを取り出すまでを解説します。余計な説明は省き、動作するスクリプト、各ステップの重要性の説明、そして一般的な落とし穴を回避するコツを提供します。

---

## 作成するもの

このガイドの最後までに、すぐに実行できる Python スクリプトが手に入ります。このスクリプトは以下を実現します。

1. 画像（例: 請求書 PNG）を Aspose OCR に読み込む。  
2. エンジンを設定し、JSON 形式のレイアウト情報を出力させる。  
3. JSON を Python の辞書型に変換する。  
4. 認識されたすべての単語を走査し、テキスト **と** バウンディングボックス座標を出力する。

さらに、マルチページ PDF、異なる画像フォーマット、カスタム座標系への対応方法も紹介します。

### 前提条件

- Python 3.8+ がインストールされていること。  
- Aspose.OCR for Python の有効なライセンスまたは無料トライアル（ライセンスなしでも動作しますが透かしが入ります）。  
- `pip install aspose-ocr`（PyPI のパッケージ名）。  
- `invoice.png` というサンプル画像を、参照できるフォルダーに配置しておくこと。

以上だけです。重いフレームワークや外部サービスは不要です。さっそく始めましょう。

---

## Step 1: 必要なライブラリのインストールとインポート

まず、Aspose OCR パッケージと組み込みの `json` モジュールが利用可能か確認します。`json` は Python に標準で同梱されているので、インストールが必要なのは Aspose だけです。

```bash
pip install aspose-ocr
```

スクリプトでインポートします。

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Why this matters:** `aspose.ocr` をインポートすると高性能 OCR エンジンにアクセスでき、`json` を使うことで生のレイアウト文字列を Python のネイティブ辞書に変換して簡単に走査できます。

---

## Step 2: OCR エンジンを作成し画像を読み込む

エンジンは処理の中心です。インスタンス化した後、スキャンしたい画像を指定します。

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro tip:** `"YOUR_DIRECTORY/invoice.png"` を実際のファイルを指す絶対パスまたは相対パスに置き換えてください。ファイルが見つからない場合、Aspose は `FileNotFoundError` をスローするので、スペルを再確認しましょう。

---

## Step 3: エンジンを JSON レイアウトデータ出力に設定する

Aspose OCR はプレーンテキスト、OCR のみの JSON、あるいは単語・行・文字レベルの座標を含むフルレイアウト JSON を返すことができます。**バウンディングボックス座標を取得**するにはレイアウト JSON が必要です。

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Why JSON?** JSON は言語に依存せず、人間が読みやすく、Python の辞書にきれいにマッピングできます。レイアウト JSON には `"words"` 配列があり、各エントリはテキストと 8 つの数値からなる `boundingBox`（4 つのコーナーポイント）を保持しています。

---

## Step 4: 認識を実行し生の JSON 文字列を取得する

いよいよ OCR を実行します。`recognize()` メソッドは `OcrResult` オブジェクトを返し、そこから JSON 文字列を取り出せます。

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

`layout_json` を `print` すると、次のような出力が得られます。

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Edge case:** 画像によっては OCR エンジンがテキストを検出できず、`"words"` 配列が空になることがあります。その場合は画像の品質（コントラスト、解像度）を確認してから再試行してください。

---

## Step 5: JSON を Python の辞書にパースする

文字列操作よりもネイティブな Python 構造を扱う方がはるかに楽です。`json.loads()` を使って文字列を辞書に変換します。

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

これで `layout_data["words"]` は、単語とバウンディングボックスを表す辞書オブジェクトのリストになります。

---

## Step 6: 単語を走査し **バウンディングボックス座標を取得**する

本チュートリアルの核心です。各単語をループし、テキストと座標を抽出して出力します。ここが **バウンディングボックス座標を取得**する正確な場所です。

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**サンプル出力**（画像に応じて数値は異なります）:

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Why the eight‑point format?** 四つのコーナー（左上、右上、右下、左下）を保持することで、テキストが傾いている場合でも単語を多角形で描画できます。単純な矩形だけが必要な場合は、`x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, `height = max(y…) - y_min` のように計算できます。

---

## Optional Enhancements

### 1. バウンディングボックスをシンプルな矩形に変換する

下流ツールが `(x, y, width, height)` 形式を期待する場合は、以下のヘルパー関数を追加してください。

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. マルチページ PDF に対応する

Aspose OCR は PDF ストリームも受け付けます。画像読み込み行を次のように置き換えます。

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

各ページに対して `set_page_number` を呼び出し、ページごとに座標を収集します。

### 3. バウンディングボックスを可視化する

元画像上にボックスを描画したい場合は Pillow を使用します。

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

これで認識されたすべての単語の周りに赤い輪郭が描かれ、デバッグや UI オーバーレイに最適です。

---

## Common Questions & Gotchas

- **JSON が巨大になる場合は？** 大規模文書では JSON をストリーミングするか、ページ単位で処理してメモリ使用量を抑えることを検討してください。  
- **一部の単語が欠落しているのはなぜ？** コントラストが低い、手書き文字などは OCR エンジンの検出が難しいです。画像を前処理（コントラスト上げ、二値化）してから Aspose に渡すと改善することがあります。  
- **文字レベルの座標も取得できるか？** 可能です。`engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` を設定すると、`"characters"` 配列とそれぞれの `boundingBox` が得られます。  
- **座標系はゼロベースか？** はい。画像左上が (0, 0) です。

---

## Full Script – Ready to Copy & Run

以下はすべての手順を組み合わせた完全な実行例です。`extract_bboxes.py` として保存し、`python extract_bboxes.py` で実行してください。

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}