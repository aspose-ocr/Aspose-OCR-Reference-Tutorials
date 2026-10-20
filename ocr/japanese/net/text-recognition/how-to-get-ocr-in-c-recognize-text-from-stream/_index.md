---
category: general
date: 2026-03-05
description: Aspose.OCR を使用して OCR を迅速に取得し、ストリームからテキストを認識する簡単な手順をご紹介します。完全な C# コードと画像データをストリーミングするためのヒントをご確認ください。
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: ja
og_description: C#でOCRを取得し、Aspose.OCRを使用してストリームからテキストを認識する方法。すぐに実行できるソリューションのステップバイステップチュートリアルをご覧ください。
og_title: C#でOCRを取得する方法 – 完全ストリーム認識ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを取得する方法 – ストリームからテキストを認識する
url: /ja/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを取得する方法 – ストリームからテキストを認識する

画像全体をディスクに保存せずに .NET アプリで **OCR を取得する** 方法を考えたことがありますか？ あなたは一人ではありません。多くの開発者が **ストリームからテキストを認識する** 必要があります—たとえばネットワーク経由で届く画像やカメラフィード、クラウドストレージ API からの画像を処理する場合です。  

このチュートリアルでは、まさにそれを示す完全な実行可能サンプルを順を追って解説します。最後まで読むと、Aspose OCR エンジンを作成し、画像チャンクをストリーミングで供給し、抽出したテキストをコンソールに出力する、自己完結型の C# プログラムが手に入ります。謎の外部ツールは不要、明快なコードと実用的なヒントだけです。

## 学習できること

- Aspose.OCR ライブラリのインストールとライセンスの設定方法。
- `AppendChunk` メソッドを使用して画像データを断片ごとに供給する方法。
- 認識サイクルの開始と終了 (`BeginRecognize` / `EndRecognize`) の方法。
- 不完全なチャンクやライセンスエラーなど、一般的なエッジケースの処理方法。
- 出力結果の確認方法。

### 前提条件

- .NET 6.0 以降（コードは .NET Core および .NET Framework でも動作します）。
- 有効な Aspose OCR ライセンス ファイル (`Aspose.OCR.lic`)。Aspose のウェブサイトから無料トライアルを取得できます。
- C# と `async`/`await` に基本的に慣れていること（非同期ストリームから読み取る場合）。例では分かりやすさのために同期スタブを使用しています。

> **Why this matters:** ストリーミング OCR を利用すると、メモリ使用量を抑えつつ大きな画像や連続ビデオフィードのレイテンシを低減できます。リアルタイム文書スキャナ、モバイルアプリ、サーバー側処理パイプラインでよく見られるパターンです。

## 手順 1: プロジェクトのセットアップと Aspose.OCR の追加

まず、新しいコンソールプロジェクトを作成し、Aspose.OCR NuGet パッケージを追加します。

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio を使用している場合は、プロジェクトを右クリック → *Manage NuGet Packages* → “Aspose.OCR” を検索して最新の安定版をインストールします。

次に、ライセンス ファイルをプロジェクトのルートに追加し、**Copy to Output Directory** プロパティを **Copy always** に設定します。これにより、実行時にファイルが利用可能になります。

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## 手順 2: OCR エンジンの初期化とライセンスの適用

エンジンの作成は簡単ですが、ライセンスの適用は **認識呼び出しの前に必ず** 行う必要があります。さもなければトライアルモードの制限に引っかかります。

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **Why we do this:** ライセンスを早期に設定することで、以降のすべての API 呼び出しがフル機能モードで実行され、“evaluation version” の透かしが表示されるのを防げます。

## 手順 3: ストリーミング ソースのシミュレーション

実際のアプリケーションでは `NetworkStream`、`FileStream`、またはカメラ SDK から読み取ります。デモ用に、JPEG 画像チャンクを表すバイト配列を返すヘルパーでストリームを模倣します。

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **Edge case note:** 多数の小さなチャンクを受け取る場合、認識を終了する前に `engine.Image.AppendChunk(chunk)` を繰り返し呼び出すことができます。エンジンは内部でバッファリングし、処理開始に十分なデータが揃うまで待ちます。

## 手順 4: 画像データを断片ごとに供給して OCR を実行する

ここまでの要素を組み合わせます。手順は次の通りです。

1. `BeginRecognize()` – エンジンにデータ供給を開始することを通知します。  
2. `AppendChunk()` – 各バイト配列を追加します（多数のチャンクをループで処理可能）。  
3. `EndRecognize()` – 最後のチャンクが送信されたことを示し、実際の認識をトリガーします。

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## 手順 5: `Main` で全体をまとめる

以下は、すべてを配線し、認識結果をコンソールに出力し、エンジンをきれいに破棄する完全な `Main` メソッドです。

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### 期待される出力

`sample.jpg` に “Hello, World!” というフレーズが含まれていれば、次のように表示されます。

```
=== Recognized Text ===
Hello, World!
```

画像がぼやけている、またはチャンクが不完全な場合、出力は空になるか文字化けすることがあります。最後のチャンクが確実に送信されているかどうかの適切なチャンク処理が重要です。

## 複数チャンクの処理（上級）

本格的なストリーミング データを扱う場合、たくさんの小さなピースが届くことが想定されます。以下のパターンは、ソースが終了するまでループする方法を示しています。

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **Why this helps:** `NetworkStream` や `FileStream` から直接ストリーミングすることで、画像全体をメモリに読み込む必要がなくなります。特に大容量 PDF や高解像度写真の処理に有効です。

## よくある落とし穴と回避策

| 落とし穴 | 症状 | 対策 |
|---------|------|------|
| ライセンスが見つからない | `SetLicense` が `FileNotFoundException` をスロー | パスを確認し、*Copy to Output Directory* を *Copy always* に設定 |
| 結果が空 | テキストが出力されない | `BeginRecognize` を **AppendChunk の前に**、`EndRecognize` を **最後のチャンクの後に** 呼び出したか確認 |
| メモリリーク | 多数の OCR 呼び出し後にアプリが遅くなる | 使用後に `OcrEngine` を破棄するか、適切に `Dispose` した単一インスタンスを再利用 |
| チャンクが破損 | 文字化け | チャンクサイズを検証；JPEG/PNG の場合、先頭バイトが `0xFF 0xD8` または `0x89 0x50` で始まることを確認 |

## ボーナス: 非同期ストリームの使用

ソースが `HttpClient` のレスポンスストリームの場合、ループを `await` 読み取りに適応できます。

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

これにより、デスクトップやモバイルアプリの UI が応答し続け、サーバー側のスループットも最大化できます。

## 結論

これで **C# で OCR を取得するための完全な自己完結型ソリューション** と **ストリームからテキストを認識する方法** が Aspose.OCR を使って実装できました。チュートリアルでは、ライセンス取得と初期化から画像チャンクの供給、エッジケースの処理、さらには非同期バリアントまで網羅しました。  

実際に試してみてください—`sample.jpg` をライブカメラ フィード、クラウド保存画像、またはマルチパート HTTP アップロードに置き換えてみましょう。慣れてきたら、言語パック、カスタム前処理、複数ストリームのバッチ処理といった高度な機能にも挑戦してください。

**次のステップ:**  
- 各ページを画像に変換してから PDF に OCR を適用してみる。  
- `engine.Config` を使って特定フォント向けに精度を向上させる実験を行う。  
- Azure Functions や AWS Lambda と組み合わせて、サーバーレスのテキスト抽出パイプラインを構築する。

Happy coding, and may your streams always be crisp and your OCR results flawless!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}