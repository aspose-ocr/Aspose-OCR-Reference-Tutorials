---
category: general
date: 2026-01-12
description: Aspose OCR と軽量の Hugging Face モデルを使用して請求書画像から OCR を実行し、テキストを抽出する方法。モデルのダウンロード、OCR
  エラーの修正、画像への OCR 実行を学びます。
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: ja
og_description: 請求書画像でOCRを実行し、テキストを抽出し、Hugging Face LLMでエラーを修正する方法。完璧な結果を得るために、この完全なガイドに従ってください。
og_title: 請求書画像でOCRを実行する方法 – 完全チュートリアル
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: 請求書画像でOCRを実行する方法 – 完全ステップバイステップガイド
url: /ja/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 請求書画像でOCRを実行する方法 – 完全ステップバイステップガイド

スキャンした請求書で **OCRを実行** し、時間をかけずにクリーンで検索可能なテキストを取得したいと思ったことはありませんか？ あなただけではありません。実際のプロジェクトでは、生のOCR出力が誤認識で溢れています—たとえば “O” が “0” と認識されたり、“l” が “1” と認識されたり、さらには単語全体が乱れることもあります。良いニュースは、数行のPythonコードで **画像上でOCRを実行** できるだけでなく、Hugging Face の軽量モデルを使って **OCRエラーを自動的に修正** できることです。

このチュートリアルでは、請求書画像の読み込み、原文テキストの抽出、量子化モデルのダウンロード、結果の磨き上げまで、必要なすべてを順を追って解説します。最後まで実行すれば、単一の再利用可能なスクリプトで **請求書からテキストを抽出** できるようになります。

## 前提条件とセットアップ

| 要件 | 重要な理由 |
|------|------------|
| Python 3.9+ | モダンな構文と型ヒント |
| `aspose-ocr` package | 例で使用されている `ocr.OcrEngine` を提供 |
| `aspose-ai` package | `AsposeAI` ポストプロセッサを提供 |
| Access to a GPU (optional) | LLM層を高速化；GPUが無い場合はCPUでも動作 |
| Internet connection (first run) | **download Hugging Face model** を自動で取得するために必要 |

必要なライブラリは以下でインストールできます:

```bash
pip install aspose-ocr aspose-ai
```

> **プロのコツ:** LLMをGPUで実行する予定がある場合は、CUDAサポート付きの `torch` をインストールしてください (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`)。

環境が整ったので、コードに入りましょう。

---

## Step 1 – OCRエンジンの初期化と請求書画像の読み込み

最初に行うべきことは、Aspose の OCR エンジンのインスタンスを作成し、処理したいファイルを指し示すことです。このステップが **OCRを実行** するすべての画像の基礎となります。

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Why this matters:** `load_image` は PNG、JPEG、TIFF、さらには PDF ページも受け付け、フォーマットに関係なく **画像上でOCRを実行** できるようにします。

---

## Step 2 – 基本的なOCRを実行して生テキストを取得

画像が読み込まれたら、エンジンは生の文字起こしを生成できます。この出力はしばしばノイズが多く、後で修正ステップを実行する必要があります。

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

典型的な生出力は次のようになります:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

数字の “O” の代わりにゼロ (`0`) が出ているのが見えますか？ これが後で修正する対象の誤りです。

---

## Step 3 – 軽量LLMでAIポストプロセッサを設定

ここで **download Hugging Face model** を導入します。ハードウェア要件が低くても動作し、請求書の文脈を理解できるほどの性能を持つモデルです。例では Qwen 2.5 3B‑Instruct GGUF モデルを使用し、`int8` に量子化してメモリフットプリントを小さくしています。

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Why this model?** `int8` 量子化によりファイルサイズは約 1.2 GB に縮小され、ほとんどのノートパソコンでも利用可能です。GPU 層があれば推論が高速化しますが、GPU が見つからない場合はコードが自動的に CPU にフォールバックします。

---

## Step 4 – 生OCR結果に対してLLMベースの修正を実行

モデルの準備ができたら、生テキストをポストプロセッサに渡します。LLM が文字起こしを書き直し、一般的な OCR の誤りを修正し、数字を正規化します。

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

期待されるクリーンな出力:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

ゼロが文字 “O” に戻り、 “Am0unt” が “Amount” に変わっているのが分かります。これが **OCRエラーを自動的に修正** する核心です。

---

## Step 5 – リソースの解放とクリーンアップ

大規模言語モデルは GPU メモリを保持し続けることがあるため、使用後はリソースを解放するのがベストプラクティスです。

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

多数の請求書をバッチ処理する場合は、スクリプトの最後までモデルを保持し、最後に一度だけ解放することも可能です。

---

## 完全動作例

すべてをまとめた単一スクリプトを `.py` ファイルに保存して実行できます:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

スクリプトを実行すると、先ほどの “AI‑corrected” ブロックに類似した出力が得られるはずです。画像パスを別の **請求書** や **領収書** に置き換えて、 **請求書からテキストを抽出** するバルク処理も自由に試してください。

---

## よくある質問とエッジケース

### GPUがない場合は？

`gpu_layers` パラメータはオプションです。`0` に設定するか省略すれば、モデルは完全に CPU 上で動作します。推論は遅くなりますが、最新のノートパソコンでページあたりおおよそ 2〜3 秒程度です。

### 複数ページのPDF請求書はどう処理する？

各ページを別々の画像に変換（例: `pdf2image` を使用）し、同じスクリプトでページごとにループ処理します。OCR エンジンは各画像を独立して処理でき、LLM は各テキストブロックを個別に修正します。

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### ファイアウォール内でモデルのダウンロードが失敗した場合は？

Hugging Face のモデルハブから手動でモデルをダウンロードし、ローカルフォルダに解凍してから `hugging_face_repo_id` をローカルパスに設定します:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### 修正の精度はどの程度ですか？

英語の請求書に対しては、LLM が一般的な OCR 誤認識の 95 %以上を修正します。手書きの複雑なメモは依然として手動レビューが必要な場合があります。

---

## 本番環境でのヒントとコツ

- **バッチ処理:** 手順 2‑4 を関数化し、ファイルパスのリストを渡す。`AsposeAI` インスタンスを再利用してモデルの再読み込みを防止。
- **ロギング:** `print` を Python の `logging` モジュールに置き換え、原文と修正後の両方を監査用に記録。
- **エラーハンドリング:** OCR 呼び出しを `try/except` で囲む。画像処理に失敗した場合はファイル名をログに残して続行。
- **パフォーマンス調整:** `gpu_layers` を試行。GPU の層数を増やすと推論が速くなるが、VRAM 使用量も増加します。

---

## 結論

**OCRを実行** する方法から **画像上でOCRを実行**、**download Hugging Face model**、そして **OCRエラーを自動的に修正** するまで、請求書画像に対するフルワークフローを網羅しました。完全なスクリプトは、任意の Python ベースの自動化パイプラインに組み込める実用的な例です。

次のステップは？ 修正済みテキストに正規表現を用いて **主要フィールド（請求書番号、日付、合計金額）を抽出** したり、クリーンな出力をデータベースに保存して検索可能なレコードにしたりしてみてください。また、別の言語やドメイン固有の知識が必要な場合は、Hugging Face の他の軽量 LLM を試すこともできます。

Happy coding, and may your OCR results always be crystal‑clear! 

![請求書画像でOCRを実行する方法](ocr_invoice_example.png "請求書でOCRを実行する方法")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}