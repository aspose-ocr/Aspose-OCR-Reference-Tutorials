---
category: general
date: 2026-04-01
description: Aspose OCR を使用して C# で検索可能な PDF を作成 – スキャンした PDF を変換し、PDF に OCR を追加し、GPU
  アクセラレーションを有効にして高速な結果を得る方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: ja
og_description: C#で検索可能なPDFを素早く作成—スキャンしたPDFを変換し、PDFにOCRを追加し、高性能処理のためにGPUアクセラレーションを有効化します。
og_title: C#でAspose OCRを使用して検索可能なPDFを作成する
tags:
- Aspose OCR
- C#
- PDF processing
title: C#でAspose OCRを使用して検索可能なPDFを作成する
url: /ja/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した C# で検索可能な PDF を作成する

スキャンした文書の山から **create searchable PDF** ファイルを作成する必要がありますか？ あなた一人ではありません—多くのチームが画像のみの PDF をテキスト検索可能な資産に変換することに苦労しています。良いニュースは？ Aspose OCR を使えば、数行の C# コードで **scanned PDF** を完全に検索可能なバージョンに **変換** できます。このガイドでは、OCR を PDF に追加する方法から、速度向上のために **enable GPU acceleration** を有効にする方法まで、全プロセスを順に解説します。

また、**convert pdf to searchable** 形式への変換方法、**add OCR to PDF** が必要になる理由、そして大量バッチ処理の実用的なヒントも紹介します。最後まで読めば、任意の文書管理システムに投入できる検索可能な PDF を生成する、すぐに実行できるコンソールアプリが手に入ります。

---

## 必要なもの

- **.NET 6.0** 以上（API は .NET Framework でも動作しますが、.NET 6+ が推奨です）。
- **Aspose.OCR for .NET** NuGet パッケージ（`Install-Package Aspose.OCR`）。
- 入力として使用するスキャン済み PDF ファイル（画像のみ）。
- オプション: **enable GPU acceleration** を使用したい場合は、CUDA® がインストールされた GPU 対応マシン。

以上です—重い OCR エンジンや外部サービスは不要です。すべてローカルで実行されます。

---

## 検索可能な PDF の作成 – 手順概要

以下は、実行する高レベルのフローです：

1. **Initialize the OCR engine** – Aspose に検索する言語と GPU の使用有無を指示します。
2. **Point the engine at your scanned PDF** – 入力と出力のパスを定義します。
3. **Run the conversion** – Aspose が重い処理を行い、検索可能な PDF を書き出します。
4. **Verify the result** – 出力を開き、テキスト検索を試みます。

各ステップは個別のセクションに分かれているので、必要な部分だけを選んで実行できます。

---

## スキャン済み PDF を検索可能な PDF に変換する

最初に行うべきことは `OcrEngine` のインスタンスを作成することです。このオブジェクトは、PDF 内のラスタ画像を読み取りテキストを抽出する作業馬です。

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Why this works:** `ConvertToSearchablePdf` は各ページを読み取り、ラスタコンテンツに OCR を実行し、元の画像の背後に不可視のテキスト層を埋め込みます。結果は元のスキャン文書と全く同じに見えますが、テキストのコピー、選択、検索が可能になります。

---

## Aspose を使用して PDF に OCR を追加する

既に PDF を持っていて、ファイル全体を変換せずに **add OCR to PDF** したい場合は、同じメソッドを呼び出すだけで済みます—Aspose はこの操作を「OCR の追加」とみなします。上記のコードはすでにそれを行っていますが、以下はループで複数ファイルを処理する簡易バリエーションです：

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Tip:** バッチ全体で同じ `OcrEngine` インスタンスを使用してください。毎回再作成すると不要なオーバーヘッドが発生します。特に **enable GPU acceleration** を使用する場合は注意が必要です。

---

## 高速 OCR のための GPU 加速を有効にする

GPU 加速は大規模バッチの処理時間を数分短縮できます。Aspose OCR は内部で NVIDIA CUDA を利用しているため、ブールフラグを切り替えるだけです：

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**When to use it:** 10 MB を超える PDF を処理する場合や、数十ファイル以上を扱う場合、GPU は通常 2‑3 倍の速度向上をもたらします。CUDA 対応 GPU がない一般的なノートパソコンでは、`false` のままにしてください—ライブラリは自動的に CPU にフォールバックします。

**Common pit‑fall:** 正しい CUDA ドライバーバージョンをインストールし忘れると、ランタイム例外（`CudaException`）が発生します。ドライバーが Aspose が期待するバージョンと一致していることを確認してください（NuGet ページのリリースノートを参照）。

---

## 完全な動作例（すべての手順を統合）

以下は、コピーして新しい .NET プロジェクトに貼り付けられる自己完結型コンソールアプリです。役立つコメント、エラーハンドリング、そして処理したページ数を出力する最終検証ステップが含まれています。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Expected output**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

`output.pdf` を任意の PDF ビューアで開き、スキャン画像に含まれる単語を入力してみてください。テキストがハイライトされれば、**create searchable pdf** に成功したことになります。

---

## よくある落とし穴とプロのコツ

| Issue | Why it Happens | How to Fix / Avoid |
|-------|----------------|--------------------|
| **GPU が検出されない** | CUDA ドライバーが欠如しているか、バージョンが合っていない。 | Aspose のリリースノートに記載されたドライバーバージョンをインストールし、フォールバックとして `UseGpuAcceleration = false` を設定します。 |
| **言語設定が間違っている** | OCR はデフォルトで英語です。その他の言語は明示的に設定する必要があります。 | `Language = Language.Spanish`（またはサポートされている任意の列挙子）を変換前に設定します。 |
| **大きな PDF が OutOfMemory を引き起こす** | エンジンがページ全体をメモリにロードするためです。 | 各バッチで `ocrEngine.PageRange = new PageRange(1, 5)` を使用して PDF を分割処理します。 |
| **出力ファイルが破損している** | 出力先フォルダーに書き込み権限がありません。 | 管理者権限でアプリを実行するか、書き込み可能なパスを選択してください。 |
| **テキスト層が検索できない** | ビューアが古いバージョンをキャッシュしているため。 | PDF ビューアを更新するか、ファイルを再度開いてください。 |

**Pro tip:** スキャン済み PDF とネイティブ PDF が混在している場合、OCR を実行する前に各ページの `HasText` フラグ（`PdfPageInfo.HasText`）を確認してください。これにより CPU サイクルが節約でき、すでに検索可能なページでの二重 OCR を防げます。

---

## 結果をプログラムで検証する（オプション）

検証を自動化したい場合は、Aspose.PDF が隠しテキストを抽出できます：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

このスニペットは、単に画像を重ねただけでなく、実際に **convert pdf to searchable** 形式に変換したことを証明します。

---

## 画像例

![検索可能な PDF 出力例](https://example.com/images/searchable-pdf.png "Aspose OCR を使用した検索可能な PDF の作成")

*Alt text:* **create searchable pdf** の例で、前（スキャン）と後（検索可能）を示しています。

---

## 次のステップと関連トピック

- **Batch processing:** “Add OCR to PDF” セクションのループを Windows Service または Azure Function でラップし、夜間ジョブとして実行します。
- **Advanced language support:** 混在したスクリプトを含む文書向けに `ocrEngine.Language = Language.Multilingual` を検討してください。
- **Post‑OCR cleanup:** Aspose.PDF の `TextFragmentAbsorber` を使用して、一般的な OCR エラー（例: “0” と “O” の混同）を修正します。
- **Security

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}