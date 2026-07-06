---
category: general
date: 2026-04-26
description: PythonでAspose OCRを使用して画像からテキストを抽出します。テキストの抽出方法、画像をテキストに変換する方法、OCR用に画像を読み込む方法を学び、多言語サポートが可能です。
draft: false
keywords:
- extract text from image
- how to extract text
- convert image to text
- load image for ocr
- multilingual ocr python
language: ja
og_description: 画像からテキストを即座に抽出します。このガイドでは、テキストの抽出、画像をテキストに変換、そしてPythonで Aspose OCR
  を使用して画像を OCR に読み込む方法を示します。
og_title: Pythonで画像からテキストを抽出 – 完全マルチリンガルOCRチュートリアル
tags:
- OCR
- Python
- Aspose
title: Pythonで画像からテキストを抽出 – 多言語OCRガイド
url: /ja/python-java/general/extract-text-from-image-with-python-multilingual-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像からテキストを抽出 – 多言語 OCR ガイド

画像からテキストを**抽出**したいと思ったことはありますか、しかし混合言語のページを扱えるライブラリが分からなかったことはありませんか？ あなたは一人ではありません。実際のアプリケーションでは、請求書処理、ソーシャルメディアモニタリング、または多言語文書のアーカイブなどを考えると、ラテン文字とキリル文字の両方を含む画像に出くわすことがあります。  

良いニュースがあります。Aspose OCR for Python を使えば、**テキストを抽出**、**画像をテキストに変換**、そして**OCR 用に画像をロード**を数行で行え、エンジンに言語を自動検出させることができます。このチュートリアルでは、完全に実行可能な例を順に解説し、各ステップの重要性を説明し、途中で遭遇する可能性のあるいくつかのエッジケースも取り上げます。  

> **得られるもの**  
> * 混合言語 PNG からテキストを取得する、すぐに実行できるスクリプト。  
> * Python で多言語 OCR を構成する方法の理解。  
> * 大きなファイル、異なる画像フォーマットの取り扱い、一般的な落とし穴のデバッグに関するヒント。  

## 前提条件

- Python 3.8 以上（コードは f‑strings を使用）。  
- `asposeocr` パッケージをインストール（`pip install asposeocr`）。  
- 複数のスクリプトでテキストが含まれる画像ファイル（例: `mixed_lang.png`）。  
- Python のインポートとオブジェクト指向 API に関する基本的な知識。  

重い依存関係も外部サービスも不要です。pip で一度インストールすればすぐに使えます。

---

## ステップ 1 – Aspose OCR ライブラリのインストールとインポート  

OCR 用に画像をロード**する前に、ライブラリ自体が必要です。パッケージにはコア OCR エンジンと軽量画像ローダーが同梱されています。  

```python
# Install the package (run once in your environment)
# pip install asposeocr

# Import the required classes
import asposeocr as aocr
from asposeocr import OcrEngine, OcrConfig, Language
```

*重要な理由*: 特定のクラスをインポートすることで名前空間が整理され、後続のコードが分かりやすくなります。`asposeocr` だけをインポートすると、すべての呼び出しを (`aocr.OcrEngine()`) のように修飾しなければならず、冗長になります。

---

## ステップ 2 – OCR エンジンの作成と多言語検出の有効化  

Aspose OCR は画像に含まれる言語を自動的に推測できます。`Language.AUTO` を設定すると、ラテン文字、キリル文字、アラビア文字など多数をカバーします。  

```python
# Initialize the OCR engine
ocr_engine = OcrEngine()

# Enable automatic language detection (covers Latin, Cyrillic, etc.)
ocr_engine.config.language = Language.AUTO
```

*プロのコツ*: 事前に言語が分かっている場合は、`Language.ENGLISH` や `Language.RUSSIAN` を指定するとわずかなパフォーマンス向上が得られます。ただし、実際に混合文書の場合は `AUTO` が最も安全です。

---

## ステップ 3 – 処理したい画像をロード  

ここで**OCR 用に画像をロード**します。Aspose は PNG、JPEG、BMP、TIFF、さらには画像として扱われる PDF ページもサポートします。  

```python
# Path to the image containing mixed‑language text
image_file_path = "YOUR_DIRECTORY/mixed_lang.png"

# Load the image into the OCR engine
ocr_engine.image = aocr.Image.load(image_file_path)
```

> **ヒント**: 画像が 2 MB を超える場合は、事前にリサイズすることを検討してください。大きな画像はメモリ使用量が増加し、検出ステップが遅くなる可能性があります。

---

## ステップ 4 – OCR プロセスを実行し、結果を取得  

`process()` を呼び出すと、テキスト検出、レイアウト解析、言語デコードという重い処理が行われます。  

```python
# Execute the OCR operation
ocr_result = ocr_engine.process()
```

返される `ocr_result` オブジェクトには、いくつかの便利なプロパティがあります：

| Property | Description |
|----------|-------------|
| `text`   | 認識されたテキストのプレーン文字列（最も頻繁に使用されます）。 |
| `confidence` | 全体の信頼度スコア（0‑100）。 |
| `lines`  | 位置データを持つ `OcrLine` オブジェクトのリスト（PDF に便利）。 |

---

## ステップ 5 – 抽出したテキストを表示  

最後に、出力をプリントします。実際のアプリケーションでは、データベースに書き込んだり、翻訳 API に渡したりすることがあります。  

```python
print("Recognized Text:")
print(ocr_result.text)
```

**期待される出力**（混合言語画像の例）:

```
Recognized Text:
Hello world!
Привет мир!
```

文字化けが見られる場合は、画像が破損していないか、最新バージョンの `asposeocr`（執筆時点では v23.7）を使用しているかを再確認してください。

---

## ステップ 6 – コピー＆ペーストできる完全なスクリプト  

すべてをまとめることで「コードはどこから始まるのか？」という混乱が解消されます。このファイルを `multilingual_ocr.py` として保存し、コマンドラインから実行してください。  

```python
# multilingual_ocr.py
# -------------------------------------------------
# Complete example: extract text from image (multilingual)
# -------------------------------------------------

import asposeocr as aocr
from asposeocr import OcrEngine, Language

def extract_text(image_path: str) -> str:
    """
    Loads an image, runs Aspose OCR with auto language detection,
    and returns the recognized text.
    """
    engine = OcrEngine()
    engine.config.language = Language.AUTO
    engine.image = aocr.Image.load(image_path)
    result = engine.process()
    return result.text

if __name__ == "__main__":
    # Adjust this path to point at your own image file
    img_path = "YOUR_DIRECTORY/mixed_lang.png"
    text = extract_text(img_path)
    print("Recognized Text:")
    print(text)
```

実行:

```bash
python multilingual_ocr.py
```

コンソールに抽出された文字列が表示されるはずです。これで完了です—**画像をテキストに変換**は数行で実現できます。

---

## よくある質問とエッジケースの対処  

### 画像に手書き文字が含まれている場合は？

Aspose OCR は印刷されたテキスト向けに調整されています。手書き文字は専用のモデル（例: Azure Read や Google Vision）が必要になることが多いです。`Language.AUTO` を試すことはできますが、信頼度は低くなることが予想されます。

### ノイズの多いスキャンで精度を上げるには？

1. 画像を前処理する（二値化、デスぺックリング）。  
2. エンジンに渡す前に DPI を少なくとも 300 ppi に上げる。  
3. 画像が傾いている場合は `ocr_engine.config.deskew = True` を明示的に設定する。

```python
ocr_engine.config.deskew = True
```

### PDF を画像に変換せずにテキストを抽出できますか？

はい、Aspose OCR は PDF ページを直接開くことができます：

```python
ocr_engine.image = aocr.Image.load("document.pdf", page_number=1)
```

ただし、各ページは内部的に画像として扱われるため、同じ品質上の考慮が必要です。

---

## 結論  

これで、Aspose OCR を使用した Python における **画像からテキストを抽出** するための、包括的で実用的なレシピが手に入りました。多言語サポートも完備しています。このスクリプトは **OCR 用に画像をロード**、**画像をテキストに変換**、そして最も一般的な落とし穴への対処方法を示しています。  

ここからは次のようなことが考えられます：

- ユーザーアップロードを受け付けるウェブサービスに機能を統合する。  
- 抽出したテキストを言語検出ライブラリと組み合わせて、適切な翻訳エンジンへルーティングする。  
- `ocr_engine.config` のオプション（例: `max_recognition_time`、`text_orientation`）を試して、パフォーマンスを微調整する。

コーディングを楽しんでください、そして OCR パイプラインが常に正確でありますように！  

---  

![抽出された多言語テキストのスクリーンショット – 画像からテキストを抽出する例](image-placeholder.png "画像からテキストを抽出する例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}