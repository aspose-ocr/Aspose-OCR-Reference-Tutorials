---
category: general
date: 2026-01-07
description: 請求書処理のためにOCRを実行し、画像からテキストを抽出する方法。OCRの精度向上、OCR用画像の読み込み、請求書OCRの効率的な処理を学びましょう。
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: ja
og_description: 請求書でOCRをステップバイステップで実行する方法。画像からテキストを抽出し、OCR精度を向上させ、Aspose AIを使用して画像をOCRにロードします。
og_title: 請求書でOCRを実行する方法 – 完全なPythonガイド
tags:
- OCR
- Python
- Image Processing
title: 請求書でOCRを実行する方法 – Pythonで画像からテキストを抽出
url: /ja/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 請求書で OCR を実行する方法 – Python で画像からテキストを抽出

スキャンした請求書で **OCR を実行** し、クリーンで検索可能なテキストを取得したいと思ったことはありませんか？ あなたは一人ではありません。多くの開発者は、生の OCR 出力が綴りミスや乱れた改行、句読点の欠落でいっぱいになる壁にぶつかります。このチュートリアルでは、**画像からテキストを抽出** するだけでなく、Aspose AI モデルによるポストプロセッシングで **OCR の精度を向上** させるフルスタックソリューションを順に解説します。

**OCR 用に画像をロード** する方法、組み込みエンジンを実行する方法、そして結果を下流の分析に使えるようにする軽量スペルチェックの適用方法を見ていきます。最後まで読むと、任意の請求書処理パイプラインに組み込める再利用可能なスクリプトが手に入ります。

> **必要なもの**  
> * Python 3.9 以上  
> * `aspose-ocr` と `aspose-ai` パッケージ（`pip` でインストール）  
> * 請求書画像（PNG、JPEG、または TIFF） – 例として `sample_invoice.png` を使用します  
> * 任意: モデル推論を高速化するための最低 4 GB VRAM を搭載した GPU（スクリプトは CPU でも動作します）

## 手順 1: 必要なパッケージをインストールし、環境を準備する

**OCR 用に画像をロード** できるようになる前に、必要なライブラリが利用可能であることを確認する必要があります。Aspose OCR エンジンはシンプルな Python ラッパーと共に提供され、AI ポストプロセッサは Hugging Face の量子化モデルに依存しています。

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **プロのコツ:** GPU 加速を使用する予定がある場合は、CUDA サポート付きの `torch` をインストールしてください（`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`）。

## 手順 2: 請求書画像をロードする

画像のロードはシンプルですが、パスを生文字列（`r"..."`）として明示的に設定する理由に触れておく価値があります。これにより、Windows のパスでのエスケープ文字の誤りを防げます。

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*なぜ重要か:* `ocr.Image.load` を使用すると、画像が Aspose の最適なデフォルト設定に従って前処理（二値化、デスキュー）されることが保証され、AI の処理が入る前からすでに **OCR の精度が向上** します。

## 手順 3: 組み込み OCR エンジンを実行する

ここで実際に **OCR を実行** し、生のテキストを取得します。このステップでは、バニラ OCR 実行時に得られる典型的な出力を示します—しばしば改行が乱れ、綴りミスが散見されます。

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**典型的な生出力**（簡潔にするために省略）:

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

「Invoice」が「Invo1ce」と表示されたり、句読点が欠落していることに気付くかもしれません。そこが AI ポストプロセッサの出番です。

## 手順 4: Aspose AI モデルを設定する

使用する AI モデルは **Qwen2.5‑3B‑Instruct‑GGUF** で、ミッドレンジ GPU でも快適に動作する軽量の指示チューニング LLM です。以下の設定は、Aspose にモデルの取得先、GPU に保持するレイヤー数、長文段落を処理するためのコンテキストサイズを指示します。

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **この設定の理由:**  
> * `gpu_layers=30` は速度とメモリのバランスを取ります—推論の大部分は GPU で行われ、残りのレイヤーは CPU に残すことで OOM エラーを回避します。  
> * `context_size=4096` はモデルが請求書全体を一度に把握できるようにし、重要なフィールドが切り捨てられるのを防ぎます。

## 手順 5: シンプルなスペルチェック ポストプロセッサを作成する

`simple_spell_check` という小さな関数で AI 呼び出しをラップします。プロンプトは意図的に簡潔にし、 “Correct spelling and punctuation:” の後に生の OCR テキストを続けます。モデルはクリーンアップされたバージョンを返します。

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**動作概要:** `ai.run_prompt` はプロンプトをローカルにロードされた LLM に送信し、修正された綴り、適切な句読点、そしてより自然な改行レイアウトを持つ単一の文字列を返します。

## 手順 6: 生 OCR テキストにポストプロセッサを適用する

ここで魔法が起きます。生の OCR 出力をポストプロセッサに渡し、強化された結果を出力します。

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**サンプル強化出力**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

修正された “Invoice” の綴り、適切なコロンの使用、そして一貫した改行に注目してください—信頼できる下流パースに必要なものがすべて揃っています。

## 手順 7: リソースをクリーンアップする

OCR エンジンと AI モデルはどちらもネイティブリソースを割り当てます。特に長時間稼働するサービスでは、使用後に解放することがベストプラクティスです。

```python
ai.free_resources()
engine.dispose()
```

## 完全スクリプト – コピーしてすぐ使える

以下は、すべての手順を結びつけた完全な実行可能スクリプトです。`invoice_ocr.py` として保存し、`YOUR_DIRECTORY` を請求書画像があるフォルダに置き換えて、`python invoice_ocr.py` で実行してください。

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

スクリプトを実行すると、騒がしい生 OCR ダンプと洗練された **改善された OCR 精度** バージョンが並んで表示されます。

## よくある質問 & エッジケース

### 1. 請求書画像が複数ページの PDF の場合は？

Aspose OCR は PDF ページを直接ロードできます。画像ロード行を次のように置き換えてください:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

`page_index` を反復させて、各ページを順次処理します。

### 2. GPU のメモリが足りなくなった場合、CPU のみで使用できますか？

もちろんです。`AsposeAIModelConfig` で `gpu_layers=0` を設定してください。モデルは完全に CPU 上で実行され、速度は遅くなりますが、低スペックハードウェアでも安全に動作します。

### 3. 英語以外の請求書を処理するには？

モデルリポジトリ ID を言語固有のモデルに置き換えてください。例: 多言語サポート用に `"mistralai/Mistral-7B-Instruct-v0.2"`。パイプラインの残りは変更不要です。

### 4. 複数のポストプロセッサをチェーンできますか（例：日付のフォーマット、合計の抽出）？

はい。`ai.set_post_processor` は呼び出し可能オブジェクトのリストを受け取ります。例:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

出力はまずスペルチェックされ、次に合計が抽出されます。

## パフォーマンスのヒント & ベストプラクティス

| Tip | Why it Helps |
|-----|---------------|
| **複数の請求書をバッチ処理** – リストにロードしてループで処理する。 | Python インタプリタのオーバーヘッドを削減し、AI モデルをメモリ上でウォームに保ちます。 |
| **モデルをキャッシュ** – Web サービスで `initialize` を繰り返し呼び出すのを避ける。 | モデルのロードに約30秒かかることがあり、キャッシュすることで即時応答が得られます。 |
| **大きな画像をリサイズ** – OCR 前に幅 1500 px に縮小する。 | 画像を小さくすることで、精度を損なうことなく OCR と AI 推論の両方が高速化します。 |
| **本番環境で `allow_auto_download="false"` を設定** – デプロイ時にモデルを同梱する。 | 起動時間を決定的にし、ネットワーク障害を回避します。 |

## 結論

請求書に対する **OCR の実行方法** を、画像のロードから AI 駆動のスペルチェックで結果を洗練するまでカバーしました。これらの手順に従うことで、確実に **画像からテキストを抽出** し、**OCR の精度を向上** させ、任意の Python ベースのワークフローで **請求書 OCR をシームレスに処理** できます。

いくつか異なる請求書レイアウト（手書きのレシートやスキャンした契約書など）で試してみてください。同じパイプラインは最小限の調整で適応でき、構造化された OCR + AI の組み合わせがあらゆる文書自動化プロジェクトに汎用的なツールであることを実証します。

このガイドが役立ったと思ったら、チームメンバーと共有したり、Aspose パッケージをホストしているリポジトリにスターを付けてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}