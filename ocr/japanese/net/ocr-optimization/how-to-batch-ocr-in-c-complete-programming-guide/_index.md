---
category: general
date: 2026-05-31
description: Aspose OCR を使用した C# でのバッチ OCR の方法。画像をテキストに変換し、画像からテキストを抽出し、複数ファイルを効率的に処理する方法を学びましょう。
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: ja
og_description: Aspose OCR を使用した C# でのバッチ OCR の方法。画像をテキストに変換し、画像からテキストを抽出し、複数ファイルの
  OCR を簡単に処理します。
og_title: C#でバッチOCRを行う方法 – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: C#でバッチOCRを行う方法 – 完全プログラミングガイド
url: /ja/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でバッチOCRを行う方法 – 完全プログラミングガイド

スキャンした画像が入ったフォルダー全体を、手動でファイルを開くことなく **バッチOCR** したいと思ったことはありませんか？ あなただけではありません。実務の多くのプロジェクト—たとえば請求書の自動化や歴史的写真のアーカイブ—では、**画像をテキストに変換** する必要があり、1枚ずつ処理するのは膨大な時間がかかります。

このチュートリアルでは、ソースディレクトリ内のすべての PNG、JPG、TIFF を取得し、Aspose OCR で処理し、対応する *.txt* ファイルを出力フォルダーに保存する、すぐに実行できる C# コンソール アプリの作成手順を解説します。最後まで読むと、**画像からテキストを抽出** する方法、**複数ファイルのOCR** の扱い方、そして後で必要になる **バッチOCR処理** の土台をしっかり身につけられます。

## 学べること

- Aspose OCR NuGet パッケージを使用した .NET プロジェクトのセットアップ方法。  
- **バッチOCR** 実行のためのソースフォルダーと出力フォルダーの定義方法。  
- 対応画像タイプを列挙し、OCR エンジンに渡す手順。  
- 認識したテキストを個別の *.txt* ファイルに書き出し、実質的に **画像をテキストに変換** する方法。  
- フォルダーが存在しない、未対応フォーマット、パフォーマンス調整などの一般的な落とし穴への対処法。

Aspose の事前経験は不要です。C# と Visual Studio の基本がわかっていればすぐに始められます。

---

![バッチOCR処理のフローを示す図（画像フォルダーからテキスト出力へ）](/images/batch-ocr-flow.png){alt="バッチOCRフローダイアグラム"}

## バッチOCRの設定 – プロジェクトのセットアップ

コードに入る前に、以下を用意してください。

1. **.NET 6 SDK**（またはそれ以降）をインストール – 最新のランタイムはパフォーマンスが向上し、async I/O のネイティブサポートが利用できます。  
2. **Visual Studio 2022**（Community エディションで問題ありません）またはお好みのエディター。  
3. **Aspose.OCR** NuGet パッケージ。Package Manager Console からインストールします：

   ```powershell
   Install-Package Aspose.OCR
   ```

以上です。このチュートリアルの残りは、パッケージが正しく参照されていることを前提に進めます。

## ステップ2: ソースと出力フォルダーの準備（画像をテキストに変換）

まず、原画像を格納するフォルダーと、生成された *.txt* ファイルを保存するフォルダーの 2 つが必要です。以下のコードは、出力フォルダーが存在しない場合に自動で作成します—手動で作業する必要はありません。

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **なぜ重要か:** `CreateDirectory` 呼び出しを省くと、最初のテキストファイルを書き込もうとした瞬間に `DirectoryNotFoundException` がスローされます。事前にディレクトリを作成しておくことで、バッチOCRプロセスの堅牢性が向上します。

## ステップ3: OCR用の画像ファイルを列挙（複数ファイル）

次に、サポートしている形式に一致するすべてのファイルを取得します。LINQ を使うことでコードを簡潔に保ちつつ、可読性も確保できます。

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **ヒント:** 後で PDF や BMP を扱う必要が出たら、`Where` 句に条件を追加するだけです。フィルタを一箇所にまとめておくと、将来的な変更が楽になります。

## ステップ4: 各画像でOCRエンジンを実行（バッチOCRの方法）

本題です。各画像を Aspose OCR に渡し、認識されたテキストを取得します。以下のループはファイルごとに新しい `OcrEngine` インスタンスを生成するため、前の画像のメモリが次の画像処理前に解放されます。

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**何が起きているか？**  

- `ImageStream.FromFile` は画像を Aspose が読み取れるストリームにロードします。  
- `ocrEngine.Recognize()` が実際の OCR アルゴリズムを実行し、結果は `ocrResult.Text` の文字列として返ります。  
- `File.WriteAllText` がその文字列をディスクに書き込み、実質的に **画像からテキストを抽出** します。

### エッジケースの処理

- **破損した画像** – 認識呼び出しを `try/catch` で囲み、失敗をログに残して次のファイルへ進めます。  
- **大規模バッチ** – マルチコアマシンを使用している場合は、`Parallel.ForEach` で非同期に処理すると効果的です。  
- **異なる言語** – `ocrEngine.Language = Language.English;` のように、`Recognize()` を呼び出す前に対象言語を設定します。

## ステップ5: 抽出したテキストを保存（画像からテキストを抽出）

前のスニペットですでに OCR 出力は保存していますが、ロジックをヘルパーメソッドに切り出してみましょう。これによりメインループがすっきりし、再利用性が高まります。

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

その後、インラインの `File.WriteAllText` 呼び出しを次のように置き換えます：

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **なぜメソッドに分離するのか？** 認識処理と永続化処理を分離でき、トリミングやタイムスタンプ付加などの後処理を一箇所で実装できるようになります。

## 完全動作例 – C#でのバッチOCR処理

すべての部品を組み合わせた、すぐにコピー＆ペーストして新しいコンソール アプリ プロジェクトで実行できる自己完結型プログラムを示します。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### 期待される出力

プログラムを実行すると、コンソールに次のような行が表示されます：

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

同時に、`C:\OCR\BatchTxt` フォルダーには以下が作成されます：

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

各ファイルには元画像のプレーンテキスト表現が格納されており、インデックス作成、検索、または下流の分析にすぐに利用できます。

## プロのコツと一般的な落とし穴（バッチOCR処理）

- **メモリ管理:** Aspose OCR は各 `Recognize()` 呼び出し後に画像バッファを解放しますが、数千ファイルを処理する場合は `GC.Collect()` を適度に呼び出してメモリ使用量を抑えることを検討してください。  
- **速度向上:** .NET 6 以降では `OcrEngine.RecognizeAsync()` を使用し、`Task` と組み合わせて複数タスクを同時に実行すると効果的です。

## 次に学ぶべきことは？

- [Aspose.OCR for .NET でリストを使用したバッチOCR画像の処理方法](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [フォルダー単位でのOCR操作で画像からテキストを抽出する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET でアーカイブ画像に対してOCRを実行する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}