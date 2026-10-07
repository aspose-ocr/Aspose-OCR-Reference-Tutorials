---
category: general
date: 2026-02-19
description: Aspose OCR を使用して C# で画像から検索可能な PDF を作成します。画像からテキストを抽出し、検索可能な PDF に変換する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- extract text from image
- image to searchable pdf
- ocr image c#
- searchable pdf from image
language: ja
og_description: C# と Aspose OCR を使用して画像から検索可能な PDF を作成します。このチュートリアルでは、画像からテキストを抽出し、検索可能な
  PDF を生成する手順をステップバイステップで示します。
og_title: C#で画像から検索可能なPDFを作成する – 完全ガイド
tags:
- C#
- OCR
- PDF
title: C#で画像から検索可能なPDFを作成する – 完全ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像から検索可能なPDFを作成する – 完全ガイド

スキャンした契約書から **searchable PDF** を作成する必要があったことはありませんか？でも、どこから始めればいいか分からないことも多いでしょう。最初に OCR 主導のワークフローに取り組む開発者の多くがこの壁にぶつかります。良いニュースは、数行の C# と Aspose OCR を使えば、任意のビットマップ（TIFF、JPEG、PNG…）を数秒で検索可能な PDF に変換できるということです。  

このチュートリアルでは、ライブラリのインストール、画像からテキストを抽出すること、最終的な **image to searchable PDF** ファイルの書き出しまで、全プロセスを順に解説します。また、他のシナリオでの **extract text from image** の方法や、下流の検索エンジンにとって「隠しテキスト層」が重要な理由にも触れます。

> **Quick note:** 以下のコードはすべてすぐに実行可能です。追加のスニペットや外部ドキュメントを探す必要はありません。

## 必要なもの

本格的に始める前に、以下の前提条件が揃っていることを確認してください。

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6 SDK (or later) | モダンな言語機能とパフォーマンス向上 |
| Visual Studio 2022 (or VS Code) | IntelliSense がある IDE で開発が楽になる |
| Aspose.OCR NuGet package | OCR エンジンと PDF ライターを提供 |
| A sample image (`input.tif`) | 検索可能な PDF に変換する元画像 |

既に .NET プロジェクトがある場合は、「新しいプロジェクトの作成」ステップを省略し、直接 NuGet のインストールに進んで構いません。

## 手順 1: Aspose OCR NuGet パッケージのインストール

まずはじめに、重い処理を担うライブラリを追加します。

```bash
dotnet add package Aspose.OCR
```

この一行でコア OCR エンジン、PDF ライター、そしてすべてのネイティブ依存関係が取り込まれます。Visual Studio では、プロジェクトを右クリック → **Manage NuGet Packages** → *Aspose.OCR* を検索し、**Install** をクリックすることでも追加できます。

> **Pro tip:** パッケージは常に最新の状態に保ちましょう。2026 年 2 月現在、最新バージョンは 23.9 で、高解像度 TIFF のパフォーマンスが改善されています。

## 手順 2: プロジェクトの骨組みを設定

まだ持っていない場合は、シンプルなコンソールアプリを作成します。

```bash
dotnet new console -n PdfDemo
cd PdfDemo
```

`Program.cs`（または名前付きクラスが好みなら `PdfDemo.cs`）を開き、デフォルトの “Hello World” コードを削除します。これを、画像から **searchable PDF** を **creates searchable PDF** する完全な実行可能サンプルに置き換えます。

## 手順 3: OCR エンジンの初期化 – “Extract Text from Image”

OCR エンジンはスキャン対象の言語を認識する必要があります。ほとんどの英語の契約書では `Language.English` を設定します。多言語文書がある場合は、後から Aspose の言語パックをロードして使用できます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Perform OCR on the input image – this is where we **extract text from image**
        OcrResult ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Write the OCR result to a searchable PDF (image + hidden text layer)
        PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");

        // 4️⃣ Notify that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

### このようにエンジンを初期化する理由

* **Language selection** は認識器に期待すべき文字セットを伝え、精度を大幅に向上させます。  
* **`RecognizeImage`** は元のビットマップと抽出された Unicode テキストの両方を含む `OcrResult` を返します。この二重表現が、後の **image to searchable PDF** 変換を可能にします。

## 手順 4: 隠しテキスト層の書き込み – **Image to Searchable PDF** の生成

`PdfResultWriter` は `OcrResult` を受け取り、各ページに元のラスタ画像と **plus** の不可視テキスト層を持つ PDF を作成します。検索エンジン（および PDF ビューア）はこの隠しテキストをインデックスでき、文書が検索可能になります。

```csharp
// Inside Main, after OCR succeeds
PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");
```

内部では、Aspose が PDF の *ActualText* 属性を使用してテキストを埋め込みます。生成されたファイルを Adobe Acrobat で開き、テキスト選択を行うと、画像として表示されていても基になる単語をコピーできることが確認できます。

## 手順 5: 出力の検証

Run the program:

```bash
dotnet run
```

You should see:

```
Searchable PDF created.
```

`YOUR_DIRECTORY` に移動し、`contract_searchable.pdf` を開きます。単語を選択してみてください—選択が不可視テキストをハイライトすれば、元の画像から **create searchable pdf** に成功したことになります。

### 簡易チェック

*PDF をテキスト抽出ツール（例: Adobe Reader → Edit → Copy）で開き、可読なテキストが貼り付けられれば隠し層は機能しています。* 文字化けする場合は、元画像の解像度が十分か（300 dpi が目安）を再確認してください。

## 手順 6: 一般的なエッジケースの処理

### 低解像度スキャン

TIFF が 200 dpi 未満の場合、OCR の精度が低下する可能性があります。認識前に画像を拡大（`System.Drawing` や `ImageSharp` を使用）すると、結果が改善されることが多いです。

```csharp
using System.Drawing;

// Load, upscale, then feed to OCR
Bitmap lowRes = new Bitmap(@"YOUR_DIRECTORY/input.tif");
Bitmap highRes = new Bitmap(lowRes, new Size(lowRes.Width * 2, lowRes.Height * 2));
highRes.Save(@"YOUR_DIRECTORY/upscaled.tif");
```

### 複数ページ文書

複数ページの TIFF を扱う場合は、各フレームをループ処理します。

```csharp
using System.Drawing.Imaging;

// Assume input.tif contains multiple frames
using (Image multiPage = Image.FromFile(@"YOUR_DIRECTORY/input.tif"))
{
    int pageCount = multiPage.GetFrameCount(FrameDimension.Page);
    for (int i = 0; i < pageCount; i++)
    {
        multiPage.SelectActiveFrame(FrameDimension.Page, i);
        string tempPath = $@"YOUR_DIRECTORY/page_{i}.tif";
        multiPage.Save(tempPath, ImageFormat.Tiff);

        OcrResult pageResult = ocrEngine.RecognizeImage(tempPath);
        PdfResultWriter.Write(pageResult, $@"YOUR_DIRECTORY/page_{i}_searchable.pdf");
    }
}
```

その後、個々の PDF を Aspose.PDF や他の PDF ライブラリで結合できます。

## 完全動作例（すべての手順を1ファイルにまとめたもの）

以下は、`Program.cs` にコピー＆ペーストできる、完全な自己完結型プログラムです。インストール、OCR、PDF 生成、簡易エラーハンドリングラッパーを網羅しています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // Path to the source image – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        const string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";

        try
        {
            // 👉 Step 1: Initialize OCR engine (English language)
            OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

            // 👉 Step 2: Run OCR – this **extracts text from image**
            Console.WriteLine("Running OCR on image...");
            OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 👉 Step 3: Convert OCR result to a searchable PDF
            Console.WriteLine("Creating searchable PDF...");
            PdfResultWriter.Write(ocrResult, outputPath);

            Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

### 期待される結果

* ディレクトリに `contract_searchable.pdf` という名前のファイルが作成されます。  
* 任意の PDF ビューアで開くと元のスキャン画像が表示されますが、テキストを選択すると実際の単語がコピーされます。  
* 文書内検索（Ctrl + F）ですぐに抽出された語句がヒットします。

## よくある質問

**Q: 他の言語でも動作しますか？**  
A: もちろんです。`Language.English` を `Language.French`、`Language.German` などに置き換えるか、Aspose からカスタム言語パックをロードしてください。

**Q: 完全にテキストのみの PDF が必要な場合は？**  
A: OCR 後に画像を省略し、`PdfResultWriter.WriteTextOnly(ocrResult, path)`（新しい Aspose バージョンで利用可能）を使用できます。

**Q: フォントを埋め込んで描画を改善できますか？**  
A: はい。PDF ライターは標準フォントセットを自動的に埋め込みますが、企業フォントが必要な場合はカスタム `PdfSaveOptions` オブジェクトを提供できます。

## まとめ

C# と Aspose OCR を使用して画像から **create searchable pdf** を作成しました。**extract text from image** から最終的な **image to searchable pdf** ファイルまでを網羅しています。このコードは本番環境でも使用可能で、より大規模なバッチ処理や多言語対応、さらには Web API への統合にも対応できる堅実な基盤が手に入ります。

### 次のステップは？

* スキャンしたフォルダ全体を 1 つの統合検索可能 PDF に変換してみてください。  
* Aspose PDF の暗号化機能を試してみる

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}