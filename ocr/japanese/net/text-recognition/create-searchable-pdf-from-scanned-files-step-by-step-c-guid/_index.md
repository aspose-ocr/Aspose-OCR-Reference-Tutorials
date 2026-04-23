---
category: general
date: 2026-03-17
description: OCRでスキャンしたPDFを変換し、すぐに検索可能なPDFを作成します。OCRの実行方法やPDFからのテキスト抽出などを学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: ja
og_description: スキャンした文書から検索可能なPDFを作成します。このガイドでは、スキャンしたPDFを変換し、OCRを実行し、C# を使用してテキストを抽出する方法を示します。
og_title: 検索可能なPDFを作成 – 完全なC# OCRチュートリアル
tags:
- OCR
- PDF
- C#
- .NET
title: スキャンしたファイルから検索可能なPDFを作成する – ステップバイステップ C# ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能なPDFを作成 – 完全なC#チュートリアル

スキャンしたページの山から **検索可能なPDFを作成** したことがありますか？古い契約書をデジタル化しているか、Windows Explorer でPDFを検索可能にしたいだけかもしれません。いずれにせよ、**スキャンしたpdfを変換**して実際に検索できる形にしたいと考えているでしょう。  

良いニュースです。C# の数行と OCR エンジンさえあれば、画像ベースの PDF を完全に検索可能な PDF に変換できます—外部サービスは不要です。このチュートリアルでは、ライブラリのインストールからテキスト抽出まで、全プロセスを順に解説し、各ステップの「なぜ」を説明するので、内部で何が起きているかをしっかり理解できます。  

> **Quick answer:** `PdfConversionMode = PdfConversionMode.SearchablePdf` を設定し、スキャンしたファイルを渡して `Recognize()` を呼び出し、結果を保存すれば完了です。  

以下に、今日すぐに動作させるために必要なすべての情報を示します。

---

## 必要なもの

| 前提条件 | 重要な理由 |
|--------------|----------------|
| .NET 6 以降（または .NET Framework 4.7+） | 使用する OCR SDK はこれらのランタイムを対象としています。 |
| Visual Studio 2022（または任意の C# IDE） | デバッグと NuGet の管理が楽になります。 |
| NuGet 対応の OCR ライブラリ（例: **Aspose.OCR** または **Tesseract.NET**） | コードで示した `OcrEngine` クラスを提供します。 |
| テスト用のスキャン済み PDF ファイル | これを検索可能な PDF に変換します。 |

既にプロジェクトがある場合は、Package Manager Console から OCR パッケージを追加するだけです：

```powershell
Install-Package Aspose.OCR
```

*(`Aspose.OCR` をご自身の選択したライブラリに置き換えてください；デモで使用している API はかなり汎用的です。)*

---

## ステップバイステップ実装

各ステップの下には、コピー＆ペーストできる正確な C# コードと、その行が存在する **理由** の簡単な説明を掲載しています。

### ステップ 1: OCR エンジンの初期化  

エンジンの作成は最初に行うべきです。なぜなら、認識実行に必要なすべての設定と状態を保持するからです。

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

**Pro tip:** 複数のファイルで単一の `OcrEngine` インスタンスを再利用すると、特に大量バッチ処理時のメモリ使用量が削減されます。

### ステップ 2: 検索可能な PDF 用にエンジンを設定  

エンジンはプレーンテキスト、画像、または検索可能な PDF を出力できます。正しいモードを設定すると、ライブラリは元のページ画像の背後に不可視のテキスト層を埋め込むよう指示します。

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*なぜ？* このフラグがないと、OCR の実行は認識されたテキストの `string` だけを返すだけで、元のページレイアウトが必要な場合には役に立ちません。

### ステップ 3: スキャンしたドキュメントの読み込み  

ほとんどの OCR SDK は `Image` または `ImageStream` を受け取ります。ここでは、PDF ファイルを読み込み、各ページを画像として扱うヘルパーを使用しています。

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

**Edge case:** PDF にラスターページとベクターページが混在している場合、エンジンによってはベクターページをスキップすることがあります。そのような場合は、OCR エンジンに渡す前に PDF を画像に事前変換（例: Ghostscript 使用）してください。

### ステップ 4: OCR 認識の実行  

`Recognize()` を呼び出すことで、重い処理（テキスト検出、言語モデリング、PDF 生成）が裏で実行されます。

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

**extract text from pdf** が必要な場合は、`ocrResult.Text` から取得できます：

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### ステップ 5: 検索可能な PDF の保存  

最後に、出力をディスクに書き込みます。`PdfDocument` プロパティには、不可視テキストオーバーレイが付いた完全な PDF が保持されています。

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

`searchable.pdf` を Adobe Reader や Edge で開くと、検索ボックスに単語を入力して一致する場所へ直接ジャンプできるようになります—まるでネイティブ PDF のように。

---

## 結果の検証

1. 任意の PDF ビューアで生成されたファイルを開きます。  
2. **Ctrl + F** を押し、スキャンしたページに確実に存在する単語を入力します。  
3. ビューアがその語句をハイライトすれば、**create searchable pdf** に成功したことになります。

何も見つからない場合は、元の PDF に実際に読み取れるテキストが含まれているか再確認してください（スキャンが低解像度すぎて OCR が何も認識できないことがあります）。OCR 前に DPI を上げる（例: `ocrEngine.Config.Dpi = 300`）と効果的なことが多いです。

---

## よくある落とし穴と対処法

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| 空白の検索可能 PDF | `PdfConversionMode` がデフォルト（画像のみ）のまま | `PdfConversionMode = PdfConversionMode.SearchablePdf` を設定する。 |
| 文字化け | 言語モデルが間違っている | `ocrEngine.Config.Language = Language.English;`（または適切な言語） |
| 大きなファイルで処理が遅い | エンジンがページごとに再初期化される | 同じ `OcrEngine` インスタンスを再利用するか、ライブラリがサポートしていればマルチスレッド化を有効にする。 |
| 変換後にテキストが検索できない | 入力 PDF がベクターのみ（ラスタ画像がない） | まず PDF ページを画像にレンダリングする（例: Aspose.PDF の `PdfRenderer`）。 |

---

## ボーナス: 検索可能な PDF から直接テキストを抽出  

インデックス作成や分析のために生テキストが必要になることがあります。`ocrResult` がすでに `Text` を提供しているので、PDF を再度開く手間は省けます。ただし、後で PDF ファイルだけが手元にある場合は、PDF テキスト抽出ツールを使用してください：

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

これで **extract text from pdf** を OCR を再実行せずに取得できます—多数のファイルを処理する際の便利なショートカットです。

---

## 完全な動作例（すべてのステップを1つのファイルにまとめたもの）

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**期待される出力**（簡略化）:

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

同じスニペットが2回表示されれば、OCR が成功し、PDF に検索可能なテキスト層が含まれています。

---

## 次のステップと関連トピック

- **Batch processing:** スキャンした PDF のフォルダーをループし、同じ `OcrEngine` インスタンスを再利用してスループットを向上させます。  
- **Language detection:** 多言語アーカイブの場合、ファイルメタデータに基づいて `ocrEngine.Config.Language` を動的に切り替えます。  
- **PDF/A compliance:** 業界によってはアーカイブ用 PDF が必要です。SDK がサポートしていれば `PdfConversionMode = PdfConversionMode.SearchablePdfA` を設定してください。  
- **Performance tuning:** `ocrEngine.Config.UseParallelProcessing = true`（利用可能な場合）を試して、大規模ジョブの速度を向上させます。  

これらすべては、**how to run OCR** を効率的に実行し、**create searchable pdf** ファイルを即座にインデックス可能にするという基本概念に基づいています。

---

## 結論

これで、任意のスキャンドキュメントを **create searchable pdf** の傑作に変えるための、完全で本番環境対応のレシピが手に入りました。OCR エンジンの設定、ソースの読み込み、認識の実行、結果の保存という全パイプライン（生画像から検索可能でテキスト抽出可能な PDF へ）を網羅しました。  
自分のファイルで試してみて、DPI や言語設定を調整すれば、

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}