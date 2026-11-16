---
category: general
date: 2026-05-31
description: C#で Aspose OCR を使用して画像からテーブルを抽出します。画像をテーブルに変換する方法、テーブル検出を有効にする方法、そして結果を効率的に出力する方法を学びましょう。
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: ja
og_description: Aspose OCRで画像からテーブルを抽出します。このガイドでは、画像をテーブルに変換し、テーブル検出を有効にし、C#で結果を処理する方法を示します。
og_title: 画像からテーブルを抽出 – ステップバイステップ C# チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Aspose OCRで画像からテーブルを抽出する – 完全C#ガイド
url: /ja/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテーブルを抽出 – 完全な C# ガイド

画像からテーブルを **extract tables from image** したいと思ったことはありませんか？ スタート地点が分からずに戸惑う開発者は多いです。スキャンした請求書や領収書を利用可能なデータに変換しようとすると、この壁にぶつかります。良いニュースは、Aspose OCR を使えば、C# の数行で **convert image to table** が可能です。

このチュートリアルでは、実際の例としてテーブルを含む PNG を読み込み、視覚的なレイアウトを構造化されたグリッドに変換し、各セルの内容と信頼度スコアを出力するまでの手順を解説します。最後まで実装すれば、任意の .NET プロジェクトに貼り付けられる完全動作のコードスニペットが手に入り、エッジケースの対処法やスケーリングのコツも学べます。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.6+ でも動作します）
- **Aspose.OCR** NuGet パッケージ（`Install-Package Aspose.OCR`）
- テーブルが実際に含まれる画像ファイル（例: `invoice_with_table.png`）
- 基本的な C# IDE（Visual Studio、Rider、または C# 拡張機能付き VS Code）

以上だけです—追加の OCR エンジンや重い依存関係は不要です。準備はできましたか？さっそく始めましょう。

## ステップ 1: OCR エンジンを初期化して **Extract Tables from Image** を行う

まず、`OcrEngine` インスタンスを作成し、対象画像を指定します。エンジンは、すべてのピクセルを読み取り、レイアウトを解釈しようとする「脳」のようなものです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Why this matters:** エンジンを正しく初期化しないと、OCR エンジンは解析対象がなく、画像からテーブルを取得できません。`ImageStream.FromFile` 呼び出しは PNG、JPEG、BMP などの一般的なフォーマット問題も自動で処理するため、追加の変換ステップは不要です。

## ステップ 2: テーブル検出を有効化 – **Convert Image to Table** の鍵

Aspose OCR は画像からプレーンテキストを読み取れますが、テーブル（行・列）を自動で認識させるには `DetectTables` フラグを有効にする必要があります。

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** 生のテキストだけが必要な場合は `DetectTables` を `false` のままにしておきましょう。有効にすると若干のオーバーヘッドが発生しますが、スプレッドシートやデータベースに直接投入できるクリーンで構造化された結果が得られます。

## ステップ 3: OCR 認識を実行 – 真実の瞬間

エンジンに画像の読み取りを指示します。`Recognize` メソッドはプレーンテキストと検出されたテーブルの両方を含む `OcrResult` オブジェクトを返します。

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **What happens under the hood?** Aspose は画像の前処理（デスキュー、二値化）を行った後、ニューラルネットワークベースのテキスト認識器を適用します。`DetectTables` が `true` の場合、文字を行・列にグループ化するレイアウト解析パスも実行されます。

## ステップ 4: 検出されたテーブルを反復処理 – **Extract Tables from Image** の実践

エンジンがテーブルを検出した場合、`result.Tables` に格納されます。各テーブル、行、列をループし、セルのテキストと信頼度（パーセンテージ）を出力します。

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Why check confidence?** OCR は完璧ではなく、特に低解像度のスキャンでは誤認識が起こりやすいです。`Confidence` 値（0‑100）を利用して、セルをそのまま受け入れるか手動でレビューするかを判断できます。重要なデータでは 80 % 前後を目安にすると良いでしょう。

### 期待される出力

ソース画像に 3 × 4 の請求書明細テーブルが含まれていると仮定すると、次のような出力が得られます。

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

テーブルが検出されなかった場合、`result.Tables` は空になります—出力はありませんが、プログラムは正常に終了します。

## ステップ 5: エッジケースと一般的な落とし穴の対処

### 低解像度画像

画像の解像度が 150 dpi 未満の場合、テーブル検出アルゴリズムがセル境界を見逃すことがあります。簡単な対策として、`System.Drawing` を使って画像を拡大してから Aspose に渡します。

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### 歪んだテーブル

テーブルが数度だけ回転している場合は、自動デスキューを有効にします。

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### 1 ページに複数テーブルがある場合

Aspose OCR は各テーブルを `result.Tables` の別々のオブジェクトとして返します。個別に処理することも、単一の `DataTable` に結合して統合ビューを作ることも可能です。

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Excel へのエクスポート

`DataTable` が手に入ったら、`ClosedXML` を使って `.xlsx` ファイルに書き出すのはとても簡単です。

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

これで本当に **convert image to table** が完了し、スプレッドシートを下流プロセスに渡すことができます。

## 完全動作サンプル – 最初から最後まで

以下はすべてをまとめた実行可能なコンソールアプリのコードです。新しいコンソールプロジェクトに貼り付け、ファイルパスを自分の画像に置き換えて **F5** を押すだけです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Explanation of the flow**

1. **Engine setup** – 画像を読み込み、Aspose にテーブル検出を指示します。
2. **Options tuning** – `DetectTables` が主要な処理を行い、`Deskew` が斜めスキャンの精度を向上させます。
3. **Recognition** – プレーンテキストと `Table` オブジェクトのコレクションを返します。
4. **Iteration** – 各セルを信頼度と共に出力しつつ、後でエクスポートできる `DataTable` を構築します。
5. **Export** – 軽量でインターロップ不要の `ClosedXML` を使用して `.xlsx` ファイルを書き出します。これにより、下流の分析やレポート作成が容易になります。

## Frequently Asked Questions

- **Does this work with PDFs?**  
  はい。各 PDF ページをまず画像に変換（`PdfRenderer` または `Ghostscript`）し、得られたビットマップを Aspose OCR に渡します。

- **Can I extract tables from a JPG?**  
  もちろん可能です。`ImageStream.FromFile` メソッドは JPEG、PNG、BMP、TIFF をそのまま受け付けます。

- **What if my table has merged cells?**  
  Aspose OCR は結合セルを別々の論理セルとして扱います。信頼度や内容パターンに基づいて、出力後に結合処理を行う必要があります。

- **Is there a limit on table size?**  
  実務上は数百行まで問題なく処理できます。行数が増えるとパフォーマンスは線形に低下するため、非常に大きなスキャンは適宜分割して処理することを検討してください。

## Wrapping Up

私たちは今回、画像からテーブルを抽出する方法を実演しました。

## What Should You Learn Next?

- [Aspose.OCR for .NET を使用した画像からテーブルを抽出する方法](/ocr/english/net/text-recognition/recognize-table/)
- [画像からテキストを抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)
- [OCR で矩形領域を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}