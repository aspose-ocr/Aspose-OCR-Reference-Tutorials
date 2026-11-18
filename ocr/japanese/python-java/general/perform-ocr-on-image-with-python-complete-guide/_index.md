---
category: general
date: 2026-07-05
description: Pythonで画像のOCRを素早く実行する。OCR用に画像を読み込む方法、スキャンしたフォームからテキストを抽出する方法、そしてPythonで画像を認識するOCRの使い方を学びましょう。
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: ja
og_description: Pythonで画像のOCRを実行します。このチュートリアルでは、OCR用に画像を読み込む方法、スキャンしたフォームからテキストを抽出する方法、そしてPythonで画像を認識するためにOCRを使用する方法を示します。
og_title: Pythonで画像のOCRを実行する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Pythonで画像のOCRを実行する – 完全ガイド
url: /ja/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像のOCRを実行する – 完全ガイド

Pythonで **画像のOCRを実行** したいと思ったことはありませんか？ でもどこから始めればいいか分からない…という方は多いです。領収書をデジタル化したり、ノイズの多いアンケート用紙からデータを抽出したり、スキャンしたPDFを検索可能なテキストに変換したりする場合、スキャンしたフォームからテキストを抽出できることは多くの開発者にとって日々の課題です。

このチュートリアルでは、画像の読み込みからフィルタリング結果の表示まで、**OCR Python の使い方** をステップバイステップで解説します。最後まで読むと、**OCR 用の画像をロード** 方法、信頼度閾値の設定方法、そして実際に重い処理を行う **OCR recognize image Python** メソッドの呼び出し方が正確に分かります。

> **得られるもの:** 画像をロードし、OCR を実行し、クリーンで信頼度でフィルタリングされたテキストを出力する、すぐに実行できるスクリプトが手に入ります。曖昧な説明やインポート忘れは一切なし—そのままコピーして使える完全なソリューションです。

---

## 必要なもの

* Python 3.9 以上がインストールされていること（コードは 3.10+ でも動作します）。
* 以下で使用する `ocr` API に準拠した OCR パッケージ（例: 架空の `simple-ocr` ライブラリや、`OcrEngine`、`Language`、`Image` を公開するラッパー）。
* 抽出したいテキストが含まれる画像ファイル（`.png`、`.jpg` など）。
* 単一の Python スクリプトを実行できるターミナルまたは IDE。

これらが揃っているなら、素晴らしいです—さっそく始めましょう。

---

## 画像のOCRを実行 – エンジンの設定

最初に行うべきことは OCR エンジンのインスタンスを作成することです。エンジンは処理の頭脳と考えてください。ピクセルを解釈し文字に変換する方法を知っています。

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* エンジンがなければ処理できるものがありません。`OcrEngine` オブジェクトは、後で調整する言語や信頼度閾値など、すべての設定を保持します。

---

## OCR用画像のロード – スキャンしたフォームの準備

エンジンが用意できたので、**OCR 用の画像をロード** する必要があります。ライブラリの `Image.load()` メソッドはディスクからファイルを読み込み、エンジンが理解できる内部表現に変換します。

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **Tip:** PDF を扱う場合は、まず各ページを画像に変換してください（例: `pdf2image` を使用）。OCR エンジンはラスタ画像のみ受け付けます。

---

## OCR Python の使い方 – 言語と信頼度の設定

多くの OCR エンジンは複数言語に対応しており、信頼度の低い文字を除外できます。これらのパラメータを早めに設定することで、信頼できるテキストだけを取得できます。

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*Why 85 %?* 実務では、80‑90 % 前後の閾値にすると、ほとんどのノイズは除去され、重要な情報は残ります。スキャンの品質に応じて自由に調整してください。

---

## スキャンしたフォームからテキスト抽出 – 画像の認識

エンジンが準備でき、画像がロードされたら、実際に **画像のOCRを実行** する時です。`recognize()` メソッドは抽出されたテキストと、必要に応じてバウンディングボックスデータを含む結果オブジェクトを返します。

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

ライブラリが対応していれば、`result` は `result.confidences`（文字ごとの信頼度スコアのリスト）や `result.words`（構造化された単語オブジェクト）も提供する場合があります。このガイドではプレーンテキスト出力に焦点を当てます。

---

## OCR Recognize Image Python – フィルタ結果の表示

最後に、フィルタ済みテキストを出力しましょう。信頼度が低い記号は `?` として表示されます（`min_confidence` を 85 % に設定したため）。

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### 期待される出力

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

読めない署名が `?` に変換されていることに注目してください。これこそが信頼度フィルタの目的で、下流処理のために出力を整えることができます。

---

## よくある落とし穴とプロのコツ

| 問題 | 発生原因 | 簡単な解決策 |
|------|----------|--------------|
| **Blank output** | 画像が暗すぎる、または解像度が低すぎる。 | OpenCV で前処理：コントラストを上げ、解像度を ≥300 dpi にリサイズ。 |
| **Garbage characters** | 言語設定が間違っている。 | `engine.language` を文書に合わせて設定する（例: `ocr.Language.FRENCH`）。 |
| **Too many `?` symbols** | 信頼度閾値が高すぎる。 | ノイズが多いスキャンの場合、`engine.min_confidence` を 70‑80 % に下げる。 |
| **Unicode errors** | 出力に非 ASCII 文字が含まれるが、コンソールのエンコーディングが間違っている。 | `python -X utf8` を実行するか、`PYTHONIOENCODING=utf-8` を設定する。 |

**Pro tip:** テーブルを抽出したい場合は、生テキストをフィルタした後、レイアウト認識対応の OCR エンジン（例: Tesseract の `--psm 6`）で2回目の処理を実行してください。

---

## 完全スクリプト – 実行準備完了

以下は、説明したすべての手順を組み込んだ、完全な単一スクリプトです。`perform_ocr.py` という名前で保存し、画像パスを調整して `python perform_ocr.py` を実行してください。

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

実行すると、フィルタ済みテキストがコンソールに出力されます—**extract text from scanned form** ステップが約束した通りです。

---

## 次にやることは？

**画像のOCRを実行** と **スキャンしたフォームからテキスト抽出** の方法が分かったので、次は以下を検討してみてください：

* **バッチ処理** – 画像ディレクトリをループして結果を CSV に生成。
* **後処理** – 正規表現や spaCy を使って日付、金額、ID などのフィールドを抽出。
* **統合** – OCR 出力をデータベース、Google Sheets、または REST API に送信。

これらのアイデアはすべて、画像のロード、エンジンの設定、そして **OCR recognize image Python** メソッドの呼び出しという、今回紹介したコア機能をそのまま利用します。

---

## 結論

Python を使って **画像のOCRを実行** するための、完全で本番環境向けの例を一通り解説しました。**OCR 用の画像をロード** から言語設定、信頼度閾値の設定、最終的に **スキャンしたフォームからテキスト抽出** まで、すべてのステップが明確なコードと説明とともに示されています。これでバッチ処理や多言語対応、テーブル抽出など、より複雑なシナリオに取り組むための確固たる基盤ができました。

スクリプトを実行し、閾値を調整すれば、数分でドキュメントが検索可能になります。質問やうまく動かないフォームがあれば、下にコメントを残してください。一緒にトラブルシュートしましょう。コーディングを楽しんで！

![画像のOCR実行例](example.png "画像のOCR実行")

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [.NET 用 AspOCR の使い方: 画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR を使用した C# の画像テキスト抽出（言語選択）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}