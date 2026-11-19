---
category: general
date: 2026-04-17
description: C#でAspose OCRを使用して画像からテキストを抽出します。PNGからテキストを読み取る方法、画像をテキストに変換する方法、OCR用に画像をロードする方法を数分で学びましょう。
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、PNGからテキストを読み取り、画像をテキストに変換し、OCR用に画像を効率的にロードする方法を示します。
og_title: C#で画像からテキストを抽出する – 完全なAspose OCRガイド
tags:
- Aspose OCR
- C#
- Image Processing
title: C#で画像からテキストを抽出 – Aspose OCRを使用したC#画像からテキストへの変換
url: /ja/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – 完全な Aspose OCR ガイド

画像からテキストを抽出**したい**けれど、どのライブラリを選べばよいか分からないことはありませんか？ あなただけではありません。PNG のスクリーンショット、スキャンした請求書、あるいは多言語の看板を持っていて、ピクセルを検索可能なテキストに変換したいと考える開発者は多くいます。  

このチュートリアルでは、**PNG からテキストを読み取る**、**画像をテキストに変換する**、そして **OCR 用に画像をロードする** 方法を、Aspose OCR を使ってクリーンでモダンな C# で実装するハンズオンの解決策をご紹介します。最後まで実行可能なプログラムが完成し、任意の .NET プロジェクトにすぐ組み込めます。

## 学べること

- OCR 用に画像ファイルをロードする方法（「load image for OCR」ステップ）  
- 特定の言語グループ向けに Aspose OCR を設定する方法  
- 認識された文字列を抽出し、コンソールに表示する方法  
- 複数言語、巨大ファイル、メモリ管理に関するヒント  

外部ドキュメントは不要です。必要な情報はすべて以下のコードスニペットに含まれています。

## 前提条件

- .NET 6+ SDK（または .NET Core 3.1+ – API は同じです）  
- Visual Studio 2022、VS Code、またはお好みの IDE  
- NuGet パッケージ **Aspose.OCR**（`dotnet add package Aspose.OCR` でインストール）  

これらが揃ったら、さっそく始めましょう。

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## Step 1 – Load the Image for OCR

OCR エンジンに読み取らせる対象を最初に用意します。Aspose OCR はさまざまなフォーマットに対応していますが、PNG はスクリーンショットやスキャン画像でよく使われます。

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** Loading the image correctly ensures that the engine sees the exact pixel data you expect. If you pass a corrupted stream, the recognition will fail silently.

## Step 2 – Create and Configure the OCR Engine

次に `OcrEngine` をインスタンス化します。必要に応じて言語グループを設定できます。多くの西洋文字はデフォルトで問題ありませんが、キリル文字、アラビア文字、またはアジア文字を扱う場合は事前にエンジンへ伝えておくと良いでしょう。

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **Pro tip:** Setting the language narrows the character set the engine searches for, which speeds up recognition and improves accuracy.

## Step 3 – Perform the OCR and Extract Text

いよいよ本番です。先ほどロードした画像で `Recognize` を呼び出し、結果の `Text` プロパティを取得します。

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### Expected Output

`sample.png` に “Hello, World!” が含まれている場合、次のように表示されます。

```
=== OCR Output ===
Hello, World!
```

画像がより複雑（例：複数行のレシート）な場合でも、エンジンは改行を保持したテキストブロックを返します。

## Step 4 – Wrap It All in a Complete Program

以下は新しい C# プロジェクトにコピペできる、完全な自己完結型コンソールアプリケーションです。エラーハンドリングと各部分を説明するコメントが含まれています。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

プロジェクトフォルダーで `dotnet run` を実行すると、コンソールに抽出された文字列が表示されます。これが **extract text from image** ワークフロー全体で、コードは 30 行未満です。

## Step 5 – Common Variations & Edge Cases

### Reading Text from PNG vs. Other Formats

例では PNG を使用していますが、Aspose OCR は JPEG、BMP、TIFF、GIF もサポートしています。ファイル拡張子を変更するだけで、`OcrImage.FromFile` 呼び出しはそのまま機能します。

### Converting Image to Text in a Web API

この機能を HTTP エンドポイントとして公開したい場合、`IFormFile` のアップロードを受け取り、`OcrImage.FromStream` でストリームを `OcrImage` に変換し、文字列を JSON で返すことができます。OCR のコアロジックは同一です。

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### Handling Large Images

高解像度の大きな画像はメモリを大量に消費します。実用的な対策として、エンジンに渡す前に画像をダウンサンプリングする方法があります。

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### Multi‑Language Documents

文書に英語とキリル文字が混在する場合は、言語フラグを組み合わせます。

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

エンジンは両方の文字セットを認識しようと試みます。

### Disposing Resources

`using` 文で `OcrEngine` を囲むことで、ネイティブリソースが確実に解放されます。これを忘れると、特に長時間稼働するサービスでメモリリークの原因になります。

## Pro Tips for Reliable OCR

- **Clear Images Win:** OCR 前に **ImageSharp** などのライブラリで画像をデスキューやノイズ除去など前処理すると効果的です。  
- **Font Size Matters:** 10 px 未満の文字は認識されにくいので、必要に応じて画像を拡大してください。  
- **Check `ocrResult.Confidence`:** `OcrResult` オブジェクトは単語ごとの信頼度スコアも提供します。信頼度が低い部分は手動レビューのフラグとして活用しましょう。  
- **Batch Processing:** 多数のファイルを処理する場合、`OcrEngine` のインスタンスを再利用して初期化コストを削減してください。

## Conclusion

C# で Aspose OCR を使い、**画像からテキストを抽出**する方法を学びました。**load image for OCR**、**convert image to text**、**read text from PNG** のすべてのステップを網羅し、実行可能なサンプルコードを提供しました。実際のシナリオに合わせたバリエーションも解説しています。

次のステップに挑戦してみませんか？ 抽出した文字列を検索インデックスに投入したり、Azure Cognitive Services で翻訳したり、同じテキストレイヤーを持つ検索可能 PDF を生成したり。可能性は無限大です。これで **c# image to text** プロジェクトの確固たる基盤が手に入りました。

ぜひ実験・設定変更・他アプリへの統合を試してみてください。問題があれば下のコメント欄へどうぞ—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}