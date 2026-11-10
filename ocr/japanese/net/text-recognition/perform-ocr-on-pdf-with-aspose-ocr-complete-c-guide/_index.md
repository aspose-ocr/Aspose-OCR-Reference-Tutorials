---
category: general
date: 2026-06-03
description: Aspose.OCR を使用して PDF の OCR を実行し、スキャンされた PDF を検索可能な PDF に変換します。PDF からテキストを認識し、数分で検索可能な
  PDF を作成する方法を学びましょう。
draft: false
keywords:
- perform OCR on PDF
- recognize text from PDF
- how to create searchable PDF
- convert scanned PDF to searchable PDF
- convert image to searchable PDF
language: ja
og_description: PDFにOCRを実行し、すぐに検索可能なPDFを作成します。このチュートリアルでは、Aspose.OCRを使用してPDFからテキストを認識する方法をステップバイステップで示します。
og_title: PDFでOCRを実行する – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  headline: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  name: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  steps:
  - name: 1. Large Files & Memory Management
    text: If you’re processing PDFs larger than 100 MB, consider using `OcrEngineSettings.MemoryLimit`
      to cap memory usage. Additionally, process pages in batches to avoid `OutOfMemoryException`.
  - name: 2. Language Support
    text: 'By default Aspose.OCR assumes English. To recognize other languages, set
      the `Language` property:'
  - name: 3. Multi‑Threaded Scenarios
    text: '`OcrEngine` is **not** thread‑safe. If you need parallel processing, create
      a separate engine per thread.'
  - name: 4. Debugging OCR Accuracy
    text: 'You can extract the plain text from `ocrResult` for debugging:'
  - name: 5. Licensing Gotchas
    text: 'When you run the evaluation version, Aspose adds a watermark to the output
      PDF. Register your license early in the application:'
  type: HowTo
- questions:
  - answer: Absolutely. Replace `OcrImage.FromFile("input.pdf")` with the path to
      your image file. The engine will rasterize the image and embed the OCR layer
      just the same.
    question: Can I use this to convert a single image (PNG/JPEG) to a searchable
      PDF?
  - answer: The engine will overlay the OCR text on top of existing content, so native
      text stays selectable while scanned pages become searchable.
    question: What if my PDF has both scanned pages and native text?
  - answer: 'Accuracy hinges on source quality. Clean, high‑resolution scans (>300
      dpi) give >95 % accuracy. For noisy documents, enable `PreprocessSettings` (deskew,
      despeckle) before calling `Recognize`. --- ## Next Steps – Extending Your OCR
      Toolkit Now that you can **recognize text from PDF** and **convert s'
    question: How accurate is the OCR?
  type: FAQPage
tags:
- Aspose
- OCR
- C#
- PDF
title: Aspose.OCRでPDFのOCRを実行する – 完全なC#ガイド
url: /ja/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用した PDF の OCR 実行 – 完全 C# ガイド

PDF ファイルに **OCR を実行する方法** を、何十ものコマンドラインツールと格闘せずに知りたくありませんか？ あなたは一人ではありません。請求書のデジタル化、古いレポートのアーカイブ、あるいはスキャンした契約書の検索可能なバージョンが必要なとき、静的な PDF を実際に検索できる形に変えることは大きな変化です。

このガイドでは、Aspose.OCR for .NET を使用して、スキャンした PDF（さらには単純な画像）から **検索可能な PDF** を作成する手順を解説します。最後まで読めば、数行の C# コードで **PDF からテキストを認識** できるようになり、各ステップの背景を理解できるので、独自のプロジェクトに応用できます。

> **クイック要点:** このプロセスは 3 つのことに集約されます—OCR エンジンの初期化、ソース（PDF または画像）の投入、検索可能な PDF の保存。さっそく見ていきましょう。

---

## 必要なもの

開始する前に、以下を用意してください。

| 前提条件 | 理由 |
|--------------|----------------|
| **.NET 6.0+**（または .NET Framework 4.6+） | Aspose.OCR は最新ランタイムを対象としており、古いバージョンでは API の更新が欠ける可能性があります。 |
| **Aspose.OCR for .NET** NuGet パッケージ | `OcrEngine` クラスと PDF 処理ユーティリティを提供します。 |
| **有効な Aspose ライセンス**（または無料評価版） | ライセンスがないと 30 日間の評価制限と透かしが適用されます。 |
| **検索可能にしたいスキャン PDF**（または画像ファイル） | OCR の対象となるソースドキュメントです。 |
| **Visual Studio 2022**（または任意の C# エディタ） | デバッグが楽になりますが、任意の IDE でも構いません。 |

ライブラリは次の NuGet コマンドでインストールできます。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** CI パイプラインで作業する場合は、ビルド成果物にライセンスファイルを含め、実行時にロードしてパスをハードコーディングしないようにしましょう。

---

## PDF で OCR を実行 – Aspose.OCR のセットアップ

最初に必要なのは新しい `OcrEngine` インスタンスです。これはドキュメントを読み取る「脳」のようなものです。

```csharp
// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

なぜ毎回新しいインスタンスが必要かというと、エンジンは言語設定などの構成情報を保持しており、ドキュメントごとに異なる場合があります。実行ごとにインスタンス化することでクリーンな状態が保証され、ジョブ間の干渉を防げます。

---

## 検索可能 PDF の作成 – パスワード設定（任意）

PDF が保護されている場合、ページを読み取る前にエンジンにパスワードを伝える必要があります。

```csharp
// Step 2: (Optional) Provide the password if the PDF is protected
ocrEngine.Settings.PdfPassword = "mySecret";
```

保護されたファイルでこの手順を省略すると `PdfPasswordException` がスローされます。保護状態が不明な場合は必ず try‑catch で囲んでください。

---

## スキャン PDF を検索可能 PDF に変換 – ソースの読み込み

Aspose.OCR は `OcrImage` 抽象化を使用し、PDF、TIFF、JPEG などをラップできます。スキャン PDF をメモリに読み込む方法は次のとおりです。

```csharp
// Step 3: Load the scanned PDF that will be converted to a searchable PDF
var sourcePdf = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");
```

内部では `FromFile` が各ページをラスタ画像に変換し、OCR エンジンが処理できる形にします。マルチページ PDF でもエンジンは自動的にすべてのページを走査します。

---

## PDF からテキストを認識 – OCR の実行

チュートリアルの核心です。エンジンにテキスト認識を指示し、検索可能 PDF を出力させます。

```csharp
// Step 4: Perform OCR and request a searchable PDF as the output format
var ocrResult = ocrEngine.Recognize(sourcePdf, OutputFormat.SearchablePdf);
```

`OutputFormat.SearchablePdf` を指定すると、エンジンは元のスキャン画像の上に見えないテキスト層を埋め込みます。結果の PDF はスキャンのビジュアル fidelity を保ちつつ、完全に検索可能になります—コンプライアンス監査に最適です。

---

## 画像を検索可能 PDF に変換 – 結果の保存

最後にバイナリデータをディスクに書き出します。

```csharp
// Step 5: Save the resulting searchable PDF to disk
File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", ocrResult.Binary);
Console.WriteLine("Searchable PDF created.");
```

`Binary` プロパティには生の PDF バイト列が格納されています。API を構築している場合は、これを直接 Web 応答のストリームに送ることも可能です。

---

![検索可能 PDF を作成する OCR 変換フローを示す図](https://example.com/ocr-flow.png "PDF で OCR を実行するフローダイアグラム")

*画像代替テキスト: PDF で OCR を実行するフローダイアグラム。スキャン PDF が検索可能 PDF に変換される様子を示しています。*

---

## エッジケースと実践的なヒント

### 1. 大容量ファイルとメモリ管理
100 MB を超える PDF を処理する場合は、`OcrEngineSettings.MemoryLimit` を使用してメモリ使用量を上限設定してください。さらに、ページをバッチ処理することで `OutOfMemoryException` を回避できます。

```csharp
ocrEngine.Settings.MemoryLimit = 512; // MB
```

### 2. 言語サポート
デフォルトでは Aspose.OCR は英語を想定しています。他言語を認識させるには `Language` プロパティを設定します。

```csharp
ocrEngine.Settings.Language = Language.French; // or Language.Multilingual
```

### 3. マルチスレッドシナリオ
`OcrEngine` は **スレッドセーフではありません**。並列処理が必要な場合は、スレッドごとに別々のエンジンを作成してください。

### 4. OCR 精度のデバッグ
`ocrResult` からプレーンテキストを抽出してデバッグできます。

```csharp
string plainText = ocrResult.Text;
Console.WriteLine(plainText);
```

出力が文字化けしている場合は、`PreprocessSettings`（例: デスキュー、デスペックル）を調整して品質向上を試みてください。

### 5. ライセンスに関する注意点
評価版を使用すると、Aspose は出力 PDF に透かしを追加します。アプリケーション起動時に早めにライセンスを登録しましょう。

```csharp
var license = new License();
license.SetLicense("Aspose.OCR.lic");
```

---

## 完全動作サンプル – 最初から最後まで

以下は、上記のすべてのポイントを組み込んだ、すぐに実行可能なコンソールアプリのコードです。新しいコンソールプロジェクトにコピー＆ペーストして使用してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class PdfOcrDemo
{
    static void Main()
    {
        // Load license (replace with your actual license file)
        var license = new License();
        license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Optional: set PDF password if needed
        // ocrEngine.Settings.PdfPassword = "mySecret";

        // Optional: tweak memory usage for large files
        ocrEngine.Settings.MemoryLimit = 1024; // MB

        // 2️⃣ Load scanned PDF (or image) – adjust path as required
        var source = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");

        // 3️⃣ Perform OCR – ask for a searchable PDF output
        var result = ocrEngine.Recognize(source, OutputFormat.SearchablePdf);

        // 4️⃣ Save the searchable PDF
        string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
        File.WriteAllBytes(outputPath, result.Binary);

        Console.WriteLine($"Searchable PDF created at: {outputPath}");
    }
}
```

**期待される出力:** 実行後、コンソールにファイルの場所が表示されます。`output.pdf` を任意の PDF ビューアで開き、元のスキャンに含まれる単語を入力してみてください。文字がハイライトされれば、**PDF で OCR を実行し、検索可能なドキュメントを作成**できたことになります。

---

## よくある質問

**Q: 単一画像（PNG/JPEG）を検索可能 PDF に変換できますか？**  
A: もちろん可能です。`OcrImage.FromFile("input.pdf")` を画像ファイルへのパスに置き換えるだけです。エンジンは画像をラスタ化し、同様に OCR 層を埋め込みます。

**Q: PDF にスキャンページとネイティブテキストの両方が混在している場合は？**  
A: エンジンは既存のコンテンツ上に OCR テキストを重ねるため、ネイティブテキストは選択可能なまま、スキャンページは検索可能になります。

**Q: OCR の精度はどの程度ですか？**  
A: 精度は元データの品質に依存します。高解像度（>300 dpi）のクリーンなスキャンであれば 95 % 以上の精度が期待できます。ノイズが多い文書では、`PreprocessSettings`（デスキュー、デスペックル）を有効にしてから `Recognize` を呼び出すと改善します。

---

## 次のステップ – OCR ツールキットの拡張

**PDF からテキストを認識**し、**スキャン PDF を検索可能 PDF に変換**できるようになったので、以下のトピックに挑戦してみてください。

- **バッチ処理**: フォルダ内の PDF をループし、自動で検索可能バージョンを生成。  
- **テキスト抽出**: `ocrResult.Text` を利用して検索インデックス（例: Elasticsearch）に投入。  
- **カスタム言語パック**: Aspose から追加の言語データをダウンロードし、アジア系文字をサポート。  
- **PDF/A 準拠**: Aspose.PDF と OCR 出力を組み合わせ、アーカイブ向け PDF を作成。  

これらは本稿で扱った基本手順を基盤にしているため、すぐに実装に移せます。

---

## まとめ

本稿では **Aspose.OCR を使用して PDF に OCR を実行**し、スキャン PDF を完全に検索可能な PDF に変換する方法を示しました。また、画像から検索可能 PDF への変換手順もカバーしました。コード

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの説明と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}