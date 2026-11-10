---
category: general
date: 2026-03-26
description: 選択した領域で OCR を実行するための ROI ポリゴンを作成します。複数の領域を定義し、登録し、Python OCR エンジンでテキストを抽出する方法を学びましょう。
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: ja
og_description: PythonエンジンでROIポリゴンを作成し、選択した領域でOCRを実行します。完全なコード、解説、ヒントが含まれています。
og_title: ROIポリゴンを作成 – 選択領域のクイックOCR
tags:
- OCR
- Python
- Image Processing
title: ROIポリゴンを作成 – 選択領域でのOCRステップバイステップガイド
url: /ja/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI ポリゴンの作成 – 選択領域での OCR 完全チュートリアル

画像の中で重要な部分だけに OCR を実行できるように **ROI ポリゴンを作成** したことはありませんか？たとえば領収書をスキャンして合計金額だけが必要だったり、フォームで署名欄だけを読み取る必要がある場合です。そのようなケースでは、**選択領域での OCR** が時間を節約し、精度を向上させます。  

このガイドでは、2 つのポリゴンを定義し、OCR エンジンに登録し、認識されたテキストを一度の呼び出しで取得するまでの手順をすべて解説します。最後まで読めば、すぐに実行できるスクリプトと、関心領域に焦点を当てる重要性がしっかり理解できるようになります。

## 学習内容

- 一般的な OCR ライブラリを使用して **ROI ポリゴン** オブジェクトを作成する方法  
- 単一領域と複数領域を定義する違い  
- `ocr on selected area` が実行されるように、エンジンに領域を登録する方法  
- 期待される出力と、一般的な落とし穴（例：ROI の重複、結果が空）のトラブルシューティング方法  

### 前提条件

- Python 3.8+ がインストールされていること  
- `Polygon`、`Point`、`add_region_of_interest` メソッドを提供する OCR ライブラリ（例では架空の `ocr` モジュールを使用しています。実際の SDK、たとえば Tesseract‑Python ラッパーや EasyOCR に置き換えてください）  
- 座標が示すテキストを含むサンプル画像ファイル（`sample.png`）  

> **プロのコツ:** 実際のライブラリを使用する場合、画像が同じ座標系（左上が原点、X が右方向に増加、Y が下方向に増加）でロードされていることを確認してください。  

---  

## Step 1: Import the OCR Module and Load Your Image  

まず OCR パッケージをインポートし、処理したい画像を読み込みます。  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Why this matters:* エンジンは **ROI ポリゴン** を付加する前に画像データが必要です。一部のライブラリでは後から画像を渡すこともできますが、早めに初期化しておくとワークフローがすっきりします。

## Step 2: Define the First ROI Polygon  

最初の関心領域を作成します。テーブルのヘッダーを囲む矩形を描くイメージです。  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explanation:*  
- `ocr.Point(x, y)` はピクセル座標を使用します。  
- 頂点のリストは時計回りに並べます（多くのエンジンがこの順序を期待します）。  
- 任意の数の点を追加できるので、不規則な形状も作れます。矩形はその特別なケースです。

## Step 3: Define Additional ROI Polygons (Optional)  

1 つだけで止める必要はありません。以下はページ下部の署名欄を捕捉する 2 番目のポリゴンです。  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Why add more?* 複数の領域に対して **選択領域での OCR** を実行すれば、1 回のパスで別々のデータを抽出でき、各スライスを切り出して個別に処理するよりもはるかに高速です。

## Step 4: Register the ROIs with the OCR Engine  

ポリゴンが用意できたら、エンジンに「ここを見てください」と指示します。  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Important note:* エンジンを別の画像で再利用する場合、`clear_regions()` メソッドで既存の領域をクリアしてから新しい領域を追加する必要がある SDK もあります。

## Step 5: Run OCR and Retrieve the Text  

いよいよ認識を実行します。エンジンは先ほど追加したポリゴン内部だけを走査します。  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Expected output**（`sample.png` に「Invoice Total: $123.45」という文字列が最初の ROI に、 「Signature: John Doe」 が2番目の ROI に含まれていると仮定）:

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

出力が空の場合は、座標が実際にテキストと交差しているか、画像解像度が座標系と一致しているかを再確認してください。

## Edge Cases & Common Pitfalls  

| 状況                               | 注意点                               | 修正・回避策                              |
|------------------------------------|--------------------------------------|-------------------------------------------|
| **重複する ROI**                    | テキストが二重に返される可能性あり   | ポリゴンを重ならないようにするか、出力を重複除去 |
| **ROI が画像範囲外**               | エンジンがエラーを出すか何も返さない | 座標を `0 ≤ x < width`、`0 ≤ y < height` の範囲にクランプ |
| **非常に小さい ROI**               | ピクセル数が不足し OCR 精度が低下   | ポリゴンを数ピクセル拡大するか、画像をアップスケール |
| **非矩形（凹形）**                 | 一部エンジンは凸多角形しかサポートしない | 複雑な形状を複数の凸 ROI に分割 |
| **画像サイズが変わる**             | ハードコードされた座標が無効になる   | 画像寸法に対する相対座標（例：パーセンテージ）で計算 |

## Full Working Example  

以下はそのままコピーして実行できる完全スクリプトです（`ocr` を実際に使用しているライブラリに置き換えてください）。  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

`python ocr_roi_example.py` で実行すると、定義した 2 つの領域から抽出された文字列が表示されます。

## Next Steps  

- **動的 ROI 生成:** 座標をハードコードせず、OpenCV の輪郭検出などでテーブルやフィールドを自動的に検出する  
- **後処理:** 空白除去、正規表現適用、数値を適切なデータ型に変換  
- **バッチ処理:** 画像フォルダをループし、レイアウトが一定なら同じ ROI 定義を再利用  

より複雑な文書（例：複数ページの PDF やスキャンフォーム）で **選択領域での OCR** に興味がある場合は、ページ単位で ROI を登録できるライブラリを調べてみてください。  

---  

### Visual Overview  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="サンプル画像上の 2 つの ROI ポリゴンを示す図"}

この図は、青と緑の 2 つの矩形が画像上にどのように配置され、OCR エンジンが読み取る領域が正確にどこかを示しています。

---  

## Conclusion  

私たちは **ROI ポリゴン** オブジェクトを作成し、OCR エンジンに登録し、`ocr on selected area` をクリーンで再現性のあるスクリプトで実行しました。関心のある領域だけにエンジンを限定することで、処理時間を短縮し、精度を向上させ、下流のデータ処理も格段にシンプルになります。  

自分の画像で試してみてください—座標を調整したり、ポリゴンを増やしたり、出力をデータベースに連携したりしてみましょう。領域ベースの OCR をマスターすれば、可能性は無限に広がります。  

質問や面白い活用例があればコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}