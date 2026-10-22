---
category: general
date: 2026-06-19
description: Aspose OCR を使用して Python で OCR の精度を向上させましょう。OCR 言語の設定方法、OCR 用に画像を読み込む方法、カスタム辞書を使用して画像からテキストを抽出する方法を学びます。
draft: false
keywords:
- improve OCR accuracy
- extract text from image
- perform OCR on image
- load image for OCR
- set OCR language
language: ja
og_description: OCR言語を設定し、OCR用に画像を読み込み、カスタム辞書を使用して画像からテキストを抽出することで、PythonのOCR精度を向上させます。
og_title: PythonでOCR精度を向上させる – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  headline: Improve OCR Accuracy in Python – Complete Guide
  type: TechArticle
- description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  name: Improve OCR Accuracy in Python – Complete Guide
  steps:
  - name: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
    text: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
  - name: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
    text: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
  - name: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
    text: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
  - name: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
    text: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
  - name: '**Setting the OCR language** to match your document.'
    text: '**Setting the OCR language** to match your document.'
  - name: '**Loading the image correctly** so the engine sees the right pixels.'
    text: '**Loading the image correctly** so the engine sees the right pixels.'
  - name: '**Performing OCR on the image** with a single method call.'
    text: '**Performing OCR on the image** with a single method call.'
  - name: '**Extracting text from the image** and confirming the result.'
    text: '**Extracting text from the image** and confirming the result.'
  - name: '**Adding a custom dictionary** to lock in domain‑specific terms.'
    text: '**Adding a custom dictionary** to lock in domain‑specific terms.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: PythonでOCR精度を向上させる – 完全ガイド
url: /ja/python-java/general/improve-ocr-accuracy-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で OCR 精度を向上させる – 完全ガイド

スキャンしたテキストに奇妙な記号や製品コード、ブランド名が含まれているとき、**OCR 精度を向上させる** 方法を考えたことはありませんか？ あなたは一人ではありません。多くのプロジェクトでデフォルトエンジンは意味不明な文字列を出力し、生産性を大きく低下させます。

このチュートリアルでは、実践的なエンドツーエンドの例を通じて、**OCR 言語の設定**、**画像の読み込み**、**画像に対する OCR の実行**、そして認識率を高めるカスタム辞書を用いた **画像からテキストを抽出** の手順を解説します。最後まで読めば、任意の Python コードベースにすぐ組み込めるスクリプトが手に入ります。

## 学べること

- Aspose OCR を使用して PNG ファイルを読み取る完全動作する Python スクリプト
- 言語設定とカスタム単語リストで **OCR 精度を向上させる** 方法
- 各設定が重要な理由の明確な説明と、ラテン文字以外の文字に対する対処法のヒント
- 一般的な OCR の落とし穴をトラブルシューティングするための簡易チェックリスト

### 前提条件

- Python 3.8 以上がインストールされていること  
- `aspose-ocr` パッケージ（`pip install aspose-ocr` でインストール）  
- 読み取り対象のテキストが含まれるサンプル画像（`technical_doc.png`）  
- Python の基本的な知識 – 特別なスキルは不要です

> **プロのコツ:** 仮想環境で作業している場合は、パッケージをインストールする前に環境をアクティベートしてください。依存関係が整理され、バージョン衝突を防げます。

---

## 手順 1: Aspose OCR をインストールしてインポート

まずはライブラリを環境に導入し、必要な要素をインポートします。

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

import aspose.ocr as ocr
```

`aspose.ocr` 名前空間から `OcrEngine` クラスにアクセスでき、これが OCR プロセスの中心です。ここでインポートしておくことで、スクリプト全体がすっきり読みやすくなります。

---

## 手順 2: OCR エンジンを作成し **OCR 言語を設定**

言語が重要なのはなぜでしょうか？ OCR エンジンは言語固有のモデルを使って文字形状や単語パターンを認識します。英語テキストをスキャンすると伝えると、キリル文字は無視され、ラテン文字に集中するため、**OCR 精度が大幅に向上**します。

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Set the recognition language to English (you can pick other languages too)
engine.language = ocr.Language.English
```

> **注:** Aspose OCR は 50 以上の言語に対応しています。ドキュメントが英語でない場合は `ocr.Language.English` を `ocr.Language.Spanish`、`ocr.Language.French` などに置き換えてください。

---

## 手順 3: **カスタム辞書** を定義して精度をブースト

請求書に「AsposeOCR」や「SKU12345」のような製品コードが含まれていると想像してください。エンジンはこれらの語を知らないため誤認識します。カスタム単語リストを提供すると、エンジンに対して「これらは正しい文字列なので修正しないで」と指示できます。これが **OCR 精度を向上させる** 簡単な方法です。

```python
# Step 3: Create a list of domain‑specific words
custom_word_list = [
    "AsposeOCR",   # brand name
    "InvoiceID",   # field label
    "SKU12345",    # product code
    "β‑cell"       # Greek character example
]

# Attach the custom dictionary to the engine
engine.text_processing.custom_dictionary = custom_word_list
```

エントリが数百件ある場合はファイルやデータベースから読み込んでも構いませんが、ここではシンプルに Python のリストに保持しています。

---

## 手順 4: **画像を OCR 用に読み込む**

次に画像が必要です。`Image.load` メソッドは PNG、JPEG、BMP などのサポートされているラスタ形式のパスを受け取ります。ファイルが見つからないと例外がスローされるため、例外処理で保護します。

```python
import os

image_path = "YOUR_DIRECTORY/technical_doc.png"

if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found: {image_path}")

# Step 4: Load the image into memory
image = ocr.Image.load(image_path)
```

> **このステップが重要な理由:** 画像を正しく読み込むことで、エンジンは意図したピクセルデータに基づいて解析できます。破損したファイルやパスミスはフラストレーションの原因となります。

---

## 手順 5: **画像に対して OCR を実行** し結果を取得

エンジンの設定と画像の準備が整ったら、認識はたった一つのメソッド呼び出しで完了します。結果オブジェクトには生テキスト、信頼度スコア、必要に応じてレイアウト情報も含まれます。

```python
# Step 5: Run OCR
result = engine.recognize(image)

# The recognized text is stored in result.text
recognized_text = result.text
```

画像から **テキストを抽出** したい場合は、改行文字で分割すれば行単位で取得できます。

```python
lines = recognized_text.splitlines()
for idx, line in enumerate(lines, start=1):
    print(f"{idx:02d}: {line}")
```

---

## 手順 6: 出力を検証 – 本当に **OCR 精度が向上** したか？

結果を出力して、カスタム辞書が効果を発揮したか確認しましょう。

```python
print("\n--- OCR Output ---")
print(recognized_text)
```

サンプル画像に対する典型的な出力例は次のようになります。

```
--- OCR Output ---
InvoiceID: 2023‑07‑15
Customer: AsposeOCR Ltd.
Product: β‑cell Therapy Kit
SKU: SKU12345
```

ブランド名、ギリシャ文字、製品コードが定義どおりに表示されていることに注目してください。カスタム辞書がなければ、エンジンは「Aspose OCR」や「SKU 1234」のように「修正」しようとしてしまいます。

---

## よくある落とし穴と対処法

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **文字化け** | 言語設定が間違っている、または解像度が低い画像 | `engine.language` がソース言語と一致しているか確認し、300 dpi 以上の高解像度でスキャンする |
| **カスタム単語が無視される** | 辞書がエンジンに紐付いていない、またはプロパティ名のタイプミス | `engine.text_processing.custom_dictionary = …` を再確認 |
| **ファイルが見つからない** | パスが誤っている、またはアクセス権が不足している | `os.path.abspath()` で絶対パスを確認し、適切な権限でスクリプトを実行 |
| **処理が遅い** | 画像が大きすぎる、ページ数が多い | 画像を事前にトリミング・リサイズするか、`engine.recognize(image, max_threads=4)` で並列化 |

---

## さらに踏み込む: **OCR 精度を向上** させる高度な調整

1. **前処理** – Pillow でコントラスト強調や二値化を行ってから Aspose OCR に渡す  
2. **複数言語** – `engine.language = ocr.Language.English | ocr.Language.French` でバイリンガル認識を有効化  
3. **領域限定 OCR** – テーブルなど特定エリアだけが必要な場合は、先に画像をトリミングしてノイズを減らす  
4. **信頼度フィルタ** – `result.confidence` で文字ごとのスコアが取得できるので、低信頼度の結果はプログラムで除外可能

---

## 完全動作スクリプト

以下は本チュートリアルで説明したすべての手順を組み込んだ、コピー＆ペースト可能なスクリプトです。`improve_ocr_accuracy.py` として保存し、コマンドラインから実行してください。

```python
# improve_ocr_accuracy.py
# Complete example that shows how to improve OCR accuracy with Aspose OCR in Python.

import os
import aspose.ocr as ocr

def main():
    # ---------- Step 1: Initialize engine and set language ----------
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English          # set OCR language

    # ---------- Step 2: Attach custom dictionary ----------
    custom_word_list = [
        "AsposeOCR",
        "InvoiceID",
        "SKU12345",
        "β‑cell"
    ]
    engine.text_processing.custom_dictionary = custom_word_list

    # ---------- Step 3: Load the image ----------
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    image = ocr.Image.load(image_path)               # load image for OCR

    # ---------- Step 4: Perform OCR ----------
    result = engine.recognize(image)                 # perform OCR on image
    recognized_text = result.text

    # ---------- Step 5: Output the recognized text ----------
    print("\n--- OCR Output ---")
    print(recognized_text)

    # Optional: print line numbers for easier debugging
    print("\n--- Line‑by‑Line View ---")
    for idx, line in enumerate(recognized_text.splitlines(), start=1):
        print(f"{idx:02d}: {line}")

if __name__ == "__main__":
    main()
```

実行例:

```bash
python improve_ocr_accuracy.py
```

先ほど示した整形済みの出力が表示されるはずです。

---

## 結論

本稿では、Python で **OCR 精度を向上** させるシンプルな手順を次のようにまとめました。

1. ドキュメントに合わせて **OCR 言語を設定**  
2. エンジンが正しいピクセルを認識できるよう **画像を正しく読み込む**  
3. **画像に対して OCR を実行** し、1 行のメソッド呼び出しで結果を取得  
4. **画像からテキストを抽出** し、結果を検証  
5. ドメイン固有の用語を固定する **カスタム辞書** を追加

これで、未加工の画像からクリーンで検索可能なテキストへ変換するワークフローが完成です。次のステップとして、画像前処理（コントラスト調整、デスケュー）に挑戦したり、`ocr.Language.English | ocr.Language.German` のように多言語設定に切り替えてみてください。同じ原則で **OCR 精度を向上** させ続けられます。

質問や特殊ケースがあればコメントで教えてください。Happy coding!

![improve OCR accuracy


## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全動作コード例が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れるのに役立ちます。

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}