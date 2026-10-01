---
category: general
date: 2025-12-29
description: C#でPDFファイルをOCRし、PDFページからテキストを抽出する方法を学びましょう。このチュートリアルでは、PDFをテキストに変換する方法や、C#でPDFページを読み取るテクニックも紹介します。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: ja
og_description: C#でPDFをOCRする方法を簡潔なガイドで解説。PDFからテキストを抽出し、PDFをテキストに変換し、PDFページを読み取るための完全なコードを入手できます。
og_title: C#でPDFをOCRする方法 – 完全プログラミングガイド
tags:
- OCR
- C#
- PDF processing
title: C#でPDFをOCRする方法 – ステップバイステップガイド
url: /ja/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF を OCR する方法 – ステップバイステップガイド

あなたは C# アプリケーションから直接 **PDF を OCR する方法** を考えたことがありますか？スキャンした請求書が山ほどあり、手動でコピー＆ペーストせずにテキストを抽出したいときに便利です。PDF が画像ベースで従来のテキスト抽出が失敗する場合、これはよくある悩みです。

このチュートリアルでは、**PDF を OCR する方法** を示すだけでなく、*PDF からテキストを抽出する*、*PDF をテキストに変換する*、*C# で PDF ページを読む* 方法を Aspose.OCR ライブラリを使って、すぐに実行できる完全なソリューションとして解説します。曖昧な説明はなく、Visual Studio に貼り付けてすぐに試せるコードだけを提供します。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.7+ でも動作します）  
- **Aspose.OCR** NuGet パッケージ – `dotnet add package Aspose.OCR` でインストール  
- スキャンした PDF（例: `invoice.pdf`）を参照できるフォルダーに配置  
- C# コンソールアプリの基本的な知識  

以上です。既にプロジェクトがある場合は、パッケージを追加するだけで準備完了です。

## ステップ 1: プロジェクトの設定と Aspose.OCR の追加

まず、新しいコンソールプロジェクトを作成（または既存のプロジェクトを使用）し、OCR ライブラリを導入します。

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

このステップが重要な理由: Aspose.OCR は画像解析、レイアウト検出、文字認識という重い処理を担当します。これがなければ、ラスタライザや Tesseract エンジン、そして多数の glue code を自分で組み合わせる必要があります。

## ステップ 2: 名前空間のインポートと OCR エンジンの準備

`Program.cs`（または任意の .cs ファイル）を開き、必要な `using` ディレクティブを追加します。

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

エンジンの作成はシンプルですが、一般的な請求書スキャンでの精度向上のためにいくつかのオプションも設定します。

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**プロのコツ:** 事前に言語が分かっている場合は `Language` を明示的に設定すると、処理が高速化します。

## ステップ 3: PDF ファイルへのパスを指定

処理対象の PDF の絶対パスまたは相対パスを指定します。この例では、ファイルが `Samples` フォルダーにあると想定します。

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

ファイルの存在確認は小さなステップですが、後で発生する曖昧な例外を防げます。

## ステップ 4: 読み取るページを選択

PDF は何十ページもあることがありますが、必要なのは特定のページだけ、例えば合計金額が記載された請求書の2ページ目などです。`RecognizePdf` メソッドを使えば、単一ページまたは全文書を対象にできます。

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

全文書を *PDF からテキストに変換* したい場合は、`pageNumber` 引数を省略するだけです。

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## ステップ 5: 抽出したテキストの表示または保存

OCR エンジンが処理を終えたら、テキストをコンソールに出力したり、`.txt` ファイルに書き込んだり、別のシステム（例: データベース）に渡したりできます。

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**この重要性:** 出力を永続化することで再利用可能な成果物が得られ、下流の分析や検索インデックス作成に最適です。

## 完全動作サンプル

すべてをまとめた、`Program.cs` にコピー＆ペーストしてすぐに実行できる単体プログラムを示します。

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### 期待される出力

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

PDF が鮮明で高解像度のスキャンであれば、出力はほぼ完璧になります。画質が低い画像の場合は、DPI を上げたりフィルタを適用したりといった前処理が必要になることがあります。そのようなシナリオでは Aspose.OCR の `ImagePreprocessingOptions` を調整できます。

## よくある質問とエッジケース

### 1️⃣ PDF がパスワードで保護されている場合は？

Aspose.OCR の `RecognizePdf` のオーバーロードは、パスワードを設定できる `PdfLoadOptions` オブジェクトを受け取ります。

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ 文書全体を一括で OCR できますか？

はい、ページ番号を指定せずに `RecognizePdf(pdfFilePath)` を呼び出すだけです。このメソッドは全ページのテキストを結合した単一の `OcrResult` を返します。

### 3️⃣ テキストベースのライブラリで「PDF からテキストを抽出する」ことと何が違うのですか？

純粋なテキスト抽出（例: iTextSharp 使用）は、選択可能なテキストが既に埋め込まれている PDF のみで機能します。**PDF を OCR する方法** が必要になるのは、スキャンした請求書のように PDF が画像の集合である場合です。そのようなケースでは OCR エンジンが光学文字認識を行い、画像を検索可能なテキストに変換します。

### 4️⃣ 大容量の PDF のパフォーマンスは？

処理時間はページ数と画像解像度にほぼ線形で増加します。大量処理の場合は以下を検討してください:
- OCR を並列実行 (`Parallel.ForEach`)  
- OCR 前に画像 DPI を下げる (`Resolution = 150`)  
- ファイルごとにエンジンを再生成せず、`OcrEngine` インスタンスをキャッシュする

### 5️⃣ 各単語のバウンディングボックスを取得する方法はありますか？

`OcrResult` は `OcrRegion` オブジェクトのコレクションを公開しており、各オブジェクトに座標が含まれます。これらを走査して検索可能な PDF を作成したり、UI で結果をハイライトしたりできます。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## 本番環境向け実装のヒント

- **エラーハンドリング:** OCR 呼び出しを try/catch で囲み、ライブラリ固有の例外を捕捉します。  
- **ロギング:** ページ番号と処理時間を記録し、問題のあるスキャンを特定しやすくします。  
- **メモリ管理:** OCR 前に PDF ページを画像に変換する場合は、大きな `Bitmap` オブジェクトを適切に Dispose します。  
- **セキュリティ:** 生の PDF を安全でないディスクに保存しないでください。OCR エンジンへ直接ストリームすることを検討してください。  

## 結論

これで C# を使って **PDF を OCR する方法** の完全なエンドツーエンドの解答が手に入りました。チュートリアルでは Aspose.OCR のインストール、特定ページの選択、テキスト抽出、一般的なエッジケースの処理まで網羅しました。この基盤があれば、*PDF からテキストを抽出*、*PDF をテキストに変換*、*C# で PDF ページを読む* といった任意の文書処理パイプラインを構築できます。

次のステップに進む準備はできましたか？OCR の出力を Lucene.NET などの全文検索エンジンに流し込んだり、認識したテキストを元画像に重ねて検索可能な PDF を生成したりしてみてください。可能性は無限大です。今手に入れたツールでその一歩を踏み出しましょう。

![OCR 処理の例](image-placeholder.png "PDF ページ上の OCR 処理のイラスト")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}