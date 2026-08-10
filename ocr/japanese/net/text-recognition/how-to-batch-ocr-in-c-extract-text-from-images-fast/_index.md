---
category: general
date: 2026-03-21
description: C#でバッチOCRを簡単に行う方法—画像からテキストを抽出し、画像をテキストに変換し、言語設定でOCR結果をテキストとして保存する方法を学びましょう。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: ja
og_description: C#でバッチOCRを行う方法は、画像からテキストを抽出し、画像をテキストに変換し、OCR言語を簡単に設定しながらOCRをテキストとして保存できます。
og_title: C#でバッチOCRを実行する方法 – クイックガイド
tags:
- OCR
- C#
- Aspose
title: C#でバッチOCRを行う方法 – 画像からテキストを高速抽出
url: /ja/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でバッチOCRを実行する方法 – 画像からテキストを高速に抽出

フォルダーに何百枚もの画像があるときに **バッチOCRをどうやって行うか** と疑問に思ったことはありませんか？ 開発者は、各ファイルごとにループを書かずに画像からテキストを抽出する方法を常に尋ねています。 良いニュースは、Aspose.OCR が数行の C# で **画像をテキストに変換** する、クリーンで並列処理対応の方法を提供してくれることです。

このチュートリアルでは、**OCRをテキストとして保存** する方法、適切な言語の選択、そして高速化のために並列処理を強化する方法を示す、完全で実行可能なサンプルを順に解説します。 最後まで読むと、任意の .NET プロジェクトに組み込める自己完結型のソリューションが手に入ります。

## 必要なもの

- .NET 6 以上（API は .NET Core と .NET Framework でも動作します）
- Aspose.OCR for .NET（NuGet パッケージ `Aspose.OCR`）
- 処理したい画像が入ったフォルダー（PNG、JPEG、TIFF など）
- 並列プログラミングへのちょっとした興味（任意ですが役立ちます）

余計なサービスやクラウドキーは不要です—ローカルで実行できる純粋な C# コードだけです。

---

![how to batch OCR workflow](placeholder.png){alt="how to batch OCR workflow diagram"}

## 手順 1: プロジェクトのセットアップと Aspose.OCR のインストール

まずはコンソール アプリを作成（または既存のものを再利用）し、Aspose.OCR パッケージを追加します：

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio を使用している場合は、プロジェクトを右クリック → *NuGet パッケージの管理* → *Aspose.OCR* を検索し、最新の安定版をインストールしてください。

これにより、`OcrBatchProcessor`、`OcrEngineSettings`、および列挙型 `Language` が使用可能になります。

## 手順 2: 入力フォルダーと出力フォルダーの定義

バッチプロセッサは、ソース画像が格納されている場所と、抽出したテキストファイルを書き込む場所を知る必要があります。 パスは絶対パスでもプロジェクトルートからの相対パスでも構いませんが、コードを実行する前にフォルダーが存在することを確認してください。

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **重要な理由:** 出力フォルダーが存在しないと、プロセッサは例外をスローし、バッチ全体が中断されます。事前にフォルダーを作成しておくことで、スムーズに実行できます。

## 手順 3: OCR 設定の構成（言語を含む）

ここでバッチ全体の **OCR 言語を設定** します。Aspose.OCR は数十の言語をサポートしており、デフォルトは英語ですが、`Language` 列挙型の値を変更することでフランス語、スペイン語などに切り替えることができます。

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

画像ごとに異なる言語を処理する必要がある場合は、後でファイル単位でこの設定を上書きできます—詳細は後述します。

## 手順 4: `OcrBatchProcessor` オブジェクトの構築

これで全てを結びつけます。`OcrBatchProcessor` では、入力フォルダー、出力フォルダー、出力形式、並列オプション、そして先ほど作成した共有設定を指定できます。

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **なぜ並列処理か？**  数十枚から数百枚の画像がある場合、1 つずつ処理すると非常に遅くなります。`MaxDegreeOfParallelism` を 4 に設定すると、ランタイムは 4 つの CPU コアを同時に使用でき、典型的なワークステーションでの総処理時間を大幅に短縮します。

## 手順 5: バッチ操作の実行

プロセッサの設定が完了したら、実行は単一のメソッド呼び出しです。ライブラリがファイル列挙、OCR、結果の書き込みを自動的に処理します。

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

コンソールに *“Batch OCR completed.”* と表示されたら、`BatchResults` 内の元画像ごとに `.txt` ファイルが作成されています。各テキストファイルには、元画像から抽出された生の文字列が含まれており、下流処理のために **画像からテキストを抽出** するのにまさに必要なものです。

### 期待される出力

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

それらのファイルのいずれかを開くと、画像内容のプレーンテキスト表現が確認できます。

## 手順 6: 結果の検証（オプション）

OCR が期待通りに動作したかを確認するために、数ファイルを二重チェックする習慣は有益です。簡単な方法は、生成された各ファイルの最初の行を読み取り、コンソールに出力することです：

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

文字化けが見られる場合は、`Language` 設定を変更するか、画像品質（例：DPI を上げる、グレースケールに変換）を調整してください。

## 高度なバリエーションとエッジケース

### 1. ファイルごとの言語上書き

バッチに多言語ドキュメントが混在することがあります。その場合、各画像名を調べてその場で言語を割り当てることができます：

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. 異なる出力形式

プレーンテキストではなく検索可能な PDF が必要な場合は、`OutputFormat` を変更します：

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

これにより、PDF コンテナ内で **画像をテキストに変換** し、元のレイアウトを保持します。

### 3. 大きな画像の処理

非常に高解像度の画像はメモリを大量に消費します。プロセスを軽量に保つために、画像のダウンサンプリングを有効にします：

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. エラーロギング

プロセッサは読み取れないファイルに対して例外をスローします。`Execute` を try/catch でラップし、問題のあるファイル名をログに記録してください：

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## 完全な動作例

全てをまとめると、以下がコピー＆ペーストで使用できる完全なプログラムです：

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

`Program.cs` として保存し、プロジェクトをビルドして `dotnet run` を実行してください。コンソールに完了を示す出力が表示され、続いて抽出されたテキストの簡単なプレビューが表示されます。

---

## 結論

ここでは、Aspose.OCR を使用して C# で **バッチOCRを実行** する方法を解説し、**画像からテキストを抽出**、**画像をテキストに変換**、そして **OCR をテキストとして保存** しながら、コンテンツに合わせて **OCR 言語を設定** する方法を示しました。サンプルは完全に機能し、速度向上のための並列処理を含み、ファイルごとの言語上書きや PDF 出力といった高度なシナリオ向けのフックも提供しています。

次のステップに進む準備はできましたか？`OcrOutputFormat.PlainText` を `SearchablePdf` に置き換えて、検索可能な PDF の生成がいかに簡単かを試してみてください。また、`MaxDegreeOfParallelism` の異なる値を試して、マルチコアマシンで可能な限りミリ秒単位の性能向上を図ってみましょう。

問題が発生した場合は、フォルダー パスを再確認し、画像が読み取れることを確認し、言語列挙型が画像内のテキストと一致しているかを検証してください。コーディングを楽しんで、OCR バッチが迅速かつ正確に動作しますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}