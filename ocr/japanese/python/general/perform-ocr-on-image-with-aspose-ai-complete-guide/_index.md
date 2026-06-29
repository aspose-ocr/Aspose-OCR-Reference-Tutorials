---
category: general
date: 2026-06-28
description: Aspose AI を使用して画像の OCR を実行し、Python の数行だけで画像からプレーンテキストを抽出します。高速統合のためのステップバイステップチュートリアル。
draft: false
keywords:
- perform OCR on image
- extract plain text from image
- Aspose AI OCR
- Python OCR tutorial
- spell‑check post‑processor
- OCR result handling
language: ja
og_description: Aspose AIで画像のOCRを実行し、画像からプレーンテキストを簡単に抽出します。この簡潔なチュートリアルでフルワークフローを学びましょう。
og_title: Aspose AIで画像のOCRを実行する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose AI and extract plain text from image
    in just a few lines of Python. Step‑by‑step tutorial for fast integration.
  headline: Perform OCR on Image with Aspose AI – Complete Guide
  type: TechArticle
- questions:
  - answer: Aspose’s OCR engine works best with 300 dpi or higher. If you’re dealing
      with lower quality scans, consider pre‑processing the image (e.g., sharpening,
      binarisation) before feeding it to `engine.set_image`.
    question: What if the image is low‑resolution?
  - answer: Yes. Loop over a list of image files, re‑using the same `engine` and `ai`
      instances. Just remember to call `engine.set_image` for each new file.
    question: Can I process multiple pages?
  - answer: Only on the first run, when the AI model is downloaded. After that, everything
      runs offline from the cached directory you specified.
    question: Do I need an internet connection?
  - answer: 'Pass a language code in the options dictionary, e.g., `ai.set_post_processor(AIProcessor.SpellCheck,
      {"lang": "fr"})` for French.'
    question: How do I change the language of the spell‑check?
  type: FAQPage
tags:
- OCR
- Python
- Aspose
- AI
title: Aspose AIで画像のOCRを実行する – 完全ガイド
url: /ja/python/general/perform-ocr-on-image-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI で画像の OCR を実行する – 完全ガイド

重いライブラリと格闘せずに、画像ファイルで **perform OCR on image**（画像の OCR を実行）する方法を考えたことはありませんか？実際のアプリケーションでは、スキャンした請求書やレシートからテキストを抽出し、必要に応じてスペルチェッカーで整形するだけで十分なことが多いです。良いニュースは、Aspose AI を使えばこれがとても簡単になり、**extract plain text from image**（画像からプレーンテキストを抽出）も単一の読みやすいスクリプトで実現できることです。

このチュートリアルでは、画像の読み込み、OCR の実行、生の結果と構造化結果の取得、組み込みのスペルチェックポストプロセッサの適用、そしてリソースのクリーンアップという一連のパイプラインを順に解説します。最後まで読めば、プロジェクトにすぐ組み込める実行可能な Python のサンプルが手に入ります。

## 学べること

- Aspose OCR エンジンを初期化し、画像ファイルを渡す方法。  
- プレーン文字列出力と、レイアウト情報を保持した構造化 `OcrResult` の違い。  
- Aspose AI ブリッジを接続し、モデルを自動ダウンロード、カスタムキャッシュフォルダーを指定する方法。  
- スペルチェックポストプロセッサを使用して **extract plain text from image**（画像からプレーンテキストを抽出）し、バウンディングボックスを保持したままスペルを修正する方法。  
- AI リソースの解放とメモリリーク回避のベストプラクティス。

Aspose の事前知識は不要です。Python 3 の実行環境と任意の画像があれば始められます。さあ、始めましょう。

![画像の OCR 実行例](image.png "OCR パイプラインを示す図 – 画像の OCR を実行")

## Step 1 – OCR エンジンを初期化し画像を読み込む

最初に行うべきことは OCR エンジンを起動し、読み取り対象の画像を指定することです。エンジンはピクセルを文字に変換するスキャナーのようなものです。

```python
# Step 1: Initialise the OCR engine and load the image
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Why this matters:** `OcrEngine()` は新しいセッションを作成し、`set_image` はエンジンに解析対象のファイルを正確に指示します。このステップを省略すると、後続の `recognize` 呼び出しで例外が発生し、処理対象が無い状態になります。

## Step 2 – OCR を実行しプレーンと構造化の両方の結果を取得

ここで実際に **perform OCR on image**（画像の OCR を実行）します。Aspose は 2 種類の出力を提供します。

1. `plain_text` – 単純な文字列。単に単語だけが必要なときに最適です。  
2. `structured` – 行区切りやバウンディングボックスなどレイアウトメタデータを保持した `OcrResult` オブジェクト。

```python
# Step 2: Perform OCR – obtain plain text and structured result
plain_text = engine.recognize()                # plain string
structured = engine.recognize_structured()    # OcrResult with layout info
```

> **Pro tip:** 文字だけが必要な場合は `plain_text` を使用します（例：文書検索）。テキストを元の位置にマッピングしたい場合は `structured` を使用し、元スキャン上でエラーをハイライトするなどの処理が可能です。

## Step 3 – Aspose AI ブリッジを初期化（初回実行時にモデルをダウンロード）

Aspose AI はスペルチェックポストプロセッサを支える脳です。初回実行時にモデルが自動的にダウンロードされます。カスタムフォルダーを指定すれば、モデルをキャッシュして次回以降の起動を高速化できます。

```python
# Step 3: Initialise the Aspose AI bridge (model will be downloaded on first use)
# Optional: specify a custom directory for the cached model
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)
```

> **Why this matters:** モデルをキャッシュすると、ネットワーク呼び出しが繰り返されず、特に本番環境でアプリケーションの応答性が向上します。

## Step 4 – 組み込みスペルチェックポストプロセッサを登録

Aspose にはプレーン文字列だけでなく構造化 OCR 結果にも対応した便利なスペルチェックプロセッサが同梱されています。1 回登録すれば、OCR に起因する誤字脱字を簡単に修正できます。

```python
# Step 4: Register the built‑in spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})
```

> **Note:** 空の辞書 `{}` は、必要に応じてカスタム辞書や言語設定を渡す場所です。

## Step 5 – プレーン OCR テキストにスペルチェックを適用

ここで **extract plain text from image**（画像からプレーンテキストを抽出）しながら、同時にスペルミスを修正します。`run_postprocessor` メソッドは生文字列を受け取り、クリーンな文字列を返します。

```python
# Step 5: Apply spell‑check to the plain OCR text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)
```

**Expected output (example):**

```
Corrected: Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Why this matters:** OCR エンジンは「0」と「O」や「1」と「l」などの文字を誤認識しがちです。スペルチェック段階でこれらを正すことで、下流処理用のデータが格段にクリーンになります。

## Step 6 – 構造化 OCR 結果にスペルチェックを適用（バウンディングボックスを保持）

元のレイアウトを保持したまま、たとえばスキャン画像上で修正箇所をハイライトしたい場合は、構造化結果を同じポストプロセッサに渡します。返却されるオブジェクトは行情報を保持したままです。

```python
# Step 6: Apply spell‑check to the structured OCR result (preserves bounding boxes)
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)
```

**Sample console output:**

```
Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Pro tip:** `Lines` コレクションが `BoundingBox` 座標を保持しているので、任意のグラフィックライブラリ（Pillow、OpenCV など）を使って修正後のテキストを元画像に重ね合わせることができます。

## Step 7 – 作業完了後に AI リソースを解放

メモリリークは長時間稼働するサービスの静かな殺し屋です。作業が完了したら必ず AI リソースを解放しましょう。

```python
# Step 7: Release AI resources when done
ai.free_resources()
```

> **Why this matters:** `free_resources()` はバックグラウンドスレッドを停止し、メモリ上のモデルをクリアしてアプリケーションを軽量に保ちます。

## 完全動作サンプル

すべてをまとめた完全スクリプトです。`YOUR_DIRECTORY` を実際のパスに置き換えてそのままコピー＆ペーストで実行できます。

```python
from aspose.ocr import OcrEngine, Image
from aspose.ai import AsposeAI, AsposeAIModelConfig, AIProcessor

# Initialise OCR engine
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))

# Perform OCR
plain_text = engine.recognize()
structured = engine.recognize_structured()

# Initialise Aspose AI bridge
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)

# Register spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Correct plain text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)

# Correct structured result
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)

# Clean up
ai.free_resources()
```

スクリプトを実行すると、修正済みの出力がコンソールに表示されます。これが **perform OCR on image**（画像の OCR を実行）ワークフロー全体です。

## よくある質問とエッジケース

- **画像の解像度が低い場合は？**  
  Aspose の OCR エンジンは 300 dpi 以上で最適に動作します。低品質のスキャンの場合は、`engine.set_image` に渡す前に画像をシャープ化や二値化などで前処理すると効果的です。

- **複数ページを処理できるか？**  
  はい。画像ファイルのリストをループし、同じ `engine` と `ai` インスタンスを再利用します。各ファイルごとに `engine.set_image` を呼び出すことを忘れないでください。

- **インターネット接続は必要か？**  
  初回のモデルダウンロード時だけ必要です。その後は指定したキャッシュディレクトリからオフラインで動作します。

- **スペルチェックの言語を変更するには？**  
  オプション辞書に言語コードを渡します。例: `ai.set_post_processor(AIProcessor.SpellCheck, {"lang": "fr"})` とすればフランス語になります。

## まとめ

これで Aspose AI を使って **perform OCR on image**（画像の OCR を実行）し、**extract plain text from image**（画像からプレーンテキストを抽出）しながら一般的な OCR エラーを自動的に修正する方法がマスターできました。チュートリアルではエンジンの初期化、プレーン vs 構造化結果、モデルキャッシュ、スペルチェック統合、リソースの適切な解放について解説しました。

ここからはカスタム辞書を追加したり、修正テキストを下流の NLP パイプラインに渡したり、バウンディングボックスを元画像に描画して視覚的に検証したりと、さまざまな応用が考えられます。コードベースはしっかりした土台となるので、自由に実験してみてください。問題があればコメントで教えてくださいね。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを取り上げています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを探求したりするのに役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}