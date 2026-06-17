---
category: general
date: 2026-03-23
description: C#でAspose OCRを使用して画像からテキストを抽出し、リアルタイムフィードバック用のコンソールロガーの追加方法を学ぶ。
draft: false
keywords:
- extract text from image
- add console logger
language: ja
og_description: Aspose OCRで画像からテキストを抽出し、コンソールロガーを追加してプロセスを監視します。ステップバイステップのC#チュートリアル。
og_title: C#で画像からテキストを抽出する – 完全プログラミングガイド
tags:
- OCR
- C#
- logging
title: C#で画像からテキストを抽出する – 完全ガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出する – 完全ガイド

画像からテキストを**迅速かつ確実に抽出**したいですか？Aspose OCR を使えば、C# の数行でそれが実現できます。さらに、**コンソールロガーを追加**する方法も紹介し、OCR エンジンの進行状況をターミナルに直接表示できるようにします。

スキャンしたレシートや手書きのメモ、あるいは PNG として保存された PDF ページがあるとします。重い UI を開かずに生の文字列が欲しいですよね。このチュートリアルでは、.NET 6+ と最新の Aspose OCR ライブラリで動作する、完全なコピーペースト可能なソリューションをステップバイステップで解説します。

このガイドの最後までに、以下ができるようになります：

* 画像ファイルを読み込み、OCR を実行して **画像からテキストを抽出** する。  
* Aspose AI にコンソールロガーをフックし、ライブラリが内部で何をしているかを確認できる。  
* 組み込みのスペルチェックポストプロセッサを適用して、OCR の誤認識を修正できる。  

> **Prerequisites** – 動作する .NET 開発環境（Visual Studio 2022、VS Code、または Rider）、.NET 6 SDK 以上、そして Aspose OCR ライセンス（または無料トライアル）。他のサードパーティパッケージは不要です。

## 必要なもの

| 項目 | 重要性 |
|------|--------|
| **Aspose.OCR** NuGet パッケージ | 画像を実際に読み取る `OcrEngine` クラスを提供します。 |
| **Aspose.OCR.AI** NuGet パッケージ | `AsposeAI` ポストプロセッサフレームワーク（スペルチェックを含む）を提供します。 |
| **Microsoft.Extensions.Logging**（オプション） | **コンソールロガーを追加**するステップで使用する `ILogger` インターフェイスを提供します。 |
| **入力画像** (`input.png`) | ここから **画像からテキストを抽出** します。 |

ターミナルからパッケージをインストールできます:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## ステップ 1 – Aspose OCR で画像からテキストを抽出

最初に画像を OCR エンジンに渡します。このブロックが重い処理を行い、まだ誤字が含まれる可能性のある生の文字列を返します。

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**この仕組みの理由:** `OcrEngine` は、二値化や傾き補正などの低レベル画像前処理をすべて抽象化します。`Recognize()` が `true` を返すと、`Text` プロパティにはすでに最良の推測文字列が格納されています。  

> **ヒント:** 画像が大きい場合、エンジンに渡す前に長辺を ≤ 2000 px 以下にリサイズすると、精度を損なうことなく処理速度が向上します。

## ステップ 2 – リアルタイムインサイトのためにコンソールロガーを追加

ここで **コンソールロガーを追加** します。ロギングはデバッグだけでなく、モデルのダウンロードや AI プロセッサのステップ、ライブラリが出す警告などを可視化してくれます。

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

このロガーを Aspose AI に組み込むことができます:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**表示される内容:** スペルチェックモデルが自動ダウンロードされると、コンソールに次のような行が出力されます:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

これが **コンソールロガーを追加** した利点です – バックグラウンド操作が成功したかどうかを疑う必要がなくなります。

## ステップ 3 – スペルチェックポストプロセッサの設定と登録

Aspose AI には、一般的な OCR エラー（例: “rec0gn1ze” → “recognize”）を修正する便利なスペルチェックポストプロセッサが同梱されています。これを設定し、オプションでモデルの保存先をライブラリに指示し、最後に登録します。

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**カスタムパスが必要になる理由:** CI/CD パイプラインでは、モデルを既知のディレクトリにキャッシュして再ダウンロードを防ぎたくなることがよくあります。`AllowAutoDownload` フラグは、コードを初めて実行したときにモデルが取得されることを保証します。

## ステップ 4 – OCR 結果にポストプロセッサを実行

OCR テキストを取得し、スペルチェックプロセッサの準備ができたら、生の文字列を `AsposeAI` に渡します。エンジンがモデルを実行し、プロセッサは内部に修正済みテキストを保存します。

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

この呼び出しの後、`spellProcessor` は `RecognitionResult` オブジェクトのコレクションを保持し、各オブジェクトの `RecognitionText` プロパティにクリーンアップされたテキストが格納されます。

## ステップ 5 – 修正済みテキストの取得と表示

最後に、プロセッサから修正済み文字列を取得して出力します。ここで OCR と **コンソールロガーを追加** ワークフローの両方の効果を実感できます。

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**期待される出力**（画像に “Aspose OCR demo” というフレーズが含まれ、いくつか OCR の誤りがあると仮定）:

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

ロガーがモデルの準備完了を通知し、修正された行がきれいに表示されていることに注目してください。

## ステップ 6 – リソースのクリーンアップ

`AsposeAI` と `OcrEngine` はどちらも `IDisposable` を実装しています。Dispose することでネイティブメモリとファイルハンドルが解放され、長時間稼働するサービスでは特に重要です。

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## 完全動作サンプル

以下は、`dotnet new console` で作成した新しいコンソールプロジェクトにコピー＆ペーストできる完全なプログラムです。`"YOUR_DIRECTORY"` を実際のフォルダーに置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}