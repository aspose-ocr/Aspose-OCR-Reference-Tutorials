---
category: general
date: 2026-06-16
description: Python OCR を使って TIFF ファイルからテキストを抽出します。TIFF をテキストに変換する手順をステップバイステップで学び、マルチページ文書も簡単に処理できます。
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: ja
og_description: Python OCRでTIFFファイルからテキストを抽出します。このガイドに従ってTIFFをテキストに変換し、マルチページスキャンを処理して、きれいな結果を得ましょう。
og_title: TIFFからテキストを抽出 – 完全なPythonガイド
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: TIFFからテキストを抽出する – 完全なPythonガイド
url: /ja/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFFからテキストを抽出 – 完全なPythonガイド

**TIFF** 画像からテキストを抽出したいけれど、どこから始めればいいか分からないことはありませんか？同じようにスキャンしたアーカイブやレガシー文書を扱う開発者は多いです。朗報です！数行の Python で **TIFF をテキストに変換** でき、ファイルに何十ページもあっても瞬時に処理できます。

このチュートリアルでは、実際の例として、マルチページ TIFF を読み込み、OCR 言語をフランス語に設定し、各ページから認識されたテキストを取得する手順を解説します。最後まで読めば、すぐに実行できるスクリプトが手に入り、各ステップの重要性が理解でき、他の言語や画像形式にも応用できるようになります。

## 前提条件

作業を始める前に、以下を用意してください。

- Python 3.8 以上がインストールされていること。
- `ocr` パッケージ（または `OcrEngine` クラスを提供する互換 OCR ライブラリ）。`pip install ocr-lib` でインストールできます（使用している実際のパッケージ名に置き換えてください）。
- 処理したいマルチページ TIFF ファイル（例: `french-scans.tif`）。
- Python スクリプトの基本的な知識。

重い依存関係や外部サービスは不要です。純粋な Python と OCR エンジンだけで完結します。

---

## Step 1: Set Up the OCR Engine to **Extract Text from TIFF**

まずは OCR エンジンのインスタンスを作成し、使用する言語を指定します。今回の資料はフランス語なので、言語設定をフランス語にします。

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Why this matters:**  
言語設定は精度に大きく影響します。フランス語の「é」や「ç」などは、エンジンがデフォルトで英語になると汎用記号として誤認識されます。フランス語を明示的に指定することで、正しい文字マップが使用されます。

> **Pro tip:** 複数言語の文書を処理する場合は、各 `recognize()` 呼び出しの直前に `engine.language` を動的に変更できます。

---

## Step 2: Load the Multi‑Page TIFF You Want to **Convert TIFF to Text**

TIFF は複数のフレーム（ページ）を保持できます。OCR ライブラリはこれを抽象化してくれるので、ファイルを指すだけです。

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Edge case alert:**  
ファイルパスが間違っている、または TIFF が破損している場合、`load_from_file` メソッドは例外をスローします。実運用コードでは `try/except` でラップしてください。

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Step 3: Run OCR on the Entire Document – The Core of **Extract Text from TIFF**

エンジンに処理を任せます。`recognize()` 呼び出しはすべてのページを一括で処理し、リッチな結果オブジェクトを返します。

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**What’s happening under the hood?**  
エンジンは各フレームを順に走査し、前処理（デスキュー、二値化）を行い、ニューラルネットワークで認識し、出力を集約します。`recognize()` を一度だけ呼び出すことで、ページ間でリソースを共有でき、手動でループするより高速です。

---

## Step 4: Pull the Recognized Text Out of the JSON Result – **Convert TIFF to Text** Page by Page

結果オブジェクトは JSON にシリアライズ可能です。その JSON には `pages` 配列があり、各要素に `text` フィールドが格納されています。

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

これで、各ページの OCR 出力が格納されたクリーンな Python リストが手に入ります。

---

## Step 5: Print or Save the Text for Each Page – The Final Piece of **Extract Text from TIFF**

ページごとにループして抽出したテキストを表示しましょう。必要に応じて、各ページを別々の `.txt` ファイルに書き出すことも可能です。

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Expected Output (sample)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

OCR が成功すれば、各ページにフランス語の文がきれいに表示されます。文字化けが見られる場合は、言語設定を再確認するか、OCR 前に画像解像度を上げることを検討してください。

---

## Handling Common Pitfalls When You **Convert TIFF to Text**

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Empty `pages` array** | TIFF が正しく読み込めていない、またはフレームがゼロです。 | ファイルパスを確認し、TIFF が単一ページの PNG になっていないか確認してください。 |
| **Garbage characters** | 言語設定の不一致または画像品質が低いです。 | 正しい `engine.language` を設定し、画像を前処理（例: DPI を上げる）してください。 |
| **Memory blow‑up on huge TIFFs** | すべてのページを同時に読み込むと RAM を大量に消費します。 | チャンク単位で処理します：1 フレームだけ読み込み、認識し、次へ進む前に破棄します。 |
| **Unicode errors when printing** | コンソールのエンコーディングがアクセント文字に対応していません。 | `print(page["text"].encode('utf-8').decode('utf-8'))` を使用するか、端末を UTF‑8 に設定してください。 |

---

## Extending the Script: From **Extract Text from TIFF** to Batch Processing

基礎ができたので、次のステップを検討してください。

1. **バッチ変換** – フロー全体を `def ocr_tiff(path):` 関数にまとめ、ディレクトリ内の TIFF ファイルを順に処理します。  
2. **ファイルへの出力** – `print` の代わりに各ページのテキストを `page_{i}.txt` に書き出す、またはすべてを単一文書に結合します。  
3. **代替 OCR エンジン** – 精度向上が必要な場合は、`ocr.OcrEngine()` を Tesseract (`pytesseract`) や Azure Cognitive Services に置き換えても、同じ「TIFF からテキストを抽出」ロジックを保てます。  
4. **ポストプロセッシング** – スペルチェック、言語検出、正規表現によるクリーンアップなどで生の OCR 出力を整形します。

---

## Full, Ready‑to‑Run Script

以下はコピー＆ペースト可能な完全版コードです。基本的なエラーハンドリングと、各ページのテキストを別ファイルに保存するオプションを含んでいます。

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

このスクリプトを実行し、`tiff_file` に対象文書を指定すれば、コンソールにフランス語の文が次々と表示されます。`out_folder` を指定した場合は、`page_#.txt` ファイルが生成され、下流処理にすぐ使えます。

---

## Conclusion

今回、シンプルな Python OCR ワークフローを使って **TIFF からテキストを抽出** する方法を学び、**TIFF をテキストに変換** する手順を確実に実装できました。エンジンの言語設定からページごとの JSON 結果のループまで、各ステップの「なぜ」を理解したので、他言語や別画像形式、より大規模なバッチ処理にも柔軟に応用できます。

次は何をしますか？Tesseract へ OCR バックエンドを切り替えてみる、別の言語パックで実験する、あるいは出力を検索可能なデータベースに統合するなど、スキャン画像を検索可能なテキストに変換できる可能性は無限です。

質問や改善案があればぜひコメントで教えてください。ハッピーコーディング！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能や代替実装方法を自分のプロジェクトに取り入れる際に役立ちます。

- [Aspose OCRで画像からテキストを抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [フォルダー単位で OCR 操作を実行して画像からテキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [画像 URL から OCR を実行してテキストに変換](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}