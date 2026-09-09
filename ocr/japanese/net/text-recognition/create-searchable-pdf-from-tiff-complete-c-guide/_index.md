---
category: general
date: 2025-12-30
description: C#で画像から検索可能なPDFを作成 – TIFFをPDFに変換し、画像からテキストを抽出し、PDF作成を自動化する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: ja
og_description: C#でAspose OCRを使用して画像から検索可能なPDFを作成します。このガイドでは、TIFFをPDFに変換し、テキストを抽出し、PDF/A‑1b準拠を確保する方法を示します。
og_title: TIFFから検索可能なPDFを作成 – ステップバイステップ C# チュートリアル
tags:
- Aspose OCR
- C#
- PDF generation
title: TIFFから検索可能なPDFを作成する – 完全C#ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFFから検索可能なPDFを作成 – 完全なC#ガイド

スキャンしたTIFFから**検索可能なPDFを作成**したいと思ったことはありませんか？でも、どこから始めればいいか分からないことも多いでしょう。アーカイブやコンプライアンスのために検索可能なPDFが必要な開発者は多く、良いニュースは、Aspose OCR を使えば解決策は驚くほどシンプルです。

このチュートリアルでは、画像をPDFに変換し、画像からテキストを抽出し、PDF/A‑1b 標準に準拠した出力に仕上げる手順を解説します。最後まで読むと、**tiff を pdf に変換**し、**画像からテキストを抽出**し、検索可能でアーカイブ対応の**pdf を作成する方法**が正確に分かります。

## 必要なもの

- .NET 6 (または最近の .NET バージョン) – コードは .NET Core と .NET Framework の両方で動作します。  
- Aspose.OCR NuGet パッケージ – `dotnet add package Aspose.OCR` でインストールします。  
- 検索可能な PDF に変換したいサンプル TIFF ファイル (`input.tif`)。  
- 開発環境 (Visual Studio、VS Code、Rider など、どれでも可)。  

以上です。追加の SDK や外部サービス、隠れた設定手順は不要です。

![Create searchable PDF example](image-placeholder.png "Create searchable PDF preview")

## ステップ 1 – OCR エンジンの初期化と英語モデルのロード

画像を検索可能なテキストに変換する前に、OCR エンジンは対象言語を認識する必要があります。Aspose OCR には必要に応じてロードできる言語パックが同梱されています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**この重要性:** 正しい言語モデルをロードすることで認識精度が大幅に向上します。このステップを省略するとエンジンは汎用モデルにフォールバックし、特に低解像度の TIFF では文字化けしやすくなります。

## ステップ 2 – ソース画像からテキストを認識 (任意だが便利)

OCR を実行すると `OcrResult` オブジェクトが取得でき、内容を検査したり、ログに記録したり、プレーンテキストとして保存したりできます。最終的な PDF のみが必要な場合はこのステップは任意ですが、デバッグには非常に便利です。

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**プロのコツ:** 抽出されたテキストが正しくない場合は、エンジンに渡す前に画像の前処理（デスキュー、デスペックル）を検討してください。Aspose OCR には画像強化ユーティリティもあり、ここでチェーンできます。

## ステップ 3 – 検索可能な PDF エクスポーターの設定

ここで Aspose に最終的な PDF の形を指示します。`SearchablePdfExporter` を使うと出力パスや PDF/A 準拠、その他いくつかのオプションを指定できます。

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**なぜ PDF/A‑1b?** 法務、医療、金融など多くの業界ではアーカイブ標準に準拠した PDF が求められます。`PdfACompliance` を設定するとフォントが埋め込まれ、色がデバイス非依存となり、検証ツールに合格します。

## ステップ 4 – OCR 結果を直接検索可能な PDF にエクスポート

エンジンとエクスポーターの準備ができたら、実際の処理は1行で完了します。エクスポーターは内部で PDF ページを作成し、認識されたテキストを不可視レイヤーとして重ね合わせ、ファイルを書き出します。

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**内部で何が起きているか?**  
1. 元の TIFF がラスタ画像として埋め込まれます。  
2. OCR で得られたテキストが上に配置され、非表示ですが選択可能です。  
3. 言語などのメタデータが追加され、PDF リーダーがテキストをインデックスできるようになります。

## ステップ 5 – 出力の検証 (手動チェック + プログラムによる検証)

PDF が実際に検索可能であることを確認するのは常に良い習慣です。

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

PDF ビューアでテキストをコピー＆ペーストできる、または上記のコンソール出力にテキストが表示されていれば成功です。

## エッジケースと一般的なバリエーション

### 他の画像フォーマットへの変換

同じコードは PNG、JPEG、BMP でも動作します。`Recognize` と `Export` の呼び出しでファイル拡張子を変更するだけです。追加設定は不要です。

### マルチページ TIFF ファイル

Aspose OCR はマルチページ TIFF の各ページを自動的に処理し、エクスポーターはそれらをマルチページ PDF にまとめます。ページをスキップしたい場合は、エクスポート前に `ocrResult.Pages` をフィルタリングしてください。

### 非英語言語

`LanguageModel.English` を `LanguageModel.Spanish`、`LanguageModel.French` などに置き換えるか、カスタム言語パックをロードします。特定のロケールを対象にする場合は PDF メタデータも調整してください。

### PDF サイズの削減

TIFF が高解像度の場合、生成される PDF が大きくなることがあります。OCR 前に画像をダウンサンプリングできます：

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### パスワード保護された PDF の取り扱い

出力を保護したい場合は、エクスポート後に `SearchablePdfExporter` を Aspose.Pdf の暗号化 API でラップしてください：

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## 完全な動作例

以下は、上記ですべてのステップとオプションの調整を組み込んだ、完全なコピー＆ペースト可能なプログラムです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**期待される出力:**  
- コンソールに TIFF からの生 OCR テキストが表示されます。  
- `output.pdf` ファイルが `YOUR_DIRECTORY` に作成されます。  
- Adobe Reader で `output.pdf` を開くとテキストを選択・コピーでき、検索可能であることが確認できます。

## まとめ

本稿では、C# で Aspose OCR を使用して TIFF 画像から **検索可能な PDF** を作成するために必要なすべてを網羅しました。OCR エンジンの初期化、テキスト抽出、PDF/A 準拠の設定、最終文書の検証まで、各ステップを明確に解説しました。これで **画像を pdf に変換**、**tiff を pdf に変換**、**画像からテキストを抽出**、そして検索可能なレイヤーを持つ **pdf の作成方法** が分かります。

## 次に探求すべきこと

- **バッチ処理:** ロジックをループでラップし、数十枚の画像を自動的に処理します。  
- **カスタムフォント:** ブランド一貫性のために社内フォントを埋め込みます。  
- **クラウド統合:** 作成後に PDF を Azure Blob Storage や AWS S3 に直接保存します。  
- **UI フロントエンド:** 画像をドラッグ＆ドロップで即座に変換できるシンプルな WinForms/WPF アプリを構築します。

さまざまな言語モデル、DPI 設定、PDF/A レベルを試してみてください。API は非常に柔軟で、想像できるほぼすべてのワークフローに適応できます。

---

*コーディングを楽しんで、PDF が常に検索可能でありますように！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}