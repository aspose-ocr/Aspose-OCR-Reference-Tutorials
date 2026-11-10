---
category: general
date: 2026-03-17
description: c# OCR チュートリアル – 画像ファイルからテキストを抽出し、WebP 写真からテキストを読み取り、シンプルな OcrEngine
  を使用して画像をテキストに変換する方法をご紹介します。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: ja
og_description: C# OCRチュートリアルでは、画像ファイルからテキストを抽出し、WebP写真からテキストを読み取り、数行のコードで画像をテキストに変換する方法を紹介します。
og_title: C# OCRチュートリアル – 画像から数分でテキストを抽出
tags:
- C#
- OCR
- Image Processing
title: C# OCRチュートリアル：画像（WebP、写真）からテキストを抽出する – クイックガイド
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – 画像からテキストを抽出 (WebP, 写真)

画像ファイルからテキストを抽出する必要があったが、C#でどこから始めればよいか分からなかったことはありませんか？WebP のスクリーンショットや、レシートの JPEG、スキャンした PDF ページなど、画像内の文字だけが欲しい場合に。この **c# OCR tutorial** では、写真からテキストを読み取り、WebP やその他の最新フォーマットに対応し、画像をプレーンテキストに変換する、すぐに実行できる完全なサンプルを数行で紹介します。

**What’s the payoff?** 任意のテキスト画像を検索可能な文字列に変換したり、データベースに投入したり、下流の AI パイプラインに渡したりできるようになります。魔法ではなく、堅実な OCR エンジンといくつかの .NET API、そして各ステップの「なぜ」についての明確な説明です。

## 必要なもの

- **.NET 6 SDK** (またはそれ以降)。以下のコードは .NET 6+ でコンパイルされ、Windows、Linux、macOS 上で動作します。
- **Visual Studio 2022** またはお好みのエディタ (VS Code でも問題ありません)。
- **`Microsoft.Windows.SDK.Contracts`** NuGet パッケージ ( `Windows.Media.Ocr` を提供)。インストールは以下の通り:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- 処理したい画像ファイル – 本チュートリアルでは、`YOUR_DIRECTORY` フォルダに置いた **WebP** 写真 `photo.webp` を使用します。

> プロ・チップ: 非 Windows プラットフォームの場合、`OcrEngine` を **Tesseract** のようなクロスプラットフォームライブラリに置き換えることができます。周囲のコードはほぼ同じままです。

## Step 1: C# OCR チュートリアル プロジェクトのセットアップ

まず、空のコンソール アプリを作成します。ターミナルを開いて次を実行してください:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

上記のように必要なパッケージを追加し、IDE でプロジェクトを開きます。この雛形により、**c# OCR tutorial** のためのクリーンな状態が得られます。

## Step 2: 名前空間のインポートと画像の準備

`OcrEngine`、`SoftwareBitmap`、画像読み込みヘルパーを見つけられるように、いくつかの `using` ディレクティブが必要です。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Why these namespaces?**  
> `Windows.Media.Ocr` は実際に認識を行う `OcrEngine` クラスを含んでいます。`Windows.Graphics.Imaging` は画像（WebP を含む）をエンジンが理解できる `SoftwareBitmap` にデコードします。`System.IO` と `Windows.Storage.Streams` のヘルパーにより、ファイルの読み込みが簡単になります。

次に画像をロードします。組み込みのデコーダは WebP、HEIF、PNG、JPEG などに対応しているため、追加プラグインなしで **WebP からテキストを読み取る** ことができます。

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Edge case:** 画像がすでに白黒の場合、変換ステップをスキップできます。グレースケール変換はわずかなパフォーマンス向上で、ノイズの多い写真の認識精度を向上させることが多いです。

## Step 3: OCR エンジンの実行 – 写真からテキストを認識

これが **c# OCR tutorial** の核心です。`OcrEngine` のインスタンスを作成し、ビットマップを渡して認識されたテキストを取得します。

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**What’s happening?**  
- `TryCreateFromUserProfileLanguages()` は、Windows ユーザープロファイルに設定された言語を取得します。通常は英語、スペイン語などがカバーされます。特定の言語が必要な場合は `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))` を使用してください。  
- `RecognizeAsync` はバックグラウンドスレッドで重い処理を実行し、生の文字列、単語のバウンディングボックス、信頼度スコアを含む `OcrResult` を返します。  
- 最後に `ocrResult.Text` を出力し、**convert image to text** の結果を他の処理に渡すことができます。

## Step 4: 完全な実行可能サンプル

すべてをまとめると、`Program.cs` にコピー＆ペーストできる自己完結型プログラムがこちらです。コンパイル・実行でき、`photo.webp` から抽出したテキストを出力します。

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### 期待される出力

`photo.webp` に “Hello, world! This is a test.” という文が含まれている場合、以下のような出力が得られます:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

改行位置は元画像のレイアウトに依存しますが、**extract text from image** の結果は常にプレーンな文字列となり、さらに操作可能です。

## よくある質問とエッジケース

### 他の画像フォーマットでも動作しますか？

もちろんです。使用しているデコーダ (`BitmapDecoder`) は JPEG、PNG、BMP、GIF、**WebP**、HEIF などを自動検出します。そのため、コードを変更せずに **WebP**、JPEG、さらには TIFF からもテキストを読み取れます。

### OCR エンジンが低い信頼度を返した場合は？

`ocrResult.Lines` と各 `OcrWord` の `ConfidenceScore` を確認できます。スコアが閾値（例: 0.6）未満の場合、以下を検討してください:

- 画像の前処理（コントラスト増加、シャープ化、デスキュー）。
- 高解像度の元画像を使用。
- 多言語サポートのために **Tesseract** などの専用ライブラリに切り替える。

### 同一画像内で複数言語を扱うには？

各言語ごとに別々の `OcrEngine` インスタンスを作成し、順次実行するか、混在言語検出をサポートするライブラリを使用します。組み込みエンジンの場合、`Language` オブジェクトを渡すことができます:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Linux/macOS でも実行できますか？

`Windows.Media.Ocr` API は Windows 専用です。非 Windows プラットフォームでは OCR 部分を **Tesseract**（`Tesseract.Net.SDK` 経由）に置き換えてください。ロードと前処理のコードは同一なので、残りの **c# OCR tutorial** はそのまま適用できます。

## 精度向上のためのプロ・ティップス

- **Resize** 大きな画像は、長辺が最大 2000 px になるようにリサイズします – OCR エンジンは中程度のサイズで高速に動作します。
- **Denoise** 画像が粒状の場合、シンプルなガウシアンブラーでノイズ除去します。
- **Deskew** テキストが完全に水平でない場合、ビットマップをデスキューします。`SoftwareBitmap` は `OcrEngine` に渡す前に回転可能です。
- **Cache** バッチで多数の画像を処理する場合は `OcrEngine` インスタンスをキャッシュします。繰り返し作成するとオーバーヘッドが増えます。

## 関連トピック

- **Convert image to text** を **Tesseract** で使用し、クロスプラットフォームプロジェクトに活用。
- **Extract text from PDF** は、各ページを画像にレンダリングしてから実行。
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}