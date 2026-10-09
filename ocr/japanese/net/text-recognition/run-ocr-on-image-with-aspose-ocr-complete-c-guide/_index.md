---
category: general
date: 2026-02-17
description: C#でAspose OCRを使用して画像のOCRを実行します。jpgからテキストを抽出する方法、OCR用に画像を前処理する方法、ステップバイステップのコードで画像をOCRにロードする方法を学びます。
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: ja
og_description: C#でAspose OCRを使用して画像のOCRを実行します。このガイドでは、jpgからテキストを抽出し、画像を前処理し、OCR用に画像を読み込む方法を示します。
og_title: Aspose OCRで画像のOCRを実行する – 完全C#ガイド
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCRで画像のOCRを実行する – 完全なC#ガイド
url: /ja/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCRで画像のOCRを実行 – 完全なC#ガイド

画像ファイルに **OCRを実行したい** が、どこから始めればよいか分からないことはありませんか？請求書スキャナーやレシート管理アプリなど、実際のアプリでは JPEG から信頼できるテキストを取得することが最初のハードルです。朗報です！Aspose OCR を使えば、数行の C# コードで **画像にOCRを実行** でき、**jpgからテキストを抽出**、**OCR用に画像を前処理**、**OCR用に画像を読み込む** 方法も散在したドキュメントを探さずに学べます。

このチュートリアルでは、エンジンの設定、便利な前処理フィルタの追加、画像を認識エンジンに渡す手順、結果をコンソールに出力するまでの、コピー＆ペースト可能な完全なサンプルを順を追って解説します。最後まで読めば、任意の .NET プロジェクトに組み込んで即座に画像からテキストを取得できる自己完結型プログラムが手に入ります。

## 必要なもの

- .NET 6.0 以降（.NET Core でも動作します）  
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）  
- フォルダー内に配置したサンプル JPEG（`input.jpg`）  
- 基本的な C# 文法の理解（特別な知識は不要）

これらが揃っていれば、さっそく始めましょう。まだの場合は NuGet パッケージとテスト用画像を入手してください。本ガイドはそれらが用意できている前提で進めます。

## Step 1: OCR エンジンの作成 – 画像にOCRを実行するコア

**画像に OCR を実行** するために最初に行うべきことは `OcrEngine` をインスタンス化することです。このオブジェクトが認識に必要なすべての設定と状態を保持します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **重要ポイント:** `OcrEngine` は Aspose の認識パイプラインへのゲートウェイです。これがなければフィルタや言語パック、`Recognize` メソッドにアクセスできません。

## Step 2: 前処理フィルタの追加 – JPG からテキストを抽出する精度向上

カメラで撮影した画像はほとんどが完璧ではありません。傾きやノイズがあると、どんなに優秀な OCR アルゴリズムでも結果が悪くなります。**JPG からテキストを抽出** する前に数個のフィルタを適用すれば、結果が劇的に改善します。

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **プロのコツ:** ソース画像がすでにきれいな場合は `DenoiseGaussianFilter` を省略できます。過度の平滑化は薄い文字を消してしまうことがあります。

## Step 3: OCR 用に画像を読み込む – JPEG をエンジンに供給

次に **OCR 用に画像を読み込む** 作業です。Aspose は `ImageStream.FromFile` ヘルパーを提供しており、ファイルパスをエンジンが理解できるストリームにラップします。

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **エッジケース:** ファイルが存在しない場合、`FromFile` は `FileNotFoundException` をスローします。実行時にファイル欠損が予想される場合は try/catch でラップしてください。

## Step 4: 認識結果の取得と表示

エンジンの処理が完了したら、`Text` プロパティからプレーンテキスト結果を取得できます。コンソールに出力すれば簡単なデモが完成しますが、データベースやテキストファイルに書き出すことも可能です。

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

画像の内容に応じて出力は変わりますが、文字化けせずに整形されたテキストブロックが表示されるはずです。

![Diagram showing the OCR pipeline – run OCR on image, preprocess, load, recognize](/images/ocr-pipeline.png "画像のOCRパイプライン図")

### 各ステップが重要な理由

| Step | Purpose | What Happens If Skipped |
|------|---------|--------------------------|
| **Create engine** | 内部構造を初期化 | 認識器が利用できず `NullReferenceException` が発生 |
| **Add filters** | 回転やノイズを補正し精度向上 | 傾いたりノイズの多い画像は文字化けした出力になる |
| **Load image** | 生のビットマップをエンジンに提供 | エンジンに処理対象がなく、`Text` が空になる |
| **Read result** | プレーンテキストを取得し次の処理へ | OCR は実行されたが結果が見えず、実用的でない |

## よくあるバリエーションと調整方法

### 言語パックの変更

Aspose OCR は多数の言語を標準でサポートしています。フランス語やドイツ語など、**画像にOCRを実行** するファイルに別言語が含まれる場合は、`Recognize` を呼び出す前に `Language` プロパティを設定します。

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### マルチページ PDF の扱い

ソースが単一 JPEG ではなくマルチページ PDF の場合、各ページを画像に変換（Aspose.PDF 使用）してから同じパイプラインに流すことができます。ページごとのループはシンプルです。

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### 大容量ファイルへの対応

高解像度画像を処理するとメモリ使用量が急増します。**OCR 用に画像を読み込む** 前に画像をダウンサンプリングすると効果的です。

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## 完全版・すぐに実行できるサンプル

以下は本稿で説明したすべてを組み込んだ完成プログラムです。新しいコンソールプロジェクトにコピー＆ペーストし、`YOUR_DIRECTORY` を `input.jpg` が格納されたフォルダーに置き換えて **F5** を押すだけで動作します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### 結果の確認

1. プログラムを実行する。  
2. コンソールを確認 – `input.jpg` に含まれていたテキストが表示されるはずです。  
3. 出力が乱れている場合は、`DenoiseGaussianFilter` の `Sigma` 値を調整するか、`ContrastEnhancementFilter` などの追加フィルタを試してください。

## まとめと次のステップ

ここまでで、Aspose OCR を使って **画像にOCRを実行** する方法、エンジンの設定からクリーンなテキストの取得までを網羅しました。主なポイントは以下の通りです。

- `OcrEngine` インスタンスを作成する。  
- `DeskewFilter` や `DenoiseGaussianFilter` などで **OCR用に画像を前処理** する。  
- `ImageStream.FromFile` で **OCR用に画像を読み込む**。  
- `Recognize` を呼び出し、`ocrResult.Text` で **JPG からテキストを抽出** する。

さらに踏み込むなら次のアイデアを試してみてください。

- **バッチ処理** – フォルダー内の JPEG をすべて走査し、各結果を個別の `.txt` ファイルに出力。  
- **Azure Blob Storage との統合** – クラウド上の画像を取得し OCR を実行、テキストを再度保存。  
- **NLP と組み合わせ** – 抽出したテキストを言語理解モデルに渡し、請求書を自動分類。

フィルタの組み合わせや言語パック、PNG や TIFF への変更など、**OCR用に画像を読み込む** 手順さえ守れば同じパイプラインが機能します。ぜひ色々試してみてください。

---

問題が発生した場合はコメントを残すか、Aspose OCR の公式ドキュメントで高度な設定を確認してください。コーディングを楽しみながら、画像を検索可能なテキストに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}