---
category: general
date: 2026-03-07
description: Learn how to deskew image, boost contrast, and extract text from scan
  using Aspose OCR. Perform OCR on image with a full C# example and load image for
  OCR easily.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: ja
og_description: Aspose OCR を使用して C# で画像の傾き補正、コントラスト強化、スキャンからのテキスト抽出方法を学びましょう。ステップバイステップのコードで画像に
  OCR を実行します。
og_title: C#で画像の傾き補正とOCRを実行する方法 – 完全ガイド
tags:
- C#
- OCR
- Image Processing
title: C#で画像の傾き補正とOCRを行う方法 – 完全ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像の傾きを補正しOCRを実行する方法 – 完全ガイド

OCRを実行する前に **画像の傾きを補正する方法** が気になったことがあるなら、ここが最適です。このチュートリアルでは、コントラストの向上、OCR用の画像読み込み、そして最終的に **スキャンからテキストを抽出する** 方法を Aspose OCR を使って解説します。  

古い領収書をデジタル化したり、スキャンした契約書をきれいにしたり、傾いた写真からテキストを確実に読み取る必要がある場合でも、以下の手順ですべてカバーできます。余計な説明は省き、Visual Studio にそのまま貼り付けて動かせる実用的なサンプルをご提供します。  

## 本ガイドで達成できること

このガイドを最後まで実施すれば、以下が可能になります：

* 最大 30° の傾きを補正（**画像の傾きを補正する方法**）。  
* 文字のエッジを鮮明にするためのコントラスト向上（**コントラストを上げる方法**）。  
* 画像を OCR エンジンに読み込む（**OCR 用に画像をロード**）。  
* 認識プロセスを実行し、**スキャンからテキストを抽出**。  

すべて、執筆時点での最新 Aspose.OCR .NET NuGet パッケージ（v23.11）で動作します。  

---

![画像の傾きを補正する例](/images/deskew-example.png "画像の傾きを補正する方法")

*上の画像は、傾き補正前後のスキャンドキュメントを示しています。*

## 前提条件

* .NET 6.0 以上（コードは .NET Framework 4.7+ でも動作します）。  
* Visual Studio 2022（またはお好みの C# IDE）。  
* Aspose.OCR NuGet パッケージ – `dotnet add package Aspose.OCR` でインストール。  

以上です。外部サービスや API キーは不要です。

---

## Aspose OCR で画像の傾きを補正する方法

まず最初に **ImageProcessingPipeline** を作成し、`DeskewFilter` を追加します。このフィルタは支配的な文字行の角度を自動検出し、画像を水平に戻します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**重要ポイント：**  
傾いたスキャンは文字がベースラインと合わなくなるため OCR エンジンが混乱します。`DeskewFilter` は画像ヒストグラムを解析して角度を算出し、回転させることで認識精度を大幅に向上させます。

> **プロのコツ：** 文書の傾きが 15° を超えないことが分かっている場合は、`MaxAngle = 15` と設定すると処理が高速化します。

---

## 認識精度向上のためのコントラスト強化方法

傾き補正の後は、文字を際立たせることが次のステップです。`ContrastBoostFilter` はピクセルの輝度範囲を拡張し、特に薄く印刷された文字に有効です。

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**効果の理由：**  
コントラストが低いスキャンは文字が灰色っぽくなり、二値化処理で背景と誤認されやすくなります。コントラストを上げることで暗いピクセルはさらに暗く、明るいピクセルはさらに明るくなり、続く `BinarizationFilter` がクリーンなキャンバスを得られます。

---

## 画像で OCR を実行 – ファイルの読み込み

画像の前処理が完了したら、**OCR 用に画像をロード** する必要があります。Aspose では便利な `ImageStream.FromFile` ヘルパーが用意されています。

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

画像がストリーム（例：Web API でアップロードされたもの）にある場合は、`ImageStream.FromStream(yourStream)` を使用できます。エンジンは BMP、JPEG、PNG、TIFF など多数の形式をサポートしています。

---

## 認識プロセスを実行し、スキャンからテキストを抽出する

すべての設定が完了したら、`Recognize()` を呼び出すだけで本格的な処理が開始されます。呼び出し後、認識されたテキストは `ocrEngine.Text` から取得できます。

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**期待される出力例**（シンプルな請求書の場合）：

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

出力が文字化けしている場合は、パイプラインの順序を再確認してください。まず傾き補正、次にノイズ除去、コントラスト強化、最後に二値化の順に実行する必要があります。順序を入れ替えると結果が劣化します。

---

## よくある落とし穴と対処法

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **結果が空** | デフォルトの二値化手法では画像が暗すぎる／明るすぎる。 | `ContrastBoostFilter.Strength` を上げるか、`BinarizationMethod.Otsu` に切り替える。 |
| **一部の文字が抜ける** | ノイズ除去が不十分。 | 画像が軽度の場合は `DenoiseLevel.Medium` を使用するか、2 つ目の `DenoiseFilter` を追加。 |
| **回転方向が逆** | 文書に混在した向き（例：回転したページの写真）がある。 | `DeskewFilter.MaxAngle` を低めに設定し、`ImageProcessor.Rotate` で手動回転させる。 |
| **処理が遅い** | 高解像度画像の大量バッチ処理。 | パイプライン前に `ImageProcessor.Resize` で縮小するか、`Parallel.ForEach` で並列処理する。 |

---

## 完全動作サンプル（コピー＆ペースト可）

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

このコードを `Program.cs` として保存し、`dotnet run` を実行すると、コンソールに **スキャンからテキストを抽出** した結果が表示されます。  

---

## 次のステップと関連トピック

* **バッチ処理** – 上記ロジックをループで包み、数十ファイルを一括処理。  
* **カスタム言語パック** – ラテン文字以外を読む必要がある場合は、`ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;` のように言語モデルをロード。  
* **PDF 出力** – Aspose.PDF と OCR を組み合わせ、検索可能なテキストを直接 PDF に埋め込む。  
* **パフォーマンスチューニング** – `ImageProcessingPipeline` の順序を実験。ノイズ除去を先に行うと、ノイズが多い写真で高速になることがあります。  

これらはすべて、**画像の傾きを補正する方法**、**コントラストを上げる方法**、**OCR 用に画像をロード**、**画像で OCR を実行**、そして最終的に **スキャンからテキストを抽出** というコア概念に基づいています。

---

## まとめ

本稿では、C# で **画像の傾きを補正し** OCR を実行するための、実践的かつ本番環境でも使える手順を示しました。傾き補正フィルタ、ノイズ除去、コントラスト強化、二値化を順に組み合わせることで、Aspose OCR が安定して **スキャンからテキストを抽出** できるクリーンな入力が得られます。  

コードを試し、フィルタパラメータを自分の文書に合わせて調整すれば、認識精度がどれだけ向上するかすぐに実感できるはずです。質問があればコメントで教えてください。 happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}