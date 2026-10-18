---
category: general
date: 2026-02-14
description: C#でOCRを使用してPNGファイルからテキストを素早く抽出する方法。バッチOCR画像の処理や複数画像の処理、Aspose OCR C#の利用をひとつのガイドで学べます。
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: ja
og_description: Aspose OCR C# を使用した C# での OCR の使い方。このチュートリアルでは、PNG ファイルからテキストを抽出し、画像をバッチ
  OCR し、複数の画像を効率的に処理する方法を示します。
og_title: C#でOCRを使用する方法 – バッチPNGテキスト抽出
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でOCRを使用する方法 – Aspose OCRでPNG画像をバッチ処理
url: /ja/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – Aspose OCR で PNG 画像をバッチ処理

**OCR を使用して** 複数の PNG ファイルからテキストを抽出したいのに、ファイルごとに別々のルーチンを書かなければならないと悩んだことはありませんか？ 同じ悩みを抱える開発者は多いです。特に画像がフォルダーに格納されていて、各ファイルごとに OCR エンジンを起動しなければならない場合、**PNG からテキストを抽出** する作業は壁にぶつかりがちです。

このガイドでは、**画像をバッチ OCR** し、**複数画像を並列に処理** でき、強力な **Aspose OCR C#** ライブラリを活用した、すぐに実行可能な完全なソリューションをステップバイステップで解説します。最終的に、任意の数の PNG を読み取り、テキストを抽出し、コンソールに結果を出力する単一の実行ファイルが手に入ります――コードは数行だけです。

## 前提条件

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）  
- 有効な Aspose.OCR for .NET ライセンス（または無料トライアル） – Aspose のウェブサイトから取得できます。  
- 読み取り対象の PNG ファイルが入ったフォルダー。  
- Visual Studio 2022（または任意の C# 対応 IDE）。  

`Aspose.OCR` 以外の NuGet パッケージは必要ありません。

## Step 1: OCR の使用方法 – Aspose OCR エンジンの初期化

最初に必要なのは `Engine` クラスのインスタンスです。このオブジェクトは基盤となる OCR 技術を抽象化し、ハードウェアとライセンスに応じて CPU または GPU 上で動作できます。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Why this matters:* エンジンを一度だけ初期化してスレッド間で再利用することで、メモリ使用量を抑え、OCR モデルのロードオーバーヘッドを回避できます。また、すべての画像で設定が一貫することが保証されます。

## Step 2: Extract Text PNG – 画像パスの取得

次に、ファイルパスのコレクションが必要です。実際のプロジェクトではディレクトリを動的に走査することが多いですが、ここでは分かりやすさのためにサンプルファイルを手動で列挙します。

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tip:* `YOUR_DIRECTORY` を画像が格納されている絶対パスまたは相対パスに置き換えてください。ファイルが多数ある場合は、手動リストの代わりに `Directory.GetFiles("YOUR_DIRECTORY", "*.png")` を使用できます。

## Step 3: Batch OCR Images – 並列で認識を実行

画像を順番に処理するのはシンプルですが遅いです。`Parallel.ForEach` を使うことで **複数画像を同時に処理** でき、マルチコア CPU の性能を活かせます。

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Why parallel?* 各 OCR 呼び出しは CPU 集中型ですが互いに独立しているため、同時に実行することで特に 4 コア以上のマシンで総実行時間を大幅に短縮できます。

## Step 4: Process Multiple Images – 抽出テキストの表示

`OcrResult` オブジェクトのコレクションが揃ったら、これらを列挙して認識結果のテキストをコンソールに出力します。実際のアプリケーションではここでデータベースに保存したりファイルに書き出したりしますが、例示の簡潔さのためコンソール出力に留めています。

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Expected console output (sample):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

画像の読み込みに失敗した場合、Aspose は例外をスローします。`engine.Recognize` 呼び出しを try/catch でラップすれば、バッチ全体を中断せずにエラーを記録できます。

## Step 5: 完全動作サンプル – すべてのコードを結合

以下は新しい C# コンソールプロジェクトにコピペできる完全版プログラムです。`using` 文から最終的な出力ループまで、すべてが含まれています。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### サンプルの実行手順

1. Visual Studio で新規 **Console App** プロジェクトを作成します。  
2. **Aspose.OCR** NuGet パッケージを追加します（`Install-Package Aspose.OCR`）。  
3. `YOUR_DIRECTORY` を PNG ファイルが格納されているパスに置き換えます。  
4. ビルドして実行 – コンソールに抽出されたテキストが表示されるはずです。

## プロのコツ & エッジケース

- **GPU 加速:** 対応 GPU とライセンスがある場合、エンジン作成前に `EngineSettings` で有効化してください。画像ごとの処理時間が数秒短縮されます。  
- **大容量ファイル:** 10 MB 超の画像は、メモリ負荷を下げるために事前に縮小すると効果的です。  
- **言語サポート:** デフォルトは英語です。`engine.Language = Language.French;`（またはサポートされている任意の言語）を設定すると、非英語テキストの認識精度が向上します。  
- **エラーハンドリング:** 並列ループ内の `try/catch` により、破損ファイルがバッチ全体を中断しないようにしています。失敗情報はファイルにログとして残すことも可能です。  
- **結果の保存:** コンソール出力の代わりに `result.Text` を `File.WriteAllText(Path.ChangeExtension(path, ".txt"))` で `.txt` ファイルに書き出すことができます。

## 結論

これで **C# で OCR を使用して** **PNG からテキストを抽出** し、**画像をバッチ OCR** し、**複数画像を効率的に処理** する方法が分かりました。ソリューションは完全に自己完結型で、並列実行され、数百から数千のファイルにも最小限の変更で対応可能です。

次のステップに進みませんか？ コンソール出力を CSV レポートに置き換えたり、GPU 加速を試したり、OCR テキストを検索インデックスに流し込んだりしてみてください。可能性は無限大です。初期化は一度、並列実行、エラーは優雅に処理するというパターンは、あらゆる画像処理パイプラインで役立ちます。

Happy coding, and may your OCR jobs be fast and error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}