---
category: general
date: 2026-03-20
description: Aspose OCR を使用して画像の傾きを補正し、ノイズを除去する方法を学びましょう。このステップバイステップガイドでは、OCR 用に画像を前処理する方法と
  OCR の精度を向上させる方法も紹介しています。
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: ja
og_description: Aspose OCRで画像の傾きを補正し、ノイズを除去する方法を学びましょう。数分でOCR精度を向上させます。
og_title: 画像の傾き補正方法 – OCR前処理のための完全C#ガイド
tags:
- OCR
- C#
- Image Processing
title: 画像の傾き補正方法 – OCR前処理の完全C#ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正 – OCR 前処理の完全 C# ガイド

スキャナーから奇妙な角度で出力された画像ファイルの **画像の傾き補正** 方法に悩んだことはありませんか？ あなただけではありません。多くの開発者が写真を OCR エンジンに投入しようとしたときにこの問題に直面します。 良いニュースは、数行の C# と Aspose OCR を使えば、Photoshop を使わずに画像をまっすぐにし、ノイズ除去し、コントラストを向上させるパイプラインを構築できることです。

このチュートリアルでは、傾いた画像の読み込みから **画像ノイズの除去**、**OCR 用画像の前処理**、そして最終的に **画像からテキストを認識** して **OCR 精度の向上** を実現するまでのすべてを解説します。最後には、乱れたスキャンをクリーンで検索可能なテキストに変換するコンソール アプリが完成します。

## 必要なもの

- .NET 6 以降（コードは `using var` 構文を使用します。C# 8 以降でサポート）
- Aspose OCR NuGet パッケージ（`Aspose.OCR`） – `dotnet add package Aspose.OCR` でインストール
- 傾いていてノイズがあるサンプル画像（例: `skewed_noisy.png`）
- お好みの IDE またはエディタ（Visual Studio、VS Code、Rider など）

> **プロのコツ:** サンプルファイルがない場合は、クリアなスクリーンショットを数度回転させ、画像エディタで「塩胡椒」ノイズを散布してください。パイプラインは同じように機能します。

## 手順 1: Deskew フィルタで画像の傾き補正

最初に回転を修正します。Aspose には `DeskewFilter` があり、設定可能な `MaxAngle` までの角度を自動検出できます。多くのスキャン文書では **5°** が安全なデフォルトです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**重要ポイント:**  
テキストが斜めだと OCR アルゴリズムが文字を誤認識しやすくなります（例: “l” が “i” になる）。**傾き補正** を最初に行うことで、エンジンにまっすぐなキャンバスを提供できます。

## 手順 2: Despeckle で画像ノイズを除去

安価なスマホや古いスキャナからのスキャンは、ランダムな点状ノイズが多く含まれます。これらの点は文字認識器を混乱させます。`DespeckleFilter` はエッジを保持しつつ画像を平滑化します。

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

ノイズ除去をより積極的に行いたい場合は、`Strength` を 3 や 4 に上げてください。ただし、細い筆跡が失われないよう注意が必要です。

## 手順 3: OCR 用画像の前処理 – コントラスト強調

薄いグレーの文字が白紙に印刷されたような低コントラストのスキャンは、OCR が文字を見逃す原因になります。`ContrastFilter` はトーン範囲を拡張し、暗いピクセルをさらに暗く、明るいピクセルをさらに明るくします。

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**例外ケース:** 元画像がすでに高コントラストの場合、このフィルタを適用するとディテールが失われることがあります。その場合は `Level` を `1.0` に設定して実質的に無効化してください。

## 手順 4: ソース画像の読み込みとクリーニング

ここで実際に画像を読み込み、先ほど組み立てたパイプラインに通します。

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **注:** `Apply` メソッドは新しい `Image` オブジェクトを返し、元の画像はそのままです。これにより、デバッグ時に「前」と「後」を簡単に比較できます。

## 手順 5: Aspose OCR で画像からテキストを認識

まっすぐでノイズがなく、コントラストが強調された画像が手元にできたら、いよいよ OCR エンジンに渡します。

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**期待される結果:** コンソールに元のスキャンのテキスト内容が出力されます。生のファイルを直接渡した場合に比べ、誤認識が大幅に減少します。

## 手順 6: OCR 精度の検証と向上

しっかりしたパイプラインでも、フォントが特殊な場合などはまだ文字がずれることがあります。**OCR 精度の向上** のための簡単なコツをいくつか紹介します。

| 問題 | クイック対策 |
|------|--------------|
| 小さな句読点が抜ける | コントラスト処理の前に `BinaryThresholdFilter` を追加 |
| 多言語（例: 英語 + スペイン語） | `ocrEngine.Language = Language.English | Language.Spanish;` |
| 背景が非常に暗い | 傾き補正の前に `new InvertFilter()` で画像を反転 |
| 大容量文書 | `Parallel.ForEach` でページを並列処理し、速度を向上 |

フィルタの順序を実験してみてください。低品質スキャンでは **コントラスト** を **デスぺックル** の前に適用した方が効果的なことがあります。

## 完全動作サンプル

以下は新しいコンソール プロジェクトにコピペできるフルプログラムです。これまで説明したすべての要素と、いくつかの安全チェックが含まれています。

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待出力**（サンプル画像に “Hello World!” が含まれている場合）:

```
=== OCR Output ===

Hello World!
```

文字化けが発生した場合は、パイプラインの順序を再確認するか、`DespeckleFilter.Strength` を上げてみてください。

## 結論

本稿では **画像の傾き補正**、**画像ノイズの除去**、**OCR 用画像の前処理**、そして Aspose OCR を使用した **画像からテキストの認識** を網羅し、**OCR 精度の向上** にも焦点を当てました。完全に実行可能なサンプルは、すべての手順をコンテキスト内で示しているので、任意の .NET プロジェクトに組み込んで即座にテキスト抽出を開始できます。

次のチャレンジに挑戦したいですか？ パイプラインを拡張してマルチページ PDF に対応させたり、マルチリンガル文書向けに言語パックを試したりしてみましょう。同じ概念が適用できます—`Language` フラグを変更し、必要に応じてページが逆さまの場合は `RotateFilter` を追加してください。

質問や、まだうまくいかない画像があればコメントで教えてください。一緒にトラブルシューティングしましょう。ハッピーコーディング！

![画像の傾き補正例](/images/deskew-example.png "Aspose OCR を使用した画像の傾き補正のイラスト")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}