---
category: general
date: 2026-02-22
description: C#でAspose OCRを使用して画像からテキストを認識します。TIFF画像の読み込み方法、OCRエンジンの作成方法、そして画像からテキストを効率的に抽出する方法を学びましょう。
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: ja
og_description: 画像からテキストをステップバイステップで認識します。TIFF画像の読み込み、OCRエンジンの作成、そしてC#でAspose OCRを使用して画像からテキストを抽出する方法を学びましょう。
og_title: 画像からテキストを認識する – 完全な C# Aspose OCR チュートリアル
tags:
- C#
- Aspose OCR
- Image Processing
title: Aspose OCRで画像からテキストを認識する – 完全C#ガイド
url: /ja/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

block placeholders after paragraphs.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する – 完全な C# Aspose OCR チュートリアル

画像から **テキストを認識** したいけど、最初のコード行でつまずいたことはありませんか？ あなたは一人ではありません。請求書のスキャン、アーカイブのデジタル化、検索可能な PDF ライブラリの構築など、多くのプロジェクトで、画像からきれいなテキストを取得することが最初のハードルです。  

良いニュースです：Aspose OCR を使えば TIFF 画像を読み込み、OCR エンジンを起動し、**画像からテキストを抽出** する処理を数行で実行できます。このチュートリアルでは、解像度の高い TIFF ファイルの読み込みから認識テキストと処理時間の出力まで、全体のフローを順を追って解説します。

また、GPU 加速の無効化やマルチページ TIFF の扱いなど、いくつかの「もしも」シナリオも取り上げますので、実際のデータが少し違う場合でも驚くことはありません。最後まで読めば、**画像からテキストを認識** できるコンソール アプリがすぐに動作するようになります。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core と .NET Framework でも動作します）
- Aspose.OCR NuGet パッケージ（`dotnet add package Aspose.OCR`）
- 処理したい TIFF ファイル（サンプルでは `high_res_page.tif` を使用）
- お好みの IDE（Visual Studio、Rider、VS Code など）

追加のネイティブ ライブラリは不要です。Aspose が内部で全て処理し、オプションで GPU サポートも提供します。

## ステップ 1: TIFF 画像を読み込む

最初に行うべきことは、画像データをメモリに取り込むことです。Aspose はほとんどの一般的なフォーマットに対応した静的メソッド `Image.Load` を提供しています。TIFF もその対象です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**重要ポイント:** TIFF ファイルは複数ページや高解像度データを含むことが多く、他のライブラリでは扱いにくい場合があります。Aspose のローダーはファイルを正しく読み取り、ピクセル深度を保持するため、後続の OCR 精度に直結します。

*プロのコツ:* マルチページ TIFF を扱う場合は `inputImage.Frames` をループして各フレームを個別に処理できます。これにより、後のページに隠れたテキストも見逃しません。

## ステップ 2: OCR エンジンを作成する

画像がメモリにロードされたら、文字を読み取るエンジンが必要です。`OcrEngine` クラスで言語、GPU 使用、その他のオプションを設定します。

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**重要ポイント:** GPU を有効化（`UseGpu = true`）すると、対応マシンでは処理時間が大幅に短縮されますが、CI サーバーや低スペックのノート PC で実行する場合はオフにしても問題ありません。また、適切な言語を選択すると、エンジンが言語固有の辞書をロードするため、文字認識精度が向上します。

*注意点:* `Language` を設定し忘れると、エンジンはデフォルトで英語になるため、ラテン文字以外のスクリプトでは奇妙な結果になることがあります。

## ステップ 3: 画像からテキストを認識する

エンジンの準備ができたら、実際の OCR 呼び出しはシンプルに `Recognize` メソッド一つです。戻り値は抽出されたテキストとパフォーマンス指標を含む `OcrResult` オブジェクトです。

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

`OcrResult` には便利なプロパティが二つあります：

- `Text` – エンジンが読み取れたすべてのテキストのプレーンテキスト表現。
- `ProcessingTime` – OCR に要した時間（ミリ秒単位）。

## ステップ 4: 結果を確認する

最後に、取得した結果を出力します。実際のアプリケーションではデータベースに保存することもあるでしょうが、デモではコンソール出力で十分です。

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**期待される出力**（実際のテキストはもちろん異なります）：

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

出力が文字化けしている場合は、画像が鮮明かつ正しい言語が選択されているか再確認してください。`ocrEngine` の `PreprocessOptions` でノイズ除去などを調整することも可能です。

## エッジケースの取り扱い

### 1. GPU が使えない場合

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

CPU 処理は遅くなります（多くの場合 2〜3 倍）、しかし Windows、Linux、macOS のすべてのマシンで動作します。

### 2. マルチページ TIFF

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

各フレームは別個の画像として扱われるため、ページごとにテキストの塊が得られます。

### 3. 異なる言語

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

言語を切り替えると、対応する文字セットと辞書がロードされ、英語以外の文書でも精度が大幅に向上します。

## 完全動作サンプル

以下は新しいコンソール プロジェクト（`dotnet new console`）にそのまま貼り付けて使用できる完全版プログラムです。これまで説明したすべての要素に加えて、いくつかの安全チェックも含んでいます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

ファイルを保存し、`dotnet run` を実行すると、コンソールに認識されたテキストが表示されます。これで **画像からテキストを認識** するパイプラインが稼働しました。

## よくある質問

**Q: PNG や JPEG でも動作しますか？**  
A: はい。`Image.Load` はフォーマットを自動検出するので、拡張子を `.tif` から `.png`、`.jpg`、あるいは `.bmp` に変更するだけで利用できます。OCR エンジンは同じように処理します。

**Q: 出力に余計な記号が多く含まれます。**  
A: 前処理を有効化してみてください：`ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`。これにより認識前に画像がクリーンアップされます。

**Q: 各単語のバウンディングボックスを取得できますか？**  
A: 可能です。`ocrResult.Regions` には座標情報を持つ `OcrRegion` オブジェクトが含まれます。UI で単語をハイライトしたい場合はこれらをループしてください。

## 結論

本稿では Aspose OCR を用いて C# で **画像からテキストを認識** する方法を示しました。TIFF ファイルの読み込み、**OCR エンジンの作成**、認識実行、結果表示という各ステップを簡潔に解説し、すぐに自分のプロジェクトに組み込める形で提供しました。  

ここからはフォルダ単位のバッチ処理や検索可能インデックスへの保存、OCR と翻訳 API の組み合わせなど、さまざまな応用が考えられます。どのような道を選んでも、基本パターンは変わりません：画像をロードし、エンジンを構成し、認識し、出力を処理する。

TIFF 画像の読み込みや画像からテキスト抽出、OCR エンジンの調整についてさらに質問があれば、下のコメント欄にどうぞ。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}