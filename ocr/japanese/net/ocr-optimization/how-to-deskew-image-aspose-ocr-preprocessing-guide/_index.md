---
category: general
date: 2026-04-29
description: Aspose OCR を使用して画像の傾きを補正し、OCR の精度を向上させる方法 – ノイズ除去、画像コントラストの強化、画像からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: ja
og_description: 画像の傾きを補正し、OCR精度を向上させる方法。このチュートリアルでは、画像のノイズ除去、コントラスト強化、そして Aspose OCR
  を使用した画像からのテキスト抽出方法を示します。
og_title: 画像の傾き補正方法 – 完全な Aspose OCR ガイド
tags:
- Aspose OCR
- C#
- Image preprocessing
title: 画像の傾き補正方法 – Aspose OCR 前処理ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像のデスキュー方法 – 完全な Aspose OCR ガイド

OCR エンジンに渡す前に画像ファイルを **画像のデスキュー方法** することを考えたことがありますか？ あなただけではありません。斜めにスキャンされた画像や角度を付けて撮影した写真は、文字認識を乱れさせ、文字化けした出力になることがあります。  

このチュートリアルでは、**画像のデスキュー方法** だけでなく、**画像からノイズを除去**、**画像のコントラストを向上**、そして最終的に Aspose OCR を使用して **画像からテキストを抽出** する、完全なエンドツーエンドのソリューションを順を追って解説します。最後まで読むと、ドキュメントを探し回ることなく **OCR の精度を向上** させる方法が分かります。

> **得られるもの:** すぐに実行できる C# コンソール アプリ、各前処理ステップの明確な説明、そして自分のプロジェクトにコピーペーストできる実用的なヒントが数点です。

## 前提条件

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）  
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）  
- 傾いている、ノイズがある、または低コントラストのサンプル画像（例: `skewed_noisy.jpg`）  
- Visual Studio、VS Code、またはお好みの C# エディタ  

追加のネイティブ ライブラリは不要です – Aspose がプロセス内で全て処理します。

---

## Aspose OCR を使用した画像のデスキュー方法

最初に必要なのは、回転角度を補正するデスキューフィルタです。Aspose OCR には `FilterDeskew` が用意されており、テキストのベースラインを解析してビットマップを適切に回転させます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**デスキューから始める理由:**  
テキスト行が水平でない場合、OCR エンジンは斜めの文字を別のグリフとして解釈しようとし、結果として **OCR の精度を向上** が大幅に低下します。デスキューはベースラインを揃え、認識器にクリーンなキャンバスを提供します。

> *プロのコツ:* 事前に回転角度が分かっている場合（例: すべてのスキャンが 90° ずれているなど）、フィルタを省略して手動で回転させることができます – これによりわずかなパフォーマンス向上が得られます。

---

## 画像からノイズを除去 – スキャンをクリーンにする

ノイズはランダムな黒または白の斑点（いわゆる「塩胡椒」パターン）として現れ、文字のセグメンテーションを混乱させます。`FilterDenoise` はメディアンフィルタを適用し、エッジを保持しながらこれらを平滑化します。

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**強度を調整するタイミング:**  
- **Strength = 1** – 軽い粒子、処理が高速。  
- **Strength = 3** – 非常にノイズの多いスキャン（例: ファックス文書）。  

強度を上げすぎると細い線がぼやけ、**OCR の精度を向上** に悪影響を与える可能性があります。代表的なサンプルでいくつかの値をテストしてください。

---

## 画像のコントラストを向上 – 薄い文字を強調

低コントラストの画像（例えば色あせた領収書）は、OCR エンジンが薄いグリフを見逃す原因となります。`FilterContrastBoost` はヒストグラムを伸長させ、暗いピクセルをさらに暗く、明るいピクセルをさらに明るくします。

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**コントラストが重要な理由:**  
コントラストが高いと信号対雑音比が向上し、Aspose のニューラル認識器が “I” と “l” を区別しやすくなります。ただし、過度にブーストすると画像が飽和し、滑らかなグラデーションが硬いエッジに変わり、アーティファクトのように見えることがあります。バランスを目指し、1.5‑2.0 程度を目安にしてください。

---

## 画像からテキストを抽出 – 最終 OCR ステップ

画像がまっすぐでクリーンかつ鮮明になったので、OCR エンジンは本来の役割を果たせます。`Recognize` メソッドは、生テキスト、信頼度スコア、必要に応じてバウンディングボックスを含む `OcrResult` オブジェクトを返します。

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**サンプル出力**（ソース画像に “Invoice #12345” が含まれていると仮定）:

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

文字が抜けている場合は、前処理パイプラインを再確認してください – 画像にまだ強いデノイズや別のコントラストレベルが必要かもしれません。  

> *よくある質問:* “英語以外の言語を認識したい場合は？”  
> `ocrEngine.Language = Language.English;` を別のサポートされている言語（例: `Language.French`）に設定するだけです。前処理の手順は同じです。

---

## OCR の精度を向上 – 追加の調整

完璧なパイプラインでも、いくつかの追加設定で **OCR の精度を向上** させることができます:

| ヒント | 使用するタイミング | 方法 |
|-----|--------------|-----|
| **Binary Thresholding** | 非常に暗いまたは非常に明るいスキャン | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | 小さなフォント (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | 既知の文字集合（数字のみなど） | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | バッチ処理 | Loop over each page and reuse the same pipeline. |

覚えておいてください: 余分なフィルタは処理時間を増やすので、本当に必要なものだけを有効にしましょう。

---

## 完全な動作例（コピー＆ペースト可能）

以下はコンパイル可能な完全なプログラムです。`YOUR_DIRECTORY` を `skewed_noisy.jpg` が格納されているフォルダに置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**期待される結果:** コンソールにクリーンでまっすぐなテキストが出力され、`ocrEngine.Recognize` に生のファイルを直接渡す場合に比べて誤認識が大幅に減少します。

---

## 結論

本稿では、Aspose OCR を使用して **画像のデスキュー方法**、**画像からノイズを除去**、**画像のコントラストを向上**、そして最終的に **画像からテキストを抽出** する方法を取り上げました。これらのフィルタを連鎖させることで、特に低品質のスキャンにおいて **OCR の精度を向上** が顕著に向上することが確認できます。

次の課題に挑戦する準備はできましたか？ 同じパイプラインにマルチページ PDF を投入したり、二値化のカスタム閾値を試したりしてみてください。同じ原則が適用されます – まずデスキュー、次にクリーン、明るくし、最後に認識です。

質問や変わったケースがありますか？ コメントを残してください。一緒にトラブルシューティングしましょう。コーディングを楽しんで！  

![画像のデスキュー例](deskew-example.png "画像のデスキュー例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}