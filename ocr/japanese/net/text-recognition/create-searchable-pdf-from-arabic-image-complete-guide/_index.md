---
category: general
date: 2026-02-11
description: C#でアラビア語画像から検索可能なPDFを作成する。画像をPDFに変換し、アラビア語テキストを抽出し、Aspose OCRを使用して隠しテキストを追加する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: ja
og_description: Aspose OCR を使用して C# でアラビア語画像から検索可能な PDF を作成します。このガイドに従って画像を PDF に変換し、アラビア語テキストを抽出し、隠しテキストを埋め込みます。
og_title: アラビア語画像から検索可能なPDFを作成 – ステップバイステップ
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: アラビア語画像から検索可能なPDFを作成する – 完全ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

codes.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# アラビア語画像から検索可能なPDFを作成する – 完全ガイド

スキャンしたアラビア語の請求書から **検索可能なPDF** を作成したいが、元の外観を保ちつつテキストを選択可能にする方法が分からないことはありませんか？ あなたは一人ではありません。多くの文書自動化プロジェクトでは、画像をPDFに変換するだけでなく、ビジュアルレイアウトを保持し、検索エンジンがインデックスできる隠しテキスト層を追加することが課題となります。

このチュートリアルでは、**画像をPDFに変換**、Aspose OCR を使用した **アラビア語テキストの抽出**、そして最終的に **隠しテキスト付きPDF** としてテキストを埋め込むという全工程を順を追って解説します。最後まで読めば、任意の .NET ソリューションに組み込める使い勝手の良い C# スニペットが手に入ります。外部サービスは不要で、すでにお持ちの Aspose ライブラリだけで完結します。

## 必要なもの

- .NET 6 以降（コードは .NET Core でも動作します）  
- **Aspose.OCR** と **Aspose.Pdf** NuGet パッケージ（2026年2月時点の最新バージョン）  
- 検索可能なPDFに変換したいアラビア語画像ファイル（例: `arabic_invoice.jpg`）  
- 少しの C# 知識 – 概念はシンプルですが、各行の「なぜ」を丁寧に説明します。

> **Pro tip:** まだ NuGet パッケージを追加していない場合は、プロジェクトフォルダーで以下を実行してください  
> `dotnet add package Aspose.OCR`  
> `dotnet add package Aspose.Pdf`

前提条件が整ったので、ステップバイステップの実装に入りましょう。

## ステップ 1 – アラビア語テキスト用 OCR エンジンの設定

最初に行うべきことは、Aspose OCR がアラビア文字を認識できるように構成することです。アラビア語は右から左へ書くスクリプトなので、エンジンにロードすべき言語を指定し、言語データがマシンに存在しない場合に自動でリソースをダウンロードする設定を有効にする必要があります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**なぜ重要か:**  
`Language = OcrLanguage.Arabic` の設定を省略すると、エンジンはデフォルトで英語を使用し、文字化けした結果になります。`AutomaticResourceDownload` を有効にすれば、言語ファイルを手動で配置する手間が省けます。

## ステップ 2 – ソース画像の読み込み

次に、アラビア語テキストが含まれる画像を読み込みます。`Image.FromFile` を使用すると、画像が GDI+ の `Image` オブジェクトとして読み込まれ、Aspose OCR が期待する形式になります。

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**エッジケース:** 画像が非常に大きい（例: スキャンした A3 ページ）場合は、パフォーマンス向上のために先に縮小することを検討してください。OCR エンジンは大容量ファイルを処理できますが、メモリ使用量が急激に増加します。

## ステップ 3 – アラビア語テキストの認識と結果の取得

いよいよ OCR を実行します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、検出されたテキスト、信頼度スコア、バウンディングボックス（高度なレイアウト解析が必要な場合に使用）を含みます。

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**プレビューを保持する理由:**  
抽出されたテキストの一部を確認することで、言語パックが正しくロードされたかを PDF 生成前に検証できます。

## ステップ 4 – 新規 PDF ドキュメントの作成と空白ページの追加

テキストが取得できたら、PDF の構築を開始します。Aspose PDF の `Document` オブジェクトがファイル全体を表し、ページを追加することで元画像と隠しテキスト層を配置するキャンバスが得られます。

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**注意:** マルチページの TIFF や PDF を処理する場合は複数ページを追加できますが、単一画像の場合は 1 ページで十分です。

## ステップ 5 – 背景要素として元画像を挿入

最終的な PDF がスキャンした請求書と全く同じ外観になるよう、画像を可視の背景として埋め込みます。Aspose PDF の `Image` クラスはストリームを受け取るため、ファイルを `MemoryStream` に読み込みます。

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**背景画像を使用する理由:**  
画像をページ上に直接配置することで、元のレイアウト・色・スタンプやロゴなど、OCR エンジンが無視しがちな要素をすべて保持できます。

## ステップ 6 – OCR テキストを隠し層として追加

**検索可能なPDF** の鍵は、画像の上に重ねる隠しテキスト層です。フォントサイズを `0` に設定すれば、人間の目には見えませんが、テキストは選択・検索可能なままです。

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**重要なポイント:**  
OCR が座標情報を返す場合は、`TextFragmentAbsorber` を使って各フラグメントを手動で配置できます。多くの請求書では、ページ全体に重ねるシンプルなオーバーレイで十分です。

## ステップ 7 – 検索可能な PDF の保存

最後に PDF をディスクに書き出します。出力ファイルは視覚的な画像と隠しアラビア語テキストの両方を含み、Adobe Reader、Google Drive、または OCR 対応ビューアで完全に検索可能になります。

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### 完全な動作例

すべてのパーツを組み合わせた、実行可能な完全プログラムは以下の通りです：

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**期待される結果:** 生成された `arabic_invoice_searchable.pdf` を任意の PDF ビューアで開き、**Ctrl + F** を押して元の請求書に含まれるアラビア語の単語を入力します。テキスト層が見えなくても、ビューアは該当単語を正しくハイライトします。

## よくある質問と落とし穴

- **他の言語でも同様に動作しますか？**  
  はい。`Language = OcrLanguage.YourLanguage` に変更し、該当言語パックが利用可能であることを確認すれば、パイプラインはそのまま使用できます。

- **OCR の信頼度が低い場合は？**  
  `ocrResult.Confidence`（0〜1 の値）を確認します。しきい値（例: 0.75）を下回る場合は、画像の前処理（デスキュー、コントラスト向上、グレースケール変換）を行ってからエンジンに渡すことを検討してください。

- **複数画像を 1 つの PDF にまとめられますか？**  
  できます。画像パスのコレクションをループし、各画像ごとに新しいページを追加してステップ 5‑6 を繰り返します。その際、各画像の GDI リソース解放のために `using` ブロックを忘れずに保持してください。

- **隠しテキストは本当に見えなくなりますか？**  
  `FontSize = 0` に設定すればほとんどのビューアでテキストは不可視になります。もしビューアが薄く文字を表示する場合は、テキスト色を完全に透明に設定できます（`TextState.FillColor = Color.Transparent`）。

## 次のステップ

アラビア語画像から **検索可能なPDF** を作成できるようになったので、以下のトピックを検討してみてください：

- **バッチ処理** – フォルダー内のすべての画像を読み取り、ファイルごとに単一の検索可能 PDF を生成する。  
- **OCR 座標の活用** – `OcrResult.Regions` を使用して各テキストフラグメントを正確な位置に配置し、複雑なレイアウトでも検索精度を向上させる。  
- **PDF の暗号化** – Aspose PDF でパスワードやデジタル署名を追加し、セキュリティを強化する。  
- **Azure Blob Storage との統合** – 生成した PDF を直接クラウドに保存し、下流のワークフローで活用する。

Each of those topics naturally involves the secondary keywords **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}