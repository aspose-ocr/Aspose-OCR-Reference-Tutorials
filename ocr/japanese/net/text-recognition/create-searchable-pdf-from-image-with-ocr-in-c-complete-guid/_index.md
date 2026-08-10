---
category: general
date: 2026-05-21
description: C#でAspose OCRを使用して画像から検索可能なPDFを作成します。画像をPDFに変換し、PDFの解像度を設定し、元の画像を埋め込みます。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- set pdf resolution
- pdf with embedded image
language: ja
og_description: C#でAspose OCRを使用して画像から検索可能なPDFを作成します。画像をPDFに変換し、PDFの解像度を設定し、元の画像を埋め込む方法を学びましょう。
og_title: C#でOCRを使用して画像から検索可能なPDFを作成
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF from an image using Aspose OCR in C#. Convert
    image to PDF, set PDF resolution, and embed the original image.
  headline: Create Searchable PDF from Image with OCR in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- PDF
title: C#でOCRを使用して画像から検索可能なPDFを作成する完全ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-with-ocr-in-c-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像から OCR を使って検索可能な PDF を作成する – 完全ガイド

スキャンした請求書、領収書、手書きメモから **検索可能な PDF** を作成したことがありますか？ あなた一人だけではありません。開発者はドキュメント管理パイプラインを構築する際にこの壁に頻繁に直面します。良いニュースは、Aspose.OCR を使えば **画像を PDF に変換** し、元の画像を埋め込み、出力 DPI も数行の C# コードで制御できることです。

このチュートリアルでは、シンプルな PNG を **検索可能な PDF** に変換する一連の手順を解説します。**画像を PDF に OCR** する方法、**PDF の解像度を設定**する方法、そして元画像をファイル内に保持する方法を学びます。最後には、任意の .NET プロジェクトに貼り付けられるコードスニペットが手に入ります。

## 前提条件

- .NET 6.0 以降（API は .NET Core と .NET Framework の両方で動作）
- Aspose.OCR のライセンスまたは無料評価キー
- アプリが読み取れる場所に置いたサンプル画像（例: `invoice.png`）
- Visual Studio、Rider、またはお好みのエディタ

`Aspose.OCR` 以外の NuGet パッケージは不要です。残りはすべて .NET の基本クラスライブラリに含まれます。

<img src="/images/searchable-pdf-example.png" alt="Create searchable PDF example in C#" />

## 手順 1: OCR エンジンの初期化 – プロセスの中心

まずは `OcrEngine` インスタンスを作成し、認識させる言語を指定します。英語は多くの請求書で十分ですが、任意の `OcrLanguage` 列挙値に置き換え可能です。

```csharp
using Aspose.OCR;

// Step 1 – create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English   // Change if you need another language
};
```

**重要ポイント:** エンジンはピクセルデータを読み取り、検索可能なテキストに変換する作業馬です。言語を事前に設定しておくことで、特にラテン文字以外のスクリプトで精度が大幅に向上します。

## 手順 2: ソース画像の読み込み – ディスクからメモリへ

次に、処理したい画像ファイルをエンジンに渡します。Aspose は生の `FileStream` の煩雑さを隠す `ImageStream.FromFile` ヘルパーを提供しています。

```csharp
using Aspose.OCR;

// Step 2 – load the image containing the text
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");
```

**ヒント:** 画像がクラウドバケットにある場合や HTTP リクエストから取得した場合は、`ImageStream.FromStream` に `MemoryStream` を渡すこともできます。OCR エンジンはバイトの出所を気にしません。

## 手順 3: PDF 保存オプションの設定 – 画像埋め込みと解像度指定

ここで Aspose に最終 PDF の形を指示します。**検索可能な PDF** に必須の2つのオプションがあります。

1. `EmbedOriginalImage = true` – スキャン画像を PDF 内に保持し、視覚的忠実度を保ちます。
2. `OutputResolution = 300` – 検索レイヤーの DPI を指定します。300 DPI は多くの OCR タスクでバランスの取れた設定です。

```csharp
using Aspose.OCR.Pdf;   // PDF‑specific options

// Step 3 – define how the PDF should be saved
var pdfOptions = new PdfSaveOptions
{
    EmbedOriginalImage = true,   // Keeps the original image inside the PDF
    OutputResolution = 300       // DPI of the searchable PDF (set PDF resolution)
};
```

**なぜこの設定か？** 元画像を埋め込む（`pdf with embedded image`）ことで、文書はスキャンそのものと同じ外観になります。一方 OCR テキストレイヤーが検索可能性を提供します。ファイルサイズを抑えたい場合は 150 DPI、精度を上げたい場合は 600 DPI へ調整してください。

## 手順 4: 結果の保存 – OCR エンジンから検索可能 PDF へ

最後に、出力ファイルのパスと先ほど作成した `PdfSaveOptions` を渡して `Save` を呼び出します。この一行で OCR 実行、隠しテキストレイヤー作成、PDF 書き出しという重い処理が完了します。

```csharp
// Step 4 – generate the searchable PDF
ocrEngine.Save("YOUR_DIRECTORY/invoice_searchable.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created.");
```

**得られるもの:** `invoice_searchable.pdf` という名前のファイル。見た目は元の `invoice.png` と同じですが、Windows Search、Adobe Reader の検索機能、あるいは任意の全文検索エンジンでインデックス可能です。

## 手順 5: 出力の検証 – 手軽にできるチェック

コード実行後、Adobe Acrobat（または任意のビューア）で PDF を開き、請求書に必ず含まれる単語（例: “Total”）を検索してみてください。検索結果がヒットすれば **ocr image to PDF** に成功です。

またファイルサイズも確認しましょう。**元画像を埋め込んでいる**ため、テキストのみの PDF より大きくなりますが、視覚的忠実度とのトレードオフは妥当です。

## よくある落とし穴とプロのコツ

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank PDF** | `ocrEngine.Image` が設定されていない、またはパスが間違っている | ファイルパスを再確認し、例外が出ないことを確認 |
| **Poor Search Accuracy** | `OutputResolution` が低すぎる、または言語設定が間違っている | `OutputResolution` を 300‑600 DPI に上げ、正しい `OcrLanguage` を設定 |
| **File Too Large** | 高解像度スキャンで `EmbedOriginalImage = true` を使用している | エンジンに渡す前に画像をダウンサンプリングするか、テキストだけが必要な場合は `EmbedOriginalImage = false` に変更 |
| **License Exceptions** | 無料トライアルキーなしで使用している | Aspose から一時ライセンスキーを取得し、エンジン作成前に `License license = new License(); license.SetLicense("Aspose.OCR.lic");` を呼び出す |

## 完全動作サンプル – コピー＆ペーストで実行

以下は即コンパイル可能なコンソールアプリです。`YOUR_DIRECTORY` を実際のフォルダに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑specific options

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image (convert image to PDF later)
            string inputPath = @"YOUR_DIRECTORY\invoice.png";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Set PDF options – embed image & set PDF resolution
            var pdfOptions = new PdfSaveOptions
            {
                EmbedOriginalImage = true,
                OutputResolution = 300 // DPI – you can change this to set PDF resolution
            };

            // 4️⃣ Save as searchable PDF
            string outputPath = @"YOUR_DIRECTORY\invoice_searchable.pdf";
            ocrEngine.Save(outputPath, pdfOptions);

            Console.WriteLine("Searchable PDF created at:");
            Console.WriteLine(outputPath);
        }
    }
}
```

**期待されるコンソール出力**:

```
Searchable PDF created at:
C:\Your\Path\YOUR_DIRECTORY\invoice_searchable.pdf
```

生成された PDF を開き、検索機能をテストしてください。これで **検索可能な PDF** を画像から作成できました。

## まとめ

Aspose OCR を使って C# で **検索可能な PDF** を作成するために必要な手順をすべて網羅しました。画像の読み込み、**PDF with embedded image** オプションの設定、**PDF 解像度の指定**、そして **OCR 結果の保存** まで、数行のコードで完結します。

次のステップは？ 複数の請求書をバッチ処理したり、別言語に挑戦したり、アップロードをリアルタイムで処理する ASP.NET Core API に組み込んでみましょう。さらに Aspose.PDF が提供する透かしやデジタル署名機能を使って、文書の堅牢性を高めることも可能です。

ライセンスやパフォーマンス調整、エッジケースに関する質問があればコメントで教えてください。Happy coding!

## 関連チュートリアル

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}