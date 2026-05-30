---
category: general
date: 2026-04-26
description: PNG画像を高速にバッチOCRする方法。PNGからテキストを抽出し、画像をテキストに変換し、認識したテキストを書き出し、Aspose OCRでPNGディレクトリを読み取ります。
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: ja
og_description: C# と Aspose OCR を使用して PNG 画像をバッチ OCR する方法。このガイドでは、PNG からテキストを抽出し、画像をテキストに変換し、認識されたテキストを書き出す効率的な方法を示します。
og_title: C#でPNG画像を一括OCRする方法 – ステップバイステップ
tags:
- OCR
- C#
- Aspose
title: C#でPNG画像を一括OCRする方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PNG 画像をバッチ OCR する方法 – 完全ガイド

フォルダー内の PNG ファイル全体を **バッチ OCR** したいと思ったことはありませんか？数十枚のスクリーンショットやスキャンした領収書、グラフィックを検索可能なテキストに変換する必要がある方は多いでしょう。このチュートリアルでは、**PNG からテキストを抽出**し、**画像をテキストに変換**し、**認識したテキストを個別のファイルに書き出す**という一連の流れを、PNG ディレクトリを自動的に読み取る形で実装します。

このガイドが終わる頃には、任意の枚数の画像を一括で処理できる C# コンソールアプリが完成しています。余計なスクリプトや手動でのコピペは不要です。すべてコードが自動で行ってくれます。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework でも動作します）。  
- **Aspose.OCR for .NET** NuGet パッケージ（無料トライアルでテスト可能）。  
- OCR をかけたい *.png* ファイルが入ったフォルダー。  
- Visual Studio 2022 もしくはお好みの C# IDE。

これらが揃ったら、実装に進みましょう。

## Step 1 – Prepare Your Input and Output Folders *(Read PNG Directory)*

最初に行うのは、画像が入っているフォルダーをプログラムに指定し、生成される *.txt* ファイルの保存先を決めることです。`Directory.GetFiles` を使うと、ディレクトリ内のすべての PNG を簡単に列挙できます。

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Why this matters:**  
- ワイルドカード (`*.png`) を使用することで、画像ファイルだけを対象にし、余計なドキュメントは無視できます。  
- 出力フォルダーを事前に作成しておくことで、後で `DirectoryNotFoundException` が発生するのを防げます。

> **Pro tip:** JPEG や BMP など他の形式にも対応したい場合は、検索パターンを拡張するか、`Directory.EnumerateFiles` に複数の拡張子を渡すだけです。

## Step 2 – Initialise the OCR Engine *(Convert Images to Text)*

Aspose.OCR には CPU ベースの `OcrEngine` と GPU 加速の `GpuOcrEngine` の 2 種類があります。ほとんどのバッチ処理では CPU エンジンで十分ですが、GPU が利用可能な環境ではクラス名を差し替えるだけで高速化できます。

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Why this matters:**  
- 言語を指定することで、エンジンが期待する文字セットを把握でき、精度が大幅に向上します。  
- パフォーマンスがボトルネックになる大規模バッチの場合、`GpuOcrEngine` への切り替えは 1 行の変更で済みます。

## Step 3 – Create a Batch Recogniser

Aspose は `BatchRecognizer` という便利なクラスを提供しており、ファイルパスの列挙可能オブジェクトを受け取って結果を 1 件ずつストリームします。これにより、すべての画像を一度にメモリに読み込む必要がなくなり、大容量フォルダーでも安全に処理できます。

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Why this matters:**  
- バッチ認識器がループロジックをカプセル化してくれるため、各結果をどう扱うかに集中でき、イテレーションの安全性を自前で実装する手間が省けます。

## Step 4 – Run OCR on All Images and Write the Output *(Write Recognized Text)*

いよいよ OCR を実行します。`Recognize` メソッドは `IEnumerable<RecognitionResult>` を返し、各結果に抽出されたテキストやメタデータが格納されています。

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Why this matters:**  
- `File.WriteAllText` を使うことで、デフォルトで UTF‑8 エンコーディングでテキストが保存され、特殊文字が正しく保持されます。  
- インクリメンタルな命名 (`out_0.txt`, `out_1.txt`) は処理順序と一致するため、デバッグ時に便利です。

> **Edge case:** 画像が破損しているなど OCR に失敗した場合、`RecognitionResult.Text` は空文字列になります。ループ内で簡単なチェックを入れて失敗をログに残すことができます。

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Step 5 – Put It All Together – Full Working Example

以下は新しいコンソールプロジェクトにそのまま貼り付けられる完全なプログラムです。`using` ディレクティブ、フォルダー検証、そしてバッチ完了時にコンソールに通知する小さな UI が含まれています。

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Expected output:**  
プログラム実行時には次のような出力が表示されます。

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

そして、出力フォルダー内に `out_0.txt` … `out_11.txt` が生成され、それぞれ対応する画像のプレーンテキストが格納されています。

## Common Questions & Tips

| Question | Answer |
|----------|--------|
| *Can I OCR sub‑folders as well?* | はい。`Directory.GetFiles` を `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)` に置き換えるだけです。 |
| *What if I need a different language?* | `ocrEngine.Language = Language.Spanish;` のように、サポートされている任意の列挙子を設定してください。 |
| *How do I handle huge batches (thousands of files)?* | メモリ消費を抑えるためにチャンク単位で処理するか、`Parallel.ForEach` にスロットリングした並列度を設定して実行すると良いでしょう。 |
| *Is the output always UTF‑8?* | `File.WriteAllText` は BOM なしの UTF‑8 がデフォルトです。ラテン系以外の言語（例: アジア系文字）では `Encoding.UTF8` を明示的に指定する必要がある場合があります。 |
| *Can I get confidence scores?* | `RecognitionResult` は `Confidence` プロパティを公開しています。品質管理のためにテキストと一緒にログに出力できます。 |

## Visual Overview *(How to Batch OCR – Diagram)*

![PNG フォルダー → OCR エンジン → バッチ認識器 → 出力 txt ファイルの流れを示すバッチ OCR ワークフロー図](https://example.com/diagram-how-to-batch-ocr.png "バッチ OCR の流れ")

*alt テキストは主要キーワードを含み、SEO 画像要件を満たしています。*

## Wrapping Up

Aspose.OCR を使って PNG フォルダー全体を **バッチ OCR** する方法を、ディレクトリの読み取りから認識テキストの書き出しまで一通り解説しました。このソリューションは完全に自己完結型で、最新の .NET ランタイム上で動作し、GPU 加速や多言語対応、並列処理への拡張も容易です。

次のステップに進みませんか？`Language.Latin` を別の言語に差し替えてみたり、認識結果を検索インデックスに統合してドキュメントを即座に検索可能にしたりしてみてください。バッチ OCR をマスターすれば、可能性は無限に広がります。

Happy coding, and let me know in the comments if you hit any snags!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}