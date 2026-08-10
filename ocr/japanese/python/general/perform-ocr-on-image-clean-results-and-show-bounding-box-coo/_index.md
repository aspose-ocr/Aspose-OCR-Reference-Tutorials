---
category: general
date: 2026-03-28
description: 画像に対して OCR を実行し、バウンディングボックス座標付きのクリーンなテキストを取得します。OCR の抽出、クリーンアップ、結果のステップバイステップ表示方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: ja
og_description: 画像でOCRを実行し、出力をクリーンアップし、簡潔なチュートリアルでバウンディングボックスの座標を表示します。
og_title: 画像でOCRを実行 – 結果とバウンディングボックスをクリーンに
tags:
- OCR
- Computer Vision
- Python
title: 画像でOCRを実行 – 結果をクリーンにし、バウンディングボックス座標を表示
url: /ja/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像でOCRを実行 – 結果をクリーンアップしバウンディングボックス座標を表示

画像ファイルで **OCRを実行** したいけれど、テキストが乱雑で画像上の各単語の位置が分からない、という経験はありませんか？ 多くのプロジェクト—請求書のデジタル化、レシートのスキャン、シンプルなテキスト抽出—で、OCR の生データを取得するだけでも最初のハードルです。 良いニュースは、出力をクリーンにして、膨大なボイラープレートコードを書かずに各領域のバウンディングボックス座標を即座に確認できることです。

このガイドでは **OCR の抽出方法**、**OCR をクリーンアップする方法** のポストプロセッサ、そして最終的に **バウンディングボックス座標を表示** する手順を順に解説します。 最後まで読むと、ぼやけた写真を整然とした構造化テキストに変換し、下流処理にすぐ使える単一の実行可能スクリプトが手に入ります。

## 必要なもの

- Python 3.9+（以下の構文は3.8以降で動作します）
- `recognize(..., return_structured=True)` をサポートする OCR エンジン（例: スニペットで使用されている架空の `engine` ライブラリ）。Tesseract、EasyOCR、または領域データを返す任意の SDK に置き換えてください。
- Python の関数とループに関する基本的な知識
- スキャンしたい画像ファイル（PNG、JPG など）

> **Pro tip:** Tesseract を使用している場合、`pytesseract.image_to_data` 関数はすでにバウンディングボックスを提供します。その結果を小さなアダプタでラップして、下記の `engine.recognize` API と同じ形にすることができます。

---

![画像でOCRを実行しバウンディングボックス座標を可視化する図](image-placeholder.png "画像でOCRを実行しバウンディングボックス座標を可視化する図")

*Alt text: diagram showing how to perform OCR on image and visualize bounding box coordinates*

## ステップ 1 – 画像でOCRを実行し構造化された領域を取得

最初に OCR エンジンに、単なるプレーンテキストではなく、テキスト領域の構造化リストを返すよう指示します。このリストは生文字列とそれを囲む矩形を含みます。

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**なぜ重要か:**  
プレーンテキストだけを取得すると空間的コンテキストが失われます。構造化データがあれば、後で **バウンディングボックス座標を表示** したり、テキストをテーブルに合わせたり、正確な位置情報を下流モデルに渡したりできます。

## ステップ 2 – ポストプロセッサでOCR出力をクリーンアップする方法

OCR エンジンは文字を検出するのは得意ですが、余計なスペースや改行アーティファクト、誤認識シンボルが残りがちです。ポストプロセッサはテキストを正規化し、一般的な OCR エラーを修正し、余分な空白をトリムします。

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

独自のクリーンアップロジックを作る場合は、以下を検討してください：

- 非ASCII文字の除去 (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- 複数のスペースを単一のスペースに縮小
- `pyspellchecker` のようなスペルチェッカーを適用して明らかな誤字を修正

**なぜ気にすべきか:**  
整った文字列は検索、インデックス作成、下流の NLP パイプラインの信頼性を格段に向上させます。言い換えれば、 **OCR をクリーンアップする方法** が使えるデータセットと頭痛の種になるデータセットの差を決めます。

## ステップ 3 – クリーンアップされた各領域のバウンディングボックス座標を表示

テキストが整ったら、各領域を走査し、矩形とクリーンな文字列を出力します。ここが最終的に **バウンディングボックス座標を表示** する部分です。

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**サンプル出力**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

この座標を描画ライブラリ（例: OpenCV）に渡して元画像にボックスを重ね合わせたり、後でクエリできるようにデータベースに保存したりできます。

## 完全な実行可能スクリプト

以下は 3 つのステップをすべて結びつけた完全なプログラムです。プレースホルダーの `engine` 呼び出しを実際に使用している OCR SDK に差し替えてください。

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### 実行方法

```bash
python perform_ocr.py sample_invoice.jpg
```

実行すると、サンプル出力と同様にクリーンテキストとバウンディングボックスの一覧が表示されます。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| **OCRエンジンが `return_structured` をサポートしていない場合はどうしますか？** | エンジンの生データ（通常は座標付き単語のリスト）を `text` と `bounding_box` 属性を持つオブジェクトに変換する薄いラッパーを書きます。 |
| **信頼度スコアを取得できますか？** | 多くの SDK は領域ごとの信頼度指標を提供しています。出力文に追加してください: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`。 |
| **回転したテキストを処理するには？** | `recognize` を呼び出す前に、OpenCV の `cv2.minAreaRect` で画像をデスクューする前処理を行います。 |
| **出力を JSON 形式にしたい場合は？** | `processed_result.regions` を `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` でシリアライズします。 |
| **ボックスを可視化する方法はありますか？** | ループ内で OpenCV を使用し、`cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` と描画し、最後に `cv2.imwrite("annotated.jpg", img)` で保存します。 |

## まとめ

**画像でOCRを実行**し、生データをクリーンアップし、 **バウンディングボックス座標を表示** する方法を学びました。認識 → ポストプロセス → 走査という 3 ステップのフローは、信頼できるテキスト抽出が必要なあらゆる Python プロジェクトに再利用可能なパターンです。

### 次にやること

- **異なる OCR バックエンド**（Tesseract、EasyOCR、Google Vision）を試して精度を比較する。
- **データベースと統合**し、領域データを検索可能なアーカイブとして保存する。
- **言語検出を追加**して、各領域を適切なスペルチェッカーにルーティングする。
- **元画像にボックスをオーバーレイ**して視覚的に検証する（上記の OpenCV スニペット参照）。

問題が発生したら、最大の効果はしっかりしたポストプロセッシングにあることを思い出してください。クリーンな文字列は、生の文字列の塊よりもはるかに扱いやすくなります。

Happy coding, and may your OCR pipelines be ever tidy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}