---
category: general
date: 2026-03-13
description: Aspose.OCR を使用して TIFF ファイルからテキストを抽出する方法を学びながら、バッチ OCR を迅速かつ確実に実行する方法。ステップバイステップのチュートリアルをご覧ください。
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ja
og_description: C#でバッチOCRを実行し、Aspose.OCRを使用してTIFFファイルからテキストを抽出する方法を学びましょう。このガイドでは、セットアップ、コード、ベストプラクティスのヒントをカバーしています。
og_title: C#でOCRをバッチ処理する方法 – 完全プログラミングガイド
tags:
- OCR
- C#
- Aspose
- Batch processing
title: C#でOCRをバッチ処理する方法 – 完全プログラミングガイド
url: /ja/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

.

Also keep "Pro tip:", "Edge case:", etc.

Translate "Expected Output", "Handling Common Gotchas", etc.

Make sure to keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でバッチ OCR を実行する方法 – 完全プログラミングガイド

膨大なスキャン済み請求書を、ファイルごとに別々のスクリプトを書かずに **バッチ OCR** したいと思ったことはありませんか？ あなただけではありません。実務プロジェクトの多くで問題になるのは OCR の精度そのものではなく、検索可能なテキストに変換しなければならない画像（主に TIFF）の量です。

このチュートリアルでは、Aspose.OCR の `BatchProcessor` を使って **バッチ OCR** を実行する方法と、**tiff からテキストを抽出** する方法を、シンプルでクリーンな一連の手順で解説します。最終的に、フォルダー全体を処理し、オプションで GPU 加速を利用し、結果のプレーンテキストを任意の場所に出力するコンソールアプリが完成します。

## 必要なもの

- **.NET 6+**（または従来のランタイムが必要なら .NET Framework 4.7.2）  
- **Aspose.OCR for .NET** – `dotnet add package Aspose.OCR` で NuGet パッケージを取得できます。  
- 読み取り対象の **TIFF** 画像が入ったフォルダー（本チュートリアルでは `Invoices` を例に使用）  
- オプション: DirectX 11 または CUDA に対応した GPU（処理速度を上げたい場合）

余計なサービスやクラウドキーは不要です。ローカルの C# プロジェクトと Aspose ライブラリだけで完結します。

## 手順 1: プロジェクトを作成し Aspose.OCR をインストール

まず、コンソールアプリを作成します。

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **プロのコツ:** Windows 環境で GPU 加速を利用する場合は、最新のグラフィックドライバーがインストールされていることを確認してください。そうでないと `UseGpu = true` フラグは自動的に CPU にフォールバックします。

## 手順 2: BatchProcessor の設定を作成

次に `BatchProcessor` を設定します。これが **バッチ OCR** の中心で、使用言語、前処理フィルタ、GPU の有無を指定します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**なぜこの設定か？**  
- `Language = Language.English` は英語モデルを使用するようエンジンに指示し、汎用モデルよりはるかに精度が高くなります。  
- `UseGpu` は適切な GPU があれば処理時間を半分に短縮できますが、ノートパソコンなど GPU が無い環境では `false` のままで問題ありません。  
- フィルタパイプラインは、人が行うようにページを整列させ、斑点を除去してから OCR エンジンに渡す流れを再現しています。

## 手順 3: TIFF フォルダーをプロセッサに指定

**バッチ OCR** の次のステップは、ライブラリにソースファイルの場所を教えることです。ワイルドカードがサポートされているので、`.tif` ファイルを一括で取得できます。

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **エッジケース:** 画像の拡張子が混在している場合（`.tiff`, `.tif`, `.png` など）、`AddFolder` を複数回呼び出すか、`*.*` を指定してコード内でフィルタリングしてください。

## 手順 4: OCR 結果の出力先を選択

「抽出したテキストはどこに保存されるのか？」と疑問に思うかもしれません。これが **バッチ OCR** の第3の柱で、出力先と形式を定義します。ここではプレーンテキストファイルを元画像と同じフォルダーに保存します。

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

プレーンテキストの代わりに JSON や XML が欲しい場合は、`OutputFormat.PlainText` を `OutputFormat.Json` または `OutputFormat.Xml` に置き換えるだけです。ライブラリが自動で変換してくれます。

## 手順 5: バッチジョブを実行し結果をレポート

最後にジョブを開始します。`Execute` メソッドは全ファイルの処理が完了するまでブロックし、`ProcessedCount` で成功件数を確認できます。

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### 期待される出力

プログラムを実行すると、コンソールに次のようなメッセージが表示されます。

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

`Output` フォルダーには、元の TIFF と同名の `.txt` ファイルが各画像ごとに作成されます（例: `Invoice_001.txt`）。任意のファイルを開くと、OCR が生成した生テキストが確認でき、検索インデックスや downstream のデータ抽出パイプラインにそのまま流し込めます。

## よくある落とし穴の対処法

### 1. GPU が利用できない

`UseGpu = true` に設定しても対応デバイスが見つからない場合、Aspose は自動的に CPU にフォールバックします。明示的にハンドリングしたい場合は `DeviceNotFoundException` を捕捉してください。

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. 同一フォルダーに非 TIFF ファイルが混在している

混在フォルダーを扱う場合は、プログラム側でフィルタリングします。

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. メモリを超える大容量ファイル

ページ数が非常に多いマルチページ TIFF では、ストリーミングを有効にしてください。

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## **tiff からテキストを抽出** する際の精度向上のプロチップ

- **解像度が重要** – 300 dpi 以上を目指しましょう。これ以下だと文字が抜け落ちやすくなります。  
- **カラー vs グレースケール** – カラースキャンは OCR 前にグレースケールに変換すると効果的です。`DeskewFilter` が内部で実施しますが、さらに速度を上げたい場合は `ColorDepthReductionFilter` を追加してください。  
- **ポストプロセッシング** – プレーンテキスト取得後にスペルチェックや正規表現でクリーンアップすると、典型的な OCR の誤認（例: “0” と “O”）を修正できます。

## 完全動作サンプル（コピペで使用可）

以下はコンパイルして実行できるフルプログラムです。プレースホルダーのパスを自分の環境に合わせて置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

コンパイルと実行:

```bash
dotnet run
```

これで、**tiff からテキストを抽出** した結果が `.txt` ファイルとして整然と出力されます。

## 結論

C# で **バッチ OCR** を最初から最後まで実装する方法を解説し、**tiff からテキストを抽出** する際に必要なすべてのポイントを網羅しました。主なポイントは次の通りです。

1. 繰り返しコードを書かずに Aspose.OCR の `BatchProcessor` を活用する。  
2. 前処理フィルタ（デスクュー、デスペックル）で精度を向上させる。  
3. 可能なら GPU 加速を利用し、常に CPU フォールバックを用意する。  
4. 結果を予測可能なフォルダー構造に保存し、 downstream ジョブが自動で取得できるようにする。

ここからさらに進める例:

- プレーンテキストを **検索インデックス**（例: Elasticsearch）に投入し、請求書を検索可能にする。  
- 出力を **JSON** に変換し、機械学習モデルで項目抽出を行う。  
- 破損した TIFF や権限エラーに対する **エラーハンドリング** を追加する。

ぜひ試してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}