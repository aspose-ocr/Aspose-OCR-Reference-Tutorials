---
category: general
date: 2026-04-26
description: Pythonで文書をバッチOCRし、スキャンからテキストを抽出する方法。OcrEngine を使用した JSON 出力のバッチ処理をステップバイステップで学びましょう。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: ja
og_description: スキャンしたファイルを一括でOCRし、単一のスクリプトでテキストを抽出する方法。完全なコード、ヒント、エッジケースの対処法。
og_title: バッチOCRのやり方 – 高速Pythonガイド
tags:
- OCR
- Python
- Automation
title: バッチOCRの方法 – スキャンからテキストを効率的に抽出する
url: /ja/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# バッチ OCR の方法 – スキャンから効率的にテキストを抽出する

大量のスキャンした PDF を正気でいながら **バッチ OCR** したいと思ったことはありませんか？ あなただけではありません—開発者は常に「スキャンから一括でテキストを抽出するにはどうすればいいのか？」と質問しています。 良いニュースは、数行の Python でその面倒な作業をスムーズな自動パイプラインに変えられることです。

このチュートリアルでは、**スキャンからテキストを抽出**し、結果を JSON として保存し、最後に簡単なサニティチェックを行う、完全で実行可能なソリューションを順を追って説明します。外部サービスや魔法は不要です—純粋な Python と `OcrEngine` クラス、そして少しのフォルダ操作だけです。

## この記事で得られるもの

- 任意の画像フォルダに対して **バッチ OCR** を実行できる完全に機能するスクリプト。
- *why* 各行が存在する理由を明確に説明し、*what* だけではなく。
- 空フォルダ、画像以外のファイル、大規模バッチの処理に関するヒント。
- JSON 出力に抽出されたテキストが実際に含まれているかを検証する方法。

### 前提条件（最低限）

| 要件 | 重要な理由 |
|-------------|----------------|
| Python 3.8+ | モダンな構文と型ヒント |
| `OcrEngine` library (or a compatible wrapper) | OCR のコア機能 |
| A directory with scanned image files (PNG, JPG, TIFF) | 入力データ |
| Write permissions for the output folder | JSON 結果の保存 |

これらがすでに揃っているなら、素晴らしい—さっそく始めましょう。

![how to batch OCR workflow](image-placeholder.png){alt="バッチ OCR ワークフロー"}

## ステップ 1 – OCR エンジンの初期化（バッチ OCR）

何かを処理する前に、OCR エンジンのインスタンスが必要です。各画像を読み取りテキストを出力する「脳」と考えてください。エンジンを一度初期化し、バッチ全体で再利用することが最も効率的なパターンです。

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **なぜ同じインスタンスを再利用するのか？**  
> 各ファイルごとに新しいエンジンを作成すると、重いモデルをメモリに何度もロードすることになり、バッチ処理が大幅に遅くなります。1つのインスタンスでモデルを RAM に保持し、何千もの画像を遅延なく処理できます。

## ステップ 2 – スキャンフォルダを指定（スキャンからテキストを抽出）

スキャン画像はディスク上のどこかに保存されています。スクリプトにその場所を教えましょう。絶対パスを使用することで、スクリプトが別の作業ディレクトリから実行されたときに「ファイルが見つからない」エラーを防げます。

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **プロのコツ:**  
> Windows でも、スラッシュ (`/`) は `os.path.abspath` でそのまま使用できるので、バックスラッシュをエスケープする必要はありません。

## ステップ 3 – JSON 結果の出力先を選択

OCR 結果用に整理されたフォルダが欲しいでしょう。出力を元データと分離しておくことで、後でクリーンアップしたり、JSON を別のパイプラインに渡すのが簡単になります。

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **なぜプログラムでフォルダを作成するのか？**  
> ディレクトリが存在しなくてもスクリプトがクラッシュしないことを保証し、`exist_ok=True` により操作が冪等になります—エラーなくスクリプトを何度も実行できます。

## ステップ 4 – バッチ処理の実行（バッチ OCR）

ここが本題です: `ocr_engine` に `input_dir` 内のすべてのファイルを走査し、OCR を実行し、結果を `output_dir` に JSON として出力するよう指示します。`format="json"` フラグは、エンジンに結果を下流ツールが好む構造化形式でシリアライズさせます。

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### 背後で何が起きているか

1. **File discovery** – エンジンは `input_folder` を再帰的にスキャンし、隠しファイルは無視します。
2. **File validation** – サポートされている画像拡張子（`.png`, `.jpg`, `.tif` など）のみが OCR モデルに渡されます。
3. **OCR execution** – 各画像が OCR エンジンに送られ、テキスト、信頼度スコア、レイアウトデータが取得されます。
4. **JSON serialization** – 結果は同じベース名で `.json` 拡張子を付けたファイルとして `output_folder` に書き込まれます。

> **エッジケースの処理:**  
> - **空フォルダ:** エンジンは「No files found」とログに記録し、穏やかに終了します。  
> - **破損画像:** ファイルをスキップし、`batch_errors.log` にエラーエントリを記録して続行します。  
> - **大規模バッチ（10k+ ファイル）:** 各画像を個別に処理するため、メモリ使用量は低く抑えられます。

## ステップ 5 – 変換完了の確認

シンプルな `print` 文でコンソールに即時フィードバックが得られます。実運用のパイプラインでは、これをロギング呼び出しやメール通知に置き換えることもできます。

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

その行が表示されたら、`json_output` フォルダを安全に確認できます。各 JSON ファイルは概ね以下のようになります:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

これらの JSON ファイルをデータベース、検索インデックス、または任意の下流分析ツールに投入できます。

## よくある質問（と簡単な回答）

**Q: 画像ではなく PDF を処理したい場合は？**  
A: 各 PDF ページをまず画像に変換（例: `pdf2image` を使用）し、生成された PNG/JPG ファイルを `input_dir` に配置します。バッチ OCR のロジックは変更不要です。

**Q: 出力形式をプレーンテキストに変更できますか？**  
A: もちろんです。`format="json"` を `format="txt"` に置き換えると、エンジンは抽出されたテキストだけを含む `.txt` ファイルを書き出します。

**Q: スキャンが複数のサブフォルダに分かれている場合、スクリプトは再帰的に処理しますか？**  
A: はい。`batch_process` はデフォルトでディレクトリツリーを走査します。フラットな出力が必要な場合は、`flatten=True`（ライブラリがサポートしていれば）を設定するか、JSON ファイル名を後処理してください。

**Q: ラテン文字以外のスクリプトを扱うには？**  
A: `OcrEngine` を言語パラメータで初期化します（例: `OcrEngine(lang="spa+eng")`）。バッチループ自体に変更は不要です。

## プロのコツとよくある落とし穴

- **Batch size matters:** CPU のスパイクが見られる場合は、ファイル間にシンプルな `time.sleep(0.1)` を入れて処理をスロットルしてください。
- **Logging:** `print` 呼び出しを Python の `logging` モジュールに置き換えて、タイムスタンプやエラーレベルを取得します。
- **File naming collisions:** 同じベース名のスキャンが別々のサブフォルダにあると、JSON ファイルが上書きされます。相対パスのハッシュを出力名に付加して回避してください。
- **Memory leaks:** 一部の OCR バックエンドはネイティブリソースを保持します。ライブラリがクリーンアップメソッドを提供している場合は、スクリプトの最後で `ocr_engine.close()` を呼び出してください。

## 完全スクリプト – コピー＆ペースト用

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**期待されるコンソール出力**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

`json_output` 内の任意のファイルをテキストエディタで開くか、Python でロードして JSON を検証できます:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

コンソールに OCR 抽出された生テキストが表示されるはずです。

## まとめ

私たちは、スキャン画像のディレクトリ全体を **バッチ OCR** し、**スキャンからテキストを抽出** してクリーンな機械可読 JSON ファイルに変換する方法を紹介しました。アプローチは意図的にシンプルです—エンジンを一度設定し、フォルダを指すだけで、ライブラリが重い処理を担います。ここからは、

- JSON を接続する

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}