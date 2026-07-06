---
category: general
date: 2026-05-03
description: Aspose OCR を使用して Python で画像からテキストを抽出します。ラテン文字とキリル文字が混在するサポートを備えた、ステップバイステップの
  Python OCR チュートリアルを学びましょう。
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: ja
og_description: 画像からテキストをPythonで迅速に抽出する。このガイドでは、ラテン文字とキリル文字が混在する画像に対して、PythonでAspose
  OCRを使用する方法を示します。
og_title: Pythonで画像からテキストを抽出 – 完全なAspose OCRウォークスルー
tags:
- OCR
- Python
- Aspose
title: Pythonで画像からテキストを抽出 – 完全なAspose OCRガイド
url: /ja/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する Python – 完全 Aspose OCR ガイド

**画像からテキストを抽出する Python** が必要だったけど、ラテン文字とキリル文字が混在した画像を扱えるライブラリが分からない、ということはありませんか？ 同じ悩みを抱える開発者は多く、マルチリンガルなスクリーンショットの OCR でつまずくことが頻繁にあります。

朗報です。Aspose OCR for Python を使えば、ほぼ手間なく処理できます。このチュートリアルでは、パッケージのインストール、ライセンスの適用、混在言語画像の読み込み、そして数行のコードで認識結果を取得する手順を解説します。最後まで読めば、どのプロジェクトにもすぐに組み込めるスクリプトが手に入ります。

## 学べること

- 仮想環境で **Aspose OCR Python** をセットアップする方法  
- 言語ヒント（ラテン文字・キリル文字など）を付けると検出が高速になる理由  
- **画像からテキストを抽出する Python** を単一関数呼び出しで実現する正確なコード  
- 混在言語 OCR の典型的な落とし穴と回避策  

### 前提条件

- Python 3.8 以上がインストールされていること  
- Aspose OCR のライセンスファイル (`Aspose.OCR.Java.lic`)。無料トライアルでもテストは可能ですが、ライセンスを適用すると透かしが除去されます。  
- ラテン文字とキリル文字が混在した PNG/JPEG 画像（例: `mixed_latin_cyrillic.png`）  

上記が揃っていれば、追加のフレームワークや重い依存関係は不要です。

---

## Step 1 – 画像からテキストを抽出する Python: Aspose OCR のインストール

まずは PyPI からライブラリを取得し、ライセンスファイルが参照できるように環境を整えます。

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **プロのコツ:** 権限エラーが出た場合は `pip install` に `--user` を付けるか、ターミナルを管理者として実行してください。

パッケージがインストールできたら、ライブラリをインポートし、ライセンスをエンジンに設定します。

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

なぜこの段階でライセンスが必要かというと、ライセンスが無いとエンジンは **評価モード** で動作し、ページ数が制限されたり出力に透かしが入ったりします。事前にライセンスを設定しておくことで、後の `recognize` 呼び出しがクリーンなテキストを返すようになります。

---

## Step 2 – ラテン‑キリル混在画像をロードする

次に画像をメモリに読み込みます。Aspose OCR は独自の `Image` クラスを使用し、基になるファイル形式を抽象化します。

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

他の形式が使えるか気になる場合は、JPEG、BMP、TIFF、さらには PDF もサポートされています。拡張子を変えて `from_file` メソッドを呼び出すだけで自動的に処理されます。

---

## Step 3 – 言語ヒントで検出を高速化（任意だが推奨）

画像に含まれる言語が分かっている場合、エンジンにヒントを与えることができます。必須ではありませんが、**処理時間が大幅に短縮** され、混在言語 OCR の精度も向上します。

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

ヒントリストには Aspose OCR がサポートする任意の言語（例: `"Arabic"`、`"Japanese"`）を指定できます。このステップを省略すると、エンジンはすべての組み込み言語を試すため、大量の画像を処理する際は遅くなることがあります。

---

## Step 4 – OCR エンジンを実行してテキストを抽出

いよいよ本番です。文字認識を実行します。`recognize` メソッドは `OcrResult` オブジェクトを返し、プレーンテキスト、信頼度スコア、必要に応じてバウンディングボックスも取得できます。

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **なぜ動くのか:** 背後では Aspose OCR がニューラルネットワークベースのテキスト検出器と、言語別の分類器を組み合わせています。`Image` オブジェクトを渡すだけで、二値化などの前処理は不要です。

---

## Step 5 – 抽出結果を表示

最後に結果をコンソールに出力します。実際のアプリではファイルへ書き出したり、データベースに保存したり、翻訳 API に渡したりすることも考えられます。

```python
print("Recognised text:")
print(extracted_text)
```

スクリプトを実行すると、次のような出力が得られるはずです。

```
Recognised text:
Hello мир! This is a test.
```

この出力は、**画像からテキストを抽出する Python** がラテン文字とキリル文字の両方を一度に正しく処理できたことを示しています。

---

## 完全動作サンプル

以下は `extract_ocr.py` というファイルに貼り付けてそのまま使えるフルスクリプトです。プレースホルダーのパスは実際の環境に合わせて置き換えてください。

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

ファイルを保存し、仮想環境を有効化した上で次のコマンドを実行します。

```bash
python extract_ocr.py
```

認識されたテキストがコンソールに表示され、エンドツーエンドで動作することが確認できます。

---

## FAQ とエッジケース

**画像がぼやけている場合は？**  
Aspose OCR には自動デスキューやノイズ除去機能がありますが、極端に劣化した写真は OpenCV で前処理（例: ガウシアンブラーと閾値処理）した方が効果的です。`Image` クラスは NumPy 配列も受け取れるので、カスタムフィルタを適用した後に `recognize` を呼び出せます。

**フォルダ内の画像を一括処理できるか？**  
可能です。`for` ループでロジックを回し、`from_file` に各ファイル名を渡して結果を辞書に格納すれば完了です。クラウド版を利用する場合は API のレートリミットに注意してください。

**言語ごとに別ライセンスが必要か？**  
不要です。単一の Aspose OCR ライセンスでサポートされているすべての言語が利用可能です。`language_hints` はあくまでパフォーマンス向上のためのヒントです。

**PDF 入力はどう扱う？**  
`Image.from_file` を `ocr.Image.from_file("document.pdf")` に置き換えるだけです。OCR エンジンが自動的に各ページをラスタライズし、結合されたテキストを返します。

---

## 結論

本稿では Aspose OCR を用いた **画像からテキストを抽出する Python** のシンプルかつ本番環境向けの手順を示しました。インストール、ライセンス設定、画像読み込み、言語ヒント、認識、表示という流れで、ラテン‑キリル混在コンテンツに対して信頼性の高い結果が得られます。

ここからは、バッチ処理向けの **画像からテキストへの変換**、自然言語処理向けの **Python OCR チュートリアル** への統合、あるいは多言語文書向けに別の言語ヒントを試すなど、応用範囲は無限です。コードはすでに手元にあるので、ぜひ活用してください。

別のユースケースや問題に直面したらコメントでシェアしてください。皆で情報を共有し、会話を続けましょう。Happy coding!  

![画像からテキストを抽出する Python の例](/images/extract-text-from-image-python.png "OCR 出力を示すスクリーンショット – 画像からテキストを抽出する Python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}