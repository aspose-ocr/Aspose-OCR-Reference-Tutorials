---
category: general
date: 2026-03-21
description: C# OCRチュートリアル：画像からテキストを抽出し、請求書をスキャンし、GPUアクセラレーション対応のAspose OCRを使用してC#で画像を読み込む方法を学ぶ。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: ja
og_description: C# OCRチュートリアル：画像からテキストを抽出し、OCR請求書スキャンを実行し、GPUアクセラレーションを使用してC#で画像をOCRする方法をステップバイステップで解説
og_title: c# OCRチュートリアル – Aspose OCRで画像からテキストを抽出
tags:
- OCR
- C#
- Image Processing
title: C# OCRチュートリアル – Aspose OCRで画像からテキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – Aspose OCR を使用した画像からテキストを抽出する

スキャンした請求書を編集可能なテキストに変換するような実際の問題を **c# OCR tutorial** スタイルで解決する方法を考えたことがありますか？ あなたは一人ではありません。多くの開発者が *extract text from image* ファイルが必要になると壁にぶつかり、最初のノイズの多いスキャンで壊れる脆弱なパーサーを書いてしまいます。

実は、Aspose.OCR を使えば全工程がとても簡単になります。特に GPU アクセラレーションを有効にすると効果的です。このガイドでは、C# で **how to ocr image** ファイルを正しく処理し、c# で画像を正しくロードする方法、さらに一般的な請求書スキャンの問題点を髪を引っ張ることなく対処する方法を正確に示します。

このチュートリアルの最後までに、TIFF 請求書を読み取り、GPU で OCR を実行し、クリーンなプレーンテキスト出力を表示する実行可能なコンソールアプリが手に入ります。魔法ではなく、コピー＆ペーストして適応できる堅実なコードです。

---

## 必要なもの

- **.NET 6.0** (またはそれ以降) – 現在の LTS バージョンで、将来にも対応できます。
- **Aspose.OCR for .NET** NuGet パッケージ – バージョン 23.10（執筆時点での最新）。
- **GPU‑enabled machine**（オプションですが推奨） – 互換性のある GPU が見つからない場合、コードは CPU にフォールバックします。
- 例として `large_invoice.tif` などの画像。PNG、JPEG、TIFF、PDF など、サポートされている形式であれば何でも構いません。

まだ NuGet パッケージをインストールしていない場合は、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

前提条件はこれで揃ったので、実際の手順に入りましょう。

---

## 手順 1: 新しいコンソールプロジェクトを作成し、Aspose.OCR を追加する

まず、チュートリアルを自己完結させるために新しいコンソールアプリを作成します。

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** `-n` フラグを使用してプロジェクトに意味のある名前を付けましょう。後でモジュールを追加する際にソリューションが整理された状態を保てます。

Visual Studio が作成する `Program.cs` ファイルが作業領域になります。これを開き、デフォルトの `Console.WriteLine` 行を削除してください。OCR ロジックに置き換えます。

---

## 手順 2: C# で画像をロードする – 正しい方法

画像のロードは簡単に見えるかもしれませんが、誤った方法で行うとメモリリークやファイルロックの原因になります。`System.Drawing.Image` クラスは多くのシナリオで問題なく動作しますが、必ず `using` ブロックでラップして確実に破棄してください。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

コメント `// 👉 Step 2:` に注目してください。これはチュートリアルのステップ番号と一致しており、後でコードを読む人の助けになります。

---

## 手順 3: GPU アクセラレーションで OCR エンジンを初期化する

Aspose.OCR はコンストラクタで処理モードを選択できます。`OcrEngineMode.Gpu` は GPU が検出された場合にグラフィックカードを使用し、検出されない場合は自動的に CPU にフォールバックします。そのため、追加のフォールバックロジックを書く必要はありません。

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **Why GPU?**  
> 高解像度の請求書に対する OCR は CPU に負荷がかかります。GPU にオフロードすることで、実行時間が数秒からほんの一部に短縮され、特にバッチ処理時に効果的です。

---

## 手順 4: OCR を実行し、画像からテキストを抽出する

いよいよ魔法の時間です。`Recognize` を呼び出してプレーンテキストを取得します。Aspose は `OcrResult` オブジェクトを返し、そこには生テキスト、信頼度スコア、必要に応じて文字ごとのバウンディングボックスが含まれます。

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、以下のような出力が表示されるはずです：

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

出力が文字化けしている場合は、画像が高コントラストであること、OCR の言語設定が正しく（デフォルトは英語）なっていることを再確認してください。`ocrEngine.Settings` を調整すれば精度を向上させることもできますが、デフォルト設定でもほとんどの印刷された請求書には十分です。

---

## 手順 5: OCR 請求書スキャンのエッジケースを処理する

請求書は様々な形態があります。マルチページのものや、テーブルや手書きのメモが含まれるものがあります。パイプライン全体を書き直すことなく、すぐに適用できる調整をいくつか紹介します。

### 5.1 マルチページ PDF または TIFF

ソースファイルに複数ページが含まれる場合、各ページをループして結果を結合する必要があります。

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 低解像度スキャン

DPI が 150 未満の場合、エンジンに渡す前に画像を拡大してください。これにより文字認識が大幅に向上します。

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 カスタム言語パック

デフォルトでは Aspose は英語を使用します。他の言語を使用する場合は、Aspose のサイトから該当する言語パックをダウンロードし、登録してください：

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

これらの調整により、**ocr invoice scanning** ソリューションは本番環境でも十分に堅牢になります。

---

## 完全な動作例

以下は、上記のすべての手順を組み込んだ完全な実行可能プログラムです。`Program.cs` にコピーし、ファイルパスを調整して **F5** を押してください。

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**期待される出力**（簡略化）:

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

プログラムを実行し、コンソールに請求書に表示されているテキストが出力されることを確認してください。空文字列が出力された場合は、画像パスが正しいか、ファイルが破損していないかを再確認してください。

---

## よくある質問 (FAQ)

**Q: Does this work on Linux?**  
A: はい。Aspose.OCR はクロスプラットフォームです。Linux 用の .NET ランタイムをインストールすれば、同じ NuGet パッケージが動作します。GPU アクセラレーションを使用するには CUDA 対応 GPU と適切なドライバーが必要です。

**Q: What if I don’t have a GPU?**  
A: `OcrEngineMode.Gpu` コンストラクタは、互換性のある GPU が検出されない場合に自動的に CPU にフォールバックします。結果は依然として正確ですが、処理にやや時間がかかります。

**Q: Can I OCR handwritten notes?**  
A: Aspose のデフォルトモデルは印刷テキストに焦点を当てています。手書き文字を認識するには、専用のモデルや別のサービス（例: Azure Form Recognizer）が必要です。ただし、同じコードで試すことは可能ですが、信頼度スコアが低くなることを想定してください。

---

## 結論

あなたは **c# OCR tutorial** を完了し、*extract text from image* ファイルの抽出方法、**ocr invoice scanning** の実行方法、そして **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}