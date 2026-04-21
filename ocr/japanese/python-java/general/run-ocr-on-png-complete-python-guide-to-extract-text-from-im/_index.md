---
category: general
date: 2026-01-12
description: PythonでPNGファイルのOCRを高速に実行しましょう。画像や請求書からテキストを抽出する方法と、Aspose.OCRを使用して画像をOCRにロードする方法を学びます。
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: ja
og_description: PNGでOCRを即座に実行します。このガイドでは、画像や請求書からテキストを抽出し、OCR用に画像を読み込み、結果をJSONおよびCSVとして保存する方法を示します。
og_title: PNGでOCRを実行する – 完全なPythonチュートリアル
tags:
- OCR
- Python
- Image Processing
title: PNGでOCRを実行 – 画像からテキストを抽出する完全なPythonガイド
url: /ja/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGでOCRを実行 – 画像からテキストを抽出する完全Pythonガイド

PNGファイルで **OCRを実行** したいけど、どのライブラリがきれいで構造化された結果を出すか分からないことはありませんか？実際のプロジェクト—たとえば請求書の自動化やレシートのスキャン—では、最初のステップは **画像からテキストを抽出** することです。PNGはロスレス品質を保つため、よく使われるフォーマットです。

このチュートリアルでは、Aspose.OCR Python パッケージを使ったハンズオン例を順に解説します。ガイドの最後まで読むと、**OCR用に画像をロード** し、すべてのテキスト行を取得し、そのデータを整った JSON オブジェクトに変換し、さらに CSV にダンプして下流処理に利用できるようになります。余計な説明は省き、実用的でそのまま実行可能なソリューションをご提供します。

## 学べること

- Aspose.OCR ライブラリのインストールとインポート方法。  
- **PNGでOCRを実行** し、結果オブジェクトを扱う正確な手順。  
- **請求書からテキストを抽出** し、出力を JSON または CSV 形式に整形する方法。  
- 低コントラスト画像、多言語文書、信頼度スコアへの対処法。  
- 今日から実行できる、コピー＆ペースト可能な完全コードサンプル。

> **前提条件:** Python 3.8+ と pip の基本的な知識。Aspose を使ったことがなくても大丈夫です—このガイドですべてカバーします。

---

## Step 1 – Install Aspose.OCR and Prepare Your Environment

**PNGでOCRを実行** できるように、まずライブラリをシステムにインストールします。

```bash
pip install aspose-ocr
```

> **プロのコツ:** 仮想環境 (`python -m venv venv`) を使って依存関係を分離しましょう。複数プロジェクトを扱う際のバージョン衝突を防げます。

インストールが完了したら、必要なモジュールをインポートします。

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

ここでは、重い処理を担う `asposeocr` と、後でシリアライズに使う組み込みの `json` ライブラリを読み込みます。

---

## Step 2 – Create the OCR Engine and Set the Language

OCR エンジンは実際にピクセルを読み取るコアコンポーネントです。英語の請求書が多い場合は、英語言語パックを指定します。

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **なぜ重要か:** 言語を指定すると文字セットが絞られ、精度が向上し処理速度も速くなります。多言語の請求書に対応したい場合は、`ocr.Language.ENGLISH` を適切な enum に置き換えるだけです。

---

## Step 3 – Load the Image for OCR

次に **OCR用に画像をロード** します。`Image.load` メソッドはファイルパスを受け取り、PNG、JPEG、BMP などに対応しています。

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **エッジケース:** PNG が非常に大きい（5 MB 超）場合は、メモリ使用量を抑えるために先にリサイズすると良いでしょう。Pillow ならワンラインで可能です。

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Step 4 – Run OCR on PNG and Capture the Result

エンジンの準備と画像のロードが完了したら、**PNGでOCRを実行** し、構造化された結果を取得します。

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` オブジェクトは `OcrRegion` アイテムのコレクションを保持しており、認識されたテキストと信頼度スコア（0‑100）を含みます。ここで **請求書からテキストを抽出** するために必要な細かいデータが得られます。

---

## Step 5 – Convert the Result to JSON and Pretty‑Print It

多くの下流システムは JSON を好むため、OCR 出力を整形された文字列に変換します。

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### サンプル出力

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

各行に信頼度メトリックが含まれているのが分かります—**請求書からテキストを抽出** を自動化する際に、低信頼度エントリを除外するのに最適です。

---

## Step 6 – Save the OCR Data as CSV (One Line per Text + Confidence)

CSV はスプレッドシートや簡易データインポートに最適です。Aspose はすべてを CSV ファイルに書き出すワンライナーを提供しています。

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

生成される CSV は次のようになります:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

これで Excel、Google Sheets、あるいはデータベースにインポートできます。

---

## Bonus – Handling Low‑Confidence Text and Multi‑Page PDFs

### 信頼度でフィルタリング

高信頼度の行だけが欲しい場合は、JSON を書き出す前にフィルタリングします:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### マルチページ文書

Aspose.OCR はマルチページ PNG や PDF の各ページに自動で `page` エントリを作成します。`ocr_data["pages"]` をループすれば、追加コードなしで全ページを処理できます。

---

## Full Working Example

以下は **完全なスクリプト** です。コピーして貼り付け、すぐに実行できます。`YOUR_DIRECTORY` を PNG ファイルが格納されているフォルダに置き換えてください。

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

`python run_ocr.py` でスクリプトを実行すると、コンソールに JSON ダンプが表示され、ディスクに CSV ファイルが生成され、さらに高信頼度エントリのフィルタ済みリストが得られます。

---

## Frequently Asked Questions

**Q: 請求書ではなくスキャンしたレシートからテキストを抽出したい場合はどうすればいいですか？**  
A: 全く同じワークフローが使えます—`image_path` をレシートの PNG に指すだけです。レシートが別言語の場合は、`engine.language` を適切に切り替えてください。

**Q: PNG に回転したテキストが含まれている場合は？**  
A: Aspose.OCR は自動で向きを検出しますが、頑固なケースでは Pillow で手動回転させてからエンジンに渡すことも可能です。

**Q: Aspose.OCR の利用には有料ライセンスが必要ですか？**  
A: ライブラリは出力に透かしが入る無料評価モードを提供しています。本番環境で使用する場合は、Aspose のウェブサイトからライセンスを取得する必要があります。

---

## Conclusion

Python で **PNGでOCRを実行** するために必要なすべての手順を網羅しました：SDK のインストール、画像のロード、構造化テキストの抽出、JSON または CSV への保存。シンプルなスクリプトで **画像からテキストを抽出** したい場合でも、**請求書からテキストを抽出** して自動会計パイプラインを構築したい場合でも、上記の手順は堅牢なプロダクションベースの基盤を提供します。

次に試すべきこと:

- CSV 出力をデータベースに統合し、請求書を一括保存。  
- 正規表現で日付、金額、税番号などを抽出するポストプロセッシングを追加。  
- 請求書に QR コードが含まれる場合は、`ocr_engine.recognize_barcode` 機能を活用。

ぜひ試してみて、信頼度閾値を調整し、ドキュメント処理ワークフローがどれだけ楽になるか体感してください。質問や面白いユースケースがあればコメントで教えてください—Happy OCRing!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – OCR結果のビジュアル例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}