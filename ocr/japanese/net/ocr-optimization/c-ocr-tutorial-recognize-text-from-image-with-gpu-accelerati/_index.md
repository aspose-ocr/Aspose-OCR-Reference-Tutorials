---
category: general
date: 2026-01-15
description: c# OCRチュートリアルで、画像からテキストを認識し、請求書からテキストを抽出し、GPU上で Aspose OCR を使用して画像をテキストに変換する方法を示します。
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: ja
og_description: GPU上のAspose OCRを使用して、画像からテキストを認識し、請求書からテキストを抽出し、画像をテキストに変換する方法を教えるC#
  OCRチュートリアル。
og_title: c# OCRチュートリアル – 高速GPU搭載テキスト認識
tags:
- OCR
- C#
- Aspose
- GPU
title: C# OCR チュートリアル – GPU 加速で画像からテキストを認識
url: /ja/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – GPUアクセラレーションで画像からテキストを認識

実際に仕事を完了できる **c# ocr tutorial** が必要だったことはありませんか？無限の試行錯誤なしで。高解像度の請求書を見て、数秒で **extract text from invoice** ファイルを抽出する方法を考えているかもしれません。良いニュースは、車輪の再発明は不要です—Aspose.OCR がクリーンで GPU 加速された API を提供し、重い処理を代行してくれます。

このガイドでは、**recognize text from image** ファイルを認識し、**convert image to text** を行い、最も一般的な落とし穴に対処する完全な実行可能サンプルを順に解説します。最後まで読むと、領収書からスキャンした契約書まで、あらゆる文書の画像を読み取り、クリーンで検索可能なテキストを出力できる自己完結型プログラムが手に入ります。

## 学習できること

- Aspose.OCR NuGet パッケージのインストールと参照方法。
- GPU 上で実行するよう OCR エンジンを構成し、超高速パフォーマンスを得る方法。
- `OcrImage.FromFile` を使用した **load image for ocr** の正しい方法。
- `Recognize` を希望の言語で呼び出し、結果を取得する方法。
- マルチページ PDF、低コントラストスキャン、エラーハンドリングに対処するためのヒント。

Aspose の事前経験は不要です；動作する .NET 開発環境（Visual Studio 2022 または VS Code）と、控えめな GPU（統合型 Intel GPU でも可）があれば十分です。

---

## Step 1 – Aspose.OCR のインストールとプロジェクトの準備

まず最初に、Aspose.OCR ライブラリが必要です。最も簡単な方法は NuGet を使用することです。

```bash
dotnet add package Aspose.OCR
```

> **プロのヒント:** .NET 6 以降を対象としている場合、パッケージは Windows、Linux、macOS 用のネイティブ GPU バイナリを自動的に取得します。コピーする余分な DLL はありません。

パッケージを追加したら、プロジェクト ファイル（`*.csproj`）を開き、参照が正しいか確認します。

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

これでコーディングを開始するために必要なものはすべて揃いました。

## Step 2 – GPU 対応 OCR エンジンの作成 (c# ocr tutorial)

**c# ocr tutorial** の中心は `OcrEngine` です。`Engine = Engine.Gpu` と設定することで、Aspose に CPU ではなくグラフィックカードを使用させます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **GPU の理由?** GPU は数千のピクセルを並列に処理でき、大きく高 DPI の画像に対して OCR 時間を数秒から数分の一秒に短縮します。

## Step 3 – OCR 用画像のロード (load image for ocr)

画像を正しくロードすることは、思っている以上に重要です。`OcrImage.FromFile` は PNG、JPEG、BMP、TIFF、さらには PDF ページもサポートします。また、画像の DPI を読み取り、精度に影響します。

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**注:** PDF を扱う場合、各ページを `OcrImage` として抽出し、1 ページずつ処理できます。

## Step 4 – 画像からテキストを認識 (recognize text from image)

さあ、魔法が始まります。エンジンに英語テキストの認識を依頼しますが、Aspose がサポートする任意の言語（スペイン語、ドイツ語、中国語など）を指定できます。

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

`result.Text` プロパティにはプレーンな文字列が格納されています。各単語の信頼度スコアが必要な場合は、`result.Regions` を調べることができます。

### 期待される出力

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

画像がぼやけている場合、文字化けした文字が表示されることがあります—このとき Step 3 の前処理が役立ちます。

## Step 5 – 請求書からテキストを抽出 – 実務例

スキャンした請求書が入ったフォルダーがあり、合計金額を抽出したいとします。以下は、シンプルな正規表現を使用した前述コードの簡易拡張です。

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

OCR 結果を出力した直後に `ExtractTotalAmount(result.Text);` を呼び出します。これにより、生の文字列が得られたら **extract text from invoice** ファイルがいかに簡単に抽出できるかが分かります。

## Step 6 – 画像を一括でテキストに変換 (convert image to text)

デモでは単一ファイルの処理で問題ありませんが、実運用コードでは数十から数百の画像を処理する必要があります。以下はディレクトリ全体を処理する簡潔なループです。

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

`ProcessFolder(ocrEngine, @"C:\Invoices")` を実行すると、フォルダー内のすべてのサポート対象ファイルに対して **convert image to text** が行われ、GPU の高速化が活かされます。

## エッジケースと一般的な落とし穴

| 状況 | 発生理由 | 簡単な対策 |
|-----------|----------------|-----------|
| **Low‑contrast scan** | OCR が前景と背景を区別できずに苦労するため。 | コントラストを上げる（`ImagePreprocessor.AdjustContrast`）か、適応的閾値処理を適用する。 |
| **Multi‑page PDF** | `OcrImage.FromFile` は最初のページしか読み込まないため。 | `PdfDocument` を使用して各ページを `OcrImage` として抽出し、ループ処理する。 |
| **Unsupported language** | デフォルトの言語設定が英語になっているため。 | `Language.Spanish` など、サポートされている列挙値を渡す。 |
| **GPU not detected** | ネイティブバイナリが欠如しているか、ドライバが古いため。 | GPU ドライバが最新であることを確認し、`-runtime` フラグ付きで NuGet パッケージを再インストールする。 |
| **Out‑of‑memory on huge images** | GPU メモリが制限されているため。 | 画像を縮小する（`image = ImagePreprocessor.Resize(image, 2000, 0)`）。 |

## 完全動作例

以下は新しいコンソール アプリにコピー＆ペーストできる完全なプログラムです。上記で説明したすべてのヘルパーメソッドが含まれています。

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**実行** (` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}