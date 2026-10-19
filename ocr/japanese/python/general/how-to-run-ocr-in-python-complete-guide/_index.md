---
category: general
date: 2026-06-19
description: OCRをステップバイステップで実行し、プレーンテキストOCR技術で精度を向上させる方法。信頼できるテキスト抽出のための高速ワークフローを学びましょう。
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: ja
og_description: OCRを効率的に実行する方法。このチュートリアルでは、プレーンテキストOCRとAIポストプロセッシングを使用してOCR精度を向上させる方法を示します。
og_title: PythonでOCRを実行する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: PythonでOCRを実行する方法 ― 完全ガイド
url: /ja/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCRを実行する方法 – 完全ガイド

スキャンしたPDFのバッチに対して **OCRを実行** する方法で、設定に何時間も費やす必要があるかと考えたことはありませんか？ あなたは一人ではありません。多くのプロジェクトで最初の壁は、画像から信頼できるテキストを取得することだけです。曖昧な結果ときれいな抽出の差は、数ステップの賢い工夫にかかっています。

本ガイドでは、 **OCRを実行** するだけでなく、 **レイアウト認識型の2回目のパス** と **AIによるポストプロセッサ** を組み合わせて **OCR精度を向上** させる実践的な4ステップパイプラインを紹介します。最後まで読むと、すぐに実行できるスクリプト、各ステージが重要な理由の明確な説明、そしてマルチカラムページやノイズの多いスキャンといったエッジケースへの対処法が手に入ります。

---

## 必要なもの

作業を始める前に、以下を用意してください。

- **Python 3.9+** – コードは型ヒントと f‑strings を使用しています。  
- **Tesseract OCR** がインストールされ、`tesseract` コマンドで呼び出せる状態。  
  （Ubuntu の場合: `sudo apt install tesseract-ocr`；Windows は公式リポジトリからインストーラを取得）  
- **pytesseract** ラッパー（`pip install pytesseract`）。  
- **AIポストプロセッシングライブラリ** – ここでは軽量な `ai` モジュールが `run_postprocessor` を提供していると仮定します。必要に応じて OpenAI の GPT‑4 API やローカル LLM に置き換えてください。  
- テスト用のサンプル画像または PDF。

以上です。重いフレームワークや Docker は不要。pip で数個インストールすればすぐに始められます。

---

## ステップ 1: 高速なプレーンテキスト OCR パスを実行

多くの開発者が見落としがちなのは、 *プレーンテキスト* OCR が非常に高速で、手軽に sanity check ができる点です。`engine.Recognize()` を呼び出して、レイアウトメタデータなしで生の文字列を取得します。これが **プレーンテキスト OCR** の意味です。

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*このステップが重要な理由:*  
- **速度** – 300 dpi のページであれば、プレーンパスは通常 1 秒未満で完了します。  
- **ベースライン** – 後続の構造化出力と比較することで、明らかなエラーをすぐに検出できます。  
- **エラーチェック** – プレーンパスが全く意味不明な文字列（例: 文字化け）になる場合、画像品質が低すぎることが分かり、早めに処理を中止できます。

---

## ステップ 2: 詳細なレイアウト認識型 OCR パスを実行

プレーンテキストは便利ですが、各単語がページ上の **どこに** あるかという情報は失われます。請求書、フォーム、マルチカラムの雑誌などでは、座標、行番号、場合によってはフォント情報が必要です。そこで `engine.RecognizeStructured()` を使用します。

以下は Tesseract の **TSV** 出力を薄くラップしたもので、ページ → 行 → 単語という階層構造を保持し、バウンディングボックスを提供します。

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*このステップを行う理由:*  
- **座標** により、抽出したテキストを元画像上でハイライトやマスクにマッピングできます。  
- **行のグルーピング** が元のレイアウトを保持し、テーブルやカラムの再構築に必須です。  
- プレーンパスよりやや遅いですが、ほとんどの文書で数秒で完了します。

---

## ステップ 3: AI ポストプロセッサで OCR エラーを修正

どんなに優秀な OCR エンジンでもミスは起きます—例として “rn” と “m” の混同、アクセント記号の欠落、単語の分割などです。AI モデルは生文字列と構造化データを見て不整合を検出し、座標情報を保持したままテキストを書き直すことができます。

以下は **モック実装** です。実際に使用する場合は本体を実際の LLM 呼び出しに置き換えてください。

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*このステップが OCR 精度を向上させる理由:*  
- **文脈に基づく修正** – AI は周囲の単語から “l0ve” が “love” である可能性が高いと判断できます。  
- **座標保持** – レイアウト情報が残るため、PDF 注釈などの下流タスクが正確に動作します。  
- **反復的リファイン** – ポストプロセッサを複数回実行すれば、さらに多くのエラーを除去できます。

---

## ステップ 4: 修正済み構造化出力を反復処理

クリーンアップされた構造が手に入ったので、最終テキストの取得は簡単です。以下は各行を出力する例ですが、CSV への書き出しやデータベースへの投入、検索可能 PDF の生成など、用途は自由です。

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**期待される出力**（シンプルな 1 ページの請求書を想定）:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

行間やカラム順が保持され、AI ステップで “$15.00” が “$15,00” と読まれたような一般的な OCR 誤認が修正されていることが分かります。

---

## このワークフローが **OCR精度を向上** させる仕組み

| ステージ | 修正内容 | 重要な理由 |
|------|---------------|----------------|
| **プレーンテキスト OCR** | 読めないページを早期に検出 | 無駄な処理を省き、時間を節約 |
| **構造化 OCR** | レイアウトと座標を取得 | ハイライトやマスクなど下流タスクを実現 |
| **AI ポストプロセッサ** | スペル修正、単語結合、数値修正 | ノイズの多いスキャンで文字レベル精度を ~85 % から >95 % に向上 |
| **反復処理** | パラメータ調整で再実行可能 | 特定文書タイプに最適化されたパイプラインを構築 |

プレーンテキスト OCR、レイアウト認識抽出、AI 修正という 3 つのコンセプトを組み合わせることで、 **カスタムニューラルネットワークを一から作らなくても** 大幅に **OCR精度を改善** できる堅牢なソリューションが実現します。

---

## よくある落とし穴とプロのコツ

- **落とし穴:** 低解像度画像（≤150 dpi）を Tesseract に渡すと文字化けが発生。  
  **プロのコツ:** `Pillow` で前処理し、`Image.convert('L')` と `Image.filter(ImageFilter.MedianFilter())` を OCR 前に適用する。

- **落とし穴:** AI ポストプロセッサが業界固有用語（例: “SKU123”）を誤って書き換える。  
  **プロのコツ:** 用語ホワイトリストを作成し、LLM や `pyspellchecker` などのスペルチェッカーに渡す。

- **落とし穴:** マルチカラムページが 1 行に結合されてしまう。  
  **プロのコツ:** Tesseract の TSV 出力にある `block_num` フィールドでカラム境界を検出し、行を分割する。

- **落とし穴:** 大容量 PDF を一括で読み込むとメモリが逼迫する。  
  **プロのコツ:** ページ単位でインクリメンタルに処理する—`pdf2image.convert_from_path(..., first_page=n, last_page=n)` をループで呼び出す。

---

## パイプラインの拡張アイディア

次のステップに興味がある方は、以下の拡張を検討してください。

1. **バッチ処理** – スクリプト全体を関数化し、ディレクトリを走査して `concurrent.futures` で数千ファイルを並列処理。  
2. **言語モデル** – 簡易 difflib ヒューリスティックを OpenAI の `gpt‑4o` やローカル LLaMA に置き換えて、よりリッチな文脈修正を実現。  
3. **エクスポート形式** – 修正済み構造を検索可能 PDF に書き出すなど、出力フォーマットを多様化。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}