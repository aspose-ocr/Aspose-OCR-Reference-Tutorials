---
category: general
date: 2026-06-06
description: Python を使って PDF を OCR し、画像から検索可能な PDF ファイルを作成する方法。数分で検索可能なテキストを追加し、画像を
  PDF/A に変換する方法を学びましょう。
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: ja
og_description: PDFをステップバイステップでOCRする方法。シンプルなPythonスクリプトを使って検索可能なテキストを追加し、画像をPDF/Aに変換する方法を学びましょう。
og_title: PDFをOCRする方法 – 検索可能なPDFを作成するクイックガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: PythonでPDFをOCRする方法 – 画像から検索可能なPDFを作成
url: /ja/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF を OCR する方法 – スキャン画像を検索可能な PDF に変換

請求書や領収書のスキャン画像しかないとき、**PDF を OCR する方法**を知りたくありませんか？ あなただけではありません。多くのオフィスでは、受信した書類が PNG や JPEG のフラット画像として届き、次のステップである「内容を検索可能にする」作業がブラックボックスのように感じられます。

朗報です！ Python の数行のコードで **検索可能な PDF** を作成し、**検索可能なテキストを追加**、さらには **PDF/A に変換** して長期保存も可能です。このチュートリアルでは、各ステップを順に解説し、すぐに実行できるスクリプトを提供します。

> **プロのコツ:** 同じアプローチは複数ページのスキャンでも機能します。ファイルをループさせるだけで、エンジンが重い処理を自動で行います。

---

## 必要なもの

作業を始める前に、以下がマシンに揃っていることを確認してください。

| 必要条件 | 重要な理由 |
|----------|------------|
| Python 3.9 以上 | 最新構文と豊富なライブラリサポート |
| `pdfium` ベースの OCR エンジン（例: `pdfocr` または商用 SDK） | 画像認識と PDF/A 生成の両方を処理 |
| 検索可能な PDF に変換したい画像ファイル（PNG、JPEG、TIFF） | テキスト抽出元 |
| 出力フォルダへの書き込み権限 | スクリプトが新しい PDF を保存できるように |

OCR SDK がまだインストールされていない場合は、以下を実行してください。

```bash
pip install pdfocr   # replace with your vendor's package name
```

これだけです—複雑なシステム依存は不要で、pip インストールだけです。

---

## PDF を OCR する方法 – 概要

全体の流れは大きく 3 つのシンプルなアクションで構成されます。

1. **画像内のテキストを認識**し、元のグラフィックを保持する。  
2. **OCR 結果と元画像を組み合わせて検索可能な PDF/A**（アーカイブ向け PDF）としてエクスポート。  
3. **生成されたファイルに、元画像上に選択可能で検索可能なテキスト層があることを検証**。

以下にコードとともに、各コマンドの *なぜ* を解説します。

---

## ステップ 1: 画像からテキストを認識

まず OCR エンジンにピクセルを読み取らせ、元画像と抽出テキストの両方を保持した結果オブジェクトを取得します。請求書をエンジンが「読む」イメージです。

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### なぜ重要か

- **グラフィックの保持** により、レイアウト（表、ロゴ、スタンプ）がスキャナが捉えたまま正確に残ります。  
- `result` オブジェクトには、後で PDF に埋め込む隠れたテキスト層が通常含まれます。  
- `recognize_image` を使用することで、`recognize_pdf` に比べて余分な変換ステップが省かれ、単ページ画像の処理が高速化します。

#### よくあるバリエーション

- **マルチページ TIFF** がある場合はファイルパスを直接渡してください。ほとんどのエンジンは各ページを別々の画像として扱います。  
- 画像をすでに含む PDF がある場合は `engine.recognize_pdf("file.pdf")` を呼び出せば、このステップは不要です。

---

## ステップ 2: OCR 結果を検索可能な PDF/A としてエクスポート

ステップ 1 の `result` を受け取り、エンジンに新しいファイルを書き出させます。ここで重要なのは *PDF/A* フラグ—長期保存向けに設計された ISO 標準の PDF バージョンです。

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### なぜ重要か

- **検索可能な PDF**: 出力ファイルには隠れた選択可能テキスト層が含まれます。これで文書内を Ctrl + F で検索できます。  
- **PDF/A 準拠**: 法務や財務など、一部の組織は監査証跡のために PDF/A を必須としています。このステップで自動的に要件を満たします。  
- 画像をフラット化せずに **検索可能なテキストを追加** できるため、視覚的な忠実度が保たれます。

#### エッジケース: 通常の PDF が欲しい場合

PDF/A が不要なら `save_as_pdfa` を `save_as_pdf` に置き換えてください。残りのワークフローは同じです。

---

## ステップ 3: 検索可能な PDF を検証

簡単なサニティチェックで、後々の不思議なバグを防げます。生成されたファイルを任意の PDF ビューアで開き、単語を選択して検索機能を試してください。

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### 期待される出力

スクリプト実行時、コンソールに次のように表示されます。

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

ファイルを開くと、元の請求書画像の上に薄く見えないテキスト層があるはずです。任意の単語をハイライトすると選択可能になっていることが確認できます—**これが先ほど追加した検索可能テキスト**です。

---

## 既存 PDF に検索可能テキストを追加する（ボーナス）

既に PDF があり、そこに **検索可能テキストを追加** したいケースがあります。同じエンジンで OCR 結果を既存 PDF にオーバーレイできます。

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

ここで `apply_to` が隠れ層と元ページをマージし、**再スキャンせずに検索可能な PDF** を作成します。

---

## よくある落とし穴と対策

| 落とし穴 | 回避策 |
|----------|--------|
| **低解像度の画像** (< 150 dpi) | 解像度を上げるか、より高解像度のスキャンを依頼。150 dpi 未満では OCR 精度が大幅に低下します。 |
| **言語データが欠如** | OCR エンジン用の言語パックをインストール（例: `pip install pdfocr[eng,spa]`）。 |
| **出力フォルダが書き込み不可** | 十分な権限でスクリプトを実行するか、別ディレクトリを指定。 |
| **PDF/A 検証に失敗** | 非対応フォントや JavaScript を埋め込んでいないか確認。`save_as_pdfa` を使用すれば多くの SDK が自動で対処します。 |

---

## フルスクリプト – ワンファイルソリューション

以下はすべてをまとめた自己完結型スクリプトです。プレースホルダーのパスを差し替えるだけで、**画像を PDF/A に変換**できるようになります。

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**スクリプトの流れ:**  
1. OCR エンジンをロード。  
2. 指定画像を読み取り、テキストを抽出。  
3. **検索可能な PDF/A** を生成し、すぐに配布またはアーカイブ可能。

フォルダ全体を処理したい場合は、`main` ロジックを関数化し、`os.listdir()` でイテレートして各ファイルに対して同じ 3 ステップを繰り返すだけです。

---

## 次のステップ & 関連トピック

**OCR PDF** をマスターした今、以下の応用アイデアを検討してください。

- **バッチ処理:** `concurrent.futures` を使って数十件の請求書を並列 OCR。  
- **メタデータ注入:** 作成日や請求書番号を PDF メタデータに追加し、インデックス化を容易に。  
- **ハイブリッド PDF:** 検索可能テキストと元画像を組み合わせ、紙文書の「デジタルツイン」を実現。  
- **代替出力:** 下流システムが編集可能形式を必要とする場合は **DOCX** や **HTML** へエクスポート。

これらはすべて、今回学んだ「認識 → エクスポート → 検証」のコア概念に基づいています。

---

## まとめ

要するに、**画像を検索可能な PDF/A に変換**する方法を 3 行の Python で実装できるようになりました。スクリプトは重い処理を担い、元のグラフィックを保持し、標準準拠の文書を即座に検索・保存・共有できます。

自分の請求書、領収書、スキャンした契約書で試してみてください。問題があればコメントを残すか、SDK の公式ドキュメントを確認してください。コードを書いて楽しく検索可能な画像を作りましょう！

![元画像と検索可能な PDF オーバーレイを示す OCR PDF の例](placeholder.png "How to OCR PDF example showing original image and searchable PDF overlay")

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}