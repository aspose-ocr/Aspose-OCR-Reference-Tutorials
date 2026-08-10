---
category: general
date: 2026-06-06
description: C# OCR を使用して画像からテキストを抽出します。OCR 用に画像を読み込む方法、スキャンした文書を認識する方法、そして数分で正確な結果を得る方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: ja
og_description: C#で画像からテキストを抽出する。このチュートリアルでは、OCR用に画像を読み込む方法、スキャンした文書を認識する方法、そしてC#
  OCRチュートリアルをステップバイステップでマスターする方法を示します。
og_title: C#で画像からテキストを抽出 – 完全OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: C#で画像からテキストを抽出 – 完全OCRチュートリアル
url: /ja/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – 完全 OCR チュートリアル

数行の C# だけで **画像からテキストを抽出** できる方法、気になりませんか？ あなたは一人ではありません。ノイズが多く、傾いたスキャン画像から文字を取り出す必要があるとき、多くの開発者が壁にぶつかります。従来の「コピー＆ペースト」手法では到底対応できません。  

このガイドでは、実践的な **c# OCR チュートリアル** として、**OCR 用に画像をロード** し、スマートな前処理を有効化し、最終的に **スキャンした文書** の内容をクリアに認識する方法をステップバイステップで解説します。最後まで読めば、任意の .NET プロジェクトに組み込める実行可能なプログラムが手に入ります。

## 本チュートリアルでカバーする内容

- Aspose.OCR（または互換パッケージ）NuGet パッケージのインストール  
- OCR エンジン インスタンスの作成と設定  
- **OCR 用に画像をロード** – ファイルパス、ストリーム、よくある落とし穴の取り扱い  
- デスクュー、デノイズ、コントラスト調整を自動で行う前処理の有効化  
- **スキャンした文書を認識** – プレーンテキスト結果の取得  
- すぐにコピー＆ペーストして実行できるフル ソースコード  

OCR の事前知識は不要です。C# と Visual Studio（またはお好みの IDE）さえあれば始められます。  

> **なぜ重要か？** テキスト抽出を自動化すれば、請求書処理、検索可能 PDF、データ入力の削減、さらには AI 用データセットの作成まで、さまざまな活用が可能になります。  

![C# OCR を使用した画像からテキストを抽出](/images/extract-text-from-image-csharp.png "extract text from image")

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Framework 4.8 でも動作します）  
- Visual Studio 2022（Community エディションで問題ありません）  
- NuGet パッケージ `Aspose.OCR`（または `OcrEngine`、`OcrResult` などを提供する任意のライブラリ）  

まだパッケージをインストールしていない場合は、以下を実行してください。

```bash
dotnet add package Aspose.OCR
```

この単一コマンドで、高性能 OCR に必要なすべてのネイティブ バイナリが取得されます。

---

## 手順 1: OCR エンジン インスタンスの作成

最初に行うのは、重い処理を担うエンジンを起動することです。`OcrEngine` は操作の中枢となる脳のようなものです。エンジンが起動すれば、画像を投入してテキストを取得できます。

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **プロのコツ:** バッチで多数の画像を処理する場合は、エンジンをシングルトンとして保持すると、内部リソースが再利用され、処理速度が向上します。

## 手順 2: 自動前処理の有効化

実際のスキャンは決して完璧ではありません。傾きやノイズ、コントラスト不足がつきものです。`AutoPreprocess` を有効にすると、エンジンは文字を解析する前に自動でデスクュー、デノイズ、コントラスト調整を行います。

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

なぜ重要かというと、前処理がなければ OCR エンジンは「8」を「B」と誤認したり、行全体を見逃したりする可能性があります。自動前処理はカスタム画像クリーニングコードを書く手間を省いてくれます。

## 手順 3: 認識言語の設定

多くの OCR ライブラリは言語パックを同梱しています。ここでは英語を設定しますが、`OcrLanguage.French`、`OcrLanguage.Spanish` など、文書に合わせて切り替えられます。

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

スキャンした文書に複数言語が混在している場合は、エンジンを2回実行するか、マルチリンガル モデルを使用するとよいでしょう（後述の検討項目）。

## 手順 4: OCR 用に画像をロード

ここで **OCR 用に画像をロード** します。`ImageStream.FromFile` ヘルパーは、エンジンが理解できる形式でファイルを読み込みます。パスが実際のファイルを指していることを確認してください。相対パスはプロジェクト フォルダーから実行したときに有効です。

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **よくあるミス:** スペースを含むパスをクオートせずに指定すると `FileNotFoundException` が発生します。`File.Exists` で事前にファイルの存在を確認する習慣をつけましょう。

## 手順 5: OCR 認識の実行

すべての設定が完了したら、いよいよ **スキャンした文書を認識** します。`Recognize` メソッドが本格的な処理を行い、抽出されたテキストと信頼度スコアを保持した `OcrResult` オブジェクトを返します。

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

各行の信頼度が必要な場合は、`ocrResult.Confidence`（0〜1 の浮動小数点）を確認してください。信頼度が低い場合は、前処理設定を調整するか、解像度の高い画像を提供すると改善します。

## 手順 6: 認識結果の出力

成功を確認する最も簡単な方法は、テキストをコンソールに出力することです。実際のアプリではファイルやデータベース、あるいは別サービスへの送信が一般的です。

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、次のような出力が得られます。

```
The quick brown fox jumps over the lazy dog.
```

たとえ元画像が少し歪んでいたりノイズが多くても、自動前処理により十分にクリアな出力が得られるはずです。

---

## 完全版ソースコード – すぐに実行できるサンプル

以下は新規コンソール プロジェクト（`dotnet new console`）に貼り付けて使用できる、上記手順をすべて網羅した完全プログラムです。簡易的なエラーハンドリングも含め、チュートリアルの堅牢性を高めています。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### 実行手順

1. 新規コンソール プロジェクト内に `Program.cs` としてコードを保存。  
2. プロジェクト ルートでターミナルを開く。  
3. `dotnet add package Aspose.OCR` を実行（未インストールの場合）。  
4. ビルドして実行：  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

抽出されたテキストと全体の信頼度パーセンテージがコンソールに表示されます。

---

## よくある質問 (FAQ)

**Q: PDF を直接処理できますか？**  
A: はい。多くの OCR ライブラリは PDF ページを画像ストリームとして読み込むか、`PdfDocument` API を提供しています。各ページを画像に変換してから同じ手順を適用してください。

**Q: 画像が PNG 形式の場合はどうすれば？**  
A: `ImageStream.FromFile` は JPEG、PNG、BMP、TIFF を標準でサポートしています。追加の変換は不要です。

**Q: 手書きノートの精度を上げるには？**  
A: 手書きは難易度が高いです。「handwriting」モデルを提供するライブラリを探すか、二値化やノイズ除去などの前処理を強化してからエンジンに渡すと効果的です。

**Q: 特定領域だけテキストを抽出する方法は？**  
A: 可能です。多くのエンジンは `Rect` や `Region` プロパティで OCR の対象領域を限定できます。フォームの固定フィールド抽出に便利です。

---

## 次のステップ & 関連トピック

この **c# OCR チュートリアル** で画像からテキストを抽出する基本をマスターしたら、以下のテーマにも挑戦してみてください。

- **バッチ処理** – ディレクトリ内の画像をループし、各結果を CSV に書き出す。  
- **PDF 生成** – 抽出したテキストと PDF ライブラリを組み合わせ、検索可能 PDF を作成。  
- **機械学習による後処理** – スペルチェッカーや言語モデルで OCR エラーを自動修正。  

これらはすべて、画像を OCR 用にロードし、エンジンを設定し、スキャン文書を認識するというコア概念に基づいています。

---

## 結論

本稿では、C# で **画像からテキストを抽出** するためのエンドツーエンド例を詳しく解説しました。`OcrEngine` の作成から最終的な文字列の出力まで、すべてのコード行に説明を付け、すぐに実行可能な形にしています。  

手順どおりに進めれば、ノイズが多いスキャンや領収書、手書きメモを数秒で検索可能かつ編集可能なテキストに変換できます。前処理フラグの調整や言語切替、バッチ処理への拡張など、さまざまな実験を続けてみてください。自動文書処理の世界はあなたの手の中にあります。

質問や面白いユースケースがあれば、ぜひコメントで共有してください。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの説明と完全なコード例が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Aspose.OCR .NET を使用した画像からテキストを抽出](/ocr/english/net/image-and-drawing-recognition/)
- [Aspose.OCR を用いた言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}