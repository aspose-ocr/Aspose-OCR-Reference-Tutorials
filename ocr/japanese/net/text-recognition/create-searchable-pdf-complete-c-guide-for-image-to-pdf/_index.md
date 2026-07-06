---
category: general
date: 2026-04-08
description: Aspose.OCR を使用して C# で検索可能な PDF を高速に作成し、PDF 画像の圧縮、フォントの埋め込み、テキスト画像の認識方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: ja
og_description: Aspose.OCRで高速に検索可能なPDFを作成しましょう。PDF画像の圧縮、フォントの埋め込み、テキスト画像の認識を1つのチュートリアルで学べます。
og_title: 検索可能なPDFの作成 – 完全C#ガイド
tags:
- Aspose.OCR
- C#
- PDF Generation
title: 検索可能PDFの作成 – 画像からPDFへの完全C#ガイド
url: /ja/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能な PDF の作成 – 完全 C# ガイド

スキャンした画像から **検索可能な PDF** を作成する必要がありますか？ 巨大な PNG を見つめて、軽量でテキスト検索可能なドキュメントに変える方法を考えたことがあるのはあなただけではありません。 良いニュースは、Aspose.OCR を使えば数行のコードで実現でき、さらに **PDF 画像の圧縮**、**PDF のフォント埋め込み**、そして **テキスト画像の認識** も簡単に学べます。

このチュートリアルでは、画像の読み込み、OCR の実行、PDF 保存オプションの調整、そして最終的に検索可能な PDF をディスクに書き出すまでの全プロセスを順を追って解説します。 最後まで読めば、任意の .NET プロジェクトにすぐ組み込めるメソッドと、後で遭遇するかもしれないエッジケースに対するプロ向けのヒントが手に入ります。

## 必要なもの

- **.NET 6+**（コードは .NET Framework 4.7 でも動作しますが、モダン構文のため .NET 6 を対象にします）。  
- **Aspose.OCR for .NET** – NuGet でインストール: `Install-Package Aspose.OCR`。  
- テキストを検索可能にしたい画像ファイル（PNG、JPEG、TIFF）。  
- 多少の好奇心 – あとは以下でカバーします。

> **Pro tip:** 数十ページを処理する予定がある場合は、言語データの読み込みオーバーヘッドを避けるために単一の `OcrEngine` インスタンスを再利用することを検討してください。

## ステップ 1: OCR エンジンの設定 – テキスト画像の認識

最初に必要なのは、ソースビットマップから文字を読み取れる OCR エンジンです。Aspose.OCR では言語（English、French など）を指定でき、`OcrResult` オブジェクトが生のテキストと画像データの両方を返します。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**この設定が重要な理由:**  
- 言語を設定することで精度が劇的に向上します。エンジンはバックグラウンドで言語固有の辞書をロードします。  
- `OcrResult` は抽出された文字列だけでなく、元のビットマップも保持しているため、後で PDF に埋め込んで元のスキャンと見た目を一致させることができます。

## ステップ 2: PDF 保存オプションの構成 – PDF 画像の圧縮とフォント埋め込み

検索可能な PDF は、スキャン画像の上に見えないテキスト層を重ねた通常の PDF です。圧縮を無視すると最終ファイルが非常に大きくなります。`PdfSaveOptions` クラスを使うと、画像品質、フォント埋め込み、フォントのサブセット化などを細かく制御できます。

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**フォントを埋め込むべき理由:**  
PDF を開くシステムに OCR 層で使用されたフォントがインストールされていない場合、テキストが文字化けして表示されることがあります。フォントを埋め込むことで、プラットフォームを問わず視覚的な忠実度が保証され、法的文書やアーカイブに必須です。

## ステップ 3: 結果を検索可能な PDF として保存 – 画像から検索可能な PDF へ

ここまでの要素をすべて結び付けます。`OcrResult` に `PdfSaveOptions` を適用し、ファイルを書き出します。`SaveAsSearchablePdf` メソッドが本質的な処理を行い、OCR 出力に合わせた隠しテキストオーバーレイを作成しつつ、元の画像はそのまま保持します。

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### 完全な動作例

以下は新規 .NET コンソールプロジェクトにコピペできる、自己完結型のコンソールプログラムです。画像は実行ファイルからの相対パスで `YOUR_DIRECTORY` フォルダーにあるものと想定しています。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

プログラムを実行すると `output.pdf` が生成され、Adobe Reader、Foxit、または任意の PDF ビューアで開き、元は画像だけだったテキストを即座に検索できるようになります。

## ステップ 4: 出力の確認 – 検索は機能しますか？

ファイル生成後に開き、組み込みの検索（Ctrl + F）を試してください。`invoice`、`date`、`total` などの単語が見つかれば、**検索可能な PDF** の作成に成功しています。

検索で何もヒットしない場合は以下を確認してください:

1. **OCR 精度の確認** – ソース画像が低解像度の場合があります。OCR 前に DPI を上げることを検討してください（Aspose ではエンジンの `Resolution` を設定可能です）。  
2. **フォント埋め込みの確認** – PDF のプロパティで *Fonts* タブを開き、埋め込まれたフォントが一覧に表示されているか確認します。  
3. **画像圧縮の確認** – `ImageQuality` を極端に低く設定すると、視覚層が読めなくなり、下流ツールが混乱することがあります。

## 一般的なバリエーションとエッジケース

| シナリオ | 調整すべき点 | 理由 |
|----------|----------------|-----|
| **マルチページ TIFF** | 各フレームをループし、ページごとに `RecognizeImage` を呼び出し、`PdfSaveOptions` の `AppendMode = true` を使用します。 | 各スキャンページを個別の検索可能ページとして保持します。 |
| **非英語言語** | `Language = "fr"`（または適切な ISO コード）に変更し、必要に応じてカスタム辞書を提供します。 | アクセント付き文字や言語固有の字形の認識精度が向上します。 |
| **非常に大きな画像** | OCR 前にビットマップを縮小します（`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`）。 | メモリ使用量を削減し、精度を大きく損なわずに OCR を高速化します。 |
| **OCR 信頼度が必要** | `ocrResult.RecognizedWords` にアクセスし、`Confidence` プロパティを確認します。 | 信頼度の低い単語を手動レビュー用にフラグ付けできます。 |

## パフォーマンスのヒント

- バッチ処理時は **`OcrEngine` を再利用** すると、言語データがキャッシュされて高速化します。  
- マルチコア環境では `Parallel.ForEach` を使って認識ステップを並列化できますが、PDF の書き込みは競合を避けるために順次実行してください。  
- `ImageQuality` の調整: 85‑90 でほぼロスレスな画像、60‑70 でテキスト中心の文書には十分です。

## 結論

Aspose.OCR を使用して画像から **検索可能な PDF** を作成する方法、さらに **PDF 画像の圧縮**、**PDF のフォント埋め込み**、そして効率的な **テキスト画像の認識** についてすべて解説しました。 完全なコードサンプルは任意の C# プロジェクトにそのまま組み込めますし、追加のヒントにより大規模なワークロードや別言語への対応も容易です。

次のステップに進む準備はできましたか？ ウォーターマークの追加、複数の検索可能 PDF の結合、またはこの処理を Web API に統合してユーザーがスキャンをアップロードし即座に検索可能な PDF を受け取れるようにするなど、可能性は無限です。 基礎ができていれば、ワークフローの拡張は簡単です。

Happy coding, and may your PDFs stay tiny, searchable, and perfectly rendered!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}