---
category: general
date: 2026-05-03
description: Aspose OCR と AI スペルチェックを使用して画像からテキストを抽出します。画像の OCR 方法、OCR 用の画像の読み込み、請求書からのテキスト認識、GPU
  リソースの解放方法を学びましょう。
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: ja
og_description: Aspose OCR と AI スペルチェックで画像からテキストを抽出する。OCR 画像の方法、OCR 用の画像の読み込み、GPU
  リソースの解放についてステップバイステップで解説。
og_title: 画像からテキストを抽出 – 完全OCR＆スペルチェックガイド
tags:
- OCR
- Aspose
- AI
- Python
title: 画像からテキストを抽出 – Aspose AI スペルチェックによる OCR
url: /ja/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – 完全OCR＆スペルチェックガイド

**画像からテキストを抽出**したいことはありますか、しかしどのライブラリが速度と精度の両方を提供するか分からなかったことはありませんか？ あなただけではありません。実際のプロジェクトでは、請求書処理、レシートのデジタル化、契約書のスキャンなど、画像からクリーンで検索可能なテキストを取得することが最初のハードルです。

良いニュースは、Aspose OCR と軽量な Aspose AI モデルを組み合わせることで、数行の Python でその作業を処理できることです。このチュートリアルでは **画像を OCR する方法** を順に説明し、画像を正しく読み込み、組み込みのスペルチェックポストプロセッサを実行し、最後に **GPU リソースを解放** してアプリのメモリ使用を抑える方法を紹介します。

このガイドの最後までに、**請求書からテキストを認識**できるようになり、一般的な OCR の誤りを自動的に修正し、次のバッチのために GPU をクリーンに保つことができます。

---

## 必要なもの

- Python 3.9 以上（コードは型ヒントを使用していますが、以前の 3.x バージョンでも動作します）
- `aspose-ocr` と `aspose-ai` パッケージ（`pip install aspose-ocr aspose-ai` でインストール）
- CUDA 対応 GPU はオプションです。GPU が見つからない場合はスクリプトが CPU にフォールバックします。
- 例として `sample_invoice.png` のような画像を、参照できるフォルダーに配置します。

重い機械学習フレームワークや大容量モデルのダウンロードは不要です—ほとんどの GPU に快適に収まる小さな Q4‑K‑M 量子化モデルだけです。

---

## ステップ 1: OCR エンジンの初期化 – 画像からテキストを抽出

最初に行うのは `OcrEngine` インスタンスを作成し、期待する言語を指定することです。ここでは英語を選択し、プレーンテキスト出力を要求します。これは下流の処理に最適です。

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**この設定が重要な理由:** 言語を設定することで文字セットが絞られ、精度が向上します。プレーンテキストモードは、画像からテキストを抽出したいだけのときに通常不要なレイアウト情報を除去します。

---

## ステップ 2: OCR 用に画像をロード – 画像を OCR する方法

ここでエンジンに実際の画像を渡します。`Image.load` ヘルパーは一般的なフォーマット（PNG、JPEG、TIFF）を理解し、ファイル I/O の細かい違いを抽象化します。

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**ヒント:** ソース画像が大きい場合は、エンジンに送る前にリサイズすることを検討してください。サイズを小さくすると、認識品質を損なうことなく GPU メモリ使用量を削減できます。

---

## ステップ 3: Aspose AI モデルの構成 – 請求書からテキストを認識

Aspose AI には自動ダウンロード可能な小さな GGUF モデルが同梱されています。例では `Qwen2.5‑3B‑Instruct‑GGUF` リポジトリを使用し、`q4_k_m` に量子化しています。また、ランタイムに GPU 上で 20 層を割り当てるよう指示し、速度と VRAM 使用量のバランスを取ります。

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**内部的には:** 量子化モデルはディスク上で約 1.5 GB で、フルプレシジョンモデルのごく一部です。それでも、典型的な OCR の綴りミスを検出できるほどの言語的ニュアンスを保持しています。

---

## ステップ 4: AsposeAI の初期化とスペルチェックポストプロセッサの添付

Aspose AI には既製のスペルチェックポストプロセッサが含まれています。これを添付することで、すべての OCR 結果が自動的にクリーンアップされます。

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**ポストプロセッサを使用する理由:** OCR エンジンはしばしば “Invoice” を “Invo1ce”、 “Total” を “T0tal” と誤認識します。スペルチェックは軽量言語モデルを生文字列に適用し、カスタム辞書を作成せずにこれらのエラーを修正します。

---

## ステップ 5: OCR 結果にスペルチェックポストプロセッサを実行

すべてが接続された状態で、1 回の呼び出しで修正されたテキストが得られます。また、元のテキストとクリーンアップ後のテキストの両方を出力し、改善を確認できるようにします。

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

請求書の典型的な出力は次のようになります：

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

“Invo1ce” が正しい単語 “Invoice” に変換されていることに注目してください。これが組み込み AI スペルチェックの力です。

---

## ステップ 6: GPU リソースの解放 – GPU リソースを安全に解放

長時間稼働するサービス（例: 1 分で数十件の請求書を処理する Web API）で実行する場合、各バッチ後に GPU コンテキストを解放する必要があります。そうしないとメモリリークが発生し、最終的に “CUDA out of memory” エラーになります。

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**プロのコツ:** 例外が発生した場合でも必ず実行されるよう、`finally` ブロックまたはコンテキストマネージャ内で `free_resources()` を呼び出してください。

---

## 完全な動作例

すべての要素を組み合わせると、任意のプロジェクトに組み込める自己完結型スクリプトが得られます。

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

ファイルを保存し、画像へのパスを調整して `python extract_text_from_image.py` を実行してください。コンソールにクリーンアップされた請求書テキストが表示されるはずです。

---

## よくある質問 (FAQ)

**Q: CPU のみのマシンでも動作しますか？**  
A: もちろんです。GPU が検出されない場合、Aspose AI は CPU 実行にフォールバックしますが、速度は遅くなります。`model_cfg.gpu_layers = 0` を設定すれば CPU を強制できます。

**Q: 請求書が英語以外の言語の場合はどうすればよいですか？**  
A: `ocr_engine.language` を適切な enum 値に変更してください（例: `aocr.Language.Spanish`）。スペルチェックモデルは多言語対応ですが、言語固有のモデルを使用した方がより良い結果が得られることがあります。

**Q: 複数の画像をループで処理できますか？**  
A: はい。ロード、認識、ポストプロセッシングのステップを `for` ループ内に移動すれば可能です。同じ AI インスタンスを再利用する場合は、ループ後または各バッチ後に `ocr_ai.free_resources()` を呼び出すことを忘れないでください。

**Q: モデルのダウンロードサイズはどれくらいですか？**  
A: 量子化された `q4_k_m` バージョンで約 1.5 GB です。最初の実行後にキャッシュされるため、以降の実行は瞬時です。

---

## 結論

このチュートリアルでは Aspose OCR を使用して **画像からテキストを抽出** する方法、小さな AI モデルの構成、スペルチェックポストプロセッサの適用、そして安全に **GPU リソースを解放** する方法を示しました。このワークフローは画像のロードから後始末までを網羅し、**請求書からテキストを認識**するシナリオに信頼できるパイプラインを提供します。

次のステップは？ スペルチェックをカスタムエンティティ抽出モデルに置き換えてみてください

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}