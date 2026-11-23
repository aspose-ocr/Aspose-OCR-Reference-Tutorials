---
category: general
date: 2026-06-25
description: バッチ OCR 処理チュートリアルでは、C# で Aspose.OCR を使用して画像をテキストに変換し、画像からテキストを抽出する方法を示します。ステップバイステップの実装を学びましょう。
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: ja
og_description: C# のバッチ OCR 処理を使用すると、画像をテキストに迅速に変換できます。このガイドに従って、Aspose.OCR を使って画像からテキストを抽出する方法を学びましょう。
og_title: C#でバッチOCR処理 – 画像をテキストに変換
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: C#によるバッチOCR処理 – 画像をすばやくテキストに変換
url: /ja/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# におけるバッチ OCR 処理 – 画像をテキストに素早く変換

スキャンしたフォルダー全体を、ファイルごとに個別のループを書かずに **バッチ OCR 処理** できるか、考えたことはありませんか？ あなただけではありません。請求書の自動化、古い文書のアーカイブ、あるいはシンプルな個人用写真‑テキスト変換ユーティリティなど、多くのプロジェクトで **画像をテキストに変換** する必要があります。  

良いニュースです。Aspose.OCR を使えば、数行のコードでそれが実現できます。このガイドでは、バッチ OCR 処理を使用して **画像からテキストを抽出する方法** を示す、完全に実行可能なサンプルをステップバイステップで解説し、各要素が重要な理由と一般的な落とし穴を回避するためのヒントを提供します。

## 学べること

- バッチ操作用に Aspose.OCR をセットアップする
- 並列処理を構成して大規模ジョブを高速化する
- OCR 結果を個別の `.txt` ファイルに自動で書き出す
- 進捗イベントを処理し、常に現在の状態を把握できるようにする
- カスタムエラーハンドリングや別の出力形式に対応できるようコードを拡張する

Aspose の経験は不要です。基本的な C# の知識と .NET 6（以降）がインストールされていれば始められます。

---

## ステップ 1: バッチ OCR 処理のためのプロジェクト準備

コードに入る前に、Aspose.OCR の NuGet パッケージがインストールされていることを確認してください。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** 最新の安定版（2026年6月時点では 23.9）を使用すると、パフォーマンス向上と最新の言語サポートが得られます。

まだコンソールアプリがない場合は、以下のコマンドで新規作成してください：

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

これでバッチ OCR 処理ロジックを書く準備が整いました。

## ステップ 2: 変換したい画像ファイルを定義する

**バッチ OCR 処理** の最初のステップは、認識器に処理対象のファイルを指示することです。リストをハードコードしたり、ディレクトリから取得したり、データベースからパスを取得したりできます。分かりやすさのため、ここでは静的リストを使用します：

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **重要な理由:** コレクションを渡すことで、`BatchRecognizer` は内部で�数スレッドに仕事をスケジュールでき、これが高速な **画像をテキストに変換** 操作の核心です。

## ステップ 3: BatchRecognizer の作成と設定

ここからがチュートリアルの核心です。`BatchRecognizer` クラスはスレッド処理の詳細を抽象化します。`Parallelism` プロパティを CPU コア数に合わせたり、他の作業用にコアを残したい場合はカスタム値に調整できます。

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **説明:** `Parallelism = 4` と設定すると、ライブラリは同時に 4 つの OCR ジョブを実行します。一般的なクアッドコアラップトップでは、システムを飽和させずに速度が向上します。コア数が多いサーバーで実行する場合は、この数値を増やしてください。

> **エッジケース:** 非常に大きな画像を処理する場合、メモリ制限に達することがあります。その場合は並列度を下げるか、ファイルを小さなチャンクに分割して処理してください。

## ステップ 4: OCR を実行し結果を取得する

`BatchRecognizer` の `Recognize` を呼び出すと、キーが元のファイルパス、値が抽出されたテキストや信頼度スコアなどを含む `OcrResult` となるディクショナリが返されます。

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **取得できるもの:** 各画像について、`OcrResult.Text` にプレーンテキストが格納されています。これは、プログラム上で **画像からテキストを抽出する方法** が必要なときにまさに求められる情報です。

## ステップ 5: 各結果を .txt ファイルに保存する

実際のシナリオでは、OCR の出力を後で処理できるように保存する必要があります（検索インデックスに投入したり、データベースレコードに添付したり）。以下のループは、元のファイル名を保持したまま、各ソース画像の隣に `.txt` ファイルを書き込みます。

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **ヒント:** 別の形式（JSON、CSV など）が必要な場合は、`entry.Value` を好きな形でシリアライズすれば OK です。`OcrResult` オブジェクトは `Confidence` や `PageCount` も提供しており、必要に応じて利用できます。

## ステップ 6: 完了を通知し、エラーを適切に処理する

きれいに終了させることで、ユーティリティの完成度が高まります。サンプルコードはすでに最終行を出力していますが、ここでは try‑catch ブロックを追加し、ファイルが見つからない、サポート外の画像形式などの予期しない例外を捕捉できるようにします。

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **ラップする理由:** 大量のフォルダーでプログラムを実行すると、1 つの破損した画像が原因でジョブ全体が中断される可能性があります。適切なエラーハンドリングを行えば、問題をログに記録し、残りのファイルの処理を続行できます。

## 完全な実行可能サンプル

以下は `Program.cs` にコピー＆ペーストできる完全なプログラムです。画像パスが実際のファイルを指していることを確認してください。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### 期待される出力

`dotnet run` を実行すると、以下のような出力が表示されます：

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

各 `.txt` ファイルには、対応する画像のプレーンテキスト版が保存されます—これがスケールで **画像をテキストに変換** する際に必要なものです。

---

## よくある質問とエッジケース

### サポートされている画像形式は？

Aspose.OCR は JPEG、PNG、TIFF、BMP、GIF を標準でサポートしています。WebP のような形式に遭遇した場合は、事前に変換するかサードパーティのデコーダーを使用してください。

### OCR 言語を英語のみに限定できますか？

はい。`Recognize` を呼び出す前に、`BatchRecognizer` の `Language` プロパティを設定します：

```csharp
ocrBatch.Language = "en";
```

言語を限定することで、特に単一言語で **画像からテキストを抽出する方法** にだけ関心がある場合、精度と速度が向上します。

### メモリを圧迫せずに数千ファイルを処理するには？

リストを小さなバッチ（例: 500 ファイルずつ）に分割し、上記の手順をループで実行します。これによりメモリ上のディクショナリが管理しやすくなり、バッチごとに進捗を記録できます。

### OCR 結果をファイルではなくデータベースに保存したい場合は？

`File.WriteAllText` の呼び出しを、好みのデータアクセスコードに置き換えます。例として Dapper を使用する場合は以下の通りです。

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

---

## 結論

これで、Aspose.OCR を使った C# の **バッチ OCR 処理** を習得し、**画像をテキストに変換** するシンプルな方法と、**画像からテキストを抽出する方法** を効率的に行うための実用的なヒントをいくつか学びました。ファイルパスの収集、`BatchRecognizer` の設定、OCR の実行、結果の保存という一連のフローは、読みやすい単一プログラムに収められています。

次は何をすべきでしょうか？マルチコアサーバーで `Parallelism` を上げてみたり、言語パックを試したり、スペルチェックなどの後処理を追加したりできます。また、抽出したテキストを Azure Cognitive Search に流し込み、スキャン文書を数秒で検索可能にすることも検討してください。

OCR の対象を PDF に拡張したり、マルチページ TIFF を扱う方法など、面白いアイデアがあればコメントで共有してください。皆で情報を広げていきましょう。Happy coding！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っており、実践的なコード例とステップバイステップの解説が含まれています。

- [フォルダー上で OCR 操作を使用して画像からテキストを抽出する](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET でリストを使って画像をバッチ OCR する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Aspose.OCR for .NET を使用して ZIP アーカイブからテキストを抽出する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}