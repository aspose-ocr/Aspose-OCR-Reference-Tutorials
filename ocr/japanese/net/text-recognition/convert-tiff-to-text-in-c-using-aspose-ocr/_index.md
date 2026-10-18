---
category: general
date: 2026-03-05
description: Aspose OCR を使用して C# で TIFF を迅速にテキストに変換します。数分でマルチページ TIFF ファイルから OCR テキストを表示する方法を学びましょう。
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: ja
og_description: Aspose OCR を使用して C# で TIFF をテキストに変換します。このガイドでは、マルチページ TIFF 画像から OCR
  テキストをステップバイステップで表示する方法を示します。
og_title: C#でTIFFをテキストに変換 – 完全なAspose OCRガイド
tags:
- Aspose
- OCR
- C#
- TIFF
title: Aspose OCR を使用して C# で TIFF をテキストに変換する
url: /ja/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert TIFF to Text in C# Using Aspose OCR

C#で **TIFF をテキストに変換** したいですか？ あなたは一人ではありません。多くの開発者がマルチページ TIFF ファイルから可読な文字列を抽出することに苦労しています。朗報は、Aspose OCR C# を使えば作業がほぼ手間なく済み、**OCR テキストをコンソールに表示** したり、数秒で別のシステムに渡したりできます。

このチュートリアルでは、マルチページ TIFF を読み込み、OCR を実行し、各ページのテキストを出力する完全な実行可能サンプルを順を追って解説します。隠された手順や「ドキュメント参照」的なショートカットはありません。最後まで読めば、任意の .NET プロジェクトに貼り付けてすぐに使える自己完結型プログラムが手に入ります。

## What You’ll Need

- .NET 6.0 以降（サンプルは .NET 6 を対象としていますが、.NET 5 でも動作します）  
- 有効な Aspose OCR ライセンスファイル (`Aspose.OCR.lic`)。ライセンスなしでも動作しますが、20 秒間の試用ウォーターマークが表示されます。  
- 処理したいマルチページ TIFF ファイル（ここでは `multipage.tif` と呼びます）。  
- Visual Studio 2022 またはお好みのエディタ—特別な環境は不要です。

上記が揃っていれば、さっそく始めましょう。

## Step 1: Install the Aspose OCR NuGet Package

コードを実行する前に、まずライブラリを取得します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

このワンライナーで最新の安定版（2026 年 3 月時点で 23.9）を取得できます。  

> **Pro tip:** パッケージは常に最新に保ちましょう。新しいリリースには大きな TIFF に対するパフォーマンス改善が含まれていることが多いです。

## Step 2: Set Up the Aspose OCR C# License (Optional but Recommended)

ライセンスなしでも OCR エンジンは動作しますが、出力に試用警告が付加されます。警告を除去したい場合は、エンジンに `.lic` ファイルのパスを指定します。

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

この手順を省略してもコードは動作しますが、結果に余分なテキストが含まれることを覚えておいてください。

## Step 3: Load and Recognize the Multi‑Page TIFF

いよいよ **TIFF をテキストに変換** します。`ImageStream.FromFile` ヘルパーがファイルをエンジンが理解できる形式に読み込みます。その後 `Recognize()` を呼び出すと、各ページのテキストを保持した `OcrResult` オブジェクトが返ります。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Why this matters:** `Recognize()` が本格的な処理を担います—ピクセル解析、言語検出、テキスト行の再構築をすべてネイティブ C# で実行します。結果オブジェクトはページ単位でアクセスできるため、後で **OCR テキストを表示** するのに最適です。

## Step 4: Iterate Through Pages and **Display OCR Text**

取得した結果を使って、ページを順にループし、各ページのテキストをコンソールに出力します。これが画像からプレーンテキストへの変換が実際に見える部分です。

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

プログラムを実行すると、以下のような出力が得られます（TIFF の内容により実際のテキストは異なります）。

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

これで完了です。**TIFF をテキストに変換** し、各ページの **OCR テキストを表示** できました。

## Full Working Example

以下は新しいコンソールプロジェクト（`dotnet new console`）にそのまま貼り付けて使用できる完全なプログラムです。using ディレクティブ、ライセンス処理、エラーチェックがすべて含まれています。

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected output**（省略表示）は前述の通りです。試用ウォーターマークが表示された場合は、ライセンスパスが正しいか再確認してください。

## Common Pitfalls When Converting TIFF to Text

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Out‑of‑memory on huge TIFFs** | エンジンが画像全体を RAM にロードするため。 | `ImageStream.FromFile(..., loadOnlyFirstPage: false)` を使用してページをバッチ処理するか、プロセスのメモリ上限を増やします。 |
| **Garbage characters** | 解像度の低い元画像が OCR エンジンを混乱させます。 | OCR に渡す前に TIFF を前処理（例: DPI を 300 に上げる）します。 |
| **License not applied** | `SetLicense` が例外を投げても無視している。 | 示した通り try/catch でラップし、エラーをログに記録します。 |
| **Missing language data** | デフォルトでは OCR が英語を前提に動作します。 | `ocrEngine.Language = OcrLanguage.French;`（またはサポートされている任意の言語）を `Recognize()` 前に設定します。 |

これらのケースに対処すれば、**変換処理** を **本番環境** でも **スムーズに** 実行できます。

## Next Steps: Going Beyond Simple Display

今や **TIFF をテキストに変換** し **OCR テキストを表示** できるようになったので、次のような拡張も検討できます。

- 抽出したテキストを `.txt` ファイルやデータベースに **保存** して後で分析に利用する。  
- 複数の TIFF を Aspose.PDF を使って検索可能な単一 PDF に **結合** する。  
- **ポストプロセッシング**（スペルチェック、正規表現によるクリーンアップ）を適用して精度を向上させる。  

これらすべては、今回学んだコアパターンを基に構築できます。

---

### TL;DR

本稿では、Aspose OCR C# を用いて **TIFF をテキストに変換** する完全な C# ソリューションを解説しました。`OcrEngine` を作成し、必要に応じてライセンスをロードし、マルチページ TIFF を読み込んで OCR を実行、そして **OCR テキストをページ単位で表示** します。提供したフルサンプルを任意の .NET プロジェクトに貼り付けるだけで、すぐにテキスト抽出を開始できます。

パフォーマンス、言語サポート、他の Aspose 製品との統合について質問があれば、下のコメント欄にどうぞ—Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}