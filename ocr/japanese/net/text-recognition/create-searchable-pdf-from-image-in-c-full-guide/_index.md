---
category: general
date: 2026-03-21
description: C#でスキャン画像から検索可能なPDFを作成する。画像をPDFに変換し、スキャンからテキストを抽出し、Aspose OCRを使用して画像に対してOCRを実行する方法を学びます。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from scan
- convert scanned document
- perform ocr on image
language: ja
og_description: C#でスキャン画像から検索可能なPDFを作成。画像をPDFに変換し、スキャンからテキストを抽出し、画像にOCRを実行する手順をステップバイステップで学べます。
og_title: C#で画像から検索可能なPDFを作成する – 完全ガイド
tags:
- OCR
- C#
- PDF
- Aspose
title: C#で画像から検索可能なPDFを作成する – 完全ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像から検索可能な PDF を作成 – 完全ガイド

スキャンした画像数枚から **検索可能な PDF** を作成したことがありますか？ 法務チーム、会計士、開発者の皆さんは、紙の契約書を Ctrl‑F で検索できる形に変換しようとして、この壁にぶつかります。  

このチュートリアルでは、Aspose OCR ライブラリを使用して **画像を PDF に変換**、**スキャンからテキストを抽出**、そして **画像で OCR を実行** する方法を学びます。最後には、数行のコードで検索可能な PDF を出力する C# スニペットが手に入ります。

## このガイドでカバーする内容

必要なすべての手順を順に解説します：

* Aspose OCR NuGet パッケージの設定。  
* スキャンした PNG または JPEG を `OcrEngine` に読み込む。  
* 1 回のメソッド呼び出しで画像を検索可能な PDF に変換。  
* 結果を保存し、テキストレイヤーが正しく機能するか検証。  

外部ドキュメントへの曖昧な参照はありません。必要な情報はすべてここにあります。C# と .NET Core/Framework の基本的な理解があれば、"Hello World" が書ける程度で問題ありません。

---

## 前提条件

| 必要条件 | 理由 |
|-------------|----------------|
| .NET 6.0+（または .NET Framework 4.7.2+） | Aspose OCR は両方をサポートしていますが、最新ランタイムの方がパフォーマンスが向上します。 |
| Visual Studio 2022 または VS Code | IDE があると NuGet パッケージの管理やデモ実行が楽になります。 |
| Aspose.OCR NuGet パッケージ（`Aspose.OCR` v23.12 以降） | 本チュートリアルで使用する `OcrEngine` クラスがこのライブラリに含まれます。 |
| スキャン画像（例: `contract_scan.png`） | 検索可能な PDF に変換したい元ファイルです。 |

上記が揃っていない場合は、ターミナルで以下を実行してください：

```bash
dotnet add package Aspose.OCR --version 23.12
```

このワンライナーですべてがインストールされます。

---

## 手順 1: OCR エンジンの初期化 – 検索可能な PDF のコア作成

最初に `OcrEngine` インスタンスを作成します。これはピクセルを読み取りテキストを出力する「脳」のようなものです。

```csharp
using System;
using System.Drawing;               // For Image handling
using Aspose.OCR;                  // Core OCR namespace
using Aspose.OCR.Output;           // PDFResult lives here

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow...
```

**ポイント:**  
エンジンは一度作成して複数画像で再利用した方が、ループ内で毎回インスタンス化するより効率的です。エンジンは言語パックなどの内部リソースを保持しており、毎回再ロードしたくありません。

---

## 手順 2: ソース画像の読み込み – 画像を PDF に変換

次に、処理したいファイルをエンジンに渡します。Aspose OCR は `System.Drawing.Image` を受け取れるので、PNG、JPEG、BMP、さらには TIFF も扱えます。

```csharp
        // Step 2: Load the scanned image
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);
```

**プロ tip:** 画像が非常に大きい（10 MP 超）場合は、メモリ使用量を抑えるために先に縮小することを検討してください。OCR の品質は 300 DPI で十分に保たれます。

```csharp
        // Optional: downscale large images (maintains aspect ratio)
        // ocrEngine.Image = ImageHelper.Resize(ocrEngine.Image, 2000, 2000);
```

---

## 手順 3: OCR 実行と検索可能 PDF の生成 – スキャンからテキストを抽出

ここで魔法が起きます。`RecognizePdf()` メソッドは 2 つのことを同時に行います：画像に対して OCR を実行し、生成されたテキストレイヤーを PDF コンテナに埋め込みます。

```csharp
        // Step 3: Run OCR and get a searchable PDF result
        PdfResult searchablePdf = ocrEngine.RecognizePdf();
```

**`PdfResult` には何が入っている？**  
メモリ上の PDF バイト列を保持する軽量ラッパーです。Web API のレスポンスに直接ストリームしたり、次のステップでディスクに保存したりできます。

---

## 手順 4: PDF をディスクに保存 – スキャン文書を検索可能 PDF に変換

最後に、PDF バイト列をファイルに書き出します。拡張子 `.pdf` が付いていることで、任意の PDF ビューアは文書が検索可能であることを認識します。

```csharp
        // Step 4: Save the searchable PDF
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

プログラムを実行（`dotnet run`）し、`contract_searchable.pdf` を Adobe Reader で開きます。テキストを選択してコピーしてみてください。隠れたテキストレイヤーが機能しているはずです。

---

## 結果の検証 – OCR が本当に機能したか？

簡単なサニティチェックを行うだけで、後々のトラブルを防げます。PDF を開き **Ctrl + F** で、元のスキャンに確実に含まれる単語（例: “Agreement”）を検索します。ヒットすれば **検索可能な PDF を作成** できています。

テキストが選択できない場合は、以下を再確認してください：

* 画像品質（ぼやけたスキャンは OCR が低下します）。  
* `RecognizePdf()` を使用したか、単に `Recognize()`（テキストだけ返す）を呼んでいないか。  
* 正しい言語が設定されているか – `ocrEngine.Language = Language.English;` で精度が向上します。

---

## 複数ページの処理 – 複数画像からスキャン文書を変換

契約書はページ数が多いことが普通です。各画像を個別に処理する代わりに、フォルダーをループして結果を結合できます：

```csharp
        var pdfPages = new System.Collections.Generic.List<PdfResult>();

        foreach (var file in System.IO.Directory.GetFiles(@"YOUR_DIRECTORY/Scans", "*.png"))
        {
            ocrEngine.Image = Image.FromFile(file);
            pdfPages.Add(ocrEngine.RecognizePdf());
        }

        // Merge all pages into one PDF
        var mergedPdf = PdfResult.Merge(pdfPages);
        mergedPdf.Save(@"YOUR_DIRECTORY/contract_full_searchable.pdf");
```

**結合する理由:**  
単一の PDF の方が共有やインデックス作成が容易です。`Merge` ヘルパーは各ページのテキストレイヤーを保持しつつページをつなぎ合わせます。

---

## よくある落とし穴と対策 – プロ並みの OCR 実行

| 問題 | 解決策 |
|-------|----------|
| **DPI が低い（150 未満）** | OCR 前に画像を 300 DPI にリサンプリング。 |
| **言語設定が間違っている** | `ocrEngine.Language = Language.Spanish;` など、正しい言語を設定。 |
| **メモリ使用量が大きい** | 各イテレーション後に `Image` オブジェクトを破棄: `ocrEngine.Image.Dispose();` |
| **PDF にフォントが埋め込まれない** | Aspose は標準フォントを自動埋め込みします。カスタムフォントが必要な場合は `PdfSaveOptions` で追加。 |

---

## 完全動作サンプル – すべてのコードを一括掲載

以下は **検索可能な PDF を作成** するための、コピー＆ペーストだけで動く完全版プログラムです。欠けている部分はありません。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load image (replace with your actual path)
        string inputPath = @"YOUR_DIRECTORY/contract_scan.png";
        ocrEngine.Image = Image.FromFile(inputPath);

        // Optional: improve accuracy by setting language
        // ocrEngine.Language = Language.English;

        // Perform OCR and get searchable PDF
        PdfResult searchablePdf = ocrEngine.RecognizePdf();

        // Save PDF to disk
        string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";
        searchablePdf.Save(outputPath);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

実行して出力を開けば、**画像を PDF に変換** しつつ検索可能なテキストを保持できたことが確認できます。これこそが現代の文書ワークフローが求めるものです。

---

## 次のステップ – OCR パイプラインを拡張

**検索可能な PDF を作成** できたら、以下の拡張を検討してください：

* **バッチ処理** – 上記のマルチページループを使ってフォルダー全体を処理。  
* **カスタム OCR 設定** – `ocrEngine.RecognizeArea` で領域を限定したり、`ocrEngine.PageSegmentationMode` を調整。  
* **Web API との統合** – ASP.NET Core エンドポイントから PDF バイト列を直接返し、オンザフライ変換を実現。  
* **ポストプロセッシング** – 抽出テキストにスペルチェックや正規表現フィルタを掛け、精度をさらに向上。  

これらのトピックはすべて **スキャンからテキストを抽出** や **画像で OCR を実行** と密接に関係しており、検索エンジンが好むキーワードでもあります。

---

## 結論

Aspose OCR を使って C# でスキャン画像から **検索可能な PDF** を作成するために必要な手順をすべて網羅しました。エンジンの初期化、画像の読み込み、OCR の実行、最終的な PDF の保存まで、シンプルかつ自己完結型のフローです。  

自分の契約書や請求書、その他スキャン文書でぜひ試してみてください。この流れをマスターすれば、**スキャン文書のバッチ変換**、**スキャンからテキストを抽出**、そして **画像で OCR を実行** といった downstream のデータ処理タスクも楽にこなせます。

問題があったり、さらなる自動化のアイデアがあればコメントで教えてください。コーディングを楽しみながら、紙の山を検索可能なデジタル資産に変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}