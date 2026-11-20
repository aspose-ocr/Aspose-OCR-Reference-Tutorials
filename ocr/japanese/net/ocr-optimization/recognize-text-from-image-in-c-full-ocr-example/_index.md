---
category: general
date: 2026-06-22
description: C#で Aspose OCR を使用して画像からテキストを認識します。画像の自動デスケュー方法、OCR 用の画像前処理、そして簡潔な C#
  OCR サンプルで自動デスケューを有効にする方法を学びましょう。
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを認識します。このガイドでは、画像の自動傾き補正、OCR用の画像前処理、そして実用的なC#
  OCRサンプルで自動傾き補正を有効にする方法を示します。
og_title: C#で画像からテキストを認識する – 完全OCR例
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#で画像からテキストを認識する – 完全OCRサンプル
url: /ja/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを認識する – 完全 OCR 例

ぼやけたスキャンで髪の毛を抜くような苦労をせずに、C# アプリケーションで **画像からテキストを認識** する方法を考えたことはありませんか？ あなたは一人ではありません。領収書をデジタル化したり、フォームからデータを抽出したり、AI 搭載の画像トリックで遊んだりする場合でも、クリーンな OCR 結果を得るには適切な前処理が鍵です—たとえば auto deskew image とノイズ除去を考えてください。

このチュートリアルでは、Aspose.OCR ライブラリを使用した **c# ocr example** を順に解説します。この例では **enable auto deskew** を有効にし、傾いた写真を自動的に水平に補正し、**preprocess image for OCR** を数行のコードで実行します。最後まで実行すれば、認識されたテキストをコンソールに直接出力する実行可能なプログラムが手に入ります。

## 学べること

- Aspose.OCR NuGet パッケージのインストールと参照方法。  
- English 言語サポートで `OcrEngine` を設定する方法。  
- **auto deskew image** とその他の前処理オプションをワンステップで有効にする方法。  
- 実際の写真にエンジンを適用し、出力を処理する方法。  
- 大きく回転した画像や低コントラストスキャンなどのエッジケースへの対処ヒント。

> **Prerequisites** – .NET 6（以降）と C# の基本的な理解が必要です。OCR の事前経験は不要です。

## ## 画像からテキストを認識 – Aspose.OCR パッケージのインストール

コードを書く前に、ライブラリをプロジェクトに追加する必要があります。ソリューションフォルダーでターミナルを開き、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版 Aspose.OCR を取得し、OCR エンジン、言語パック、そして必要な前処理ユーティリティをバンドルします。  

*Pro tip:* .NET Framework を対象としている場合は、Visual Studio の NuGet パッケージ マネージャ UI を使用してください—“Aspose.OCR” を検索し、**Install** をクリックするだけです。

## ## 画像からテキストを認識 – OCR エンジンの初期化

パッケージの準備ができたので、エンジンを作成できます。最初のステップは、エンジンに期待する言語を指定することです。ほとんどの場合 English で十分ですが、ライブラリはデフォルトで数十の言語をサポートしています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Why this matters:**  
- `Language = OcrLanguage.English` はエンジンに使用する文字セットを指定し、精度を大幅に向上させます。  
- `Preprocessing` プロパティは `AutoDeskew` と `Denoise` の 2 つのフラグを組み合わせます。この **auto deskew image** ステップは画像を水平基線に戻し、`Denoise` は OCR エンジンを混乱させる粒状ノイズを除去します。  

前処理を省略すると、スキャンした領収書や斜めに撮った写真で文字化けした出力が頻繁に発生します。

## ## 画像からテキストを認識 – エンジンに画像を渡す

エンジンの準備が整ったら、次は画像ファイルを渡します。Aspose.OCR はパスまたは `Stream` を受け付けるので、ローカルファイル、埋め込みリソース、あるいはウェブからダウンロードした画像でも扱えます。

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**エッジケースの注意点:**  
- 画像が **heavily rotated**（45° 超）である場合、`AutoDeskew` は可能な限り補正しますが、`System.Drawing` や `ImageSharp` を使って手動で事前に回転させた方が確実です。  
- **multi‑page PDFs** に対しては `engine.RecognizePdf` を呼び出してください。同じ前処理フラグが適用されます。

## ## 画像からテキストを認識 – 結果の出力

最後に抽出したテキストを表示します。`result` オブジェクトは単なる文字列だけでなく、信頼度スコア、バウンディングボックス、ハイライトされた領域を持つ元画像も提供します。簡単なデモとしては `result.Text` を出力すれば十分です。

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

プログラムを実行すると、次のような出力が得られます：

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

出力が文字化けしている場合は、元画像が鮮明で十分に照明されているか、**preprocess image for OCR** が確実に有効になっているか（上記の `Preprocessing` フラグ）を再確認してください。

## ## 画像からテキストを認識 – 共通の落とし穴への対処

### 1. 低コントラストまたは暗い背景
Aspose.OCR は追加フラグ `PreprocessingOptions.ContrastEnhancement` を提供しています。`Preprocessing` 行に以下を追加してください：

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. 非英語文書
`OcrLanguage.English` を `OcrLanguage.Spanish`、`OcrLanguage.French` などに置き換えます。エンジンは自動的に適切な言語モデルをロードします。

### 3. 大きな画像
5 MP の写真を処理するとメモリを大量に消費します。まずサイズを縮小してください：

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. バウンディングボックスの取得
各単語の正確な位置が必要な場合（例: UI オーバーレイ用）は、`result.Regions` を反復処理します：

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## ## 画像からテキストを認識 – 完全動作サンプル

以下は、上記のすべてのポイントを組み込んだ **complete, copy‑and‑pasteable** プログラムです。`Program.cs` として保存し、`YOUR_DIRECTORY` をテスト画像が格納されているフォルダーに置き換えてから `dotnet run` を実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**期待されるコンソール出力**（画像がシンプルな領収書を含む場合）：

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

テキストがきれいに表示されれば、auto‑deskew と前処理を備えた **recognize text from image** に成功したことになります。おめでとうございます！

## ## 画像からテキストを認識 – 次のステップと関連トピック

- **Batch processing:** エンジン呼び出しを `foreach` ループでラップし、数十枚の写真を一括処理します。  
- **PDF conversion:** `engine.RecognizePdf` を使用してマルチページ文書を処理し、結果をマージします。  
- **Custom dictionaries:** `engine.CustomWords` に単語リストを渡すことで、医療コードなどドメイン固有用語の精度を向上させます。  
- **Performance tuning:** 多数の画像を処理する場合は `OcrEngine` インスタンスをキャッシュします。エンジンの生成が最もコストのかかるステップです。  

これらの拡張はすべて同じ概念—**preprocess image for OCR**、**enable auto deskew**、**recognize text from image**—を利用しているので、今回学んだコードパターンをそのまま再利用できます。

## Conclusion

今回の **c# ocr example** では、Aspose.OCR を使って **recognize text from image** を実現し、画像の自動デスクューとデノイズを行う方法を紹介しました。`AutoDeskew`（**auto deskew image** 機能）を有効にし、いくつかの前処理フラグを追加するだけで、画像操作コードを書かずに OCR の信頼性を大幅に向上させられます。

この雛形をベースに自分の画像を差し替え、請求書や身分証明書、紙媒体のあらゆる文書からデータを抽出し始めてください。難しいスキャンがありますか？ 前述の追加前処理オプションを試すか、カスタム言語パックで実験してみましょう。可能性は無限です。

このガイドが役に立ったら、コメントを残すか、結果を共有するか、GitHub で ping してください—ハッピーコーディング！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}