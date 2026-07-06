---
category: general
date: 2026-04-26
description: Pythonで画像からOCRを抽出する方法 – OCR用に画像を読み込み、レシートからテキストを抽出するPython OCRの例
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: ja
og_description: Python を使って画像から OCR を抽出する方法。Python の OCR の例を学び、画像を読み込んで OCR を実行し、数分でレシートのテキストを抽出します。
og_title: PythonでOCRを抽出する方法 – 完全ガイド
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRを抽出する方法 – ステップバイステップチュートリアル
url: /ja/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを抽出する方法 – 完全ガイド

ぼやけたレシートやスキャンした請求書から **OCRを抽出する方法** を考えたことがありますか？ あなただけではありません—開発者は画像からクリーンで機械可読なテキストが必要になると、しばしば壁にぶつかります。 良いニュースは？ Python数行でレシートの画像を高信頼性の検索可能テキストに変換できます。

このチュートリアルでは、**python ocr example** を通じて **how to load image for ocr** を実演し、エンジンを実行し、85 % の信頼度閾値を満たす文字だけを保持する方法を説明します。最後までに、**extract text from receipt** 画像をドキュメントを探したり API パラメータを推測したりせずに抽出できるようになります。

## 必要なもの

- Python 3.9 以上（使用している構文は 3.8+ でも動作します）
- `aocr` パッケージ（または `OcrEngine` クラスを提供する任意の OCR ライブラリ）。以下でインストールします：

```bash
pip install aocr
```

- 参照できるフォルダーに配置したサンプルレシート画像（`receipt.png`）
- テキストエディタまたは IDE—VS Code、PyCharm、あるいはシンプルなノートブックでも構いません。

以上です。重いフレームワークも外部サービスも不要で、純粋な Python だけです。

![高信頼度 OCR 結果 – レシートから OCR を抽出する方法](/images/ocr-high-confidence.png)

*画像の代替テキスト: Python OCR を使用してレシートから OCR を抽出する方法*

## Step 1 – OCR エンジンインスタンスの作成 (how to extract ocr)

最初に行うのは OCR エンジンを起動することです。ピクセルを読み取る脳と考えてください。

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**なぜですか？** `OcrEngine` をインスタンス化すると、新しい設定オブジェクトが得られます。後から言語モデルや DPI 設定、前処理ステップを調整でき、コア処理ループに手を加える必要はありません。

## Step 2 – OCR 用画像のロード

次に、エンジンに解析したい画像を指示します。ここで **load image for ocr** キーワードが登場します。

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **プロのコツ:** 画像が別のディレクトリにある場合は、`os.path.join` を使用してプラットフォームに依存しないパスを作成してください。

**なぜこの方法で画像をロードするのか？** `Image.load` ヘルパーはファイルをエンジンが理解できる形式に読み込み、一般的なフォーマット（PNG、JPEG、TIFF）を自動的に処理します。このステップを省略したり生バイトを渡したりすると `ValueError` が発生します。

## Step 3 – OCR 処理の実行

いよいよ OCR を実行します。`process` メソッドは、認識されたシンボル、信頼度スコア、バウンディングボックスを含むリッチな結果オブジェクトを返します。

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**`ocr_result` には何が含まれますか？** 多くのライブラリでは以下が含まれます：

- `text`: 生の連結文字列。
- `symbol_confidences`: `(char, confidence)` タプルのリスト。
- `boxes`: 各文字の座標（ビジュアルデバッグに便利）。

文字ごとの信頼度にアクセスできることは、次のステップに不可欠です。

## Step 4 – 高信頼度シンボルのみを保持 (≥ 85 %)

レシートには汚れや薄い印字、背景ノイズがあることが多いです。低信頼度シンボルを除去することで、下流のパース処理が大幅に改善されます。

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**なぜ 85 % なのか？** 経験的に、0.85 前後の閾値はほとんどの印刷レシートで再現率と精度のバランスが取れます。数字が抜けている場合は閾値を下げ、文字化けが多い場合は上げてください。

## Step 5 – 高信頼度抽出テキストの出力

最後に、サニタイズされた文字列を出力（または保存）します。これが **extract text from receipt** ワークフローの核心です。

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

典型的な出力例は次のようになります：

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

この文字列を CSV ライターやデータベース、あるいは任意の下流分析パイプラインに渡すことができます。

## 完全な実行可能スクリプト

以下は `ocr_receipt.py` にコピー＆ペーストしてすぐに実行できる完全なコードスニペットです。

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

ファイルを保存し、`receipt.png` が存在することを確認した上で実行してください：

```bash
python ocr_receipt.py
```

コンソールにクリーンアップされたレシートテキストが表示されるはずです。

## エッジケースと想定シナリオ

| 状況 | 推奨される対策 |
|-----------|----------------|
| **全体的に非常に低い信頼度** | 画像を前処理する：コントラストを上げ、グレースケールに変換、またはノイズ除去フィルタ（`cv2.GaussianBlur`）を適用する。 |
| **ラテン文字以外の文字** | `OcrEngine` に言語モデルを渡す（例：スペイン語の場合 `ocr_engine.language = "spa"`）。 |
| **1枚の画像に複数のレシートがある** | 画像全体で OCR を実行し、`\n\n+`（二重改行）を検出する正規表現で結果を分割する。 |
| **生の OCR テキストも必要** | フィルタリング版と並行して `ocr_result.text` を保持し、デバッグに利用する。 |

## よくある落とし穴（回避方法）

- **ライブラリのインストール忘れ** – `pip install aocr` がインポート前に成功している必要があります。
- Windows で **パス区切り文字を間違える**（`\` と `/` の違い）。`os.path.join` を使用してください。
- **テストせずに信頼度閾値をハードコーディング** – まず数枚のレシートで簡易的に目視確認を行いましょう。
- **Unicode 正規化を無視** – 一部のレシートには特殊なダッシュ文字が含まれるため、出力を保存する場合は `unicodedata.normalize('NFKC', text)` を実行してください。

## 次のステップ – 基礎を超えて

単一のレシートから **how to extract ocr** データを取得できるようになったので、次のことを検討したくなるでしょう：

1. **レシートフォルダーをバッチ処理** – すべての PNG/JPG ファイルをループし、各結果を CSV に書き込む。
2. **データベースと統合** – `high_confidence_text` を SQLite に保存し、迅速に検索できるようにする。
3. **自然言語解析を適用** – 正規表現や `dateutil` を使って日付、合計金額、税額を抽出する。
4. **代替ライブラリを試す** – 多言語サポートや高精度が必要な場合は `pytesseract`、`easyocr`、またはクラウドサービス（Google Vision、Azure OCR）を検討してください。

これらのトピックはすべて、*python ocr example*、*extract text from receipt*、*load image for ocr*、*how to use OCR* という二次キーワードを自然に含んでいます。

## 結論

ここでは、レシート画像から **how to extract ocr** テキストを抽出し、低信頼度シンボルを除去してクリーンな結果を出力する完全な **python ocr example** を一通り解説しました。手順はシンプルで、コードは自己完結しており、規模の大きなプロジェクトにも柔軟に適応できます。

ぜひ自分のレシートで試し、信頼度閾値を調整し、バッチ処理へと拡張してみてください。ロゴが薄い、フォントが特殊などの問題に直面したら、上記のエッジケース対策を思い出しましょう。コーディングを楽しんで、OCR パイプラインが常に正確でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}