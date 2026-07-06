---
category: general
date: 2026-06-25
description: PythonでOCRを実行する方法を学び、OCR用画像の最適な読み込み方法を見つけ、さらにAspose AIのポストプロセッシングで精度を向上させましょう。
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: ja
og_description: PythonでOCRを実行する方法は？このガイドに従って画像をOCR用に読み込み、基本的な認識を行い、Aspose AIのポストプロセッシングで結果を強化しましょう。
og_title: PythonでOCRを実行する方法 – 完全なAspose OCRとAIチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: PythonでOCRを実行する方法 – 完全なAspose OCR＆AIガイド
url: /ja/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを実行する方法 – 完全な Aspose OCR & AI ガイド

低レベルの画像処理に悩むことなく **PythonでOCRを実行する方法** を知りたくありませんか？このチュートリアルでは、OCR 用の画像を読み込み、プレーンテキスト抽出を実行し、Aspose の AI 後処理で出力を磨く手順を解説します。最後まで読めば、ノイズの多いスキャン画像をクリーンで検索可能なテキストに変換できるスクリプトが手に入ります—追加のサービスは不要です。

SDK のインストールから長時間稼働するアプリでのリソース解放まで、すべてをカバーします。**OCR 用に画像を読み込む** ときに文字化けした経験がある方は、このガイドが解決策です。従来の OCR と言語モデルを組み合わせることで、人が手入力したかのような結果が得られる理由をご覧ください。

## 前提条件

作業を始める前に、以下を用意してください。

- Python 3.9 以上（コードは古いインタプリタが嫌う型ヒントを使用しています）
- 有効な Aspose OCR ライセンスまたは無料トライアル（評価目的ならコミュニティエディションで可）
- GPU がある場合は最低 4 GB VRAM（AI モデルを高速化したいときにオプションで使用）
- サンプル画像（例: `sample_invoice.png`）を参照できる場所に配置

これらが見慣れないものであっても慌てないでください。SDK のインストールはワンライナーで済み、GPU 設定は後からオフにできます。

## Step 1: Aspose OCR と依存パッケージをインストール

ターミナルを開いて次を実行します。

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

最初のパッケージで `aspose.ocr` が手に入り、2 番目で AI 後処理ユーティリティが追加されます。どちらも純粋な Python ホイールなので、コンパイルは不要です。

## Step 2: OCR 用に画像を読み込みエンジンを初期化

ここでは Aspose の `OcrEngine` を使って **OCR 用に画像を読み込む** 方法を示します。紙の書類を非常に勤勉な事務員に渡すイメージです。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **なぜ重要か:** `load_image` 呼び出しはファイルシステムと OCR エンジンをつなぐ橋渡しです。パスが間違っていると、認識が始まる前に `FileNotFoundError` が発生します。特に Windows と macOS/Linux でディレクトリ区切り文字を必ず確認してください。

## Step 3: Aspose AI 後処理を設定

Aspose AI は Hugging Face から言語モデルをダウンロードし、ローカルにキャッシュして GPU（または CPU）で推論を実行できます。以下では、ほとんどのモダンノートパソコンに収まる軽量な 30 億パラメータモデルを設定します。

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **ヒント:** CPU のみのマシンを使用している場合は `gpu_layers = 0` に設定してください。モデルは動作しますが少し遅くなります。`int8` 量子化によりメモリフットプリントは小さく保たれ、精度もほぼ維持されます。

## Step 4: カスタム後処理を登録

AI モデルには「何をすべきか」を指示するプロンプトが必要です。ここでは OCR 校正者として振る舞い、スペルミスの修正、単語の結合、アーティファクトの除去を行うよう指示します。

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **なぜカスタムプロセッサが必要か？** デフォルトの後処理は余計な説明やフォーマットを付加することがあります。独自の関数を提供することで、出力は純粋にクリーンテキストだけに限定でき、下流のインデックス作成やデータベース保存に最適です。

## Step 5: AI 強化 OCR パイプラインを実行

次に、生の OCR 出力を AI 層に渡します。エンジンは `correction_processor` を呼び出し、言語モデルと対話します。

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

文字の欠損が復元され、「0」対「O」などの一般的な OCR 誤認が修正され、改行も論理的に整理されるのが実感できるはずです。

## Step 6: 後片付け – リソース解放

Web サービスや長時間稼働するデーモン内で実行する場合、GPU メモリの解放は必須です。`free_resources` を呼び忘れると、数百件のリクエスト後に「メモリ不足」クラッシュが発生します。

```python
ocr_ai.free_resources()
```

以上で、フル OCR パイプラインが本番環境で使用できる状態になりました。

## Full Script Recap

以下が完全に実行可能なサンプルです。`ocr_with_ai.py` というファイル名で保存し、画像パスを調整した上で `python ocr_with_ai.py` を実行してください。

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Expected Output

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

「Inv0ice」が「Invoice」に変換され、金額の後に残っていた余計な「O」が消えているのが確認できます。これが AI の魔法です。

## Common Questions & Edge Cases

### GPU がない場合は？

`model_config.gpu_layers = 0` と設定し、必要に応じて `model_config.context_size` を 2048 に拡大して CPU パフォーマンスを向上させます。モデルは遅くなりますが、同等の補正品質が得られます。

### 画像が回転している場合 – `load_image` は対応できる？

Aspose OCR は自動で向きを検出しますが、極端に歪んだスキャンの場合は Pillow で事前に回転させると良いでしょう。

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### フォルダ内の複数ファイルを処理したい場合は？

パイプライン全体を `for` ループで回し、各 `enhanced_text` をリストに格納するか CSV に直接書き出します。ループ後に **一度だけ** `ocr_ai.free_resources()` を呼び出すことを忘れないでください。各ファイルごとにモデルを再初期化すると無駄が大きくなります。

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### 言語モデルを差し替えられる？

もちろんです。`model_config.hugging_face_repo_id` を任意の GGUF 互換モデル（例: `Meta/Llama-3.2-1B-Instruct-GGUF`）に変更すれば OK。ハードウェアに合わせて量子化設定を合わせてください。

## Pro Tips & Pitfalls

- **プロのコツ:** 確定的な補正を得るために `temperature=0.0` を設定しましょう。温度を上げると創造的だが誤った変更が入りやすくなります。
- **注意点:** 非常に長い文書（> 5000 文字）に注意。サンプルではコンテキストウィンドウが 1024 トークンに制限されているため、送信前に段落単位で分割してください。
- **セキュリティ上の注意:** 規制が厳しい環境で実行する場合、モデルダウンロード URL がホワイトリストに登録されていることを確認してください。`allow_auto_download` フラグで自動ダウンロードを制御できます。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}