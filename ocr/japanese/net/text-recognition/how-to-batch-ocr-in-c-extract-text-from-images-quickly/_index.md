---
category: general
date: 2026-02-19
description: C#でAspose.OCRを使用したバッチOCRの方法を学びましょう。このガイドでは、画像からテキストを抽出し、画像を効率的にtxtに変換する手順を示します。
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: ja
og_description: C#でAspose.OCRを使用してバッチOCRを行う方法。画像からテキストを抽出し、画像をtxtに変換する簡単な手順。
og_title: C#でバッチOCRを行う方法 – 高速な画像からテキストへの変換
tags:
- OCR
- C#
- Aspose
title: C#でバッチOCRを実行する方法 – 画像からテキストを素早く抽出
url: /ja/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でバッチ OCR を行う方法 – 完全ステップバイステップガイド

個別にプログラムを書かずに、フォルダー内の画像全体を **how to batch OCR** したいと思ったことはありませんか？ あなただけではありません。多数（時には何千もの）スキャンしたページ、領収書、スクリーンショットからテキストを抽出する必要があるとき、多くの開発者が壁にぶつかります。良いニュースは、Aspose.OCR を使えば、パイプライン全体を自動化し、**extract text from images** と **convert images to txt** を数行のコードで実現できることです。

このチュートリアルでは、OCR バッチプロセッサの設定方法、前処理の調整、並列処理の扱い方、そして各結果を `.txt` ファイルに書き出す方法を示す、完全に実行可能なサンプルを順に解説します。最後まで読むと、任意の .NET プロジェクトに組み込める自己完結型コンソールアプリが手に入ります。

## 必要なもの

- .NET 6.0 以降（コードは .NET Core および .NET Framework でも動作します）
- Aspose.OCR for .NET NuGet パッケージ (`Aspose.OCR`)  
- 処理したい画像ファイル（`.png`、`.jpg` など）が入ったフォルダー
- 適度な量の RAM；デモは 4 並列スレッドを使用しますが、調整可能です

外部サービスや隠し設定ファイルは不要です—今日コンパイルして実行できる純粋な C# コードだけです。

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## 手順 1: Aspose.OCR をインストールし、プロジェクトを設定する

まず、プロジェクトに Aspose.OCR パッケージを追加します：

```bash
dotnet add package Aspose.OCR
```

これが重要な理由: Aspose.OCR には OCR エンジン、言語データ、前処理ユーティリティがすべて含まれているため、サードパーティのバイナリは不要です。パッケージをインストールしたら、新しいコンソールアプリを作成する（または既存のアプリにコードを追加する）し、必要な名前空間をインポートします：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

これらの `using` 文により、バッチプロセッサクラスや便利な I/O ヘルパーにアクセスできるようになります。

## 手順 2: OCR バッチプロセッサを構成する

ここでは `OcrBatchProcessor` をインスタンス化し、対象言語、画像のクリーンアップ方法、並列実行するスレッド数を設定します。これが **how to batch ocr** を効率的に行うための核心です。

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Why enable Deskew?** 多くのスキャン文書は完全に揃っていません。Deskew アルゴリズムは画像を水平に回転させ、認識率を 10‑15 % 向上させることがよくあります。

## 手順 3: 結果コールバックを設定してテキストファイルを保存する

バッチプロセッサは処理が完了した各画像ごとにイベントを発生させます。`ResultProcessed` にサブスクライブして、各 OCR 結果を `.txt` ファイルに書き出すことで、実質的に **convert images to txt** をリアルタイムで行います。

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

ちょっとしたコツ: 元のフォルダー構造を保持したい場合は、`txtPath` をサブフォルダーや別の出力ディレクトリを含むように変更できます。

## 手順 4: 画像フォルダーでバッチを実行する

残すは、**extract text from images** したい画像が入っているフォルダーをプロセッサに指定するだけです。`ProcessFolder` メソッドはサブフォルダーを再帰的に走査するので、スキャンのツリー全体を投入してライブラリに任せられます。

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

プログラムを起動すると、次のようなコンソール出力が表示されます：

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

各画像には、抽出されたテキストを含む同名の `.txt` ファイルが作成されます。

## 完全な動作例

すべてをまとめると、`Program.cs` にコピー＆ペーストできる完全なプログラムは以下の通りです：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### 期待される出力

- ソースディレクトリ内の各 `*.png` または `*.jpg` に対して、同名の `*.txt` ファイルが隣に作成されます。
- コンソールはファイルごとに1行を出力し、リアルタイムのフィードバックを提供します。
- 画像が読み取れない場合（破損ファイル、未対応形式など）、Aspose.OCR はエラーをログに記録しますが、バッチエンジンの組み込みの堅牢性により残りの処理は継続されます。

## よくある質問とエッジケース

### 画像ではなく PDF を処理したい場合は？

Aspose.OCR は内部的に PDF ページを画像として受け取れますが、まず PDF をラスタ画像（例: Aspose.PDF を使用）に変換する必要があります。PNG が得られれば、同じバッチコードをそのまま使用できます。

### 実行時に言語を変更できますか？

はい。`Language` プロパティは任意の `Language` 列挙値（Spanish、French、Chinese など）を受け付けます。多言語文書がある場合は、言語ごとに2回実行するか、`Language.AutoDetect` を使用することを検討してください。

### バッチを特定のファイルタイプに限定するには？

`ProcessFolder` はオプションの `SearchOption` と `string[] extensions` を受け取ります。例：

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### GPU 加速はどうですか？

Aspose.OCR は `OcrEngine` の設定で GPU をサポートしていますが、バッチプロセッサの `MaxDegreeOfParallelism` が依然として並列度の主要な調整項目です。対応 GPU がある場合は、`OcrBatchProcessor` を作成する前にエンジン設定で有効にしてください。

### 非常に大きなフォルダー（数万ファイル）を扱うには？

- `MaxDegreeOfParallelism` を慎重に増やす；スレッドが多すぎるとメモリが枯渇します。
- 整理のために専用の出力フォルダーを使用する。
- メモリ肥大化を防ぐため、定期的にログをディスクにフラッシュする。

## 高品質 OCR のプロティップス

- **DPI Matters**: 300 DPI 以上の画像は最高の精度を提供します。スキャンがそれ以下の場合は、処理前にバイキュービックフィルターで拡大することを検討してください。
- **Noise Reduction**: ソース画像がざらついている場合は `Preprocessing.NoiseRemoval` を有効にしてください。
- **File Naming**: ファイル名は短く英数字のみで保ちましょう。特殊文字はコールバックのパスロジックを混乱させる可能性があります。
- **Logging**: 本番環境では `Console.WriteLine` を適切なロガー（例: `Serilog`）に置き換えてください。

## 次のステップ

これで **how to batch OCR** を習得したので、次のことを検討できるでしょう：

- **Extract text from images** を実行し、出力を検索インデックス（例: Elasticsearch）に投入して全文検索を行う。
- **Convert images to txt** した後、自然言語処理（NLP）を実行して文書を自動分類する。
- **different language packs** や業界固有用語のカスタム辞書を試す。

ポストプロセッシングに興味がある場合は、「正規表現で OCR 出力を解析する」や「OCR 結果を SQL データベースに保存する」などのチュートリアルをご覧ください。

---

**Happy coding!** 並列度を調整したり、前処理ステップを追加したり、継続的監視のために Windows サービスとしてラップしたり、自由にカスタマイズしてください。Aspose.OCR のバッチ機能と .NET の工夫を組み合わせれば、可能性は無限です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}