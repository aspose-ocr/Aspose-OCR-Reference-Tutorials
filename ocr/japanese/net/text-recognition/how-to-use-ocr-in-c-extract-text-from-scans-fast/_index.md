---
category: general
date: 2026-03-13
description: C#でOCRを使用してスキャンからテキストを抽出する方法。Aspose OCRとGPUアクセラレーションを活用し、TIFFをテキストに変換する手順とステップバイステップのコードを学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: ja
og_description: C#でOCRを使用してスキャンからテキストを抽出する方法。このガイドでは、Aspose OCRとGPUアクセラレーションを利用してTIFFをテキストに変換する手順を示します。
og_title: C#でOCRを使用する方法 – スキャンからテキストを高速に抽出
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でOCRを使用する方法 – スキャンからテキストを高速抽出
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – スキャンからテキストを高速抽出

スキャンしたTIFFファイルの山から可読テキストを **OCRで抽出** できるか、考えたことはありませんか？ あなただけではありません。実務のプロジェクト—たとえば請求書のデジタル化、歴史的文書のアーカイブ、あるいはPDFを検索可能にするだけでも—開発者は **スキャンからテキストを抽出** する信頼できる方法を求めています。

朗報です。Aspose OCR と数行の C# コードさえあれば、モダンなワークステーションでも数秒で TIFF をテキストに変換できます。以下では、すぐに実行可能な完全なサンプルと、各選択肢の背景にある考え方を示すので、独自のワークフローに合わせてカスタマイズできます。

## 必要なもの

本題に入る前に、以下が揃っていることを確認してください。

| 前提条件 | 理由 |
|--------------|----------------|
| .NET 6+（または .NET Framework 4.7+） | Aspose OCR NuGet パッケージは最新の .NET ランタイムを対象としています。 |
| Visual Studio 2022（またはお好みの IDE） | IntelliSense とデバッグが簡単に行えます。 |
| CUDA 対応 GPU とドライバ（任意） | `ocrEngine.UseGpu = true` を設定すると、大量バッチで顕著な速度向上が期待できます。 |
| 処理したい TIFF 画像が入ったフォルダー | 本チュートリアルは `*.tif` ファイルを対象としていますが、パターンは変更可能です。 |
| Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`） | 重い処理を担うコアライブラリです。 |

これらが不足している場合は、先に入手してください。依存関係が足りないまま読み進めても意味がありません。

## ソリューションの概要

大まかにプログラムは次の 3 つの処理を行います。

1. **OCR エンジンを作成**し、必要に応じて GPU 加速を有効化。  
2. **ディレクトリ内のすべての TIFF ファイルを走査**し、認識を実行してプレーンテキストを取得。  
3. **テキストを元画像と同じ場所に `.txt` ファイルとして書き出す**。

以上です。コードは意図的にコンパクトにしていますが、明示的な言語選択、リソースの適切な破棄、一般的なエッジケースへのエラーハンドリングといったベストプラクティスを示しています。

![C#でOCRを使用する例](/images/how-to-use-ocr-csharp.png "C#でOCRを使用してスキャンからテキストを抽出するイラスト")

## 手順 1: OCR エンジンの初期化（How to Use OCR）

最初に必要なのは `OcrEngine` のインスタンスです。このオブジェクトが Aspose OCR のすべての機能へのゲートウェイとなります。デフォルトでは CPU が使用されますが、`UseGpu = true` を設定すると、CUDA 対応ドライバがインストールされている環境では重い行列計算が GPU にオフロードされます。

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**この設定が重要な理由:**  
- **GPU 加速** により、高解像度スキャンの場合は処理時間が最大 70 % 短縮されます。  
- **明示的な言語選択** によりエンジンの推測を防ぎ、特に非ラテン文字系での精度が向上します。

## 手順 2: エンジンにスキャン画像の場所を指定（Convert TIFF to Text）

次に、画像が格納されているフォルダーをプログラムに教えます。`Directory.GetFiles` に `*.tif` フィルタを渡すことで、ロジックをシンプルに保ち、`.jpg` や `.png` といった無関係なファイルが混入するのを防げます。

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**エッジケースの注意点:** ディレクトリが空の場合、以下のループは一度も実行されませんが、これは問題ありません。後述の「ファイルが見つかりません」メッセージが表示されます。

## 手順 3: 各 TIFF ファイルを処理（Extract Text from Scans）

プログラムの核心部分です。各画像を読み込み、OCR を実行し、結果を保存します。`ImageStream.FromFile` ヘルパーはファイルを直接メモリにストリームし、`Bitmap` を先にロードするよりも効率的です。

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**`try/catch` で各イテレーションをラップする理由:**  
大量の文書をバッチ処理すると、破損した TIFF やメモリ不足が発生しがちです。例外が起きても全体の実行を中断せず、問題をログに残して次のファイルへ進むことで、パイプラインの堅牢性を保ちます。

### 期待される出力

`example.tif` ごとに、同名の `example.txt` が生成され、以下のような内容が入ります。

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

OCR エンジンが行を読めなかった場合は空行または文字化けが入りますが、例外は発生しません。

## 手順 4: クリーンアップと破棄（Best Practice）

`OcrEngine` は `IDisposable` を実装しているため、使用後はネイティブリソースを解放するのがマナーです。短いコンソールアプリでは GC に任せても問題ありませんが、明示的に破棄する習慣は後々役立ちます。

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## 完全動作サンプル（コピー＆ペーストで使用可）

以下は新規コンソールアプリプロジェクトに貼り付けられる、完全なプログラムです。Aspose.OCR NuGet パッケージを追加していれば、そのままビルドできます。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### クイックチェックリスト

- **GPU フラグ** – CUDA ドライバが無い場合は削除するか `false` に設定。  
- **言語** – `Language.English` を他のサポート言語に置き換え。  
- **ファイルパターン** – スキャンが別形式の場合は `"*.png"` や `"*.*"` に変更。  

## よくある落とし穴とプロのコツ（c# OCR tutorial）

| 落とし穴 | 回避策 |
|---------|-----------------|
| 大量バッチで **メモリ不足エラー** が発生 | ファイルを小さなチャンクに分割して処理するか、50 ファイルごとに `GC.Collect()` を呼び出す（稀に必要）。 |
| **GPU が検出されない** が `UseGpu = true` になっている | エンジンは自動で CPU にフォールバックしますが、構築後に `ocrEngine.IsGpuAvailable` を確認できます。 |
| **言語パックが間違っている** と文字化け | 常に `ocrEngine.Language` を明示的に設定してください。デフォルトは `Language.Unknown` になることがあります。 |
| **ファイルパスに Unicode 文字が含まれる** | `Path.GetFullPath` で正規化するか、Windows でパスが長すぎる場合は `@"\\?\"` をプレフィックスとして使用。 |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}