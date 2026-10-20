---
category: general
date: 2026-04-04
description: C#でTIF画像から検索可能なPDFを作成 – 画像をPDFに変換し、PDFメタデータを追加し、Aspose.OCRを使用して検索可能なドキュメントを生成する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: ja
og_description: C#でTIFファイルから検索可能なPDFを作成します。画像をPDFに変換し、PDFメタデータを追加し、Aspose.OCRを使用して検索可能なドキュメントを生成します。
og_title: TIFから検索可能なPDFを作成する – ステップバイステップガイド
tags:
- Aspose.OCR
- C#
- PDF generation
title: TIFから検索可能なPDFを作成 – 画像をPDFに変換し、PDFメタデータを追加
url: /ja/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIF から検索可能な PDF を作成 – 完全な C# ウォークスルー

スキャンした請求書から **create searchable PDF** を作成したいが、テキストを検索可能に保ち、ファイルのメタデータを整える方法が分からないことはありませんか？ あなただけではありません。多くの自動化プロジェクトでは、PDF は機械が読み取れるだけでなく、タイトル、作成者、信頼度閾値などの情報で適切にタグ付けされている必要があります。

このガイドでは、**画像を PDF に変換**し、**PDF メタデータ**を注入し、低信頼度の OCR 結果をフィルタリングする完全なソリューションを、すべて Aspose.OCR ライブラリを使用して解説します。最後まで読むと、任意の .NET プロジェクトに組み込めるすぐに使えるスニペットと、エッジケースを処理するためのいくつかのヒントが手に入ります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）  
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）  
- 検索可能な PDF に変換したい TIF 画像（例: `input.tif`）  
- C# と Visual Studio（またはお好みの IDE）に関する基本的な知識  

他の外部サービスは必要ありません。すべてローカルで実行されます。

## ステップ 1 – OCR エンジンの設定（Searchable PDF Core の作成）

最初に必要なのは、認識すべき言語を把握した `OcrEngine` インスタンスです。多くのビジネスシナリオでは英語で十分ですが、`Language.English` を任意のサポートされている言語に置き換えることができます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Why this matters:** OCR エンジンはラスタピクセルを Unicode テキストに変換する重い処理を担当します。言語を正しく設定することで精度が向上し、後でフィルタリングされる低信頼度の単語の数が減少します。

> **Pro tip:** 多言語ドキュメントを処理する場合は、複数のエンジンをインスタンス化するか、`Language.Multilingual` を使用して Aspose に言語検出を自動的に任せてください。

## ステップ 2 – TIF 画像の読み込み（TIF から PDF の作成）

ここでエンジンにソースファイルを指示します。`ImageStream.FromFile` ヘルパーは画像をストリームに読み込み、OCR エンジンが使用できるようにします。

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

「JPEG や PNG を使用できるか？」と疑問に思うかもしれません。もちろんです—Aspose.OCR はほとんどのラスタ形式をサポートしています。ファイル拡張子を変更すればすぐに使用できます。

## ステップ 3 – PDF オプションの設定（PDF にメタデータを追加）

変換する前に、`PdfOptions` オブジェクトを定義します。ここでタイトルや作成者などの **PDF メタデータ** を追加し、信頼度が閾値以下の単語をエンジンに除外させます。

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**What’s happening here?**  
- `Title` と `Author` は PDF のドキュメント情報辞書の一部となり、ドキュメント管理システムでのインデックス作成が容易になります。  
- `MinConfidence` は安全装置です。OCR は薄い文字を誤認識しがちですが、これを除外することで検索可能なレイヤーがクリーンになり、下流のテキスト抽出が向上します。

カスタムメタデータ（例: `Subject`、`Keywords`）が必要な場合は、`PdfOptions.CustomProperties` を使用して設定できます。

## ステップ 4 – 画像を検索可能な PDF に変換（画像から PDF へ変換）

エンジンの準備が整い、オプションが設定されたら、最後の呼び出しで変換を実行します。検索可能な PDF をディスクに書き込み、元の画像の下に OCR テキストレイヤーを埋め込みます。

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

この行が実行されると、`output.pdf` には以下が含まれます：  
- ビジュアル背景としての元の TIF 画像  
- 検索エンジンやコピー＆ペースト操作で読み取れる不可視のテキストレイヤー  
- 先ほど定義したメタデータ（タイトル、作成者など）

### 期待される結果

生成された PDF を Adobe Reader や任意の PDF ビューアで開き、テキスト選択を試みてください。元のスキャンと一致する文をコピーできるはずです。ドキュメントの **Properties** ダイアログにはタイトル “Invoice #12345” と作成者 “MyCompany” が表示されます。

## ステップ 5 – 信頼度フィルタリングの検証（MinConfidence が有効な理由）

低信頼度の単語が実際に除去されたことを確認すると便利です。`pdftotext` のようなツールを使って PDF の隠しテキストを検査できます。

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

単語が表示されなければ、`MinConfidence` フィルタは期待通りに機能しています。より厳しいまたは緩やかなフィルタが必要な場合は、閾値（例: `0.7f`）を調整してください。

## ステップ 6 – 複数ページの処理（マルチページ TIF から検索可能な PDF を作成）

多くの請求書はマルチページ TIFF 形式です。Aspose.OCR は各フレームを自動的に別ページとして扱います。エンジンにマルチページファイルを指すだけで、同じ `ConvertToSearchablePdf` 呼び出しがマルチページの検索可能な PDF を生成します。

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Edge case:** ページが空白の場合、OCR は空のテキストレイヤーを生成することがありますが、これは無害です。ただし、変換前に `ocrEngine.HasText` をチェックすることで空白ページをスキップできます。

## ステップ 7 – 完全なサンプルのパッケージ化（全ステップをまとめて）

以下は、すべてをまとめた単一の実行可能プログラムです。`YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

プログラムを実行します（`dotnet run` または Visual Studio で **F5** を押す）と、確認メッセージが表示されます。生成された PDF はソース画像の隣に保存され、インデックス作成やアーカイブの準備が整っています。

## よくある質問と注意点

| Question | Answer |
|----------|--------|
| **検索可能なレイヤーにカスタムフォントを追加できますか？** | OCR レイヤーは Unicode を使用します。視覚的な外観は元の画像によって決まるため、追加のフォント埋め込みは必要ありません。 |
| **TIF がカラーの場合はどうなりますか？** | Aspose.OCR は OCR のためにカラー画像を自動的にグレースケールに変換しますが、`PdfOptions.PreserveColor = true` を設定すれば PDF で元の色を保持できます。 |
| **このライブラリはスレッドセーフですか？** | `OcrEngine` インスタンスは各スレッドで単独に使用すべきです。並列処理を行う場合は、スレッドごとに別々のエンジンを作成してください。 |
| **PDF を暗号化するにはどうすればよいですか？** | OCR 変換後に `PdfOptions.Security` を使用してパスワードと権限を設定します。 |

## 次のステップ（PDF ツールキットを拡張）

- **Batch processing:** フォルダ内の TIFF をループして各々検索可能な PDF を生成します。  
- **Post‑processing:** 生成された PDF を Aspose.PDF でマージし、単一のマスタードキュメントにします。  
- **Advanced metadata:** カスタム XMP フィールドを設定して、SharePoint や ECM システムとの統合を強化します。  

これらの拡張は、先ほど説明したコアパターン（**create searchable PDF**、**convert image to PDF**、**add PDF metadata**）に基づいています。

---

*ハッピーコーディング！問題が発生したら、下にコメントを残すか、最新の API 更新情報については Aspose.OCR のドキュメントをご確認ください。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}