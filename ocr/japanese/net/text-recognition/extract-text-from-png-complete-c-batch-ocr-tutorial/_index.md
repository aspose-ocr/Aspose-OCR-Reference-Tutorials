---
category: general
date: 2026-04-26
description: C#でPNGファイルからテキストを高速に抽出。画像をテキストに変換する方法、PNGファイルの読み取り、画像をループ処理する方法、数分で画像をバッチOCRする方法を学びましょう。
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: ja
og_description: C#でPNGファイルからテキストを高速に抽出します。このガイドでは、画像をテキストに変換する方法、PNGファイルの読み取り、画像のループ処理、バッチOCR画像の実行方法を示します。
og_title: PNGからテキストを抽出 – 完全版C#バッチOCRチュートリアル
tags:
- C#
- OCR
- Aspose
title: PNGからテキストを抽出 – 完全なC#バッチOCRチュートリアル
url: /ja/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG からテキストを抽出 – 完全な C# バッチ OCR チュートリアル

PNG ファイルから**テキストを抽出**する必要があったが、どこから始めればよいか分からなかったことはありませんか？あなた一人ではありません—スクリーンショットのフォルダーで OCR を初めて試すとき、多くの開発者が同じ壁にぶつかります。良いニュースは、数行の C# と Aspose OCR を使うだけで、画像をテキストに変換し、PNG ファイルを読み取り、画像をループ処理し、すべてを一括でバッチ処理できることです。

このチュートリアルでは、すぐに実行できるコンソールアプリを順に解説します。最後まで読むと、ディレクトリ内のすべての PNG からテキストを抽出し、各画像の隣に対応する `.txt` ファイルを作成する、自己完結型のソリューションが手に入ります。余計なスクリプトや手動でのコピーペーストは不要で、純粋にコードだけです。

## 必要なもの

- **.NET 6 SDK** (またはそれ以降の .NET バージョン)。無料で高速、どこでも動作します。
- **Aspose.OCR for .NET** (NuGet パッケージ)。互換性のある GPU があれば GPU 加速が利用でき、無い場合は自動的に CPU にフォールバックします。
- 処理したい **PNG 画像** が入ったフォルダー。  
- テキストエディタまたは IDE—Visual Studio、VS Code、Rider—好きなものを使用してください。

以上です。これらが揃っていれば、すぐに始められます。

![C# バッチ OCR を使用した PNG からテキストを抽出](image.png "PNG からテキストを抽出したデモスクリーンショット")

*画像の代替テキスト: “C# バッチ OCR を使用した PNG からテキストを抽出”*

## ステップ 1 – プロジェクトのセットアップと Aspose.OCR のインストール

まず、新しいコンソールプロジェクトを作成し、Aspose OCR パッケージを導入します。

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

なぜコンソールアプリを使うのでしょうか？バッチジョブの最もシンプルなホストであり、コマンドラインから実行したりタスクランナーでスケジュールしたりできます。後で UI が必要になった場合は、コアロジックをクラスライブラリに移すだけです。

## ステップ 2 – GPU 加速 OCR エンジンの初期化（または CPU フォールバック）

Aspose は `GpuOcrEngine` を提供しており、対応する GPU を自動的に検出します。GPU が見つからない場合は、通常の CPU エンジンに自動で切り替わります—追加のコードは不要です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**プロのコツ:** GPU のないヘッドレスサーバー上で実行する場合は、`GpuOcrEngine` を `OcrEngine` に置き換えるだけで、コードは同じように動作します。

## ステップ 3 – 対象ディレクトリ内の画像をループ処理

画像を**ループ処理**し、PNG ファイルだけを選択する必要があります。`Directory.GetFiles` メソッドが主な処理を行い、空のフォルダーに対する対策も行います。

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

`SearchOption.TopDirectoryOnly` の使用に注目してください。後でサブフォルダーも再帰的に処理したい場合は、`AllDirectories` に切り替えるだけです。その小さな変更で、ツリー全体の画像を**テキストに変換**できるようになります。

## ステップ 4 – OCR を実行し結果を保存

ここからが **バッチ OCR 画像** ワークフローの核心です。各 PNG を読み込み、`Recognize()` を実行し、抽出した文字列を同じベース名の `.txt` ファイルに書き込みます。

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**なぜ try/catch で囲むのか？** 実際の画像バッチには破損したファイルや、珍しいカラープロファイルを使用した PNG が含まれることがあります。例外を捕捉することで、全体の実行がクラッシュするのを防ぎ、残りのファイルの処理を続行できます。

## ステップ 5 – アプリケーションを実行し出力を確認

アプリをビルドして起動します:

```bash
dotnet run
```

以下のようなコンソールログが表示されるはずです:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

生成された `.txt` ファイルのいずれかを開くと、抽出されたテキストが確認できます。ファイルが空の場合は、画像の品質を再確認してください。OCR は明瞭で高コントラストなテキストで最も効果的です。

### クイック検証スクリプト（オプション）

すべての PNG に対応するテキストファイルが作成されたことを確認したい場合は、以下の小さな PowerShell ワンライナーを実行してください:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## 一般的なバリエーションとエッジケース

| Situation | What to Change |
|-----------|----------------|
| **ラテン文字以外の言語**（例: キリル文字） | Set `ocrEngine.Language = Language.Cyrillic;` |
| **大量の画像セット（>10 000 ファイル）** | `Parallel.ForEach` を使用して処理速度を上げますが、GPU メモリ使用量に注意してください。 |
| **元の画像順序を保持する必要がある** | `foreach` の前に `pngFiles` をソートします（`Array.Sort(pngFiles);`）。 |
| **GPU のない CI サーバーで実行する** | GPU 初期化エラーを回避するために `GpuOcrEngine` を `OcrEngine` に置き換えます。 |
| **特定のキーワードを含むファイルだけを処理したい** | `result.Text` を取得した後、ファイルを書き込む前に `result.Text.Contains("Invoice")` でキーワードをチェックします。 |

これらの調整により、**画像をテキストに変換** パイプラインをほぼすべてのシナリオに適応できます。

## 完全なソースコード（コピー＆ペースト可能）

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すると、魔法が起きます。

## 結論

これで、C# を使用して PNG ファイルからテキストを抽出する **完全で本番環境対応の方法** が手に入りました。このチュートリアルでは、プロジェクトのセットアップ、GPU 加速 OCR エンジンの初期化、**画像のループ処理**、**バッチ OCR 画像** の実行と結果をプレーンテキストとして保存するまで、すべてを網羅しました。

次のステップに興味があるなら、以下を試してみてください:

- **画像をテキストに変換** する他のフォーマット（JPG、BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}