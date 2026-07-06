---
category: general
date: 2026-03-26
description: C#でバッチOCRを行う方法は、PNGファイルからテキストを抽出することを簡単にします。Aspose OCRを使用したバッチテキスト抽出のためのステップバイステップC#
  OCRチュートリアルをご覧ください。
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: ja
og_description: C#でバッチOCRを行う方法は、PNGファイルからテキストを迅速に抽出できます。このガイドでは、バッチテキスト抽出を含む完全なC#
  OCRチュートリアルをご案内します。
og_title: C#でバッチOCRを行う方法 – PNGからテキストを抽出
tags:
- OCR
- C#
- Aspose
title: C#でバッチOCRを行う方法 – PNGからテキストを抽出
url: /ja/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でバッチ OCR を実行する方法 – PNG からテキストを抽出

**バッチ OCR** で大量のスクリーンショットを個別にプログラムを書かずに処理したいと思ったことはありませんか？ あなたは一人ではありません。多くのプロジェクトで、テキスト抽出が必要な PNG が何十枚もあり、1 枚ずつ処理するのは面倒です。  

良いニュースは、Aspose OCR を使えば、すべての画像を並列に処理する小さな C# コンソール アプリを作成でき、**バッチ テキスト抽出** が高速に行え、結果もすっきりします。このガイドでは、完全な **c# ocr tutorial** を順に解説し、各要素がなぜ必要かを説明し、出力例を示します。

この記事を読み終えると、以下ができるようになります。

* PNG ファイル（またはサポートされている画像）を一括で読み込む。  
* 共有 `OcrEngine` を設定し、バッチ全体で設定を統一する。  
* 最大 4 つの並列ワーカーで認識キューを実行する。  
* 各ページの認識テキストを取得し、コンソールに出力する。

魔法はありません。すぐにソリューションに組み込める実用的なコードです。

## 必要なもの

作業を始める前に、以下を用意してください。

* .NET 6 SDK（または最近の .NET バージョン）。  
* 有効な Aspose OCR ライセンス、または一時的な評価キー。  
* 処理したい PNG ファイルが入ったフォルダー。  
* Visual Studio 2022 またはお好みのエディタ。

以上です。`Aspose.OCR` と標準の `System.Collections.Generic` 以外に追加の NuGet パッケージは不要です。

## バッチ OCR の設定 – プロジェクトの作成

まずは新しいコンソール プロジェクトを作成し、Aspose OCR ライブラリを導入します。

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

復元が完了したら **Program.cs**（または新規ファイル）を開き、通常の `using` ディレクティブを追加します。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

このシンプルな雛形で、後で使用する `OcrEngine`、`RecognitionQueue`、ヘルパークラスにアクセスできるようになります。

## PNG からテキストを抽出 – 画像リストの準備

次に、プログラムに **どの PNG を OCR するか** を指示する必要があります。最もシンプルなのは、絶対パスまたは相対パスを保持する `List<string>` を作成する方法です。

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

`YOUR_DIRECTORY` を実際のフォルダー パスに置き換えてください。動的に取得したい場合は `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` を使ってリストに流し込むこともできます。重要なのは、**PNG からテキストを抽出** するには正しいファイル名をキューに渡すだけという点です。

![バッチ OCR ワークフロー](https://example.com/placeholder.png "PNG ファイルのコレクションに対してバッチ OCR を実行するフローを示す図")

*画像代替テキスト: バッチ OCR ワークフロー図*

## C# OCR チュートリアル – 認識キューの設定

バッチ処理の中心は `RecognitionQueue` です。これは各画像を共有 `OcrEngine` に渡すコンベアベルトのようなものです。エンジンを共有することでメモリ使用量を抑え、すべてのページで同一設定が保証されます。

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

`MaxDegreeOfParallelism` を 4 に設定する理由は何でしょうか？ 一般的なクアッドコア ラップトップでは、OS を飢餓状態にせずに最大スループットが得られるからです。サーバーでコア数が多い場合は、適宜数値を上げてください。

### プロのコツ

カスタム言語パックや DPI 設定、ROI（関心領域）クロッピングが必要な場合は、画像をキューに入れる前に **共有 Engine** で一度だけ設定します。例:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

以降の認識は自動的にこれらのオプションを継承します――**OCR パイプラインを一貫させる** 本質がここにあります。

## バッチ テキスト抽出 – 画像をキューに入れて実行

キューの準備ができたら、次は各画像をキューにプッシュします。`Enqueue` メソッドは `OcrImage` インスタンスを受け取り、ファイル パスから作成します。

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

すべてのファイルがキューに入ったら、処理を開始します。

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` はすべての画像が完了するまでブロックし、入力順に対応したリストを返します。これにより、ページ 1 の結果はインデックス 0、ページ 2 はインデックス 1 といった具合に、元ファイルへ結果をマッピングしやすくなります。

## OCR の作成方法 – 結果の表示

最後に、認識テキストをコンソールに出力します。ここで **バッチ テキスト抽出** の効果を実感できます。

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

プログラムを実行 (`dotnet run`) すると、次のような出力が得られるはずです。

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

画像が破損しているなどで失敗した場合、該当する `OcrResult` の `Text` プロパティは空になり、`ocrResults[i].Exception` で診断情報を確認できます。

## OCR の作成方法 – ヒント、エッジケース、ベストプラクティス

### 大規模バッチの取り扱い

数百枚の PNG を処理すると、すべての `OcrResult` オブジェクトを保持するとメモリを圧迫します。そのような場合は、結果が得られ次第すぐにファイルやデータベースへストリーム出力してください。

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### PNG 以外のフォーマットへの対応

Aspose OCR は JPEG、BMP、TIFF も標準でサポートしています。リストの拡張子を変更するか、ワイルドカード検索を利用してください。同じ **c# ocr tutorial** 手順で対応可能です――コード変更は不要です。

### 空白ページのスキップ

スキャンした PDF に空白ページが混在する場合、結果をフィルタリングできます。

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### ライセンスに関する注意点

評価版は各ページに透かしを付与します。製品版で使用する際は、`Main` の冒頭でライセンス ファイルを埋め込んでください。

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### 並列度の調整

`MaxDegreeOfParallelism` の既定値は `Environment.ProcessorCount` です。CPU 使用率やメモリ圧迫が顕著な場合は値を下げ、逆にコア数の多いクラウド VM では上げてハードウェアを最大限に活用してください。

## まとめ

これで C# における **バッチ OCR** ソリューションが完成しました。**PNG からテキストを抽出** し、並列処理で高速に実行し、整然とした結果を得られます。単一の `OcrEngine` を共有することで、**OCR パイプラインの作成方法** を学び、メモリ効率と保守性を両立させました。この **c# ocr tutorial** は、数百枚の画像に対して **バッチ テキスト抽出** を拡張する方法も示しています。

---

### 次のステップは？

* 言語自動検出 (`Engine.Language = Language.AutoDetect`) を試す。  
* 出力形式を JSON や CSV に変更し、下流の分析に活用する。  
* バッチ OCR を PDF‑to‑image 変換と組み合わせ、スキャン文書全体を処理する。

並列度を調整したり、独自の画像ソースに差し替えたり、結果を検索インデックスに流し込んだりして自由にカスタマイズしてください。**C# でバッチ OCR をマスターすれば、可能性は無限大です。**

Happy coding, and may your OCR runs be fast and error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}