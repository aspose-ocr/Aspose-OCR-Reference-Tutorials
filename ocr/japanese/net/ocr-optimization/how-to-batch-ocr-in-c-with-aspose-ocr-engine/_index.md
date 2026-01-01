---
category: general
date: 2026-01-01
description: C#でAspose OCRエンジンを使用したバッチOCRの方法。画像からテキストを認識し、GPUアクセラレーションでTIFFファイルからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: ja
og_description: Aspose OCRエンジンを使用したC#でのバッチOCR方法。このガイドでは、画像からテキストを認識し、TIFFファイルからテキストを効率的に抽出する方法を示します。
og_title: C#でバッチOCRを行う方法 – 完全なAsposeガイド
tags:
- OCR
- C#
- Aspose
- GPU
title: C# と Aspose OCR エンジンでバッチ OCR を行う方法
url: /ja/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR エンジンを使用したバッチ OCR の方法

数十枚のスキャン済みドキュメントがフォルダーに入っているとき、**バッチ OCR をどうやって実行するか** と悩んだことはありませんか？ 同じ壁にぶつかる開発者は多いです。単一画像の認識からコレクション全体の処理へ移行する際に直面します。朗報です。Aspose OCR を使えば、CPU でも GPU 加速でも、簡単に実現できます。

このチュートリアルでは、**画像からテキストを認識**し、**TIFF ファイルからテキストを抽出**する完全な実行可能サンプルをステップバイステップで解説します。「ドキュメント参照」だけの曖昧な手順はありません。今日すぐにコピー＆ペーストして実行できる自己完結型のソリューションです。

## 前提条件

始める前に以下を用意してください。

* .NET 6.0 以降がインストール済み（コードは .NET 6 を対象としていますが、.NET 5 でも動作します）。
* Aspose.OCR for .NET NuGet パッケージ（CPU 版と GPU 版があり、ハードウェアに合わせてインストールしてください）。
* 処理したいサンプル TIFF または PNG ファイルが入ったフォルダー。
* Visual Studio 2022 もしくはお好みの IDE。

> **プロのコツ:** GPU 版を使用する場合は、グラフィックドライバーが最新であること、CUDA 11 以上がインストールされていることを確認してください。互換性のある GPU が見つからない場合、エンジンは自動的に CPU にフォールバックします。

## 手順 1 – プロジェクトの作成と Aspose.OCR のインストール

### H2: Create a New Console App and Add Aspose.OCR

ターミナル（または Visual Studio のパッケージマネージャコンソール）で次を実行します。

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

GPU 対応ライセンスをお持ちの場合は、代わりに GPU パッケージを追加します。

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

これでプロジェクトに **バッチ OCR** に使用する OCR ライブラリが参照されました。

## 手順 2 – OCR エンジンの初期化（CPU または GPU）

### H2: How to Batch OCR – Engine Initialization

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**ポイント:** `UseGpu` を切り替えるだけで、Aspose が最速のパスを自動選択します。GPU が利用できない場合はエンジンが静かに CPU に切り替わるため、ハードウェアが欠けていてもバッチジョブがクラッシュしません。

## 手順 3 – 処理対象ファイルの取得

### H2: Recognize Text from Images – Building the File List

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**エッジケース:** 形式が混在している場合は検索パターンを `"*.*"` に変更し、ループ内で拡張子でフィルタリングしてください。これによりバッチ処理の柔軟性が保たれます。

## 手順 4 – 各画像を処理しプレビューを表示

### H2: Extract Text from TIFF – Loop Through the Files

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**出力例:** 各 TIFF に対してコンソールに次のようなプレビューが表示されます。

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

このプレビューにより、すべてのファイルを手動で開かなくてもバッチが正常に完了したことが確認できます。

## 手順 5 – 結果の保存（任意だが便利）

### H3: Persist OCR Output to Text Files

下流処理で全文テキストが必要な場合は、`foreach` ループ内に以下を追加します。

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

これで各 TIFF に対して同名の `.txt` ファイルが生成され、完全な OCR 出力が保存されます。インデックス作成や検索、あるいは言語モデルへの入力に最適です。

## 手順 6 – デモ実行と検証

1. プロジェクトをビルド: `dotnet build`。
2. 実行: `dotnet run --project GpuBatchDemo.csproj`。

コンソールにプレビュー行が表示され、（任意ステップを追加した場合は）画像と同じディレクトリに `.txt` ファイルが生成されます。

### H3: Common Pitfalls & How to Fix Them

| 症状 | 考えられる原因 | 対処方法 |
|------|----------------|----------|
| **Empty `ocrResult.Text`** | 画像が暗すぎる、または DPI が低い | 画像を前処理（コントラスト上げ、拡大）するか、`ocrEngine.Settings.PreprocessImage = true` を設定 |
| **GPU error “CUDA driver version is insufficient”** | ドライバーが古い | GPU ドライバーを更新、または `UseGpu = false` にして CPU 強制 |
| **Exception “File not found”** | Linux/macOS でパス区切りが誤っている | `Path.Combine` またはスラッシュ（`/`）を使用 |

## 手順 7 – スケールアップ（数千ファイル以上）

数千枚の TIFF に拡張する際は次を検討してください。

* **並列処理:** `foreach` を `Parallel.ForEach` に置き換える（エンジンがスレッドセーフでない場合はスレッドごとにインスタンスを作成）。
* **チャンク I/O:** メモリ枯渇を防ぐために画像をバッチで読み込む。
* **ロギング:** 進捗をログファイルに書き出すと、クラッシュ後の再開が容易になる。

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **覚えておいて:** GPU メモリは共有されるため、並列 GPU ジョブを増やしすぎると逆に遅くなることがあります。まずは少数のスレッドでテストしてください。

## 完全動作サンプル（コピー＆ペースト可能）

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

このプログラムを実行すると、**画像からテキストを認識**し、**TIFF からテキストを抽出**し、**バッチ OCR を効率的に実行**する方法がデモンストレーションされます。

---

## 結論

これで C# と Aspose の OCR エンジンを使った **バッチ OCR** のエンドツーエンド例が完成しました。プロジェクトのセットアップ、GPU 加速の切り替え、ファイルリスト作成、各画像の処理、結果の永続化まで網羅しています。TIFF に限らず、任意の画像形式でも同じパターンが適用可能です—拡張子を差し替えるだけです。

次のステップに進みませんか？ OCR 出力を検索インデックスに統合したり、テキストを大規模言語モデルに投入したり、並列処理で大量バッチの処理時間を短縮したりしてみましょう。可能性は無限大です。土台はすでに手に入れました。

質問や独自のバッチ OCR テクニックを共有したい方は、下のコメント欄にどうぞ—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}