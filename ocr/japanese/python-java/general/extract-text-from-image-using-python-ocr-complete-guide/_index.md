---
category: general
date: 2026-06-06
description: 数分でPython OCRを使って画像からテキストを抽出できます。多言語画像OCRや自動言語検出OCR、そしてOCRテキストを正確に抽出する方法をご紹介します。
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: ja
og_description: Python OCRで画像からテキストをすばやく抽出しましょう。多言語画像OCR、言語自動検出OCR、そしてOCRテキストの抽出手順をステップバイステップで学びます。
og_title: Python OCRで画像からテキストを抽出する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: Python OCRで画像からテキストを抽出する – 完全ガイド
url: /ja/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR を使用した画像からのテキスト抽出 – 完全ガイド

画像から **テキストを抽出** したいが、複数言語を自動で処理できるライブラリが分からない…という経験はありませんか？開発者は国際文書、領収書、スキャンしたチラシを扱う際に、*OCR テキストを抽出する方法* を頻繁に質問します。このチュートリアルでは、画像からテキストを抽出するだけでなく、**言語を自動検出** する実用的な Python の例を順を追って解説します。これにより、多言語画像 OCR が簡単になります。

OCR パッケージのインストールから **自動言語検出 OCR** の有効化、サンプル画像でエンジンを実行し、検出された言語と抽出された文字列の両方を出力するまでを網羅します。最後まで読めば、翻訳パイプラインやデータインジェストサービスを構築する際に、どのプロジェクトにもすぐに組み込める再利用可能なスニペットが手に入ります。

## 画像からテキスト抽出 – 環境構築

コードに入る前に、作業環境が以下の最低要件を満たしていることを確認してください。

- Python 3.8 以上（ライブラリは型ヒントを使用しており、古いバージョンでは無視されます）
- `pip` によるパッケージ管理
- 少なくとも 2 種類の言語（例：英語 + スペイン語）が混在したテキストを含む画像ファイル

このデモで使用する OCR ライブラリも必要です。本ガイドでは、実際のツール（Tesseract や EasyOCR）に似た架空の `ocr` パッケージを使用しますが、同様の API を持つ実際のライブラリでも置き換えて利用できます。

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **プロのコツ:** 権限エラーが出た場合はコマンドの先頭に `python -m` を付けるか、仮想環境を使用してください。グローバルの site‑packages が汚染されません。

## OCR エンジンインスタンスの作成

ライブラリの準備ができたら、最初のステップは **OCR エンジンインスタンスを作成** することです。エンジンは画像を投入する前に設定できるスマートスキャナと考えてください。

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

なぜ静的メソッドを直接呼び出さずにエンジンをインスタンス化するのか？エンジンオブジェクトは言語設定などの構成状態を保持します。これにより、複数の画像に対して同じ設定を再利用でき、毎回の初期化オーバーヘッドを削減できます。

## 自動言語検出 OCR の有効化

多くの OCR ツールは言語コード（英語は `eng`、スペイン語は `spa` など）を指定する必要があります。手動で言語を推測すると、**多言語画像 OCR** の本来の目的が失われます。幸い、`ocr` パッケージは *auto detect language OCR* モードを提供しており、画像を解析して最適な言語モデルを自動的に選択します。

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

このように **detect language OCR** を有効にすれば、長大な言語コードリストを管理する必要がなくなります。エンジンは Latin、Cyrillic、Han などの文字体系を検出し、適切なモデルを自動でロードします。

## 多言語画像 OCR の実行

エンジンの準備ができたら、いよいよ **画像からテキストを抽出** します。`recognize_image` メソッドはファイルパスを受け取り、抽出されたテキストと検出された言語の両方を含む結果オブジェクトを返します。

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

PDF から *OCR テキストを抽出* したい場合は、同じエンジンの `recognize_pdf` を使用すれば OK です。内部ロジックは同一なので、**自動言語検出 OCR** 機能もそのまま利用できます。

## 検出された言語と抽出テキストの表示

最後に、エンジンが見つけた情報を出力します。結果オブジェクトは `detected_language`（例: `en` や `es` の BCP‑47 タグ）と、OCR の生データを保持する `text` を公開します。

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

サンプル画像でスクリプトを実行すると、次のような出力が得られるはずです。

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

エンジンが英語を主要言語として正しく認識しつつ、スペイン語の行も正確に取得していることが分かります。これこそが堅牢な **多言語画像 OCR** ソリューションが提供すべき結果です。

### 検出が失敗した場合は？

画像がぼやけていたり、文字体系が極端に珍しい場合、OCR エンジンはデフォルト言語（通常は英語）にフォールバックすることがあります。その際は言語リストを強制指定できます。

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

ただし、言語を強制すると **auto detect language OCR** の利便性が失われるため、限定された言語セットが分かっている場合にのみ使用してください。

## よくある落とし穴と信頼性の高い OCR テキスト抽出方法

自動検出を利用しても、以下のような問題でつまずくことがあります。

1. **低解像度画像** – 150 dpi 未満では OCR 精度が急激に低下します。画像を拡大するか、より高解像度のスキャンを依頼してください。
2. **ノイズ・圧縮アーティファクト** – 画像をエンジンに渡す前に、シンプルな閾値フィルタ（`opencv` や `Pillow`）で前処理すると効果的です。
3. **1 ページに混在するスクリプト** – Latin と CJK 文字が同時に存在すると一部エンジンは苦手です。必要に応じてページを領域ごとに分割し、別々に認識させてください。

これらの対策を講じることで、**画像からテキストを抽出** するプロセスの品質が大幅に向上し、実務での多言語文書処理が格段に楽になります。

## 完全動作サンプル

以下に、これまで説明したすべての手順を組み合わせた実行可能なスクリプトを示します。`multilingual_ocr.py` という名前で保存し、コマンドラインから実行してください。

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**期待される出力**（サンプル画像に英語とスペイン語が含まれている場合）:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

`multilang_page.png` を、他の言語が混在した任意の画像に差し替えても構いません。**自動言語検出 OCR** が有効なので、適切な言語タグと対応するテキストが得られます。

![画像からテキストを抽出する例](https://example.com/ocr-sample.png "画像からテキストを抽出する例")

## 結論

これで **画像から OCR テキストを抽出** する方法、**自動言語検出 OCR** を有効にする手順、そして最小限のコードで **多言語画像 OCR** シナリオに対応する方法がマスターできました。OCR エンジンインスタンスを作成し、言語自動検出をオンにし、`recognize_image` を呼び出すだけで、言語識別子と生テキストの両方を確実に取得できます。

次のステップは？抽出した文字列を翻訳 API に渡す、検索可能なデータベースに保存する、または複数ページを 1 つの PDF レポートにまとめる、などです。Tesseract、EasyOCR、Google Vision など別の OCR バックエンドに切り替えても、同じ高レベルワークフローが使えるのが **detect language OCR** インターフェースの強みです。

問題が発生したら「よくある落とし穴」セクションを再確認するか、画像前処理のパラメータを調整してください。コーディングを楽しみながら、正しく検出・抽出されたテキストが次のプロジェクトで活躍することを願っています！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースは完全なコード例とステップバイステップの解説を含んでおり、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}