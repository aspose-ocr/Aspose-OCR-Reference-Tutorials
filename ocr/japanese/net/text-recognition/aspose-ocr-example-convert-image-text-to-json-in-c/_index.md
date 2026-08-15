---
category: general
date: 2026-04-17
description: Aspos e OCR の例を学び、C# で画像ファイルを読み取り、テキストを抽出し、JSON ファイルを書き出す方法を習得します。完全なステップバイステップ
  C# OCR チュートリアルです。
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: ja
og_description: Aspose OCR のサンプルをマスターして画像を読み取り、テキストを抽出し、C# で JSON ファイルを書き出しましょう。この簡潔な
  C# OCR チュートリアルに従ってください。
og_title: Aspose OCR の例 – 画像テキストを C# で JSON に変換
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose OCR の例 – C# で画像テキストを JSON に変換
url: /ja/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – 画像テキストを JSON に変換する C# の例

画像を読み取るだけでなく、下流処理用にきれいな JSON を出力する **aspose ocr example** が必要だったことはありませんか？ あなただけではありません。請求書自動化、レシートスキャン、あるいはシンプルな文書アーカイブなど、多くのプロジェクトで開発者は同じ壁にぶつかります。「OCR の結果を API が好む形式にどうやって変換すればいいのか？」  

良いニュースです。Aspose.OCR を使えば数行のコードで実現でき、その方法をここで詳しく解説します。このガイドが終わる頃には、**read image file C#**、**extract text image C#**、**write JSON file C#** のやり方をすべて把握し、再利用可能な C# OCR チュートリアルとしてまとめられます。

## What You’ll Need

- .NET 6.0 以降（コードは .NET Core でもコンパイル可能）  
- Aspose.OCR for .NET NuGet パッケージ (`Install-Package Aspose.OCR`)  
- 明瞭で機械可読なテキストが含まれる画像（`input.jpg`）  
- テキストエディタまたは Visual Studio（任意の IDE で構いません）  

余計な設定ファイルや隠しマジックは不要です。SDK と画像だけで始められます。

## Step 1 – Read image file C# with Aspose.OCR

まず最初に、OCR エンジンに有効な画像を渡す必要があります。Aspose.OCR は `OcrImage` オブジェクトを受け取り、ファイルパスから直接作成できます。

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Why this matters:* 画像を早めにロードすることで、ファイルの存在確認やフォーマットの問題をエンジンがピクセル処理を始める前に検出できます。ファイルが見つからない場合、`FromFile` は明確な例外をスローし、下流でハンドリング可能です。

## Step 2 – Initialize the Aspose OCR engine

エンジンの生成は軽量ですが、`using` ステートメントでラップしてリソースを速やかに解放するようにしましょう。

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Pro tip:* デフォルトエンジンはほとんどのラテン系テキストでうまく機能します。別の言語が必要な場合は、`ocrEngine.Language = Language.YourLanguage;` を `Recognize` を呼び出す前に設定してください。

## Step 3 – Extract text image C# – Perform the recognition

ここで本格的な処理が行われます。`Recognize` メソッドは `OcrResult` オブジェクトを返し、そこに生テキスト、信頼度スコア、各単語のバウンディングボックスが格納されます。

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

`ocrResult.Text` がプレーン文字列を保持し、`ocrResult.Regions` は UI 上で単語をハイライトしたい場合に役立つ位置情報を提供します。

## Step 4 – Write JSON file C# – Serialize the result

JSON へのシリアライズは `System.Text.Json` でシンプルに行えます。出力は人が読みやすいように整形します。

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Why we use `System.Text.Json`*: .NET に標準搭載されており高速で、余計な依存関係が不要です。Newtonsoft を好む場合は、数行のコード変更だけで対応可能です。

## Step 5 – Persist the JSON to disk

最後に文字列をファイルに書き出します。これで **write json file c#** の部分が完了です。

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Expected JSON output (sample)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Note:* 正確な数値は画像によって異なりますが、構造は同じです。API、データベース、フロントエンドの可視化ツールへの入力として最適です。

## Full C# OCR tutorial – All steps combined

以下は、すべての手順を統合したコピー＆ペースト可能な完全プログラムです。抜けや「ドキュメント参照」的なショートカットはありません。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Running the code

1. `@"C:\MyProject\…"` の 2 つのパスを実際のディレクトリに置き換えます。  
2. プロジェクトをビルドします（`dotnet build`）し、実行します（`dotnet run`）。  
3. `output.json` を開くと、画像のテキストがきれいに構造化された形で表示されます。

## Common Questions & Edge Cases

**What if my image is blurry?**  
Aspose.OCR には `ocrEngine.ImagePreprocessOptions.Deskew = true;` などの前処理オプションがあります。`Recognize` を呼び出す前に有効化して精度を向上させましょう。

**Can I limit the output to just the plain text?**  
もちろんです。オブジェクト全体ではなく `ocrResult.Text` をシリアライズすれば OK です。

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Do I need to handle multi‑page PDFs?**  
この例は単一画像に焦点を当てていますが、各ページ画像をループで処理し、同じ手順を適用して結果を JSON 配列に集約すれば対応可能です。

## Pro Tips & Gotchas

- **File paths:** `Path.Combine` を使用してハードコーディングされたバックスラッシュを回避しましょう。特に Linux へ移行する場合に有効です。  
- **Memory:** 大量バッチを処理する際は、画像ごとに新しい `OcrEngine` を作成するのではなく、1 つのインスタンスを再利用してください。  
- **JSON size:** テキストだけが必要な場合は `Regions` プロパティを除外してペイロードを小さく保ちます。  
- **Version check:** 本チュートリアルは Aspose.OCR 23.9.0 で検証しました。新しいバージョンでも API は基本的に同じですが、破壊的変更がないかリリースノートは必ず確認してください。

![サンプル OCR JSON 出力 – aspose ocr example](https://example.com/sample-ocr-json.png "aspose ocr example JSON プレビュー")

## Conclusion

私たちは、画像を読み取りテキストを抽出し、純粋な C# で結果を JSON ファイルに書き出す **aspose ocr example** を完成させました。このソリューションは自己完結型で本番環境でも利用可能、言語サポートの追加や信頼度閾値の調整、JSON を下流サービスへ渡すといった拡張も容易です。

次のステップとして、**C# OCR tutorial** と組み合わせて JSON を Azure Cognitive Search にアップロードしたり、請求書からテーブルを抽出したりしてみてください。JSON が手元にあれば、可能性は無限です。

何か独自の工夫があればコメントで共有してください。リポジトリをフォークしたり、GitHub で ping したりしていただいても構いません。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}