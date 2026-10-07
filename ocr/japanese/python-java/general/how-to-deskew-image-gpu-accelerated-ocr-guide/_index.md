---
category: general
date: 2026-01-02
description: 画像の傾きを補正し、コントラストを強化してテキストを素早く取得する方法を学びましょう。ステップバイステップのPythonコードとテキスト抽出のコツが含まれています。
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: ja
og_description: 画像の傾きを補正し、コントラストを高めてプレーンテキストを取得する方法。テーブル抽出とGPUアクセラレーションを含む完全なPython例。
og_title: 画像の傾き補正方法 – 完全GPU OCRチュートリアル
tags:
- OCR
- Python
- Image Processing
title: 画像の傾き補正方法 – GPU 加速 OCR ガイド
url: /ja/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像のデスクュー – GPU 加速 OCR ガイド

レシートが斜めに撮られてしまったとき、**画像のデスクュー** 方法に悩んだことはありませんか？斜めの写真は、完璧に読めるはずのレシートを読みにくい混乱した状態にしてしまいます。朗報です。数行の Python コードさえ書けば、画像を自動でデスクューし、コントラストを上げ、きれいなプレーンテキストを取得できます—Photoshop の手作業は不要です。

このチュートリアルでは、**画像のデスクュー** 方法だけでなく、**コントラストを上げる** 方法、**プレーンテキストを取得** する方法、さらに OCR エンジンが検出したテーブルから**テキストを抽出** する方法も示す、完全に実行可能なサンプルを段階的に解説します。最後まで読めば、どのプロジェクトにもすぐに組み込めるスクリプトが手に入ります。

## 必要なもの

- Python 3.9 以上（コードは型ヒントを使用しているため、比較的新しいインタプリタが望ましい）
- `ocr` ライブラリ（`OcrEngine`、`EngineMode`、`ImageProcessingOptions`、`OcrResult` を提供）※ `pip install ocr‑sdk` でインストール（実際に使用しているパッケージ名に置き換えてください）
- GPU と対応ドライバ（速度向上を望む場合は必須、任意ですが推奨）
- 多少回転している、またはコントラストが低い画像ファイル（例: `receipt_skewed.jpg`）

> **プロのコツ:** GPU がない場合は `EngineMode.GPU` を `EngineMode.CPU` に変更すれば、スクリプトはそのまま動作します—ただし少し遅くなります。

## 手順別実装

以下で解決策を論理的なブロックに分割しています。各ブロックは、主要キーワード *how to deskew image* または二次キーワードを含む説明的な **H2** です。コードは完全でコメント付き、すぐに実行可能です。

### How to Deskew Image with GPU‑Accelerated OCR

最初に OCR エンジンに GPU での実行を指示し、auto‑deskew 機能を有効にします。auto‑deskew は画像のジオメトリを解析し、正立させます。

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **なぜこれが重要か:** GPU 加速により処理時間が秒単位からミリ秒単位に短縮されます。これは、1 分間に数十枚のレシートを処理する場合に特に重要です。

### Boost Image Contrast for Better Recognition

コントラストが低いレシートは OCR にとって悪夢です。コントラストを上げることで、エンジンが扱いやすいエッジを提供できます。

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **コントラストを上げる方法:** `set_contrast_boost` メソッドはパーセンテージを受け取ります。30 % がほとんどのスキャンレシートで安全なデフォルトです。画像が極端に暗い場合は 50 % に上げるか、試行錯誤してください。

### Get Plain Text from the Processed Image

画像がまっすぐで明るくなったら、エンジンに渡してプレーンテキスト結果を取得します。

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**期待される出力**（簡略化）:

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **プレーンテキストを取得する方法:** `get_text()` メソッドはレイアウト情報をすべて除去し、クリーンな文字列を返します。この文字列はデータベースに保存したり、API に送信したり、下流の分析に利用できます。

### How to Extract Text from Detected

レシートには商品、数量、価格などの表形式データが含まれることが多いです。OCR SDK はテーブルを検出でき、行やセルを反復処理できます。

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**テーブル出力例**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **テーブルを抽出する理由:** 構造化データは合計金額の計算、レポート作成、会計ソフトへの取り込みを簡単にします。

### Full Working Script

すべてをまとめたスクリプトを `deskew_and_ocr.py` にコピーして使用できます。

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

実行方法:

```bash
python deskew_and_ocr.py
```

コンソールにクリーンアップされたテキストと検出されたテーブルが表示されます。

## よくあるエッジケースと対処法

| 状況 | 対処方法 |
|-----------|------------|
| **画像が逆さま** | SDK が提供している場合は `set_rotation_correction(True)` も併用して `set_auto_deskew(True)`信頼度を上げます。 |
| **コントラスト上げすぎで画像が明るすぎる** | `set_contrast_boost` に渡すパーセンテージを下げます（例: 15 %）。 |
| **GPU が使用できない** | `EngineMode.GPU` を `EngineMode.CPU` に切り替えます。パイプラインの残りはそのままです。 |
| **テーブルが検出されない** | 解像度の高いスキャンを試すか、ライブラリが提供している場合は `set_table_detection(True)` を有効にします。 |

## 次のステップ: プレーンテキストから構造化データへ

**画像のデスクュー**、**コントラストを上げる**、**プレーンテキストを取得** の方法が分かったら、以下のような拡張が考えられます。

- 正規表現でプレーンテキストを解析し、`total`、`date` などのキー‑バリューを抽出する
- 結果を SQLite や PostgreSQL に保存し、後でレポートに利用する
- スクリプトをサーバーレス関数（AWS Lambda、Azure Functions）に組み込み、アップロードを自動処するこれらすべては、本チュートリアルで扱った基盤の上に構築できます。

## 結論

GPU 加速 OCR エンジンを用いた **画像のデスクュー** 方法、認識精度を高める **コントラストの上げ方**、正確な **プレーンテキスト取得** 方法、そしてテーブルから **テキストを抽出** する手順をすべて解説しました。完全な実行可能スクリプトを提供したので、任意の Python プロジェクトにすぐに組み込んで、斜めでコントラストの低い写真からクリーンなデータを抽出できます。

自分のレシートで試し、コントラストレベルを微調整し、OCR に任せてみてください。問題が発生したら、上記のエッジケース表を参照すればほとんどの課題は調整で解決できます。

コーディングを楽しんで、画像が常にまっすぐで明るくありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}