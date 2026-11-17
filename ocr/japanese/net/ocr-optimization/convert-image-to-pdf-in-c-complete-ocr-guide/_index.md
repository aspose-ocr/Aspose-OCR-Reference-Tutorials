---
category: general
date: 2026-09-13
description: Aspose OCR を使用して C# でスキャンしたページを PDF に変換する方法を学びます。このガイドでは、画像の前処理、韓国語テキスト認識、検索可能な
  PDF の作成方法を紹介します。
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aspose OCR を使用して C# でスキャンしたページを PDF に変換する方法を学びます。このチュートリアルでは、画像の前処理、GPU
  加速 OCR による韓国語テキスト認識、数分で検索可能な PDF を生成する手順を解説します。
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: C# と OCR を使用してスキャンしたページを PDF に変換する方法
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: C# と OCR を使用してスキャンしたページを PDF に変換する方法
url: /ja/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャンしたページをC#でOCRを使用してPDFに変換する方法

スキャンしたページをテキスト検索可能なPDFに **convert a scanned page to PDF** したい場合、ここが正解です。このチュートリアルでは、Aspose OCR を使用して **preprocess image for OCR**、**recognize Korean text image**、そして最後に **create searchable PDF image** を行う方法を、シンプルな C# コンソールアプリケーションで解説します。

## クイック回答
- **What library handles OCR?** Aspose.OCR for .NET  
- **Can I use the GPU?** はい – GPU 加速を有効にすると最大 2 倍速く処理できます  
- **Do I need a Korean language pack?** 初回使用時に自動でダウンロードされます  
- **Will the output be searchable?** 生成された PDF には不可視のテキストレイヤーが含まれます  
- **What .NET versions are supported?** .NET 6.0 以降 ( .NET Core と .NET Framework を含む)

## 必要条件
- **.NET 6.0 or later** – .NET Core、.NET Framework、.NET 5/6+ でも動作します  
- **Aspose.OCR for .NET** NuGet パッケージ (`Aspose.OCR`) – 試用キーは Aspose サイトで無料です  
- 韓国語文字を含むサンプル画像、例: `korean_book_page.jpg`  
- お好みの IDE (Visual Studio 2022、VS Code、Rider など)

> **Pro tip:** 画像は `Resources/` フォルダーに保存すると、マシン間でパスが一貫します。

## プロセスの概要
1. GPU サポート付きで OCR エンジンを初期化します。  
2. **preprocess image for OCR** フィルター（デスキューやデノイズなど）を追加します。  
3. 韓国語言語モデルをダウンロードしてロードします（自動処理）。  
4. 画像に対して OCR を実行します。  
5. **SearchablePdfExporter** を使用して結果をエクスポートし、**create searchable PDF image** を作成します。  
6. （オプション）OCR 出力を JSON にシリアライズして下流パイプラインで使用します。

以下で各ステップを展開し、*why* が重要な理由を説明し、コピー＆ペーストできる正確なコードを提供します。

## スキャンしたページをPDFに変換する仕組みは？

`OcrEngine` は Aspose.OCR の主要クラスで、画像に対して光学文字認識を実行します。  
`SearchablePdfExporter` は元の画像と検索用の不可視テキストレイヤーを含む PDF を作成します。  
`RecognitionResult` は OCR エンジンが返すテキストと信頼度データを保持します。

画像は `new OcrEngine()` で読み込み、`engine.Recognize("korean_book_page.jpg")` を呼び出し、`RecognitionResult` を `SearchablePdfExporter.Export` に渡します。この 2 段階のフローはビットマップを読み取り、Unicode テキストを抽出し、両方を単一の PDF に埋め込みます。テキストレイヤーは不可視ですが検索可能です。GPU 加速により認識時間は約半分に短縮され、デスキューとデノイズフィルターによりノイズの多いスキャンで精度が最大 15 % 向上します。

## 画像をPDFに変換 – 完全なワークフロー
以下のスニペットは *complete* なプログラムです。新しいコンソールプロジェクト (`dotnet new console -n OcrPdfDemo`) を作成し、自動生成された `Program.cs` をプレースホルダーに示されたコードに置き換えます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### なぜこれが機能するのか
- **GPU acceleration** は CPU のみモードと比べて認識時間を約半分に短縮します。  
- **Deskew** と **Denoise** は古典的な *preprocess image for OCR* 手法で、エンジンが文字を見逃す原因となる一般的なスキャン欠陥を修正します。  
- **Language model loading** は **recognize Korean text image** に不可欠です。韓国語モデルがないとエンジンは汎用ラテン文字にフォールバックし、意味不明な出力になります。  
- **SearchablePdfExporter** は元のビットマップと不可視テキストオーバーレイを束ね、**create searchable pdf image** の結果を提供し、任意の PDF ビューアでインデックス可能にします。

## なぜこれが機能するのか
- **GPU acceleration** は CPU のみモードと比べて認識時間を約半分に短縮します。  
- **Deskew** と **Denoise** は古典的な *preprocess image for OCR* 手法で、エンジンが文字を見逃す原因となる一般的なスキャン欠陥を修正します。  
- **Language model loading** は **recognize Korean text image** に不可欠です。韓国語モデルがないとエンジンは汎用ラテン文字にフォールバックし、意味不明な出力になります。  
- **SearchablePdfExporter** は元のビットマップと不可視テキストオーバーレイを束ね、**create searchable pdf image** の結果を提供し、任意の PDF ビューアでインデックス可能にします。

## OCR 用画像前処理 – ヒントとコツ
`DeskewFilter` はスキャンページの回転を補正します。  
`ContrastFilter` は画像のコントラストを調整し、OCR の精度を向上させます。  
`BinarizationFilter` はしきい値に基づいて画像を白黒に変換し、背景ノイズを減らします。  
`OrientationFilter` は縦横混在ページを検出し補正します。

| 問題 | 追加フィルター | 追加方法 |
|-------|-------------------|------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** フィルターを増やしすぎると処理が遅くなる可能性があります。スケールアップする前に、単一ページで各変更をテストしてください。

## 韓国語テキスト画像の認識 – よくある落とし穴
韓国語スクリプトは視覚的に密集したハングル音節を含みます。文字化けが発生した場合は次を確認してください:

1. **Ensure the language model is fully downloaded** – コンソールに “Downloading Korean model…” のようなメッセージが出ているか確認します。  
2. **Increase the `MaxAngle`** を `DeskewFilter` で設定し、スキャンが 12° を超えて回転している場合に調整します。  
3. **Boost GPU memory** を `ocrEngine.GpuMemoryLimit = 2048;` (単位は MB) に設定します。

`LanguageModel.Korean` は OCR 用の韓国語データをロードし、正確なハングル認識を可能にします。

これらの調整は **recognize Korean text image** の成功に直接影響します。

## 検索可能な PDF 画像の作成 – 結果の検証
プログラムが終了したら、任意の PDF リーダー（Adobe Acrobat Reader、Foxit、Chrome など）で `korean_page.pdf` を開きます。次の操作が可能になるはずです:

- マウスで **Select text** でき、ネイティブ PDF のようにテキストを選択できます。  
- 組み込みの検索ボックスで韓国語単語を **Search** できます。  

テキストレイヤーが空白の場合、`Export` メソッドに正しい画像パスが渡されているか、OCR 結果の `RecognitionResult.Text` が空でないかを再確認してください。

## 完全な JSON 出力 – 期待される内容
コンソールは整形された JSON ペイロードを出力します。以下は抜粋例です:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## トラブルシューティング & FAQ
**Q: My PDF is huge compared to the original image.**  
A: エクスポーターは元のビットマップをネイティブ解像度で埋め込みます。サイズが問題の場合は、認識 *before* に画像を縮小してください：

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: The OCR returns empty strings.**  
A: 画像パスが正しいか、ファイルが破損していないか確認してください。また、GPU ドライバーが最新であることを確認してください。古いドライバーはサイレント失敗を引き起こすことがあります。

**Q: Can I process multiple pages in a loop?**  
A: もちろんです。ステップ 4‑6 を `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` ループで囲み、出力 PDF のパスを適宜変更してください。

## 結論
私たちは **converted image to PDF** を実現し、検索可能なテキストを保持しました。これはすべて Aspose OCR の強力なパイプラインのおかげです。**preprocess image for OCR** により精度が向上し、**recognize Korean text image** により複雑なスクリプトを処理し、**create searchable pdf image** により携帯性とインデックス可能なドキュメントが得られます。

コードを取得し、独自のスキャン画像に適用して、追加のフィルターや言語モデルで実験してください。同じパターンは中国語、日本語、または任意のラテン系言語でも機能します—適切な列挙子に `LanguageModel.Korean` を置き換えるだけです。

質問がありますか？コメントを残してください。ハッピーコーディング！

---

**最終更新日:** 2026-09-13  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose

## 関連チュートリアル
- [Aspose Ocr を使用してスキャンファイルから検索可能な PDF を作成](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR 前処理パイプライン：画像からテキストを認識する方法](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Aspose Ocr で画像からテキストを認識する完全ガイド](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}