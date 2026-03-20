---
category: general
date: 2026-03-20
description: 検索可能なPDFをすばやく作成：画像をPDFに変換し、画像からテキストを抽出し、完全な検索性のために隠しテキスト層を追加する。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: ja
og_description: 画像をPDFに変換し、テキストを抽出して、C#で検索可能なPDFを作成し、即時検索用の隠しレイヤーを埋め込む。
og_title: 画像から検索可能なPDFを作成 – 完全なC#チュートリアル
tags:
- Aspose
- C#
- OCR
- PDF generation
title: C#で画像から検索可能なPDFを作成する – ステップバイステップガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像から検索可能な PDF を作成する – 完全ガイド

スキャンした請求書から **検索可能な PDF** を作成したいけど、手入力したくない、という経験はありませんか？ あなただけではありません。多くのオフィスワークフローで、ビットマップスキャンを実際に検索できる PDF に変換することは日常的な課題です。朗報です！ C# の数行と Aspose の OCR & PDF ライブラリさえあれば、手作業のコピー＆ペーストは不要で全自動化できます。

このチュートリアルでは、**画像を PDF に変換**し、画像からテキストを抽出し、テキストを目に見えないレイヤーとして重ね合わせ、最終的にネイティブ PDF のように動作するファイルを作る手順を解説します。最後まで読めば、請求書・契約書・領収書など、あらゆるスキャン文書に対して **隠しテキスト付き PDF** を構築できるようになります。

## 必要なもの

- .NET 6.0 以降（`using var` 文を使用しているため、比較的新しい SDK が便利です）
- Aspose.OCR と Aspose.Pdf の NuGet パッケージ（`Install-Package Aspose.OCR` と `Install-Package Aspose.Pdf`）
- テキストをインデックスしたいサンプル画像ファイル（PNG、JPG、または TIFF）
- Visual Studio 2022 もしくはお好みの IDE

> **プロのコツ:** 複数ページのスキャンを扱う場合は、各画像をループで処理すれば同じロジックがそのまま使えます。

---

## Step 1 – OCR エンジンの初期化（画像からテキストを抽出）

検索可能なテキストを埋め込む前に、画像から文字を実際に読み取る必要があります。Aspose の `OcrEngine` がその重い処理を担います。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**重要ポイント:** 正しい言語でエンジンを初期化すると精度が大幅に向上します。これを省略すると、特に数字の認識ミスが増え、財務文書では致命的です。

---

## Step 2 – スキャン画像の読み込み（画像を PDF に変換）

ビットマップをメモリにロードします。Aspose は `System.Drawing.Image` と直接連携できるため、.NET がサポートする形式なら何でも構いません。

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

**ヒント:** すでに **scan image to PDF** のワークフローでマルチページ TIFF が生成されている場合は、拡張子を変更し、各ページごとにこのロード処理を繰り返すだけです。

---

## Step 3 – OCR 実行と認識テキストの取得

画像の準備ができたら、OCR エンジンに処理を任せます。

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**エッジケース:** 画像の解像度が低い（300 dpi 未満）と信頼度が下がります。エンジンに渡す前に拡大するか、より高 DPI で再スキャンしてください。

---

## Step 4 – PDF を作成し、元画像を背景として配置

**隠しテキスト付き PDF** でも、スキャンのビジュアルは必要です。画像をページの背景として追加します。

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**背景に画像を使う理由:** ユーザーは元のスキャン（署名やスタンプを含む）をそのまま確認でき、隠しテキストレイヤーが検索機能を提供します。

---

## Step 5 – OCR テキストを不可視レイヤーとしてオーバーレイ（PDF with hidden text）

ここが肝心です。画像の上に `TextFragment` を配置し、可視性をオフにします。Aspose.Pdf なら簡単に実装できます。

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**解説:** フォントサイズを極小にし、フラグメントを hidden に設定することで、見た目は変わらず PDF のテキスト層に OCR 結果が保持されます。検索エンジンや PDF リーダーはこの層をインデックスします。

---

## Step 6 – 検索可能な PDF を保存

最後にドキュメントをディスクに書き出します。

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

生成されたファイルを Adobe Reader で開き、**Ctrl + F** で請求書に記載されていた単語を検索すると、テキストは見えないはずですがハイライトされます。

---

## 完全動作サンプル（全ステップ統合）

以下はコンソールアプリにそのまま貼り付けて実行できる完全プログラムです。NuGet パッケージがインストールされ、ファイルパスが正しければそのままコンパイル・実行できます。

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**期待される結果:**  
- `invoice_searchable.pdf` は `invoice.png` と見た目が同一です。  
- 元スキャンに含まれる任意の単語でテキスト検索が可能です。  
- ファイルサイズの増加はごくわずか（隠しテキストは数キロバイト程度）です。

---

## FAQ とエッジケース

### 複数ページを 1 つの PDF にまとめられますか？
可能です。`foreach (string imagePath in imageFiles)` ループで OCR と PDF のロジックを回し、各イテレーションで新しい `Page` を作成します。隠しテキストレイヤーはページ単位で追加されるため、文書全体で検索が機能します。

### 文書に複数言語が混在している場合は？
`ocrEngine.Language` を `Language.Multilingual` に設定するか、言語ごとに別々のエンジンをインスタンス化します。Aspose は混在言語の結果を返すので、同じ PDF ページにそのまま流し込めます。

### DPI や画像スケーリングはどう制御しますか？
PDF に画像を追加する前に、`System.Drawing` でリサイズできます。

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

リサイズ後の `resized` を PDF 画像コンストラクタに渡してください。

### 隠しテキストはすべてのビューアで本当に見えなくなりますか？
ほとんどの最新ビューアは `IsHidden` フラグを尊重します。もしテキストが表示されるビューアがある場合は、フォントサイズをさらに小さく（例: `0.01f`）するか、`TextState.FillColor = Color.Transparent` で完全に透明にしてください。

### セキュリティ面は？ PDF にパスワードを設定できますか？
できます。コンテンツ追加が完了したら以下を呼び出します。

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

これで検索可能な PDF も組織の機密ポリシーに合わせてパスワード保護できます。

---

## 本番環境向け実装のポイント

- **バッチ処理:** 大量画像は `Parallel.ForEach` で並列化できますが、`OcrEngine` はスレッド非安全なのでスレッドごとにインスタンスを作成してください。  
- **エラーハンドリング:** OCR 呼び出しは try/catch で囲み、`ocrResult.IsRecognized` を確認して失敗したページはスキップします。  
- **ロギング:** `ocrResult.Confidence` を記録し、低信頼度は画像前処理（デスケュー、デスペックル）を検討するシグナルにします。  
- **パフォーマンス:** 全ページで同じ `Document` オブジェクトを再利用し、ファイルのオープン/クローズを最小限に抑えます。  
- **テスト:** `pdfDocument.Pages[1].ExtractText()` で抽出したテキストを OCR 出力と比較し、切り捨てや欠落がないか検証します。

---

## 結論

C# と Aspose.OCR を組み合わせて、画像から **検索可能な PDF** を作成する方法をご紹介しました。画像からテキストを抽出し、PDF ページに不可視レイヤーとして重ね合わせて保存するだけで、見た目は元のスキャンと同一、機能はネイティブ PDF になるというワンストップのワークフローが完成します。これにより、従来の **convert image to PDF** プロセスに **pdf with hidden text** が加わり、実際に検索できる **scan image to PDF** が実現します。

次のステップに進みませんか？ フォルダ内の領収書を一括処理したり、検索可能 PDF をリアルタイムで返す Web API に組み込んだりしてみてください。フォントやメタデータの追加、OCR 信頼度を PDF アノテーションとして埋め込むなど、さらに応用の幅は広がります。

本ガイドが役立ったら、スターを付ける、チームと共有する、または独自の改善点をコメントで教えてください。Happy coding、そしてあなたの PDF が常に検索可能でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}