---
category: general
date: 2026-02-09
description: Aspose を使用した Python で OCR による PDF からのテキスト抽出。OCR で PDF を読む方法、OCR 用に PDF
  をロードする方法、そして PDF テキストを効率的に抽出するコツをマスターしましょう。
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load pdf for ocr
- how to extract pdf text
language: ja
og_description: Aspose を使用して OCR で PDF からテキストを抽出します。このガイドでは、OCR で PDF を読み取る方法、OCR
  用に PDF をロードする方法、そして PDF テキストを抽出する方法について説明します。
og_title: OCRでPDFからテキストを抽出 – Pythonチュートリアル
tags:
- OCR
- Python
- PDF processing
title: OCRでPDFからテキストを抽出 – 完全なPythonガイド
url: /ja/python/general/extract-text-from-pdf-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFからテキストを抽出する OCR – 完全な Python ガイド

PDF が単なるスキャン画像だったことがありますか？その壁にぶつかっているのはあなただけではありません。実務で受け取る PDF の多くは画像のみで、単純に「PDF を読む」だけでは何も取得できません。そこで OCR が登場し、今回は Aspose OCR for Python を使って **PDF からテキストを抽出する方法** を詳しくご紹介します。

このチュートリアルでは **OCR で PDF を読む** 方法を学び、**OCR 用に PDF をロードする** 最適な手順を確認し、各単語とその信頼度スコアを返す完全なサンプルを実行します。曖昧な説明は一切なく、実行可能なスクリプト、各行が重要な理由の解説、すぐに使えるヒントが満載です。

## このガイドでカバーする内容

まず Aspose OCR パッケージをインストールし、`OcrEngine` を作成、PDF をロード、構造化認識を実行し、最後にすべての単語と信頼度を取得します。これを終えると、スキャンしたドキュメントに対して **PDF からテキストを抽出する方法** に自信を持って答えられるようになり、構造化 OCR とプレーン OCR のトレードオフも理解できるようになります。

前提条件は最小限です：Python 3.8 以上、pip でインストール可能な Aspose OCR ライブラリ、そして処理したい PDF があれば OK。基本的な Python のループが書ければ問題ありません。

なぜ重要かというと、信頼度スコアを使えば低品質な結果を自動的に除外でき、構造化テキストはページ・ブロック・行・単語の階層情報を保持するため、下流の分析や検索インデックス作成に最適だからです。

---

![Extract text from PDF using Aspose OCR](https://example.com/placeholder-image.jpg "extract text from pdf")

*画像代替テキスト: “Python で Aspose OCR エンジンを使用して PDF からテキストを抽出”*

## Step 1 – Install and Import Aspose OCR

コードを実行する前にライブラリが必要です。Aspose OCR は純粋な Python の wheel として提供されているので、`pip` コマンド一つで完了します。

```bash
pip install aspose-ocr
```

次にモジュールをインポートします。インポート行は `aspose.ocr as aocr` のように見えるかもしれませんが、名前空間をすっきり保つための書き方です。

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr
```

*なぜ重要か:* `aspose.ocr` をインポートすることで、ファイルのロードから構造化結果の取得までを司るコアクラス `OcrEngine` にアクセスできるようになります。

## Step 2 – Create the OCR Engine Instance

`OcrEngine` オブジェクトは言語、認識モード、パフォーマンス設定などの構成をカプセル化します。ほとんどの場合デフォルトで問題ありませんが、後で調整可能です。

```python
# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()
```

> **プロのコツ:** PDF が英語のみの場合は `ocr_engine.language = aocr.Language.English` と設定すると処理が高速化します。

## Step 3 – Load PDF for OCR

ここで **OCR 用に PDF をロード** します。`load_image` メソッドは PDF、JPG、PNG、TIFF など多数のフォーマットを受け付けるため、他のソースでも同じコードを再利用できます。

```python
# Step 3: Load the document you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.pdf")
```

*内部で何が起きているか?* Aspose は各ページをラスタ画像に変換し、OCR エンジンはそれを通常の画像として扱います。そのためマルチページ PDF を直接渡しても、エンジンが内部でページを順に処理してくれます。

## Step 4 – Perform Structured Recognition

構造化認識はレイアウト階層（ページ → ブロック → 行 → 単語）を保持した `OcrResult` オブジェクトを返します。これはプレーンテキスト出力より遥かにリッチです。

```python
# Step 4: Perform structured recognition to obtain detailed results
ocr_result = ocr_engine.recognize_structured()   # returns an OcrResult object
```

プレーンテキストだけが欲しい場合は `ocr_engine.recognize()` を呼び出すことも可能ですが、信頼度スコアや位置情報が失われます。これらの情報は検証パイプラインでしばしば重要です。

## Step 5 – Extract Words and Confidence Scores

ここが **PDF からテキストを抽出しつつ信頼度も取得する** 核心部分です。入れ子になったループで階層をたどり、`(word, confidence)` のタプルを収集します。

```python
# Step 5: Extract recognized words and their confidence scores
recognized_words = []
for page in ocr_result.structured_text.pages:
    for block in page.blocks:
        for line in block.lines:
            for word in line.words:
                recognized_words.append((word.text, word.confidence))
```

*なぜこのようにループするのか?* 各レベル（ページ → ブロック → 行 → 単語）でコンテキストが得られます。たとえば後で単語を文に再構成したり、信頼度が低いヘッダーブロックの単語を除外したりできます。

### Edge‑Case Handling

- **空の PDF:** `ocr_result.structured_text.pages` が空の場合、`recognized_words` も空のままです。適切にハンドリングしてください。
- **低信頼度:** `confidence < 0.6` の単語を除外したい場合は次のようにします。

```python
high_confidence = [(t, c) for t, c in recognized_words if c >= 0.6]
```

## Step 6 – Show a Sample Word with Its Confidence

簡単なサニティチェックとして、最初の単語とその信頼度を出力します。これでエンジンが実際に読み取っていることを確認できます。

```python
# Step 6: Show a sample word with its confidence
if recognized_words:
    sample_text, sample_conf = recognized_words[0]
    print(f"{sample_text} (conf: {sample_conf:.2f})")
```

典型的な出力例:

```
Invoice (conf: 0.98)
```

信頼度が 0.5 未満の場合は、OCR 前に画像前処理（例: デスキュー）を行うことを検討してください。

## Step 7 – Summarize the Total Number of Words Recognized

最後に、ユーザー向けに認識された単語数の概要を表示します。ログや UI フィードバックに便利です。

```python
# Step 7: Summarize the total number of words recognized
print(f"Total words recognized: {len(recognized_words)}")
```

コンソール出力例:

```
Total words recognized: 1,342
```

## Full Working Example

以上をまとめた完全なスクリプトを以下に示します。`extract_ocr.py` という名前で保存し、`"YOUR_DIRECTORY/input.pdf"` を対象の PDF パスに置き換えてください。

```python
# extract_ocr.py – Complete example to extract text from PDF with OCR

import aspose.ocr as aocr

def extract_words(pdf_path):
    # Initialize OCR engine
    ocr_engine = aocr.OcrEngine()
    
    # Load PDF (this is the step where we **load PDF for OCR**)
    ocr_engine.load_image(pdf_path)
    
    # Run structured recognition
    ocr_result = ocr_engine.recognize_structured()
    
    # Collect words + confidence
    words = []
    for page in ocr_result.structured_text.pages:
        for block in page.blocks:
            for line in block.lines:
                for word in line.words:
                    words.append((word.text, word.confidence))
    return words

if __name__ == "__main__":
    pdf_file = "YOUR_DIRECTORY/input.pdf"
    recognized = extract_words(pdf_file)
    
    # Show first word as a quick sanity check
    if recognized:
        txt, conf = recognized[0]
        print(f"{txt} (conf: {conf:.2f})")
    
    # Summary
    print(f"Total words recognized: {len(recognized)}")
```

このスクリプトを実行すると、サンプル単語とその信頼度、そして総単語数が表示されます。これで **OCR で PDF を読む** が期待通りに動作したことを確認できます。

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *What if my PDF is password‑protected?* | Call `ocr_engine.load_image("file.pdf", password="secret")`. The engine will decrypt before rasterizing. |
| *Can I process multiple PDFs in a batch?* | Absolutely. Wrap the `extract_words` call in a loop over a list of file paths. |
| *Do I need to install additional language packs?* | For non‑English PDFs, install the appropriate language pack (`pip install aspose-ocr‑lang‑<lang>`). |
| *How do I improve low confidence scores?* | Preprocess the PDF pages (increase DPI, apply binarization) before loading, or enable `ocr_engine.image_preprocessing = True`. |

## Next Steps – Going Beyond Basic Extraction

今や **PDF からテキストを抽出する** 方法と信頼度スコアの取得ができるようになったので、次のような拡張を検討できます。

- **Indexing** the words into Elasticsearch for full‑text search.
- **Exporting** the structured hierarchy to JSON for downstream analytics.
- **Combining** Aspose OCR with PDF‑to‑image tools to fine‑tune DPI settings.
- **Integrating** the pipeline into a Flask or FastAPI endpoint to provide OCR as a service.

これらの拡張はすべて、ここで紹介したコアコードをベースにすぐに実装可能です。

---

### Conclusion

本稿では、Aspose OCR を用いた Python での **PDF からテキストを抽出** のエンドツーエンドソリューションを解説しました。PDF を OCR 用にロードし、構造化認識を実行し、ページ・ブロック・行・単語を順に走査することで、単なるテキストだけでなく単語ごとの信頼度も取得できます。これは品質管理に不可欠です。

スクリプトを自由にカスタマイズしたり、前処理を追加したり、より大規模なドキュメント処理ワークフローに組み込んだりしてください。疑問や問題があればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}