---
category: general
date: 2026-03-26
description: Python OCR を使用して画像から表を抽出し、画像をスプレッドシートに変換します。OCR 用に画像を読み込む方法、表を読み取る方法、表データを抽出する方法を学びましょう。
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: ja
og_description: Python OCRで画像からテーブルを抽出します。このガイドでは、OCR用に画像を読み込む方法、テーブルを読み取る方法、そしてスプレッドシートに変換する方法を示します。
og_title: 画像からテーブルを抽出 – 完全OCRチュートリアル
tags:
- OCR
- Python
- Data Extraction
title: 画像からテーブルを抽出する – ステップバイステップ OCR ガイド
url: /ja/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテーブルを抽出 – 完全OCRチュートリアル

画像から **extract tables from image** が必要だったことはありませんか？でもどこから始めればいいか分からない…という方は多いです。PDF やスクリーンショットにテーブル形式のデータが含まれていて、編集可能な行と列に変換しなければならないとき、多くの開発者が壁にぶつかります。朗報です！数行の Python コードと信頼できる OCR エンジンさえあれば、画像を数秒で使えるスプレッドシートに変換できます。

このチュートリアルでは、OCR 用に画像を読み込む方法、認識エンジンを実行する方法、テーブルを行単位で抽出する方法を順を追って解説します。最後まで読めば **convert image to spreadsheet** ができるようになり、 **ocr read tables** や **ocr extract table data** を下流処理に活用する方法も学べます。隠された魔法はなく、すぐにプロジェクトに組み込める実行可能なコードだけをご紹介します。

---

## 必要なもの

本格的に始める前に、以下が揃っていることを確認してください。

- **Python 3.9+** – 最新の安定版がベストです。  
- **`ocr`** ライブラリ（または `OcrEngine`、`Image`、テーブル関連メソッドを提供する互換 OCR SDK）。`pip install ocr‑sdk` でインストールします（実際のパッケージ名に置き換えてください）。  
- 明瞭に印刷されたテーブルを含む画像ファイル（`.png`、`.jpg` など）。  
- 任意：抽出したデータを直接 CSV や Excel に書き出したい場合は **pandas**（`pip install pandas`）。

すべて揃いましたか？それでは、始めましょう。

---

## Step 1: OCR SDK をインポートし環境を整える

まず最初に、OCR クラスをスクリプトに取り込み、後で生のテーブルデータを DataFrame に変換するための小さなヘルパーを用意します。

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**この処理が重要な理由:** `ocr` をインポートすることで `OcrEngine`、`Imaging.Image`、そしてイテレート対象となるテーブルオブジェクトにアクセスできます。`pandas` は抽出自体には必須ではありませんが、**convert image to spreadsheet** を簡単に実現できるようになります。

---

## Step 2: 処理したい画像を読み込む

ここで実際に **load image for OCR** を行います。SDK は `Image` オブジェクトを期待するので、ヘルパーメソッド `Image.load()` でファイルパスをラップします。

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**プロチップ:** 画像ファイルは `assets/` や `data/` といった専用フォルダに入れ、相対パスで指定するとスクリプトがマシン間でポータブルになります。

---

## Step 3: 認識プロセスを実行する

画像がセットされたら、エンジンに **ocr read tables** を指示します。`recognize()` の呼び出しは、テキストブロック、行、そして最も重要なテーブル情報をすべて含む結果オブジェクトを返します。

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**チェックする理由:** 画像がノイズが多い、またはテーブルの枠線が薄い場合、エンジンがテーブルを見逃すことがあります。警告をログに出すことで、スクリプトが途中で止まることなく早期にフィードバックを得られます。

---

## Step 4: 各テーブルの行とセルを抽出する

ここが本番です。検出されたすべてのテーブルを走査し、行ごとにセルのテキストを取得します。内側のリスト内包表記でコードを簡潔に保ちつつ、流れを解説します。

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**何が起きているのか？**  

- `enumerate(..., start=1)` でログ用に見やすいテーブル番号を付与。  
- `row_obj.get_cells()` が各セルオブジェクトを返し、`cell.get_text()` が OCR でデコードされた文字列を取得。  
- 行データは `rows_data` に格納し、`pandas.DataFrame` に渡すことで自動的に列が揃えられます。  
- `print` 部分は元のスニペットと同様の **essential output** を表示し、結果をすぐに確認できます。

**エッジケースの処理:** 行ごとにセル数が異なる場合、`pandas` は不足分を `NaN` で埋めます。空文字列にしたい場合は後で `df.fillna('')` で置換できます。

---

## Step 5: 抽出したテーブルをスプレッドシートに保存する

DataFrame のリストができたので、Excel ブック（または CSV）に書き出すのは簡単です。これで **convert image to spreadsheet** の目的が達成されます。

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**なぜ Excel？** 多くのビジネスユーザーは `.xlsx` を好みます。CSV が欲しい場合は、ループを `df.to_csv(f"table_{idx}.csv", index=False)` に置き換えてください。

---

## Step 6: 完全実行可能スクリプト

すべてをまとめると、以下がコピー＆ペーストでそのまま実行できる完全版プログラムです。

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**期待されるコンソール出力**（シンプルな 2×3 テーブルを想定）:

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

スクリプトと同じフォルダに `extracted_tables.xlsx` が生成され、各テーブルが個別シートに保存されます。

---

## Frequently Asked Questions & Tips

| Question | Answer |
|----------|--------|
| **別の OCR ライブラリは使えますか？** | もちろんです。パターンは同じです：画像をロード → 認識 → `get_tables()` をイテレート。インポート文とオブジェクト名を置き換えるだけです。 |
| **画像がノイズが多い場合は？** | OCR エンジンに渡す前に OpenCV で前処理（閾値処理、デスキュー）を行うと効果的です。ノイズ除去は **ocr extract table data** の精度向上に寄与します。 |
| **`openpyxl` は必要ですか？** | はい、`pandas` が Excel 出力の裏で使用します。`pip install openpyxl` でインストールしてください。 |
| **結合セルはどう扱いますか？** | SDK によっては `cell.is_merged()` が提供されます。結合セルを検出したら、手動で値を結合範囲全体にコピーしてください。 |
| **特定のテーブルだけ抽出したい場合は？** | `table_obj.get_confidence()` で信頼度でフィルタしたり、ヘッダーキーワードをチェックして対象テーブルを絞り込むことができます。 |

---

## まとめ

これで **extract tables from image** のエンドツーエンドソリューションが完成し、結果を整然としたスプレッドシートに変換し、画像内の複数テーブルにも対応できるようになりました。スクリプトは **load image for OCR**、**ocr read tables**、**ocr extract table data** を実演しつつ、実務でのバリエーションにも柔軟に対応できます。

次のステップは？PDF ページを画像化して OCR にかけてみる、異なる言語やフォントで実験してみる、あるいは DataFrame を直接データベースやレポートツールに流し込むなど、可能性は無限です。

このガイドが役に立ったら、ぜひシェアしたり、SDK をホストしているリポジトリにスターを付けたり、独自のコツをコメントで共有してください。Happy coding、そしてテーブルが常に完璧にパースされますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}