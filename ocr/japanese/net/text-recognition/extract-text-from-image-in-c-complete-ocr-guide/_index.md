---
category: general
date: 2026-04-11
description: C#でAspose OCRを使用して画像からテキストを抽出します。OCR用に画像をロードする方法と、GPUサポート付きでTIFFファイルからテキストを認識する方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize text from TIFF
- Aspose OCR C#
- GPU OCR processing
- high‑resolution OCR
language: ja
og_description: C# で Aspose OCR を使用して画像からテキストを抽出する。このチュートリアルでは、OCR 用に画像をロードし、GPU 加速を利用して
  TIFF からテキストを認識する方法を示します。
og_title: C#で画像からテキストを抽出する – 完全OCRガイド
tags:
- OCR
- C#
- Aspose
- GPU
title: C#で画像からテキストを抽出する – 完全OCRガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像からテキストを抽出 – 完全OCRガイド

画像から**テキストを抽出**したいことはありますが、巨大なTIFFを処理できるライブラリが分からずに困ったことはありませんか？ あなたは一人ではありません。実務のプロジェクト、たとえば請求書のデジタル化やスキャンした書籍のアーカイブなどでは、OCR 用に画像を読み込み、TIFF からテキストを認識できるかどうかが、成功を左右する重要な機能となります。

このガイドでは、Aspose OCR for .NET を使用した実践的な解決策をステップバイステップで解説します。最終的に、高解像度スキャンを読み込み、GPU 加速処理（フォールバックも自動）を実行し、プレーンテキストを出力する C# コンソール アプリが完成します。抜け落ちた部分や「ドキュメント参照」だけの行き止まりはありません。

## 必要な環境

- **.NET 6 以降**（任意の最新 SDK でコンパイル可能）
- **Aspose.OCR for .NET** NuGet パッケージ  
  `dotnet add package Aspose.OCR`
- OCR したい **大容量 TIFF** またはその他の画像形式  
  （例では `large_scan.tif` を使用）
- （任意）CUDA 11+ に対応した GPU – なしの場合は自動で CPU モードに切り替わります。

以上です。さっそく始めましょう。

![Extract text from image using Aspose OCR in C#](image-placeholder.png "Extract text from image using Aspose OCR in C#")

## Step 1: Extract Text from Image – Initialise the OCR Engine

画像を処理する前に、`OcrEngine` インスタンスを作成する必要があります。エンジンは認識の動作を制御するすべての設定を保持します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine and request GPU processing.
        // ProcessingMode.Auto tells Aspose to fall back to CPU if a GPU isn’t detected.
        var ocrEngine = new OcrEngine
        {
            Settings = { ProcessingMode = ProcessingMode.Gpu }
        };

        // Optional: cap GPU memory usage to avoid OOM on shared machines.
        ocrEngine.Settings.GpuMemoryLimit = 1024; // MB
```

**ポイント:**  
`ProcessingMode.Gpu` を使用すると、最新の GPU で認識時間を数秒短縮できますが、`ProcessingMode.Auto`（またはデフォルト）にしておくと、GPU が無い環境でも安全です。`GpuMemoryLimit` の設定は実用的なヒントで、これがないと巨大画像が VRAM を独占し、他のアプリがクラッシュする可能性があります。

## Step 2: Load Image for OCR – Bring the TIFF Into Memory

エンジンの準備ができたら、解析したい画像を供給します。Aspose の `ImageStream.FromFile` はフォーマット処理を抽象化してくれます。

```csharp
        // Load the high‑resolution TIFF you want to OCR.
        // Replace the path with the location of your own file.
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/large_scan.tif");
```

**内部で何が起きているか:**  
`ImageStream.FromFile` はファイルをストリームに読み込み、画像形式（TIFF、PNG、JPEG など）を自動検出します。マルチページ TIFF を扱う場合、Aspose は各ページを別々のフレームとして扱い、必要に応じて後でイテレートできます。

## Step 3: Recognize Text from TIFF – Run the OCR Engine

画像がロードされたら、いよいよ本格的な処理が始まります。`Recognize` メソッドは抽出されたテキストといくつかの便利なメタデータを含む `OcrResult` オブジェクトを返します。

```csharp
        // Perform the OCR operation.
        var ocrResult = ocrEngine.Recognize(image);
```

**なぜ `Recognize` を一度だけ呼ぶのか:**  
エンジンは最初の実行後に内部構造をキャッシュするため、ほとんどのシナリオでは一回の呼び出しで十分です。多数のページを処理する場合は同じ `OcrEngine` インスタンスを再利用すると、GPU コンテキストの再初期化オーバーヘッドを回避できます。

## Step 4: Display the Result – Show the Extracted Text

最後に、認識結果の文字列をコンソールに出力します。実際のアプリケーションでは、データベースやファイルに書き込むことが多いでしょう。

```csharp
        // Show the extracted plain text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力例:**  
`large_scan.tif` が印刷された請求書の場合、次のようなテキストが表示されます。

```
Invoice #12345
Date: 2024‑03‑15
Total: $1,234.56
...
```

レイアウトは元画像に依存しますが、重要なのは **画像からテキストを抽出** した結果が得られ、以降の処理に利用できるようになったことです。

## Step 5: Troubleshooting & Edge Cases

### GPU が検出されない場合

GPU が無いマシンでサンプルを実行すると、`ProcessingMode.Auto` を使用した場合にエンジンは自動的に CPU にフォールバックします。CPU モードを明示的に指定したい場合は、先ほどの行を次のように置き換えてください。

```csharp
ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
```

### メモリを大量に消費する TIFF

非常に大きなスキャン（例: 10 000 × 10 000 px）では、設定した 1 GB の GPU 上限を超えることがあります。その場合は `GpuMemoryLimit` を増やす（余裕があれば）か、エンジンに渡す前に画像を縮小してください。

```csharp
var resized = image.Resize(4000, 4000); // keep aspect ratio as needed
var ocrResult = ocrEngine.Recognize(resized);
```

### マルチページ ドキュメント

TIFF に複数ページが含まれる場合は、以下のようにループ処理します。

```csharp
for (int i = 0; i < image.PageCount; i++)
{
    var pageStream = image.GetPage(i);
    var result = ocrEngine.Recognize(pageStream);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

### 言語・フォントのサポート

Aspose OCR はラテン系スクリプトを自動検出しますが、キリル文字、アラビア文字、またはカスタムフォントを扱う場合は言語パックを追加する必要があります。

```csharp
ocrEngine.Settings.Language = Language.Russian; // example
```

## Pro Tips & Best Practices

- **エンジンを再利用**: 画像ごとに新しい `OcrEngine` を作成すると、目に見える遅延が発生します。
- **バッチ処理**: 数十枚の TIFF を処理する際はキューに入れ、並列スレッドで実行します。ただし GPU メモリの競合に注意してください。
- **出力の検証**: OCR は完璧ではありません。`ocrResult.Text` に対して簡易スペルチェックや正規表現でのバリデーションを行い、明らかな誤認識を検出しましょう。
- **パフォーマンスの記録**: `Stopwatch` で `Recognize` 前後の経過時間を測定し、環境において GPU 加速が導入コストに見合うか判断します。

## Conclusion

これで、Aspose OCR を使用して C# で **画像からテキストを抽出** する完全なエンドツーエンドのサンプルが完成しました。画像を OCR 用に読み込み、TIFF からテキストを認識し、GPU と CPU のシナリオを適切にハンドリングする方法を学び、請求書、パスポート、スキャン文書などあらゆる用途に応用できる基盤が手に入りました。

次のステップは？ TIFF をマルチページ PDF に置き換えてみる、カスタム言語パックで精度を上げる、あるいは出力を自然言語処理パイプラインに流し込んで自動データ抽出を実装する、などです。可能性は無限です—楽しいコーディングを！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}