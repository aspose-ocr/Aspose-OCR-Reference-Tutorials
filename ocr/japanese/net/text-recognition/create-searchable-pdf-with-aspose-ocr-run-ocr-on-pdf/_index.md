---
category: general
date: 2026-05-28
description: C# で Aspose OCR を使用して検索可能な PDF を作成する。PDF に OCR を実行し、テキストを認識し、OCR スキャンされた
  PDF を検索可能な PDF に変換する方法を学びます。
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: ja
og_description: C#でAspose OCRを使用して検索可能なPDFを作成します。PDFにOCRを実行し、テキストを認識し、OCRでスキャンされたPDFファイルを処理するためのステップバイステップガイドをご覧ください。
og_title: Aspose OCRで検索可能なPDFを作成 – PDFにOCRを実行
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Aspose OCRで検索可能なPDFを作成 – PDFにOCRを実行
url: /ja/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した検索可能 PDF の作成 – PDF で OCR を実行

スキャンした文書の山から **検索可能な PDF** ファイルを作成する必要がありましたか？ あなたは一人ではありません。多くのオフィスワークフローでは、完全に検索可能なアーカイブとあなたの間にある唯一の障壁は、PDF ページで OCR を実行する数行のコードです。  

このチュートリアルでは、Aspose OCR for .NET ライブラリを使用して **検索可能な PDF** ファイルを作成する方法を、完全に実行可能なサンプルを通して詳しく解説します。最後まで実施すれば、*PDF で OCR を実行* し、*テキスト PDF を認識* し、*OCR スキャン PDF* をサードパーティサービスを使わずに検索可能なバージョンに変換できるようになります。

> **Prerequisites** – 最近の .NET SDK（6.0 以上推奨）、有効な Aspose.OCR for .NET ライセンス（または一時的な評価キー）、そして処理したい PDF。

![Create searchable PDF diagram](alt="Aspose OCR を使用した検索可能 PDF ワークフローの図解")  

---

## 本ガイドでカバーする内容

- C# プロジェクトへの Aspose OCR ライブラリの設定方法。  
- ソース PDF の読み込み（ページ数は任意）。  
- **検索可能 PDF** を出力するようエンジンを構成。  
- OCR プロセスの実行と結果の保存。  
- 複数ページ文書、言語選択、一般的な落とし穴の対処法。  

各ステップを順に実行すれば、Adobe Reader でファイルを開き **Ctrl + F** を押すだけで、元のスキャンに含まれていた任意の単語を瞬時に検索できるようになります。

---

## Step 1: Install Aspose OCR for .NET

コードを書く前に、NuGet パッケージをプロジェクトに追加します。

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** `--version` フラグを使用して最新の安定版（例: `Aspose.OCR 23.10`）にロックすると、.NET 6 以降との互換性が確保されます。

---

## Step 2: Create an OCR Engine Instance

プロセスの中心となるのは `OcrEngine` です。画像を読み取りテキストを出力する「脳」のようなものです。初期化はとてもシンプルです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

`OcrEngine` オブジェクトは、入力画像ストリームと、Aspose に出力方法を指示する設定の両方を保持します。

---

## Step 3: Load the Source PDF (Run OCR on PDF)

Aspose OCR は PDF を直接取り込めます。内部で各ページを画像として抽出します。プレースホルダーのパスを、スキャンした文書の場所に置き換えてください。

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Why this works:** `ImageStream.FromFile` メソッドは PDF 形式を自動的に検出し、OCR 用のラスタ表現を準備します。追加の変換ステップは不要です。

---

## Step 4: Configure Output Format and Language

ここで Aspose に求める出力を指示します。`OutputFormat` を `SearchablePdf` に設定すると、エンジンは元のページ画像の背後に認識したテキストを埋め込み、**検索可能 PDF** を生成します。精度向上のために言語も指定できます—デフォルトは英語ですが、フランス語、ドイツ語などに切り替え可能です。

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

バイリンガル文書を処理する場合は、`Language` 列挙体のフラグを組み合わせて使用できます。

---

## Step 5: Run the OCR Process – Recognize Text PDF

いよいよ本格的な処理です。`Recognize` メソッドは全ページを走査し、グリフを抽出して、元画像と不可視テキスト層の両方を含む内部 PDF ストリームを構築します。これが *テキスト PDF を認識* するステップです。

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Common question:** *PDF が 200 ページあったらどうなるの？*  
> エンジンはページを順次処理しながらストリームで結果を出力するため、メモリ使用量は抑えられます。ただし、極端に大きなファイルの場合は `ocrEngine.Configuration` の `MemoryLimit` 設定を増やすことを検討してください。

---

## Step 6: Save the Searchable PDF

最後に出力をディスクに書き込みます。`Save` メソッドは内部ストリームを新しいファイルに保存し、任意の PDF ビューアで開くことができます。

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

プログラムを (`dotnet run`) 実行し、コンソールにファイル作成が確認されたら完了です。`handbook_searchable.pdf` を開き、元のスキャンに含まれていることが分かっている単語で検索してみてください—即座にヒットするはずです。

---

## Handling Edge Cases and Advanced Scenarios

### Multiple Languages (OCR Scanned PDF)

ソース PDF に英語とスペイン語の両方が混在している場合は、言語を組み合わせます。

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR はオンザフライで辞書を切り替え、混在言語文書の精度を向上させます。

### Password‑Protected PDFs

保護された PDF を扱う場合は、`Recognize` を呼び出す前にパスワードを設定します。

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

パスワードが間違っていると `Recognize` は `InvalidPasswordException` をスローします。例外を捕捉してユーザーに正しいパスワードを再入力させることができます。

### Controlling Image Quality

DPI を上げると OCR の精度は向上しますが、メモリ消費も増えます。文字化けが目立つ場合は DPI を調整してください。

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### License vs. Evaluation Mode

評価モードでは各ページに透かしが入ります。透かしを除去するには、OCR 呼び出しの前にライセンスを適用してください。

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Pro Tips for Production Use

- **バッチ処理:** コアロジックを `foreach` ループでラップし、PDF のリストを順に処理します。各ファイル処理後に `OcrEngine` を破棄してネイティブリソースを解放しましょう。  
- **ロギング:** `ocrEngine.Configuration.Logger` を使用して、1 秒あたりの認識文字数など詳細な OCR 統計を取得できます。精度低下のトラブルシューティングに非常に有用です。  
- **パフォーマンスチューニング:** マルチコアサーバーではスレッドごとに別々の `OcrEngine` インスタンスを生成します。インスタンスが分離されていればライブラリはスレッドセーフです。  
- **エラーハンドリング:** `Recognize` と `Save` は必ず `try/catch` で囲みます。代表的な例外は `FileNotFoundException`、`OutOfMemoryException`、`UnsupportedFormatException` です。

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Expected output** (console):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

生成されたファイルを開き **Ctrl + F** を押すと、元のスキャンページに含まれていた任意の単語をすぐに見つけられます。これが *OCR スキャン PDF* を **検索可能 PDF** に変換する魔法です。

---

## Conclusion

Aspose OCR for .NET を使って **検索可能 PDF** を作成する方法を、パッケージのインストールから多言語・パスワード保護 PDF の取り扱いまで網羅的に示しました。これらの手順に従えば、*PDF で OCR を実行* し、*テキスト PDF を認識* し、任意の *OCR スキャン PDF* を完全に検索可能な資産に変換できます。

### What’s Next?

- **aspose ocr pdf** API をさらに探求：プレーンテキスト抽出、DOCX へのエクスポート、または大量の検索可能 PDF の一括生成。  
- Aspose.PDF と組み合わせて、ブックマークや透かしを追加。  
- 異なる DPI 設定やカスタム OCR 辞書を試して、特殊フォントに最適化。

サンプルを自由にカスタマイズし、ドキュメント管理パイプラインに組み込んだり、コメントで質問したりしてください。コーディングを楽しみながら、読めないスキャンを検索可能な金鉱に変えましょう！

## Related Tutorials

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}