---
category: general
date: 2026-06-06
description: 検索可能なPDFの作成方法と、OCRを使用した画像のPDFへの変換方法を学びます。レイヤーの追加、圧縮設定、完全なC#コードが含まれています。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: ja
og_description: OCRを使用して画像から検索可能なPDFを作成します。このガイドでは、隠しテキスト層の追加、圧縮設定、画像のPDFへの変換方法を示します。
og_title: 検索可能なPDFを作成する – 完全C#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: 画像から検索可能なPDFを作成する – 完全ステップバイステップガイド
url: /ja/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能な PDF を作成 – 完全 C# チュートリアル

スキャンした請求書から **検索可能な PDF** を、GUI ツールで何時間もかけずに作成する方法を考えたことはありませんか？ あなたは一人ではありません。画像を元の見た目のまま PDF に変換し、ユーザーがテキストをコピーしたり検索できるようにする必要があるとき、多くの開発者が壁にぶつかります。  

このチュートリアルでは、**画像を PDF に変換**し、OCR を実行し、隠しテキストレイヤーを追加し、さらには圧縮設定を調整する正確な手順を順に説明します。最後まで読むと、任意の .NET プロジェクトに組み込める、すぐに使える C# スニペットが手に入ります。

## 学べること

- OCR エンジンをセットアップし、**how to OCR image** ファイルの仕組みを理解する。
- **how to add layer** オプションを使用して、検索可能なテキストオーバーレイを埋め込む。
- 小さく、ZIP 圧縮された PDF のために **how to set compression** を適用する。
- 単純な画像を自動化可能な **create searchable pdf** ワークフローに変換する。
- PDF を鮮明かつ高速に保つための一般的な落とし穴とプロのコツ。

### 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。
- Aspose.OCR と Aspose.Pdf の NuGet パッケージ（または `OcrEngine` と `PdfSaveOptions` を提供する同等のライブラリ）。
- サンプル画像（例: `invoice.png`）を、参照できるフォルダーに配置します。
- C# の基本的な構文の理解—深い OCR 知識は不要です。

> **Pro tip:** Visual Studio を使用している場合は、Package Manager Console からパッケージをインストールしてください：  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![隠しテキストレイヤー付きで請求書画像が PDF に変換された検索可能な PDF の例](/images/create-searchable-pdf.png)

## ステップ 1: OCR エンジンの初期化 – **how to ocr image**

まず、画像から英語テキストを読み取れる OCR エンジンが必要です。`OcrEngine` クラスがエントリーポイントで、言語を設定し、後で画像を渡すだけです。

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Why this matters:* エンジンを正しい言語で初期化すると、精度が劇的に向上します。これを省略すると、文字化けが発生する可能性があります。

## ステップ 2: 画像の読み込み – **convert image to pdf**

次に、エンジンに処理したいファイルを指示します。`ImageStream.FromFile` はバイトを読み取り、OCR 用に準備します。

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

画像が Web リクエストやデータベースから来る場合は、`MemoryStream` からロードすることもできます。

## ステップ 3: OCR 認識の実行 – **how to ocr image**

画像がロードされたら、重い処理は 1 回の呼び出しで行われます。`Recognize` メソッドは抽出されたテキストと元のビットマップの両方を保持する `OcrResult` を返します。

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Behind the scenes:* エンジンは各ピクセルを解析し、文字を検出し、Unicode 文字列を構築します。また、後で隠しテキストレイヤーに必要な位置データも保持します。

## ステップ 4: PDF 保存オプションの設定 – **how to add layer** & **how to set compression**

ここが検索可能な PDF の魔法が発生する場所です。`PdfSaveOptions` オブジェクトを作成し、Aspose.Pdf に元の画像を埋め込み、隠しテキストオーバーレイを追加し、最終ファイルを圧縮する方法を指示します。

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** は元のスキャンの視覚的忠実度を保証します。
- **AddTextLayer** は、ブラウザや PDF リーダーが検索用にインデックスできる不可視レイヤーを作成します。
- **Compression** は品質を犠牲にせずファイルサイズを削減します。ZIP はほとんどの文書に適したデフォルトです。

## ステップ 5: 結果の保存 – **create searchable pdf**

最後に、先ほど定義したオプションを使用して OCR 結果をディスクに書き込みます。`Save` メソッドは保存先パスと `PdfSaveOptions` インスタンスを受け取ります。

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

`invoice_searchable.pdf` を Adobe Reader や最新のビューアで開くと、元の画像が表示されますが、テキストを選択、コピー、検索できるようになり、まるでネイティブ PDF のように扱えます。

### 完全な動作例

すべてをまとめると、以下が完全で実行可能なプログラムです：

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**期待される出力**（コンソール）:  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

生成されたファイルを開き、**Ctrl F** を押して、請求書にある単語を入力すると、ビューアが即座にその場所にジャンプします。これが **create searchable pdf** の実装の核心です。

## よくある落とし穴と回避方法

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| テキストが検索できない | `AddTextLayer` が `false` のまま、または古い Aspose バージョンを使用している | `AddTextLayer = true` に設定し、最新の NuGet パッケージに更新する |
| PDF が巨大（メガバイト） | 圧縮が `PdfCompression.None` に設定されている | `PdfCompression.Zip` または画像用に `PdfCompression.Jpeg` に切り替える |
| 文字化け | 言語設定が間違っている、または低解像度画像 | `engine.Language` を適切に設定し、少なくとも 300 dpi の画像を使用する |
| 一部のビューアで隠しレイヤーが見えない | 非標準の PDF バージョンで生成された PDF | `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7`（デフォルト）を使用するか、ビューアをアップグレードする |

### プロのコツ

OCR なしで **convert image to PDF**（単なる画像 PDF）を作成する必要がある場合は、`AddTextLayer = false` に設定します。同じ `PdfSaveOptions` で圧縮を制御できるため、検索可能性が不要なスキャン文書のアーカイブに便利です。

## ソリューションの拡張

- **Multiple pages**: 画像ファイルのリストをループし、毎回 `engine.Image = ...` を呼び出し、`PdfDocument` の集約機能を使って結果を単一の PDF にまとめます。
- **Different languages**: `engine.Language = OcrLanguage.Spanish`（またはサポートされている任意の言語）に変更して、多言語の請求書に対応します。
- **Custom compression**: カラフルな画像の場合、品質設定付きの `PdfCompression.Jpeg`（`pdfOptions.JpegQuality = 80`）を使用すると、ファイルをさらに縮小できます。

## 結論

ここまでで、C# を使用して画像から **create searchable PDF** ファイルを作成するために必要なすべてを網羅しました。OCR エンジンの初期化、画像の読み込み、認識の実行、隠しテキストレイヤーの設定、圧縮の設定—それぞれが高速で検索可能なドキュメントを提供する重要な役割を果たします。  

これで、請求書処理の自動化、契約書のアーカイブ、または紙の山を即座に検索可能な PDF に変換するバルクスキャンユーティリティの構築が可能です。  

次の課題に挑戦する準備はできましたか？透かしを追加したり、複数の検索可能な PDF を結合したり、このロジックを Web API 経由で提供し、組織全体が画像をアップロードして即座に検索可能な PDF を受け取れるようにしてみてください。

*このガイドが役に立ったと思ったら、⭐ を付けて同僚と共有したり、独自の調整点をコメントで教えてください。ハッピーコーディング！*

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.OCR を使用した .NET での PDF OCR 方法](/ocr/english/net/text-recognition/recognize-pdf/)
- [画像を PDF に変換 C# – マルチページ OCR 結果の保存](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [画像の OCR 方法 – OCR 画像認識で画像に OCR を実行](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}