---
category: general
date: 2026-01-09
description: C#でAspose OCRを使用してTIFFファイルからテキストを抽出します。このステップバイステップのチュートリアルで、各結果の最初の50文字を取得する方法を学びましょう。
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: ja
og_description: C#でAspose OCRを使用してTIFFからテキストを抽出します。このガイドでは、各OCR結果の最初の50文字をステップバイステップで取得する方法を示します。
og_title: Aspose OCRでTIFFからテキストを抽出する – 完全なC#ガイド
tags:
- Aspose OCR
- C#
- TIFF processing
title: Aspose OCR C# を使用した TIFF からのテキスト抽出 – 完全チュートリアル
url: /ja/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFFからテキストを抽出 – 完全な Aspose OCR C# チュートリアル

TIFF 画像から **テキストを抽出** したいことはありますか？どのライブラリを信頼すべきか分からないと感じたことはありませんか？同じ悩みを抱える開発者は多いです。特にパフォーマンスが重要な場合、マルチページ TIFF から検索可能なテキストを取得しようとして壁にぶつかることがよくあります。

この **aspose ocr c# tutorial** では、フルテキストを抽出するだけでなく、各ページの **最初の 50 文字** を取得してプレビューを作成する方法も紹介します。最後まで読めば、任意の .NET プロジェクトに組み込める自己完結型プログラムが手に入ります。

## 必要なもの

- .NET 6（または最近の .NET バージョン） – コードは .NET Core と .NET Framework のどちらでもコンパイル可能です。  
- 有効な Aspose.OCR for .NET ライセンス（無料トライアルから開始可能）。  
- 処理したい `.tif` ファイルが 1 つ以上入っているフォルダー。  
- Visual Studio、VS Code、またはお好みの IDE – サンプルは純粋な C# なのでエディタは問いません。

> **Pro tip:** CI サーバー上で作業している場合は、プロジェクト ファイルに Aspose.OCR NuGet パッケージ（`Aspose.OCR`）を追加してください。ライブラリは完全にマネージドで、ネイティブ依存関係がありません。

## Step 1: Install the Aspose OCR NuGet Package

まずは OCR エンジンをプロジェクトに導入します。ソリューション フォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版（2026 年 1 月時点で 23.9）を取得し、`.csproj` を自動的に更新します。手動で DLL を配置する必要はありません。

## Step 2: Initialize the OCR Engine

次に `OcrEngine` のインスタンスを作成します。これは TIFF の各ページを読み取る「脳」のようなものです。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

エンジンを一度だけインスタンス化する理由は何でしょうか？`RecognizeImages` はファイル パスのコレクションを受け取れるため、内部バッファを再利用でき、バッチ処理の速度が大幅に向上します。

## Step 3: Gather All TIFF Files in One Call

ディレクトリを自分でループする代わりに、.NET に任せて一括取得します。`Directory.GetFiles` メソッドは `IEnumerable<string>` を返すので、そのまま OCR 呼び出しに渡せます。

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **画像が JPEG や PNG の場合は？** 検索パターンを `"*.jpg"` や `"*.*"` に変更すれば OK です。Aspose OCR は一般的なラスタ形式すべてに対応しています。

## Step 4: Run OCR on the Whole Collection

以下の一行で、すべてのファイルを一括で処理します。メソッドは、キーがファイル パス、値が認識テキストを保持する `OcrResult` オブジェクトとなるディクショナリを返します。

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

バッチ処理を行う理由は何ですか？OCR エンジンのロードを繰り返すオーバーヘッドが削減され、マルチコア マシンでは内部で並列化されるため、顕著な速度向上が得られます。

## Step 5: Show a Preview – Get First 50 Characters

多くの UI シナリオでは、全文ではなくスニペットだけが必要です。ここでは最初の 50 文字（ページが短い場合はそれ未満）を抽出し、ファイル名と共に表示します。

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

`Math.Min(50, fullText.Length)` によって文字列の範囲を超えることが防がれ、OCR 結果が 50 文字未満の場合でも `ArgumentOutOfRangeException` が発生しません。

### Expected Console Output

2 つの TIFF ファイル（`invoice1.tif` と `receipt2.tif`）があると仮定すると、コンソールは次のように表示されるかもしれません。

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

各行は省略記号（`...`）で終わり、プレビューが長いテキストの冒頭に過ぎないことを示しています。

## Step 6: Handle Edge Cases and Common Pitfalls

### Empty or Corrupt Files

ファイルの読み取りに失敗した場合でも、`RecognizeImages` は空の `Text` プロパティを持つエントリを返します。次のようにフィルタリングできます。

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Large Batches

数千枚の TIFF を処理するとメモリ使用量が増大します。そのような場合は、画像ごとに `Stream` を受け取るオーバーロードを使用するか、リストを小さなチャンクに分割して処理してください。

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Language and Font Support

文書にラテン文字以外が含まれる場合は、`RecognizeImages` を呼び出す前に言語を設定します。

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

この小さな設定で認識精度が大幅に向上します。

## Step 7: Full Working Example (Copy‑Paste Ready)

以下は新しいコンソール プロジェクト（`dotnet new console`）に貼り付けてそのまま実行できる完全プログラムです。`YOUR_DIRECTORY/Batch` を実際のパスに置き換えてください。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

`dotnet run` でプログラムを実行すると、各 TIFF ファイルの簡潔なプレビューが表示され、**TIFF からテキストを抽出** できたことが確認できます。

## Frequently Asked Questions (FAQ)

**Q: Does this work with multi‑page TIFFs?**  
A: Yes. Aspose OCR treats each page as a separate image internally, so a multi‑page TIFF yields a single concatenated string per file. You can split it later if needed.

**Q: How accurate is the OCR out of the box?**  
A: For clean, high‑resolution scans (300 DPI or higher) you can expect >95 % accuracy on English text. Pre‑processing (deskew, binarization) can push it even higher.

**Q: Can I output the results to a CSV file?**  
A: Absolutely. Replace the `Console.WriteLine` with a `StreamWriter` and write `fileName,preview` rows. Remember to escape commas in the preview text.

## Next Steps and Related Topics

- **Persist OCR results** – Store the full text in a database for searchable archives.  
- **Combine with PDF conversion** – Use Aspose.PDF to embed the extracted text back into searchable PDFs.  
- **Batch processing on Azure Functions** – Scale out the OCR work without managing servers.  

これらすべての拡張は、**TIFF からテキストを抽出** するというコア アイデアに基づきつつ、**最初の 50 文字** を取得して UI プレビューを高速に提供するという目的に合致しています。

---

*Happy coding! If you run into any quirks, drop a comment below – I’ll do my best to help you fine‑tune the OCR pipeline.* 

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}