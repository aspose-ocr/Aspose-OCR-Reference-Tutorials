---
category: general
date: 2026-06-25
description: シンプルでライセンスフリーのエンジンを使用し、テキストPNGファイルの抽出、テキスト画像の読み取り、画像テキストの認識方法を示すPython
  OCRチュートリアル。
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: ja
og_description: Python OCR チュートリアルでは、OCR 用に画像を読み込み、テキスト PNG ファイルを抽出し、数行のコードだけで画像のテキストを認識する方法を教えます。
og_title: Python OCRチュートリアル – PNGからテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: Python OCRチュートリアル：PNG画像からテキストを抽出する
url: /ja/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR チュートリアル – PNG 画像からテキストを抽出

レシートのスクリーンショットを編集可能なテキストに変換できる **python ocr tutorial** があるとしたら、考えたことはありませんか？ あなたは一人ではありません。実際のプロジェクトでは、*read text image* ファイルを素早く読み取る必要があり、毎回 GUI からコピー＆ペーストするより自分で行う方が便利です。  

このガイドでは、**extracts text PNG** ファイルのハンズオン例を順に解説し、*load image for OCR* の方法を示し、最後に *recognize image text* の結果を出力します――すべて無料の評価版 OCR エンジンを使用します。ライセンスキーも重い依存関係も不要で、純粋な Python と数個の小さなパッケージだけです。

## What You’ll Learn

- 軽量 OCR ライブラリのインストールとインポート方法。
- **load image for OCR** の正確な手順とよくある落とし穴の対処法。
- 品質がさまざまな *read text image* ファイルの読み取り方法。
- **extract text png** ファイルの精度を向上させるコツ。
- 認識した文字列を表示し、必要に応じてディスクに書き出す方法。

このチュートリアルの最後までに、**recognize image text** をオンザフライで実行できる再利用可能なスクリプトが手に入ります。魔法ではなく、明快なコードと解説だけです。

### Prerequisites

- Python 3.8 以上（ライブラリは 3.7+ でも動作しますが、3.8+ 推奨）。
- pip と仮想環境の基本的な知識。
- `sample.png` という名前の画像ファイル（テストしたい任意の PNG）を参照できるフォルダーに保存しておくこと。

これらに心当たりがない場合は、少し時間を取って環境を整えてください――その価値は必ずあります。

---

## Python OCR Tutorial – Setting Up the Engine

まず最初に OCR エンジンオブジェクトが必要です。今回使用するライブラリは、評価版としてすぐに使えるネイティブ OCR エンジンの小さなラッパーです。ライセンスキーが不要なので、*python ocr tutorial* に最適です。

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Why this matters:** エンジンを作成することで OCR ランタイムを他のコードから分離でき、重いリソースを毎回再初期化することなく複数画像で再利用できます。

---

## Load Image for OCR – Reading a PNG File

エンジンが用意できたら、次は *load image for OCR* を行います。ライブラリの `Image.load` メソッドはパスを受け取り、PNG、JPEG、BMP などを自動でデコードします。

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tip:** PNG にアルファチャンネルが含まれている場合、ライブラリは自動で除去します。ただし、*read text image* タスクで最高の結果を得るには画像をグレースケールにしておくと、ノイズが減り認識速度も向上します。

---

## Recognize Image Text – Running the OCR Engine

画像オブジェクトが準備できたら、いよいよ **recognize image text** を実行します。これが *python ocr tutorial* の核心で、たった一行のコードで完了します。

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**What happens under the hood?** エンジンは一連の前処理フィルタ（デスキュー、二値化）を適用した後、何百万もの文字で学習したニューラルネットワークにビットマップを渡します。そのため、低解像度の PNG でも驚くほど正確な出力が得られることが多いです。

---

## Display and Save the Extracted Text

結果が得られたら、表示したり保存したりしたくなるでしょう。`result` オブジェクトはプレーンテキストを保持する `text` 属性を公開しています。

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Expected output** (assuming `sample.png` contains “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

文字化けした場合は、次のセクションで一般的な対策を確認してください。

---

## Handling Common Issues When You Extract Text PNG

最高の OCR エンジンでも特定の画像では失敗します。以下は典型的な障壁とその克服方法です。

### 1. Low Contrast or Dark Backgrounds

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Skewed Text Lines

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Non‑English Characters

PNG にアクセント付き文字や非ラテン文字が含まれる場合は、適切な言語パックでエンジンを初期化してください。

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Very Large Images

4000×3000 の PNG を処理すると遅くなることがあります。可読性を保ちつつダウンサンプルしましょう。

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

これらの調整は、ハッピーパス以外でも機能する堅牢な *python ocr tutorial* の一部です。

---

## Full Script – One‑File Solution

以下は、これまで説明したすべての手順とオプション改善を組み込んだ、実行可能な単一ファイルスクリプトです。`ocr_extract.py` にコピー＆ペーストし、`python ocr_extract.py` を実行してください。

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Run it:**  
```bash
python ocr_extract.py ./sample.png
```

認識された文字列がコンソールに表示され、画像と同じディレクトリに `sample_extracted.txt` が作成されます。

---

## Visual Overview

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Python OCR チュートリアルの図で、OCR 用に画像をロードしてからテキスト PNG を抽出するまでのフローを示しています。*

この図は **load image for OCR** → **recognize image text** → **extract text PNG** の直線的な流れを示し、前処理ステップを挿入できるポイントをハイライトしています。

---

## Conclusion

今回、**python ocr tutorial** を通じて *load image for OCR*、*recognize image text*、そして **extract text png** ファイルを数行の Python コマンドだけで実現する方法を学びました。スクリプトは完全に動作し、一般的なエッジケースに対応し、バッチ処理や多言語サポートへ拡張可能です。

次のステップに挑戦したいですか？ PDF を画像に変換してエンジンに渡す、別の言語パックで実験する、あるいは Flask API に組み込んでアップロードされたスクリーンショットをリアルタイムで読み取るなど、*read text image* の自動化は実質的に無限の可能性があります。

質問や解決できない画像があれば、下のコメント欄で教えてください。一緒にトラブルシュートしましょう。Happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}