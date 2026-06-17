---
category: general
date: 2026-05-31
description: Aspose OCR を使用して C# で画像からテキストを認識する方法を学びます。tiff ファイルからテキストを抽出する方法や、OCR
  用に画像を効率的に読み込む方法も含まれます。
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: ja
og_description: Aspose OCR を使用して画像からテキストを認識するためのステップバイステップガイド。TIFF からの抽出と OCR 用の適切な画像読み込みをカバーしています。
og_title: Aspose OCR を使用して C# で画像からテキストを認識する
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: C#でAspose OCRを使用して画像からテキストを認識する
url: /ja/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使用して画像からテキストを認識する

画像からテキストを **recognize text from image** したいことはありますか？でも C# でどこから始めればいいか分からない…という開発者は多いです。スキャンした文書やマルチページ TIFF を扱うときに壁にぶつかることがよくあります。このガイドでは、Aspose OCR ライブラリを使って **recognize text from image** する完全な実行可能サンプルをステップバイステップで解説し、さらに **extract text from tiff** の方法や **load image for OCR** のベストプラクティスも紹介します。

NuGet パッケージのインストールから GPU 加速の設定、必要に応じた CPU フォールバックまで網羅します。チュートリアルの最後には、認識したテキストと処理時間をコンソールに出力するアプリが完成します—抜け落ちた部分や曖昧な記述は一切ありません。

## What You’ll Build

- .NET コンソール アプリケーション（マルチページ TIFF も含む画像をロード）  
- GPU 使用を設定した OCR エンジン（必要に応じて CPU にフォールバック）  
- 画像から抽出したプレーンテキストをコンソールに出力  
- GPU と CPU の性能差を確認できる処理時間の計測情報  

**Prerequisites**

- .NET 6 SDK 以降（コードは .NET Core と .NET Framework でも動作）  
- C# とコマンドラインの基本的な知識  
- Aspose.OCR NuGet パッケージを取得できるインターネット接続  

これらが揃っていれば、さっそく始めましょう。

![Aspose OCR を使用して画像からテキストを認識する C# コード](image.png "Aspose OCR を使用して画像からテキストを認識する C# コード")

## Step 1 – Recognize text from image: Set up the OCR engine

まず最初に `OcrEngine` インスタンスを作成します。Aspose OCR は処理デバイスを選択でき、速度重視なら GPU、保守的にしたい場合は CPU を使用します。また、エンジンはメモリ上限のヒントも受け取れるので、共有マシンで便利です。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Why this matters:**  
`OcrDevice.Gpu` を選択すると、大きな画像やマルチページ TIFF の認識時間が数秒短縮されます。`GpuMemoryLimit` は、共有ワークステーションで GPU メモリを使いすぎないようにするための設定です。

## Step 2 – Load image for OCR (including TIFF support)

次にエンジンに画像を渡します。Aspose の `ImageStream.FromFile` はライブラリがサポートする **any** 形式（TIFF、PNG、JPEG など）を受け取れます。このステップが **load image for OCR** の要件に直接対応します。

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Pro tip:** マルチページ TIFF を扱う場合、Aspose は自動的に各ページを別々のフレームとして扱い、エンジンは順次処理します。追加コードは不要です。

## Step 3 – Run the recognition and **extract text from tiff**

エンジンの準備と画像のロードが完了したら、OCR 処理を開始します。`Recognize` メソッドは `OcrResult` を返し、プレーンテキスト、信頼度スコア、処理時間などが含まれます。

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Edge case handling:**  
GPU が利用できない環境でも `engine.Recognize()` は動作します。エンジンは自動的に CPU に切り替えるためです。実際に使用されたデバイスを記録したい場合は、認識後に `engine.Device` を確認してください。

## Step 4 – Retrieve the recognized plain text

テキストの取得はシンプルです。`Text` プロパティを読むだけで、**extract text from tiff**（または他の画像）した結果が得られます。

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

ソース画像に現れる改行がそのまま保持された文字列が出力されます。JSON や CSV など構造化された出力が必要な場合は、`result.Regions` や `result.Lines` を調べれば対応可能ですが、クイックスクリプトではプレーンテキストで十分です。

## Step 5 – Measure processing time and handle GPU fallback

大量のページを処理する際はパフォーマンスが重要です。`ProcessingTime` プロパティは、GPU で実行したか CPU で実行したかに関わらず、OCR に要した正確な時間を教えてくれます。

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Why you should care:**  
処理時間が急激に伸びた場合は `GpuMemoryLimit` を調整するか、明示的に CPU に切り替えてみてください（`Device = OcrDevice.Cpu`）。逆に大きな TIFF でサブ秒の結果が出れば、GPU 加速がうまく機能している証拠です。

## Full, Ready‑to‑Run Example

以下のコードを新しいコンソール プロジェクト（`dotnet new console -n OcrDemo`）に貼り付け、`dotnet add package Aspose.OCR` でパッケージを追加します。その後、`YOUR_DIRECTORY/sample_multi_page.tif` を実際の画像パスに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Expected output (truncated for brevity):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

GPU が搭載されていないマシンでは、処理時間が数秒長くなることがありますが、テキスト抽出自体は正しく行われます。

## Common Questions & Gotchas

- **画像が巨大（10 MB 超）だったら？**  
  エンジンに渡す前に解像度を下げるか、VRAM が十分にある場合は `GpuMemoryLimit` を増やしてください。  
- **複数画像をループで処理したい**  
  もちろん可能です。同じ `OcrEngine` インスタンスを再利用し、各イテレーションで新しい `ImageStream` を割り当てれば OK です。  
- **リソースの解放は必要？**  
  `OcrEngine` は `IDisposable` を実装しています。GPU リソースのクリーンアップを確実に行うため、`using` ブロックで囲むことを推奨します。  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **英語以外の言語は？**  
  `engine.Language = OcrLanguage.Spanish`（またはサポートされている任意の言語）を `Recognize()` 呼び出し前に設定すれば対応できます。  

## Conclusion

これで、Aspose OCR を使って C# で **recognize text from image** する完全なエンドツーエンド ソリューションが手に入りました。チュートリアルでは **load image for OCR**、**extract text from tiff**、GPU フォールバックを考慮したパフォーマンス測定の方法を網羅しました。

ここからは次のようなことに挑戦できます：

- さまざまな画像形式（BMP、PDF など）で Aspose の挙動を確認する  
- レイアウト情報が必要な場合は `result.Regions` のバウンディングボックスデータを活用する  

## What Should You Learn Next?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}