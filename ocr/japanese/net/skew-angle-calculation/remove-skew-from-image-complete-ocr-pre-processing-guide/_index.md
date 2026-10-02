---
category: general
date: 2026-02-14
description: Aspose OCR を C# で使用して、画像の傾きを除去し、OCR 用に画像を前処理し、画像のノイズを低減し、画像からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: ja
og_description: 画像の歪みを除去し、OCR用に画像を前処理し、Aspose OCR を使用したステップバイステップの C# チュートリアルで画像からテキストを抽出します。
og_title: 画像の傾き補正 – 完全なOCR前処理ガイド
tags:
- OCR
- CSharp
- ImageProcessing
title: 画像の傾き除去 – 完全なOCR前処理ガイド
url: /ja/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き除去 – 完全な OCR 前処理ガイド

OCR エンジンに渡す前に **画像の傾きを除去** したことがありますか？ あなただけではありません。スキャンした文書やレシートの写真、スクリーンショットはしばしば傾いて届き、その小さな角度がテキスト認識を妨げてしまいます。  

良いニュースです。Aspose OCR のフィルタをいくつか組み合わせるだけで、画像を真っすぐにし、ノイズを除去し、コントラストを上げ、そして **画像からテキストを抽出** する一連の流れをシームレスに実行できます。このガイドでは、傾いた画像を読み込むところから **文書からテキストを認識** し結果を出力するまでの全工程を順を追って解説します。

---

## 作成するもの

このチュートリアルの最後までに、以下の機能を持つ C# コンソール アプリが完成します。

1. `DeskewFilter` を使用して **画像の傾きを除去** する。
2. `DenoiseFilter` で **画像のノイズを低減** する。
3. コントラストを上げて **OCR 用に画像を前処理** する。
4. Aspose OCR の `Engine` を使って **文書からテキストを認識** する。
5. **画像からテキストを抽出** し、コンソールに表示する。

外部サービスは不要で、Aspose OCR の NuGet パッケージと数行のコードだけで実現できます。

---

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core や .NET Framework でも動作します）。  
- Visual Studio 2022 またはお好みのエディタ。  
- Aspose.OCR for .NET がインストール済み（`dotnet add package Aspose.OCR`）。  
- サンプル画像（`skewed_noisy.jpg`）を参照できるフォルダに配置。

上記が揃っていれば、さっそく始めましょう。

---

## Step 1: Load the Source Image

最初に必要なのは、クリーンアップしたいファイルを指す `ImageStream` です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Why this matters:** `ImageStream` は基になるビットマップを抽象化し、Raw ピクセル データを自分で管理しなくても Aspose フィルタが動作できるようにします。

---

## Step 2: Build a Pre‑processing Pipeline (Remove Skew & Reduce Noise)

各フィルタを個別に呼び出す代わりに、Aspose では `ImageProcessingPipeline` にチェーンでき、コードがすっきりし、処理順序も保証されます。

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### なぜ順序が重要か

1. **まず Deskew** – デノイズする前に画像を真っすぐにすると、ノイズフィルタが斜めのエッジをアーティファクトと誤認識しにくくなります。  
2. **次に Denoise** – 画像が水平になることで、アルゴリズムは信号と粒子をより正確に区別できます。  
3. **最後に Contrast Boost** – 画像がクリーンになった後にコントラストを上げることで、ノイズを増幅せずに OCR の可読性を最大化します。

---

## Step 3: Apply the Pipeline and Get a Cleaned Image

元のストリームに対してパイプラインを実行します。

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

この時点で画像は傾きが除去され、ノイズが低減され、コントラストが高くなっています。OCR に最適です。

---

## Step 4: Initialise the OCR Engine and Recognise Text

きれいになった画像を Aspose OCR に渡します。

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Tip:** 言語固有のチューニングが必要な場合は、`Engine` の `Language` プロパティを設定できます（例: `ocrEngine.Language = Language.English;`）。ラテン系の文書であればデフォルトで問題ありません。

---

## Step 5: Display the Extracted Text

`Console.WriteLine` で結果を簡単に表示できます。

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、`skewed_noisy.jpg` のテキスト内容が端末に出力されます。クリーンで読みやすく、次の処理にすぐ使えます。

---

## 完全動作サンプル

以下がコピー＆ペーストで使える完全版プログラムです。`Program.cs` として保存し、`YOUR_DIRECTORY` を実際のパスに置き換えて `dotnet run` を実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**期待される出力**（シンプルなレシートの例）:

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

出力が文字化けしている場合は、画像パスが正しいか、元ファイルに読み取れるテキストが含まれているかを再確認してください。

---

## よくある質問とエッジケース

### 画像がわずかな傾きではなく 90° 回転している場合は？

`DeskewFilter` は ±15° の小角度しか扱えません。全回転が必要なときは、Deskew の前に `new RotateFilter { Angle = 90 }` を呼び出します。

### 画像が PNG 形式の場合、何か変わりますか？

変わりません。`ImageStream.FromFile` がフォーマットを自動検出するので、PNG、JPEG、BMP、TIFF すべて同様に扱えます。

### ノイズ除去の強さはどう調整すれば？

`DenoiseFilter` の `Strength` プロパティ（0‑100）で調整できます。数値が大きいほど粒子は除去されますが、細部がぼやける可能性があります。テキスト中心の文書では 30‑50 前後が目安です。

### バッチ処理したい場合、パイプラインは再利用できますか？

できます。`processingPipeline` を一度作成し、各ファイルに対してループ処理します。

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

同じ `Engine` インスタンスを使い回すとパフォーマンスも向上します。

---

## 本番向け OCR のプロ・ティップ

- **パイプラインをキャッシュ**: フィルタを毎回インスタンス化すると高スループット環境でコストがかかります。  
- **OCR 言語を設定**: `ocrEngine.Language = Language.Spanish;` のように、英語以外の文書に対応させましょう。  
- **空結果の処理**: `ocrResult.Text?.Length > 0` を必ず確認してから次の処理に進みます。  
- **中間画像をログに残す**: `cleanedImage.Save("debug.png");` で中間結果を保存すると、フィルタパラメータの微調整がしやすくなります。

---

## 結論

本稿では、Aspose OCR の強力なフィルタ パイプラインを使って **画像の傾きを除去**、**画像のノイズを低減**、**OCR 用に画像を前処理**し、続いて **文書からテキストを認識**、最終的に **画像からテキストを抽出** する方法を示しました。全体のワークフローは 50 行未満の C# で実装でき、バッチ処理やカスタム言語モデル、追加フィルタへの拡張も容易です。

次のステップに進みませんか？ `BinarizeFilter` を追加して白黒出力にしたり、`ContrastBoostFilter` のレベルを変えて認識精度への影響を試したりしてみてください。パイプラインをいろいろ試すほど、各フィルタがクリーンな OCR 結果にどのように貢献するかが分かります。

Happy coding, and may your images always stay straight!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}