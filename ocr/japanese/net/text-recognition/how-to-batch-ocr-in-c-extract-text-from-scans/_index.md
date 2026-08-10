---
category: general
date: 2026-05-06
description: C#でバッチOCRを実行し、Aspose OCR Batchを使用してスキャンからテキストを迅速に抽出する方法を学びましょう。コード、ヒント、エッジケースの対処法を含む、完全なステップバイステップガイドをご覧ください。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ja
og_description: C#でバッチOCRを行う方法は？このガイドでは、Aspose OCR、GPUサポート、並列処理を使用して、スキャンからテキストを効率的に抽出する方法を示します。
og_title: C#でバッチOCRを行う方法 – スキャンからテキストを抽出
tags:
- C#
- OCR
- Aspose
title: C#でバッチOCRを行う方法 – スキャンからテキストを抽出
url: /ja/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でバッチOCRを行う方法 – スキャンからテキストを抽出

スキャンした PDF や JPEG が大量に入ったフォルダーがあるときに **バッチOCRのやり方** を考えたことはありませんか？ 画像の山を前に「テキストをもっと速く取り出す方法があるはずだ」と思っているのはあなただけではありません。このチュートリアルでは、**スキャンからテキストを抽出** できる実用的なソリューションを紹介すると同時に、GPU 加速と並列処理で処理速度を向上させる方法を解説します。

ポイントはこれです：1 ファイルずつ OCR を実行するのは時間がかかります。特に数十〜数百ページを扱う場合はなおさらです。このガイドが終わる頃には、ディレクトリ全体をワンコマンドで処理できる C# コンソール アプリが完成し、インデックス作成や検索、次のステップにすぐ使えるクリーンなテキスト ファイルが手に入ります。

## 前提条件

以下を事前に用意してください。

- **.NET 6.0 以降**（コードは最新の C# 機能を使用しています）。
- **Aspose.OCR のライセンス**（無料トライアルでもテストは可能です）。
- **GPU 対応マシン**（`UseGpu` を有効にしたい場合）。GPU が無い場合は自動的に CPU にフォールバックします。
- **C# コンソール アプリケーション** の基本的な知識。

外部サービスや隠し設定ファイルは不要です。SDK と画像フォルダーだけで完結します。

## Step 1: Install the Aspose.OCR NuGet Package

まず、Aspose OCR ライブラリをプロジェクトに追加します。ソリューション フォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio を使用している場合は、NuGet パッケージ マネージャー UI からもパッケージを追加できます。

## Step 2: Create the Console Application Skeleton

バッチ プロセッサをホストする最小限のコンソール アプリを作成します。`Program.cs` という名前の新しいファイルを作成し、以下の雛形を貼り付けてください。

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

なぜロジックを `Main` 内にラップするのか？ コンソール アプリは `Console.WriteLine` で即座にフィードバックを得られるため、**バッチ OCR** ジョブが正しく完了したかを手軽に確認できます。

## Step 3: Configure the OcrBatchProcessor

これが解決策の核心です。`OcrBatchProcessor` をインスタンス化し、入力フォルダーと出力先を指定し、いくつかのパフォーマンス設定を調整します。

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Why these settings matter

| Setting | What it does | When you might change it |
|---------|--------------|--------------------------|
| `InputFolder` | 処理したいスキャン画像へのパス。 | ポータビリティを重視する場合は相対パスを使用。 |
| `OutputFolder` | 各画像から抽出したテキストが `.txt` ファイルとして保存される場所。 | 中央保存が必要な場合はネットワーク共有先を指定。 |
| `Language` | OCR の言語モデル。ここでは多言語対応の例としてスペイン語を使用。 | `OcrLanguage.English` など、サポートされている言語に切り替え。 |
| `UseGpu` | 重い行列計算を GPU にオフロードするか。 | GPU が無いヘッドレスサーバーでは `false` に設定。 |
| `MaxDegreeOfParallelism` | 同時に処理する画像数を制御。 | CPU が低スペックなマシンではスロットリング防止のために減らす。 |

## Step 4: Execute the Batch Operation with Error Handling

バッチの実行は `Execute()` を呼び出すだけですが、例外が発生した場合に分かりやすいメッセージを出すために try‑catch でラップします（例：フォルダーが見つからない、画像形式に未対応など）。

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

プロセッサが完了するとコンソールに **Batch completed.** と表示され、`OcrResults` フォルダー内に元画像と同名の `.txt` ファイルが作成されます。ファイル名が元画像と一致しているので、スキャン元との対応付けが簡単です。

## Step 5: Verify the Output – What to Expect

プログラム実行後、`YOUR_DIRECTORY/OcrResults` 内の任意のファイルを開いてください。対応する画像から抽出されたプレーンテキストが表示されます。例：

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

出力が文字化けしている場合は、`Language` がスキャン画像の言語と合っているか再確認してください。Aspose OCR は 100 以上の言語に対応しているので、`OcrLanguage.Spanish` を必要な言語に置き換えるだけで対応可能です。

## Handling Edge Cases and Common Pitfalls

### 1. GPU Not Available

GPU が搭載されていない環境では `UseGpu = true` は自動的に CPU モードにフォールバックしますが、速度向上は得られません。明示的に GPU の有無を判定したい場合は次のようにします。

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Large Files Exceeding Memory

巨大な TIFF や PDF を扱う場合は、事前に小さな画像に分割することを検討してください。Aspose OCR はマルチページ PDF を処理できますが、ページ数が増えるほどメモリ消費が大きくなります。`Aspose.Imaging` を使った前処理で文書を適切なサイズに分割すると効果的です。

### 3. Non‑Image Files in the Input Folder

バッチプロセッサは解析できないファイルを自動的に無視しますが、フォルダーはできるだけクリーンに保つのがベストです。拡張子でフィルタリングすることも可能です。

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(注: `FileFilter` は仮想的なプロパティです。実際の API が存在すればそれを使用してください。)*

## Full Working Example

以下に、コピー＆ペーストでそのまま使用できる完全版プログラムを示します。`YOUR_DIRECTORY` を実際の絶対パスに置き換えてください。

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Expected Console Output

```
Batch completed.
```

`C:\OcrResults` フォルダーには、`C:\MyScans` 内の各画像に対応する `.txt` ファイルが生成されます。

## Conclusion

これで **C# でバッチOCRを行う方法** と **スキャンからテキストを抽出** する、手動でファイルを開く必要のない堅牢なプロダクション向けソリューションが手に入りました。Aspose のバッチ API、GPU 加速、設定可能な並列処理を活用すれば、数ページから数千ページまでスケールします。

次は何をしますか？以下のアイデアを試してみてください。

- **検索インデックスと統合**（例: Elasticsearch）して抽出テキストを検索可能にする。
- **ポストプロセッシング**（スペルチェックや言語検出など）を追加する。
- **コンソール アプリを Windows Service にラップ**して、ドロップフォルダーの継続監視を実現する。

自由に実験し、並列度を調整したり、言語モデルを入れ替えたりしてください。問題が発生したらコメントで教えてください—楽しい OCR ライフを！ 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}