---
category: general
date: 2026-01-10
description: C#でAspose OCRを使用して画像からテキストを抽出します。バッチ処理でスキャンした文書のテキストを変換し、結果を保存する方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、バッチ処理を利用してスキャンされた文書のテキストを変換する方法を示します。
og_title: C#で画像からテキストを抽出 – 完全なAspose OCRガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#で画像からテキストを抽出 – 完全なAspose OCRガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – 完全な Aspose OCR ガイド

**extract text from image** が必要だったことはありますか？でも、どこから始めればいいか分からない…という方は多いです。スキャンした PDF、マルチページ TIFF、写真ベースのレシートを扱うときに、同じ壁にぶつかる開発者はたくさんいます。良いニュースは、Aspose OCR を使えば、C# の数行で **convert scanned document text** が可能になることです。

このチュートリアルでは、実際のシナリオとして、マルチページ TIFF を取得し、各ページにバッチ OCR を実行し、すべてのページの内容を含む単一のテキストファイルを書き出す手順を解説します。最後まで読むと、すぐに実行できるコンソールアプリが手に入り、各ステップの重要性が理解でき、パスワード保護された画像やカスタム言語パックといったエッジケースへの対応方法も把握できます。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core や .NET Framework でも動作します）  
- Visual Studio 2022（またはお好みのエディタ）  
- Aspose OCR ライセンスファイル（または無料評価モード）  
- フォルダー内に配置したマルチページ画像ファイル（例: `multipage.tif`）  

`Aspose.OCR` 以外の NuGet パッケージは不要です。最初の手順でインストールします。

## Step 1 – Install Aspose OCR and Set Up the Project

まず、新しいコンソールプロジェクトを作成し、Aspose OCR ライブラリを導入します。

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Pro tip:** ライセンスファイル（`Aspose.OCR.lic`）がある場合は、プロジェクトのルートにコピーしてください。実行時にライブラリが自動的に検出します。

この手順の目的は何かというと、`BatchProcessor`、`OcrEngine` など、低レベルの画像処理を抽象化した便利なクラスにアクセスできるようになることです。また、Aspose が提供する最新の OCR アルゴリズムを利用できるようになります。

## Step 2 – Load the Multi‑Page Image with BatchProcessor

`BatchProcessor` は、マルチページ画像の各ページを手動で分割することなく反復処理できるよう設計されています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` はすべてのページをメモリに読み込み、`batchProcessor.Pages` で取得できます。各ページオブジェクトはページ番号（`ocrPage.Number`）を保持しており、後で見出しとして利用します。

## Step 3 – Prepare a StringBuilder to Accumulate Results

すべてのページの OCR 出力をヘッダーで区切って単一のテキストファイルにしたいので、ループ内で文字列を結合する最も効率的な方法は `StringBuilder` です。

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

なぜ `StringBuilder` かというと、ループ内で `+` 演算子で文字列を結合すると、イテレーションごとに新しい文字列が割り当てられ、特に大きな文書ではパフォーマンスが低下します。

## Step 4 – Iterate Over Each Page, Run OCR, and Append Results

チュートリアルの核心部分です。各ページをループし、テキストを認識し、ページマーカーと共に保存します。

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**なぜページごとに新しい `OcrEngine` を作成するのか？**  
一部の開発者は単一のエンジンを再利用して `Image` プロパティを差し替えますが、言語設定や前回の結果が残り、微妙なバグの原因になることがあります。新しいエンジンをインスタンス化することで、常にクリーンな状態から開始できます。

### Handling Common Edge Cases

- **空ページ:** ページに認識可能なテキストがない場合、`ocrEngine.Text` は空文字列になります。`"(No text detected)"` のようなプレースホルダーを挿入すると良いでしょう。  
- **言語選択:** デフォルトでは Aspose OCR は英語を使用します。ドイツ語やフランス語を処理したい場合は、`ocrEngine.Language = Language.German;` のように `Recognize()` 前に設定してください。  
- **パフォーマンスのヒント:** 巨大な TIFF の場合、`ocrEngine.UseParallelProcessing = true;` を有効にするとマルチコアを活用できます。

## Step 5 – Write the Combined Output to a Text File

最後に、蓄積した文字列をディスクに保存します。

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

生成される `multipage_result.txt` の例は次のようになります。

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

これで **extract text from image** が完了し、**convert scanned document text** を検索可能で編集可能な形式に変換できました。

## Bonus – Visual Overview (Image Alt Text)

以下はプロセスを示すシンプルなフローダイアグラムです。  
*Alt text:* “Aspose OCR のバッチ処理を使用して画像からテキストを抽出する方法を示す図”。

![OCR Flow Diagram](placeholder-image-url.png)

*(静的サイトにこのチュートリアルを公開する場合は、プレースホルダーを実際の SVG または PNG に置き換えてください。)*

## Frequently Asked Questions

**Does this work with PDF files?**  
はい、Aspose OCR は PDF ページを画像として読み取れます。まず PDF を画像に変換するか、`Aspose.PDF` の `PdfDocument` を使用して各ページのラスタライズ画像を `OcrEngine` に渡してください。

**What if my TIFF is password‑protected?**  
`BatchProcessor` は暗号化を直接扱いません。`Aspose.Imaging` などのライブラリでファイルを復号化してから OCR パイプラインに渡す必要があります。

**Can I output JSON instead of plain text?**  
もちろん可能です。`StringBuilder` のロジックを JSON シリアライザー（例: `System.Text.Json`）に置き換え、各ページのテキストを `pageNumber` キーの下に格納してください。

## Full Working Example

以下は `Program.cs` にそのまま貼り付けられる完全なプログラムです。すべての using ディレクティブ、エラーハンドリング、コメントを含みます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Run the program with:

```bash
dotnet run
```

コンソールに成功メッセージが表示され、出力ファイルには結合された OCR 結果が格納されます。

## Conclusion

今回、Aspose OCR を使用して **extract text from image** を実現し、マルチページのスキャンファイルをプレーンテキストの検索可能な形式に変換する実用的な方法を示しました。`BatchProcessor` とページごとのクリーンな `OcrEngine` 設定を活用することで、コードベースをシンプルかつ保守しやすく保ちつつ、**convert scanned document text** を確実に行えます。

ぜひ色々試してみてください。別の言語に切り替えたり、JSON 出力に変更したり、アップロードをリアルタイムで処理する Web API に組み込んだりすることも可能です。基本パターンは変わりません—ロード、認識、蓄積、永続化です。

OCR、Aspose のライセンス、または大量ドキュメントバッチの取り扱いについてさらに質問があれば、コメントを残すか、Aspose の公式ドキュメントで詳細を確認してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}