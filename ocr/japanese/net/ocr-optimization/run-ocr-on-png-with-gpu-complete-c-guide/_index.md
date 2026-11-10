---
category: general
date: 2026-01-02
description: Aspose OCR と GPU サポートを使用して PNG の OCR を高速に実行します。画像からテキストを認識し、画像からテキストを抽出し、GPU
  メモリ上限を設定する方法を学びましょう。
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: ja
og_description: Aspose OCR と GPU 加速を活用して、PNG の OCR を効率的に実行します。このチュートリアルでは、画像からテキストを認識し、テキストを抽出し、GPU
  メモリ使用量を制御する方法を示します。
og_title: GPUでPNGのOCRを実行する – 完全C#ガイド
tags:
- OCR
- C#
- GPU
title: GPUでPNGのOCRを実行する – 完全C#ガイド
url: /ja/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPUでPNGのOCRを実行 – 完全C#ガイド

高解像度の **PNG** ファイルで OCR を実行したいけれど、パフォーマンスがボトルネックになっていると感じたことはありませんか？ あなただけではありません。実際のパイプラインでは、1枚の高解像度 PNG が CPU のみの OCR エンジンを圧迫し、瞬時に終わるはずの処理が数分待ちになることがあります。  

良いニュースは、Aspose OCR が GPU 拡張機能を提供しており、**画像からテキストを認識** する処理を格段に高速化できることです。このチュートリアルでは、C# で **PNG の OCR を実行** する具体的なハンズオン例を通じて、**画像からテキストを抽出** する方法や、**GPU メモリ上限を設定** してハードウェア予算内に収める方法まで解説します。

各ステップの「やり方」だけでなく「なぜそうするのか」も説明するので、単なるコピペスニペットに留まらない、しっかりとしたメンタルモデルを身につけられます。

## 学べること

- Aspose OCR の GPU サポートを利用するための前提条件。  
- PNG を `Bitmap` に読み込み、OCR エンジンに渡す方法。  
- 最適なパフォーマンスを得るための `GpuDevice` と `GpuMemoryLimitMb` の設定方法。  
- **画像からテキストを認識** し、プレーンテキスト結果を取得する手順。  
- メモリが少ない GPU やマルチページ PNG など、一般的なエッジケースへの対処法。  

このガイドを終える頃には、**PNG の OCR を GPU 速度で実行** でき、OCR ジョブのメモリフットプリントを自信を持ってコントロールできるようになります。

![GPU 加速で PNG の OCR を実行する図](run-ocr-on-png-diagram.png "GPU 加速で PNG の OCR 実行例")

## 前提条件

作業を始める前に、以下を用意してください。

1. .NET 6.0 以上（コードは .NET Core と .NET Framework でも動作します）。  
2. CUDA 対応の NVIDIA GPU（例ではデバイスインデックス 0 を使用）。  
3. Aspose.OCR NuGet パッケージとその GPU 拡張 (`Aspose.OCR.Extensions`)。  
4. プロジェクトから参照できるフォルダーに配置したサンプル PNG（`input.png`）。  

これらに心当たりがない場合でも心配はいりません。該当箇所で代替手段を示します。

---

## 手順 1 – Aspose OCR と GPU 拡張をインストール

まずはライブラリを揃えましょう。必要なライブラリが無いとコードはコンパイルできません。

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` パッケージは GPU 加速に必要なネイティブ CUDA バイナリを自動で取得します。  
*プロ tip:* GPU が無いマシンでもプロジェクトはビルド可能です。その場合は後述の `PreferGpu = false` を設定してください。

---

## 手順 2 – 処理対象の PNG を読み込む

ここで **PNG の OCR を実行** するために、画像を `Bitmap` にロードします。`Bitmap` はファイルパスを受け取るので、実行ファイルからの相対パスが正しいことを確認してください。

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

PNG が非常に大きい（例: 片側が 5000 px 超）場合は、GPU メモリの枯渇を防ぐために先に縮小すると良いでしょう。後述の **GPU メモリ上限を設定** オプションが役立ちます。

---

## 手順 3 – GPU 使用のために OCR エンジンを作成・設定

本チュートリアルの核心です。GPU を利用して **画像からテキストを認識** するためのエンジン設定を行います。重要なプロパティは次の 2 つです。

- `GpuDevice` – 使用する CUDA デバイスを指定。  
- `GpuMemoryLimitMb` – エンジンが確保できる GPU メモリ上限を設定。

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**メモリ上限を設定する理由**: 一部の GPU はディスプレイとメモリを共有したり、同時に複数のワークロードを走らせたりします。上限を設けることで、特に多数の PNG を並列処理する際のメモリ不足クラッシュを防げます。

---

## 手順 4 – 認識オプションを定義（言語と GPU 優先度）

`RecognitionOptions` オブジェクトで、エンジンに対して対象言語と **GPU を優先** するかどうかを指示します。英語文書が多い場合はこの設定で十分ですが、必要に応じて `Language.English` を他のロケールに置き換えてください。

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

英語以外の言語で **画像からテキストを抽出** したい場合は、`Language` 列挙体を変更するだけです。ライブラリは多数の言語を標準でサポートしています。

---

## 手順 5 – OCR を実行し結果を取得

すべての設定が完了したら、実際に **PNG の OCR を実行** してリッチな結果オブジェクトを取得します。

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` にはプレーンテキスト (`ocrResult.Text`) の他、信頼度スコア、バウンディングボックス、ハイライトされた元画像などが含まれます。デバッグや可視化が必要なときに便利です。

**期待される出力例**（サンプル PNG に「Hello World」と書かれている場合）:

```
=== OCR Output ===
Hello World
```

文字化けが発生したら、PNG が破損していないか、GPU メモリ上限が画像サイズに対して低すぎないかを確認してください。

---

## 手順 6 – エッジケースとベストプラクティス

### メモリが少ない GPU

`CudaException: out of memory` のような例外が出たら、`GpuMemoryLimitMb` を下げるか、処理前に PNG をタイルに分割します。タイル分割は `Graphics.DrawImage` と `Bitmap` のクローンで実装可能です。

### バッチで複数 PNG を処理

フォルダー内の PNG をまとめて処理する場合は、同じ `OcrEngine` インスタンスを再利用しましょう。1 回だけ初期化すれば GPU コンテキストの切り替え回数が減り、パフォーマンスが向上します。

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### CPU へのフォールバック

GPU が利用できない環境では、単に `PreferGpu = false` を設定すれば自動的に CPU にフォールバックします。コードの変更は不要です。

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## 完全動作サンプル

以下は新規コンソールプロジェクトにコピペできる、全手順を網羅したサンプルプログラムです。安全チェックもいくつか入れています。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すれば、抽出されたテキストがコンソールに表示されます。

---

## まとめ

本稿では、Aspose OCR の GPU 拡張を使って **PNG の OCR を実行** し、**画像からテキストを認識**、さらに **GPU メモリ上限を設定** しながら安全に処理する方法を実演しました。`GpuDevice` と `GpuMemoryLimitMb` を適切に構成すれば、低スペックの GPU でも高速かつ安定した OCR アプリケーションが構築できます。

次のステップとしては:

- 他言語 (`Language.French`, `Language.Spanish` など) を試す。  
- OCR ステップをより大規模な文書処理パイプラインに組み込む。  
- 抽出テキストに対してスペルチェックやエンティティ抽出などの後処理を追加し、品質を向上させる。  

コードだけでなく、各設定が何を意味するかを理解することが重要です。**GPU メモリ上限を設定** するタイミングと CPU フォールバックの判断ができれば、スケーラブルな OCR ソリューションを構築できます。

PNG のサイズやマルチページ TIFF、GPU エラーのトラブルシューティングについて質問があれば、下のコメント欄でお気軽にどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}