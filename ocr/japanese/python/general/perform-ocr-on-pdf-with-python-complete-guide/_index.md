---
category: general
date: 2026-06-25
description: PythonでPDFにOCRを実行する—OCR用にPDFを読み込む方法、PDFページからテキストを抽出する方法、そして認識されたテキストを効率的にプレビューする方法を学びましょう。
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: ja
og_description: PythonでPDFにOCRを実行します。このガイドでは、OCR用にPDFを読み込む方法、PDFページからテキストを抽出する方法、そして認識されたテキストをすばやくプレビューする方法を示します。
og_title: PythonでPDFのOCRを実行する – ステップバイステップチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: PythonでPDFにOCRを実行する – 完全ガイド
url: /ja/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFのOCRを実行する – 完全ガイド

PDFファイルに **OCR を実行** したいけれど、どこから手を付ければいいか分からないことはありませんか？大量のスキャン済み契約書や、通常のテキスト抽出ツールがまったく機能しない巨大なハンドブックがあるかもしれません。要するに、 **PDF を OCR 用に読み込み**、テキストを抽出し、メモリを大量に消費せずに簡単にプレビューしたい、ということです。

ここがその答えです。このチュートリアルでは、 **PDF ページからテキストを抽出** する完全に動作する Python スクリプトを解説し、 **認識されたテキストをプレビュー** する方法、そして **大きな PDF を効率的に OCR する** という古典的な課題への対処法も紹介します。

最後まで読むと、すぐに実行できるプログラム、各設定項目の明確な理解、そして初心者が陥りがちな落とし穴を回避するためのヒントが手に入ります。

---

## 学べること

- `aocr` ライブラリを使って **PDF を OCR 用に読み込む** 方法
- **PDF のページを1枚ずつ OCR** する具体的手順
- メモリ使用量を抑えながら **PDF ページからテキストを抽出** する方法
- 結果を **認識されたテキストとしてプレビュー** し、正しさを確認する手順
- **大きな PDF** を RAM を使い果たさずに処理する戦略

> **Tip:** 本ガイドは Python 3.9 以上がインストールされており、仮想環境の基本的な使い方を知っていることを前提としています。Python が初めての方は、まず virtualenv を作成してください。後々のトラブル防止になります。

---

## 前提条件

| 必要条件 | 理由 |
|-------------|----------------|
| `aocr` Python パッケージ（または互換性のある OCR エンジン） | スクリプト全体で使用する `OcrEngine` クラスを提供します。 |
| `pip` と仮想環境 | 依存関係をシステム Python から分離して管理できます。 |
| 一時的な画像抽出用の十分なディスク容量 | 一部の OCR エンジンはページ画像をディスクに書き出してから処理します。 |
| 任意: 進捗バー用の `tqdm` | **大きな PDF を OCR する** 作業の UX を向上させます。 |

必須パッケージは以下でインストールできます：

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

PDF がパスワードで保護されている場合は、後述の「エッジケース」セクションでパスワードを指定してください。

---

## 手順 1: OCR エンジンのセットアップ – OCR エンジンを作成

まずは OCR エンジンのインスタンスを作ります。これは各ページの画像を読み取り、プレーンテキストを出力する「脳」に相当します。

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **`max_memory_mb` を設定する理由**  
> OCR エンジンはページ画像を RAM にキャッシュすることがあります。メモリ上限を設けることで、500 ページの契約書でもスクリプトがクラッシュするのを防げます。

---

## 手順 2: PDF を OCR 用に読み込み、設定を構成

ここで実際に **PDF を OCR 用に読み込み** ます。パスは絶対でも相対でも構いませんが、ファイルが存在することを確認してください。

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

PDF が暗号化されている場合、`engine.load_pdf` は例外を投げます。その際は `engine.load_pdf(pdf_path, password="secret")` のようにパスワードを渡してください（詳細は後述）。

---

## 手順 3: PDF ページからテキストを抽出 – コアループ

ここで **PDF のページごとに OCR を実行** します。さらに **認識されたテキストをプレビュー** し、最初の数百文字で正しく処理されているか確認します。

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **プロのコツ:** `tqdm` の進捗バーは視覚的な手がかりを提供します。特に **大きな PDF を OCR する** 作業で、数分かかる場合に便利です。

---

## 手順 4: 完全版スクリプト – すぐに実行可能なコード

以下がフルスクリプトです。`pdf_ocr.py` という名前で保存し、`python pdf_ocr.py path/to/your/file.pdf` で実行してください。

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### 期待される出力（抜粋）

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

各ページの短いプレビューが表示され、最後に結合されたテキストファイルが書き込まれたことが確認できます。

---

## エッジケースと実践的なヒント

| 状況 | 対処方法 |
|-----------|------------|
| **暗号化 PDF** | パスワードを渡す: `engine.load_pdf(pdf_path, password="mySecret")` |
| **非常に大きな PDF（> 1000 ページ）** | `max_memory_mb` を慎重に増やすか、200 ページずつなどに分割して処理 |
| **印刷物 + 手書き混在** | ライブラリが対応していれば `engine.recognition_mode` を `aocr.RecognitionMode.MIXED` に変更 |
| **フォント欠損やスキャン品質が低い** | `recognize()` 前に Pillow などで画像前処理を行う |
| **メモリ不足でクラッシュ** | `preview_len` を減らすか、テキストをリストに保持せずページごとに直接ディスクへ書き出す |

---

## 大きな PDF を効率的に OCR する方法 – 上級戦略

**大きな PDF を OCR** する際は、速度と安定性が鍵になります。以下のテクニックをスクリプトに組み込んでみてください。

1. **ページ単位で並列化** – OCR エンジンがスレッドセーフなら `concurrent.futures.ThreadPoolExecutor` を使用。  
2. **中間画像をキャッシュ** – 一部エンジンはラスタライズしたページを SSD に保存でき、再実行時の CPU 負荷を大幅に削減。  
3. **バッチ書き込み** – Python のリストに蓄積せず、出力ファイルを一度だけ開き、ページが完了したらすぐに追記。  
4. **DPI を調整** – ラスタライズ時の DPI を下げるとメモリ使用量が減りますが精度が低下する可能性あり。200‑300 DPI が目安です。

以下は OCR ステップを並列化する簡易サンプルです（オプション、使用する場合はコメントを外してください）：

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

※並列処理は CPU 使用率を上げるため、長時間実行時はシステム温度を監視してください。

---

## よくある質問

**Q: このスクリプトを Tesseract など他の OCR ライブラリと組み合わせて使えますか？**  
A: もちろん可能です。`aocr` の呼び出し部分を `pytesseract.image_to` などに置き換えるだけで動作します。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで学んだテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}