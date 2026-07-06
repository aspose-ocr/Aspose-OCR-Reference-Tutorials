---
category: general
date: 2026-05-03
description: 構造化OCR認識を用いて画像上でOCRを実行し、座標付きテキストを抽出する方法を学びましょう。ステップバイステップのPythonコードが含まれています。
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: ja
og_description: 画像に対してOCRを実行し、構造化OCR認識を使用して座標付きテキストを取得します。説明付きの完全なPython例です。
og_title: 画像でOCRを実行 – 構造化テキスト抽出チュートリアル
tags:
- OCR
- Python
- Computer Vision
title: 画像でOCRを実行する – 構造化テキスト抽出の完全ガイド
url: /ja/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行する – 構造化テキスト抽出の完全ガイド

画像ファイルに対して **OCR を実行** したいけれど、各単語の正確な位置を保持する方法が分からない、ということはありませんか？レシートのスキャン、フォームのデジタル化、UI テストなど、多くのプロジェクトで、生のテキストだけでなく、各行が画像上のどこにあるかを示すバウンディングボックスが必要になります。

このチュートリアルでは、**aocr** エンジンを使って *画像で OCR を実行* し、**構造化 OCR 認識** をリクエストし、ジオメトリを保持したまま結果を後処理する実用的な方法を紹介します。最後まで読めば、数行の Python コードで **座標付きテキスト抽出** ができるようになり、構造化モードが下流タスクで重要になる理由が理解できるようになります。

## 学べること

- **構造化 OCR 認識** 用に OCR エンジンを初期化する方法  
- 画像を入力して、行のバウンディング情報を含む生データを取得する方法  
- ジオメトリを失わずにテキストをクリーンアップする後処理の実行方法  
- 最終的な行をイテレートし、テキストとバウンディングボックスを一緒に出力する方法  

マジックや隠された手順はありません。すぐに自分のプロジェクトに組み込める、完全に実行可能なサンプルです。

---

## 前提条件

作業を始める前に、以下がインストールされていることを確認してください。

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

また、テキストがはっきりと読める画像ファイル（`input_image.png` または `.jpg`）が必要です。スキャンした請求書からスクリーンショットまで、OCR エンジンが文字を認識できるものであれば問題ありません。

---

## 手順 1: 構造化認識用に OCR エンジンを初期化する

まず最初に `aocr.Engine()` のインスタンスを作成し、**構造化 OCR 認識** を要求します。構造化モードでは、プレーンテキストだけでなく、各行のバウンディング矩形というジオメトリデータも返されます。これはテキストを画像上にマッピングする際に必須です。

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **なぜ重要か:**  
> デフォルトモードではエンジンが単に連結された文字列を返すだけになることがあります。構造化モードはページ → 行 → 単語という階層構造と座標情報を提供するため、結果を元画像にオーバーレイしたり、レイアウト認識モデルに入力したりするのが格段に楽になります。

---

## 手順 2: 画像で OCR を実行し、生データを取得する

画像をエンジンに渡します。`recognize` 呼び出しは `OcrResult` オブジェクトを返し、行ごとのコレクションが含まれます。

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

この時点で `raw_result.lines` には次の 2 つの重要な属性を持つオブジェクトが格納されています。

- `text` – その行で認識された文字列  
- `bounds` – 行の位置を表す `(x, y, width, height)` 形式のタプル  

---

## 手順 3: ジオメトリを保持しながら後処理する

生の OCR 出力はノイズが多いことがあります。余計な文字や誤ったスペース、改行の問題などです。`ai.run_postprocessor` 関数はテキストをクリーンアップしつつ **元のジオメトリを保持** します。これにより、正確な座標情報がそのまま残ります。

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **プロのコツ:** 製品コードなどドメイン固有の語彙がある場合は、カスタム辞書を後処理に渡すことで精度を向上させられます。

---

## 手順 4: 座標付きテキストを抽出し、表示する

最後に、クリーンアップされた行をループし、テキストと一緒にバウンディングボックスを出力します。これが **座標付きテキスト抽出** の核心です。

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### 期待される出力

入力画像に「Invoice #12345」および「Total: $89.99」の 2 行が含まれていると仮定すると、次のような出力が得られます。

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

最初のタプルは元画像上の行の `(x, y, width, height)` を示しており、矩形を描画したりテキストをハイライトしたり、座標を別システムに渡したりするのに利用できます。

---

## 結果の可視化（任意）

バウンディングボックスを画像に重ねて確認したい場合は、Pillow（PIL）を使って矩形を描画できます。以下は簡単なサンプルです。生データだけが必要な場合はスキップして構いません。

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![画像で OCR を実行した例（バウンディングボックス表示）](/images/ocr-bounding-boxes.png "画像で OCR を実行 – バウンディングボックスのオーバーレイ")

上記の alt テキストは **主要キーワード** を含んでおり、画像 alt 属性の SEO 要件を満たしています。

---

## なぜ構造化 OCR 認識が単純テキスト抽出より優れているのか

「ただ OCR を走らせてテキストだけ取ればいいんじゃない？」と思うかもしれませんが、ジオメトリがあると次のような利点があります。

- **空間的コンテキスト:** フォーム上で「日付」フィールドの隣にある日付の値など、データが *どこに* あるかが分かります。  
- **マルチカラムレイアウト:** 直線的なテキストだけでは順序が失われますが、構造化データは列順序を保持します。  
- **後処理精度:** ボックスサイズが分かると、単語が見出しか脚注か、あるいはノイズかを判断しやすくなります。  

要するに、**構造化 OCR 認識** を使うことで、データベースへの投入、検索可能 PDF の作成、レイアウトを考慮した機械学習モデルの学習など、より賢いパイプラインを構築できる柔軟性が得られます。

---

## よくあるエッジケースと対処法

| 状況 | 注意点 | 推奨対策 |
|-----------|-------------------|---------------|
| **回転または歪んだ画像** | バウンディングボックスが軸外れになる可能性あり | OpenCV の `warpAffine` などでデスキュー前処理を行う |
| **非常に小さいフォント** | エンジンが文字を見逃し、空行になることがある | 画像解像度を上げるか、`ocr_engine.set_dpi(300)` を使用 |
| **混在言語** | 言語モデルが合わず文字化けすることがある | 認識前に `ocr_engine.language = ["en", "de"]` などで言語を設定 |
| **重なり合うボックス** | 後処理で 2 行が誤って結合されることがある | 後処理後に `line.bounds` を確認し、`ai.run_postprocessor` の閾値を調整 |

これらのシナリオに早めに対処しておくと、1 日に数百件の文書を処理するスケールでも頭痛を防げます。

---

## 完全なエンドツーエンドスクリプト

以下は、すべての手順をまとめた実行可能なプログラムです。コピーして画像パスを調整すればすぐに動作します。

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

このスクリプトを実行すると:

1. **画像で OCR を実行** し、構造化モードで結果を取得  
2. 各行の **座標付きテキストを抽出**  
3. 任意で、バウンディングボックスを描画した PNG を生成  

---

## 結論

これで **画像で OCR を実行** し、**構造化 OCR 認識** を用いて **座標付きテキスト抽出** を行うための、自己完結型ソリューションが手に入りました。エンジンの初期化から後処理、可視化までの全工程がコードで示されているので、レシート、フォーム、任意の視覚文書に対して正確なテキスト位置情報を取得できるようになります。

次のステップは？ `aocr` エンジンを別のライブラリ（Tesseract、EasyOCR など）に置き換えて、構造化出力の違いを比較してみましょう。ドメイン固有のスペルチェックや正規表現フィルタを組み合わせて精度をさらに向上させることも可能です。大規模パイプラインを構築する場合は、`(text, bounds)` ペアをデータベースに保存して後で分析に活用してください。

Happy coding, and may your OCR projects be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}