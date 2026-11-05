---
category: general
date: 2026-04-26
description: C#でAspose OCRを使用してスキャン画像から検索可能なPDFを作成します。スキャン画像の変換、テキスト抽出、検索可能なPDFの迅速な生成方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: ja
og_description: Aspose OCR を使用してスキャン画像から検索可能な PDF を作成します。変換、テキスト抽出、検索可能な PDF の生成を行うステップバイステップの
  C# コード。
og_title: スキャン画像から検索可能なPDFを作成 – C# ガイド
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: スキャン画像から検索可能なPDFを作成する – C# ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャン画像から検索可能なPDFを作成 – C# ガイド

紙の契約書、領収書、古いアーカイブから **検索可能なPDF** を作成したことがありますか？ あなただけではありません—多くの開発者が、クライアントから大量のTIFFスキャンが渡され、最終成果物として検索可能なPDFが求められるという壁にぶつかります。  

このチュートリアルでは、Aspose OCR for .NET を使用して **ドキュメントのOCR方法** を正確に示し、スキャン画像を **検索可能なPDF** に変換する方法を紹介します。最後までで、**スキャン画像** ファイルを **変換** し、**画像からテキストを抽出** でき、さらにマルチページTIFFも楽に扱えるようになります。

## 必要なもの

Before we dive in, make sure you have:

* .NET 6.0 以降（API は .NET Core、.NET Framework、.NET 5+ でも動作します）。  
* 有効な Aspose OCR ライセンス、または評価用の透かしで問題ない場合。  
* `Aspose.OCR` NuGet パッケージがインストール済み（`dotnet add package Aspose.OCR`）。  
* 例として `contract_scan.tif` のようなサンプル TIFF ファイルで、検索可能なPDFに変換したいもの。

以上です—追加のライブラリや面倒な設定は不要です。準備はいいですか？さあ始めましょう。

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## ステップ 1 – OCR エンジンの初期化 (検索可能なPDFの作成)

First thing’s first: you need an `OcrEngine` instance. This object is the workhorse that reads the bitmap, identifies characters, and hands you the text back.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**なぜ言語を設定するのか？**  
デフォルトのままにすると、Aspose はすべての言語パックを試すため処理が遅くなります。`Language.Latin` を指定すると、エンジンはラテン文字に集中し、英語の契約書に対して速度と精度が向上します。

## ステップ 2 – スキャン画像の読み込み (スキャン画像の変換)

Now we feed the engine the image we want to process. Aspose can read a file path, a stream, or even a `byte[]`. For simplicity we’ll use `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

後で **TIFF を PDF に変換** したくなる場合、マルチページTIFFは自動的に処理され、各フレームが別々のPDFページになります。

## ステップ 3 – OCR を実行してテキストを取得 (画像からテキストを抽出)

Running OCR is as easy as calling `Recognize`. The engine will return a `RecognitionResult` that contains the plain text, confidence scores, and layout information.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**プロのコツ:** テキストだけが必要で（PDF が不要な）場合、ここで止めて `extractedText` を `.txt` ファイルに書き出すことができます。しかしほとんどの場合、目的は検索可能なPDFなので、続行します。

## ステップ 4 – 検索可能なPDFとして保存 (検索可能なPDFの作成)

Aspose は最終ステップを簡単にします：`SaveFormat.PdfSearchable` を指定して `Save` を呼び出すだけです。内部では抽出したテキストを不可視レイヤーとして埋め込み、元の画像の外観はそのまま保持します。  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

`contract_searchable.pdf` を任意の PDF ビューアで開くと、テキストの選択、コピー、検索が可能になります—クライアントが「検索可能なPDF」に期待する通りです。

## マルチページTIFFの処理 (TIFF を PDF に変換)

If your source file contains several pages, Aspose will treat each frame as a separate page automatically. No extra loops required. However, you might want to control the DPI or image quality for each page:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

これらのオプションを設定したら、各フレームに対して **ステップ 2** を繰り返すか、または `ImageStream.FromFile` でマルチページTIFFを指定し、Aspose に処理を任せます。

## よくある落とし穴と対処法

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| テキストが乱れたり欠落している | 言語設定が間違っている | `ocrEngine.Language` を正しい言語パック（例: `Language.German`）に設定する。 |
| PDF が巨大（単ページスキャンで10 MB） | デフォルトの画像圧縮が低い | `ocrEngine.ImageProcessingOptions.Compression` を `Jpeg` に変更し、適切な `Quality` 値（0‑100）を設定する。 |
| OCR の実行が非常に遅い | デフォルトの `Auto` 言語検出を使用している | 期待する言語を明示的に設定する。 |
| 検索可能なレイヤーが表示されない | `SaveFormat.Pdf` で保存しているため `PdfSearchable` ではない | `PdfSearchable` を使用する。 |

## 完全なエンドツーエンド例

Putting everything together, here’s a ready‑to‑run console app you can copy‑paste into Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**実行結果:**  
* OCR されたテキストの抜粋を表示するコンソールウィンドウ。  
* 元の TIFF の隣に作成された `contract_searchable.pdf` ファイル。これを開き、**Ctrl + F** で元のスキャンに含まれる任意の単語を検索すると、期待通りに動作します。

## 次のステップと関連トピック

* **ドキュメントの OCR バッチ処理** – 上記コードを `foreach` ループでラップし、フォルダー全体を処理する。  
* **TIFF 以外のスキャン画像形式の変換**（PNG、JPEG） – 同じ API が使えます。拡張子を変更するだけです。  
* **画像からテキストを抽出** してさらに分析 – `result.Text` を自然言語処理パイプラインに渡す。  
* **PDF サイズの最適化** – `PdfSaveOptions` を調べて画像をさらに圧縮したり、必要なときだけフォントを埋め込む。  

これらのアイデアを試すことで、あらゆる「スキャンを検索可能なPDFに変換」依頼に対応できる頼りになる存在になるでしょう。

---

### TL;DR

これで、Aspose OCR を C# で使用してスキャン画像から **検索可能なPDF** を作成する方法が分かりました。手順は、エンジンの初期化、画像の読み込み、OCR の実行、そして `PdfSearchable` で保存する、という流れです。言語設定、DPI、圧縮を調整すれば、さまざまなケースに対応でき、**スキャン画像の変換**、**画像からテキストの抽出**、さらには **TIFF を PDF に変換** も大規模に行えるようになります。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}