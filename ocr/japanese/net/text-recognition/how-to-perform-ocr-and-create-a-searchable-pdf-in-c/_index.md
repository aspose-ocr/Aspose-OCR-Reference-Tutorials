---
category: general
date: 2026-02-14
description: TIFFまたは画像に対してOCRを実行し、OCRを使用して検索可能なPDFに変換する方法を学ぶ—ステップバイステップのC#ガイド。
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: ja
og_description: 画像に対するOCRの実行方法、OCRを使用したPDF変換、そしてAspose OCRで検索可能なPDFを作成する方法を、簡潔なC#チュートリアルで紹介します。
og_title: C#でOCRを実行し、検索可能なPDFを作成する方法
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: C#でOCRを実行し、検索可能なPDFを作成する方法
url: /ja/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

translate all textual content, keep code block placeholders unchanged.

Also need to translate "Running the App" heading etc.

Make sure to keep markdown formatting.

Let's produce final translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行し、検索可能なPDFを作成する方法

スキャンしたドキュメントに対して **perform OCR** が必要だったことはありませんか？しかし、結果を検索可能な PDF に変換する方法が分からずに困ったことはありませんか？同じ悩みを抱える開発者は多く、レガシーな TIFF アーカイブや画像のみの PDF を扱う際に壁にぶつかります。朗報です！C# の数行と Aspose.OCR ライブラリさえあれば、TIFF や任意の画像を数秒で完全に検索可能な PDF に変換できます。

このチュートリアルでは、ライブラリのインストールからマルチページ TIFF の読み込み、`RecognizeToPdf` の呼び出しまで、**convert PDF using OCR** と **make searchable PDF** を実現する手順をすべて解説します。最後まで読めば、画像ソースから検索可能な PDF を生成するコンソール アプリがすぐに実行できるようになります。

## Prerequisites

- **.NET 6.0** 以上（コードは .NET Framework 4.7+ でも動作します）。
- 有効な **Aspose.OCR** ライセンスまたは一時的な評価キー（無料トライアルでテストは十分可能です）。
- **NuGet** パッケージ マネージャーが使用できる Visual Studio 2022（またはお好みのエディタ）。
- `input.tif` という名前の入力ファイルを任意のフォルダーに配置してください。マルチページ TIFF はそのまま使用できます。

> **Pro tip:** Windows を使用している場合、TIFF をコンパイルされた `.exe` と同じフォルダーにコピーすると、パス関連のトラブルを回避できます。

## Step 1: Install the Aspose.OCR NuGet Package

ターミナルでプロジェクト フォルダーを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

これにより、最新の安定版（2026 年 2 月時点で 23.10）と必要な依存関係が取得されます。復元が完了すると、Solution Explorer の **Dependencies** に `Aspose.OCR` が表示されます。

## Step 2: Create a Minimal Console Application

まだコンソール プロジェクトがない場合は新規作成します。

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

自動生成された `Program.cs` を **Step 3** で示す完全なコードに置き換えてください。プログラムの流れは次の通りです。

1. OCR エンジンをインスタンス化する。  
2. ソース画像（またはマルチページ TIFF）を読み込む。  
3. OCR を実行し、出力を直接検索可能な PDF に書き込む。  
4. 処理が成功したことをユーザーに通知する。

## Step 3: Full Working Code – From Image to Searchable PDF

以下が **全体** のソース ファイルです。`Program.cs` にコピー＆ペーストしてください。コメントで非自明な部分を説明しています。

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**期待される結果:** プログラム実行後、`searchable.pdf` というファイルが対象フォルダーに生成されます。Adobe Reader などの PDF ビューアで開き、元の TIFF に含まれる単語で検索してみてください。テキストが即座に見つかり、**made searchable PDF** に成功したことが確認できます。

### Running the App

```bash
dotnet run
```

正しく設定されていれば、次のような出力が得られます。

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

PDF を開き、`Ctrl+F` でソースに含まれる単語を入力すると、ハイライトが正しい位置にジャンプします。

## Step 4: Common Variations and Edge Cases

### Converting a Regular PDF (image‑only) to Searchable PDF

ソースがテキストではなくスキャン画像だけの PDF でも、同じ手順で処理できます。`ImageStream` のソースだけを変更してください。

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

これで **convert pdf using OCR** のシナリオを追加コードなしで実現できます。

### Handling Large Multi‑Page Documents

数百ページを超える文書を扱う場合は、次を検討してください。

- **メモリ上限の増加** (`Engine.MemoryLimit = 2_000; // MB`)。  
- **チャンク処理**: ページのサブセットを読み込み、中間 PDF を書き出し、最後に PDF ライブラリ（例: Aspose.PDF）で結合する。

### Dealing with Languages Other Than English

Aspose.OCR は多数の言語を標準でサポートしています。認識前に言語を設定してください。

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

非ラテン文字の **tiff to searchable pdf** が必要な場合は、該当言語パックがインストールされていることを確認してください。

### What If the Output PDF Is Blank?

- 入力ファイルが破損していないか確認する。  
- OCR エンジンに有効なライセンスがあるか確認する（評価モードではページ数制限がある場合があります）。  
- 画像解像度が最低 300 dpi であることを確認する。低解像度だと認識精度が低下します。

## Step 5: Verifying the Result Programmatically (Optional)

PDF にテキスト層が確実に含まれているか確認したい場合は、Aspose.PDF を使ってテキストを抽出できます。

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

`extracted` が空でなければ、**made searchable pdf** に成功しています。

## Conclusion

**how to perform OCR** で TIFF（または任意の画像）を処理し、**convert PDF using OCR** で検索可能な PDF をシームレスに作成する方法を解説しました。重要な手順は次の通りです。

1. Aspose.OCR をインストール。  
2. `Engine` を初期化。  
3. `ImageStream` で画像を読み込む。  
4. `RecognizeToPdf` を呼び出す。  

ここからは言語設定や大規模バッチ処理、他の PDF 操作との組み合わせを自由に試せます。**tiff to searchable pdf**、**searchable pdf from image**、スキャン PDF への対応も同様のパターンで実現可能です。

次のステップに挑戦してみませんか？OCR を Web API に組み込み、ユーザーがアップロードしたスキャンを即座に検索可能な PDF に変換したり、`OcrEngine` の高度な設定で手書きノートを認識したりしてみましょう。可能性は無限大です—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}