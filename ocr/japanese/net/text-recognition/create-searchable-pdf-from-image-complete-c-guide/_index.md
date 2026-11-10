---
category: general
date: 2026-02-13
description: Aspose.OCR を使用して画像から検索可能な PDF を作成します。画像を PDF に変換し、画像からテキストを抽出し、PDF にフォントを埋め込み、PNG
  からテキストを認識する方法を学びます。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: ja
og_description: Aspose.OCR を使用して画像から検索可能な PDF を作成します。このガイドでは、画像を PDF に変換し、フォントを埋め込み、PNG
  からテキストを簡単に抽出する方法を示します。
og_title: 画像から検索可能なPDFを作成 – ステップバイステップ C# チュートリアル
tags:
- C#
- OCR
- Aspose
- PDF generation
title: 画像から検索可能なPDFを作成する – 完全C#ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から検索可能なPDFを作成 – 完全なC#ガイド

スキャンしたPNGから**検索可能なPDFを作成**したいと思ったことはありませんか？でもどこから始めればいいか分からないという方は多いです。請求書のデジタル化や古いマニュアルのアーカイブなど、多くのプロジェクトで画像を実際に検索できるPDFに変換できることは大きな変化をもたらします。  

このチュートリアルでは、**画像をPDFに変換**し、**画像からテキストを抽出**し、必要なフォントを埋め込み、最終的に完全に検索可能なPDFファイルを作成する手順を正確に解説します。曖昧な参照は一切なく、今日すぐにVisual Studioにコピーペーストできる完全な実行例を提供します。

> **得られるもの:** `input.png` を読み込み、OCR を実行し、フォントを埋め込み、元のラスタ画像を背景として保持し、`output.pdf` として書き出す C# コンソールアプリです。最後まで読めば、各行が *なぜ* 必要なのか、そして自分のシナリオに合わせてどう調整すればよいかが理解できます。

---

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Framework 4.7+ でも動作します）。  
- Aspose.OCR for .NET – NuGet から取得できます（`Install-Package Aspose.OCR`）。  
- フォルダー内に配置したサンプル PNG 画像（`input.png`）。  
- C# コンソールプロジェクトの基本的な知識（未経験の場合は Visual Studio → **Create a new project** → **Console App** → **C#** を開くだけで OK）。

> **ヒント:** Aspose は無料トライアルライセンスを提供しています。`.lic` ファイルを実行ファイルの隣に配置すれば、透かしなしでライブラリが動作します。

---

## ステップ 1: OCR エンジンの設定 – PNG からテキストを認識

まず必要なのは、PNG ファイル内の文字を実際に読み取れる OCR エンジンです。Aspose.OCR を使えばこの作業はシンプルです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**この設定が重要な理由:**  
`Language` を設定すると、エンジンが期待すべき文字セットを認識します。これを省略すると、エンジンは汎用モードになり、アクセント付き文字や数字を誤認識する可能性があります。多言語ドキュメントの場合は、`OcrLanguage.English | OcrLanguage.French` のようにカンマ区切りで指定できます。

---

## ステップ 2: 画像を読み込み認識 – 画像からテキストを抽出

エンジンの準備ができたら、処理したい PNG を渡します。

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**内部で何が起きているか:**  
`RecognizeImage` がビットマップを走査し、テキストブロックを特定して結果を `ocrEngine` に格納します。生の文字列だけが必要な場合は `ocrEngine.Text` にアクセスできますが、検索可能な PDF を作成する場合は Aspose に変換を任せます。

> **エッジケース:** PNG が非常に大きい（10 MB 超）とメモリ不足になることがあります。その場合は画像をリサイズするか、`OcrEngine.RecognizeImage(Stream)` を使ってストリーム処理してください。

---

## ステップ 3: PDF エクスポートオプションの設定 – PDF にフォントを埋め込む

フォントが埋め込まれていない検索可能な PDF は実用的ではありません。必要なフォントが無い環境では文書が崩れて表示されます。Aspose ではシンプルなオプションオブジェクトでこの設定を切り替えられます。

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**フォントを埋め込む理由:**  
`EmbedFonts` が `true` の場合、PDF はフォントデータをファイル内部に保持します。これにより、Chrome、Adobe Reader、モバイルアプリなど、どのビューアでもフォントが無くても正しく表示されます。

**`KeepOriginalImage` を `false` に設定するのはいつ？**  
抽出したテキストだけが必要で、ファイルサイズを小さくしたい場合は、このオプションをオフにすると背景画像が除去され、テキストのみの「クリーン」な PDF が生成されます。

---

## ステップ 4: 検索可能なPDFへエクスポート – 画像をPDFに変換

OCR 結果と PDF オプションが揃ったら、最後の一行で検索可能な PDF をディスクに書き出します。

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**期待される結果:**  
任意のビューアで `output.pdf` を開くと、テキストを選択・コピーでき、`Ctrl + F` で検索も可能です。元はピクセルだけだった PNG の文字列が検索できるようになります。

---

## 完全な動作例

以下はすぐにコンパイルして実行できる完全なプログラムです。`YOUR_DIRECTORY` を `input.png` があるフォルダーに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**コンソールに期待される出力:**

```
Searchable PDF created.
```

`output.pdf` を開き、`input.png` に含まれることが分かっている単語で検索してみてください。ハイライトされれば、画像から**検索可能なPDFを作成**できています。

---

## よくある質問とプロのコツ

### 「1回の実行で複数の画像を処理できますか？」

もちろんです。認識とエクスポートのロジックをループで囲み、`Directory.GetFiles(..., "*.png")` などで画像を取得します。その際、各 PDF にユニークな名前を付けることを忘れずに、例: `Path.GetFileNameWithoutExtension(img) + ".pdf"`。

### 「ドキュメントに英語とスペイン語の両方が含まれている場合は？」

言語プロパティに複合フラグを設定します:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### 「PDFファイルが大きすぎます—どうやって縮小できますか？」

簡単な 2 つの手法:

1. `pdfOptions.KeepOriginalImage = false` に設定してラスタ背景を除去。  
2. `pdfOptions.ImageCompression = ImageCompression.Jpeg;`（プロパティを追加する必要があります）で埋め込み画像を圧縮。

### 「本番環境でライセンスが必要ですか？」

トライアルはテストには十分ですが、商用展開する場合はライセンスを購入し、アプリ起動時に早めに登録する必要があります:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## ソリューションの拡張

**検索可能なPDFを作成**できるようになったので、次のような拡張も検討できます:

- **ウォーターマークの追加** – OCR 後に Aspose.PDF の `PdfDocument` を使ってテキストをオーバーレイ。  
- **PDF のバッチ処理** – `PdfFileEditor` を使って複数の検索可能 PDF を 1 つに結合。  
- **Azure Blob Storage との統合** – 画像と PDF のストリームをクラウド上で直接読み書きし、ローカル I/O を排除。

これらの拡張はすべて同じパターンに従います。OCR 結果を取得し、次のライブラリを設定し、操作をチェーンするだけです。

---

## 結論

Aspose.OCR を使って PNG 画像から **検索可能なPDF** を作成する方法を学びました。OCR エンジンの初期化、テキスト認識、`SearchablePdfOptions` で **PDF にフォントを埋め込む** 設定、そしてエクスポートの手順を踏むことで、元画像と見た目は同じでも完全に検索可能なファイルが得られます。  

ここからはバッチ変換や別言語対応、圧縮率の調整など、ワークフローに合わせて自由に実験してください。問題が発生した場合は Aspose のフォーラムや API ドキュメントが有力な情報源です。上記の手順さえ押さえておけば、典型的なユースケースの 90 % はカバーできます。

コーディングを楽しんで、PDF が常に検索可能でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}