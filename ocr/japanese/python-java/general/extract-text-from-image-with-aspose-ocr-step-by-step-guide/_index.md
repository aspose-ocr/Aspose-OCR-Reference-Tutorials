---
category: general
date: 2026-05-03
description: Aspose OCR を使用して画像からテキストを瞬時に抽出します。関心領域の定義方法、OCR 用に画像を読み込む手順、そして数分で請求書からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- extract text from image
- define region of interest
- load image for ocr
- extract text from invoice
- process image with ocr
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出します。このガイドでは、関心領域の定義、OCR 用の画像の読み込み、そして請求書からのテキスト抽出を効率的に行う方法を示します。
og_title: Aspose OCRで画像からテキストを抽出する – 完全チュートリアル
tags:
- ocr
- python
- image-processing
title: Aspose OCRで画像からテキストを抽出する – ステップバイステップガイド
url: /ja/python-java/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド

画像からテキストを**迅速に抽出**したいですか？ あなたは一人ではありません—開発者は常にノイズの多いスキャン、領収書、請求書と格闘しています。このチュートリアルでは、*画像からテキストを抽出*する方法だけでなく、**関心領域（ROI）を定義**し、**OCR 用に画像をロード**し、請求書から必要な行を正確に取得する方法を示す完全なソリューションを順を追って説明します。

Aspose OCR ライブラリのインストールから、回転したページなどのエッジケースの処理まで、すべてカバーします。最後までに、手動でのトリミングは不要で、1 回の呼び出しで目的のテキストを抽出できる実行可能なスクリプトが手に入ります。

## 学習内容

- Aspose の Python API を使用して **OCR 用に画像をロード**する方法。  
- 重要な部分だけを処理できるように **関心領域（ROI）を定義**する最適な方法。  
- ページ全体を取得せずに **請求書からテキストを抽出**する方法。  
- **OCR で画像を処理**する際の効率的なヒントと一般的な落とし穴の回避策。  

**前提条件** – 最近の Python 3.9+ 環境、正当な Aspose OCR ライセンスファイル、そして画像（例: 請求書 PNG）。他の外部ツールは必要ありません。

---

## ステップ 1 – OCR エンジンの初期化（基本設定）

**OCR で画像を処理**する前に、ライセンスを保持するエンジンインスタンスが必要です。このステップは重要で、ライセンス未取得のエンジンは限定された結果しか返しません。

```python
import aspose.ocr as ocr  # Make sure you installed aspose-ocr via pip

# Create the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with your actual .lic file location
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

*重要な理由*: `OcrEngine` オブジェクトはライブラリの中核であり、言語モデル、画像前処理、ライセンス管理を行います。事前にライセンスを設定することで、完全な精度と透かしなしの結果が得られます。

---

## ステップ 2 – OCR 用に画像をロード

エンジンの準備ができたので、**OCR 用に画像をロード**する必要があります。Aspose は多数のフォーマット（PNG、JPEG、TIFF）をサポートしていますが、`Image.from_file` を使用すると画像が正しくデコードされることが保証されます。

```python
# Load the target image – change the path to point at your invoice file
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.from_file(image_path)
```

> **プロのコツ**: 画像ファイルは 5 MB 未満に保つと処理が最速です。大きなファイルは OCR 前に `image.resize(width, height)` で縮小できます。

---

## ステップ 3 – 関心領域（ROI）の定義

ほとんどの請求書には、住所ブロックやフッターなどの不要なテキストが多数含まれます。**関心領域（ROI）を定義**することで、金額や日付がある部分だけをエンジンに見せ、速度と精度を向上させます。

```python
# Define ROI: (x, y, width, height) in pixels
# Adjust these numbers based on the layout of your specific invoice
roi = ocr.Rectangle(150, 300, 400, 120)
```

*動作原理*: `Rectangle` クラスは画像を仮想的に切り取ります。OCR エンジンは矩形外のピクセルを一切見ないため、ROI 外のノイズは無視されます。

---

## ステップ 4 – ROI 内のテキストを認識

エンジン、画像、ROI の準備ができたら、ついに **画像からテキストを抽出**します。`recognize` メソッドは検出された文字列と信頼度スコアを含む `OcrResult` オブジェクトを返します。

```python
# Perform OCR only within the defined ROI
ocr_result = ocr_engine.recognize(image, roi=roi)

# Print the raw extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

**期待される出力**（典型的な請求書の合計行の例）:

```
Text inside ROI:
Total Amount: $1,245.67
```

ROI が正しく位置していれば、必要な行だけが表示されます—他のものは表示されません。

---

## ステップ 5 – 完全動作例（コピー＆ペースト可能）

以下は、これまでのすべてのステップを結びつけた完全なスクリプトです。`extract_invoice_roi.py` として保存し、`python extract_invoice_roi.py` を実行してください。

```python
# extract_invoice_roi.py
import aspose.ocr as ocr

def main():
    # 1️⃣ Initialize OCR engine and apply license
    ocr_engine = ocr.OcrEngine()
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image you want to process
    image = ocr.Image.from_file("YOUR_DIRECTORY/invoice.png")

    # 3️⃣ Define the region of interest (ROI) – rectangle where the text lives
    roi = ocr.Rectangle(150, 300, 400, 120)   # (x, y, width, height)

    # 4️⃣ Recognize text only inside the ROI
    ocr_result = ocr_engine.recognize(image, roi=roi)

    # 5️⃣ Display the extracted text
    print("Text inside ROI:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

スクリプトを実行すると、対象の行がコンソールに出力されます。空文字列が返った場合は、ROI の座標を再確認してください—数ピクセルのずれでもテキストが完全に除外されることがあります。

---

## ステップ 6 – 一般的なバリエーションとエッジケース

### a) 異なる請求書レイアウト  
ベンダーごとに請求書のレイアウトが異なり、合計金額のボックスがずれることがあります。複数のレイアウトで **OCR で画像を処理**するには、次を検討してください:

- **複数の ROI**: 複数の矩形でエンジンを順次実行し、最も信頼度の高い結果を選択します。  
- **動的 ROI 検出**: 軽量な画像処理ライブラリ（例: OpenCV）を使用してまず “Total” ラベルを検出し、それに対して ROI を計算します。

### b) 回転または歪んだ画像  
スキャンが傾いている場合、認識前に `image.rotate(angle)` を呼び出します:

```python
image = image.rotate(2.5)  # Rotate 2.5 degrees clockwise
```

Aspose OCR には自動デスケュー機能もありますが、手動回転の方が細かい制御が可能です。

### c) ラテン文字以外の文字  
デフォルトの言語モデルは英語です。別の言語で書かれた **請求書からテキストを抽出**するには、認識前に言語を設定します:

```python
ocr_engine.language = ocr.Language.French  # Example for French invoices
```

### d) 大きな PDF  
マルチページ PDF を扱う場合、まず各ページを画像として抽出します（Aspose PDF → Image）、その後各ページに同じ ROI ロジックを適用します。

---

## ステップ 7 – パフォーマンスのヒントとプロのコツ

- **エンジンをキャッシュ**: ループ内で `OcrEngine` を繰り返し作成すると遅くなります。一度インスタンス化して再利用してください。  
- **バッチ処理**: 複数の請求書がある場合、OCR 呼び出しを `ThreadPoolExecutor` でラップして I/O バウンドの作業を並列化します。  
- **信頼度チェック**: `ocr_result.confidence` は 0 から 1 の浮動小数点数です。0.85 未満の結果は拒否し、より大きな ROI または手動レビューにフォールバックします。  

> **注意**: ROI を小さくしすぎると文字が切れ、出力が乱れる可能性があります。スケールする前に、必ずいくつかのサンプル請求書でテストしてください。

---

## 結論

これで、Aspose OCR を使用して **画像からテキストを抽出**するための堅牢で本番環境向けの手法が手に入りました。**関心領域（ROI）を定義**し、**OCR 用に画像をロード**し、請求書のフィールドから確実に **テキストを抽出**する方法が含まれています。OCR を狭い ROI に限定することで、速度と精度の両方が向上し、何千件もの領収書のバッチ処理に最適です。

次のステップに進む準備はできましたか？このスクリプトを Flask API に統合し、ウェブアプリが請求書をアップロードして即座に合計金額を返すようにしてみてください。また、複数の ROI を試して日付、請求書番号、ベンダー名を一度に抽出することもできます。可能性は無限で、ここで紹介した基礎を押さえていれば、どんな OCR の課題にも対応できるでしょう。

コーディングを楽しんで、抽出したテキストが常にきれいでありますように！  

![画像からテキストを抽出する方法を示すワークフローダイアグラム](workflow.png){: .center-image alt="画像からテキストを抽出するワークフロー"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}