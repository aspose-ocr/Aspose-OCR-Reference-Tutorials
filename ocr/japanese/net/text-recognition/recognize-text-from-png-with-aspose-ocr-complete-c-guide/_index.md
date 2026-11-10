---
category: general
date: 2026-05-28
description: C#でAspose OCRを使用してPNGからテキストを認識します。スキャンしたページからテキストを抽出し、画像上で効率的にOCRを実行する方法を学びましょう。
draft: false
keywords:
- recognize text from png
- extract text from scanned pages
- perform ocr on images
- Aspose OCR C#
- OCR image processing
language: ja
og_description: C#でAspose OCRを使用してPNGからテキストを認識する。スキャンしたページからテキストを抽出し、画像のOCRを数分でマスターしよう。
og_title: Aspose OCRでPNGからテキストを認識する – 完全C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  headline: recognize text from png with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: recognize text from png using Aspose OCR in C#. Learn how to extract
    text from scanned pages and perform OCR on images efficiently.
  name: recognize text from png with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
    text: '**Engine initialization** – The `OcrEngine` class is the entry point; it
      holds all configuration and state.'
  - name: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
    text: '**Evaluation‑mode guard** – If you’re using a trial license, Aspose caps
      the number of pages you can process. Setting `MaxPagesInEvaluation` prevents
      the library from throwing a *LicenseException* halfway through.'
  - name: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
    text: '**Image loading** – `ImageStream.FromFile` abstracts away the `System.Drawing`
      dependency, letting you feed any supported format (PNG, JPEG, BMP) directly.'
  - name: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
    text: '**Recognition loop** – By iterating, you can **perform OCR on images**
      in bulk, which is exactly what most real‑world scanning pipelines need.'
  - name: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
    text: '**Disposal** – The engine holds unmanaged resources; disposing releases
      memory promptly, especially important when processing many high‑resolution PNGs.'
  - name: Install the NuGet package.
    text: Install the NuGet package.
  - name: Initialise `OcrEngine`.
    text: Initialise `OcrEngine`.
  - name: (Optional) Set a page limit for evaluation mode.
    text: (Optional) Set a page limit for evaluation mode.
  - name: Load each PNG with `ImageStream.FromFile`.
    text: Load each PNG with `ImageStream.FromFile`.
  - name: Call `Recognize()` and output the result.
    text: Call `Recognize()` and output the result.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Aspose OCRでPNGからテキストを認識する – 完全C#ガイド
url: /ja/net/text-recognition/recognize-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCRでPNGからテキストを認識する – 完全なC#ガイド

.NET アプリケーションで **PNG からテキストを認識** する必要がありましたか？Aspose OCR を使用すれば、低レベルの画像処理に苦労することなく、**スキャンしたページからテキストを抽出** したり **画像で OCR を実行** したりできます。このチュートリアルでは、すぐに実行できる C# のサンプルを順に解説し、各行がなぜ重要かを説明し、実際のプロジェクトに適用する方法を示します。

マルチページのスキャンでも動作するか、評価モードを制限できるか、巨大な画像ファイルの扱い方はどうか、気になる方はぜひご覧ください。最後まで読むと、実務でそのままコピーペーストできる、堅牢なプロダクション向けコードスニペットが手に入ります。

---

## 必要なもの

本題に入る前に、以下が揃っていることを確認してください。

| Prerequisite | Why it matters |
|--------------|----------------|
| **.NET 6.0 or later** (or .NET Framework 4.6+) | Aspose.OCR は最新のランタイムを対象としており、最新のパフォーマンス向上が得られます。 |
| **Visual Studio 2022** (or any IDE you like) | 使いやすいエディタはコードのテストを容易にします。 |
| **Aspose.OCR NuGet package** | 実際に重い処理を行うライブラリです。 |
| A folder with a handful of **PNG images** you want to read | このチュートリアルでは `page1.png`、`page2.png` などの名前のファイルがあることを前提としています。 |

もしこれらに心当たりがなければ、NuGet パッケージをインストールしてシンプルなコンソールプロジェクトを作成するだけです—追加設定は不要です。

---

## ステップ 1: NuGet で Aspose.OCR をインストール

ターミナル（またはパッケージ マネージャ コンソール）を開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

または UI が好きな場合は、**Dependencies → Manage NuGet Packages** を右クリックし、*Aspose.OCR* を検索して **Install** をクリックします。これにより、後で使用する `ImageStream` ヘルパークラスを含む必要なものがすべて取得されます。

> **プロのコツ:** 最新の安定版（2026年5月時点で 23.10）を使用してください。新しいリリースには、扱いにくい画像形式に対するバグ修正が含まれることが多いです。

---

## ステップ 2: 最小限のコンソールアプリを作成

まだ作成していない場合は、新しいコンソールプロジェクトを作成してください。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

`Program.cs` の内容を以下の完全なサンプルに置き換えます。コードは **自己完結** であり、外部設定ファイルや隠れたマジックはありません。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine
            // -------------------------------------------------
            var engine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Optional: limit pages when running in evaluation mode
            // -------------------------------------------------
            // Evaluation licenses only allow a few pages; set this to avoid runtime errors.
            engine.Configuration.MaxPagesInEvaluation = 5;

            // -------------------------------------------------
            // 3️⃣  Define where your PNG files live
            // -------------------------------------------------
            string basePath = @"YOUR_DIRECTORY"; // <-- change this to your real folder

            // -------------------------------------------------
            // 4️⃣  Loop through the images you want to process
            // -------------------------------------------------
            for (int i = 0; i < 5; i++) // adjust the loop count to match your file count
            {
                // Load the current page image
                engine.Image = ImageStream.FromFile($"{basePath}/page{i + 1}.png");

                // -------------------------------------------------
                // 5️⃣  Perform OCR and display the result
                // -------------------------------------------------
                Console.WriteLine($"--- Page {i + 1} ---");
                string recognizedText = engine.Recognize();

                // Show the extracted text; you could also write it to a file.
                Console.WriteLine(recognizedText);
                Console.WriteLine(); // blank line for readability
            }

            // -------------------------------------------------
            // 6️⃣  Clean up (optional but good practice)
            // -------------------------------------------------
            engine.Dispose();
        }
    }
}
```

### なぜこの構成が機能するのか

1. **エンジンの初期化** – `OcrEngine` クラスはエントリーポイントで、すべての設定と状態を保持します。  
2. **評価モードのガード** – トライアル ライセンスを使用している場合、Aspose は処理できるページ数に上限を設けます。`MaxPagesInEvaluation` を設定することで、途中で *LicenseException* が発生するのを防げます。  
3. **画像の読み込み** – `ImageStream.FromFile` は `System.Drawing` への依存を抽象化し、サポートされている形式（PNG、JPEG、BMP）を直接読み込めます。  
4. **認識ループ** – ループ処理により、**画像で OCR を実行** を一括で行えます。これは実際のスキャンパイプラインで最も必要とされる機能です。  
5. **破棄処理** – エンジンはアンマネージドリソースを保持しているため、Dispose でメモリを速やかに解放します。特に高解像度 PNG を多数処理する場合に重要です。

---

## ステップ 3: アプリを実行して出力を確認

ビルドして実行します。

```bash
dotnet run
```

指定したフォルダーに `page1.png` … `page5.png` の 5 つの PNG ファイルを配置したとすると、以下のような出力が表示されます。

```
--- Page 1 ---
Invoice #12345
Date: 2026-05-01
Total: $1,250.00

--- Page 2 ---
Thank you for your purchase!
...

```

空文字列が出力された場合は、画像に **認識可能なテキスト** が含まれているか（コントラストがはっきりしているか、ぼやけたサインの写真ではないか）を再確認してください。Aspose OCR は高品質なスキャン（300 dpi 以上）で最も効果を発揮します。

> **画像例**  
> ![recognize text from png example output](https://example.com/ocr-output.png "recognize text from png – console output")

---

## ステップ 4: **スキャンしたページからテキストを抽出** する際の一般的な落とし穴

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| 空の出力 | 画像のコントラストが低い、またはノイズが多い | Aspose.Imaging で前処理（二値化、デスケュー）を行う。 |
| 文字化け | 言語が設定されていない（デフォルトは英語） | `engine.Configuration.Language = Language.English;` または `Language.French` などに設定する。 |
| 例外 *“File not found”* | フォルダー パスが間違っている、または拡張子が欠落している | 安全のために `Path.Combine(basePath, $"page{i+1}.png")` を使用する。 |
| 数ページ処理後のライセンスエラー | `MaxPagesInEvaluation` を設定せずにトライアル ライセンスを使用している | ライセンスを購入するか、`MaxPagesInEvaluation` 行を残してください。 |

これらのヒントにより、**スキャンしたページからテキストを抽出** のワークフローがスムーズに保たれ、元の素材が完璧でなくても対応できます。

---

## ステップ 5: 上級編 – 数百枚の画像にスケールアップ

データベースやクラウド バケットに保存された画像に対して **画像で OCR を実行** する必要がある場合は、`for` ループをファイルパスのコレクションに対する `foreach` に置き換えます。

```csharp
string[] pngFiles = Directory.GetFiles(basePath, "*.png");
foreach (var file in pngFiles)
{
    engine.Image = ImageStream.FromFile(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(engine.Recognize());
}
```

また、**マルチスレッド**（Aspose OCR はスレッドセーフ）を有効にすれば、マルチコアマシンでの処理速度を向上させられます。

```csharp
Parallel.ForEach(pngFiles, file =>
{
    var localEngine = new OcrEngine(); // each thread gets its own engine
    localEngine.Image = ImageStream.FromFile(file);
    string text = localEngine.Recognize();
    lock (Console.Out) // avoid garbled console output
    {
        Console.WriteLine($"--- {Path.GetFileName(file)} ---");
        Console.WriteLine(text);
    }
    localEngine.Dispose();
});
```

各エンジンインスタンスを必ず破棄してください。そうしないとネイティブメモリがリークします。

---

## ステップ 6: PNG 以外 – 他のフォーマットと PDF

Aspose OCR は PNG に限定されません。JPEG、BMP、TIFF、あるいは **PDF ページ**（まず画像に変換してから）も処理できます。PDF の場合は Aspose.PDF と Aspose.OCR を組み合わせます。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load PDF, render each page to a PNG stream, then OCR
Document pdf = new Document("sample.pdf");
for (int pageNum = 1; pageNum <= pdf.Pages.Count; pageNum++)
{
    using var imgStream = new MemoryStream();
    var rasterizer = new PngDevice();
    rasterizer.Process(pdf.Pages[pageNum], imgStream);
    imgStream.Position = 0;

    engine.Image = ImageStream.FromStream(imgStream);
    Console.WriteLine($"--- PDF Page {pageNum} ---");
    Console.WriteLine(engine.Recognize());
}
```

このスニペットは、PDF として届く **スキャンしたページからテキストを抽出** する方法を示しています。請求書処理パイプラインでよくあるシナリオです。

---

## まとめと次のステップ

ここでは Aspose OCR を使用した **PNG からテキストを認識** の全ライフサイクルをカバーしました。

1. NuGet パッケージをインストールする。  
2. `OcrEngine` を初期化する。  
3. （オプション）評価モード用にページ数上限を設定する。  
4. `ImageStream.FromFile` で各 PNG を読み込む。  
5. `Recognize()` を呼び出し、結果を出力する。

## 関連チュートリアル

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}