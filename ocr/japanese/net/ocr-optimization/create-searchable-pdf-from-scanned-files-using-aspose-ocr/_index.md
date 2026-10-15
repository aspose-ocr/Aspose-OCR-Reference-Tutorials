---
category: general
date: 2026-01-04
description: スキャンした PDF からすぐに検索可能な PDF を作成します。スキャン PDF の変換方法、PDF への OCR の追加方法、そして
  C# で Aspose OCR を使用した画像品質の調整方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: ja
og_description: スキャンしたPDFからすぐに検索可能なPDFを作成します。ステップバイステップのガイドに従って、スキャンPDFを変換し、PDFにOCRを追加し、画像品質を調整してください。
og_title: Aspose OCR を使用してスキャンしたファイルから検索可能な PDF を作成する
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCR を使用してスキャンファイルから検索可能な PDF を作成する
url: /ja/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャンしたファイルから検索可能なPDFを作成する（Aspose OCR使用）

スキャンした文書の山から **検索可能なPDF** を作成したいと思ったことはありませんか？でも、どこから始めればいいか分からない…という方は多いです。ドキュメント管理パイプラインを構築する際に多くの開発者がこの壁にぶつかります。朗報です。Aspose OCR を使えば、**スキャンしたPDFを変換**し、OCR を適用し、画像品質を数行の C# コードで微調整できます。

このチュートリアルでは、スキャンした PDF を読み込んで完全に検索可能なバージョンとして保存するまでの全工程を順に解説します。最後まで読むと、Aspose で **OCR の使い方** が正確に分かり、各設定がなぜ重要か、うまくいかないときに何を調整すべきかが把握できます。曖昧な参照は一切なく、すぐにプロジェクトに組み込める実行可能なサンプルが手に入ります。

## Prerequisites

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）
- 有効な Aspose OCR ライセンス（無料トライアルでテスト可能）
- `input.pdf` という名前の入力 PDF を、管理できるフォルダーに配置してください
- Visual Studio 2022 またはお好みの C# エディタ

以上です。どれかが不明な場合は、まず不足しているものをインストールしてください。その他の前提条件は不要です。

## Step 1: Initialize the OCR Engine and Load the Scanned PDF  
**（ここで **PDF に OCR を追加** します。）**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*このステップの理由は？*  
`OcrEngine` は Aspose OCR の中核です。PDF を読み込むことで、エンジンは後で解析するラスタ画像の位置を把握します。これを省略すると変換対象がなく、次のステップで例外が発生します。

> **Pro tip:** PDF がパスワードで保護されている場合は、`ocrEngine.LoadPdf(path, password)` を使用して実行時エラーを回避してください。

## Step 2: Set Primary and Additional Languages  
**（**スキャンした PDF** を英語、フランス語、ドイツ語で変換します。）**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*言語設定が重要な理由は？*  
OCR の精度は期待する文字セットに依存します。英語をメイン言語に設定し、フランス語・ドイツ語を追加することで、アクセント文字や特殊グリフを正しく認識できます。設定を忘れると文字化けが頻発します。

## Step 3: Adjust Image Quality – Fine‑tune the PDF Output  
**（**画像品質を調整** してファイルサイズと可読性のバランスを取ります。）**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*`ImageQuality` を調整する理由は？*  
値を高く（90‑100）するとシャープさが保たれ、OCR の精度が向上しますが、ファイルサイズが大きくなります。何百万ページもアーカイブする場合は、70‑80 に下げることでサイズを削減しつつ可読性を大きく損なわない PDF が作れます。

## Step 4: Save the Result as a Searchable PDF  
**（ついに **検索可能な PDF** を作成し、インデックス化できるようにします。）**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*実際に何が起きているのか？*  
Aspose OCR は各ページからテキスト層を抽出し、元の画像の背後に埋め込みます。見た目は変わりませんが、テキストの選択・コピー・検索が可能になり、下流のワークフローが大幅に改善されます。

## Step 5: Verify the Output (Optional but Recommended)  
**（出力を確認します。省略可能ですが推奨します。）**

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

ファイルを開き、単語を選択してみるか、`Ctrl+F` で元のスキャンに存在するフレーズを入力してください。テキストが選択できれば **検索可能な PDF の作成** に成功しています。

## Common Edge Cases & How to Handle Them  

| Situation | Why It Happens | Quick Fix |
|-----------|----------------|-----------|
| **Mixed‑resolution pages** (some 150 dpi, others 300 dpi) | OCR の品質がページごとに異なり、検索性が不均一になる | `ocrEngine.Config.Dpi = 300;` をロード前に設定してアップサンプリングするか、`ImageProcessor` で DPI を正規化してください |
| **Encrypted PDF** | パスワードがないと Aspose OCR が読み取れない | 前述のように `LoadPdf` にパスワードを渡す |
| **Large PDFs (>500 MB)** | メモリ使用量が急増し `OutOfMemoryException` が発生 | `ocrEngine.SplitPdfIntoPages();` でページ単位に分割し、個別に OCR 後に結果をマージ |
| **Non‑Latin characters** (e.g., Cyrillic) | 言語が追加されていないため文字が “?” になる | `AdditionalLanguages` に `Language.Russian`（または必要な言語）を追加 |
| **Too low image quality** | 文字がぼやけて OCR が失敗 | `ImageQuality` を上げるか、`pdfOptions.Dpi = 300;` で高解像度画像を埋め込む |

## Full, Ready‑to‑Run Example  

以下は新しいコンソールアプリにそのまま貼り付けられる完全なプログラムです。全ステップ、エラーハンドリング、コメントが含まれています。

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**期待される出力:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

`output.pdf` を開くと、元のスキャンに含まれていたテキストを選択・検索できるはずです。

---

## Frequently Asked Questions (FAQs)

**Q: スキャン画像とネイティブテキストが混在する PDF でも動作しますか？**  
A: はい。Aspose OCR は必要な箇所にだけ隠しテキスト層を追加し、既存のテキストはそのまま残します。

**Q: フォルダー内の PDF を一括処理できますか？**  
A: 可能です。上記コードを `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` ループで囲み、出力パスを適宜変更してください。

**Q: 最終的な PDF サイズをさらに削減する方法は？**  
A: `ImageQuality` を 70‑80 に下げ、`Compress` を有効にするか、`pdfOptions.Dpi = 150` で埋め込む画像をダウンサンプリングしてください。

**Q: PDF を作成せずに OCR テキストだけ抽出できますか？**  
A: `ocrEngine.ExtractText();` を PDF 読み込み後に呼び出すと、プレーンテキスト文字列が返ります。これを保存またはインデックス化できます。

## Wrap‑Up  

今回は Aspose で **OCR の使い方** をマスターし、**検索可能な PDF の作成**、**スキャンした PDF の変換**、**PDF に OCR を追加**、そして **画像品質の調整** までを実践しました。フルコードサンプルはすぐに実行可能で、トラブルシューティング表が予期せぬ問題に対処する手助けになります。

次のステップとしては：

- 多言語アーカイブ向けに別言語パックを試す
- `ImageProcessor` でデスクューやデスペックルなどのカスタム前処理を行う
- 検索可能な PDF を SharePoint や ElasticSearch パイプラインに統合する

実装中に問題が発生したり、便利な工夫を見つけたらぜひコメントで共有してください。コーディングを楽しみながら、即座に検索可能な PDF を手に入れましょう！

![OCR エンジン → 言語設定 → PDF 保存オプション → 検索可能な PDF 出力 を示すフローチャート](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}