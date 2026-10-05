---
category: general
date: 2026-10-05
description: 画像からPDFへのOCRチュートリアルでは、OCR用に画像を読み込む方法、前処理を適用する手順、そしてAspose OCR C#の例を使用してキリル文字テキスト画像を抽出する方法を示しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- image to pdf OCR
- load image for OCR
- ocr image preprocessing steps
- aspose OCR C# example
- extract Cyrillic text image
language: ja
lastmod: 2026-10-05
og_description: 画像をPDFに変換するOCRガイドでは、OCR用に画像を読み込む方法、前処理ステップを適用する方法、そしてAspose OCR C#の例を使用してキリル文字テキスト画像を抽出する手順を案内します。
og_image_alt: Developer view of OCR converting an image to PDF with Aspose OCR in
  C#
og_title: C#でAspose OCRを使用した画像からPDFへのOCR – 完全例
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Image to PDF OCR tutorial shows how to load image for OCR, apply preprocessing
    steps, and extract Cyrillic text image using an Aspose OCR C# example.
  headline: 'Image to PDF OCR with Aspose OCR in C#: step‑by‑step guide'
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- PDF
- Image processing
title: C#でAspose OCRを使用した画像からPDFへのOCR：ステップバイステップガイド
url: /ja/net/ocr-optimization/image-to-pdf-ocr-with-aspose-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した C# の画像から PDF への OCR: ステップバイステップ ガイド

.NET アプリケーションで **image to PDF OCR** が必要な場合、本ガイドでは OCR 用に画像をロードし、前処理を行い、認識されたテキストを検索可能な PDF としてエクスポートする方法を詳しく解説します。画像からキリル文字テキストを抽出し、結果を PDF ファイルとして保存する完全な *Aspose OCR C# example* が示されます。

スキャンした文書を検索可能な PDF に変換することは、アーカイブ、コンプライアンス、またはデータ抽出パイプラインで一般的な要件です。このチュートリアルの最後までに、画像のロードから PDF 生成までのフル OCR ワークフローを実行できるプロジェクトが完成し、キリル文字を正しく処理できるようになります。

## 学習できること

- C# プロジェクトで **Aspose.OCR** ライブラリをインストールし、参照する方法。  
- Aspose の `Image.Load` メソッドを使用して **load image for OCR** を正しく行う方法。  
- 認識精度を向上させる重要な **OCR image preprocessing steps**（回転とデスクュー）。  
- エンジンを設定して **extract Cyrillic text image** を行い、検索可能な PDF を出力する方法。  
- 言語モジュールが欠如しているなどの一般的な落とし穴をトラブルシューティングするためのヒント。

### 前提条件

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 SDK またはそれ以降 | 例で使用されている C# 10 機能のランタイムを提供します。 |
| Visual Studio 2022（または .NET をサポートする任意の IDE） | プロジェクト作成とデバッグが容易になります。 |
| インターネット接続（初回実行時） | OCR エンジンがキリル文字言語モジュールを自動的にダウンロードできるようにします。 |
| キリル文字を含むサンプル画像（例: `sample_cyrillic.jpg`） | *extract Cyrillic text image* シナリオを示します。 |

> **Pro tip:** 企業プロキシの背後で作業している場合、初回実行前に `Resources.AutoDownload` プロパティを設定してプロキシ設定を使用してください。

## 手順 1: Aspose.OCR NuGet パッケージをインストールする

ソリューション フォルダーでターミナルを開き、次のコマンドを実行します:

```bash
dotnet add package Aspose.OCR
```

このパッケージには `Aspose.Ocr` 名前空間、OCR エンジン、および多言語認識に必要な言語リソースが含まれています。

## 手順 2: OCR 用に画像をロードする

最初の機能的ステップは、ソースファイルを `Aspose.Ocr.Image` オブジェクトに読み込むことです。フルパスを使用することで、現在の作業ディレクトリに関係なくエンジンがファイルを見つけられます。

```csharp
// Load the source image that contains Cyrillic text
var inputImage = Aspose.Ocr.Image.Load(@"C:\OCR\sample_cyrillic.jpg");
```

> **Why this matters:** 画像を早期にロードすることでピクセルデータにアクセスでき、前処理フェーズに必要です。`Image.Load` メソッドはファイル形式も検証し、サポートされていない画像の場合は明確な例外をスローします。

## 手順 3: キリル文字抽出のために OCR エンジンを設定する

Aspose OCR は多数の言語をサポートしていますが、期待する言語を明示的に設定する必要があります。キリル文字テキストの場合は `Language.Cyrillic` 列挙値を使用します。`Resources.AutoDownload` を有効にすると、コードを初めて実行したときに必要な言語モジュールが自動的に取得されます。

```csharp
using (var ocrEngine = new Aspose.Ocr.OcrEngine())
{
    // Select Cyrillic language to correctly recognize Russian, Ukrainian, etc.
    ocrEngine.Language = Aspose.Ocr.Language.Cyrillic;

    // Automatically download missing language modules (required on first run)
    ocrEngine.Resources.AutoDownload = true;
```

> **Why this matters:** 言語を設定しないとエンジンはデフォルトで英語になり、キリル文字の精度が大幅に低下します。

## 手順 4: OCR 画像の前処理ステップを適用する

前処理は一般的な画像の問題を修正することで OCR の品質を向上させます。例では最も効果的なオプションのうち 2 つを使用しています:

- **Rotate** – 画像が角度でスキャンされた場合にページを整列させます。  
- **Deskew** – 文字分割を混乱させる可能性のあるわずかな傾きを除去します。

```csharp
    // Preprocess the image: rotate to correct orientation and deskew to flatten text lines
    ocrEngine.PreprocessImage(
        inputImage,
        Aspose.Ocr.PreprocessOptions.Rotate |
        Aspose.Ocr.PreprocessOptions.Deskew);
```

> **How it works:** `PreprocessImage` は OCR エンジンが使用する内部ビットマップを作成します。ビット単位の OR 演算で複数のオプションを組み合わせ、追加コードなしでステップを連結できます。

## 手順 5: テキストを認識し PDF に変換する（image to PDF OCR）

画像が前処理され、言語が設定されたので、`Recognize` を呼び出します。このメソッドは `OcrResult` オブジェクトを返し、直接 PDF として保存できます。生成された PDF には隠しテキスト層が含まれ、検索可能になります。

```csharp
    // Perform OCR and ask for PDF output format
    var ocrResult = ocrEngine.Recognize(inputImage, Aspose.Ocr.OutputFormat.Pdf);
```

> **Result:** PDF には元のラスタ画像と、認識されたキリル文字に一致するテキストオーバーレイが含まれます。検索エンジンはこのテキストをインデックスでき、ユーザーはコピー＆ペーストが可能です。

## 手順 6: 検索可能な PDF を保存する

最後に、PDF をディスクに書き込みます。アプリケーションが書き込み権限を持つパスを選択してください。

```csharp
    // Save the searchable PDF to the desired location
    ocrResult.Save(@"C:\OCR\result.pdf");
}
```

### 期待される出力

`result.pdf` を任意の PDF ビューアで開くと、元の画像が表示され、認識されたキリル文字テキストを選択できるようになります。元画像に含まれる単語をすばやく検索すると、PDF 内の該当箇所がハイライトされます。

![OCR conversion result](/images/ocr-conversion.png){alt="Aspose OCR を使用した画像から PDF への OCR 変換を示すスクリーンショット（C#）"}

## 完全に実行可能なサンプル

以下はコンソール アプリケーションにコピーできる完全なプログラムです。必要なすべての `using` ディレクティブと、実稼働環境向けのエラーハンドリングが含まれています。

```csharp
// ------------------------------------------------------------
// Image to PDF OCR – Aspose OCR C# example
// ------------------------------------------------------------
using System;
using Aspose.Ocr;

namespace ImageToPdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the image that contains Cyrillic text
            const string inputPath = @"C:\OCR\sample_cyrillic.jpg";
            // Destination PDF file
            const string outputPath = @"C:\OCR\result.pdf";

            try
            {
                // Step 1: Load the image for OCR
                var inputImage = Image.Load(inputPath);

                // Step 2: Create and configure the OCR engine
                using (var ocrEngine = new OcrEngine())
                {
                    // Choose Cyrillic language
                    ocrEngine.Language = Language.Cyrillic;
                    // Enable automatic download of language resources
                    ocrEngine.Resources.AutoDownload = true;

                    // Step 3: Apply preprocessing (rotate + deskew)
                    ocrEngine.PreprocessImage(
                        inputImage,
                        PreprocessOptions.Rotate |
                        PreprocessOptions.Deskew);

                    // Step 4: Recognize and export as PDF (image to PDF OCR)
                    var ocrResult = ocrEngine.Recognize(
                        inputImage,
                        OutputFormat.Pdf);

                    // Step 5: Save the searchable PDF
                    ocrResult.Save(outputPath);
                }

                Console.WriteLine($"✅ OCR completed. PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
                // In a real application, consider logging the stack trace.
            }
        }
    }
}
```

プログラムを実行（`dotnet run`）し、`C:\OCR` に `result.pdf` が生成されていることを確認してください。コンソールに成功完了のメッセージが表示されます。

## よくある落とし穴と回避方法

| Symptom | Cause | Fix |
|---------|-------|-----|
| **PDF にキリル文字がない** | 言語がキリル文字に設定されていない。 | `ocrEngine.Language = Language.Cyrillic;` を設定してください。 |
| **PDF が空** | `Resources.AutoDownload` が無効で、言語モジュールが欠如している。 | `ocrEngine.Resources.AutoDownload = true;` を保持するか、Aspose のウェブサイトからキリル語モジュールを手動でダウンロードしてください。 |
| **回転したスキャンでの認識が不十分** | 前処理ステップが省略されている。 | `PreprocessOptions.Rotate` を追加し、必要に応じて `Deskew` も追加してください。 |
| **画像ロード時の `FileNotFoundException`** | 画像パスが間違っているか、ファイルが存在しません。 | 絶対パスを使用するか、ロード前にファイルが存在することを確認してください。 |
| **大きな画像でメモリ不足** | スケーリングせずに非常に高解像度の画像をロードしている。 | OCR 前に画像を縮小（`Image.Resize`）するか、プロセスのメモリ上限を増やしてください。 |

## サンプルの拡張

- **Multiple languages:** `ocrEngine.Language = Language.Cyrillic | Language.English;` を設定して、混在スクリプトを認識します。  
- **Different output formats:** `OutputFormat.Pdf` を `OutputFormat.Txt` または `OutputFormat.Docx` に置き換えて、プレーンテキストまたは Word 出力にします。  
- **Batch processing:** OCR ロジックを `foreach` ループでラップします。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.OCR を使用した言語選択付き画像テキスト抽出 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [C# で OCR を実行する方法 – Aspose OCR を使用した画像からのテキスト抽出](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)
- [.NET 用 Aspose.OCR を使用した画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}