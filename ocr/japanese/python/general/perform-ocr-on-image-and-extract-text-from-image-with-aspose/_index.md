---
category: general
date: 2026-11-20
description: Aspose OCRで画像のOCRを実行し、組み込みのAIポストプロセッサで画像からテキストを抽出します。数分で完全なPythonワークフローを学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: ja
lastmod: 2026-11-20
og_description: Aspose OCRで画像のOCRを実行し、AIによるポストプロセッシングで画像からテキストを抽出します。ステップバイステップのPythonガイドに従ってください。
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Asposeを使用して画像のOCRを実行し、画像からテキストを抽出する
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Asposeで画像のOCRを実行し、画像からテキストを抽出する
url: /ja/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像でOCRを実行し、Asposeで画像からテキストを抽出する

Pythonで画像ファイルに対して **perform OCR on image** を行う必要がある場合、このガイドではエンドツーエンドの完全なソリューションを示します。Aspose OCR と Aspose AI ポストプロセッサを組み合わせることで、**extract text from image** ファイルを確実に抽出し、軽量言語モデルで生の OCR 出力を改善できます。

このチュートリアルで行うこと：

* Aspose OCR エンジンをセットアップする。
* OCR を実行して **extract text from image** を取得する。
* 必要に応じて AI モデルをポストプロセッシング用に設定する。
* カスタムポストプロセッサ関数を登録する。
* 強化されたテキストを生成し、リソースをクリーンアップする。

この手順は任意のラスタ画像（PNG、JPEG、BMP）で動作し、`aspose-ocr` パッケージだけが必要です。

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| Python 3.8+ | Aspose SDK が必要です。 |
| `aspose-ocr` pip package | `AsposeOCR`, `AsposeAI`, およびモデル設定クラスを提供します。 |
| An image file (e.g., `sample_image.png`) | **perform OCR on image** を行うソースです。 |
| Optional: GPU support | より大きなモデルを GPU で実行する場合は、`gpu_layers` を設定します。 |

SDK をインストールするには：

```bash
pip install aspose-ocr
```

## ステップ 1: 画像で OCR を実行する

最初の操作は画像を読み込み、生のテキストを取得することです。これがコアの **perform OCR on image** 手順です。

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Why this works:** `AsposeOCR.recognize_image` は、一般的なフォントに対して速度と精度が最適化された事前学習済み光学文字認識モデルを実行します。このメソッドはプレーンな Unicode 文字列を返し、以降のすべての処理のベースラインとなります。

> **Pro tip:** 画像に複数言語が含まれる場合、`recognize_image` を呼び出す前に `ocr_engine.language = "eng+spa"`（またはサポートされている ISO‑639‑2 コード）を設定してください。

## ステップ 2: AI ポストプロセッサを初期化する

Aspose AI は、OCR の誤認識をクリーンアップしたり、句読点を修正したり、カスタムビジネスロジックを適用したりできる軽量なポストプロセッシング層を提供します。

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Why you need it:** 生の OCR は文字を誤認識しがちです（例: “0” と “O”）。AI ステップは出力を洗練させ、**extract text from image** の結果をインデックス作成や分析といった下流タスクでより信頼できるものにします。

## ステップ 3: (オプション) AI モデルを設定する

特定の Hugging Face モデルを指すようにプロセッサを設定したり、自動ダウンロードを有効にしたり、CPU 実行を強制したりできます。このステップはオプションですが、決定的な動作が必要なときに便利です。

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Explanation:**  
* `allow_auto_download` は手動でのモデル管理を不要にします。  
* `hugging_face_repo_id` でモデルを選択します。`gpt2` は短文修正においてサイズと品質のバランスが取れた選択肢です。  
* `gpu_layers` は GPU 上で実行するトランスフォーマーレイヤー数を制御します。`0` にすると純粋な CPU 実行となり、すべてのマシンで安全に動作します。

## ステップ 4: カスタムポストプロセッシング関数を登録する

Aspose AI は、生の OCR 文字列を受け取り変換後の文字列を返す任意の呼び出し可能オブジェクトをプラグインできるようにしています。以下は、すべてを大文字に変換するシンプルな例です。

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**When to customise:** ドメイン固有のクリーンアップが必要な場合（機密識別子の除去、日付の正規化、正規表現ベースの修正など）にカスタム関数を使用します。AI モデルはこの関数 *後* に実行されるため、決定論的ルールと確率的改善を組み合わせられます。

## ステップ 5: AI ポストプロセッサで OCR 結果を強化する

フルパイプラインを実行します。生の OCR テキストはまずカスタム関数に渡され、次に AI モデルに渡され、最終的に洗練された出力が得られます。

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**What you should see:**  
元の画像に “Hello world” が含まれていた場合、コンソールには次のように表示されることがあります。

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

実際のシナリオでは、AI モデルがスペルミスを修正し、欠落した句読点を追加し、改行を再フォーマットして、保存や分析に適したクリーンな **extract text from image** 結果を提供します。

## ステップ 6: 終了時にリソースを解放する

OCR エンジンと AI ポストプロセッサはどちらもネイティブリソースを割り当てます。明示的に解放することで、特に長時間稼働するサービスにおけるメモリリークを防げます。

```python
# Clean up native resources
ai_processor.free_resources()
```

重いバックエンドで `ocr_engine` をインスタンス化した場合は、同様に `ocr_engine.dispose()`（利用可能な場合）を呼び出すことができます。

## 一般的なバリエーションとエッジケース

| 状況 | 推奨される調整 |
|------|----------------|
| **大量ページを含む大きな PDF** | 各ページをループし、ラスタライズされた各ページに対して `recognize_image` を呼び出し、結果を集約します。 |
| **GPU 対応環境** | `model_config.gpu_layers` を GPU に配置したいレイヤー数（例: `4`）に設定します。CUDA ドライバがインストールされていることを確認してください。 |
| **英語以外のテキスト** | `ocr_engine.language` を適切な言語コードに変更し、必要に応じて言語固有の Hugging Face モデルを選択します。 |
| **非常にノイズの多いスキャン** | `recognize_image` を呼び出す前に OpenCV で画像を前処理（ノイズ除去、閾値処理）します。 |
| **元のケースを保持したい** | `my_post_processor` 関数を `text.upper()` ではなく、何もしない関数やより微妙なルールに置き換えます。 |

## 完全な動作例

すべてをまとめた単一スクリプトを以下に示します（`YOUR_DIRECTORY/sample_image.png` を実際のファイルパスに置き換えてください）。

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

このスクリプトを実行すると、生の OCR 出力と AI 強化版の両方がコンソールに表示され、**perform OCR on image** ファイルを確実に **extract text from image** できる単一かつ再現性のあるワークフローが実証されます。

## 結論

これで、Aspose OCR を使って **perform OCR on image** ファイルを処理し、組み込みの AI ポストプロセッサで **extract text from image** を行う方法が分かりました。本チュートリアルでカバーした内容は：

* OCR エンジンの初期化。
* 生テキスト取得のための OCR 実行。
* （オプション）軽量 Hugging Face モデルの設定。
* カスタム関数の追加と

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR & AI で画像テキスト抽出 – 完全ステップバイステップガイド](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [OCR エラー修正方法 – Aspose OCR で画像テキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Python で画像からテキスト抽出 – 完全 Aspose OCR ガイド](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}