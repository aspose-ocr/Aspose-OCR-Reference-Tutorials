---
category: general
date: 2026-04-26
description: スキャンしたフォームでOCRを実行し、ノイズを減らす画像前処理を学び、画像からテキストを迅速に抽出する方法。
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: ja
og_description: スキャンした文書でOCRを実行し、画像を前処理し、ノイズを低減し、効率的にテキストを抽出する方法。
og_title: OCRの実行方法と画像の前処理 – クイックガイド
tags:
- OCR
- image processing
- Python
title: OCRの実行と画像前処理の方法 – スキャンしたフォームからテキストを抽出する
url: /ja/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRの実行方法 – 画像からテキストを抽出する完全ガイド

汚れたスキャンフォームで **how to run OCR** を考えたことがありますか？きれいで検索可能なテキストを取得したいですよね。あなただけではありません。実際のプロジェクトでは、生の画像が斑点や不均一な照明、その他の問題でいっぱいで、標準のOCRがうまく機能しないことが多いです。  
良いニュースは？Pythonの数行とスマートな前処理パイプラインを使うだけで、認識精度を大幅に向上させ、**reduce noise**ことができ、必要な正確な単語を抽出できます。このチュートリアルでは、画像の読み込みから最終文字列の出力まで、すべてのステップを順に解説しますので、請求書や領収書、任意のスキャン文書に適用できる、すぐに使えるスニペットが手に入ります。

## 作成するもの

- 基盤となるOCRライブラリとやり取りする `OcrEngine` インスタンス。  
- 画像を **binarizes** し、**median blur** を適用して斑点を平滑化する前処理チェーン。  
- `process()` を呼び出すだけで、抽出された文字列を保持する `text` 属性を持つオブジェクトが返ります。  

最終的に、任意の画像ファイルで実行でき、コンソールに抽出されたテキストがすぐに表示される、自己完結型のスクリプトが手に入ります。

## 前提条件

- Python 3.9+（ここで使用している構文は最新の安定版に合わせています）。  
- 架空の `aocr` パッケージ – Tesseract や最新の OCR エンジンの薄いラッパーと考えてください。`pip install aocr` でインストールします。  
- 参照できるフォルダーに配置したスキャン画像（`scanned_form.jpg`）。  

実際の OCR ライブラリ（例: `pytesseract`）を使用する場合は、`OcrEngine` を適切なクラスに置き換えるだけで、他はそのままです。

![](how-to-run-ocr-example.png "OCR実行例 – スキャンフォームと抽出テキストを示す")

*Alt text: スキャンした文書で OCR を実行し、抽出されたテキストを表示する方法*

---

## ステップ 1: OCRの実行方法 – エンジンの初期化

エンジンが何かを読む前に、インスタンスを作成する必要があります。`OcrEngine` を、後で視覚データを解釈する脳と考えてください。

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Why this matters:** エンジンのインスタンス化は内部モデルの設定、言語パックのロード、ランタイム環境の準備を行います。このステップを省略すると、後で `process()` を呼び出したときに `NoneType` エラーが発生することが多いです。

---

## ステップ 2: 画像の前処理 – スキャンしたフォームの読み込み

脳が準備できたので、画像を渡します。画像は `aocr.Image` がサポートする任意の形式で構いません。

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro tip:** 開発中は絶対パスを使用して、スクリプトが別の作業ディレクトリから実行されたときに “file not found” エラーが出るのを防ぎましょう。

---

## ステップ 3: ノイズの低減 – 二値化とメディアンブラーの適用

生のスキャン画像には、散在する点や不均一な背景、薄い影が含まれることが多いです。2つの古典的な手法—**binarization** と **median blur**—は、文字のエッジを損なうことなく画像をきれいにします。

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### 詳細解説

- **Binarization**: `threshold=180` の値はアルゴリズムに「180 より明るいものは白、その他は黒になる」ことを指示します。スキャンが暗すぎる、または明るすぎる場合はこの数値を調整してください。  
- **Median Blur**: 半径 `2` は、フィルタが 5×5 ピクセルのウィンドウを見て、中心ピクセルを中央値に置き換えることを意味します。これにより、文字の筆跡を保ちつつ孤立した斑点が平滑化されます。

> **Edge case:** 文書にカラーのハイライトがある場合、単純な二値閾値ではそれらが消えてしまうことがあります。そのような場合は、代わりに `aocr.ImageFilters.adaptive_threshold()` の使用を検討してください—画像全体でローカルに閾値を調整します。

---

## ステップ 4: テキスト抽出 – OCRプロセスの実行

クリーンな画像が手に入ったので、いよいよエンジンに処理させます。

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **What happens under the hood?** エンジンはピクセルマトリックス上でニューラルネットワーク（または従来のパターンマッチャ）を実行し、認識された各グリフを Unicode 文字に変換し、行や段落に組み立てます。

---

## ステップ 5: テキスト抽出 – 結果の出力

`ocr_result` オブジェクトは便利な `text` 属性を提供します。取得した内容を見てみましょう。

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### 期待される出力

スキャンしたフォームに以下が含まれている場合：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

次のような出力が得られるはずです：

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

前処理ステップで、以前は “Amount” が “Am0unt” になる原因だった散在する点が除去されたことに注目してください。これが OCR 前の **how to reduce noise** の力です。

---

## よくある落とし穴と対処法

| 症状 | 考えられる原因 | 簡単な対処法 |
|------|----------------|--------------|
| 文字化け（例: “@#%”） | 画像が暗すぎるまたは明るすぎる | `binarize()` の `threshold` を調整；`adaptive_threshold` を試す。 |
| 欠落した単語 | ノイズが残っている | `median_blur` の `radius` を増やすか、`gaussian_blur` フィルタを追加する。 |
| 言語が間違っている（例: 英字が中国語になる） | 誤った言語パックがロードされている | ライブラリがサポートしていれば、`OcrEngine()` 作成時に `language="eng"` を指定する。 |
| 大きなファイルで処理が遅い | 解像度が高すぎる | 二値化前に画像を縮小する：`aocr.ImageFilters.resize(width=1200)` を使用。 |

---

## さらに進める – 次のステップと関連トピック

- **Batch processing**: 上記ロジックをループでラップし、数十ファイルを自動的に処理します。  
- **Structured output**: `ocr_result.text` に正規表現を使用して、日付や金額などのフィールドを抽出します。  
- **Alternative libraries**: `aocr` を `pytesseract` に置き換えるだけで、コードの変更はエンジン初期化ステップのみです。  
- **How to preprocess image for PDFs**: 各 PDF ページを画像に変換し、同じパイプラインを適用します。  

---

## 結論

私たちは **how to run OCR** を最初から最後までカバーし、**how to preprocess image** で **reduce noise** する方法を示し、**how to extract text from image** をクリーンで再現可能なスクリプトで実演しました。重要なポイントは？ 二値化とメディアンブラーというシンプルなフィルタを数個使うだけで、ノイズの多いスキャンを信頼できるデータ源に変え、手作業のクリーンアップにかかる時間を何時間も節約できることです。  

自分の文書でスクリプトを試し、閾値を調整して精度が向上する様子を確認してください。準備ができたら、バッチ処理を検討したり、出力をデータベースに統合して検索可能なアーカイブを作成しましょう。コーディングを楽しんで、OCRが常に的確でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}