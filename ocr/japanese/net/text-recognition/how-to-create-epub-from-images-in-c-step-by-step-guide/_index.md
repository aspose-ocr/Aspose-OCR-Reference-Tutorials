---
category: general
date: 2026-03-07
description: Aspose OCR を使用してスキャン画像から ePub を作成する方法 – 画像を ePub に変換し、画像からテキストを抽出し、ePub
  に作者を追加し、OCR 用に画像を読み込む方法を学びます。
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: ja
og_description: C#でスキャン画像からePubを作成する方法。このチュートリアルでは、画像をePubに変換する手順、画像からテキストを抽出する方法、ePubに著者情報を追加する方法、OCR用に画像を読み込む方法を紹介します。
og_title: C#で画像からePubを作成する方法 – 完全ガイド
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: C#で画像からePubを作成する方法 – ステップバイステップガイド
url: /ja/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像から ePub を作成する方法 – 完全ガイド

スキャンしたページのコレクションから **ePub を作成する方法** を考えたことはありませんか？ たとえば、古典小説の PNG が数枚あり、どのデバイスでも読めるきれいな ePub に変換したいとします。 良いニュースは、Aspose OCR を使えば **画像を OCR 用に読み込む**、テキストを抽出し、そして **画像を ePub に変換する** ことが C# の数行で可能です。

このチュートリアルでは、画像の読み込み、テキスト抽出、メタデータの付与（はい、**author を ePub に追加**します）、そして最終的に標準準拠の ePub ファイルを書き出すまでの全工程を解説します。最後まで読むと、すぐに公開できる ePub と各ステップの確かな理解が得られ、マルチページの書籍やカスタムフォント、さらには DRM フリー配布にもコードを応用できます。

## 必要なもの

- **.NET 6** 以上（API は .NET Standard 2.0+ でも動作します）  
- **Aspose.OCR for .NET** – Aspose のウェブサイトから無料トライアルを取得できます。  
- `book_page.png` のようなスキャン画像をディスク上の任意の場所に配置します。  
- お好みの IDE（Visual Studio、Rider、または VS Code – スクリーンショットでは Visual Studio を使用します）。

追加の NuGet パッケージは不要です。Aspose.OCR には ePub エクスポートに必要なものがすべて同梱されています。

---

![スキャン画像から ePub を作成する方法](/images/how-to-create-epub.png "Aspose OCR を使用してスキャン画像から ePub を作成する方法")

## ステップ 1 – プロジェクトのセットアップと Aspose.OCR のインストール

まずは基本から。新しいコンソール アプリを作成します:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

Aspose.OCR パッケージを追加します:

```bash
dotnet add package Aspose.OCR
```

これで完了です。ライブラリには OCR と ePub エクスポート機能の両方が同梱されているため、追加の依存関係は不要です。

## ステップ 2 – OCR 用に画像を読み込む

**画像からテキストを抽出**する前に、OCR エンジンに読み込む対象を渡す必要があります。`ImageStream.FromFile` ヘルパーを使えばこれが簡単に行えます:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **プロのコツ:** 画像が埋め込みリソースにある場合は、`FromFile` の代わりに `ImageStream.FromResource` を使用してください。

## ステップ 3 – 画像からテキストを抽出する

エンジンは実際にピクセルを読み取り、Unicode 文字列に変換します。`Recognize` メソッドがその主要な処理を行います。

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

`Recognize` を別途呼び出す理由は何でしょうか？ これにより、生の OCR 出力を確認したり、言語設定を調整したり、ePub 作成に進む前にスペルチェックを実行したりできます。

## ステップ 4 – ePub エクスポートオプションの準備（author を ePub に追加）

洗練された ePub を作成するにはテキストを投げ込むだけでなく、適切なメタデータも必要です。`EpubExportOptions` クラスを使うと、**author を ePub に追加**したり、タイトルを設定したり、元画像を埋め込むかどうかを決めたりと、簡潔に設定できます。

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

複数ページがある場合は、ループ内で `ocrEngine.Image = …` と `ocrEngine.Recognize()` を呼び続けることができます。各呼び出しで新しいページの内容が同じ ePub ドキュメントに追加されます。

## ステップ 5 – 画像を ePub に変換してエクスポート

テキスト抽出とメタデータ設定が完了したら、最後のステップは ePub ファイルをディスクに書き出すワンライナーです:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

生成された `book.epub` は Calibre、Apple Books、または任意の EPUB 対応リーダーで開くことができます。`IncludeImages = true` を設定したため、元の PNG が画像ページとして表示され、スキャン元の外観が保持されます。

## 完全動作サンプル

すべてをまとめた、完全に実行可能なプログラムは以下です:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### 期待される出力

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

`book.epub` をお好みのリーダーで開くと、タイトルページ、著者行（たとえ「Unknown」と表示されても）、そして選択可能なテキストと共にスキャン画像が表示されます。

## よくある質問とエッジケース

### OCR の言語が英語でない場合は？

Aspose.OCR は 70 以上の言語に対応しています。`Recognize` を呼び出す前に `Language` プロパティを設定するだけです:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### マルチページの書籍はどう処理する？

読み込みと認識のロジックを `foreach` ループで囲みます:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

各イテレーションで新たに認識されたテキストが同じ ePub に追加され、ページ順が保たれます。

### 元画像を除外できますか？

もちろんです。`EpubExportOptions` で `IncludeImages = false` を設定してください。これにより、生成される ePub は純粋なリフロー可能テキストのみとなり、ファイルサイズが大幅に削減されます。

### カスタムフォントやスタイリングはどうですか？

Aspose.OCR の ePub エクスポーターでは、`EpubExportOptions` の `Css` プロパティで CSS スタイルシートを指定できます。これにより、特定のフォントファミリー、行間、余白などを強制できます。

## 結論

これで、C# で Aspose OCR を使用してスキャン画像から **ePub を作成する方法** が分かりました。このチュートリアルでは、**画像を OCR 用に読み込む**、**画像からテキストを抽出する**、**author を ePub に追加する**、そして最終的に **画像を ePub に変換する** までのすべてを単一のエクスポート呼び出しでカバーしました。完全なコードサンプルが手元にあれば、ライブラリ全体をバッチ処理したり、カスタム表紙画像を挿入したり、ワークフローを Web API に統合したりと、ソリューションを拡張できます。

次の課題に挑戦する準備はできましたか？ PDF を ePub に変換してみたり、ノイズの多いスキャンで精度を上げるために OCR の信頼度閾値を調整してみたりしてください。強力な OCR と柔軟な ePub 生成を組み合わせれば、可能性は無限です。

コーディングを楽しみ、作成したばかりの ePub を読んでみてください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}