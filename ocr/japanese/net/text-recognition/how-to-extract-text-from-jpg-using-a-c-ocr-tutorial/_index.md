---
category: general
date: 2026-09-13
description: C#でJPGファイルからテキストを抽出する方法を学び、画像をOCR用に読み込み、OCR言語を設定し、Aspose OCRを実行するステップバイステップガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from jpg
- load image for ocr
- set ocr language
- c# ocr tutorial
language: ja
lastmod: 2026-09-13
og_description: この簡潔なOCRチュートリアルで、C#を使ってJPGファイルからテキストを抽出しましょう。OCR用に画像を読み込む方法、OCR言語を設定する方法、そして正確な結果を得る方法を学べます。
og_image_alt: Screenshot of C# console output showing extracted Ukrainian text from
  a JPG image
og_title: C#でJPGからテキストを抽出 – 完全OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  headline: How to extract text from JPG using a C# OCR tutorial
  type: TechArticle
- description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  name: How to extract text from JPG using a C# OCR tutorial
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your project folder and run:'
  - name: Create a console application skeleton
    text: 'Create a new console project if you don’t already have one:'
  - name: Load an image for OCR
    text: The first operation after instantiating the engine is to provide the image
      you want to process. Aspose.OCR supports JPEG, PNG, BMP, GIF, and TIFF. In this
      tutorial we work with a JPEG file named **sample_ukrainian.jpg**.
  - name: Set OCR language
    text: OCR accuracy heavily depends on the language model. Aspose.OCR ships with
      data files for more than 30 languages. To recognize Ukrainian text, set the
      language code to `"ukr"`.
  - name: Perform OCR and extract text from JPG
    text: Calling `Recognize()` runs the recognition pipeline and returns the detected
      text as a plain string.
  - name: Run the program and verify the output
    text: 'Compile and execute the application:'
  - name: Loading images from memory or a web request
    text: 'Instead of `ImageStream.FromFile`, you can create a stream from a byte
      array:'
  - name: Processing multiple images in a batch
    text: 'Wrap the OCR logic in a method and iterate over a collection of file paths:'
  - name: Handling errors and edge cases
    text: 'OCR can fail if the image is corrupted or the language data cannot be downloaded.
      Catch exceptions to provide a graceful fallback:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C# OCRチュートリアルでJPGからテキストを抽出する方法
url: /ja/net/text-recognition/how-to-extract-text-from-jpg-using-a-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG からテキストを抽出する C# OCR チュートリアル

.NET アプリケーションで JPG 画像からテキストを抽出したい場合、本ガイドではその手順を詳しく解説します。画像を OCR 用に読み込み、OCR 言語を設定し、Aspose.OCR を使用して認識されたテキストを取得するまでを、単一の自己完結型 C# プログラムで実演します。

このチュートリアルでは、ウクライナ語、英語、またはサポートされている任意の言語で OCR を実行するために必要なすべてを網羅しています。必要なのは Aspose.OCR NuGet パッケージだけで、コードはリソース管理とエラーハンドリングのベストプラクティスに従っています。

## 本チュートリアルで達成できること

このチュートリアルの最後までに、以下ができるようになります。

* ファイルシステムから直接 OCR 用画像を読み込む。  
* ソースドキュメントに合わせて OCR 言語を設定する。  
* JPG ファイルからテキストを抽出し、コンソールに出力する。  
* 他の画像形式や言語に合わせてサンプルをカスタマイズする方法を理解する。

**前提条件**  

* .NET 6.0 SDK 以降がインストールされていること。  
* Visual Studio 2022（または任意の C# IDE）。  
* Aspose.OCR NuGet パッケージ（`dotnet add package Aspose.OCR`）。  

OCR の事前知識は不要です。

## Aspose OCR を使って C# で JPG からテキストを抽出する方法

以下のセクションでは、プロセスをわかりやすくステップに分けて解説します。各ステップにはコードスニペット、ステップの重要性の説明、実際のプロジェクトで役立つヒントが含まれています。

### 手順 1: Aspose.OCR パッケージをインストール

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

このパッケージには `OcrEngine` クラス、言語データファイル、画像読み込みユーティリティが含まれています。一度インストールすれば、`.csproj` を参照するすべてのプロジェクトでライブラリが利用可能になります。

### 手順 2: コンソール アプリケーションの雛形を作成

まだプロジェクトがない場合は、新しいコンソール プロジェクトを作成します。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

自動生成された `Program.cs` を、次のステップで示すコードに置き換えてください。プロジェクトを最小限に保つことで、OCR ワークフローに集中できます。

### 手順 3: OCR 用に画像を読み込む

エンジンをインスタンス化した後の最初の操作は、処理対象の画像を指定することです。Aspose.OCR は JPEG、PNG、BMP、GIF、TIFF をサポートしています。本チュートリアルでは **sample_ukrainian.jpg** という JPEG ファイルを使用します。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 3: Load the image to be processed
        // ImageStream.FromFile reads the file and creates a stream compatible with OcrEngine.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";
        using (var engine = new OcrEngine())
        {
            engine.Image = ImageStream.FromFile(imagePath);
```

**重要ポイント** – 画像を `ImageStream` に読み込むことで、エンジンは元ファイルをロックせずにピクセルデータへアクセスできます。この方法は、メモリ上の画像や Web API から受け取った画像にも適用可能です。

### 手順 4: OCR 言語を設定

OCR の精度は言語モデルに大きく依存します。Aspose.OCR には 30 以上の言語データが同梱されています。ウクライナ語を認識させるには、言語コードを `"ukr"` に設定します。

```csharp
            // Step 4: Set the language for recognition (Ukrainian = "ukr")
            engine.Language = "ukr";
```

英語の場合は `"eng"`、スペイン語の場合は `"spa"` を使用してください。言語コードは ISO 639‑2 標準に従っています。まだダウンロードされていない言語を指定すると、初回実行時にエンジンが自動的に必要なデータを取得します。

### 手順 5: OCR を実行し、JPG からテキストを抽出

`Recognize()` を呼び出すと認識パイプラインが実行され、検出されたテキストがプレーン文字列として返されます。

```csharp
            // Step 5: Perform OCR – required language data will be downloaded automatically if missing
            string recognizedText = engine.Recognize();

            // Step 6: Output the recognized text
            Console.WriteLine("=== Extracted text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**解説** – `using` ブロックにより `OcrEngine` インスタンスが適切に破棄され、ネイティブメモリバッファなどのアンマネージドリソースが解放されます。多数の画像を処理する長時間稼働サービスでは、エンジンの破棄が特に重要です。

### 手順 6: プログラムを実行し、出力を確認

アプリケーションをビルドして実行します。

```bash
dotnet run
```

期待される出力例は次のとおりです。

```
=== Extracted text ===
Привіт, це тестовий текст українською мовою.
```

コンソールに文字化けが表示された場合は、端末が UTF‑8 エンコーディングを使用しているか確認してください（Windows では `chcp 65001`）。また、元画像に十分なコントラストのテキストが含まれていることも重要です。

## C# OCR チュートリアルを他のシナリオに適用する方法

### メモリまたは Web リクエストから画像を読み込む

`ImageStream.FromFile` の代わりに、バイト配列からストリームを作成できます。

```csharp
byte[] imageBytes = await httpClient.GetByteArrayAsync(imageUrl);
engine.Image = ImageStream.FromBytes(imageBytes);
```

この手法は、API エンドポイント経由でアップロードされた画像を処理する際に便利です。

### バッチで複数画像を処理する

OCR ロジックをメソッドにまとめ、ファイルパスのコレクションを反復処理します。

```csharp
static string ExtractText(string path, string language = "eng")
{
    using var engine = new OcrEngine();
    engine.Image = ImageStream.FromFile(path);
    engine.Language = language;
    return engine.Recognize();
}
```

`using` 文をループの外に出すことで、同一の `OcrEngine` インスタンスを再利用でき、オーバーヘッドが削減されます。

### エラーと例外ケースの処理

画像が破損している、または言語データがダウンロードできない場合に OCR は失敗します。例外を捕捉して、適切なフォールバックを提供しましょう。

```csharp
try
{
    string text = ExtractText(imagePath, "ukr");
    Console.WriteLine(text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

例外をログに記録すれば、言語ファイル取得時のネットワーク問題をトラブルシューティングしやすくなります。

## 完全に実行可能なサンプル

以下は `Program.cs` にそのまま貼り付けて使用できる完全版プログラムです。必要な `using` ディレクティブ、コメント、エラーハンドリングがすべて含まれています。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Path to the JPEG image you want to process.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";

        // Ensure the file exists before attempting OCR.
        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        try
        {
            // Create the OCR engine inside a using block to guarantee disposal.
            using var engine = new OcrEngine();

            // Load the image for OCR.
            engine.Image = ImageStream.FromFile(imagePath);

            // Set OCR language (Ukrainian = "ukr").
            engine.Language = "ukr";

            // Perform OCR and retrieve the recognized text.
            string recognizedText = engine.Recognize();

            // Output the extracted text.
            Console.WriteLine("=== Extracted text from JPG ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            // Handle any exceptions that occur during OCR.
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

このコードを実行すると JPG ファイルからテキストが抽出され、コンソールに出力されます。`imagePath` と `engine.Language` を変更すれば、他のファイルや言語でも同様に動作します。

## まとめ

これで、C# で JPG 画像からテキストを抽出する方法がマスターできました。画像を OCR 用に読み込み、OCR 言語を設定し、簡潔な C# OCR チュートリアルを実行する流れです。サンプルは `OcrEngine` の適切な破棄、言語データの自動取得、明確なエラーメッセージ表示といったベストプラクティスを示しています。

今後は以下に挑戦してみてください。

* 異なる言語コード（`"eng"`、`"spa"`、`"fra"` など）を試す。  
* ASP.NET Core API に OCR ロジックを組み込み、オンデマンドで画像処理を提供する。  
* OCR 出力を自然言語処理ライブラリと組み合わせ、抽出したコンテンツを分析する。

コードを自分のプロジェクトに合わせてカスタマイズし、コメントやソーシャルメディアで結果を共有してください。楽しいコーディングを！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能や代替実装アプローチを習得するのに役立ちます。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image in C# – Offline OCR with Aspose (Step‑by‑Step Guide)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}