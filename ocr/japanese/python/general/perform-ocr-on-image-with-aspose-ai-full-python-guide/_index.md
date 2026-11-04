---
category: general
date: 2026-06-19
description: PythonでAspose OCRとAIポストプロセッサを使用して画像のOCRを実行する方法を学びます。自動ダウンロードモデル、スペルチェック、GPUアクセラレーションが含まれます。
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: ja
og_description: Aspose OCR と AI ポストプロセッサを使用して画像の OCR を実行します。自動ダウンロードされたモデル、スペルチェック、GPU
  加速を備えたステップバイステップガイド。
og_title: 画像でOCRを実行 – 完全なPythonチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Aspose AIで画像のOCRを実行する – 完全Pythonガイド
url: /ja/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像でOCRを実行する – 完全なPythonチュートリアル

何度も **画像でOCRを実行する** ファイルを、何十ものライブラリと格闘せずにできないかと考えたことはありませんか？ 私の経験では、問題点は主に生のOCRエンジンを扱い、そのノイズの多い出力をクリーンアップしようとすることにあります。幸い、Python 用 Aspose OCR とその AI ポストプロセッサを組み合わせれば、パイプライン全体が楽になります。

このガイドでは、実用的なエンドツーエンドの例を通して、**画像でOCRを実行する** 方法、auto‑download されたモデルで精度を向上させる方法、スペルチェックを有効にする方法、そして利用可能な場合は GPU 加速を活用する方法を詳しく解説します。最後まで読めば、請求書、レシートスキャン、文書デジタル化プロジェクトにすぐに組み込める再利用可能なスクリプトが手に入ります。

## 作成するもの

以下の小さな Python プログラムを作ります。

1. Aspose OCR エンジンを初期化し、サンプルの請求書画像を読み込む。  
2. 基本的な OCR を実行し、生のテキストを出力する。  
3. **Aspose AI** を **auto‑download されたモデル**（Hugging Face から）で構成する。  
4. **AI ポストプロセッサ**（**スペルチェック ポストプロセッサ** を含む）を実行して OCR 出力をクリーンアップする。  
5. すべてのリソースをきれいに解放する。

外部サービスや API キーは不要です—数行の Python と Aspose の力だけで完結します。

> **プロのコツ:** 十分な GPU を搭載したマシンを使用している場合、`gpu_layers` を設定するとポストプロセッシングのステップで数秒短縮できます。

## 前提条件

- Python 3.8 以上（コードは型ヒントを使用していますが、必須ではありません）。  
- `aspose-ocr` と `aspose-ai` パッケージを `pip` でインストール。  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- 参照できる場所に置いたサンプル画像（PNG、JPG、または TIFF）、例: `sample_invoice.png`。  
- （オプション）**GPU 加速** を利用したい場合は、CUDA 対応 GPU と適切なドライバーを用意。

基礎が整ったので、コードに入りましょう。

![perform OCR on image example](image.png)

## 画像でOCRを実行する – 手順 1: OCR エンジンを初期化し画像を読み込む

最初に必要なのは OCR エンジンのインスタンスです。Aspose OCR は、低レベルの画像前処理を抽象化したクリーンなオブジェクト指向 API を提供します。

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**この設定が重要な理由:**  
言語を早めに設定することで、エンジンが期待すべき文字セットを把握し、認識速度と精度が向上します。多言語文書を扱う場合は、`"en"` を `"fr"` や `"de"` など必要に応じて変更してください。

## 手順 2: 基本 OCR を実行し、生テキストを確認する

いよいよ認識を実行します。結果オブジェクトには生テキスト、信頼度スコア、必要に応じてバウンディングボックスが含まれます。

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

典型的な出力例は次のようになります（時折文字が誤認識されていることに注意）:

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

エンジンが「O」と判断した箇所が `0` になっているのが分かります。ここで **AI ポストプロセッサ** が活躍します。

## Aspose AI の構成 – auto‑download されたモデルとスペルチェック

生の OCR 結果を AI 層に渡す前に、Aspose AI に使用するモデルを指示する必要があります。ライブラリは Hugging Face から自動的にモデルをダウンロードできるため、巨大な `.bin` ファイルを自分で管理する手間が省けます。

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**設定項目の説明**

| 設定 | 機能 | 調整タイミング |
|------|------|----------------|
| `allow_auto_download` | 初回実行時に Aspose が自動でモデルを取得できるようにする。 | オフラインで事前にダウンロードしない限り `true` のままで OK。 |
| `hugging_face_repo_id` | Hugging Face 上のモデル識別子。 | ドメイン固有のモデルが必要な場合は別の ID に差し替える。 |
| `hugging_face_quantization` | 量子化レベル（`int8`、`float16` など）を選択。 | メモリが限られる環境では `int8`、高精度が必要な場合は `float16` を使用。 |
| `gpu_layers` | GPU 上で実行するトランスフォーマーレイヤー数。 | CPU のみの場合は `0`、モデル全体（例: Qwen2.5‑3B の 20 層）まで設定可能。 |

## OCR 結果に AI ポストプロセッサを適用

エンジンが準備できたら、生の OCR 出力を AI パイプラインに流すだけです。組み込みの **スペルチェック ポストプロセッサ** が明らかな誤字を修正し、追加のプロセッサを有効にすれば言語モデルが文言のリフレーズや欠落情報の補完を行います。

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

スペルチェック後の期待出力例:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

ゼロが正しい文字に置き換えられ、誤字の “Am0unt” が “Amount” に修正されていることが分かります。**AI ポストプロセッサ** は、生テキストを選択したモデルに送信し、学習結果に基づく洗練されたテキストを返す仕組みです。

### エッジケースとヒント

- **低解像度画像**: OCR エンジンが苦戦する場合は、画像を先に拡大（`Pillow` が便利）するか、`ocr_engine.ImagePreprocessingOptions` を増やしてください。  
- **非ラテン文字**: `ocr_engine.Language` を適切な ISO コード（例: 中国語は `"zh"`、アラビア語は `"ar"`）に変更します。  
- **GPU が検出されない**: `gpu_layers` 設定は互換性のある GPU が見つからない場合、自動的に CPU にフォールバックするため、追加のエラーハンドリングは不要です。  
- **モデルサイズの制限**: Qwen2.5‑3B モデルは圧縮で約 4 GB です。自動ダウンロードのために十分なディスク容量を確保してください。

## リソース解放 – クリーンなシャットダウン

Aspose オブジェクトはネイティブハンドルを保持するため、使用後に解放することがベストプラクティスです。これにより、特に長時間稼働するサービスでのメモリリークを防げます。

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

明示的なクリーンアップが好みの場合は、スクリプト全体を `try…finally` ブロックでラップすると良いでしょう。

## 完全スクリプト – コピー＆ペーストで実行可能

以下は `YOUR_DIRECTORY` を画像へのパスに置き換えればすぐに実行できる、全コードです。

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

実行コマンド:

```bash
python perform_ocr_on_image.py
```

コンソールに生テキストとクリーンアップ後のテキストが表示されます。

## 結論


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりする際に役立ちます。

- [Aspose OCR で画像からテキストを抽出する – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像を URL から取得して OCR を実行する](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}