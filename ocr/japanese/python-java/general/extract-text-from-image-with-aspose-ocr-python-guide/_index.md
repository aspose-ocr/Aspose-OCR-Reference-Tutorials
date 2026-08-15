---
category: general
date: 2026-03-28
description: Aspose OCR を使用して Python で画像からテキストを抽出 – PNG からテキストを認識する方法、画像をテキストに変換する
  Python の手順、そして OCR 用に画像をすばやく読み込む方法を学びましょう。
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to text python
- load image for ocr
- read text from scanned image
language: ja
og_description: Aspose OCR を使用して Python で画像からテキストを抽出します。このチュートリアルでは、PNG からテキストを認識する方法、画像をテキストに変換する
  Python の手順、そして OCR 用に画像を読み込む方法を示します。
og_title: Aspose OCRで画像からテキストを抽出する – Pythonガイド
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCR を使用した画像からのテキスト抽出 – Python ガイド
url: /ja/python-java/general/extract-text-from-image-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からテキスト抽出 – Python ガイド

PNG スキャンで信頼できる結果が得られるライブラリがどれか分からず、**画像からテキストを抽出**したいと思ったことはありませんか？同じ壁にぶつかる開発者は多いです。スキャンした PDF やレシートの写真を扱うときに特にそうです。朗報です！Aspose OCR for Python を使えば、PNG ファイルからテキストを認識し、Python 風に画像をテキストに変換し、数行のコードで OCR 用に画像を読み込むことができます。

このチュートリアルでは、Aspose OCR を使って **画像からテキストを抽出** する完全な実行可能サンプルを順を追って解説します。画像の読み込み、言語自動検出の有効化、OCR エンジンの実行、検出された言語と抽出テキストの取得方法を示します。最後まで読めば、スキャン画像からテキストを読み取る必要がある任意のプロジェクトにこのコードをそのまま組み込めます。

## 学べること

- Aspose Storage を使って **OCR 用に画像を読み込む** 方法  
- PNG から **テキストを認識** し、言語を自動検出する方法  
- 低レベルのバイトバッファを扱わずに **Python で画像をテキストに変換** する方法  
- マルチページ PDF の取り扱い、よくある落とし穴、エッジケースへの対処法  
- 期待される出力例と、抽出が成功したかをすばやく確認する方法  

### 前提条件

- Python 3.8 以上がインストールされていること  
- Aspose OCR for Python のライセンス（または無料トライアルキー）—Aspose のウェブサイトから取得できます  
- `aspose-ocr` と `aspose-storage` パッケージを `pip install aspose-ocr aspose-storage` でインストール済みであること  
- 処理したい PNG もしくは他のサポート対象画像ファイル  

それでは、始めましょう。

## Step 1: Load image for OCR

OCR エンジンが何かをする前に、画像オブジェクトが必要です。Aspose Storage を使えばこの手順はとても簡単です。

```python
# Step 1: Import required Aspose modules
import aspose.ocr as aocr
import aspose.storage as storage

# Step 1.1: Define the path to your image file
input_image_path = "YOUR_DIRECTORY/input_image.png"

# Step 1.2: Load the image – Aspose supports PNG, JPEG, BMP, TIFF, etc.
# The Image class abstracts away file‑system handling.
image = storage.Image.load(input_image_path)
```

*ポイント:* `storage.Image.load` を使うとフォーマット固有の癖を意識せずに済み、**png からテキストを認識** したり JPEG を扱ったりできます。ファイルが見つからない場合は Aspose が明確な `FileNotFoundError` を投げるので、例外処理で優雅にフォールバックできます。

> **プロのコツ:** パフォーマンスを最大化するため、画像は 5 MB 以下に抑えてください。大きいファイルは OCR 前に `image.resize()` でダウンサンプリングすると良いでしょう。

## Step 2: Initialise the OCR engine and enable language detection

Aspose OCR には、テキストの言語を自動検出できる強力な `OcrEngine` が同梱されています。これを有効にすると、多言語ドキュメントの認識精度が向上します。

```python
# Step 2: Initialise the OCR engine
ocr_engine = aocr.OcrEngine()

# Step 2.1: Enable automatic language detection (AUTO mode)
ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO
```

*ポイント:* **Python で画像をテキストに変換** する際、言語は文字セットや辞書に影響するため重要です。AUTO モードにするとエンジンが最適な言語を自動で選択します（英語、スペイン語、中文など）。

## Step 3: Recognize text from PNG and extract the result

いよいよ本番です。`recognize` メソッドが OCR パイプラインを実行し、リッチな結果オブジェクトを返します。

```python
# Step 3: Run OCR on the loaded image
ocr_result = ocr_engine.recognize(image)

# Step 3.1: Pull out the detected language and the plain text
detected_lang = ocr_result.detected_language
extracted_text = ocr_result.text
```

文字列だけが欲しい場合は `ocr_result.text` をそのまま使えます。`detected_language` プロパティは ISO‑639‑1 コード（例: 英語なら `"en"`）を返します。

> **エッジケース:** 画像が極端に劣化していると空文字列が返ることがあります。その場合は Pillow などでコントラストを上げたりデスキューしたりして前処理を行ってから Aspose に渡してください。

## Step 4: Display the outcome – what to expect

結果を出力して、正しく動作したか確認しましょう。

```python
# Step 4: Show the detection results
print(f"Detected language: {detected_lang}")
print("Extracted text:")
print(extracted_text)
```

### サンプル出力

```
Detected language: en
Extracted text:
Invoice #12345
Date: 2026‑03‑01
Total: $1,250.00
Thank you for your business!
```

このような出力が見られたら、**画像からテキストを抽出** に成功です！出力が文字化けしている場合は、画像品質（印刷文字なら最低 300 dpi）を再確認してください。

## Step 5: Advanced tips – handling multi‑page PDFs and scanned docs

基本フローは単一 PNG で動作しますが、実務ではマルチページ PDF や TIFF スタックを扱うことが多いです。

1. **PDF ページを画像に変換** – Aspose PDF で各ページを PNG にレンダリングし、OCR ループに渡す  
2. **バッチ処理** – スキャン画像が入ったディレクトリを走査し、結果をリストに蓄積するか CSV に書き出す  
3. **カスタム言語指定** – 文書が常にフランス語であることが分かっている場合は `ocr_engine.language_detection = aocr.LanguageDetectionMode.FRENCH` と設定すると速度が向上します  

```python
# Example: Batch processing a folder of PNGs
import os

folder = "scans/"
texts = []
for file_name in os.listdir(folder):
    if file_name.lower().endswith(".png"):
        img = storage.Image.load(os.path.join(folder, file_name))
        result = ocr_engine.recognize(img)
        texts.append({"file": file_name,
                      "lang": result.detected_language,
                      "text": result.text})
```

結果は `json` や `pandas` で簡単にエクスポートできます。

## Step 6: Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Blank output | 画像の解像度が低すぎる、または過度に圧縮されている | 300 dpi 以上に拡大、Pillow でシャープ化 |
| Wrong language detection | ページ内に複数言語が混在している | `language_detection` を特定言語に手動設定、またはページごとに個別処理 |
| Memory error on large batches | 高解像度画像を多数同時に読み込んでいる | 画像を1枚ずつ処理し、各イテレーション後に `gc.collect()` を呼ぶ |
| Unexpected characters | OCR 辞書がフォントをサポートしていない | アラビア語やヒンディー語など複雑スクリプトを扱う場合は `ocr_engine.enable_complex_script` を有効化 |

## Full runnable script

以下のスクリプトを `extract_text.py` という名前で保存し、`YOUR_DIRECTORY/input_image.png` を実際の画像パスに置き換えてください。

```python
# extract_text.py
# Complete example: extract text from image with Aspose OCR (Python)

import aspose.ocr as aocr
import aspose.storage as storage

def main():
    # 1️⃣ Load the image
    input_image_path = "YOUR_DIRECTORY/input_image.png"
    try:
        image = storage.Image.load(input_image_path)
    except Exception as e:
        print(f"❗ Unable to load image: {e}")
        return

    # 2️⃣ Initialise OCR engine and enable auto language detection
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO

    # 3️⃣ Run OCR
    try:
        ocr_result = ocr_engine.recognize(image)
    except Exception as e:
        print(f"❗ OCR failed: {e}")
        return

    # 4️⃣ Output results
    print(f"Detected language: {ocr_result.detected_language}")
    print("Extracted text:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

実行方法:

```bash
python extract_text.py
```

コンソールに検出された言語と抽出テキストが順に表示されます。

## Conclusion

これで、Python で Aspose OCR を使って **画像からテキストを抽出** する方法がマスターできました。ファイルの読み込みから認識結果の表示まで、エンドツーエンドのフローが完成です。この手順で **png からテキストを認識** し、**Python で画像をテキストに変換** し、任意の自動化パイプラインに **OCR 用に画像を読み込む** 機能を組み込めます。

次のステップは？スキャンしたレシートをバッチ処理して CSV にエクスポートしたり、OCR ステップをドキュメント処理ワークフロー全体に統合したりしてみましょう（例: データベースへの自動入力）。さらに、Aspose PDF を使ってスキャン PDF を検索可能な文書に変換すれば、**スキャン画像からテキストを読む** というシナリオの自然な拡張になります。

コーディングを楽しんでください！言語設定や画像前処理のテクニック、あるいは Aspose OCR と Tesseract を組み合わせたハイブリッドアプローチなど、色々試してみてください。問題があればコメントで教えてください。一緒にトラブルシュートしましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}