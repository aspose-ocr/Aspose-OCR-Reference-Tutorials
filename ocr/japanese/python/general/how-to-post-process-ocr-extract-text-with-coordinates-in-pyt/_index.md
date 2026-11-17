---
category: general
date: 2026-04-26
description: OCR結果を後処理し、座標付きテキストを抽出する方法。構造化出力とAI補正を用いたステップバイステップの解決策を学びましょう。
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: ja
og_description: OCR結果を後処理し、座標付きテキストを抽出する方法。信頼できるワークフローのための包括的なチュートリアルをご覧ください。
og_title: OCRの後処理方法 – 完全ガイド
tags:
- OCR
- Python
- AI
- Text Extraction
title: OCRの後処理 – Pythonで座標付きテキストを抽出する
url: /ja/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRのポストプロセス方法 – Pythonで座標付きテキストを抽出する

生の出力がノイズが多かったり、ずれていたりして、**OCRのポストプロセス方法**が必要になったことはありませんか？ あなただけではありません。実際のプロジェクト—請求書スキャン、レシートのデジタル化、あるいはAR体験の拡張—では、OCRエンジンが生の単語を提供しますが、まだそれらをクリーンアップし、各単語がページ上のどこにあるかを追跡する必要があります。そこで、構造化出力モードとAI駆動のポストプロセッサを組み合わせると効果的です。

このチュートリアルでは、画像から**座標付きテキストを抽出**し、AIベースの補正ステップを実行し、各単語とその (x, y) 位置を出力する、完全で実行可能なPythonパイプラインを順に解説します。インポートの抜けや「ドキュメント参照」のような曖昧な手順はありません—今日からプロジェクトに組み込める自己完結型のソリューションです。

> **プロチップ:** 別のOCRライブラリを使用している場合は、“structured” または “layout” モードを探してください。概念は同じです。

---

## 前提条件

本格的に始める前に、以下が揃っていることを確認してください：

| 必要条件 | 重要性 |
|----------|--------|
| Python 3.9+ | モダンな構文と型ヒント |
| `ocr` ライブラリ（`OutputMode.STRUCTURED` をサポート、例: 架空の `myocr`） | バウンディングボックスデータに必要 |
| AI ポストプロセッシングモジュール（OpenAI、HuggingFace、またはカスタムモデル） | OCR 後の精度向上 |
| 画像ファイル（`input.png`）を作業ディレクトリに配置 | 読み込むソース |

これらに心当たりがない場合は、`pip install myocr ai‑postproc` でプレースホルダーのパッケージをインストールしてください。以下のコードにはフォールバック用スタブも含まれているので、実際のライブラリがなくてもフローをテストできます。

---

## ステップ1: OCRエンジンで構造化出力モードを有効にする  

最初に行うのは、OCRエンジンにプレーンテキスト以上の情報を返すよう指示することです。構造化出力は各単語とそのバウンディングボックス、信頼度スコアを返し、後で**座標付きテキストを抽出**する際に不可欠です。

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*重要性:* 構造化モードがなければ長い文字列しか得られず、画像上にテキストを重ね合わせたり、下流のレイアウト解析に必要な空間情報が失われます。

---

## ステップ2: 画像を認識し、単語、バウンディングボックス、信頼度を取得する  

ここで画像をエンジンに入力します。結果は単語オブジェクトのリストを含むオブジェクトで、各オブジェクトは `text`, `x`, `y`, `width`, `height`, `confidence` を提供します。

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*エッジケース:* 画像が空または読み取れない場合、`structured_result.words` は空リストになります。これをチェックし、適切に処理するのがベストプラクティスです。

---

## ステップ3: 位置情報を保持しながらAIベースのポストプロセッシングを実行する  

最高のOCRエンジンでもミスは起こります—たとえば “O” と “0” の混同や、アクセント記号の欠落などです。ドメイン固有のテキストで訓練されたAIモデルがこれらのエラーを修正できます。重要なのは、空間レイアウトを保つために元の座標を保持することです。

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*座標を保持する理由:* PDF生成やARラベリングなど多くの下流タスクは正確な配置に依存します。AIは `text` フィールドのみを変更し、`x`, `y`, `width`, `height` はそのままです。

---

## ステップ4: 修正された単語を反復し、座標付きテキストを表示する  

最後に、修正された単語をループし、各単語とその左上隅 `(x, y)` を出力します。これで**座標付きテキストを抽出**する目的が達成されます。

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**期待される出力（例）：**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

各行は修正された単語と元画像上の正確な位置を示します。

---

## 完全な動作例  

以下は全体を結びつけた単一のスクリプトです。コピーして貼り付け、インポート文を実際のライブラリに合わせて調整すれば、すぐに実行できます。

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**スクリプトの実行**

```bash
python ocr_postprocess_demo.py
```

実際のライブラリがインストールされていれば、スクリプトは `input.png` を処理します。そうでなければ、スタブ実装により外部依存なしで期待されるフローと出力を確認できます。

---

## よくある質問 (FAQ)

| 質問 | 回答 |
|------|------|
| *Tesseractでも動作しますか？* | Tesseract自体は構造化モードを標準で提供していませんが、`pytesseract.image_to_data` のようなラッパーはバウンディングボックスを返すので、同じAIポストプロセッサに渡すことができます。 |
| *左上ではなく右下の座標が必要な場合は？* | 各単語オブジェクトは `width` と `height` も提供します。`x2 = x + width`、`y2 = y + height` と計算すれば反対側の角（右下）を取得できます。 |
| *複数画像をバッチ処理できますか？* | もちろん可能です。`for image_path in Path("folder").glob("*.png"):` のループで各ステップを包み、ファイルごとに結果を収集してください。 |
| *補正に使うAIモデルはどう選べばいいですか？* | 汎用テキストの場合、OCRエラーに微調整した小型のGPT‑2が有効です。ドメイン固有のデータ（例：医療処方箋）では、ノイズ付きとクリーンなペアデータでシーケンス‑ツー‑シーケンスモデルを学習させます。 |
| *AI補正後に信頼度スコアは有用ですか？* | デバッグのために元の信頼度は保持できますが、モデルが対応していればAIが独自の信頼度を出力することもあります。 |

---

## エッジケースとベストプラクティス  

1. **空または破損した画像** – 進む前に必ず `structured_result.words` が空でないことを確認してください。  
2. **非ラテン文字スクリプト** – OCRエンジンが対象言語に設定されていることを確認し、AIポストプロセッサも同じスクリプトで訓練されている必要があります。  
3. **パフォーマンス** – AI補正はコストがかかることがあります。同じ画像を再利用する場合は結果をキャッシュするか、AIステップを非同期で実行してください。  
4. **座標系** – OCRライブラリは原点が異なる場合があります（左上か左下）。PDFやキャンバスに重ね合わせる際は適宜調整してください。  

---

## 結論  

これで、**OCRのポストプロセス方法**と、信頼性の高い**座標付きテキストの抽出**のためのエンドツーエンドの手順が手に入りました。構造化出力を有効にし、結果をAI補正レイヤーに通し、元のバウンディングボックスを保持することで、ノイズの多いOCRスキャンをクリーンで空間情報を持つテキストに変換でき、PDF生成、データ入力自動化、拡張現実のオーバーレイなどの下流タスクに活用できます。

次のステップに進みませんか？スタブAIをOpenAI の `gpt‑4o‑mini` 呼び出しに置き換えるか、パイプラインを FastAPI に統合してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}