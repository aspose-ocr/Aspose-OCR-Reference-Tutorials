---
category: general
date: 2026-06-16
description: Python OCR を使用して画像からテキストを認識します。OCR 用に画像を読み込む方法、高精度モードの設定方法、そして OCR 認識を実行して画像をテキストに変換する方法を学びます。
draft: false
keywords:
- recognize text from image
- convert image to text
- load image for ocr
- run ocr recognition
- set high accuracy mode
language: ja
og_description: Pythonで画像からテキストを認識します。このガイドでは、OCR用に画像を読み込む方法、高精度モードの設定方法、そしてOCR認識を実行して画像をテキストに変換する手順を示します。
og_title: 画像からテキストを認識する – 完全なPython OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  headline: recognize text from image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  name: recognize text from image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Empty Result
    text: 'Sometimes the engine returns an empty string. This usually means the image
      is too blurry or the text color blends with the background. Try:'
  - name: 2. Non‑Latin Scripts
    text: 'If your picture contains Cyrillic, Chinese, or Arabic characters, you’ll
      need to tell the OCR engine which language pack to use:'
  - name: 3. Large Batches
    text: Processing a folder of images? Wrap the core logic in a loop and reuse the
      same engine instance to avoid repeated initialization overhead.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像からテキストを認識する – 完全ステップバイステップガイド
url: /ja/python-java/general/recognize-text-from-image-with-python-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する – 完全なPython OCRチュートリアル

クラウドサービスに料金を払わずに **画像からテキストを認識** できる方法を考えたことはありませんか？ あなただけではありません。古いレシートをデジタル化したり、スクリーンショットからキャプションを抽出したり、画像を編集可能なテキストに変換することは便利なスキルです。

このチュートリアルでは、**画像をOCR用にロード**、**高精度モードを設定**、そして **OCR認識を実行** して、Python数行で **画像をテキストに変換** できる **完全な実行可能サンプル** を順に解説します。余計な説明は省き、すぐにコピー＆ペーストできる実践的な内容だけです。

## 作成するもの

このガイドの最後までに、以下の機能を持つ小さなスクリプトが完成します。

1. OCRエンジンをインスタンス化します。
2. 低解像度画像での結果向上のために **set high accuracy mode** フラグを有効にします。
3. ディスクから **画像をOCR用にロード** します。
4. **OCR認識を実行** して **画像からテキストを認識** します。
5. 抽出された文字列を出力し、実質的に **画像をテキストに変換** します。

Python 3.8 以上と少しの好奇心があれば、すぐに始められます。

## 前提条件

- **Python 3.8以上** – コードは古いバージョンが理解できない型ヒントを使用しています。
- `ocr` モジュールを提供するOCRライブラリ（例は汎用ラッパーを模倣しています。`pytesseract`、`easyocr`、または好みのベンダー固有SDKに置き換えてください）。
- 制御できるフォルダーに `low-res.jpg` という名前の低解像度JPEGがあること。
- (オプション) 依存関係を整理するための仮想環境: `python -m venv venv && source venv/bin/activate`。

```bash
# Example installation for a hypothetical `ocr` package
pip install ocr-lib
```

> **Pro tip:** `pytesseract` を使用している場合は、Tesseractエンジンを別途インストールしてください（Linuxでは `sudo apt-get install tesseract-ocr`、macOSでは Homebrew）。

---

## ステップ1: 画像からテキストを認識する – OCRエンジンの初期化

まず最初に、重い処理を担当する新しい OCR エンジンオブジェクトが必要です。

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* `OcrEngine` クラスは以降のすべての操作のエントリーポイントです。ピクセルを解釈する脳のようなものと考えてください。実行ごとに新しいインスタンスを作成することで、後で **set high accuracy mode** などの設定を切り替える際にクリーンな状態が保たれます。

---

## ステップ2: 高精度モードの設定 – 低解像度結果の向上

低解像度画像は OCR エンジンを混乱させやすいです。高精度フラグを有効にすると、エンジンは文字を読む前に追加の前処理（アップスケーリング、ノイズ除去など）を適用します。

```python
# Step 2: Enable high‑accuracy mode for better results
engine.high_accuracy = True   # <-- activates advanced preprocessing
```

> **Why enable it?** 画像が粒状だったり小さすぎたりすると、デフォルトモードでは文字が抜け落ちたり単語が結合したりします。高精度モードは速度を少し犠牲にして、正確さを大幅に向上させます—レイテンシが重要でないワンオフスクリプトに最適です。

---

## ステップ3: OCR用に画像をロード – ファイルの準備

ここで実際に **画像をOCR用にロード** します。`ocr.Image.load_from_file` ヘルパーはファイル I/O と画像デコードの手順を抽象化します。

```python
# Step 3: Load the low‑resolution image to be processed
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/low-res.jpg")
```

*What’s happening under the hood?* ライブラリは JPEG を読み込み、ビットマップに変換し、エンジンインスタンス内に保持します。Web リクエストなどでメモリ上にある画像を扱う必要がある場合、多くのライブラリは `from_bytes` メソッドも提供しているので、呼び出しを置き換えるだけです。

---

## ステップ4: OCR認識の実行 – コアアクション

エンジンが準備でき、画像が配置されたら、ついに **OCR認識を実行** します。このステップが実際のテキスト抽出を行います。

```python
# Step 4: Perform OCR recognition on the image
high_res_result = engine.recognize()
```

`recognize()` メソッドは生文字列、信頼度スコア、場合によってはバウンディングボックスのメタデータを含む結果オブジェクトを返します。**画像をテキストに変換** する目的では、`text` 属性に注目します。

---

## ステップ5: 認識されたテキストの出力 – 画像をテキストに変換

プロセスの最終段階：抽出された文字列を出力します。ここで画像がついに編集可能なテキストになります。

```python
# Step 5: Output the recognized text
print(high_res_result.text)
```

**期待される出力**（実際のテキストは画像に依存します）:

```
Invoice #12345
Date: 2024‑03‑15
Total: $256.78
Thank you for your business!
```

文字化けが出た場合は、**set high accuracy mode** が `True` になっているか、画像が過度に圧縮されていないかを再確認してください。

---

## 一般的なエッジケースの処理

### 1. 空の結果

エンジンが空文字列を返すことがあります。これは通常、画像がぼやけているか、文字色が背景と混ざっていることを意味します。次を試してください：

- ロード前に画像解像度を上げる（`PIL.Image.resize`）。
- コントラストを調整する（`ImageEnhance.Contrast`）。

### 2. 非ラテン文字スクリプト

画像にキリル文字、中文、アラビア文字などが含まれる場合、OCR エンジンに使用する言語パックを指定する必要があります：

```python
engine.language = "eng+rus"   # Example for English + Russian
```

### 3. 大量バッチ処理

フォルダー内の画像を一括処理しますか？ コアロジックをループで包み、同じエンジンインスタンスを再利用すれば、初期化オーバーヘッドを削減できます。

```python
import pathlib

engine = ocr.OcrEngine()
engine.high_accuracy = True
engine.language = "eng"

for img_path in pathlib.Path("batch/").glob("*.jpg"):
    engine.image = ocr.Image.load_from_file(str(img_path))
    result = engine.recognize()
    print(f"{img_path.name}: {result.text[:50]}...")
```

---

## 完全な動作例

すべてをまとめると、以下のスクリプトを `ocr_demo.py` という名前で保存すればすぐに実行できます。

```python
#!/usr/bin/env python3
"""
ocr_demo.py – Recognize text from image using a generic OCR library.
"""

import ocr  # Replace with the actual OCR package you installed

def main():
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.high_accuracy = True          # set high accuracy mode
    engine.language = "eng"              # optional: specify language pack

    # Load image – change the path to your own file
    image_path = "YOUR_DIRECTORY/low-res.jpg"
    engine.image = ocr.Image.load_from_file(image_path)

    # Perform recognition
    result = engine.recognize()

    # Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

保存し、実行可能にして（`chmod +x ocr_demo.py`）、実行してください：

```bash
./ocr_demo.py
```

コンソールに **画像をテキストに変換** の結果が表示されます。

---

## 現場からのヒントとコツ

- 多数の画像を処理する場合は **エンジンをキャッシュ** してください。各ファイルごとに新しいインスタンスを作成すると実行時間が倍になることがあります。
- 組み込みの高精度モードだけでは不十分な場合は **自前で前処理** してください：OpenCVでノイズ除去（`cv2.fastNlMeansDenoisingColored`）や二値化（`cv2.threshold`）を使用します。
- 自動で低品質結果を除外したい場合は **信頼度をログ**（`result.confidence`）してください。
- パスをハードコーディングしないでください；クロスプラットフォーム互換性のために `pathlib.Path` を使用します。

---

## 結論

私たちは、**画像からテキストを認識** するシンプルな Python ワークフローを実装しました：**画像をOCR用にロード**、**高精度モードを設定**、**OCR認識を実行**、そして最終的に **画像をテキストに変換**。全体のパイプラインは20行未満で収まり、バッチ処理や多言語文書、ノイズが多い入力にも柔軟に対応できます。

次のチャレンジは準備できましたか？ 汎用 `ocr` ライブラリを `pytesseract` や `easyocr` に置き換えてみたり、追加の前処理ステップを試したり、Flask API に組み込んでウェブページから画像をアップロードしリアルタイムで文字起こしを返すようにしたりしてください。

質問やクールなユースケースがあればコメントで教えてください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [画像からテキストを抽出する（Aspose OCR） – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR画像認識でしきい値を設定する方法](/ocr/english/net/ocr-settings/set-threshold-value/)
- [画像をURLから取得してOCRを実行 – 画像をテキストに変換](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}