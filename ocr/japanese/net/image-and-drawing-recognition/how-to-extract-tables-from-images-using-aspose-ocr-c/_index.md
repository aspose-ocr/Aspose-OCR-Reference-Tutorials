---
category: general
date: 2026-03-28
description: C#でAspose OCRを使用して画像からテーブルを抽出する方法を学びましょう。このガイドでは、画像内のテーブルを検出し、OCR用に画像を読み込み、PNGファイルからテーブルを抽出する手順を解説しています。
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: ja
og_description: C# で Aspose OCR を使用して画像からテーブルを抽出する手順ごとのチュートリアルです。コード、解説、画像ファイル内のテーブル検出に関するヒントが含まれています。
og_title: Aspose OCR（C#）を使用して画像からテーブルを抽出する方法
tags:
- Aspose OCR
- C#
- Table Extraction
title: Aspose OCR（C#）を使用して画像からテーブルを抽出する方法
url: /ja/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR (C#) を使用して画像からテーブルを抽出する方法

スキャンした請求書やスプレッドシートのスクリーンショットから **テーブルを抽出する方法** を考えたことがありますか？ あなただけではありません。実際のプロジェクトでは、テーブルの画像をクエリ可能な形、たとえば CSV や DataTable に変換する必要があります。良いニュースは、Aspose OCR がそれを簡単にし、C# の数行で実現できるということです。

このチュートリアルでは、**OCR 用画像の読み込み**、**画像内のテーブル検出**、そして最終的に **画像からテーブルを抽出** して CSV ファイルとして保存するまでの全プロセスを解説します。最後まで実行すれば、**PNG ファイルからテーブルを抽出**（またはサポートされている任意のビットマップ）できる、すぐに実行可能なコンソール アプリが手に入ります。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Framework でも動作します）
- Visual Studio 2022（またはお好みの IDE）
- Aspose.OCR for .NET のライセンス ファイル（無料トライアルから開始可能）
- テーブルを含むサンプル画像（例：`invoice_table.png`）

これらに心当たりがなくても心配はいりません。.NET SDK をインストールし、NuGet パッケージを取得すればすぐに始められます。

## ソリューションの概要

全体のワークフローは次のようになります：

1. **画像の読み込み**：処理したい画像を読み込む。
2. **OCR 認識の実行**：エンジンがテキストの位置を把握できるようにする。
3. **TableExtractor の作成**：OCR 結果をスキャンしてグリッド構造を検出する。
4. **検出されたすべてのテーブルを抽出**し、必要なものを選択する。
5. **テーブルを保存**：CSV（または任意の形式）として保存する。

各ステップは以下で詳しく説明し、コピー＆ペーストできる完全なコードスニペットを示します。

<img src="table_extraction_example.png" alt="画像からテーブルを抽出する例" width="600">

（上の画像は、抽出対象となるサンプル請求書テーブルです。）

## ステップ 1 – OCR 用画像の読み込み

最初に行うべきことは、Aspose OCR に読み込むファイルを指定することです。ライブラリは PNG、JPEG、BMP、TIFF などの形式をサポートしています。以下が最小限のコードです：

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**なぜ重要か:**  
`Image.FromFile` は PNG（または他のビットマップ）をデコードし、OCR エンジンが理解できる形式に変換する重い処理を行います。このステップを省略したり、破損したファイルを渡すと、次の `Recognize()` 呼び出しで例外がスローされます。

> **プロのコツ:** 大きな PDF を扱う場合は、まず各ページを画像として抽出してください。そうしないと OCR エンジンがメモリ不足になります。

## ステップ 2 – ページの認識（テーブル検出の前提）

認識は生のピクセルデータを検索可能なテキストレイアウトに変換します。このステップがないと `TableExtractor` は何も処理できません。

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**内部で何が起きているか:**  
Aspose OCR はニューラルネットワークベースのテキスト検出器を実行し、`Page`、`Paragraph`、`Word` オブジェクトの階層を作成します。テーブル検出器は後でこれらの単語間の空間関係を調べます。

多数の画像をループで処理する場合は、同じ `OcrEngine` インスタンスを再利用し、`Image` プロパティだけを差し替えることを検討してください。これにより割り当てオーバーヘッドが削減されます。

## ステップ 3 – TableExtractor の作成と画像内テーブルの検出

OCR データが取得できたので、Aspose にテーブルを探させます。`TableExtractor` クラスがまさにそれを行います。

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**なぜ `ExtractAll()` を使うのか？**  
1 つの画像に複数のテーブルが含まれることがあります（マルチセクションレポートを想像してください）。`ExtractAll()` は `List<Table>` を返すので、イテレートしたり、適切なテーブルを選択したり、後で結合したりできます。

最初のテーブルだけが必要な場合は `extractedTables[0]` を安全に使用できますが、`IndexOutOfRangeException` を防ぐためにリストが空でないことを必ず確認してください。

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## ステップ 4 – 抽出したテーブルを CSV（または他の形式）で保存

Aspose はエクスポートを簡単にします。`Table` クラスには組み込みの `SaveCsv`、`SaveXls`、`SaveJson` メソッドがあります。CSV ファイルを書き出す方法は以下の通りです：

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**CSV の内容はどうなるか？**  
元画像が 4 × 3 のグリッドだったと仮定すると、CSV は次のようになります：

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

このファイルは Excel、Power BI で開くことも、データパイプラインに直接取り込むこともできます。

## 完全なエンドツーエンド例

以下は完全な単体プログラムです。新しいコンソール プロジェクト（`dotnet new console`）にコピーして実行してください。NuGet パッケージ `Aspose.OCR` がインストールされていることを確認してください（`dotnet add package Aspose.OCR`）。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### 期待される出力

プログラムを実行すると、以下のような出力が表示されます：

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

`invoice_table.csv` を開くと、元の画像と同じ行と列が確認できます。

## よくある質問とエッジケース

### 画像が PNG ではなく JPEG の場合は？

同じコードが動作します。`Image.FromFile` の拡張子を変更するだけです。Aspose OCR は自動的にフォーマットを検出するため、**png からテーブルを抽出** という硬い要件はなく、サポートされている任意のビットマップで動作します。

### テーブルに結合セルがある場合、保持されますか？

結合セルは CSV 出力では別々の列として扱われます。CSV はセル結合をサポートしていないためです。リッチなフォーマット（例：結合セルを持つ Excel）が必要な場合は、代わりに `SaveXls` を使用してください：

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### 検出で列が抜け落ちた場合、精度を上げるには？

- 画像解像度を上げる（理想は 300 dpi 以上）。
- 画像を前処理する：グレースケール変換、コントラスト強化、またはデスキュー（傾き補正）フィルタを適用。
- テーブルに非ラテン文字が含まれる場合は、`PageSegMode` や `Language` など Aspose OCR の設定を調整する。

### PDF から直接テーブルを抽出できますか？

はい。まず各 PDF ページを画像に変換します（`Aspose.PDF` や任意の PDF‑to‑image ライブラリを使用）。その後、同じワークフローに画像を渡します。

## 本番環境向け実装のヒント

1. **OCR を try/catch でラップ** – ネットワーク ライセンス環境ではライセンス例外がスローされることがあります。
2. **`Image` オブジェクトを破棄** – `using` ブロックでラップしてネイティブリソースを解放します。
3. **信頼度スコアをログに記録** – `TableExtractor` は `Table.Confidence` を公開しているので、品質監視のために保存できます。
4. **バッチ処理** – 数百件の請求書を処理する場合、OCR 呼び出しを並列化できますが、ライセンスのスレッド安全ガイドラインを守ってください。

## 次のステップ

画像から **テーブルを抽出する方法** が分かったので、次のことを検討できるでしょう：

- **画像内テーブルの検出** ビデオ（各フレームで Aspose の `TableExtractor` を使用）。
- **OCR 用画像の読み込み** を Web API から行い、クラウドベースのテーブル抽出サービスを実現。
- **PNG ファイルからテーブルを抽出** を Azure Blob Storage に保存された画像で行い、Azure Functions と統合してサーバーレス処理を実装。

さまざまなファイル形式を試したり、OCR 設定を調整したり、CSV 出力を直接データベースに流し込んだりしてみてください。可能性は無限です。

*コーディングを楽しんでください！問題が発生したり改善案があれば、下にコメントを残してください。一緒に解決しましょう。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}