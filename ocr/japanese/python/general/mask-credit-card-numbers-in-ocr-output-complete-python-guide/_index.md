---
category: general
date: 2026-04-26
description: AsposeAI OCR の後処理を使用して、クレジットカード番号を迅速にマスクします。PCI コンプライアンス、正規表現によるマスク、データサニタイズについて、ステップバイステップのチュートリアルで学びましょう。
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: ja
og_description: AsposeAIでOCR結果のクレジットカード番号をマスクします。このチュートリアルでは、PCIコンプライアンス、正規表現によるマスキング、データサニタイズについて解説します。
og_title: クレジットカード番号のマスク – 完全Python OCRポストプロセッシングガイド
tags:
- OCR
- Python
- security
title: OCR出力でクレジットカード番号をマスクする – 完全Pythonガイド
url: /ja/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# クレジットカード番号のマスク – 完全な Python ガイド

OCR エンジンから直接取得したテキストで **クレジットカード番号をマスク** する必要があったことはありませんか？ あなただけではありません。規制の厳しい業界では、完全な PAN（Primary Account Number）を露出させると PCI コンプライアンス監査人から厳しい指摘を受ける可能性があります。良いニュースは、数行の Python と AsposeAI の post‑processing フックを使えば、真ん中の 8 桁を自動的に隠すことができ、安全に対応できるということです。

このチュートリアルでは、実際のシナリオを通して解説します。レシート画像に OCR を実行し、PCI データをサニタイズするカスタム **OCR post‑processing** 関数を適用します。最後まで進めば、任意の AsposeAI ワークフローに組み込める再利用可能なスニペットと、エッジケースの処理やスケーリングに関する実用的なヒントが手に入ります。

## 学べること

- **AsposeAI** でカスタム post‑processor を登録する方法
- **正規表現マスク** アプローチが高速かつ信頼できる理由
- データサニタイズに関する **PCI コンプライアンス** の基本
- 複数のカードフォーマットや国際番号に対応するためのパターン拡張方法
- 期待される出力と、マスクが正しく機能したかを検証する方法

> **前提条件** – Python 3 環境が動作していること、Aspose.AI for OCR パッケージがインストールされていること（`pip install aspose-ocr`）、クレジットカード番号を含むサンプル画像（例: `receipt.png`）が用意されていることが必要です。その他の外部サービスは不要です。

---

## Step 1: Define a Post‑Processor that Masks Credit Card Numbers

ソリューションの核心は、OCR 結果を受け取り **正規表現マスク** 処理を実行し、サニタイズされたテキストを返す小さな関数です。

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Why this works:**  
- 正規表現 `(\d{4})\d{8}(\d{4})` は、Visa、MasterCard などで一般的な 16 桁の連続数字に正確にマッチします。  
- 先頭と末尾の 4 桁（`\1` と `\2`）をキャプチャすることで、デバッグに必要な情報は保持しつつ、**PCI コンプライアンス** の規則である「完全な PAN を保存しない」要件を満たします。  
- 置換文字列 `\1****\2` により、センシティブな中間の 8 桁が隠され、`1234567812345678` は `1234****5678` に変換されます。

> **プロのコツ:** 15 桁の American Express 番号にも対応したい場合は、`r'(\d{4})\d{6}(\d{5})'` のような第2パターンを追加し、両方の置換を順に実行してください。

---

## Step 2: Initialise the AsposeAI Engine

post‑processor を登録できるようにする前に、OCR エンジンのインスタンスを作成します。AsposeAI は OCR モデルとカスタム処理用のシンプルな API をバンドルしています。

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Why initialise here?**  
`AsposeAI` オブジェクトを一度作成して再利用することで、複数画像に対するオーバーヘッドが削減されます。エンジンは言語モデルをキャッシュするため、続く呼び出しが高速化され、レシートのバッチ処理に便利です。

---

## Step 3: Register the Custom Masking Function

AsposeAI は任意の呼び出し可能オブジェクトを受け付ける `set_post_processor` メソッドを提供しています。ここでは `mask_pci` 関数と（現時点では空の）設定辞書を渡します。

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**What’s happening behind the scenes?**  
後で `run_postprocessor` を呼び出すと、AsposeAI は生の OCR 結果を `mask_pci` に渡します。関数は認識されたテキストを含む軽量オブジェクト（`data`）を受け取り、新しい文字列を返します。この設計により、コア OCR は変更せずに **データサニタイズ** ポリシーを一箇所で適用できます。

---

## Step 4: Run OCR on the Receipt Image

エンジンが出力クリーンアップ方法を認識したので、画像を渡して OCR を実行します。このチュートリアルでは、すでに言語と解像度設定が済んだ `engine` オブジェクトがある前提です。

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** 事前に設定したオブジェクトがない場合は、次のように作成できます。

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` 呼び出しは、`text` 属性に生の（マスクされていない）文字列を保持したオブジェクトを返します。

---

## Step 5: Apply the Registered Post‑Processor

生の OCR データを取得したら、AI インスタンスに渡します。エンジンは自動的に先ほど登録した `mask_pci` 関数を実行します。

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Why use `run_postprocessor` instead of calling the function manually?**  
この方法により、ワークフローが一貫したものになります。特に複数の post‑processor（例: スペルチェック、言語検出）を持つ場合、AsposeAI は登録順にキューイングし、決定的な出力を保証します。

---

## Step 6: Verify the Sanitized Output

最後にサニタイズされたテキストを出力し、クレジットカード番号が正しくマスクされていることを確認します。

```python
print(final_result.text)
```

**Expected output**（抜粋）:

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

レシートにカード番号が含まれていなければ、テキストはそのまま変更されません。マスク対象が無いだけなので安心です。

---

## Handling Edge Cases and Common Variations

### Multiple Card Numbers in One Document
レシートに複数の PAN（例: ロイヤリティカードと決済カード）が含まれる場合でも、正規表現はグローバルに適用され、すべての一致が自動的にマスクされます。追加コードは不要です。

### Non‑Standard Formatting
OCR がスペースやハイフンを挿入することがあります（`1234 5678 1234 5678` や `1234-5678-1234-5678`）。このような文字を無視するパターンに拡張します：

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

追加した `[ -]?` が、数字ブロック間の任意のスペースまたはハイフンを許容します。

### International Cards
一部地域で使用される 19 桁の PAN に対応するには、パターンを次のように広げます：

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

長さが変わっても、**PCI コンプライアンス** では中間桁のマスクが必須であることを忘れないでください。

### Logging Masked Values (Optional)
監査証跡が必要な場合は、`custom_settings` 経由でフラグを渡し、関数を次のように調整します：

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

その後、以下のように登録します：

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

このスクリプトを `4111111111111111` を含むレシートで実行すると、次のように出力されます：

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

これで、RAW OCR から **データサニタイズ** までの全パイプラインが、数行の Python で完結します。

---

## Conclusion

AsposeAI の post‑processing フック、簡潔な正規表現ルーチン、そして **PCI コンプライアンス** に関するベストプラクティスを組み合わせて、OCR 結果中の **クレジットカード番号をマスク** する方法を紹介しました。ソリューションは完全に自己完結型で、OCR エンジンが読める画像であればどれでも動作し、より複雑なカードフォーマットやロギング要件にも拡張可能です。

次のステップに進みませんか？マスクした後に **データベース挿入** ルーチンで下4桁だけを保存したり、**バッチプロセッサ** を組んで一晩でフォルダ内のレシート全体を走査したりしてみましょう。また、住所標準化や言語検出といった他の **OCR post‑processing** タスクにも挑戦できます—いずれもここで示したパターンに沿って実装できます。

エッジケースやパフォーマンス、別の OCR ライブラリへの適用方法について質問があれば、下のコメント欄にどうぞ。皆さんのコードが安全であることを願っています。Happy coding, and stay secure!

![クレジットカード番号のマスクが OCR パイプラインでどのように機能するかを示す図](https://example.com/images/ocr-mask-flow.png "OCR post‑processing マスクフローの図")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}