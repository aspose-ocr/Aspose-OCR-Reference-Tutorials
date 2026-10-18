---
category: general
date: 2026-06-22
description: Aspose OCR を Python で使用して PNG ファイルからテキストを認識します。バッチ OCR 画像を学習し、GPU レイヤーを設定して高速処理を実現します。
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: ja
og_description: PythonでAspose OCRを使用してPNGファイルからテキストを認識します。このガイドでは、画像をバッチでOCRし、速度向上のためにGPUレイヤーを設定する方法を示します。
og_title: PNGからテキストを認識する – ステップバイステップ Aspose OCR チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: PNGからテキストを認識する – Aspose OCR と AI を使った完全ガイド
url: /ja/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを認識 – フル機能の Aspose OCR & AI チュートリアル

PNGファイルから**テキストを認識**したいと思ったことはありませんか？設定の細部で戸惑ったことがあるなら、あなただけではありません。領収書のデジタル化、フォームのスキャン、スクリーンショットを検索可能なテキストに変換するなど、Pythonでバッチ OCR 画像をマスターすれば、何時間も節約できます。  

このガイドでは、**PNGからテキストを認識**するだけでなく、**GPUレイヤーを設定**して速度を大幅に向上させる方法も示す、すぐに実行できるサンプルを順を追って解説します。最後まで読むと、単体のスクリプト、各ステップの明確な説明、そして自分のプロジェクトにコピペできる実用的なヒントが手に入ります。

## What This Tutorial Covers

- Aspose OCR と Aspose AI の Python パッケージのインストール  
- Hugging Face から自動ダウンロードされる AI モデルの設定  
- 最も一般的な OCR の誤字を修正する小さなポストプロセッサの作成  
- フォルダ内の PNG 全体に対して **バッチ OCR 画像** を実行するループ  
- **GPUレイヤーを設定** してグラフィックカードを活用する方法  
- 処理後のリソースを安全にクリーンアップする手順  

外部サービスは不要、隠されたマジックもなし—そのまま `.py` ファイルに貼り付けて実行できる純粋な Python コードです。

![Diagram of recognize text from png workflow](workflow.png){alt="PNGからテキストを認識するワークフロー図"}

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Aspose AI のホイールは最新のインタプリタを対象にしています |
| CUDA 対応 GPU（オプション） | **GPUレイヤーを設定** して高速化したい場合に必要です |
| 初回実行時のインターネット接続 | モデルが Hugging Face から自動ダウンロードされます |
| `pip` がインストール済み | Aspose パッケージを取得するために必要です |

これらがすでに揃っていれば、すぐに始められます。足りないものがある場合は、以下のインストール手順で補完してください。

---

## Step 1: Install Aspose OCR and Aspose AI Packages

まず、PyPI からライブラリを取得します。以下のコマンドで OCR エンジンと AI ヘルパーの両方を一度にインストールできます。

```bash
pip install aspose-ocr aspose-ai
```

*Pro tip:* 仮想環境（`python -m venv .venv`）を使用すると、パッケージがグローバルの Python インストールから分離されます。

---

## Step 2: Create and Configure the Aspose AI Instance

AI コンポーネントが OCR エンジンの「インテリジェント」モードを支えます。`Qwen/Qwen2.5-3B-Instruct-GGUF` モデルを指定し、未取得時は自動ダウンロードさせ、**GPUレイヤーを 30** に設定します（後で調整可能です）。

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Why this matters:**  
- `allow_auto_download` により、約 2 GB のモデルを手動で取得する手間が省けます。  
- `gpu_layers=30` は、対応 GPU がある環境で最初の 30 層を GPU 上で実行させ、推論時間を大幅に短縮します。  
- `int8` 量子化を使用することで、メモリ使用量を抑えつつ精度の低下を最小限に抑えられます。

---

## Step 3: Define a Simple Post‑Processor to Clean Up OCR Mistakes

OCR は完璧ではありません—特に低解像度の PNG では顕著です。頻繁に誤認識される文字を置換する簡易的な修正を行います。以下の関数は「0」を「o」に、「1」を「l」に置き換えるパターンを処理します。これはスキャンした請求書でよく見られる誤りです。

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

次のステップでこの関数を AI インスタンスに結び付け、すべての認識結果が自動的に通過するようにします。

---

## Step 4: Bind the Post‑Processor and the OCR Engine

ここで、OCR エンジン、AI モデル、ポストプロセッサをすべて接続します。

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**What’s happening under the hood?**  
`OcrEngine` は重い処理を設定した AI モデルに委譲します。モデルが生テキストを返した後、Aspose が `fix_common_errors` を呼び出して出力を整形し、最終的に表示される形にします。

---

## Step 5: Batch OCR Images – Process Every PNG in a Folder

チュートリアルの核心部分です。ディレクトリを走査し、各 `.png` を読み込んで OCR を実行し、クリーンアップ済みの結果を出力するループです。このパターンが **バッチ OCR 画像** を効率的に処理する標準的な方法です。

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Expected output** (example for a receipt):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

数十、数百のファイルがあっても、このループは順次処理し、同じ AI インスタンスを再利用することでモデル読み込みのオーバーヘッドを回避します。

---

## Step 6: Clean Up – Free Resources and Dispose the Engine

処理が終わったら、GPU メモリやその他のネイティブリソースを解放するのがベストプラクティスです。Aspose はそのための明示的なメソッドを提供しています。

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

このステップを省くと、GPU メモリが解放されずに残り、次回スクリプトを実行した際にメモリ不足エラーが発生する可能性があります。

---

## Bonus: Tweaking GPU Layers for Different Hardware

先ほど設定した `gpu_layers` の値は多くの最新 GPU にとってバランスの取れた設定ですが、ハードウェアに合わせて調整が必要な場合があります。

| GPU メモリ (GB) | 推奨 `gpu_layers` |
|-----------------|-------------------|
| 4 GB 以下       | 10‑15             |
| 6‑8 GB          | 20‑30             |
| 12 GB 以上      | 35‑45（またはそれ以上） |

GPU のメモリを超えると、エンジンは自動的に残りのレイヤーを CPU にフォールバックするため、クラッシュはしませんが速度は低下します。`nvidia‑smi` で使用状況を監視しながら実験してみてください。

---

## Common Pitfalls & How to Avoid Them

1. **Model download fails** – 環境が `https://huggingface.co` にアクセスできることを確認してください。企業ネットワークの場合はプロキシ設定（`https_proxy` 環境変数）が必要になることがあります。  
2. **GPU not detected** – 依存関係としてインストールされた `torch` ライブラリが GPU を認識しているか確認します: `import torch; print(torch.cuda.is_available())`。`False` が返る場合は、CUDA 対応の PyTorch ホイールをインストールしてください。  
3. **Incorrect image path** – Linux では `Path.glob("*.png")` は大文字小文字を区別します。`*.PNG` や `*.png` を使い分けるか、`pathlib.Path(...).rglob("*.[pP][nN][gG]")` を利用して安全に検索してください。  
4. **Post‑processor over‑corrects** – シンプルな置換は正当な “0” を “o” に変えてしまう可能性があります。代表的なサンプルでテストし、必要に応じてロジックを調整してください。

---

## Full Working Example (Copy‑Paste Ready)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Run it with:

```bash
python recognize_text_from_png_batch.py
```

各 PNG ファイル名と抽出されたテキストが、先ほどの例と同様に順に表示されます。

---

## Conclusion

私たちは **PNGからテキストを認識** するための、Aspose OCR と Aspose AI を用いた完全なプロダクション向けワークフローを一通り実装しました。ステップをひとつのスクリプトにまとめることで、簡単に **バッチ OCR 画像** を実行でき、`set gpu layers` のおかげで高速化も実現できます。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深掘りするものです。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりする際に役立ちます。

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}