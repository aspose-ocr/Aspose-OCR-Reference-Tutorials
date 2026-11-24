---
category: general
date: 2026-06-16
description: Pythonで数分でPDFをOCRする方法 – PDFからテキストを抽出し、PDFにOCRを実行し、スキャンしたPDFのテキストを効率的に変換する方法を学びましょう。
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: ja
og_description: PythonでPDFをOCRする方法：PDFからテキストを抽出し、PDFにOCRを実行し、スキャンしたPDFのテキストを変換するステップバイステップの手順。
og_title: PythonでPDFをOCRする方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: PythonでPDFをOCRする方法 – 完全ガイド
url: /ja/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでPDFをOCRする方法 – 完全ガイド

スキャンしたページを検索可能なテキストに変換しようとして、**PDFをOCRする方法**で悩んだことはありませんか？ あなただけではありません。多くの開発者が同じ壁にぶつかります。朗報です！数行のPythonコードで PDF を OCR 用に読み込み、ページごとに OCR を実行し、数秒でクリーンで編集可能な文字列を取得できます。

このチュートリアルでは、実際の例を通して PDF 文書を OCR し、PDF ページからテキストを抽出し、スキャンした PDF テキストを JSON 形式の結果に変換する方法を詳しく解説します。余計な説明は省き、すぐにプロジェクトに組み込める動作スクリプトだけを提供します。

## 必要なもの

- Python 3.8+（最近のバージョンならどれでも可）
- `ocr` ライブラリ（または互換ラッパー – ここでは示した API に従う汎用 `ocr` パッケージを想定）
- 処理したいマルチページのスキャン PDF
- お好みの IDE またはエディタ（VS Code、PyCharm、シンプルなテキストエディタでも可）

以上です。揃っていれば、プロ並みで PDF ファイルからテキストを抽出する準備は完了です。

## Step 1 – OCR エンジンのセットアップ（How to OCR PDF）

まず最初に OCR エンジンのインスタンスを作成します。エンジンは文書上のすべてのピクセルを読む「脳」のようなものです。

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **プロのコツ:** エンジンの初期化はコストが低いですが、バッチで数十個の PDF を処理する場合は、同じ `engine` オブジェクトを再利用してメモリ使用量を抑えましょう。

![Diagram of the OCR pipeline illustrating how to OCR PDF](/images/ocr-pdf-workflow.png "How to OCR PDF workflow")

## Step 2 – 正しい言語を選択（Run OCR on PDF）

スキャンが英語の場合は、言語を明示的に設定します。このステップを省くとエンジンが自動推測しますが、遅くなるだけでなく精度が落ちることがあります。

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

なぜ必要かというと、**run OCR on PDF** 時に既知の言語を指定すると認識率が大幅に向上するからです。特に専門用語が多い文書で効果を実感できます。

## Step 3 – 特定ページに絞る（Load PDF for OCR）

500ページもの大規模アーカイブを全部処理するのは、最初の数章だけが必要な場合は過剰です。ページ範囲を次のように限定できます。

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

この小さな調整で、エンジンは **load PDF for OCR** しますが、関心のあるページだけを処理するため、時間と CPU サイクルの両方を節約できます。

## Step 4 – ドキュメントを読み込む（Load PDF for OCR）

実際のファイルパスをエンジンに渡します。パスが間違っていると `FileNotFoundError` が発生しますので注意してください。

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

この時点でエンジンは **loaded the PDF for OCR** し、内部構造を解析済みで、重い処理を開始する準備が整いました。

## Step 5 – 認識を開始（Run OCR on PDF）

いよいよ魔法の瞬間です。`recognize()` 呼び出しがすべてのピクセルを走査し、言語モデルを適用してリッチな結果オブジェクトを返します。

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

裏側ではエンジンが **run OCR on PDF** ページを処理し、テキストレイヤーを構築、さらに単語ごとの信頼度スコアも保持します。

## Step 6 – テキスト全体を取得（Extract Text from PDF）

多くのユースケースではプレーンテキストだけで十分です。`text` 属性はエンジンが見つけたすべての文字列を連結したものを返します。

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

これで **extracted text from PDF** が完了しました。検索インデックスやデータベース、あるいは単純な `print()` にそのまま渡せます。

## Step 7 – 詳細結果を確認（Convert Scanned PDF Text）

文字列だけでなく、バウンディングボックスや信頼度スコアが必要な場合は JSON エクスポートを利用します。これは実質的に **convert scanned PDF text** を機械可読形式に変換することです。

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

JSON にはページごとの配列が含まれ、各エントリは認識されたテキスト、ページ上の位置、信頼度メトリックを保持しています。エンティティ抽出やカスタムハイライトなど、下流処理に最適です。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 簡単な対処法 |
|------|----------|--------------|
| **文字化け** | 言語設定が間違っている、またはフォントが欠如 | `engine.language` を正しい言語に明示的に設定 |
| **ページが抜ける** | `pdf_page_range` が狭すぎる | タプル `(start, end)` が文書全体に合っているか再確認 |
| **パフォーマンス低下** | 大きな PDF を一括処理 | PDF をチャンクに分割するか、`concurrent.futures` でページ単位に並列処理 |
| **出力が空** | ファイルパスのタイプミス、または PDF が読めない | ファイルが存在し、パスワードで保護されていないことを確認 |

これらを事前に対策しておくと、後々のデバッグ時間を大幅に削減できます。

## 例の拡張

- **バッチ処理:** ディレクトリ内の PDF をループし、同じ `engine` インスタンスを再利用
- **カスタム出力:** `pdf_result.text` を `.txt` ファイルに書き出す、または Elasticsearch などの検索エンジンに直接投入
- **画像抽出:** 一部の OCR ライブラリはページごとの画像を提供。視覚的検証のために取り出すことが可能

以下はフォルダをバッチ処理する小さなスニペットです。

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## まとめ – 本チュートリアルで学んだこと

Python で **how to OCR PDF** という疑問から始め、次の手順を実施しました。

1. OCR エンジンを初期化
2. 言語を設定（任意だが推奨）
3. ページ範囲を限定して高速化
4. PDF ファイルを読み込み
5. 文書に対して OCR を実行
6. **Extracted text from PDF** を取得し即時利用
7. 詳細結果を **convert scanned PDF text** して JSON にエクスポート

これらのステップを組み合わせることで、任意のスキャン PDF を検索可能で編集可能なコンテンツに変換するための堅実な基盤が手に入ります。

## 次のステップ

- `ocr.Language.SPANISH`、`ocr.Language.FRENCH` など異なる言語で試し、多言語文書への対応を確認
- スキャンが低解像度の場合は `engine.dpi` 設定を調整。高 DPI にすると精度が向上することがあります
- OCR 出力を spaCy などの自然言語処理ライブラリと組み合わせ、エンティティ、日付、キーフレーズを自動抽出

**load PDF for OCR** や **run OCR on PDF** で質問や問題があれば、下のコメント欄で教えてください。一緒にトラブルシュートしましょう。コーディングを楽しみながら、頑固なスキャンを検索可能な金鉱に変えていきましょう！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}