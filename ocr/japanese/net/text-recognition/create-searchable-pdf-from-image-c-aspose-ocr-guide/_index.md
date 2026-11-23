---
category: general
date: 2026-05-06
description: Aspose OCR を使用して C# で画像から検索可能な PDF を作成します。png を PDF に変換し、画像からテキストを抽出して検索可能な
  PDF を生成する方法を学びます。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: ja
og_description: C#でAspose OCRを使用して画像から検索可能なPDFを作成します。このステップバイステップのチュートリアルでは、pngをPDFに変換し、画像からテキストを抽出し、検索可能なPDFを生成する方法を示します。
og_title: 画像から検索可能なPDFを作成 – C# Aspose OCRガイド
tags:
- Aspose
- C#
- OCR
- PDF
title: 画像から検索可能なPDFを作成 – C# Aspose OCR ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から検索可能なPDFを作成 – C# Aspose OCR ガイド

スキャンした画像から **検索可能なPDFを作成** したいと思ったことはありませんか？ PNGのレシートや契約書のJPEG、あるいは検索できるPDFに変換したい任意のビットマップがあるかもしれません。これは特に、フォルダーに放置されたレガシーなスキャン画像を扱うときによくある悩みです。

良いニュースは、Aspose OCR を使えば **画像を PDF に変換** し、隠れたテキストを抽出して、完全に検索可能なドキュメントを数行の C# で作成できることです。このガイドでは **png を PDF に変換**、**画像からテキストを抽出**、さらにマルチページ TIFF の取り扱いといったエッジケースも紹介します。最後まで読めば、任意の .NET プロジェクトに組み込める自己完結型ソリューションが手に入ります。

## 必要なもの

- **.NET 6+**（コードは .NET Framework 4.6+ でも動作します）
- **Visual Studio 2022** またはお好みの IDE
- **Aspose.OCR** NuGet パッケージ（自動的に Aspose.PDF が含まれます）
- 検索可能なPDFに変換したい画像ファイル（PNG、JPEG、BMP、TIFF）

余計なライセンス操作や外部サービスは不要です。NuGet 参照を1つ追加し、数分のコーディングで完了します。

## 手順 1: Aspose.OCR NuGet パッケージをインストール

まずはライブラリをプロジェクトに追加します。Package Manager Console を開いて次のコマンドを実行してください。

```powershell
Install-Package Aspose.OCR
```

この単一コマンドで **Aspose.OCR** とそれが依存する **Aspose.Pdf** アセンブリの両方が取得されるため、画像の読み取りと PDF の書き出しの準備が整います。

> **プロのコツ:** .NET CLI を使用している場合、同等のコマンドは `dotnet add package Aspose.OCR` です。

## 手順 2: OCR エンジンを初期化

`OcrEngine` のインスタンスを作成することが、すべての OCR 作業へのゲートウェイになります。画像を見て文字を「読む」脳のようなものです。

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

*なぜ静的メソッドを呼び出さないのか？* と疑問に思うかもしれませんが、オブジェクト指向のアプローチにより、後から設定（言語、解像度など）を調整でき、全体のフローを変える必要がありません。

## 手順 3: 変換したい画像をロード

ここで **画像を PDF に変換** する精神的なステップです—ビットマップを OCR エンジンに渡します。`"YOUR_DIRECTORY/input.png"` を実際のファイルパスに置き換えてください。

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

**png を pdf に変換** のシナリオがある場合は、PNG を指すだけで構いません。マルチページ TIFF の場合、Aspose.OCR は各フレームを自動的に別ページとして扱います。

## 手順 4: OCR を実行し、必要に応じてテキストを取得

`Recognize()` を呼び出すと、画像を解析し文字を検出、構造化された結果を返します。取得したテキストはログ、検索インデックス、表示などに利用できます。

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **なぜテキストを抽出するのか？** 最終的な PDF に埋め込むだけでなく、生の文字列があると検証や分析に便利です。

## 手順 5: 検索可能なドキュメント用に PDF オプションを設定

Aspose.PDF には **CreateSearchablePdf** という特別な `PdfSaveOptions` モードがあります。これにより、OCR テキストが画像の背後に見えないレイヤーとして埋め込まれ、PDF が検索可能になります。

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

テキストなしの単なる画像 PDF が必要な場合は、代わりに `PdfSaveOptions.CreatePdf()` に切り替えることもできます。ただし、今回の目的は **検索可能な PDF を作成** することなので、検索可能モードが主役です。

## 手順 6: 検索可能な PDF をディスクに保存

ここで全てを結びつけます。`SavePdf` メソッドが画像と隠しテキストを 1 つのファイルに書き込みます。

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

この時点で **検索可能な PDF** が完成し、Adobe Reader で開いて検索ボックスに単語を入力すれば、元の画像ページのままでも即座に該当箇所へジャンプできます。

## 完全な動作例

全体を組み合わせた、すぐに実行できるコンソールアプリです。新しい C# プロジェクトにコピー＆ペーストし、ファイルパスを調整して **F5** を押してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### 期待される出力

プログラムを実行すると、コンソールに次のような出力が表示されます。

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

そして `YOUR_DIRECTORY` 内に `output.pdf` が生成されます。開いて **Ctrl F** を押し、"Invoice" と入力すれば、ページがフラットなスキャン画像のままでも単語に直接ジャンプできます。

## 一般的なバリエーションの処理

### 複数画像を一括変換

PNG が多数入ったフォルダーがあり、1 つの検索可能 PDF にまとめたい場合は、ファイルをループして各画像を別ページとして追加します。

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

また、Aspose.PDF の `PdfFileEditor` を使って一時的な PDF を 1 つの最終ファイルにマージすることもできます。

### 低解像度スキャンへの対処

画像 DPI が 150 未満だと OCR の精度が低下します。画像を渡す前に拡大すると効果的です。

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### 特定の言語を選択

文書が英語でない場合は、`Recognize()` を呼び出す前に言語を設定してください。

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

これらの調整により、**画像からテキストを抽出** がさまざまなシナリオで確実に機能します。

## ビジュアル結果

![Aspose OCR で作成された検索可能なPDF – 検索可能なPDFを作成](https://example.com/images/searchable-pdf.png)

*上のスクリーンショットは、画像は表示されたままですが、テキストレイヤーが検索可能なPDFを示しています。*

## 結論

これで、Aspose OCR と C# を使って任意の画像から **検索可能な PDF** を作成するための完全な本番レシピが手に入りました。**画像を PDF に変換**、**画像からテキストを抽出**、さらに **png を pdf に変換** や **ocr image to pdf** といったエッジケースにも対応しました。コードは自己完結型で、任意の .NET ランタイム上で動作し、バッチ処理やカスタム言語サポートへ拡張可能です。

次は何をしますか？透かしを追加したり、PDF を暗号化したり、抽出したテキストを Elasticsearch などの検索インデックスに流し込んでみてください。可能性は無限大ですし、同じパターン（ロード → 認識 → 保存）が OCR 主導のワークフロー全般で有効です。

問題が発生したり、面白いユースケースを共有したい場合はコメントを残してください。コーディングを楽しみながら、頑固なスキャン画像を検索可能な金の山に変えていきましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}