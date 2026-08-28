---
category: general
date: 2025-12-27
description: Aspose OCR を使用して画像からテキストを抽出し、OCR エラーを修正します。OCR 用に画像を読み込む方法と、ミスをすばやく修正する方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: ja
og_description: Aspose OCRで画像からテキストを抽出し、OCRエラーを即座に修正します。このチュートリアルに従って画像をOCRに読み込み、結果をクリーンアップしてください。
og_title: Aspose OCRで画像からテキストを抽出する – 完全ガイド
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Aspose OCRで画像からテキストを抽出する – ステップバイステップガイド
url: /ja/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト抽出 – ステップバイステップガイド

画像からテキストを**抽出**したことがありますか？しかし、乱雑な OCR 出力に悩まされたことはありませんか？あなたは一人ではありません。多くの自動化プロジェクト—たとえば請求書処理、レシートスキャン、古文書のデジタル化—では、最初のハードルは画像からクリーンで検索可能なテキストを取得することです。

このチュートリアルでは、**load image for OCR** の方法、認識の実行、そして Aspose の AI 搭載スペルチェックポストプロセッサを使用した **correct OCR errors** の手順を示す、完全に実行可能なサンプルを順に解説します。最後まで実行すれば、請求書の PNG を洗練された検索可能テキストに変換する単一スクリプトが手に入ります。

## What You’ll Learn

- Python で Aspose OCR と AI ライブラリをインストールおよびインポートする方法。  
- **load image for OCR** に必要な正確なコード（推測不要）。  
- OCR エンジンを実行し、生の文字列を取得する方法。  
- OCR がしばしば誤字を生成する理由と、組み込みのスペルチェックプロセッサで **correct OCR errors** を自動的に修正する方法。  
- マルチページ PDF や低解像度スキャンなどのエッジケースの取り扱いに関するヒント。

> **Prerequisites:** Python 3.8+、有効な Aspose OCR ライセンス（または無料トライアル）、処理したい画像ファイル（例: `invoice.png`）。

---

## 画像からテキストを抽出 – Aspose OCR の設定

何かを始める前に、正しいパッケージが必要です。Aspose は OCR エンジンを pip でインストール可能なモジュールとして配布しています。

```bash
pip install aspose-ocr
```

AI ポストプロセッサも必要な場合は、コンパニオンパッケージをインストールします。

```bash
pip install aspose-ocr-ai
```


> **プロのヒント:** パッケージは常に最新の状態に保ちましょう。執筆時点での最新バージョンは `aspose-ocr 23.12` と `aspose-ocr-ai 23.12` です。

ライブラリがシステムにインストールされたら、使用するクラスをインポートします。

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **Why this matters:** 特定のクラスだけをインポートすることで名前空間がすっきりし、認識コンポーネントとポストプロセッシングコンポーネントを明確に区別できます。

---

## OCR 用の画像の読み込み – 請求書 PNG の準備

次の論理的ステップは、エンジンに読み取るファイルを指示することです。ここで **load image for OCR** キーワードが活躍します。

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Explanation:** `OcrEngine()` はデフォルト設定（英語、オートローテーションなど）で新しいエンジンを作成します。`load_image()` メソッドはファイルパス、ストリーム、バイト配列のいずれでも受け付けるため、ディスク、ウェブ、またはメモリバッファから画像を供給できます。

### 画像読み込み時のよくある落とし穴

| 問題 | 症状 | 解決策 |
|-------|---------|-----|
| Low DPI (<300) | 文字化け、数字が抜ける | 画像を 300 dpi 以上にリサンプリングしてから読み込む |
| Incorrect color mode (CMYK) | 文字形状が誤る | Pillow の `Image.convert("RGB")` で RGB に変換 |
| Multi‑page PDF | 最初のページしか処理されない | 各ページを画像に変換し、ループで処理する |

---

## OCR を実行して生のテキストを取得する

エンジンが画像の場所を把握したので、実際に読み取ります。

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

`recognize()` 呼び出しはプレーンな Python 文字列を返します。実務では、レシートのように圧縮フォントが使われている場合、余分なスペースや誤認識文字、改行の乱れが含まれることが多いです。

> **Why we capture raw_text first:** 後でクリーンアップされたバージョンと比較できる基準が得られるため、デバッグや監査に便利です。

---

## OCRエラーの修正方法 – Aspose AI Spell‑Checkの使用

Aspose は軽量な AI ラッパーを提供しており、生の出力に対してスペルチェックポストプロセッサを実行できます。これが **how to correct OCR errors** の直接的な回答です。

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

`"spell_check"` の代わりに、用途に応じて `"grammar_check"` や `"named_entity_recognition"` などの他のプロセッサに切り替えることも可能です。

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### スペルチェックの仕組み

1. **Tokenisation** – 生文字列を単語と句読点に分割。  
2. **Dictionary Lookup** – 各トークンを英語辞書（またはカスタム辞書）と照合。  
3. **Contextual Scoring** – 小規模言語モデルを使い、修正が周囲の単語に適合するか評価。  
4. **Replacement** – 最も確率の高い修正を適用した新しい文字列を返す。

> **Edge case:** ソース言語が英語でない場合は、`AsposeAI()` 作成時に適切な言語コードを渡してください（例: `AsposeAI(language="fr")`）。

---

## クリーンアップされたテキストの検証と使用

ここまでで、`raw_text`（直接の OCR ダンプ）と `clean_text`（スペルチェック済みバージョン）の二つの変数が手に入ります。どちらを保持するかは、下流の要件次第です。

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

検索エンジン、データベース、機械学習モデルに結果を渡す場合は、常に **cleaned** バージョンを使用してください。そうしないと OCR ノイズがパイプライン全体に伝搬してしまいます。

---

## 完全な動作例

以下は `extract_invoice.py` というファイルにコピペできる完全なスクリプトです。二つの Aspose パッケージがインストール済みで、`YOUR_DIRECTORY/invoice.png` に画像があることを前提としています。

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

実行は次のコマンドで行います。

```bash
python extract_invoice.py
```

実行すると、生のダンプと整形されたバージョンが表示され、同じフォルダに `invoice_extracted.txt` というファイルが生成されます。

---

## よくある質問 (FAQ)

**Q: PDFでも動作しますか？**  
A: 直接はできません。各 PDF ページを画像に変換（例: `pdf2image` を使用）し、生成された PNG に対してスクリプトをループしてください。

**Q: 私の言語は英語ではありません—それでもスペルチェックは使えますか？**  
A: はい。`AsposeAI(language="de")` のように目的の言語コードを渡すことで、ドイツ語、スペイン語（`"es"`）などに対応できます。

**Q: OCR エンジンがテーブルレイアウトを誤検出した場合は？**  
A: Aspose OCR は `set_layout_analysis(True)` フラグを提供しています。有効にするとテーブル検出が改善されますが、処理時間が増加する可能性があります。

**Q: 非常に大規模なバッチを処理するにはどうすればよいですか？**  
A: コアロジックを関数にまとめ、スレッドプールまたは非同期 IO を使用して複数コアやマシンにわたって並列化してください。

---

## まとめ

Aspose OCR を使用した **extract text from image** の方法、**load image for OCR** の手順、そして組み込み AI スペルチェックで **correct OCR errors** を行う最もシンプルな方法を示しました。完全に実行可能なスクリプトは、請求書 PNG の読み込みからクリーンで検索可能な `.txt` ファイルの保存まで、エンドツーエンドのフローを実演しています。

ぜひ試してみてください：スペルチェックを文法チェックに置き換えたり、出力を NLP 分類器に渡したり、ドキュメント管理システムに統合したり。信頼できる、修正済みテキストが手に入れば、可能性は無限に広がります。

OCR、Aspose、Python 自動化についてさらに質問があれば、下のコメント欄にどうぞ。Happy coding!

---

![画像からテキスト抽出の例](extract_text_image.png "Aspose OCR を使用した画像からのテキスト抽出")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}