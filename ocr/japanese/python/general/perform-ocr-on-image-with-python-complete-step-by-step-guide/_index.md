---
category: general
date: 2026-07-05
description: Python を使って画像の OCR を実行します。画像をテキストに変換する方法、OCR 用に画像を読み込む方法、数分で画像からキリル文字テキストを抽出する方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: ja
og_description: Pythonで画像のOCRを実行します。このガイドでは、画像をテキストに変換する方法、OCR用に画像を読み込む方法、そして画像からキリル文字テキストを迅速に抽出する方法を示します。
og_title: Pythonで画像のOCRを行う – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Pythonで画像のOCRを実行する – 完全ステップバイステップガイド
url: /ja/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image with Python – Complete Step‑by‑Step Guide

画像ファイルから **OCR を実行** したいが、サードパーティのサービスに渡したくない、と思ったことはありませんか？ パスポートスキャナ、レシートのデジタル化、アーカイブツールなど、多くのプロジェクトで画像から生のテキストを取得することが最初のハードルです。  

このチュートリアルでは、実用的な例を通して **image to text python** スタイルの変換方法を解説し、**load image for OCR** の手順を示し、最後にオープンソースの `aocr` ライブラリを使って **extract Cyrillic text from image** を行います。最後まで読めば、任意の画像から **recognize Cyrillic text** できるようになります。

> **得られるもの:** 実行可能なスクリプト、各ステップの明確な説明、ぼやけたスキャンや予期しないフォントといった一般的な落とし穴への対処法。外部 API は不要、純粋な Python だけです。

---

## Prerequisites

始める前に以下を用意してください。

- Python 3.8 以上がインストールされていること。
- 使い慣れたターミナルまたはコマンドプロンプト。
- `aocr` パッケージ（`pip install aocr` でインストール可能）。
- キリル文字を含む画像ファイル（例: スキャンしたロシアのパスポート）。  

これらに心当たりがなくても安心してください。各項目は後ほど簡単に説明します。

---

## Step 1: Perform OCR on Image – Setting Up the Environment

まず最初に、OCR ライブラリを配置するクリーンな Python 環境を用意します。仮想環境を使うことで依存関係を分離し、バージョン衝突を防げます。

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Why?**  
専用の環境を作ることで `aocr` パッケージとそのネイティブバイナリが他のプロジェクトに影響しません。また、再現性が高くなり、他の開発者がリポジトリをクローンして同じ `pip install -r requirements.txt` を実行すれば同じ環境が構築できます。

> **Pro tip:** `pip freeze > requirements.txt` で依存関係を固定しておくと、使用した正確なバージョンが常に分かります。

---

## Step 2: Load Image for OCR – Importing and Preparing the File

ライブラリの準備ができたら、次は **load image for OCR** します。`aocr.Image.from_file` メソッドは PNG、JPEG、TIFF などの一般的なフォーマットを扱えます。使用例は以下の通りです。

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**What’s happening here?**  
`aocr.Image.from_file` はバイナリデータを読み込み、デコードして OCR エンジンが理解できるオブジェクトに格納します。ファイルが見つからない場合は Python が `FileNotFoundError` を送出し、後で例外処理で捕捉できます。

> **Edge case:** スキャナによってはマルチページ TIFF を出力します。その場合はページを分割する必要があります—`aocr` には `Image.from_tiff_pages()` が用意されています。

---

## Step 3: Configure the OCR Engine – Forcing Cyrillic Recognition

デフォルトでは多くの OCR エンジンが言語を自動推測しますが、ラテン文字以外では文字化けしやすくなります。**recognize Cyrillic text** を確実に行うため、言語を “cyrillic” に明示的に設定します。

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Why force the language?**  
キリル文字はラテン文字と形が似ている（例: “A” と “А”）ため、エンジンにキリル文字を期待させることで誤認識が大幅に減少します。特に低解像度のスキャンで効果的です。

---

## Step 4: Perform OCR on Image – Running the Recognition

画像がロードされ、エンジンが調整されたら、いよいよ **perform OCR on image** です。`recognize` メソッドは抽出されたテキストと信頼度スコアを含む `OcrResult` オブジェクトを返します。

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**What does `ocr_result` give you?**  
- `text`: 認識された文字列（プレーンテキスト）。  
- `confidence`: 0‑1 の範囲で全体的な確信度を示す浮動小数点数。  
- `lines`: 必要に応じて行単位でアクセスできるオブジェクトのリスト。  

> **Common question:** *テキストが逆さまだったら？*  
> `aocr` は自動回転機能を持っています。`recognize` を呼ぶ前に `ocr_engine.auto_rotate = True` を設定してください。

---

## Step 5: Convert Image to Text Python – Post‑Processing the Output

生の文字列には余分な空白や改行が混入していることがあります。**convert image to text python** スタイルに整えるため、簡単なクリーンアップ手順を実行します。

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Why bother?**  
クリーンな出力は、データベースへの保存、翻訳 API への送信、パスポート番号の正規表現検索など、下流のパイプラインにそのまま流し込めます。

---

## Step 6: Extract Cyrillic Text from Image – Putting It All Together

すべてをひとつの再利用可能な関数にまとめましょう。これで **extract Cyrillic text from image** がワンライナーで呼び出せます。

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Result you should see (sample):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

画像が鮮明でフォントが OCR モデルに合致していれば、ほぼ完璧な文字起こしが得られます。

---

## troubleshooting & Tips

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| 文字化け | 言語設定が間違っている | `ocr_engine.language = "cyrillic"` を確認 |
| 出力が空 | 画像が暗すぎる、または解像度が低い | `opencv` でコントラストを上げて前処理 |
| 向きが間違っている | 画像が 90° 回転している | `ocr_engine.auto_rotate = True` を設定 |
| 処理が遅い | 画像が大きすぎる ( >5 MP ) | 認識前に `aocr.Image.resize(width=1024)` でリサイズ |

---

![perform OCR on image example](ocr_example.png "perform OCR on image example")

*Alt text: 「パスポートスキャンからキリル文字を抽出する Python コードを示す OCR の実行例」*

---

## Conclusion

純粋な Python だけで **perform OCR on image** を実現し、**load image for OCR** の方法を学び、エンジンに **recognize Cyrillic text** を強制し、最終的に **extract Cyrillic text from image** を整然としたヘルパー関数で取得できました。`aocr` のインストールから結果のクリーンアップまで、数十行のコードで完結し、**convert image to text python** スタイルのパイプラインとして任意のプロジェクトに組み込めます。

---

## What’s Next?

- **バッチ処理:** フォルダ内のスキャン画像をループし、結果を SQLite に保存。  
- **言語検出:** `langdetect` と `aocr` を組み合わせて、キリル文字とラテン文字を自動切替。  
- **高度な前処理:** `opencv` を使ってデスキュー、ノイズ除去、二値化などを行い、精度を向上。  
- **FastAPI との統合:** `extract_cyrillic_text` 関数を REST エンドポイントとして公開し、Web アプリから利用可能に。

言語を “latin” に変えて英語パスポートを処理したり、別の OCR バックエンドに置き換えてみても構いません。概念は同じで、コードは柔軟に適応できます。

Happy coding, and may your images always be legible!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}