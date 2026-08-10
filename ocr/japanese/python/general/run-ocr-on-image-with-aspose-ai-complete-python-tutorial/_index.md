---
category: general
date: 2026-07-18
description: PythonでAspose OCRを使用して画像のOCRを実行します。画像からプレーンテキストを抽出し、AIによる後処理を適用して、迅速にクリーンな結果を得る方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: ja
lastmod: 2026-07-18
og_description: Aspose OCR と Python を使用して画像の OCR を実行します。このチュートリアルでは、画像からプレーンテキストを抽出し、AI
  ポストプロセッサを使用して精度を向上させる方法を示します。
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: 画像でOCRを実行 – Aspose AI を使用した完全な Python ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Aspose AIで画像のOCRを実行する – 完全なPythonチュートリアル
url: /ja/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI を使用した画像の OCR 実行 – 完全な Python チュートリアル

低レベルの API と格闘せずに **画像で OCR を実行** する方法を考えたことはありませんか？ あなたは一人ではありません。請求書処理、領収書スキャン、古い文書のデジタル化など、多くのプロジェクトで、画像からクリーンで検索可能なテキストを取得することが最初のステップであり、しばしば最も難しいステップです。

このガイドでは、**画像で OCR を実行** するだけでなく、Aspose の OCR エンジンを使用して **画像からプレーンテキストを抽出** する方法を示すハンズオン例を順に解説し、結果を小さな AI ポストプロセッサで仕上げます。最後までに、すぐに実行できるスクリプト、各パーツの明確な理解、そして一般的な落とし穴を回避するためのいくつかのヒントを得られます。

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="元のテキストと AI 強化テキストを表示する画像 OCR のコンソール出力"}

## 必要なもの

Before we dive, make sure you have:

- Python 3.8+ がインストールされていること（コードは Windows、macOS、Linux で動作します）。
- 有効な Aspose OCR for Python ライセンスまたは無料トライアル（パッケージは PyPI の `aspose-ocr`）
- ローカルに保存されたサンプル画像ファイル（例：スキャンした請求書や領収書）
- オプション: 後で `gpu_layers` 設定を変更する予定がある場合は GPU 対応マシン

それだけです—重厚な OCR エンジンも外部のクラウド呼び出しも不要で、pip でのインストール1回と数行のコードだけです。

## ステップ 1: Aspose OCR パッケージのインストール

Open a terminal and run:

```bash
pip install aspose-ocr
```

The package pulls in the core OCR engine plus the lightweight `aspose.ocr` namespace we’ll use throughout the tutorial.

## ステップ 2: 必要なクラスのインポート

We start by pulling in the two main classes: `AsposeAI` for AI‑enhanced post‑processing and `OcrEngine` for the actual text extraction.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*なぜ重要か*: `OcrEngine` は文字の認識という重い処理を担当し、`AsposeAI` は OCR コアを書き換えることなく、単語ごとの大文字化などのカスタムロジックをフックできるようにします。

## ステップ 3: AsposeAI インスタンスの作成（オプションのロガー）

If you want verbose logging you can pass a custom logger, but the default works fine for most cases.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## ステップ 4: 基礎モデルの調整（オプション）

Aspose OCR はデフォルトの言語モデルと共に提供されますが、HuggingFace リポジトリを指定したり CPU 実行を強制したりできます。以下では自動ダウンロードを有効にし、tiny な `gpt2` モデルを選択しています—調整可能な項目の例示です。

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **プロのコツ:** CUDA 対応 GPU がある場合、`gpu_layers` を `1` または `2` に上げると顕著な速度向上が得られます。

## ステップ 5: シンプルなポストプロセッサの登録

Our goal is to **extract plain text from image** and then make it look nicer. Here’s a tiny function that capitalizes every word. You could replace it with spell‑checking, language detection, or even a full‑blown LLM call.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

`custom_settings` 辞書は後で追加パラメータを渡すことができ、プロセッサを拡張する際に便利です。

## ステップ 6: 画像の読み込みと OCR の実行

Now we finally **run OCR on image**. We’ll retrieve two flavors of output:

1. **Plain text** – レイアウト情報のない生文字列。
2. **Structured text** – レイアウトを認識し、列やテーブルを保持したテキスト。

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **なぜ両方必要か?** `plain_text` は素早い検索に最適で、`structured_text` はテーブルを再構築したり列の配置を保持したりする際に有用です。

## ステップ 7: AI ポストプロセッサで OCR 出力を強化する

With the OCR results in hand, we hand them off to `AsposeAI.run_postprocessor`. This is where the earlier `capitalize_words` function runs.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

If you decide later to swap the post‑processor for something more sophisticated—say a grammar‑corrector—just replace the function in step 5 and the rest of the pipeline stays identical.

## ステップ 8: 結果の確認

Let’s print everything side‑by‑side so you can compare the raw OCR with the AI‑enhanced version.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### 期待される出力

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Notice how the AI post‑processor turned all‑lowercase words into capitalized ones, making the text far more readable. You can apply any transformation you like—this is just a proof of concept.

## ステップ 9: リソースのクリーンアップ

Aspose loads heavy model files into memory. When you’re done, free them to avoid memory leaks, especially in long‑running services.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| **複数の画像をループで OCR 実行できますか？** | もちろんです。`OcrEngine` を一度だけインスタンス化し、ループ内で `load_image` を呼び出し、同じ `AsposeAI` インスタンスをポストプロセッシングに再利用してください。 |
| **画像が低解像度の場合はどうすればいいですか？** | `OcrEngine` に渡す前に OpenCV で前処理（例: `cv2.resize` と `cv2.threshold`）を行ってください。 |
| **GPU は必要ですか？** | 必須ではありません。デフォルトの CPU モードでほとんどの文書は問題なく処理できます。速度が必要で互換性のある GPU がある場合のみ、`ai.config.gpu_layers` を 0 より大きく設定してください。 |
| **他の言語で画像からプレーンテキストを抽出するには？** | `recognize` を呼び出す前に `ocr_engine.language = "fr"`（または任意の ISO‑639‑1 コード）に変更してください。同じポストプロセッサは引き続き動作しますが、言語固有のロジックが必要になる場合があります。 |

## 完全な動作スクリプト

Putting everything together, here’s the complete, ready‑to‑run program:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Save this as `run_ocr_on_image.py`, replace the placeholder path with your actual image, and execute `python run_ocr_on_image.py`. You should see the before/after output just like the sample above.

## 結論

Aspose OCR を使用して画像ファイルの **OCR を実行** に成功し、**画像からプレーンテキストを抽出** する方法を示し、AI ポストプロセッサで可読性を向上させる軽量な手法を紹介しました。コアパターン—OCR

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR を使用した画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR を使用した言語選択付き画像テキスト抽出（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像からテキスト抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}