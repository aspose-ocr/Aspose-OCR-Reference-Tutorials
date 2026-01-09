---
category: general
date: 2026-01-09
description: C#でAspose OCRを使用してJPGのテキストを迅速に認識します。画像からテキストを抽出し、画像をJSONおよびEPUBに変換する方法を1つのチュートリアルで学びましょう。
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: ja
og_description: Aspose OCRでJPGのテキストを認識します。このガイドでは、画像からテキストを抽出し、画像をJSONやEPUBに変換し、画像からePubを作成する方法を示します。
og_title: JPGでテキストを認識する – 完全C#チュートリアル
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCRでJPGのテキストを認識する – 完全C#ガイド
url: /ja/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG 画像のテキスト認識 – 完全 C# ガイド

JPG ファイルの **テキスト認識** が必要だったことはありませんか？ どのライブラリを選べばよいか分からずに悩んだことがある方も多いでしょう。写真やスキャンした文書から文字を抽出しようとしたとき、多くの開発者が同じ壁にぶつかります。  

良いニュースです。Aspose OCR を使えば、数行の C# コードで **画像からテキストを抽出** でき、すぐに **画像を JSON に変換** したり **画像を EPUB に変換** したりできます—IDE を離れることはありません。

このチュートリアルでは、適切な NuGet パッケージのインストールから JPG のテキスト認識、結果を構造化された JSON および ePub ドキュメントとして保存するまで、全工程を順に解説します。最後まで実施すれば、**画像から ePub を作成** できるようになり、e‑ラーニングプラットフォームやデジタルライブラリ、検索可能な電子書籍が必要なアプリケーションに便利なテクニックとなります。

---

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。コードは最新のランタイムであればどれでも動作します。
- **Aspose.OCR** NuGet パッケージ – コア OCR エンジン。
- **Aspose.Publishing** NuGet パッケージ – ePub 出力形式に必要です。
- ディスク上の任意の場所にある `input.jpg` という名前の画像ファイル（パスはご自身の環境に合わせて変更してください）。
- テキストエディタまたは IDE（Visual Studio、VS Code、Rider など）

以上です。余計なサービスや外部 API は不要で、ライブラリと JPG ファイルだけで完結します。

---

## 手順 1: プロジェクトを **JPG のテキスト認識** 用に設定する

まず、新しいコンソール アプリケーションを作成します（既存プロジェクトに追加しても構いません）。次に、NuGet パッケージ マネージャーを使って 2 つの Aspose パッケージを追加します：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **プロのコツ:** Visual Studio を使用している場合、プロジェクトを右クリック → *NuGet パッケージの管理* → *Aspose.OCR* と *Aspose.Publishing* を検索し、**インストール** をクリックします。

これらのパッケージにより、**画像からテキストを抽出** し、後で ePub ファイルを出力するために必要なすべてが揃います。

---

## 手順 2: Aspose OCR を使用して **画像からテキストを抽出**

ここでは、JPG を読み込み文字を抽出するコードを書きます。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**このコードが機能する理由:** `OcrEngine` は低レベルの画像前処理、言語検出、文字セグメンテーションをすべて抽象化します。ファイルを指定するだけで、プレーンテキスト文字列（`ocrResult.Text`）と豊富なメタデータを含む `OcrResult` オブジェクトが返されます。

---

## 手順 3: **画像を JSON に変換** – OCR 結果のエクスポート

OCR の出力を構造化された形式（API、データベース、下流処理など）で保存したい場合、Aspose は結果を JSON にシリアライズする作業を簡単に行えます。

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

生成される JSON は概ね以下のようになります（簡略化しています）：

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**使用シーン:** OCR データをウェブサービスに渡す場合や、NoSQL ストアに保存する場合、あるいは任意の言語でパース可能な汎用的な表現が必要な場合に JSON は最適です。

---

## 手順 4: **画像を EPUB に変換** – 電子書籍として保存

Aspose Publishing は EPUB を含む複数の電子書籍フォーマットをサポートします。`OcrResult` の `Save` メソッドを呼び出すことで、認識されたテキストと（オプションで）元画像を含む完全に準拠した ePub ファイルを生成できます。

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**得られるもの:** 任意のリーダー（Calibre、Apple Books、Adobe Digital Editions など）で開ける ePub が生成されます。ファイルには検索可能なテキストコンテンツとして抽出された文字列と、背景レイヤーとして元画像が含まれます—**画像から ePub を作成** パイプラインに最適です。

---

## 手順 5: 完全動作サンプル – JPG から JSON と EPUB へ

すべてを統合した、実行可能な完全プログラムを以下に示します。`Program.cs` にコピー＆ペーストし、ファイルパスを調整して **F5** を押してください。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

プログラムを実行すると、次の 3 つが確認できます：

1. コンソールに認識されたテキストが表示される。
2. 構造化された OCR データを含む `output.json` ファイルが生成される。
3. 任意の電子書籍リーダーで開ける `output.epub` ファイルが生成される。

---

## よくある質問とエッジケース

- **画像が PNG や BMP の場合は？**  
  Aspose OCR はほとんどのラスタ形式（PNG、BMP、TIFF、GIF）をサポートしています。`inputPath` の拡張子を変更すれば、同じコードが動作します。

- **英語以外の言語を指定できますか？**  
  はい。`RecognizeImage` を呼び出す前に `ocrEngine.Language = OcrLanguage.French;`（またはサポートされている任意の言語）を設定してください。

- **マルチページ PDF はどうしますか？**  
  PDF の場合、まず各ページを画像に変換します（Aspose.PDF が可能）。その後、各画像を `RecognizeImage` に渡します。得られた `OcrResult` オブジェクトは、JSON や EPUB にエクスポートする前にマージできます。

- **信頼度スコアが低いです。精度を上げるには？**  
  画像を前処理します：コントラストを上げる、傾きを補正する、グレースケールに変換するなど。Aspose OCR には調整可能な `PreprocessOptions` も用意されています。

---

## 結論

これで、Aspose OCR を使用して **JPG ファイルのテキスト認識** を行い、データパイプライン用に **画像を JSON に変換**、検索可能な電子書籍を作成するために **画像を EPUB に変換** という、エンドツーエンドの確実な手順が手に入りました。この手法は軽量で、必要なのは 2 つの NuGet パッケージだけ、そして最新の .NET ランタイムすべてで動作します。

ここからは次のような活用が考えられます：

- JSON 出力を検索インデックス（Azure Cognitive Search、Elastic など）に統合する。
- 画像フォルダーをバッチ処理し、ePub 書籍のライブラリを生成する。
- 翻訳 API と組み合わせて、マルチ言語の電子書籍を自動的に作成する。

ぜひ試してみて、画像の品質を変えて実験し、OCR エンジンに重い処理を任せてください。コーディングを楽しんで！

![JPG 画像のテキスト認識 出力スクリーンショット](placeholder-image.png "JPG 画像のテキスト認識 例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}