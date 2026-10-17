---
category: general
date: 2026-02-22
description: C# と Aspose.OCR を使用して JPEG 画像をバッチ OCR する方法。jpg からテキストを抽出し、jpg を txt に変換し、画像を効率的にバッチ処理する方法を学びます。
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: ja
og_description: Aspose.OCR を使用して C# で JPEG 画像をバッチ OCR する方法。このチュートリアルでは、jpg からテキストを抽出し、jpg
  を txt に変換し、数分で画像をバッチ処理する方法を示します。
og_title: C#でJPEG画像を一括OCRする方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でJPEG画像を一括OCRする方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で JPEG 画像をバッチ OCR する方法 – 完全ガイド

フォルダー内の多数の画像を、ファイルごとに別々のプログラムを書かずに **バッチ OCR** したいと思ったことはありませんか？このガイドでは、Aspose.OCR を使って JPEG ファイルを **バッチ OCR** する方法を具体的に示します。数行のコードで **jpg からテキストを抽出** し、**jpg を txt に変換** できます。  

スキャンした請求書が大量に入ったディレクトリを見て「もっと速くできないか？」と思ったことがあるなら、ここが正解です。すべての手順を解説し、各工程の重要性を説明し、さらに大規模バッチ処理のコツもいくつか紹介します。

## 作成するもの

このチュートリアルの最後までに、以下を実行できる小さなコンソールアプリが完成します。

* 指定したディレクトリ内の `*.jpg` ファイルを走査する。  
* 各画像を Aspose OCR エンジンに通す（対応 GPU があれば GPU 加速）。  
* 認識されたテキストを、元画像と同じ場所にある `.txt` ファイルに書き出す。  

外部サービスは使用せず、手動でのコピペも不要。純粋に C# と信頼性の高い OCR ライブラリだけです。

### 前提条件

* .NET 6.0 以上（コードは .NET Framework 4.8 でも動作）。  
* Visual Studio 2022 または C# に対応したエディタ。  
* Aspose.OCR NuGet パッケージ（無料トライアルでテスト可能）。  

これらが揃っていない場合は、ここで止めてインストールしてください。以降の手順はすでに環境が整っていることを前提とします。

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## 手順 1: Aspose.OCR NuGet パッケージをインストール

まずはプロジェクトに OCR ライブラリを追加します。ソリューションフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の NuGet パッケージマネージャ UI を使っても構いません。これで GPU 対応バイナリが必要な場合は自動的に取得されます。

> **プロのコツ:** サーバーで GPU が使えない場合は、後述の `UseGpu = false` を設定すればエンジンは自動的に CPU にフォールバックします。

## 手順 2: OCR エンジンを構成

`OcrEngine` の生成と設定が、実際の処理の出発点です。ここで使用言語、GPU の有無、出力フォーマットなどを指定します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**重要ポイント:** `Language` を設定すると文字セットが絞り込まれ、精度が向上します。`UseGpu` を有効にすると、最新のグラフィックカード上で処理時間が半分になることもあり、**画像のバッチ処理** では大きなメリットです。

## 手順 3: フォルダー内のすべての JPEG ファイルを認識

ここからは Aspose に処理を任せます。静的メソッド `BatchProcessor.RecognizeFolder` がディレクトリを走査し、該当ファイルごとに OCR を実行して結果コレクションを返します。

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**エッジケース:** フォルダーにサブフォルダーが含まれる場合は、`SearchOption.AllDirectories` オーバーロード（または手動で再帰処理）を追加して、すべてのファイルを対象にできます。

## 手順 4: 各結果を対応する `.txt` ファイルに書き出す

`OcrResult` オブジェクトは元画像のパスと認識テキストを保持しています。拡張子を変更しながらループで書き出します。

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

これで完了です。各 JPEG の隣にテキストファイルが生成され、下流プロセスや検索インデックス、単なるアーカイブとして活用できます。

## 手順 5: アプリを実行し出力を確認

プログラムをビルドして実行します。

```bash
dotnet run
```

フォルダーに `invoice1.jpg` と `receipt2.jpg` があると、`invoice1.txt` と `receipt2.txt` が同じ場所に生成されます。任意の `.txt` を開くと、OCR の生データが表示されます（例:）。

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

テキストが乱れている場合は、画像のコントラストが十分か、`Language` プロパティが文書の言語と合っているかを再確認してください。

## 手順 6: 高度な調整（任意）

### a) 低品質スキャンへの対応

JPEG がノイズが多い場合は、Aspose.Imaging などで前処理できます。

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) バッチの並列化

多数のファイルがありマルチコア CPU を活用したい場合は、ループを `Parallel.ForEach` でラップします。

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

ただし、Aspose OCR エンジン自体はスレッドセーフではないため、スレッドごとに別々の `OcrEngine` インスタンスを用意するか、キューで管理する必要があります。

### c) ロギングとエラーハンドリング

堅牢な実装では失敗をログに残し、後でリトライできるようにします。

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## 完全動作サンプル

すべてをまとめたフルプログラムを以下に示します。新しいコンソールアプリにコピー＆ペーストして使用してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

実行してコンソール出力を確認し、数個の `.txt` ファイルを開いて **jpg からテキストを抽出** できていることを確かめましょう。  

---

## 結論

C# と Aspose.OCR を使って JPEG 画像のコレクションを **バッチ OCR** し、各画像を検索可能な `.txt` ファイルに変換する方法を解説しました。コンパクトで GPU 対応、エラーハンドリングや画像前処理、並列実行への拡張も容易です。  

さらに踏み込むなら次のステップを検討してください。

* `searchPattern` を変更して他のフォーマット（`*.png`、`*.tif`）も **バッチ処理**。  
* Lucene.NET などの全文検索エンジンと組み合わせて、即時ドキュメント検索を実現。  
* OCR 結果から直接検索可能な PDF を生成する Aspose の PDF 変換機能を活用。  

言語を変える、GPU をオフにする、テキストをデータベースに流し込むなど、自由に実験してください。基本パターンは変わりませんので、これを土台にさまざまな OCR パイプラインを構築できます。

コーディングを楽しんで、あなたの OCR パイプラインが常に高速かつ正確でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}