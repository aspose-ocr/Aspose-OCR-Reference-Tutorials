---
category: general
date: 2026-03-18
description: C#でAspose OCRを使用して画像から表を抽出します。表をJSONに変換する方法、表のJSONを取得する方法、画像からテキストを抽出する方法を数分で学べます。
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: ja
og_description: C#でAspose OCRを使用して画像からテーブルを抽出します。テーブルをJSONに変換する方法、テーブルJSONを取得する方法、画像からテキストを迅速に抽出する方法を学びましょう。
og_title: Aspose OCRで画像からテーブルを抽出する – 完全なC#ガイド
tags:
- Aspose OCR
- C#
- Table Extraction
title: Aspose OCRで画像からテーブルを抽出 – 完全C#ガイド
url: /ja/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテーブルを抽出 – 完全な C# ガイド

テーブルを **画像から抽出** したいけれど、手動でのパースが山ほど必要になるライブラリはどれか分からない、ということはありませんか？請求書処理やレシートスキャンのプロジェクトでは、ノイズの多いビットマップを下流システムが利用できる構造化テーブルに変換することが最大の課題です。  

良いニュースは、Aspose OCR を使えば **テーブルを JSON に変換** でき、さらに画像全体のプレーンテキストも取得できるので **画像からテキストを抽出** するのも簡単です。このチュートリアルでは、画像の読み込みから検出されたテーブルの整然とした JSON 表現を取得するまでの全フローを解説します。

> **クイックウィン:** 最終的に、OCR の生テキストと JSON 文字列の両方をコンソールに出力する C# コンソールアプリが完成します。これらはそのままデータベースや API に投入できます。

## 前提条件

作業を始める前に、以下を用意してください。

- .NET 6.0 SDK（または最新の .NET バージョン）をインストール済み  
- 有効な Aspose OCR ライセンス、または無料トライアル（ライセンスなしでも動作しますが透かしが入ります）  
- テーブルが含まれる画像（例: `invoice_table.png`）  
- Visual Studio 2022、VS Code、またはお好みのエディタ

`Aspose.OCR` 以外の NuGet パッケージは不要です。

## ステップ 1: プロジェクトのセットアップと Aspose OCR のインストール

まず、コンソールプロジェクトを作成し OCR ライブラリを導入します。

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **プロのコツ:** 社内プロキシを使用している場合は `--no-restore` フラグを付けてプロジェクトを作成し、後で環境変数を設定した上で `dotnet restore` を実行してください。

## ステップ 2: OCR エンジンの初期化とテーブル認識の有効化

解決策の中心は `OcrEngine` です。`EnableTableRecognition` を有効にすると、Aspose OCR がプレーンテキストではなくグリッド構造を探すようになります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

このステップが重要な理由は何でしょうか？テーブル認識をオフにすると、エンジンは画像全体を単一の文字列に平坦化してしまい、後から行や列を再構築することが不可能になります。テーブル認識を有効にすると、ほぼコストゼロで軽量なレイアウト解析フェーズが追加され、下流の利便性が大幅に向上します。

## ステップ 3: 画像の読み込みと認識実行

次に、テーブルが格納されたファイルをエンジンに渡します。`ImageStream.FromFile` は PNG、JPEG、TIFF などの一般的なフォーマットをサポートしています。

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

画像が大きい場合は、処理速度向上のためにリサイズを検討してください。Aspose OCR は DPI を自動検出しますが、300 DPI のスキャンが多くのテーブルにとって最適です。

## ステップ 4: プレーンテキストの抽出 – “画像からテキストを抽出”

メインの目的はテーブルですが、ログやフォールバック処理のために生テキストが必要になることもあります。

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

`Text` プロパティはエンジンが認識したすべての文字列を結合し、改行を保持します。テーブル外のヘッダーやフッターが正しく読めているか確認したいときに便利です。

## ステップ 5: 検出されたテーブルを JSON として取得 – “テーブルを JSON に変換” & “テーブル JSON を取得”

ここが本番です。`GetTableAsJson()` は検出された行・列・セルの内容を整然とした JSON 文字列にシリアライズします。

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

生成される JSON は次のような形になります（可読性のために整形しています）。

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

なぜ JSON が推奨されるのでしょうか？言語非依存で、オブジェクトへのデシリアライズが容易であり、モダンな Web API と相性が抜群です。CSV が必要な場合は、行を走査してセルテキストをカンマで結合すれば簡単に変換できます。

## ステップ 6: (任意) JSON を .NET オブジェクトに変換 – “画像を JSON に変換”

強い型で扱いたい場合は、`System.Text.Json` を使って JSON をデシリアライズします。

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

`TableModel`、`RowModel`、`CellModel` を JSON スキーマに合わせて定義します。このステップは **画像を JSON に変換** から型付きオブジェクトまでの流れを示し、下流のバリデーションを楽にします。

## 完全動作サンプル

すべてを組み合わせた、実行可能なプログラム全体です。先ほど作成したプロジェクトフォルダ内に `Program.cs` として保存してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### 期待される出力

`dotnet run` を実行すると、以下のような出力が得られるはずです。

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

出力が空の場合は、`EnableTableRecognition` が `true` に設定されているか、画像に明瞭なグリッド線が含まれているかを再確認してください。

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **JSON が返ってこない** | テーブル検出が無効、または画像のコントラストが低すぎる | `ocrEngine.Settings.EnableTableRecognition = true` を確認し、コントラストを上げるか二値化する |
| **行が途中で切れる** | 結合セルや回転テキストで OCR が混乱 | 画像前処理でデスキュー (`ImageProcessor.Rotate`) するか、結合セルを手動で分割 |
| **Unicode が文字化け** | フォントが認識できない（手書きなど） | `ocrEngine.Language = Language.English;` など言語パックを切り替えるか、手書き用 OCR エンジンに切り替える |
| **処理が遅くなる** | 画像が非常に大きい（5 MP 超） | 幅約1500 px にダウンサンプリングし、DPI は維持する |

## 次のステップ: 基礎を超えて

**画像からテーブルを抽出** し **テーブルを JSON に変換** できたら、以下の拡張を検討してください。

- **JSON を Entity Framework でデータベースに永続化**  
- **JSON を後処理して通貨表記を正規化**（例: `$` を除去）  
- **`Directory.GetFiles` と `Parallel.ForEach` を使ってフォルダ内の請求書をバッチ処理**  
- **Azure Functions や AWS Lambda と統合し、サーバーレス OCR パイプラインを構築**  

これらのトピックは、**画像を JSON に変換**（OCR 結果全体をクラウドエンドポイントへ送信）や **テーブル JSON を取得**（下流分析用）といった二次キーワードとも自然に結びつきます。

---

### 結論

本稿では Aspose OCR を用いて **画像からテーブルを抽出** し、テーブルをクリーンな JSON に変換、さらに C# オブジェクトへデシリアライズする方法を示しました。同じパターンを使えば、さまざまなシナリオで OCR データを有効活用できます。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}