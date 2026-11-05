---
category: general
date: 2026-06-25
description: Aspose OCR と AI を使用して画像からテキストを抽出します。画像 OCR の読み込み方法、OCR 精度の向上、OCR エラーの修正、そして
  AI リソースの効率的な解放方法を学びましょう。
draft: false
keywords:
- extract text image
- free ai resources
- improve ocr accuracy
- load image ocr
- correct OCR errors
language: ja
og_description: Aspose OCR と AI を使用して画像からテキストを抽出します。このチュートリアルでは、画像の OCR の読み込み方法、OCR
  精度の向上、OCR エラーの修正、そして AI リソースの解放方法を示します。
og_title: Aspose OCR と AI を使ったテキスト画像抽出 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  headline: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  type: TechArticle
- description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  name: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  steps:
  - name: Import Aspose OCR and AI Modules
    text: 'We start by pulling in the two namespaces we’ll need: the core OCR engine
      and the AI helper that hosts the LLM.'
  - name: Create and Configure the OCR Engine (Enable GPU)
    text: Turning on GPU accelerates the pixel‑analysis phase, which can shave seconds
      off large batches.
  - name: Load the Image That Contains the Text to Be Recognized
    text: This is where we **load image OCR**. The path can be absolute or relative;
      just make sure the file exists.
  - name: Perform OCR and Obtain the Raw Extracted Text
    text: Now we actually **extract text image** content. The `recognize()` call returns
      a raw string, often riddled with line breaks and mis‑read characters.
  - name: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)
    text: We instantiate `AsposeAI`, configure it to pull the Qwen model from Hugging
      Face, and allocate GPU layers for inference.
  - name: Define a Simple Correction Function
    text: The function receives the raw OCR string, builds a prompt, and asks the
      model to proof‑read it. Temperature `0.0` forces deterministic output, which
      is ideal for correction tasks.
  - name: Attach the Correction Function and Clean the Raw OCR Result
    text: We bind `fix` as a post‑processor, then let the AI run over the `raw_text`.
      The result lands in `cleaned_text`.
  - name: Display the Corrected Text
    text: A quick `print` lets you verify that the pipeline succeeded.
  - name: Release AI Resources When Done
    text: Finally, we **free AI resources**. This call unloads the model from GPU
      memory, preventing leaks in long‑running services.
  type: HowTo
tags:
- OCR
- AI
- Aspose
title: Aspose OCR と AI でテキスト画像を抽出する – 完全ステップバイステップガイド
url: /ja/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR と AI を使用した画像からのテキスト抽出 – 完全ステップバイステップガイド

クラウドサービスに高額な費用をかけずに **画像からテキストを抽出** したいと思ったことはありませんか？ 同じ悩みを抱える開発者は多いです。特にノイズが多いスキャン画像では、生の OCR 出力が文字化けしたように見えることがあります。  

本ガイドでは、**画像 OCR をロード**し、**OCR 精度を向上**させ、**OCR エラーを自動修正**し、最後に **AI リソースを解放** してアプリを軽量に保つ、実行可能な完全サンプルを順を追って解説します。

最終的に得られるクリーンな文字列は、データベースや検索インデックス、あるいは downstream の NLP パイプラインにそのまま投入できます。外部ドキュメントへの不明瞭なリンクは一切なく、必要なものはすべてここに揃っています。

## 作成するもの

- 画像ファイルを読み込み、Aspose OCR で生テキストを取得。  
- デバイス上の LLM（Qwen2.5‑3B モデル）を OCR パイプラインのポストプロセッサとして組み込む。  
- 小さなプロンプトで OCR 出力を校正・修正。  
- 1 回の呼び出しでモデルと GPU メモリを解放。  

この手順を終えると、請求書、領収書、スキャンした契約書、あるいは可読文字を含む任意のビットマップ画像に対して再利用できる堅牢なパターンが手に入ります。

---

## 前提条件

| 必要条件 | 理由 |
|-------------|----------------|
| Python 3.9+ | 最新構文と型ヒントが利用可能。 |
| `aspose-ocr` パッケージ | `OcrEngine` クラスを提供。 |
| CUDA 対応 GPU（任意） | `ocr_engine.use_gpu = True` で認識速度が向上。 |
| インターネット接続（初回実行時） | Qwen モデルの自動ダウンロードに必要。 |
| 関数の基本的な知識 | 修正コールバックを設定するために必須。 |

ライブラリは以下でインストールします:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

> **プロのコツ:** CPU のみの環境の場合は `use_gpu` 行をスキップすれば、コードは自動的にフォールバックします。

---

## Aspose OCR と AI を使用した画像からのテキスト抽出

以下に、全 9 ステップに分割した完全スクリプトを示します。各ステップは簡単な説明と、コピー＆ペースト可能なコードで構成されています。

### Step 1: Import Aspose OCR and AI Modules

OCR エンジンと LLM をホストする AI ヘルパーという、必要な 2 つの名前空間をインポートします。

```python
# Step 1: Import Aspose OCR and AI modules
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai
```

> **Why?** インポートをまとめておくことでスクリプトの監査が容易になり、後から隠れた依存関係が出てくるのを防げます。

### Step 2: Create and Configure the OCR Engine (Enable GPU)

GPU を有効にすると、ピクセル解析フェーズが高速化され、大量バッチで数秒の短縮が期待できます。

```python
# Step 2: Create and configure the OCR engine (enable GPU for faster processing)
ocr_engine = aocr.OcrEngine()
ocr_engine.use_gpu = True   # Set to False if you lack a compatible GPU
```

> **Note:** `use_gpu` フラグは安全に切り替え可能です。エンジンは CUDA の有無を自動検出します。

### Step 3: Load the Image That Contains the Text to Be Recognized

ここで **画像 OCR をロード** します。パスは絶対でも相対でも構いませんが、ファイルが存在することを確認してください。

```python
# Step 3: Load the image that contains the text to be recognized
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

> **よくある落とし穴:** パスが間違っていると `FileNotFoundError` が発生します。特に大文字小文字を区別するファイルシステムでは綴りを再確認してください。

### Step 4: Perform OCR and Obtain the Raw Extracted Text

いよいよ **画像からテキストを抽出** します。`recognize()` の戻り値は、生の文字列で、改行や誤認識文字が多数含まれることが多いです。

```python
# Step 4: Perform OCR and obtain the raw extracted text
raw_text = ocr_engine.recognize()
```

この時点で `raw_text` を `print` すると、次のような出力が得られます:

```
Th1s is a s4mple test.
```

「i」の代わりに「1」、 「e」の代わりに「4」などが見られるでしょう。ここで AI ポストプロセッサの出番です。

### Step 5: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)

`AsposeAI` をインスタンス化し、Hugging Face から Qwen モデルを取得、GPU レイヤーを割り当てます。

```python
# Step 5: Set up the AI post‑processor (auto‑download Qwen2.5‑3B model)
ai_processor = aocr_ai.AsposeAI()
model_cfg = aocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_cfg.gpu_layers = 20               # Adjust based on your GPU VRAM
ai_processor.initialize(model_cfg)
```

> **Why this model?** Qwen2.5‑3B‑Instruct は中程度の GPU でも動作可能なサイズでありながら、**OCR 精度を向上** させる校正プロンプトを理解できる十分な性能を持ちます。

### Step 6: Define a Simple Correction Function

この関数は生 OCR 文字列を受け取り、プロンプトを組み立ててモデルに校正を依頼します。`temperature` を `0.0` に設定すると決定的な出力が得られ、修正タスクに最適です。

```python
# Step 6: Define a simple correction function that asks the model to proof‑read the OCR output
def fix(text, _):
    prompt = f"Proof‑read and correct the OCR text:\n\n{text}"
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=512)
```

> **How it works:** LLM が元テキストをそのまま見て、クリーンなバージョンを返します。実質的に高度なスペルチェッカー兼改行修正ツールです。

### Step 7: Attach the Correction Function and Clean the Raw OCR Result

`fix` をポストプロセッサとしてバインドし、AI が `raw_text` に対して走ります。結果は `cleaned_text` に格納されます。

```python
# Step 7: Attach the correction function as a post‑processor and clean the raw OCR result
ai_processor.set_post_processor(fix, None)
cleaned_text = ai_processor.run_postprocessor(raw_text)
```

この時点で `cleaned_text` は次のように表示されるはずです:

```
This is a simple test.
```

### Step 8: Display the Corrected Text

`print` で簡単に結果を確認できます。

```python
# Step 8: Display the corrected text
print("Cleaned text:\n", cleaned_text)
```

コンソール出力は次のようになります:

```
Cleaned text:
 This is a simple test.
```

### Step 9: Release AI Resources When Done

最後に **AI リソースを解放** します。この呼び出しでモデルが GPU メモリからアンロードされ、長時間稼働するサービスでのメモリリークを防げます。

```python
# Step 9: Release AI resources when done
ai_processor.free_resources()
```

> **Why it matters:** リソース解放を忘れると、特にサーバーレス環境でメモリ不足によるクラッシュが頻発します。各呼び出し後に必ずクリーンアップしましょう。

---

## How to Load Image OCR Efficiently

多数のファイルを処理する必要がある場合は、ロードと認識をループで回します:

```python
def ocr_one(path):
    ocr_engine.load_image(path)
    return ocr_engine.recognize()
```

同じ `ocr_engine` インスタンスを再利用することを忘れないでください。画像ごとに新しいエンジンを作成すると余計なオーバーヘッドが発生し、**画像 OCR のロード** 最適化の目的が失われます。

---

## Techniques to Improve OCR Accuracy

1. **画像の前処理** – グレースケール化、コントラスト強調、デスキュー処理を行ってからエンジンに渡す。  
2. **GPU の有効化** – Step 2 で示したように、GPU パスは信頼度スコアを向上させることが多い。  
3. **AI でのポストプロセス** – **OCR エラーを修正** するステップが最も効果的です。ルールベースのスペルチェッカーでは捉えきれない言語固有の癖も対応できます。  

この 3 つの手法を組み合わせると、実務スキャンでの単語エラー率（WER）が 30‑40 % 程度低減します。

---

## Correct OCR Errors Using an AI Post‑Processor

先ほど定義した `fix` 関数は極力シンプルにしていますが、以下のように指示を追加して機能拡張できます:

```python
def fix_with_formatting(text, _):
    prompt = (
        "You are a proofreading assistant. Return ONLY the corrected text, "
        "preserving line breaks and punctuation. Do not add explanations.\n\n"
        f"{text}"
    )
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=1024)
```

`ai_processor.set_post_processor(fix_with_formatting, None)` に差し替えると、フォーマットを保持したままよりクリーンな結果が得られます。これも **OCR 精度を向上** させる一手です。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全動作コードが含まれているので、API の追加機能習得や別実装アプローチの探索に役立ちます。

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}