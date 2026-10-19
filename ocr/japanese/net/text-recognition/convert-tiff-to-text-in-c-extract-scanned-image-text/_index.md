---
category: general
date: 2026-03-05
description: Aspose OCR を使用して C# で TIFF をテキストに変換—スキャンした画像ファイルからテキストを迅速に抽出し、OCR 処理のために
  C# で画像ファイルをロードする方法を学びましょう。
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: ja
og_description: C#でAspose OCRを使用してTIFFをテキストに変換。スキャン画像からテキストを抽出し、画像ファイルを効率的に読み込むフルワークフローを学びましょう。
og_title: C#でTIFFをテキストに変換 – スキャン画像のテキスト抽出
tags:
- OCR
- C#
- Aspose
title: C#でTIFFをテキストに変換 – スキャン画像のテキスト抽出
url: /ja/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で TIFF をテキストに変換 – スキャン画像のテキスト抽出

C# で **TIFF をテキストに変換**したいですか？検索可能な文字列に変換できないマルチページのスキャン画像と格闘しているのはあなただけではありません。  
このガイドでは、TIFF ファイルを取得し Aspose OCR に渡してプレーンテキストを出力する、完全で実行可能なソリューションをステップバイステップで解説します—追加のサービスや隠されたマジックは不要です。

> **プロのコツ:** 高解像度のスキャンを扱う場合、GPU 処理を有効にすると各ページの処理時間を数秒短縮できます。

また、**スキャン画像からテキストを抽出**する方法と、OCR エンジンに **C# で画像ファイルをロード**する最適な方法も紹介しますので、このロジックを任意の .NET プロジェクトにすぐ組み込むことができます。

---

## 必要なもの

本題に入る前に、以下のものが環境に揃っていることを確認してください：

| 要件 | 理由 |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | 最新のランタイムで、`Span<T>` と非同期 I/O をサポートします |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | 使用する OCR エンジンです |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | これがないと評価版の制限に達してしまいます |
| A TIFF file (single‑ or multi‑page) to test | 使用例: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | `EngineMode = Gpu` の場合、認識が高速化します |

これらが揃っていない場合は、今すぐ NuGet パッケージを取得してください：

```bash
dotnet add package Aspose.OCR
```

---

## ステップ 1: プロジェクトのセットアップと名前空間のインポート

新しいコンソール アプリを作成する（または既存プロジェクトにコードを追加）します。最初に行うのは、必要なクラスのインポートです。

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **重要な理由:** `Aspose.OCR.Image` をインポートすると `ImageStream` ファクトリが利用でき、ディスクやストリームから直接 TIFF ファイルを読み取れます。このステップを省略するとコンパイル時エラーが発生します。

---

## ステップ 2: OCR エンジンの初期化と処理モードの選択

OCR エンジンは画像を割り当てる **前に** 設定する必要があります。ここで CPU で実行するか GPU を利用するかを決めます。

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*グラフィックカードのないヘッドレスサーバーの場合は、`Gpu` を `Cpu` または `Auto` に変更してください。*  
エンジンモードはメモリ割り当てと速度に影響します。GPU モードは大きく高解像度の TIFF で 2〜3 倍速くなることがあります。

---

## ステップ 3: Aspose OCR ライセンスの適用

ライセンスなしで実行すると、数ページに制限されウォーターマークが付加されます。ライセンスは早めにロードして、以降の操作を制限なしにしましょう。

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **よくある落とし穴:** `SetLicense` を `Recognize()` の後に配置すると、その呼び出しはトライアルモードにフォールバックします。

---

## ステップ 4: TIFF ファイルのロード – シングルページとマルチページ画像の処理

Aspose OCR はマルチページ TIFF をそのまま読み取れますが、正しいストリームを渡す必要があります。以下は両方のシナリオで機能する堅牢なパターンです。

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### `ImageStream.FromFile` を使用する理由

- 内部で `FileStream` を抽象化し、TIFF のページ列挙を自動で処理します。  
- `MemoryStream` でも動作するため、ファイルシステムに触れずデータベースや Web API から画像をロードできます。

### エッジケース: 非常に大きな TIFF

TIFF が 200 MB を超える場合は、メモリ不足例外を回避するためにページ単位でロードすることを検討してください：

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## ステップ 5: 出力の検証

プログラムを実行すると、以下のような出力が表示されます：

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

テキストが乱れている場合は、以下を再確認してください：

1. 解像度 – OCR は 300 dpi 以上で最適に動作します。  
2. EngineMode – GPU ドライバが古い場合は `Cpu` に切り替えてください。  
3. ライセンス – ライセンスファイルのパスが正しく、ファイルが読み取り可能であることを確認してください。

---

## よくある質問 (FAQ)

### 他の画像形式でも動作しますか？

もちろんです。`ImageStream.FromFile` は JPEG、PNG、BMP、さらには PDF（Aspose.PDF 経由）もサポートしています。拡張子を置き換えるだけです。

### データベースに保存された画像を処理したい場合は？

BLOB を `MemoryStream` に読み込み、`ImageStream.FromStream(memoryStream)` に渡します。OCR エンジンはファイルベースのストリームと同様に扱います。

### Linux でも実行できますか？

はい。Aspose OCR はクロスプラットフォームです。適切な .NET ランタイムをインストールし、GPU を使用する場合は必要なネイティブライブラリが利用可能であることを確認してください。

---

## 完全動作例（コピー＆ペースト可能）

以下はコンパイル可能な完全なプログラムです。`YOUR_DIRECTORY` とライセンスファイルのパスを実際の場所に置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行してテキストを確認してください

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}