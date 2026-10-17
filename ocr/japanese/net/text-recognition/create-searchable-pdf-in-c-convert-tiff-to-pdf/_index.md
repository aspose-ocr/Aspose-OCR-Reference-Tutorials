---
category: general
date: 2026-02-17
description: Aspose OCR を使用して C# でマルチページ TIFF から検索可能な PDF を作成します。数分で TIFF を PDF に変換し、PDF
  をファイルに書き込む方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- write pdf to file
- ocr engine c#
- convert multi page tiff
language: ja
og_description: C#でAspose OCRを使用して、マルチページTIFFから検索可能なPDFを作成します。このガイドでは、TIFFをPDFに変換し、PDFをファイルに書き込む方法を示します。
og_title: C#で検索可能なPDFを作成 – TIFFをPDFに変換
tags:
- Aspose OCR
- C#
- PDF generation
title: C#で検索可能なPDFを作成 – TIFFをPDFに変換
url: /ja/net/text-recognition/create-searchable-pdf-in-c-convert-tiff-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で検索可能なPDFを作成 – TIFFをPDFに変換

スキャンしたドキュメントから **create searchable PDF** を作成したいと思ったことはありませんか？でも、どこから始めればいいか分からないことも多いでしょう。多くのオフィス自動化プロジェクトでは、複数ページのTIFFを検索・コピー・インデックス可能なPDFに変換することが求められます。  

このチュートリアルでは、Aspose OCR を使用して **create searchable PDF** を作成する方法、**convert tiff to pdf** の手順、そしてディスクに **write pdf to file** する方法を示す、完全に実行可能なサンプルを順に解説します。最後まで読むと、全体のパイプラインの流れや各ステップの重要性、**ocr engine c#** を使って **convert multi page tiff** シナリオを処理する際の注意点が理解できるようになります。

## 作成するもの

- ディスクからマルチページTIFF画像をロードする。  
- Aspose OCR の `OcrEngine` を使って各ページに OCR を実行する。  
- 生成された検索可能なPDFをメモリにストリームする。  
- `WriteAllBytes` を一度呼び出すだけでPDFをファイルに保存する。  

外部サービスや面倒なコマンドラインツールは不要です。純粋な C# コードだけなので、任意の .NET コンソールアプリにそのまま組み込めます。

> **Pro tip:** Aspose OCR は商用ライブラリですが、無料トライアルで学習には十分に機能します。本番環境で使用する場合は有効なライセンスを設定してください。

## 前提条件

- .NET 6.0 SDK（または最新の .NET バージョン）。  
- Visual Studio 2022 または VS Code—お好きな IDE で構いません。  
- Aspose.OCR NuGet パッケージ（`dotnet add package Aspose.OCR`）。  
- 既知のフォルダーに配置したマルチページTIFFファイル（`multi_page.tif`）。

以上です。追加の設定は不要です。

![検索可能なPDF作成例](https://example.com/create-searchable-pdf.png){: .align-center alt="検索可能なPDF作成例"}

## Step 1 – OCRエンジンの初期化 (ocr engine c#)

画像を処理する前に、`OcrEngine` のインスタンスが必要です。このオブジェクトはすべての OCR 設定を保持し、裏で重い処理を行います。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

なぜ毎回新しいエンジンを作成するのでしょうか？エンジンは内部リソースをキャッシュします。使用後に破棄することでネイティブメモリが解放され、大きなマルチページTIFFを扱う際に重要です。

## Step 2 – マルチページTIFFのロード (convert multi page tiff)

Aspose OCR は TIFF ストリームを直接読み取れるので、ディスク上のファイルを指定するだけです。

```csharp
        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");
```

TIFF がストリーム（例: データベース）にある場合は、`FromFile` を `FromStream` に置き換えてください。エンジンはページ数を自動的に検出するため、**convert multi page tiff** を余分なループなしで処理できます。

## Step 3 – PDF用のMemoryStreamを準備 (write pdf to file)

ディスクに直接書き込まないのは、ストリーミングにより PDF のサイズを確認したり、暗号化したり、永続化前に HTTP で送信したりできるからです。

```csharp
        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
```

`using` ブロックを使用することでストリームが確実に破棄され、ファイルハンドルのリークを防げます。これは長時間稼働するサービスで問題になることがあります。

## Step 4 – OCRを実行し検索可能なPDFとして保存 (create searchable pdf)

ここが核心の操作です: TIFF を `SaveAsSearchablePdf` に渡します。このメソッドはページごとに OCR を実行し、見えないテキストレイヤーを含む PDF を生成します。

```csharp
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);
```

内部では、Aspose が各 TIFF フレームごとに PDF ページを作成し、OCR エンジンを実行して認識したテキストを重ね合わせます。これがスキャンドキュメントを **create searchable pdf** に変換する正確な仕組みです。

## Step 5 – PDFをディスクに書き込む (write pdf to file)

最後に、メモリバッファを実際のファイルにフラッシュします。

```csharp
            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }
```

`WriteAllBytes` はほとんどのプラットフォームで原子的に実行されるため、書き込み途中でプロセスがクラッシュしても半端なファイルが残りません。既存の PDF に追記したい場合は、代わりに Aspose.PDF の使用を検討してください。

## Step 6 – 確認メッセージ

簡単なコンソールメッセージで、すべてが正常に完了したことを通知します。

```csharp
        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

プログラムを実行し、実際の TIFF を指定すると、ソースファイルの隣に `result.pdf` が生成されます。任意の PDF ビューアで開き、テキスト選択を試すと OCR レイヤーが機能しているのが確認できます。

## エッジケースと一般的な落とし穴の対処

| Situation | What to Do |
|-----------|------------|
| **非常に大きなTIFF（数百MB）** | プロセスのメモリ上限を増やすか、バッチ処理でページを処理します。1フレームずつロードし、既存ストリームに追加する `PdfSaveOptions` を指定して `SaveAsSearchablePdf` を呼び出します。 |
| **OCRの言語が英語でない** | `SaveAsSearchablePdf` を呼び出す前に `ocrEngine.Language = Language.Spanish;`（またはサポートされている任意の言語）を設定します。 |
| **ライセンスが未設定** | 体験版は透かしが付加されます。`License license = new License(); license.SetLicense("Aspose.OCR.lic");` でライセンスを登録してください。 |
| **破損したTIFFファイル** | `ImageStream.FromFile` を try/catch で囲み、`Aspose.OCR.Exception` の詳細をログに記録します。 |
| **画像なしの検索可能PDFが必要** | `PdfSaveOptions` の `RemoveImages = true` を使用して、出力サイズを縮小します。 |

## 完全な動作例（全ステップ統合）

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language if needed
        // ocrEngine.Language = Language.English;

        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");

        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);

            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**期待結果:** `result.pdf` が `YOUR_DIRECTORY` に生成されます。開くと各元の TIFF ページに加えて、隠れた選択可能なテキストレイヤーが表示されます。これがスキャン画像から **create searchable pdf** を作成する際に必要なものです。

## まとめ

ここでは、**convert tiff to pdf** ワークフローから **create searchable PDF** を作成するために必要なすべてを解説しました。**write pdf to file** の方法、**ocr engine c#** の役割、**convert multi page tiff** ソースに対する特別な考慮点も含まれます。コードは自己完結型で .NET 6+ で動作し、最小限の変更で Web API やバックグラウンドサービスにも適用可能です。

### 次にやること

- **パスワード保護を追加** するには、`PdfSaveOptions` を使用します。  
- **出力を圧縮** するには、`PdfSaveOptions.CompressionLevel` を調整します。  
- **ASP.NET Core と統合** して、PDF をブラウザに直接配信します。  
- **Azure Functions を調査** して、サーバーレス OCR パイプラインを構築します。

自由に実験してみてください。入力フォーマットを変更したり、別の OCR 言語を試したり、PDF を文書管理システムに流し込んだりできます。**convert tiff to pdf** と **write pdf to file** の方法さえ分かっていれば、可能性は無限です。

コーディングを楽しんで、PDF が常に検索可能でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}