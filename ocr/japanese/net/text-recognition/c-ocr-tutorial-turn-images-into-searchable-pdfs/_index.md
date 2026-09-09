---
category: general
date: 2026-01-12
description: c# OCRチュートリアルで、テキスト画像の認識方法、c#によるテキスト画像の抽出、そして信頼度スコア付きの画像からPDFへのOCRファイル生成方法を示します。
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: ja
og_description: テキスト画像を認識し、テキスト画像を抽出し、信頼度スコア付きで画像をPDFのOCR文書に変換する完全なC# OCRチュートリアルを学びましょう。
og_title: c# OCRチュートリアル – 画像を検索可能なPDFに変換
tags:
- OCR
- C#
- PDF
title: c# OCRチュートリアル – 画像を検索可能なPDFに変換
url: /ja/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 画像を検索可能な PDF に変換

サードパーティのサービスを探さずに C# プロジェクトで **テキスト画像を認識** できる方法を考えたことはありませんか？ あなただけではありません。実際のアプリケーション—たとえば請求書スキャナ、レシートトラッカー、または多言語文書アーカイブ—では、信頼性の高いオンプレミス OCR エンジンに加えて、信頼度スコアも出力できるものが必要です。  

この **c# ocr tutorial** では、画像の読み込み、言語モデルの選択、GPU 加速の切り替え、検索可能な PDF への保存まで、必要なすべての手順を解説します。最後まで実行すれば、テキスト抽出、OCR 信頼度のレポート、そしてオプションで *image to pdf ocr* ファイルの作成までを、わずか数分のコーディングで行えるサンプルコードが手に入ります。

## 作成するもの

- プレースホルダーとして `sample_multi_lang.jpg` を使用した多言語画像を読み込む。  
- アラビア語、ヒンディー語、ロシア語の言語モデルを選択（必要に応じて追加可能）。  
- マシンが対応していれば GPU 処理を有効にする。  
- 生の OCR 結果 **with confidence scores** を取得。  
- 結果を整形された JSON にシリアライズ **or** 検索可能な PDF として書き出す。  

外部の Web サービスや隠されたマジックは一切不要です。Aspose.OCR for .NET と数行の C#、そして各行が何を意味するかの明確な説明だけで完結します。

## 前提条件

- .NET 6.0 以上（コードは .NET Core と .NET Framework でもコンパイル可能）。  
- Visual Studio 2022（またはお好みの IDE）。  
- Aspose.OCR for .NET のライセンス（無料トライアルでテスト可能）。  
- オプション: 認識速度を上げたい場合は CUDA 対応 GPU。

> **Pro tip:** GPU が無い場合は `UseGpu = false` に設定すれば、コードを変更せずに CPU にフォールバックします。

## 手順 1: 必要な NuGet パッケージをインストール

Open the **Package Manager Console** and run:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

これら 3 つのパッケージが OCR エンジン、GPU 加速、そして信頼度出力用の JSON シリアライザーを提供します。

## 手順 2: プロジェクト構成を設定

Create a new console project (`dotnet new console -n AsposeOcrDemo`) and replace the generated `Program.cs` with the code below.  
All the logic lives inside the `Program` class; the only extra type is a small extension method that formats the OCR result for JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### このコードが機能する理由

1. **GPU toggle** – `GpuOcrEngine` leverages CUDA cores; the ternary operator makes switching painless.  
2. **Automatic language download** – `AutoDownloadResources = true` ensures the Arabic, Hindi, and Russian models are fetched the first time you run the app.  
3. **Confidence scores** – `result.Words` contains a `Confidence` for each recognized word; the extension method formats them into a clean JSON object.  
4. **Searchable PDF** – `result.Pdf` is already a fully searchable PDF, so we just write the byte array to disk. No extra libraries needed.

## 手順 6: サンプルを実行

Open a terminal, navigate to the project folder, and execute:

```bash
dotnet run
```

If you chose **JSON** output, you’ll see something like:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

If you switched to **PDF**, the console prints the path and you’ll find a searchable PDF right next to the source image.

## よくある質問とエッジケース

- **What if a language model isn’t available?**  
  The OCR engine throws a clear `ResourceNotFoundException`. Because we set `AutoDownloadResources = true`, the missing model is fetched automatically the first time, so the exception rarely surfaces in production.

- **Can I process a batch of images?**  
  Absolutely. Wrap the `engine.Recognize` call in a `foreach` loop over a directory of files. The same `OcrResultExtensions` works for each image.

- **Do I need a license for GPU?**  
  No. The free trial works for both CPU and GPU. A full license removes the trial watermark and lifts the page‑limit restrictions.

- **How accurate are the confidence scores?**  
  Scores range from 0.0 (no confidence) to 1.0 (perfect confidence). In practice, anything above 0.90 is reliable for downstream processing; you can filter lower‑confidence words if you need stricter validation.

## 手順 7: 次のステップ (OCR ツールキットを拡張)

1. **Add more languages** – just append `LanguageModel.French` (or any supported model) to the `Languages` array.  
2. **Combine OCR with PDF/A conversion** – Aspose.PDF can embed the OCR layer into a PDF/A‑2b compliant document for archival.  
3. **Integrate with Azure Functions** – wrap the logic into a serverless endpoint to process uploads on the fly.  
4. **Fine‑tune confidence thresholds** – use `result.Words.Where(w => w.Confidence < 0.85)` to flag uncertain words for manual review.

### TL;DR

This **c# ocr tutorial** shows you how to:

- Load an image and select multiple language models.  
- Turn on GPU acceleration with a single boolean flag.  
- Retrieve OCR results **with confidence scores** and serialize them to JSON.  
- Optionally write a searchable PDF (**image to pdf ocr**).  

All of that is achievable with just a handful of lines, a free Aspose.OCR trial, and the code above. Give it a spin, tweak the language list, and you’ll have a production‑ready OCR pipeline in minutes.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}