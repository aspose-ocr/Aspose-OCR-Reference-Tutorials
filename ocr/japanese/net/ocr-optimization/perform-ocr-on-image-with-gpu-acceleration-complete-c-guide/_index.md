---
category: general
date: 2026-02-11
description: C#でGPU OCRを使用して画像のOCRを実行する方法を学びましょう。このステップバイステップのチュートリアルでは、セットアップ、コード、ベストプラクティスをカバーしています。
draft: false
keywords:
- perform OCR on image
- use GPU OCR
- Aspose OCR C#
- GPU acceleration OCR
- OCR performance tuning
language: ja
og_description: C#でGPU OCRを使用して画像のOCRを実行します。Aspose OCRを使った高速で信頼性の高いソリューションのためにこのガイドに従ってください。
og_title: GPUで画像のOCRを実行 – 完全なC#実装
tags:
- OCR
- C#
- Aspose
- GPU Computing
title: GPUアクセラレーションで画像のOCRを実行する – 完全C#ガイド
url: /ja/net/ocr-optimization/perform-ocr-on-image-with-gpu-acceleration-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPUアクセラレーションで画像のOCRを実行 – 完全なC#ガイド

大きなTIFFファイルでCPUが苦しんでいるときに **画像のOCRを実行** したことがありますか？ あなたは一人ではありません。実際のプロジェクトでは、大きなドキュメントの処理が数秒を数分に変えてしまい、その遅延はユーザーと予算の両方に悪影響を与えます。  

良いニュースです。GPUを活用すれば、処理時間を劇的に短縮できます。このチュートリアルでは、AsposeのGPUアクセラレートエンジンを使用して **画像のOCRを実行する方法** を正確に示すハンズオン例を順に解説し、一般的なドキュメントには載っていない実用的なヒントもいくつか紹介します。

> **得られるもの:** すぐに実行できるC#コンソールアプリ、各行の解説、一般的な問題のトラブルシューティングガイド。外部参照は不要です—必要なものはすべてここにあります。

## 必要なもの

始める前に、開発マシンに以下がインストールされていることを確認してください。

| 前提条件 | 最小バージョン |
|--------------|-----------------|
| .NET 6.0 SDK またはそれ以降 | 6.0 |
| Visual Studio 2022（または好きなIDE） | 17.0 |
| Aspose.OCR for .NET（NuGet パッケージ） | 23.11 以上 |
| CUDA 対応 GPU（NVIDIA） | Compute Capability 3.5 以上 |
| サンプル画像 – 例: `large_document.tif` | 任意のサイズ |

これらのいずれかに心当たりがなくても、慌てないでください。**GPU OCR の使用** 機能は、控えめなGPUでも動作し、NuGet パッケージが必要なネイティブバイナリをすべて取得してくれます。

## 手順 1: GPU アクセラレーションで画像の OCR を実行

最初に必要なのは、GPU 対応 OCR エンジンのインスタンスです。このオブジェクトはグラフィックカード上で重い処理を行いながら、シンプルで同期的な API を提供します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System.Drawing;

// Create a GPU‑accelerated OCR engine and configure it
var ocrEngine = new GpuOcrEngine
{
    // Select the first GPU in the system (device index 0)
    DeviceId = 0,
    // Let the engine download language packs automatically if they’re missing
    AutomaticResourceDownload = true,
    // Specify the language you want to recognize – English in this case
    Language = OcrLanguage.English
};
```

**この設定が重要な理由:**  
- `DeviceId = 0` はライブラリにプライマリ GPU を使用させることを示します。複数のカードがある場合は変更できます。  
- `AutomaticResourceDownload = true` は、ローカルに英語の言語データが存在しない場合のランタイムエラーを防ぎます。  
- `Language` を明示的に設定することで、エンジンがデフォルトで遅い汎用モデルにフォールバックするのを回避できます。

> **プロのコツ:** ヘッドレスサーバーで実行する場合は、NVIDIA ドライバーがインストールされており、`nvidia-smi` コマンドが GPU を “Online” と報告していることを確認してください。そうでなければエンジンは静かに CPU にフォールバックします。

## 手順 2: 画像ファイルをロードする

次に、OCR を実行したい画像をロードします。Aspose は任意の `System.Drawing.Image` を扱えるので、JPEG、PNG、TIFF、あるいは変換後のマルチページ PDF も入力できます。

```csharp
// Load the image from disk – replace the path with your own file location
using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");
```

**この設定が重要な理由:**  
- `using` 文を使用することで、画像のアンマネージドリソースが速やかに解放されます。これはループで多数のファイルを処理する際に重要です。  
- 画像が非常に大きい場合（例: 500 MB 超）、GPU メモリ使用量を抑えるために先にダウンサンプリングすることを検討してください。

## 手順 3: GPU OCR エンジンでテキストを認識する

ここで画像を GPU エンジンに渡し、結果を待ちます。`Recognize` メソッドは抽出されたテキストとパフォーマンス指標を含む `OcrResult` オブジェクトを返します。

```csharp
// Perform OCR – this call runs on the GPU
var ocrResult = ocrEngine.Recognize(image);
```

**この設定が重要な理由:**  
- 呼び出しは同期的で、GPU が完了するまでスレッドがブロックされます。UI アプリでは UI の応答性を保つためにバックグラウンドスレッドで実行するのが望ましいです。  
- `ocrResult.ProcessingTime` は経過時間をミリ秒で提供し、**GPU OCR の使用** と CPU のみの代替手段をベンチマークするのに最適です。

## 手順 4: 結果と統計情報を表示する

最後に、認識されたテキストの長さと処理にかかった時間を出力します。実際のアプリケーションでは `ocrResult.Text` をファイルやデータベースに書き込むことが多いでしょう。

```csharp
// Show a quick summary on the console
Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

// Optionally, dump the full text (commented out for brevity)
// Console.WriteLine(ocrResult.Text);
```

**期待される出力（例）:**

```
Recognized 12457 characters in 312 ms
```

マルチメガバイトの TIFF に対して、処理時間が数百ミリ秒程度で測定されていることに注目してください—これは **GPU OCR を使用** したときに期待できる速度向上そのものです。

![画像で OCR を実行する例](/images/perform-ocr-on-image.png "画像で OCR を実行した後のコンソール出力を示すスクリーンショット")

*上のスクリーンショットは、GPU アクセラレーションで画像の OCR を実行した後のコンソール出力を示しています。*

## GPU OCR を効率的に使用する方法

上記のコードはすぐに動作しますが、実運用ではいくつかの問題に直面することがあります。以下に最も一般的な問題とその解決策を示します。

| 問題 | 原因 | 解決策 |
|-------|-------|----------|
| **Out‑of‑memory (GPU)** | 画像が GPU VRAM に対して大きすぎる | `Recognize` を呼び出す前に画像をダウンスケール（`Bitmap` リサイズ）してください。 |
| **Language pack not found** | `AutomaticResourceDownload` が無効、またはインターネット未接続 | `ocrEngine.DownloadResources(OcrLanguage.English)` で言語パックを事前にダウンロードしてください。 |
| **Slow first run** | GPU ドライバの JIT コンパイル | 起動時に小さなダミー画像を一度実行してエンジンをウォームアップしてください。 |
| **Incorrect character set** | `Language` プロパティが誤っている | 正しい列挙体（例: `OcrLanguage.French`）に `Language` を設定してください。 |

**プロのコツ:** 数十ファイルをバッチ処理する場合は、同じ `GpuOcrEngine` インスタンスを再利用してください。ファイルごとに新しいエンジンを作成すると、コストの高い GPU コンテキストスイッチが発生します。

## 完全な動作例

以下は、単一ファイルにまとめた完全なプログラムです。新しいコンソールプロジェクトにコピー＆ペーストして使用できます。

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Drawing;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize GPU OCR engine
            var ocrEngine = new GpuOcrEngine
            {
                DeviceId = 0,
                AutomaticResourceDownload = true,
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the image (adjust the path to your file)
            using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");

            // 3️⃣ Run recognition on the GPU
            var ocrResult = ocrEngine.Recognize(image);

            // 4️⃣ Output statistics
            Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

            // Optional: write the extracted text to a file
            // System.IO.File.WriteAllText("output.txt", ocrResult.Text);
        }
    }
}
```

ファイルを保存し、`dotnet run` を実行すると、文字数と処理時間がコンソールに表示されます。`output.txt` を開く（行のコメントを外す）と、下流処理用の生の OCR テキストが確認できます。

## 結論

ここでは、Aspose の GPU アクセラレートエンジンを使用して **画像の OCR を実行する方法** を、`GpuOcrEngine` の設定から結果の処理、一般的な落とし穴のトラブルシューティングまで示しました。重い処理をグラフィックカードにオフロードすることで、桁違いの速度向上が得られます—大きなドキュメントやリアルタイムスキャンシナリオで必要とされるものです。

> **要点:** `GpuOcrEngine`、自動リソース処理、慎重な画像サイズ設定の組み合わせにより、**GPU OCR を使用** する必要があるあらゆる C# プロジェクトに対して、堅牢で高性能なパイプラインが提供されます。

### 次にやることは？

- **バッチ処理:** コアロジックを `foreach` ループでラップし、画像フォルダーを処理します。  
- **並列処理:** `Parallel.ForEach` と組み合わせてマルチ GPU サーバーで GPU OCR を実行します。  
- **後処理:** `ocrResult.Text` をスペルチェッカーやエンティティ抽出器に渡し、より賢い下流分析を行います。  

自由に実験してください—`OcrLanguage.English` を別の言語に置き換えたり、異なる画像形式を試したり、エンジンを ASP.NET API に統合したりできます。**GPU OCR を適切に使用** すれば、可能性は無限です。

コーディングを楽しんで、OCR ジョブが閃光のような速度で実行されますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}