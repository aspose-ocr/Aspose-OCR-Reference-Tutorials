---
category: general
date: 2026-06-25
description: aocr ライブラリを使って OCR がサポートする文字をすばやく取得しましょう。OCR 文字の一覧取得方法、言語設定、Python での
  OCR エンジンのデバッグ方法を学べます。
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: ja
og_description: aocrでOCR対応文字を取得します。このガイドでは、OCR文字の一覧取得、言語の選択、Pythonでのエッジケースの処理方法を示します。
og_title: PythonでOCR対応文字を取得する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: PythonでOCR対応文字を取得する – 完全ガイド
url: /ja/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCR対応文字を取得する – 完全ガイド

OCRエンジンをいじっているときに、特定の言語で **OCRがサポートする文字** を取得したいと思ったことはありませんか？レシートスキャナや多言語ドキュメントパーサを作るとき、エンジンが認識できるグリフを正確に把握できることは命綱です。このチュートリアルでは、ライブラリのインストール、言語の設定、そして文字一覧の取得までの一連の流れを解説します。数分でOCRパイプラインのデバッグやチューニングができるようになります。

今回は **aocr** ライブラリを使用します。軽量なPython OCRエンジンで、言語機能の問い合わせがとても簡単です。このガイドが終わる頃には、 **OCR文字を一覧表示** でき、 **サポートされているOCR言語** を切り替え、さらに本番環境で問題になる前にカバレッジのギャップを見つけられるようになります。

---

## 前提条件

始める前に以下を確認してください。

* Python 3.8 以上（aocr パッケージは 3.7 のサポートを終了しています）
* インターネットに接続できるターミナルまたはコマンドプロンプト
* 基本的な Python スクリプトの知識（`print()` が書ければ問題ありません）

外部依存はほとんどありません。`aocr` の pip パッケージだけです。

---

## aocr ライブラリのインストール（OCR Engine Python）

まずは **OCRエンジン Python** の環境を整えます。aocr パッケージは PyPI に掲載されているので、以下の pip コマンド一つで完了します。

```bash
pip install aocr
```

仮想環境を使用している場合（強く推奨）、先にそれをアクティブにしてください。

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **プロのコツ:** バージョンを固定しておく（`pip install aocr==1.2.4`）と、後で予期しない API 変更に悩まされません。

---

## 言語の選択（Supported OCR Languages）

aocr にはいくつかの組み込み言語パックが同梱されています。各パックはエンジンが認識できる Unicode コードポイントの集合を定義しています。これらのパックを問い合わせるには、エンジンインスタンスの `language` 属性に設定します。

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

`aocr.Language.ENGLISH` の部分は、他の列挙値（`FRENCH`、`GERMAN` など）に置き換えられます。バンドルされていない言語を指定しようとすると、aocr は `ValueError` を送出します。そのため、まず **サポートされている OCR 言語** のリストを確認しておくと安全です。

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## 文字集合の取得（Get OCR Supported Characters）

本題に入ります：実際に **OCRがサポートする文字** を取得します。エンジンは `get_supported_characters()` という便利なメソッドを提供しており、単一文字列のリストを返します。

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

内部では、aocr は言語パックに同梱された JSON ファイルを読み込み、各 Unicode コードポイントを Python の文字列に変換しています。結果は決定的で、同じ言語バージョンでスクリプトを実行すれば毎回同じリストが得られます。

---

## サポート文字数の表示

文字数を把握すると、カバレッジの広さをすぐに評価できます。英語の場合、句読点や数字を含めて数千文字が一般的です。

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()` の呼び出しは O(1) です。Python がリスト長を内部で保持しているため、大規模なアルファベットでもパフォーマンスへの影響はありません。

---

## 最初の 100 文字をプレビュー

簡単なビジュアルチェックで、必要なシンボル（ユーロ記号やスマートクオートなど）が含まれているか確認できます。最初の 100 文字を出力してみましょう。

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join` 操作でスライスを単一文字列に結合しているので、Python のリストをそのまま出力するより読みやすくなります。

---

## 完全スクリプト – すべての手順を一括

以下は、すべてをまとめた実行可能なサンプルです。`list_supported_chars.py` という名前で保存し、ターミナルで `python list_supported_chars.py` を実行してください。

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**期待される出力（抜粋）:**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

正確な文字数は aocr のバージョンにより若干異なる場合がありますが、長いアルファベットと一般的な句読点が必ず表示されます。

---

## エッジケースの取り扱い

### 言語パックが存在しない場合は？

バンドルされていない言語を要求すると、`aocr.Language` に該当の列挙子がなくなり、`AttributeError` が発生します。以下のように簡単なチェックでガードしましょう。

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### 空の文字リスト

一部のマイナー言語では、基礎となる学習データが不完全なため空リストが返ることがあります。その場合はデフォルト（例: English）にフォールバックするか、警告を出すようにしてください。

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode 正規化

リストに結合文字（例: `e` + アクサン） が含まれることがあります。下流の処理が合成済みグリフを前提としている場合は、正規化ステップを実行します。

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## 実務向けプロティップ

* **文字リストをキャッシュ** – 何千枚もの画像を処理する場合、各イテレーションで `get_supported_characters()` を呼び出すと余計なオーバーヘッドが発生します。モジュールレベルの変数に保持するか、JSON にシリアライズして再利用しましょう。
* **クロス言語検証** – 複数言語を単一アプリで扱う際は、文字集合の交差を取って共通サブセットを見つけます。これにより、ロケール間で UI が一貫したまま設計できます。
* **OCR 失敗のデバッグ** – エンジンが文字を誤認した場合、`list_supported_chars` の出力と比較してください。対象文字がリストに無ければ、カバレッジギャップが原因であり、カスタム学習が必要になるかもしれません。
* **カスタムフォントとの組み合わせ** – aocr は Unicode 範囲を尊重しますが、フォントによって描画品質が変わります。本番で使用するフォントでサポート文字をテストし、予期せぬ問題を防ぎましょう。

---

## よくある質問

**Q: aocr バージョン 2.x でも動作しますか？**  
A: はい、`get_supported_characters()` メソッドは 1.x と 2.x で安定しています。唯一の変更点は、言語列挙子が `aocr.languages` に移動したことです。

**Q: 各文字の Unicode コードポイントも取得できますか？**  
A: もちろんです。リスト内包表記で `ord(ch)` を使えば取得できます。

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: アラビア語など右から左へのスクリプトはどうですか？**  
A: aocr には `ARABIC` 列挙子が用意されています。文字リストにはアラビア文字が含まれますが、下流の UI で RTL 表示を有効にする必要があります。

---

## 結論

このガイドで、Python の aocr ライブラリを使って **OCRがサポートする文字を取得する方法**、**サポートされている OCR 言語の切り替え方**、そして **文字一覧を取得する重要性** を理解できたはずです。完全なスクリプトと上記のヒントを活用すれば、言語カバレッジの検証、欠損グリフのデバッグ、そしてより賢い OCR アプリケーションの構築が迅速に行えます。

次のステップに進みませんか？この文字リストをカスタム単語リストフィルタと組み合わせたり、別の OCR エンジン（Tesseract、EasyOCR）で比較実験を行ったりしてみてください。探求すればするほど、OCR ソリューションは進化します。

Happy coding, and may your character sets always be complete!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するテーマを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに最適です。

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}