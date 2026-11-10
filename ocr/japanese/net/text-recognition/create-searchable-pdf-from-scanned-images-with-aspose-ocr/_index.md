---
category: general
date: 2026-02-27
description: Aspose OCR を使用して、スキャンした PDF から数秒で検索可能な PDF を作成します。スキャン PDF の変換方法、OCR
  での PDF 変換、PDF からのテキスト抽出を簡単に学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: ja
og_description: 検索可能なPDFを即座に作成します。このチュートリアルでは、スキャンしたPDFを変換し、OCRでPDFを変換し、Aspose OCRを使用してPDFからテキストを抽出する方法を示します。
og_title: 検索可能PDFの作成 – Aspose OCR クイックガイド
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCRでスキャン画像から検索可能なPDFを作成する
url: /ja/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャン画像から Aspose OCR で検索可能な PDF を作成する

紙だけの請求書から **検索可能な PDF** を作成したいけど、どこから始めればいいか分からないことはありませんか？Aspose OCR を使えば、数行の C# コードだけで **検索可能な PDF** を作成できます—外部サービス不要、手動でのコピー＆ペーストも不要です。

このガイドでは、**スキャンした pdf** ファイルを完全に検索可能な PDF に変換するために必要な手順をすべて解説し、各ステップの重要性を説明します。また、PDF 出力ではなく生の文字列が欲しい場合の **pdf からテキストを抽出** 方法も紹介します。最後まで読むと、一般的な「画像だけの PDF」問題を処理できる再利用可能なスニペットと、エッジケースに対するいくつかのヒントが手に入ります。

![create searchable pdf using Aspose OCR](image-placeholder.png "create searchable pdf using Aspose OCR")

## 必要なもの

- .NET 6.0 以降（API は .NET Core、.NET Framework、.NET 5+ でも動作します）
- Visual Studio 2022（またはお好みのエディタ）
- Aspose OCR NuGet パッケージ（`Aspose.OCR`）— 最初の手順でインストールします
- 画像だけの **検索可能な PDF** に変換したいスキャン済み PDF ファイル

以上だけです—追加の OCR エンジンは不要、トライアル実行のためのライセンス問題もありません。  

それでは、始めましょう。

## 手順 1: Aspose OCR ライブラリをインストールする（クイックヒント付き）

コードを実行する前に、ライブラリを参照に追加する必要があります。プロジェクトフォルダでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio のパッケージマネージャを使用している場合は “Aspose.OCR” を検索し、**インストール** をクリックします。無料トライアルは最大 20 ページまで利用でき、テストに最適です。

パッケージをインストールすると、`OcrEngine`、`OcrLanguage`、`OcrOutputFormat` の 3 クラスが利用可能になります。これらを使って **ocr convert pdf** を行います。

## 手順 2: OCR エンジンを構成する（検索可能な PDF 作成 – コア設定）

エンジンに認識させる言語と期待する出力形式を指定する必要があります。ここでは、英語の検索可能な PDF を作成します。

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

`Language` を明示的に設定する理由は何ですか？エンジンが言語を推測すると OCR の精度が大幅に低下します。特に数字や混在スクリプトが含まれる文書では顕著です。英語に固定することで、テキストレイヤーがクリーンになり、後続の **pdf からテキストを抽出** ステップが改善されます。

## 手順 3: スキャン PDF を検索可能な PDF に変換する

エンジンの準備ができたら、ソースファイルを指定し、結果を書き出す場所を設定します。この一呼び出しで、各ページをラスタライズし、OCR を実行し、不可視のテキストレイヤーを持つ新しい PDF を生成します。

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

ソース PDF が複数ページの場合、Aspose OCR は順次処理し、元のレイアウトを保持します。出力ファイルは任意の PDF ビューアで開くことができ、以前は画像だった文字列が選択・検索できるようになります。

### 結果の検証（PDF からテキストを抽出）

変換が確実に成功したか確認したい場合は、プログラムからテキストを取得すると良いでしょう。

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

このスニペットは OCR 後に **pdf からテキストを抽出** する方法を示しています。インデックス作成や検索エンジンへの投入に便利です。この部分には別途 `Aspose.PDF` パッケージが必要ですが、軽量なアドオンです。

## 手順 4: **画像 PDF を変換** する際の一般的なエッジケースへの対処

基本フローはほとんどの PDF で機能しますが、実務ではさまざまな例外が発生します。

| Situation | Why It Happens | How to Handle It |
|-----------|----------------|------------------|
| **回転したページ** | スキャナが自動でページを 90° 回転させることがあります。 | `ocrEngine.RotatePages = true` を `RecognizePdf` 呼び出し前に設定します。 |
| **混在言語** | 請求書にフランス語やドイツ語が混在していることがあります。 | `OcrLanguage.Multilingual` を使用するか、`|` で複数言語を組み合わせます（例: `OcrLanguage.English \| OcrLanguage.French`）。 |
| **大容量ファイル（> 100 ページ）** | 無料トライアルの制限で途中で処理が止まることがあります。 | ライセンスを購入するか、`Aspose.Pdf` を使って PDF を分割してから OCR を実行します。 |
| **低解像度スキャン** | 文字がぼやけ、OCR 精度が低下します。 | `ocrEngine.ImageResolution = 300`（デフォルトは 200）で DPI を上げます。 |

これらのシナリオに対処することで、**ocr convert pdf** パイプラインを本番環境でも堅牢に保てます。

## 手順 5: 全プロセスを自動化する（メソッドにまとめる）

請求書処理サービスを構築する場合、再利用可能なメソッドが欲しいでしょう。以下は、入力・出力パスを受け取り、回転処理を行い、抽出テキストを返すコンパクト版です。

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

次のように呼び出せます：

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

これで **画像 pdf を変換** → **検索可能な PDF** の完全なワークフローが完成です。任意の ASP.NET Core サービスやコンソールアプリにそのまま組み込めます。

## よくある質問 (FAQ)

**Q: macOS/Linux でも動作しますか？**  
A: はい。.NET 6 ランタイムと Aspose OCR はクロスプラットフォーム対応なので、Windows、macOS、Linux コンテナでも同じコードが動作します。

**Q: テキストだけが欲しくて検索可能な PDF が不要な場合は？**  
A: `OutputFormat` の設定をスキップし、`OutputFormat = OcrOutputFormat.Text` にします。エンジンが直接プレーンテキストを返します。

**Q: 元の PDF のメタデータを保持できますか？**  
A: できます。変換後、元の `Document` オブジェクトから `doc.Info.Title`、`doc.Info.Author` などを新しいドキュメントにコピーします。

**Q: ページ数に制限はありますか？**  
A: 無料トライアルはドキュメントあたり 20 ページまでです。フルライセンスを取得すれば制限は解除されます。

## 結論

これで **検索可能な PDF を作成** する方法が分かりました。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}