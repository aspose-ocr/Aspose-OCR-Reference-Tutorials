---
category: general
date: 2026-06-25
description: Python OCR を使用して画像からテキストを抽出します。OCR 用に画像を読み込む方法、Python で OCR を実行する方法、そして領収書を
  JSON に変換する方法を、簡単な手順で学びましょう。
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: ja
og_description: Python OCR を使用して画像からテキストを抽出します。このチュートリアルでは、OCR 用に画像を読み込む方法、Python
  で OCR を実行する方法、そして領収書を JSON に変換する方法を順を追って説明します。
og_title: Pythonで画像からテキストを抽出する – 完全OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Pythonで画像からテキストを抽出する – 完全OCRガイド
url: /ja/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像からテキストを抽出 – 完全OCRガイド

画像からテキストを**抽出**したいと思ったことはありますか？でもどこから始めればいいか分からない…このチュートリアルでは、**OCR用に画像をロード**し、**PythonでOCRを実行**し、**レシートをJSONに変換**する方法を、ほんの数行のコードでご紹介します。

レシートスキャンアプリや経費トラッカーを作ったことがある方、またはデータ入力を自動化したい方は、このフローをマスターすることでどれだけ便利になるか実感できるはずです。最後まで読めば、レシートの画像を読み取り、下流サービスで使えるクリーンなJSONペイロードを出力する動作スクリプトが手に入ります。

## 学べること

`aocr` ライブラリのインストールから生データの処理まで、すべてのステップをカバーします。具体的には以下を学びます：

1. **OCRエンジンインスタンスの作成** – 認識処理のエントリーポイント。  
2. **OCR用に画像をロード** – エンジンにどのファイルを読み込むか指示。  
3. **エクスポート形式の選択** – JSON または XML。ここでは扱いやすい JSON を選択。  
4. **認識の実行** – Pythonで実際に OCR を行う。  
5. **結果の出力または保存** – レシートを JSON に変換し、出力を確認。

OCR の事前知識は不要です。基本的な Python 環境と画像ファイル（レシート、チラシなど）さえあれば始められます。

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="Python OCRを使用した画像からテキスト抽出のフロー"}

## 画像からテキスト抽出 – ステップバイステップ Python OCR

以下に、完全に実行可能なスクリプトを示します。`receipt_ocr.py` というファイルにコピー＆ペーストし、`python receipt_ocr.py` を実行してください。

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### なぜこれが機能するのか

- **Engine instance** – `aocr.OcrEngine()` は、モデルのロードや前処理など、重い処理をすべてカプセル化します。  
- **Loading the image** – `engine.load_image()` は、ライブラリに解析すべきビットマップを正確に指示します。JPEG、PNG、さらにはマルチページ PDF も入力可能です。  
- **Export format** – `engine.export_format` を `aocr.ExportFormat.JSON` に設定すると、結果は構造化された文字列となり、JSON を期待する API に最適です。  
- **Recognition call** – `engine.recognize()` は、裏でニューラルネットの推論を実行し、検出されたテキストブロック、信頼度スコア、レイアウト情報を含む JSON 文字列を返します。

---

## aocrでOCR用に画像をロード

画像に特別な前処理が必要か気になるかもしれませんが、簡単に言えば **不要**です。`aocr` はコントラスト調整や傾き補正など、一般的なケースを自動で処理します。ただし、精度を上げるために以下を行うと効果的です：

- 画像の解像度が最低でも 300 dpi であることを確認。  
- 不要な余白をトリミング。  
- グレースケールに変換してから入力（任意、`engine.load_image()` が自動で行います）。

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*プロチップ:* レシートにノイズが多い場合、上記の追加ステップで **PythonでOCRを実行** の精度がかなり向上します。

---

## エクスポート形式を選択し、レシートをJSONに変換

「なぜプレーンテキストだけじゃだめなのか？」と疑問に思うかもしれません。JSON は階層構造（行、単語、バウンディングボックス）を保持するため、後で *合計金額* や *日付* といったフィールドをマッピングしやすくなります。

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

スクリプトを実行すると、`json_result` は以下のような形になります（簡略化しています）：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

これで **レシートをJSONに変換** したペイロードが得られ、データベースや REST エンドポイント、機械学習モデルに直接渡すことができます。

---

## 認識を実行し結果を取得

最終ステップ—実際に OCR を実行する—は `recognize()` を呼び出すだけです。ライブラリは内部で以下を行います：

1. 画像を事前学習済みの畳み込みネットワークに通す。  
2. ネットワーク出力を可読文字にデコード。  
3. すべてを選択した形式（今回は JSON）にパッケージ化。

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

出力を画面に表示する代わりに保存したい場合は、ファイルに書き込むだけです：

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*エッジケース:* 一部のレシートには非 ASCII 文字（例: “€”）が含まれます。上記のように UTF‑8 エンコーディングでファイルを開き、文字化けを防いでください。

---

## 完全動作例（すべてのステップを1つのスクリプトに統合）

すべてを統合した最終スクリプトを以下に示します。これでエンドツーエンドに実行できます：

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

以下のコマンドで実行します：

```bash
python receipt_ocr.py
```

実行すると確認メッセージが表示され、同じフォルダに構造化データを含む `receipt_output.json` が生成されます。

---

## 結論

これで Python を使って **画像からテキストを抽出** する方法、**OCR用に画像をロード** する方法、**PythonでOCRを実行** する方法、そして **レシートをJSONに変換** して下流で利用する方法が分かりました。このエンドツーエンドのフローは軽量で、`aocr` パッケージだけで動作し、任意の自動化パイプラインに組み込むことができます。

次は何をすべきか？エクスポート形式を XML に変更したり、さまざまな画像前処理を試したり、アップロードされたレシートを受け取り即座に JSON ペイロードを返す小さな Flask API を作ってみましょう。基本が身につけば可能性は無限です。

質問や問題があれば、下のコメント欄に書き込んでください。楽しいコーディングを！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR を使用した画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [画像からテキスト抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET を使用して画像からテーブルを抽出する方法](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}