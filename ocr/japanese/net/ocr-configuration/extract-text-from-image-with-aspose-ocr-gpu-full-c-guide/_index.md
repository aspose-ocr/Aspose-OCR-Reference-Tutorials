---
category: general
date: 2026-04-06
description: C#でAspose OCR GPUを使用して画像からテキストを抽出します。このステップバイステップガイドで、ファイルから画像を読み込む方法とGPUメモリ制限の設定方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: ja
og_description: C#でAspose OCR GPUを使用して画像からテキストを抽出します。このステップバイステップガイドで、ファイルから画像を読み込む方法とGPUメモリ制限の設定方法を学びましょう。
og_title: Aspose OCR GPUで画像からテキストを抽出 – 完全C#ガイド
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Aspose OCR GPUで画像からテキストを抽出する – 完全C#ガイド
url: /ja/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU を使用した画像からのテキスト抽出 – 完全 C# ガイド

画像からテキストを**抽出**したいと思ったことはありますか、しかしパフォーマンスが重要になる段階で行き詰まったことはありませんか？ あなたは一人ではありません—多くの開発者が OCR がボトルネックになると同じ壁にぶつかります。このチュートリアルでは、Aspose OCR の GPU ランタイムを使用して画像からテキストを抽出する方法、ファイルから画像をロードする方法、さらにはリソース管理を厳密にするために GPU メモリ上限を設定する方法を正確に示します。

完全に実行可能な C# のサンプルを順に解説し、各行が重要な理由を説明し、遭遇しやすい落とし穴を指摘します。最後まで読めば、GPU 上で動作する高速でスケーラブルな OCR パイプラインを構築するための確固たる基礎が身につきます。

## このガイドでカバーする内容

- **Prerequisites**: .NET 6+ (or .NET Framework 4.6+), Aspose.OCR NuGet package, a compatible GPU driver.
- **Step‑by‑step code** that loads an image from file, configures the Aspose OCR GPU engine, and extracts text.
- **Why** you might want to set a GPU memory limit and how to do it safely.
- **Edge‑case handling**: low‑resolution images, missing GPU, and troubleshooting confidence scores.
- **Next steps**: batch processing, integrating with ASP.NET Core, and switching back to CPU if needed.

> **Pro tip:** GPU が使用されているか不安な場合は、OCR 実行中に GPU アクティビティモニタ（例: NVIDIA‑SMI）を確認してください。設定した上限に合わせたメモリ使用量のスパイクが見えるはずです。

![Aspose OCR GPU エンジンを使用した画像からテキスト抽出のフローを示す図](extract-text-from-image-aspose-ocr-gpu.png "Aspose OCR GPU を使用した画像からテキスト抽出")

## ステップ 1: GPU 処理用に Aspose OCR エンジンを初期化する

最初に必要なのは、GPU で実行すべきことを認識した `OcrEngine` インスタンスです。Aspose はランタイムを指定できるシンプルな `OcrEngineSettings` オブジェクトを提供しています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Why this matters:** デフォルトでは Aspose OCR は CPU にフォールバックしますが、これは小さな画像には問題なくても高解像度の写真では非常に遅くなります。`Runtime = OcrRuntime.Gpu` を明示的に設定することで、重い処理をグラフィックカードにオフロードし、目に見える速度向上が得られます。

## ステップ 2: (オプション) GPU メモリ上限を設定する

共有ワークステーションやリソースが限られたコンテナで実行する場合、OCR エンジンが消費するメモリ量を上限設定できます。これによりメモリ不足によるクラッシュを防ぎ、他のプロセスとの競合を回避できます。

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**When to use it:**  
- **Multi‑tenant environments** where several services share the same GPU.  
- **CI/CD pipelines** that allocate a fixed amount of GPU memory per job.  

この行を省略すると、Aspose は必要なだけメモリを使用しますが、専用ワークステーションであれば問題ありません。

## ステップ 3: ファイルから画像をロードする

次に画像をメモリに取り込みます。Aspose OCR は `System.Drawing.Image` と連携するため、`Image.FromFile` を使用します。パスが実在するファイルを指していることを確認してください。存在しない場合は例外がスローされます。

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Why loading from file matters:** 多くの開発者がバイト配列を直接渡そうとしますが、余計な変換ステップが発生します。`Image.FromFile` を使うのがシンプルで、`using` 文によりファイルハンドルが速やかに解放されます。

## ステップ 4: OCR を実行して結果を取得する

エンジンの設定と画像のロードが完了したら、いよいよテキストを抽出します。`Recognize` メソッドは、生テキストと信頼度スコアの両方を含む `OcrResult` を返します。

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Understanding the output:**  
- `Confidence` は 0 から 1 の範囲の値です。0.95（95 %）の信頼度は通常、OCR が正確であることを意味します。  
- `Text` には画像内の改行がそのまま保持されており、後続の処理に便利です。

## ステップ 5: 出力を検証しエッジケースを処理する

### 信頼度レベルの確認

信頼度が例えば 80 % 以下に下がった場合、CPU 処理にフォールバックするか、画像前処理（例: 二値化）を適用したいでしょう。

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### GPU が見つからない場合の対処

すべてのマシンに互換性のある GPU があるわけではありません。GPU ランタイムの初期化に失敗すると、Aspose は `OcrException` をスローします。

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### 高解像度画像

非常に大きな画像（例: 幅 4000 px 超）は大量の GPU メモリを消費します。事前に設定した上限に達した場合、Aspose は処理を途中で切り捨てます。そのような場合は、まず画像を縮小してください。

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## 完全な動作例

以下は新しいコンソールプロジェクトにコピー＆ペーストできる完全なプログラムです。すべての手順、エラーハンドリング、オプションのフォールバックロジックが含まれています。

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### 期待される出力

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

信頼度が閾値を下回った場合、追加の CPU フォールバックメッセージが表示されます。

---

## 結論

これで **画像からテキストを抽出する方法**、**ファイルから画像をロードする方法**、そして本番環境で **GPU メモリ上限を設定する理由** が理解できました。上記のサンプルは完全に機能し、任意の .NET プロジェクトに組み込める引用に値するソリューションです。

次は何をすべきか？以下を検討してください：

- **Batch processing**: 画像フォルダーをループし、結果を CSV に書き出す。  
- **ASP.NET Core integration**: アップロードされた画像を受け取り OCR テキストを返す API エンドポイントを公開する。  
- **Performance tuning**: 異なる `GpuMemoryLimit` 値を試し、最適な GPU 使用率をモニタリングする。

コードはシナリオに合わせて自由に適応してください—ドキュメントデジタル化パイプライン、リアルタイム翻訳アプリ、レシートスキャンサービスなど、どんな用途でも基本は同じです：GPU エンジンを初期化し、メモリを賢く管理し、常に信頼度を検証すること。

質問や問題があれば下のコメント欄に書き込んでください。一緒にトラブルシューティングしましょう。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}