---
category: general
date: 2026-05-03
description: Aspose OCR を使用してテキストを迅速に抽出します。OCR の精度向上方法、画像の OCR 読み込み、画像の前処理、そして Python
  での OCR スキャン実行方法を学びましょう。
draft: false
keywords:
- extract text ocr
- improve ocr accuracy
- load image ocr
- preprocess image ocr
- run OCR scan
language: ja
og_description: Aspose OCR を使用してテキストを迅速に抽出します。OCR の精度向上、画像の OCR 読み込み、画像の前処理、Python
  での OCR スキャンの実行方法をマスターしましょう。
og_title: テキスト抽出 OCR – Aspose OCR を使った完全ガイド
tags:
- OCR
- Python
- Aspose
title: テキスト抽出 OCR – Aspose OCR を使った完全ガイド
url: /ja/python-java/general/extract-text-ocr-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extract text ocr – Aspose OCR を使用した完全ガイド

スキャン画像が歪んでいて、結果が意味不明な文字列になってしまったことはありませんか？同じ壁にぶつかる開発者は多いです。画像が傾いていたり、ノイズが多かったり、コントラストが低いだけで OCR の精度は大きく低下します。幸い、いくつかの設定を調整するだけで、乱れた画像をきれいな検索可能テキストに変換できます。このチュートリアルでは、OCR の精度向上、画像の OCR 読み込み、前処理、そして最終的に Aspose OCR for Python でスキャンを実行するまでのフルエンドツーエンド例を順を追って解説します。

このガイドが終わる頃には、スキャンした JPEG を自動でクリーンアップし、抽出したテキストをコンソールに出力する実行可能スクリプトが手に入ります。「ドキュメントを見る」リンクは不要です。必要なものはすべてここにあります。

## 必要なもの

- **Python 3.8+**（最新の安定版がベストです）
- **Aspose.OCR for Python via .NET** – `pip install aspose-ocr` でインストール
- 購入済みの場合は **ライセンスファイル**（`Aspose.OCR.Java.lic`）※無料トライアルでもテスト可能
- 処理したい画像（例：`skewed_scanned_doc.jpg`）

以上です。これらが揃っていれば、すぐにコードに取り掛かれます。

## Step 1: Extract Text OCR with Aspose OCR Engine

最初に OCR エンジンを起動し、ライセンスを適用します。エンジンは画像を読む「脳」のようなものです。ライセンスが無いと、デモ制限を超えて動作しません。

```python
# Step 1: Create an OCR engine instance and apply your license
import aspose.ocr as ocr

ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

> **ポイント:** 事前にライセンスを適用しておかないと、後で静かな失敗が起きます。このステップを省くと、エンジンは制限モードに入り、数文字しか取得できません。テキスト OCR を抽出したいときに期待する結果にはなりません。

## Step 2: Improve OCR Accuracy with Pre‑processing

歪んだり粒状になったスキャンは OCR プロジェクトの最大の障害です。Aspose では、デスクュー、ノイズ除去、コントラスト強化といった便利な設定を簡単に切り替えられます。これが **improve ocr accuracy** の核心です。

```python
# Step 2: Enable preprocessing to improve accuracy on skewed or noisy scans
ocr_engine.config.auto_deskew = True          # automatically corrects rotation
ocr_engine.config.remove_noise = True         # reduces speckles
ocr_engine.config.enhance_contrast = True     # boosts text visibility
ocr_engine.config.binarization = "Otsu"       # choose a robust binarization method
```

- **auto_deskew** – 画像を水平に回転させます。元の文書が完全に平坦でない場合に必須です。
- **remove_noise** – 低解像度 JPEG によく見られるランダムな斑点を除去します。
- **enhance_contrast** – 暗い文字をさらに暗く、背景を明るくして、文字と背景の区別をしやすくします。
- **binarization = "Otsu"** – 黒白変換の最適閾値を決定する古典的アルゴリズムです。

> **プロのコツ:** ソース画像がすでにクリアであることが分かっている場合は、これらのオプションをオフにして処理速度を上げられます。ただし、実務のスキャンではオンのままが安全です。

## Step 3: Load Image OCR for Scanning

エンジンの準備ができたら、**load image ocr** を行います。Aspose の `Image.from_file` メソッドは JPEG、PNG、TIFF など複数のフォーマットに対応しています。

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Image.from_file("YOUR_DIRECTORY/skewed_scanned_doc.jpg")
```

`YOUR_DIRECTORY` を実際のパスに置き換えてください。Web アップロードなどでメモリ上のバイトストリームから読み込む場合は、`ocr.Image.from_bytes(byte_data)` も使用可能です。同じエンジンが処理します。

> **エッジケース:** 大きな TIFF ファイルはメモリを大量に消費します。`MemoryError` が出たら、まず画像をダウンサンプリングするか、`ocr_engine.config.max_image_size` でサイズ上限を設定してください。

## Step 4: Run OCR Scan and Get Results

画像のロードと前処理が完了したら、最後に **run OCR scan** を実行します。この呼び出しが裏で重い処理をすべて行います。

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.recognize(input_image)
```

`ocr_result` オブジェクトには便利なプロパティがいくつかあります：

- `ocr_result.text` – 取得したプレーンテキスト
- `ocr_result.confidence` – 0〜100 の数値スコアで全体的な信頼度を示します
- `ocr_result.words` – バウンディングボックス座標を持つ単語オブジェクトのリスト。ハイライト表示に便利です

## Step 5: Print the Extracted Text

最後に結果を出力します。実際のアプリではテキストをファイルやデータベースに保存したり、検索インデックスに流し込んだりしますが、このチュートリアルではシンプルに `print` で表示します。

```python
# Step 5: Print the extracted text
print("=== Extracted Text ===")
print(ocr_result.text)
print("\nConfidence:", ocr_result.confidence)
```

**期待される出力**（シンプルな請求書の例）：

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00

Confidence: 96.2
```

信頼度が低い（< 80）場合は、前処理オプションを見直すか、`"Sauvola"` など別の二値化手法を試してください。

## Bonus: Visualizing the Pre‑processing Pipeline (Optional)

エンジンが画像に対して何をしたかを確認したくなることがあります。Aspose は処理後のビットマップをエクスポートできます：

```python
# Save the pre‑processed image for debugging
processed_image = ocr_engine.config.get_processed_image()
processed_image.save("processed_debug.png")
```

この画像をドキュメントに埋め込むことも可能です：

<img src="ocr_workflow.png" alt="extract text ocr workflow diagram showing preprocessing steps">

> **なぜやるのか:** OCR 結果が期待外れの場合、`processed_debug.png` をざっと見るだけで、画像がまだ暗すぎる、傾いている、ノイズが残っているなどの原因が分かります。

## Common Questions & Gotchas

- **文書が複数ページの場合は？**  
  Aspose OCR はページ単位で処理します。各ページ画像をループし、`ocr_result.text` を結合してください。

- **英語以外の言語は認識できますか？**  
  はい。`ocr_engine.config.language = "fra"`（または任意の ISO‑639‑2 コード）を `recognize` 呼び出し前に設定します。

- **画像サイズに上限はありますか？**  
  デフォルトで 10 MP が上限です。より大きなスキャンが必要な場合は `ocr_engine.config.max_image_size` を増やしますが、メモリ使用量に注意してください。

- **PDF 用に別の OCR エンジンが必要ですか？**  
  PDF の場合は、Aspose.PDF で各ページを画像に変換してから本手順を実行するか、組み込みの PDF OCR 機能を使用します。画像が得られれば手順は同じです。

## Recap

Aspose OCR for Python を使って **extract text ocr** を行う方法を、ライセンス適用から **improve ocr accuracy** の設定、画像の読み込み、最終的な **run OCR scan** まで網羅しました。完全なスクリプトはそのままコピー＆ペースト可能で、各設定フラグの意味も理解できたはずです。

## What’s Next?

- **異なる二値化手法**（`"Sauvola"`、`"Bradley"`）を試す。フォントによっては適応閾値の方が効果的です。
- **検索エンジン**（例：Elasticsearch）と統合し、信頼度スコアで結果をランク付けする。
- **OCR 後処理** ライブラリ（`pyspellchecker` など）を組み合わせて、一般的な認識ミスを修正する。
- **バッチ処理** を実装し、数百枚のスキャンを一括処理できるように関数化し、フォルダ単位で画像を渡す。

コードを自由にカスタマイズし、ロギングを追加したり、ドキュメント管理パイプラインに組み込んだりしてください。問題があればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}