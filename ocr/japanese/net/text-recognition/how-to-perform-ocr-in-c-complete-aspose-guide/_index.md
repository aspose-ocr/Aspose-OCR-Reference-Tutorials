---
category: general
date: 2026-02-16
description: Aspose.OCR を使用して C# で OCR を実行する方法を学びましょう – 写真からテキストを認識し、スキャンからテキストを読み取り、レシートから高精度でテキストを抽出します。
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: ja
og_description: Aspose.OCR を使用した C# での OCR の実行方法を学びましょう。このガイドでは、写真からテキストを認識し、スキャンからテキストを読み取り、レシートからテキストを抽出する方法を示します。
og_title: C#でOCRを実行する方法 – 完全なAsposeガイド
tags:
- C#
- Aspose.OCR
- Image Processing
title: C#でOCRを実行する方法 – 完全なAsposeガイド
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を実行する方法 – 完全 Aspose ガイド

ぼやけたレシートやスマートフォンで撮影したランダムな写真で **OCR を実行する方法** を知りたくありませんか？ あなただけではありません。実際のアプリでは、**写真からテキストを認識** したり、**スキャンした文書からテキストを読み取る** ことや、**レシート画像からテキストを抽出** する必要がありますが、データをクラウドサービスに送信したくないこともあります。  

このチュートリアルでは、Aspose.OCR を使って **OCR を実行する方法** を示す自己完結型のサンプルを順に解説し、途中で **OCR の精度を向上させる** ヒントも紹介します。最後まで読めば、任意の画像からプレーンテキストを抽出できる C# コンソールプログラムがすぐに実行できるようになります。

> **必要なもの**  
> * .NET 6 SDK（または最近の .NET バージョン）  
> * Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）  
> * サンプル画像 – 例として `photo_receipt.jpg` という名前のレシート写真  

これらに心当たりがあるなら、さっそく始めましょう。

![how to perform OCR example](image.png){alt="OCR の実行方法"}

## Aspose.OCR を使った C# での OCR 実行手順

最初のステップは OCR エンジンを設定し、英語の言語モデルをロードすることです。これが **OCR を実行する方法** の核心で、言語モデルがなければエンジンはどの文字を探すべきか分かりません。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*なぜ重要か*: 正しい言語モデルをロードすることで認識速度と精度が直接影響を受けます。英語は最も一般的ですが、Aspose にはフランス語やドイツ語など、**スキャンした文書からテキストを読み取る** 必要がある場合に備えて多数のモデルが同梱されています。

## 写真からテキストを認識する

スマートフォンで撮影した写真は回転やノイズ、コントラスト低下が起こりやすいです。エンジンに **写真からテキストを認識** させる前に、画像をクリーンアップする前処理オプションを設定します。

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*プロのコツ*: 文字が抜けていると感じたら、`DenoiseLevel` を `High` に変更したり、`BinarizeMethod.Sauvola` を使用してみてください。これらの調整は **OCR の精度を向上させる** 戦略の一部です。

## スキャン画像からテキストを読み取る

エンジンの準備ができたら画像をロードします。JPEG として保存されたスキャン PDF ページでも、印刷されたフォームの写真でも、コードは同じです。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

ファイルパスの代わりに `Stream` がある場合は、`FromFile` を `FromStream` に置き換えるだけです。この柔軟性は、Web アップロードから取得した **スキャンした画像からテキストを読み取る** ときに便利です。

## レシートからテキストを抽出する

すべての準備が整ったら、実際の OCR 呼び出しはたった一行です。メソッドは抽出されたプレーンテキスト文字列を返すので、表示したり保存したり、別システムに渡したりできます。

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**期待される出力**（シンプルなレシートの例）:

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

出力が文字化けしている場合は、前処理セクションを見直してください。ここが **OCR の精度を向上させる** 最も一般的なポイントです。

## OCR の精度を向上させる – 高度な調整

デフォルト設定で多くのケースはカバーできますが、実運用向けパイプラインでは追加の調整が必要になることがあります。

| 状況 | 調整 | 理由 |
|-----------|------------|--------|
| 背景が非常に暗い | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | テキストと背景の分離が向上 |
| 手書きメモ | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | 手書き筆跡用の専門モデル |
| 複数ページのスキャン | 各ページ画像をループし、イテレーションごとに `Recognize()` を呼び出す | メモリ使用量を抑制 |
| 大きな画像（> 2000 px） | OCR に渡す前にリサイズ (`Image.Resize(width, height)`) | 処理が速くなり、メモリ消費が減少 |

覚えておいてほしいのは、**OCR を実行する方法** は一律のレシピではなく、出力が求める品質になるまでこれらのノブを試行錯誤する必要があるということです。

## 完全動作サンプル

以下はコピー＆ペーストでそのまま使える完全版プログラムです。これまで説明したすべての要素に加えて、ファイルの存在を確認する小さなヘルパーも含まれています。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

`dotnet run` でプログラムを実行してください。正しく設定されていれば、抽出されたテキストがコンソールに表示されます。

## よくある質問とエッジケース

**Q: 画像が PDF の場合はどうすればいいですか？**  
A: まず各 PDF ページを画像に変換します（例: `Aspose.Pdf` や `PdfSharp` を使用）。変換後のビットマップを `ocrEngine.Image` に渡します。

**Q: 画像を並列処理できますか？**  
A: 可能ですが、スレッドごとに別々の `OcrEngine` インスタンスを作成してください。エンジンはスレッドセーフではなく、単一インスタンスを共有すると競合が発生します。

**Q: Linux でも動作しますか？**  
A: 完全に対応しています。Linux 上の .NET Core ではネイティブ依存関係（`libgdiplus` など）をインストールしておく必要があります。

**Q: 多言語のレシートに対応するには？**  
A: 認識前に複数の言語モデルをロードします:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
エンジンは順番に各モデルを試みます。

## 結論

これで C# と Aspose.OCR を使った **OCR を実行する方法** のエンドツーエンドの解答が手に入りました。チュートリアルではエンジンの初期化、**写真からテキストを認識**、**スキャンした文書からテキストを読み取る**、**レシートからテキストを抽出** までを網羅し、**OCR の精度を向上させる** 実践的な方法も紹介しました。  

次のステップは、英語モデルを手書きモデルに差し替えてみたり、さまざまな `BinarizeMethod` の値を試したり、アップロードをリアルタイムで処理する ASP.NET API に OCR 呼び出しを組み込んでみることです。画像のバリエーション次第で可能性は無限に広がります。

OCR、画像前処理、または Aspose ライブラリ全般についてさらに質問があれば、コメントを残すか、公式の Aspose.OCR ドキュメントで詳細を確認してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}