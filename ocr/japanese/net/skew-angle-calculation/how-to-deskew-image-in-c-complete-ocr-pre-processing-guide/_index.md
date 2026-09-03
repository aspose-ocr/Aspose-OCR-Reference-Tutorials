---
category: general
date: 2026-01-10
description: Aspose.OCRで画像の傾きを補正し、OCR結果を向上させる方法。OCR用に画像を前処理し、スキャンのノイズを除去し、スキャンからテキストを認識する方法を学びます。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: ja
og_description: 画像の傾きを補正し、OCR精度を向上させる方法。このガイドでは、OCR用に画像を前処理し、スキャンからノイズを除去し、Aspose.OCRを使用してスキャンからテキストを認識する方法を示します。
og_title: C#で画像の傾き補正を行う方法 – 完全なOCR前処理ガイド
tags:
- OCR
- C#
- Image Processing
title: C#で画像の傾き補正を行う方法 – 完全なOCR前処理ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像の傾きを補正する方法 – 完全な OCR 前処理ガイド

スキャンした文書を OCR エンジンに渡す前に **how to deskew image** したいと思ったことはありませんか？ あなただけではありません。スキャンされた文書はしばしば傾いていたり、ノイズが多かったり、コントラストが低かったりし、テキスト認識の精度を大きく下げてしまいます。  

このチュートリアルでは、**preprocess image for OCR** を行い、スキャンからノイズを除去し、最終的に Aspose.OCR ライブラリを使って **recognize text from scan** する完全な実行可能サンプルを段階的に解説します。最後まで読むと、C# で **how to use OCR** する方法がシンプルに理解でき、コードもコンパクトに保てます。

> **Pro tip:** たった 5‑10° の小さな回転でも OCR の精度が 30 % 以上低下することがあります。**Deskewing** は決して省いてはいけない最初のステップです。

---

## 必要なもの

- **.NET 6+**（コードは .NET Framework でも動作しますが、現在の LTS は .NET 6 です）
- **Aspose.OCR for .NET** – NuGet から取得できます（`Install-Package Aspose.OCR`）
- 回転またはノイズが入ったサンプル TIFF/PNG/JPEG（例では `noisy_rotated.tif` を使用）
- お好みの IDE – Visual Studio、Rider、または VS Code で構いません

以上です。追加のライブラリや外部サービスは不要です。

---

## Step 1 – Load the Source Image (Why It Matters)

**deskew image** を行う前に、画像を Aspose の `ImageStream` に読み込む必要があります。このオブジェクトはファイル I/O を抽象化し、OCR エンジンに一貫したインターフェイスを提供します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*なぜ最初に読み込むのか？* すべてのフィルタはメモリ上の画像に対して動作します。ファイルが読み込めなければ、パイプライン全体が機能しません。

---

## Step 2 – Build a Pre‑Processing Pipeline (Deskew + Denoise + Contrast)

堅牢な OCR ワークフローは通常、複数のフィルタをチェーンします。ここで **preprocess image for OCR** を行い、特に **how to deskew image** を自動的に実行します。

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**なぜこの 3 つか？**  
- **DeskewFilter** は「**how to deskew image**」の問題を自動で解決し、角度を推測する必要がありません。  
- **DenoiseFilter** は「**remove noise from scan**」の要件に対応し、幻の文字が出るのを防ぎます。  
- **ContrastBoostFilter** は OCR エンジンが暗い文字と明るい背景を区別しやすくするため、**preprocess image for OCR** の典型的な課題を解決します。

---

## Step 3 – Apply the Pipeline (Seeing the Transformation)

実際にフィルタを実行します。返される `processedImage` が OCR エンジンに渡す画像です。

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

`cleaned_output.tif` を開くと、テキストがまっすぐになり、粒子が減り、コントラストが向上していることが確認できます。これは **remove noise from scan** を行った後に **deskew** が正しく機能したかを視覚的にチェックするのに便利です。

---

## Step 4 – Create and Configure the OCR Engine (How to Use OCR)

整った画像が手に入ったら、`OcrEngine` をインスタンス化します。これが **how to use OCR** のコアです。

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*なぜ `AutoPageSegmentation` を設定するのか？* 多くのスキャンは表や複数列を含むため、これを有効にするとエンジンがページを賢く分割し、最終的な **recognize text from scan** の結果が向上します。

---

## Step 5 – Run the Recognition Process (Finally Recognize Text)

いよいよ本番です。エンジンにテキストの読み取りを指示します。

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

すべてが順調に進めば、元の文書と一致するクリーンなテキストブロックが得られます。これは **deskewing image**、**remove noise**、そして **preprocess image for OCR** を正しく行った成果です。

---

## Step 6 – Full Working Example (Copy‑Paste Ready)

以下はコンパイル可能な完全プログラムです。ファイルパスを置き換えるだけで実行できます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**期待される出力**（抜粋）:

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

出力が乱れている場合は、元画像が 30° 以上回転していないか確認するか、`DeskewFilter.MaxAngle` を増やしてください。

---

## Frequently Asked Questions (Edge Cases & Variations)

| Question | Answer |
|----------|--------|
| **What if my scan is rotated 45°?** | `DeskewFilter` は `MaxAngle` で上限を設定しています。`MaxAngle = 60` のように上げるか、パイプラインに渡す前に別のグラフィックライブラリで事前に回転させてください。 |
| **Can I process PDFs page‑by‑page?** | はい。各 PDF ページを画像に変換（例: `Aspose.Pdf` を使用）し、同じパイプラインを各ビットマップに適用します。 |
| **My document is in French – do I need to change anything?** | `ocrEngine.Language = Language.French;` またはカスタム言語パックをロードしてください。パイプライン自体は同じです。 |
| **Is there a way to keep the original resolution?** | `PreprocessPipeline` は元のビットマップ上で動作し、DPI を保持します。パフォーマンス上の理由でダウンスケールが必要な場合を除き、`ImageStream.Resize` は呼び出さないでください。 |
| **How does contrast boosting affect colored scans?** | `ContrastBoostFilter` は各チャンネルに対して動作するため、グレースケールでもカラーでも安全に使用できます。必要に応じて `new GrayscaleFilter()` で先にグレースケール変換しても構いません。 |

---

## Image Example (Visual Aid)

![画像の傾きを補正する例](/images/deskew-example.png)

*この画像は 12° 回転し、ノイズが入ったスキャンを **deskew** と **clean** したビフォー/アフターを示しています。*

---

## Conclusion

Aspose.OCR を使った **how to deskew image** の方法を解説し、完全な **preprocess image for OCR** パイプラインを実演し、**remove noise from scan** と **recognize text from scan** を数行の C# で実現しました。`DeskewFilter`、`DenoiseFilter`、`ContrastBoostFilter` を組み合わせることで、OCR エンジンがアーティファクトに悩まされずに済む整ったビットマップが得られます。  

次のステップは、フィルタ強度を調整したり、純粋な白黒出力のために `BinarizationFilter` を追加したり、クリーン画像を下流の NLP パイプラインに渡すことです。同じパターンは領収書、パスポート、歴史的文書などでも有効です。  

**how to use OCR** に関して他の言語やフレームワークでの質問があればコメントを残してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}