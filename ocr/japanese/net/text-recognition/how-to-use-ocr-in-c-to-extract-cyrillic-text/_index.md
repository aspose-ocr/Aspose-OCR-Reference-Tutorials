---
category: general
date: 2026-09-10
description: C#でOCRを使用してキリル文字テキストを抽出し、画像を前処理し、単一の実行可能なサンプルでPDFまたはHTMLファイルに変換する方法。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: ja
lastmod: 2026-09-10
og_description: C#でOCRを使用してキリル文字テキストを抽出し、画像を前処理し、結果をPDFまたはHTMLとしてエクスポートする方法。ステップバイステップのガイドに従ってください。
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: C#でOCRを使用する方法 – キリル文字テキストを抽出し画像を変換する
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: C#でOCRを使用してキリル文字テキストを抽出する方法
url: /ja/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用してキリル文字を抽出する方法

スキャンしたドキュメントからキリル文字を抽出するためにC#で **OCRの使用方法** が必要な場合、本ガイドでは完全で実行可能なソリューションを示します。また、**OCR用の画像前処理** の方法や、テキストが認識された後に **画像をPDFに変換** または **画像をHTMLに変換** する方法も学べます。

文書デジタル化プロジェクトは、低品質なスキャンと結果を複数フォーマットで保存する必要という二つの問題に直面しがちです。このチュートリアルは、欠落した言語パックを自動でダウンロードし、組み込みの画像処理ヘルパーを提供し、OCR結果をワンコールでPDFまたはHTMLにエクスポートできる Aspose.OCR ライブラリを使用することで、両方の課題を解決します。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0 SDK 以降（コードは .NET Framework 4.7+ でも動作します）。
* Visual Studio 2022 または C# プロジェクトをサポートする任意のエディタ。
* **Aspose.OCR** NuGet パッケージ。以下でインストールします。

```bash
dotnet add package Aspose.OCR
```

* キリル文字を含む画像ファイル（例: `sample_cyrillic.jpg`）。  
  ファイルは `YOUR_DIRECTORY` として参照できるフォルダに配置してください。

`ocrEngine.Language = Language.Cyrillic;` を初めて設定したときに、ライブラリがキリル語言語パックを自動でダウンロードするため、手動でのダウンロードは不要です。

## Step 1 – Initialize the OCR engine (how to use OCR)

`OcrEngine` インスタンスを作成すると、以降のすべての操作のためのエンジンが準備されます。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Why this matters:** エンジンは言語、画像処理設定、出力オプションなどの構成情報を保持します。1 回だけ初期化すれば、残りのコードをすっきりさせ、スレッドセーフに保つことができます。

## Step 2 – Choose the Cyrillic language (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Why this matters:** OCR の精度は正しい言語モデルに大きく依存します。`Language.Cyrillic` を明示的に選択することで、ロシア語、ウクライナ語、ブルガリア語などに適した文字頻度テーブルがエンジンに適用されます。

## Step 3 – Preprocess the image for OCR

低品質なスキャンには歪み、斑点、照明ムラなどが含まれます。組み込みの `ImageProcessor` を使うだけで、認識率を大幅に向上させることができます。

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Why this matters:** 前処理により誤認識文字が減り、信頼度スコアが向上します。歪んだテキストは文字化けしやすいため、デスキューで直線化します。デスぺックリングは、OCR エンジンが文字と誤認識しがちな微小なアーティファクトを除去します。

> **Pro tip:** ソース画像がすでにクリアな場合は、これらの呼び出しを省略できます。大幅に劣化したスキャンの場合は、`Binarize()` や `ContrastStretch()` といった追加ステップを検討してください。

## Step 4 – Perform OCR on the input image

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Why this matters:** `Process` は提供されたビットマップ上で認識パイプラインを実行します。戻り値は `void` で、認識されたテキストは `Text` プロパティから取得できます。

## Step 5 – Retrieve the recognized text and save it to a file

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Why this matters:** 生テキストを保存することで、検索、インデックス作成、翻訳サービスへの入力など、下流の処理が可能になります。

## Step 6 – Export the OCR result to other formats (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Why this matters:** OCR 結果を PDF や HTML に変換すると、元画像のビジュアルコンテキストを保持しつつ検索可能なテキストを提供できます。これは法務やアーカイブのワークフローで特に有用です。

### Expected output

クリアなキリル文字スキャンでプログラムを実行すると、以下の 3 つのファイルが生成されます。

* `result.txt` – プレーンな Unicode テキスト、例: `Пример текста на кириллице`。
* `result.pdf` – 画像と検索用の不可視テキストレイヤーを含む PDF。
* `result.html` – 画像と選択可能なテキストを表示する HTML ページ。

いずれかのファイルを開き、キリル文字が正しく抽出されていることを確認してください。

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **What if the language pack fails to download?** | マシンがインターネットに接続されていることを確認してください。また、Aspose のサイトからパックを事前にダウンロードし、`bin` フォルダに配置することも可能です。 |
| **Can I recognize other alphabets in the same run?** | はい。`Process` の前に `ocrEngine.Language = Language.English;`（またはサポートされている任意の enum）を呼び出します。画像に複数のスクリプトが混在している場合は、言語ごとに `Process` を別々に実行する必要があります。 |
| **My image is a multi‑page TIFF – does this work?** | `OcrEngine` は 1 回に 1 つのビットマップを処理します。各ページを `Bitmap` にロードし、ループ内で `Process` を呼び出して結果を連結してください。 |
| **How do I increase performance for large batches?** | 単一の `OcrEngine` インスタンスを再利用し、`ocrEngine.OptimizeMemory = true;` を設定します。また、スレッドごとに別々のエンジンインスタンスを使用した並列処理も検討してください。 |

## Conclusion

これで **C#でOCRを使用してキリル文字を抽出する方法**、**OCR用の画像前処理**、そして **画像をPDFに変換** または **画像をHTMLに変換** を数ステップで実行できるようになりました。完全なサンプルは本番環境での利用を想定した実装例を示しています。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract OCR Text in C# – Complete Step‑by‑Step Guide](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}