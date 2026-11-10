---
category: general
date: 2026-04-29
description: C# で Aspose OCR を使用して画像を高速にバッチ OCR しましょう。jpg ファイルからテキストを抽出する方法、スキャン画像からテキストを読み取る方法、そして画像リストを並列処理する方法を学びます。
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: ja
og_description: Aspose OCRで画像を迅速にバッチOCR処理します。このガイドでは、jpgからテキストを抽出し、スキャン画像からテキストを読み取り、画像リストを並列に処理する方法を示します。
og_title: C#で画像をバッチOCR – JPGスキャンの並列OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#で画像のバッチOCR – JPGスキャンの並列OCR
url: /ja/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でバッチOCR画像 – JPGスキャンの並列OCR

Ever needed to **batch OCR images** but weren’t sure how to scale the work across multiple files? You’re not alone—developers often hit a wall when they try to read text from scans one by one. The good news is that with Aspose OCR you can **extract text from jpg** files, **read text from scans**, and **process image list** items in parallel with just a few lines of C#.

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows exactly how to do that. By the end you’ll have a self‑contained console app that recognises a folder of JPEG scans, prints each page’s text, and tells you how long each operation took. No external docs to chase, no half‑filled code snippets—just a full solution you can drop into Visual Studio and run.

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.6+ でもコンパイル可能）
- **Aspose.OCR** NuGet パッケージ (`Install-Package Aspose.OCR`)
- 処理したい JPG またはスキャン画像ファイル数点
- お好みの IDE；私は Visual Studio 2022 を使用していますが、VS Code でも問題ありません

以上です。NuGet パッケージがすでにインストール済みならすぐに始められます。

## Step 1 – Initialize the OCR Engine (Batch OCR Images Setup)

最初に `OcrEngine` インスタンスを作成し、認識対象の言語を指定します。ほとんどの場合 English で十分ですが、 `OcrLanguage.English` を任意のサポート言語に置き換えることができます。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Why this matters:* エンジンを一度だけ初期化してすべての画像で再利用する方が、ファイルごとに新しいインスタンスを作成するよりもはるかに効率的です。これにより Aspose は内部リソースを共有でき、**parallel OCR processing** に不可欠です。

## Step 2 – Build the List of Images (Process Image List)

次に、バッチ認識に渡すファイルパスのコレクションを定義します。`Directory.GetFiles` で動的に生成することもできますが、ここでは分かりやすさのために数件をハードコードします。

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Tip:* 数千枚のスキャンがある場合は、`Directory.EnumerateFiles` に `*.jpg` などのフィルタを付けて、リスト全体をメモリに読み込むのを防ぎましょう。

## Step 3 – Run the Batch Recognition (Parallel OCR Processing)

本題です：`BatchRecognize` を呼び出します。このメソッドは `maxDegreeOfParallelism` 引数を受け取り、Aspose が起動するスレッド数を制御します。デフォルトは 4 スレッドですが、CPU にコアが多ければ増やすことが可能です。

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*What’s happening under the hood?* Aspose は `imagePaths` コレクションをチャンクに分割し、各チャンクを別々のスレッドに割り当てて結果を集約します。これは **process image list** を同時に処理できる、**extract text from jpg** ファイルに最も効率的な方法です。

## Step 4 – Display the Results (Read Text from Scans)

最後に `recognitionResults` コレクションをループし、各ファイルのテキストと処理時間を出力します。`OcrResult` オブジェクトは元ファイル名も提供するため、ログや保存時に便利です。

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Expected output (example):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

各ブロックがファイル名、OCR にかかった時間、抽出されたテキストを示していることに注目してください。これは **reading text from scans** を本番パイプラインで行う際に必要な情報そのものです。

## Handling Common Edge Cases

| 状況 | 注意点 | 簡単な対処法 |
|-----------|-------------------|-----------|
| **Missing file** | `BatchRecognize` 内で `FileNotFoundException` がスローされる | `File.Exists` でパスを検証してから `imagePaths` に追加 |
| **Unsupported format** | Aspose はラスタ画像 (JPG, PNG, BMP, TIFF) のみ対応 | PDF を画像に変換してから処理 (Aspose.PDF を使用) または対象外にする |
| **Memory pressure** | 大きな画像が多数スレッドで走ると RAM が逼迫する | `maxDegreeOfParallelism` を下げるか、OCR 前に画像をリサイズ |
| **Non‑English text** | 言語が English に固定されていると他のスクリプトが認識されない | `Language = OcrLanguage.French` などに変更（多言語コンボも可） |

これらのポイントを抑えておけば、ユーザーアップロードやスキャンアーカイブから来る **processing an image list** に対してもバッチジョブを安定させられます。

## Pro Tip – Tuning Parallelism

8 コアマシンで実行する場合、並列度を 6〜8 に上げると速度が向上します。ただし、各スレッドはビットマップ用のメモリも消費する点に注意。目安としては次のコードをご参照ください。

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

`maxThreads` を `BatchRecognize` に渡すことで、マシンのスペックに合わせた動的設定が可能です。

## Full Working Example (Copy‑Paste Ready)

以下はそのままコンパイルできる完全プログラムです。`YOUR_DIRECTORY` を JPEG スキャンが格納されたフォルダーのパスに置き換えてください。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Note:** `using System.IO;` 行は `Directory` ヘルパーに必須です。JPG が見つからない場合はフレンドリーなメッセージを出力し、サイレント失敗を防ぎます。

## Conclusion

今回、**batch OCR images** ワークフローを実演しました。**extract text from jpg** ファイルを **read text from scans** し、**process image list** を **parallel OCR processing** で効率的に処理する方法です。エンジンの初期化、ファイルコレクションの投入、結果処理のすべてがメモリ使用量とスレッド数をコントロールしながら実装されています。

次のステップに進みませんか？言語をフランス語に変えてみる、PDF‑to‑image 変換を追加する、OCR テキストをデータベースに保存するなど、パターンは変わりません：一度だけ初期化し、リストを渡し、Aspose に並列で重い処理を任せるだけです。

質問や独自のチューニングを共有したい方はコメントを残してください。Happy coding!

![バッチOCR画像処理フロー](https://example.com/placeholder.png "バッチOCR画像ワークフローを示す図")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}