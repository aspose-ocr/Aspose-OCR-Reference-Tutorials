---
category: general
date: 2026-06-28
description: Python OCR を使用してテキスト画像を認識し、テキスト PNG ファイルを抽出し、堅牢なエラーハンドリングで認識されたテキストを出力する方法を学びましょう。
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: ja
og_description: Pythonでテキスト画像を認識し、テキストPNGを抽出し、認識したテキストを安全に出力するステップバイステップチュートリアル。
og_title: Python OCRでテキスト画像を認識する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python OCRでテキスト画像を認識する – 完全ガイド
url: /ja/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR でテキスト画像を認識する – 完全ガイド

重いフレームワークを導入せずに、**テキスト画像**を Python スクリプトで認識したいと思ったことはありませんか？同じ悩みを持つ開発者は多いです。スクリーンショットやスキャンしたレシート、シンプルな PNG を読み込み、テキストを取得したいというニーズです。  

このチュートリアルでは、最小限の OCR エンジンを組み立て、カスタムロガーを添付し、**load image OCR** を実行し、**process image OCR** を走らせ、最後に**print recognized text** します。最後まで読めば、オンデマンドで **extract text png** ファイルを抽出できる自己完結型スクリプトが手に入ります。

## 学べること

- OCR エンジンを作成し、すべてのステップをログに記録し、失敗を優雅に処理する完全動作の Python スニペット。  
- 各行が **なぜ** 必要なのかを明確に解説 – Tesseract、EasyOCR、その他のバックエンドへも簡単に適応可能。  
- よくある落とし穴（フォント欠如、破損した PNG）への対処法とデバッグ手順。  

### 前提条件

- Python 3.8+ がインストール済み  
- `OcrEngine` クラスを提供する OCR ライブラリ（例では架空の API を使用していますが、`pytesseract`、`easyocr` などに置き換えてください）。  
- 解析したい PNG 画像を `input.png` という名前で、管理できるフォルダーに保存しておくこと。  

> **Pro tip:** `pytesseract` を使用する場合は、まずシステムに Tesseract バイナリをインストール（Linux なら `sudo apt install tesseract-ocr`）し、続いて `pip install pytesseract pillow` を実行してください。

---

## ## Recognize Text Image: Setting Up the Logger

良いロガーは OCR パイプラインの隠れた英雄です。エンジンが開始した時点、開いたファイル、失敗した理由をすべて教えてくれます。

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Why this matters:*  
ロガーは診断出力を OCR コアから切り離すため、後でファイルやモニタリングサービス、あるいは UI へ簡単にリダイレクトできます。  

---

## ## Load Image OCR: Feeding the Engine a PNG

エンジンが **process image OCR** を実行できるようになる前に、適切な画像オブジェクトが必要です。ほとんどのライブラリは Pillow の `Image` インスタンスを受け取ります。

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Key points:*  

- **load image ocr** – `Image.from_file` が PNG デコードの詳細を抽象化します。  
- パスは設定可能にしておくこと；ハードコーディングはスクリプトを脆弱にします。  
- ロガー呼び出しで画像が正常に読み込まれたことを確認でき、ファイルが欠損または破損している場合に有用です。

---

## ## Process Image OCR: Recognizing the Text

いよいよ本格的な処理が始まります。エンジンはビットマップを走査し、ニューラルネットやヒューリスティックを適用して Unicode 文字列を出力します。

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Why we wrap it in `try/except`:*  
OCR は低解像度 PNG、未対応のカラースペース、言語データ欠如などで例外を投げやすいです。`OcrException` を捕捉すれば、**print recognized text** を実際にテキストが存在する場合にのみ実行でき、エンドユーザーに不明瞭なスタックトレースが表示されるのを防げます。

---

## ## Print Recognized Text & Extract Text PNG

認識が成功したら結果を表示し、必要に応じて元の PNG 名に対応した `.txt` ファイルへ書き出します。

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*What you get:*  

- **print recognized text** – ターミナルに即時のビジュアルフィードバックを提供。  
- 元画像と同名の `.txt` ファイルが生成され、実質的に **extract text png** して下流処理（検索インデックス、データ入力など）に利用可能。

---

## ## Common Edge Cases & How to Tackle Them

| 状況 | 症状 | 対処法 |
|-----------|---------|-----|
| PNG がグレースケールのみ | OCR が空文字列を返す | エンジンに渡す前に `Image.convert("RGB")` で RGB に変換 |
| 言語が未対応 | `OcrException` がコード `LANG_NOT_FOUND` を返す | 言語パックをインストール（例：フランス語なら `tesseract‑lang‑fra`）し、`ocr_engine.language = "fra"` を設定 |
| 画像が非常に大きい（> 5 MB） | 認識が遅い、またはメモリエラー | `image.thumbnail((2000, 2000))` でダウンサンプルしてから `set_image` |
| 予期しない文字が出力される | 文字化け | 本当に PNG か確認。JPEG などを装った PNG があるので、`Image.verify()` で検証 |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**期待されるコンソール出力（正常系）:**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

何か問題が起きた場合は、カスタムロガーのおかげで理由が明示された `[ERROR]` 行が表示されます。

---

## ## Next Steps & Related Topics

- バッチで **extract text png** する場合は、ディレクトリツリーを走査する `for` ループでスクリプトをラップ。  
- OpenCV を使って前処理（デスキュー、コントラスト強化）を行い、**process image ocr** の精度を向上。  
- `OcrEngine` 実装をクラウド OCR サービス（Google Vision、Azure Read）に差し替えても、周辺コードはそのまま。  
- `reportlab` を使って **print recognized text** を PDF に埋め込み、レポート自動生成を実現。  

---

## Conclusion

Python で **recognize text image** を行う、コンパクトかつ本番環境でも使える手順を一通り解説しました。PNG の読み込みから **print recognized text**、結果の保存まで、ミニロガーの導入、例外処理、出力の永続化を組み込むことで、クイック実験から大規模パイプラインへの統合まで対応可能です。  

自分のスクリーンショットで試し、画像前処理をいじってみれば、どんな PNG からでもテキストを抽出できるようになります。質問があればコメントでどうぞ—Happy OCRing!  

![recognize text image example](placeholder.png)


## What Should You Learn Next?


以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}