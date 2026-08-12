---
category: general
date: 2026-08-12
description: PythonでOCRを使用して画像からテキストを認識し、テキストを抽出し、画像をテキストに変換し、AIによるポストプロセッシングでOCRテキストをクリーンアップする方法
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: ja
lastmod: 2026-08-12
og_description: PythonでOCRを使用して画像を編集可能なテキストに変換する方法。画像からテキストを認識し抽出し、画像をテキストに変換し、AIでOCRテキストをクリーンアップする方法を学びましょう。
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: PythonでOCRを使用する方法 – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: PythonでOCRを使用する方法 – ステップバイステップガイド
url: /ja/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを使用する方法 – ステップバイステップガイド

スキャンしたドキュメントやスクリーンショットを編集可能なテキストに変換するために **how to use OCR** が必要な場合、このチュートリアルでは Python での完全なソリューションを示します。画像からテキストを認識し、画像からテキストを抽出し、画像をテキストに変換し、軽量な AI ポストプロセッサで OCR テキストをクリーンアップする方法を学びます。

このガイドでは、必要なライブラリのインストールから低品質画像の処理まで、すべてをカバーしています。そのため、どのステップが不足しているか推測することなく、OCR を任意の自動化パイプラインに統合できます。

## 作成するもの

この記事の最後までに、次のことができる単一の Python スクリプトが完成します：

1. 画像ファイル（PNG、JPEG、または TIFF）を読み込む。  
2. OCR エンジンを使用して画像からテキストを認識する。  
3. AI 駆動のポストプロセッサで生の出力を改善する。  
4. クリーンアップされたテキストをコンソールに出力する。

外部サービスは不要です—すべてローカルで実行されるため、オフライン環境やプライバシーに配慮したプロジェクトに適したソリューションです。

## 前提条件

- Python 3.9 以上。  
- `pytesseract` と `Pillow` ライブラリ（`pip install pytesseract pillow`）。  
- Tesseract‑OCR バイナリがインストールされ、システムの `PATH` で利用可能であること。  
- Python の関数に関する基本的な理解。

これらがすでに揃っている場合は、最初のコードブロックへすぐに進めます。

## PythonでOCRを使用する方法

**how to use OCR** の核心は OCR エンジンを初期化し、画像を渡すことです。このチュートリアルでは、オープンソースの Tesseract エンジンの薄いラッパーである `pytesseract` を使用します。

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **このステップが重要な理由** – Tesseract はクリーンで正しく向けられた画像を期待します。Pillow を使用することで OCR 実行前に画像データが正規化され、以降の **recognize text from image** 操作の精度が向上します。

## 画像からテキストを認識する

ここでは `pytesseract.image_to_string` を呼び出して生の文字列を抽出します。これは古典的な “recognize text from image” 呼び出しです。

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **関数を分離する理由** – OCR ステップを分離することで、後でエンジンを交換（例: EasyOCR に切り替え）してもパイプラインの他の部分に手を加える必要がなくなります。また、ユニットテストが容易になります。

## 画像からテキストを抽出し、品質を向上させる

生の OCR 出力には改行や余計な文字、誤認識された単語が含まれることがよくあります。AI ポストプロセッサはこれらのアーティファクトを自動的にクリーンアップできます。以下は `transformers` ライブラリを使用してローカルで小さな言語モデルを実行する最小限の例です。必要に応じて任意のプロプライエタリサービスに置き換えることも可能です。

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **AI ポストプロセッサが有効な理由** – 従来の OCR エンジンは文字認識に優れていますが、レイアウトやノイズには苦手です。言語モデルは文脈を理解できるため、“Th1s 1s 4 test.” を “This is a test.” に変換できます。このステップは **clean up OCR text** の要件に直接対応しています。

## 画像をテキストに変換 – 完全スクリプト

すべてを組み合わせると、エンドツーエンドで **convert image to text** を実現する短いスクリプトが得られます。

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### 期待される出力

サンプル画像（`sample.png`）でスクリプトを実行すると、次のような出力になる可能性があります：

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

AI ポストプロセッサが誤読された文字を修正し、余計な改行を削除したことに注目してください。この例は **extract text from image** の全体的なワークフローを示し、OCR テキストのクリーンアップの利点を示しています。

## 一般的なエッジケースの処理

| 状況 | 推奨される調整 |
|---|---|
| Low‑contrast image | OCR の前に `ImageEnhance` を使用してグレースケールに変換し、コントラストを上げる。 |
| Multi‑language document | `lang` にカンマ区切りのリストを渡す（例: `lang='eng+fra'`）。 |
| Very large images ( > 2000 px ) | `img.thumbnail((2000, 2000))` でダウンスケールし、Tesseract の速度を上げる。 |
| Missing Tesseract binary | `pytesseract.pytesseract.tesseract_cmd` が実行ファイルを指しているか確認する。 |
| AI post‑processor too slow | より小さなモデル（`t5-small`）を使用するか、GPU 上でポストプロセッサを実行する。 |

> **プロのコツ:** 示されているように、モジュールのインポート時に AI モデルオブジェクト（`_ai_postprocessor`）をキャッシュしておくと、呼び出しごとに再ロードする必要がなくなります。多数の画像を処理する際のレイテンシが大幅に削減されます。

## 代替アプローチ

- **EasyOCR**: 外部バイナリ不要で 80 以上の言語をサポートする純粋な Python OCR ライブラリです。pip のみで完結するソリューションが好みの場合は、`ocr_recognize` を `EasyOCR.Reader` に置き換えます。
- **Cloud OCR APIs**: Google Cloud Vision、Azure Computer Vision、Amazon Textract は、複雑なレイアウトに対して高精度を提供しますが、ネットワークアクセスと課金が必要です。
- **Custom post‑processing**: 決定的なクリーンアップのために、正規表現（`re.sub`）を使用して一般的なパターン（例: ハイフンで分割された改行の除去）を AI モデルなしで修正できます。

## まとめ

これで、Python で **how to use OCR** を使用して画像からテキストを認識し、画像からテキストを抽出し、画像をテキストに変換し、AI ポストプロセッサで OCR テキストをクリーンアップする方法が分かりました。完全なスクリプトは、追加の前処理（ノイズ除去、デスキュー）や下流のアクション（データベースへの保存、検索インデックスへの投入）で拡張できる、実運用可能なパイプラインを示しています。

### 次のステップ

- 異なる AI モデル（例: `gpt‑2`、`flan‑ul2`）を試して、ドメインに最適なクリーンアップが得られるものを見つける。  
- Flask や FastAPI を使用してパイプラインをウェブサービスに統合し、スクリプトをオンデマンド OCR エンドポイントに変える。  
- バッチ処理を検討する：画像ディレクトリをループし、各クリーンアップされた出力を対応する `.txt` ファイルに書き込む。

コードを自分のワークフローに合わせて自由に調整し、クリーンで検索可能なテキストでアプリケーションの次の段階を強化してください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [画像をテキストに変換: Aspose OCR（Python）を使用した画像からテキスト抽出](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Aspose OCR で画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキスト抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}