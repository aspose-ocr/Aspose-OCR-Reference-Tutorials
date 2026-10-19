---
category: general
date: 2026-03-07
description: C# を使用して PNG ファイルからテキストを抽出します。画像をテキストに変換する方法と、スキャンした画像からテキストを素早く読み取る方法を学びましょう。
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: ja
og_description: C# を使用して PNG ファイルからテキストを抽出します。このガイドでは、画像をテキストに変換する方法と、Aspose OCR を使用してスキャン画像からテキストを読み取る方法を示します。
og_title: C#でPNGからテキストを抽出する – 完全OCRガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でPNGからテキストを抽出する – 完全OCRガイド
url: /ja/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG からテキストを抽出する C# 完全 OCR ガイド

**PNG** ファイルからテキストを抽出したいけど、どこから始めればいいかわからない…という経験はありませんか？ 開発者の多くが、スキャンした画像やスクリーンショットを検索可能なテキストに変換しようとしたときに壁にぶつかります。 良いニュースは、数行の C# と Aspose OCR さえあれば、どんな PNG でもすぐに編集可能な文字列に変換できるということです。

このチュートリアルでは、ディスク上の PNG を見つけるところから、並列に OCR タスクを起動し、各結果のプレビューを整然と表示するまでの全工程を解説します。 最後まで読めば、**C# で画像をテキストに変換**する方法が分かり、**スキャン画像からテキストを読む**作業を効率的に行えるようになり、**画像上で OCR を実行**するベストプラクティスも把握できます。

## 必要な環境

- .NET 6.0 以上（コードは .NET Core や .NET Framework でも動作します）  
- Aspose.OCR NuGet パッケージ (`Install-Package Aspose.OCR`)  
- 処理したい *.png* ファイルが入ったフォルダー  
- お好みの IDE（Visual Studio、VS Code、Rider など）

追加設定は不要です。ライブラリには PNG、JPEG、TIFF などをデコードするために必要なものがすべて同梱されています。

## 手順 1: すべての PNG ファイルを取得 – 「PNG からテキストを抽出」開始

まず OCR を実行したい PNG をすべて見つけます。`Directory.GetFiles` を使えば手軽で確実です。

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*重要ポイント:* ディレクトリを一度だけ走査すれば、以降のパイプラインがシンプルになり、早期に「出力がない」状態を防げます。

## 手順 2: 並列 OCR タスクを起動 – 効率的に **画像上で OCR を実行**

数ファイルなら順次実行でも問題ありませんが、実務では数十〜数百の画像を扱うことが多いです。画像ごとに `Task` を立ち上げることで、CPU を有効活用しつつライブラリの重い処理を並列化できます。

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*プロ tip:* `Task.Run` は作業をスレッドプールに委譲するため、UI がある場合でもレスポンスが保たれます。サーバー側でも同様にコア数に応じてスケールします。

## 手順 3: すべてのタスクを待機 – 結果を集める

ここで各 OCR 処理の完了を待ちます。`Task.WhenAll` は元のファイル順と同じ配列を返すので、結果とファイル名を簡単に対応付けられます。

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*エッジケース:* 1 つでも例外（破損ファイルや未対応フォーマット）が発生すると `WhenAll` 全体が例外をスローします。内部の `Task.Run` を try/catch で囲み、空文字列や診断メッセージを返すようにすればフォールトトレラントにできます。

## 手順 4: プレビューを表示 – **C# で画像をテキストに変換**した結果を確認

簡易プレビューで OCR が正しく動作したかを確認してから、結果を永続化すると安心です。

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

典型的なコンソール出力例:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

プレビューが文字化けしている場合は、画像品質を再確認するか、前処理（二値化など）を検討してください。ほとんどのクリアな PNG では Aspose OCR が最初の試行で正しく認識します。

## 任意: 結果を CSV に保存 – 実務での利用例

多くのプロジェクトでは抽出したテキストを構造化データとして扱う必要があります。以下はファイル名と OCR 結果全文を CSV に書き出す小さなヘルパーです。

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

これで CSV を Excel、Power BI、あるいは **スキャン画像からテキストを読む**ことを前提とした downstream システムにインポートできます。

## FAQ

**PNG が巨大（5 MB 超）だったらどうする？**  
Aspose OCR は自動で大きな画像をダウンサンプリングしてメモリ使用量を抑えますが、`engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` のように幅を 2000 px にリサイズすればアスペクト比を保ったままサイズ上限を設定できます。

**Linux でも動かせる？**  
はい。Aspose OCR はクロスプラットフォーム対応です。ディストリビューションによっては `libgdiplus` などのネイティブ依存関係をインストールしてください。

**OCR の言語はデフォルトで英語か？**  
その通りです。別の言語が必要な場合は `engine.Language = OcrLanguage.French;`（またはサポートされている enum）を `Recognize()` 呼び出し前に設定します。

**パスワード保護された PDF に PNG が埋め込まれている場合は？**  
まず PDF ページを画像に変換（Aspose PDF など）し、得られた PNG を同じパイプラインに流し込みます。**画像上で OCR を実行**する基本的な流れは変わりません。

## 完全動作サンプル（Async Main）

以下はコンソールプロジェクトにそのまま貼り付けられる自己完結型プログラムです。先ほどの全パーツに加えて、入力フォルダーを検証する小さなヘルパーも含んでいます。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**期待される出力**（2 枚の PNG のサンプル）:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## まとめ

C# を使って **PNG からテキストを抽出**するために必要な手順をすべて網羅しました。ファイルの検索、並列 OCR ジョブの起動、文字列のプレビュー、CSV への永続化まで、このガイドは **C# で画像をテキストに変換**シナリオ向けの実践的パターンを提供します。

次のステップとして、同じパイプラインで JPEG や TIFF を処理したり、別言語の OCR を試したり、結果を検索インデックスに連携させて **スキャン画像からテキストを読む**体験をリアルタイム化してみてください。

エッジケースやパフォーマンスチューニング、ライセンスに関する質問があればコメントや Aspose コミュニティへどうぞ。Happy coding!

![Extract text from PNG example](extract-text-png.png "Aspose OCR を使用した PNG からテキスト抽出")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}