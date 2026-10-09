---
category: general
date: 2026-02-09
description: Aspose AI と Hugging Face モデルを使用して OCR を実行する方法 – Hugging Face モデルのダウンロード方法、OCR
  エラーの修正、GPU メモリの解放を学ぶ。
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: ja
og_description: Aspose AIでOCRを実行する方法は最初の段落で説明されています – hugging faceモデルのダウンロード方法、OCRエラーの修正、GPUメモリの解放方法をご確認ください。
og_title: Aspose AIでOCRを実行する方法 – 完全ガイド
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Aspose AIでOCRを実行する方法 – ステップバイステップガイド
url: /ja/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AIでOCRを実行する方法 – 完全ガイド

スキャンした請求書で **OCRを実行** し、タイポ修正に何時間も費やさずに完璧にクリーンな数字を取得できたらと思ったことはありませんか？ あなたは一人ではありません。実際のプロジェクトでは、従来のOCRエンジンから出力される生テキストに、余計な文字や壊れた通貨記号、乱れた数字が含まれることが多く、特に画像がノイズの多い場合に顕著です。

良いニュースは、LLMをAspose OCRに接続し、Hugging Faceのモデルをその場でダウンロードして、AIに出力を磨かせることができる点です。このチュートリアルでは、モデルの取得（はい、**download hugging face model** を自動で行う方法も示します）から、終了時にGPUリソースを解放するまで、全パイプラインを順に解説します。最後まで読むと、**OCRエラーを修正** し、控えめなGPUでも高速に動作し、メモリを無駄にしない自己クリーンアップ機能を備えた再現可能なスクリプトが手に入ります。

## 学習できること

- Aspose AIを設定し、Hugging Faceから **Qwen2.5‑3B‑Instruct‑GGUF** モデルを取得する。
- 標準のAspose OCRエンジンで画像ファイルを処理する。
- 数字と通貨記号を保持するカスタムLLMプロンプトを使用する。
- 組み込みの **free gpu memory** ルーチンでGPUメモリを解放する。
- マルチページPDFや低スペックGPUなどのエッジケースに合わせてワークフローを調整する。

> **前提条件** – Python 3.9+、`aspose-ocr` パッケージ、最初のモデルダウンロードのためのインターネット接続、そして最低4 GB VRAMを持つGPU（任意だが推奨）。GPUがない場合、スクリプトは残りの層を自動的にCPUにフォールバックします。

---

## OCRを実行し結果を向上させる方法

以下に、すぐに実行できる完全なPythonスクリプトを示します。`ocr_with_ai.py` として保存し、プレースホルダーのパスを自分のファイルに置き換えてください。

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **プロのコツ:** `gpu_layers` パラメータで、GPU上に保持するトランスフォーマーレイヤー数を決められます。メモリ不足エラーが出た場合はこの数値を下げれば、残りはCPUで実行されます – 後で `ai.free_resources()` を呼び出すことで **free gpu memory** が行われます。

### 期待される出力

サンプルの請求書でスクリプトを実行すると、以下のような出力が得られます:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

AIが `$1O0.00` の “O” を正しいゼロに修正し、ドル記号はそのまま保持していることに注目してください。これが金融文書における **correct OCR errors** の本質です。

---

## Hugging Faceモデルのダウンロード – 内部で何が起きているか

`allow_auto_download="true"` を設定すると、Aspose AIラッパーは `directory_model_path` を確認します。モデルファイルが存在しない場合、Hugging Face Hub にアクセスし、`Qwen2.5‑3B‑Instruct‑GGUF` の **int8‑quantized** バージョンを取得してローカルに保存します。この一度きりのダウンロードは通常2 GB未満で、控えめなSSDでも問題なく扱えます。

> **なぜint8か？** 8ビットに量子化することでメモリ使用量が劇的に減少し、処理後に **free gpu memory** を行いたい場合に重要です。トレードオフとして精度がわずかに低下しますが、OCRテキストの後処理においては影響はほぼ無視できます。

自分でモデルをホストしたい場合は、`.gguf` ファイルを `YOUR_DIRECTORY/Models` に配置すれば、Aspose がインターネットに再度アクセスすることなく自動的に取得します。

---

## GPUを解放する方法 – ベストプラクティス

多くのワークステーションではGPUリソースは共有資源です。スクリプト終了後にテンソルが残っていると、次のジョブで「CUDA out of memory」エラーが発生することがあります。`ai.free_resources()` の呼び出しは以下の3つを行います:

1. **基底となるトランスフォーマーを破棄** – GPU上にあるすべての重みが解放されます。
2. **PyTorchキャッシュをクリア** – 内部で `torch.cuda.empty_cache()` が呼び出されます。
3. **一時ファイルを削除** – ダウンロード中に作成されたディスク上のキャッシュが削除されます。

他のPyTorchワークロードとAspose AIを併用している場合は、手動で `torch.cuda.empty_cache()` を呼び出すこともできますが、組み込みメソッドで通常は十分です。

---

## ステップバイステップウォークスルー（副キーワード付きH2）

### Hugging Faceモデルを自動でダウンロード

`AsposeAIModelConfig` コンストラクタはHugging Face API の複雑さを隠蔽します。スクリプトを初めて実行する際にインターネット接続があることを確認してください。その後、モデルは `YOUR_DIRECTORY/Models` に保存され、以降の実行は即座に開始できます。

### 推論後にGPUメモリを解放

長時間稼働するサービス（例：Flask API）内で実行する場合、各リクエストの後に `ai.free_resources()` を呼び出してください。これによりメモリリークを防ぎ、次のリクエストが同じGPUを問題なく再利用できるようになります。

### カスタムプロンプトでOCRエラーを修正

我々の `financial_prompt` 関数は、キーが `prompt` の辞書を返します。これを任意のドメインに合わせてカスタマイズできます:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

`ai.set_post_processor(...)` 内の関数名を入れ替えれば、医療記録用の **correct OCR errors** パイプラインが完成します。

### マルチページPDFでOCRを実行する方法

Aspose OCR はPDFをそのまま処理できます:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

生の文字列を取得した後、同じLLMポストプロセッサが各ページのテキストをクリーンアップします。追加のコードは不要です。

### GPUがない場合 – GPUを解放する方法（GPUがなくても）

CPUのみのマシンでも、`ai.free_resources()` を呼び出すことは問題ありません。内部キャッシュをクリアし、RAMを解放できます。したがって **how to free gpu** のアドバイスは普遍的に適用でき、常に自分でクリーンアップすることが重要です。

---

## よくある落とし穴と解決策

| 問題 | 発生原因 | 対策 |
|-------|----------------|-----|
| **GPUのメモリ不足** | `gpu_layers` がカードに対して高すぎる設定になっている | `gpu_layers` を10または5に減らし、残りをCPUで実行する |
| **モデルがダウンロードされない** | 社内ファイアウォールが huggingface.co へのHTTPSをブロックしている | 別のネットワークでモデルを手動でダウンロードし、`directory_model_path` をローカルフォルダに設定する |
| **数字が破損する** | 数字を保持する旨の指示が不十分 | プロンプトに「数値と通貨記号はそのまま正確に保持する」旨を追加する |
| **`free_resources` が例外を投げる** | 古いバージョンの Aspose OCR を使用している | 最新の `aspose-ocr` パッケージにアップグレードする (pip install --upgrade aspose-ocr) |

---

## 完全例のまとめ

改めてスクリプトを示します。今回は各行を説明するインラインコメント付きです:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## 結論

Aspose を用いた **OCRの実行方法**、オンデマンドでの Hugging Face モデルのダウンロード、**OCRエラーを修正** するプロンプトの作成、そして最終的に **GPUメモリを解放** してワークステーションの応答性を保つ方法を網羅しました。全体のワークフローは単一の自己完結型 Python ファイルに収まり、外部スクリプトや手動でのモデル管理、GPUリソースの残留は不要です。

次のステップは？ `financial_prompt` を別のものに置き換えてみてください

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}