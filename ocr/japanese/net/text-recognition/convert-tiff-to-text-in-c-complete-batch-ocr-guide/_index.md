---
category: general
date: 2026-05-25
description: C#で Aspose.OCR を使用して TIFF をテキストに変換します。バッチ画像からテキストへの変換方法を学び、TIFF ファイルから効率的にテキストを抽出しましょう。
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: ja
og_description: Aspose.OCRでTIFFをテキストに変換します。このガイドでは、バッチ画像からテキストへの変換方法と、C# の数行で TIFF
  ファイルからテキストを抽出する方法を示します。
og_title: C#でTIFFをテキストに変換 – 完全バッチOCRガイド
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: C#でTIFFをテキストに変換 – 完全バッチOCRガイド
url: /ja/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でTIFFをテキストに変換 – 完全バッチOCRガイド

Ever needed to **convert TIFF to text** but weren’t sure where to start? You’re not alone—many developers stumble over batch OCR when dealing with scanned documents. In this tutorial we’ll walk through a hands‑on solution that **extracts text from TIFF** files using Aspose.OCR, and we’ll do it in parallel so large folders finish in seconds.

You’ll also touch on **batch image to text conversion** best practices, so by the end you’ll have a reusable snippet that turns a whole directory of scanned images into neat *.txt* files—perfect for indexing, searching, or feeding into downstream analytics.

## 必要なもの

- **.NET 6.0** 以上 (コードは .NET Framework でもコンパイル可能)  
- **Aspose.OCR for .NET** NuGet パッケージ (`Install-Package Aspose.OCR`)  
- *.tif* ファイルが1つ以上含まれるフォルダー (従来の TIFF スキャン形式)  
- お好みの IDE (Visual Studio、VS Code、Rider など好きなもの)

以上です。外部サービスや API キーは不要で、純粋な C# と Aspose だけです。

![TIFF ファイルが処理され、結果のテキストファイルが生成されるスクリーンショット](/images/ocr-result.png "OCR 結果：変換された TIFF からテキストへの出力")

*(Alt text: 画面上で変換された TIFF からテキストへの出力を示すスクリーンショット)*

## ステップ 1: OCR エンジンの設定 – TIFF をテキストに変換

まず最初に、英字を読み取ることを認識した `OcrEngine` インスタンスが必要です。エンジンは変換の中心であり、正しく構成することで信頼できる結果が得られます。

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*この点が重要な理由:*  
Aspose.OCR は数十の言語をサポートしています。多言語のスキャンを扱う場合は、`OcrLanguage.English` を適切な enum 値に変更するだけです。言語を未定義のままにすると、エンジンは自動検出モードになり、速度が遅くなり精度も低下する可能性があります。

## ステップ 2: すべての TIFF ファイルを取得 – TIFF からテキストを効率的に抽出

次に、指定したフォルダーからすべての *.tif* ファイルを取得します。`Directory.GetFiles` を使用すると、バッチプロセッサに渡せるクリーンな配列が得られます。

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Pro tip:* スキャンがサブフォルダーに入れ子になっている場合は、`SearchOption.AllDirectories` フラグを使用できます。ただし、再帰が深くなるとバッチ処理中のメモリ使用量が増加する可能性があることを覚えておいてください。

## ステップ 3: 並列 OCR の実行 – バッチ画像からテキストへの変換

さあ、楽しいパートです。Aspose.OCR には、ファイルパスの配列、エンジン、`parallelism` ヒントを受け取る静的ヘルパー `BatchOcr.RecognizeAll` が用意されています。4つのスレッドを起動しますが、最新のクアッドコアラップトップではほぼ線形の速度向上が得られます。

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*なぜ並列処理なのか？*  
高解像度の TIFF バッチをスキャンすると CPU に負荷がかかります。作業を複数のスレッドに分散させることで、すべてのコアを稼働させ、総実行時間を大幅に短縮できます。コア数が多いサーバーで実行する場合は、`parallelism` の値をそれに応じて増やしてください。

## ステップ 4: 出力を書き込む – スキャン画像の TXT ファイルに変換

最後に、ディクショナリをループし、各テキストを元のベース名と同じ *.txt* ファイルに書き込みます。これが **convert scanned images txt** が実現する瞬間です。

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### コードが行うこと（平易な英語で）

1. **Create** 英語用に設定された OCR エンジンを作成します。  
2. **Collect** 対象フォルダーからすべての TIFF ファイルを収集します。  
3. **Run** `BatchOcr.RecognizeAll` を4スレッドで実行し、各画像を文字列に変換します。  
4. **Loop** 結果をループし、`.tif` 拡張子を `.txt` に置き換えて文字列をディスクに書き込みます。

これが 50 行未満のコードで実現する **convert TIFF to text** ワークフロー全体です。

## エッジケースの処理 – うまくいかないとき

- **Missing or corrupted TIFFs** – `BatchOcr` は `OcrException` をスローします。グレースフルにダウングレードする必要がある場合は、呼び出しを `try / catch` でラップしてください。  
- **Non‑English documents** – `OcrLanguage.English` を `OcrLanguage.Spanish`、`OcrLanguage.French` などに変更するか、`OcrLanguage.AutoDetect` を使用してください。  
- **Very large images** – OCR 前に DPI を下げること（`ocrEngine.ImagePreprocessing.Dpi = 200`）を検討してメモリを節約できますが、精度が低下する可能性があります。  
- **Output encoding** – 特定のコードページが必要な場合（例: Windows‑1252）、`File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))` に渡してください。

## 安定したバッチ変換のためのプロチップ

- **Log failures**: `List<string> failedFiles` を作成し、例外が発生したファイルを追加します。ループ後にリストをログに書き出してください。  
- **Reuse the engine**: 同じ `OcrEngine` インスタンスを多数のファイルで再利用できます。ループ内でインスタンス化しないでください。  
- **Validate the result**: 簡単な `if (string.IsNullOrWhiteSpace(extractedText))` で、空白または読めないスキャンをフラグ付けできます。  
- **Combine with PDF**: ソースがマルチページ PDF の場合、まず各ページを TIFF に変換します（Aspose.PDF が対応）。その後、このバッチを実行します。

## 次のステップ – シンプルな変換を超えて

大量に **extract text from TIFF** ファイルを抽出できるようになったので、次のことを検討したくなるかもしれません：

- *.txt* ファイルを検索インデックス（Elasticsearch、Azure Cognitive Search）に投入する。  
- 各結果に対して言語検出を実行し、文書をロケール固有のパイプラインにルーティングする。  
- OCR テキストを元画像に重ね合わせて検索可能な PDF を生成する（再び Aspose.PDF を使用）。

これらすべてのシナリオは同じコアアイデアに基づいています：**batch image to text conversion** は、より大規模な文書処理システムの構成要素です。

---

### 結論

あなたは Aspose.OCR を使用して **convert TIFF to text** を行い、フォルダー全体を並列処理し、各結果をきれいな *.txt* ファイルとして保存する方法を学びました。このソリューションは軽量で、完全に構成可能で、プロダクションにすぐに使用できます—レガシー請求書のデジタル化、スキャンした契約書のアーカイブ、テキスト検索エンジンの構築など、あらゆる用途に適しています。

実際に試してみて、parallelism を調整し、作成したテキストファイルを必要なワークフローに流し込みましょう。OCRを楽しんでください！

---

## 関連チュートリアル

- [フォルダー上で OCR 操作を使用して画像からテキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [画像からテキストを抽出 – Aspose.OCR for .NET を使用した OCR 最適化](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR を使用した言語選択付き C# で画像テキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}