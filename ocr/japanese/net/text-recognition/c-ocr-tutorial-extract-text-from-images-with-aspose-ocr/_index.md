---
category: general
date: 2026-02-20
description: C# OCRチュートリアルで、画像からテキストを抽出し、PNGから文字を認識し、数行のコードで画像をテキストに変換する方法を紹介します。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: ja
og_description: c# OCRチュートリアルで、画像ファイルからテキストを抽出し、png からテキストを認識し、Aspose.OCR を使用して画像をテキストに変換する方法を段階的に説明します。
og_title: c# OCRチュートリアル – 画像からテキストを抽出するクイックガイド
tags:
- OCR
- C#
- Aspose
title: C# OCRチュートリアル – Aspose.OCRで画像からテキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr チュートリアル – Aspose.OCR を使用した画像からのテキスト抽出

実際の PNG ファイルで動作する **c# ocr tutorial** が必要だったことはありませんか？ あなただけではありません。多くのプロジェクト—例えば請求書スキャン、領収書のアーカイブ、またはシンプルなスクリーンショット解析—で、開発者は信頼できるライブラリなしに **extract text from image** ファイルを試みると壁にぶつかります。  

良いニュースは、Aspose.OCR が全工程をとても簡単にしてくれることです。このガイドでは、PNG から **how to extract text** を示す完全な実行可能な例を順に解説し、各行がなぜ重要かを説明し、ライセンスや画像前処理といったエッジケースにも触れます。最後まで読めば、**recognize text from png** ファイルと **convert image to text** を数行の C# 文だけで実現できるようになります。

## このチュートリアルでカバーする内容

- .NET コンソール アプリで Aspose.OCR エンジンを設定する。  
- ディスクから PNG（またはサポートされている任意のビットマップ）をロードする。  
- OCR を実行し、結果をコンソールに出力する。  
- オプションのライセンス設定、エラーハンドリング、パフォーマンスのヒント。  

外部サービスや隠されたマジックは一切なし—コピー＆ペーストして実行できる純粋な C# コードだけです。スキャンしたドキュメントから **how to extract text** できるか気になったことがあるなら、ぜひ最後までご覧ください。途中でいくつかの “what if” 質問にも答えます。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Framework 4.7+ でも動作します）。  
- Visual Studio 2022（またはお好みのエディタ）。  
- 無料または有料の Aspose.OCR for .NET NuGet パッケージ。  
- `sample.png` という名前の画像ファイルを、参照できるフォルダーに配置する。  

以上です—他のサードパーティツールは不要です。

## c# OCR チュートリアル: Aspose.OCR のセットアップ

まず最初に、Aspose.OCR ライブラリが必要です。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

これにより最新の安定ビルドが取得され、必要な DLL 参照が追加されます。ライセンスファイル（`Aspose.OCR.lic`）がある場合は手元に置いておいてください。無い場合は無料トライアルが動作しますが、OCR 結果に透かしが入ります。

### ライセンスが重要な理由

ライセンスがない場合、エンジンは評価モードで動作し、いくつかの言語では出力に “Powered by Aspose” の行が挿入されます。実運用コードでは、以下のコードのように `SetLicense` を早めに呼び出すことが推奨されます。1 行の呼び出しですが、透かしが除去され、フルスピード処理が可能になります。

## Aspose.OCR を使用した画像からのテキスト抽出

それでは実際の OCR コードに入りましょう。以下は **complete, self‑contained** なプログラムで、すぐにコンパイルして実行できます。

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**ここで何が起きているか？**  

1. **Engine creation** – `OcrEngine` はメインエントリーポイントで、内部で言語データをロードします。  
2. **License loading** – 任意ですが推奨されます。`.lic` ファイルへのパスを指定するだけです。  
3. **Image loading** – `Image.FromFile` は任意のビットマップ形式に対応します。PNG を使用するのは、ロスレス品質を保ち、OCR 精度に重要だからです。  
4. **Recognition** – `ocrEngine.Recognize` が全ての処理を行い、検出された文字列を返します。  
5. **Output** – 結果をコンソールに出力しますが、ファイルやデータベース、UI コントロールに送ることも簡単です。

### 期待される出力

`sample.png` にテキスト “Hello World” が含まれている場合、コンソールは次のように表示します：

```
=== OCR Result ===
Hello World
```

画像がぼやけている、またはラテン文字以外を含む場合、出力に乱れた記号が含まれることがあります。そこで前処理（コントラスト調整、二値化）が必要になります—次のセクションで説明します。

## PNG ファイルからテキストを認識する – ヒントとコツ

PNG は圧縮アーティファクトがなくピクセルを保存できるため人気のフォーマットです。しかし、すべての PNG が同等ではありません。以下は実用的なヒントです：

- **Resolution matters** – 少なくとも 300 dpi を目指してください。これ以下は文字が抜けやすくなります。  
- **Color vs. Grayscale** – OCR 前にカラー PNG をグレースケールに変換すると、精度を損なわずに速度が向上します。  
- **Noise removal** – 小さなノイズはエンジンを混乱させることが多く、シンプルなメディアンフィルタで対処できます。  

以下は、Aspose.OCR に渡す前に画像を前処理する方法を示す簡単なスニペットです：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** 数十枚の画像を処理する場合は、単一の `OcrEngine` をインスタンス化して再利用してください。画像ごとに新しいエンジンを作成すると不要なオーバーヘッドが発生します。

## 画像をテキストに変換する – 高度なオプション

Aspose.OCR は単純なテキスト抽出にとどまりません。**structured data**（単語のバウンディングボックスなど）を返すように指示したり、**language hints** を設定して多言語ドキュメントの精度を向上させることができます。

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

`OcrResult` オブジェクトは各単語の座標を提供し、UI でテキストをハイライトしたり、事後処理（例: 敏感情報のマスク）に便利です。

## 実際のシナリオでテキストを抽出する方法

本節では、実運用環境でよく出てくる “what if” 質問をいくつか取り上げます。

### 画像が PDF ページだった場合は？

Aspose.OCR は PDF を直接読み取れますが、各ページを画像にラスタライズするために Aspose.PDF ライブラリが必要です。ワークフローは次の通りです：

1. `Aspose.Pdf.Document` で PDF をロードする。  
2. ページをビットマップに変換する（`PdfConverter`）。  
3. ビットマップを `OcrEngine.Recognize` に渡す。  

### OCR 結果にゴミ文字が含まれる場合は？

典型的な原因は低解像度、過度のノイズ、または未対応フォントです。次を試してください：

- 画像の拡大（`Bitmap` リサイズ）。  
- シャープフィルタの適用。  
- 正しい言語を指定する（上記参照）。  

### 画像を並列処理する必要がある場合は？

`OcrEngine` はスレッドセーフではないため、**スレッドごとに別々のインスタンス** を作成するか、スレッドローカルプールを使用してください。`Parallel.ForEach` を使った例：

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## 完全な動作例

すべてをまとめると、以下のようなコンパクトなバージョンを新しいコンソールプロジェクトに貼り付けて使用できます：

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

`dotnet run` でコンパイルし、コンソールに抽出されたテキストが表示されるのを確認してください。シンプルですよね？ それが、よく設計された …  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}