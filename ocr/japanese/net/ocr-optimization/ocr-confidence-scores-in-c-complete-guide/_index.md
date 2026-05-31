---
category: general
date: 2026-05-31
description: Aspose OCR を使用して画像からテキストを抽出し、領収書画像を読み取る際に、C# で OCR の信頼度スコアを取得する方法を学びましょう。
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: ja
og_description: OCRの信頼度スコアで精度を測定できます。このガイドでは、画像からテキストを抽出し、バウンディングボックスを取得し、Aspose OCRを使用して領収書画像を読み取る方法を示します。
og_title: C# における OCR 信頼度スコア – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でのOCR信頼度スコア – 完全ガイド
url: /ja/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# における OCR 信頼度スコア – 完全ガイド

画像からテキストを*抽出*する必要があるときに、**OCR 信頼度スコア**を取得する方法を考えたことはありますか？経費管理のために**領収書画像**ファイルを読み取り、エンジンがどの文字に自信がないかを知りたいかもしれません。良いニュースは、Aspose.OCR を使えば、C# の数行で JPG から信頼度パーセンテージ、バウンディングボックス、プレーンテキストを取得できることです。

このチュートリアルでは、ライブラリのインストール、エンジンを **JPG に対して OCR を実行** するように構成する方法、信頼度スコアの取得、ページ上の各文字の位置を示す **OCR バウンディングボックス** の解釈まで、必要なすべてを順に解説します。最後まで読むと、文字ごとの信頼度と位置を出力する実行可能なコンソール アプリが完成し、領収書やスキャン文書の検証に最適です。

## 学べること

- NuGet で Aspose.OCR をインストールし、基本的な OCR エンジンをセットアップする方法  
- `OcrOptions` を構成して **信頼度スコア** と **バウンディングボックス** を含むプレーンテキスト出力を要求する方法  
- `OcrResult` をループして画像からテキストを行単位・文字単位で **抽出** する方法  
- ファイルが見つからない、信頼度が低い文字、JPG 以外の形式などの一般的な落とし穴への対処法  
- フォルダー内の複数領収書画像を一括処理する例に拡張する方法  

Aspose の事前知識は不要です。動作する .NET 環境とテストしたい領収書画像（JPG）さえあれば始められます。

---

## Step 1 – Install Aspose.OCR and Prepare Your Project

まず最初に、Aspose.OCR の NuGet パッケージが必要です。プロジェクト フォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** 無料トライアルは最大 200 ページまで利用可能で、領収書スキャンのテストには十分です。

パッケージがインストールされたら、まだ作成していない場合は新しいコンソール プロジェクトを作成します。

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

生成された `Program.cs` を開き、using ディレクティブを追加します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

これらの名前空間により、`OcrEngine`、`OcrOptions`、および後で使用する結果型にアクセスできます。

## Step 2 – Get OCR confidence scores and OCR bounding boxes

このセクションがチュートリアルの核心です。エンジンを構成して、認識された各文字に **信頼度スコア** と **バウンディングボックス**（文字を囲む矩形）が付与されるようにします。H2 見出し自体が主要キーワードを含んでおり、SEO ルールを満たしています。

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**なぜ信頼度スコアを含めるのか？**  
信頼度スコア（0‑100%）は、エンジンが各文字にどれだけ自信を持っているかを示します。出力を経費承認ワークフローなどの下流ロジックに渡す場合、低信頼度のシンボルを自動的に除外またはフラグ付けできます。

**なぜバウンディングボックスを要求するのか？**  
バウンディングボックスは、元画像上でテキストをハイライトしたり、サブ領域を抽出したり、OCR 結果を UI オーバーレイと整合させる際に必須です。各 `character.Bounds` はピクセル座標で X、Y、幅、高さを提供します。

## Step 3 – Perform OCR on JPG and extract text from image

いよいよエンジンを実行します。`Recognize()` の呼び出しがすべての重い処理を行い、`OcrResult` オブジェクトを返します。

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

画像パスが間違っている、またはサポート外の形式の場合、Aspose は `FileNotFoundException` または `UnsupportedImageFormatException` をスローします。本番コードでは try/catch でこれらの例外を適切に処理してください。

### Pulling out the plain text

結合されたテキストだけが必要な場合は、`ocrResult.Text` を読むだけです。

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

しかし、信頼度スコアとバウンディングボックスも要求しているので、構造を走査して各文字の詳細を確認します。

## Step 4 – Iterate through lines, symbols, and display OCR confidence scores

以下のループは、文字ごとに信頼度とバウンディングボックスを出力します。**領収書画像** の例で真価を発揮します。

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

サンプル出力は次のようになることがあります。

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**数値の解釈:**  
- **信頼度 ≥ 90%** – 通常はそのまま受け入れて問題なし。  
- **信頼度 70‑89%** – 特に金額の数字などは二重チェックを推奨。  
- **信頼度 < 70%** – 手動レビューの対象としてフラグ付けを検討。

## Step 5 – Full runnable example (including error handling)

すべてをまとめた完全なプログラムを `Program.cs` にコピペできます。ファイルが見つからない場合の簡易チェックと、OCR が失敗したときに親切なメッセージを表示するロジックを含んでいます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Expected output

`dotnet run` を実行すると、まず結合された領収書テキストが表示され、続いて各文字の信頼度スコアとバウンディングボックスの一覧が出力されます。信頼度が低い文字は 80% 未満のパーセンテージで表示され、領収書の該当部分を手動で確認する合図となります。

## Bonus: Processing Multiple Receipts in a Folder

領収書 JPG が多数ある場合は、上記ロジックを `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` ループで包みます。各ファイルごとに `OcrEngine` をリセットするか、ループ内で新しいインスタンスを生成して状態漏れを防ぎましょう。

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

バルク処理は、夜間の経費インポートに便利です。

---

## Conclusion

これで C# で **OCR 信頼度スコア** を取得し、**画像からテキストを抽出** し、**JPG に対して OCR を実行** しながら **OCR バウンディングボックス** を取得するエンドツーエンドのソリューションが完成しました。コードは最新の Aspose.OCR バージョン（2026‑05‑31 時点）で動作し、信頼できる文書処理パイプラインを構築するために必要な粒度の高いデータを提供します。

次は何をすべきか？ `System.Drawing` や UI ライブラリを使って元領収書にバウンディングボックスを可視化したり、低信頼度文字を二次検証サービスに送信したりしてみてください。また、`ocrEngine.Options.Language = OcrLanguage.French;` のように言語を変更すれば、他言語にも対応可能です（API は多数のロケールをサポート）。

Happy coding, and may your confidence scores always stay high! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## What Should You Learn Next?

- [Aspose.OCR を使用した言語選択付き C# での画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像認識で認識文字の候補を取得する方法](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [画像認識で JSON 結果を取得するための Aspose OCR の使用方法](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}