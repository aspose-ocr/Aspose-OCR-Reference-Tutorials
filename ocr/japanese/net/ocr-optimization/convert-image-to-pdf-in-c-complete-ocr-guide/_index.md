---
category: general
date: 2025-12-30
description: C#で Aspose OCR を使用して画像を PDF に変換します。OCR 用の画像前処理方法、韓国語テキスト画像の認識、そして検索可能な
  PDF 画像を迅速に作成する方法を学びましょう。
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: ja
og_description: Aspose OCRで画像をPDFに変換します。このチュートリアルでは、OCR用の画像前処理、韓国語テキスト画像の認識、検索可能なPDF画像の作成方法を示します。
og_title: C#で画像をPDFに変換 – 完全OCRガイド
tags:
- C#
- OCR
- Aspose
- PDF
title: C#で画像をPDFに変換する – 完全OCRガイド
url: /ja/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像をPDFに変換 – 完全OCRガイド

画像を **convert image to PDF** したいけど、内部のテキストも検索可能にしたいと感じたことはありませんか？ あなただけではありません。特に韓国語で書かれたスキャンページを扱う際、多くの開発者が同じ壁にぶつかります。良いニュースは、Aspose OCR を使えば **preprocess image for OCR**、**recognize Korean text image**、そして最終的に **create searchable PDF image** を数行のコードで実現できることです。

このチュートリアルでは、韓国語の書籍ページの生JPEGを読み込み、画像をクリーニングし、テキストを抽出し、検索可能なPDFとしてまとめるまでの全パイプラインを解説します。最後には、任意の .NET プロジェクトに組み込める実行可能な C# コンソールアプリが手に入ります。

## What You’ll Need

- **.NET 6.0 以降**（コードは .NET Core と .NET Framework のどちらでも動作します）  
- **Aspose.OCR for .NET** NuGet パッケージ (`Aspose.OCR`) – 無料トライアルキーは Aspose のサイトで入手可能です。  
- 韓国語テキストを含むサンプル画像（例: `korean_book_page.jpg`）。  
- お好みの開発環境（Visual Studio、VS Code、Rider – ここでは VS 2022 を使用）。

> **Pro tip:** 画像ファイルは `Resources/` のような専用フォルダに入れておくと、マシン間でパスが一貫します。

## Overview of the Process

1. **GPU サポート付き OCR エンジンを初期化** して高速化。  
2. **前処理フィルタを追加**（デスキュー、デノイズ）して認識精度を向上。  
3. **韓国語モデルをダウンロードしてロード** – 必要に応じて Aspose が自動で行います。  
4. **入力画像に対して認識を実行**。  
5. **組み込みエクスポーターで検索可能 PDF としてエクスポート**。  
6. **必要に応じて結果を JSON にシリアライズ** し、分析やロギングに活用。

以下で各ステップを詳しく解説し、*why* が重要かを説明し、コピー＆ペーストできる正確なコードを提示します。

---

## ## Convert Image to PDF – Full Workflow

以下のスニペットは *complete* プログラムです。新しいコンソールプロジェクト（`dotnet new console -n OcrPdfDemo`）を作成し、生成された `Program.cs` をこのコードに置き換えてください。

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

### Why This Works

- **GPU 加速** により、CPU のみモードに比べて認識時間が約半分に短縮されます。  
- **Deskew** と **Denoise** は古典的な *preprocess image for OCR* 手法で、スキャン時の歪みやノイズを除去し、エンジンが文字を見逃すのを防ぎます。  
- **言語モデルのロード** は **recognize Korean text image** に不可欠です。韓国語モデルが無いとエンジンは汎用ラテン文字にフォールバックし、意味不明な結果になります。  
- **SearchablePdfExporter** は元のビットマップと不可視のテキストレイヤーを組み合わせ、**create searchable pdf image** の結果を提供し、任意の PDF ビューアでインデックス可能にします。

---

## ## Preprocess Image for OCR – Tips & Tricks

追加フィルタが必要になることもあります。以下はよくある問題と対処法です。

| 問題 | 追加フィルタ | 追加方法 |
|------|--------------|----------|
| コントラストが低い | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 背景ノイズが多い | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 画像の向きが混在（縦横） | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** フィルタを増やしすぎると処理が遅くなります。スケールアップする前に、単一ページで各変更をテストしてください。

---

## ## Recognize Korean Text Image – Common Pitfalls

韓国語はハングル音節が密集しているため、出力が乱れることがあります。

1. **言語モデルが完全にダウンロードされているか確認** – コンソールに “Downloading Korean model…” のようなメッセージが表示されます。  
2. スキャンが 12° を超えて回転している場合は、`DeskewFilter` の `MaxAngle` を増やす。  
3. `ocrEngine.GpuMemoryLimit = 2048;`（単位は MB）で GPU メモリを増やす。

これらの調整は **recognize Korean text image** の成功率に直結します。

---

## ## Create Searchable PDF Image – Verifying the Result

プログラムが終了したら、`korean_page.pdf` を任意の PDF リーダー（Adobe Acrobat Reader、Foxit、Chrome など）で開きます。以下が確認できるはずです。

- マウスでテキストを **選択** できる（まるでネイティブ PDF のよう）。  
- PDF の検索ボックスで韓国語の単語を **検索** できる。  

テキストレイヤーが空白の場合は、`Export` メソッドに正しい画像パスが渡されているか、OCR 結果の `RecognitionResult.Text` が空でないかを再確認してください。

---

## ## Full JSON Output – What to Expect

コンソールには整形された JSON ペイロードが出力されます。例として以下のようにトリミングされたものがあります。

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

この JSON を downstream サービス（インデックスパイプライン、翻訳 API など）にそのまま渡すことで、OCR を再実行する必要がなくなります。

---

## ## Troubleshooting & FAQ

**Q: My PDF is huge compared to the original image.**  
A: エクスポーターは元のビットマップをそのまま埋め込むため、サイズが大きくなります。サイズが問題になる場合は、認識前に画像をダウンサンプルしてください。

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: The OCR returns empty strings.**  
A: 画像パスが正しいか、ファイルが破損していないかを確認してください。また、GPU ドライバが最新であることも重要です。古いドライバはサイレント失敗を引き起こすことがあります。

**Q: Can I process multiple pages in a loop?**  
A: もちろん可能です。ステップ 4‑6 を以下のように `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` ループで囲み、出力 PDF のパスを適宜変更してください。

---

## ## Conclusion

私たちは **convert image to PDF** を実現し、検索可能なテキストを保持しました。すべては Aspose OCR の強力なパイプラインのおかげです。**preprocess image for OCR** で精度を上げ、**recognize Korean text image** で複雑なスクリプトに対応し、**create searchable pdf image** でポータブルかつインデックス可能な文書を手に入れました。

コードを取得して自分のスキャンに適用し、追加フィルタや言語モデルで実験してみてください。同じパターンは中国語、日本語、またはラテン系言語にも適用可能です – `LanguageModel.Korean` を適切な enum に置き換えるだけです。

質問があればコメントを残してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}