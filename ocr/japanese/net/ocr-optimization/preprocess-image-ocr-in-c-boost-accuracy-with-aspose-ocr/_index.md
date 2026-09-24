---
category: general
date: 2026-01-01
description: 画像OCRを前処理して精度を向上させます。テキスト画像の認識方法、OCR精度の改善、画像OCRの読み込みとAspose OCRを使用したOCRテキストの表示方法を学びます。
draft: false
keywords:
- preprocess image ocr
- recognize text image
- improve ocr accuracy
- display ocr text
- load image ocr
language: ja
og_description: 画像OCRを前処理して精度を向上させます。このガイドでは、テキスト画像の認識、画像OCRの読み込み、フィルタの適用、そしてOCRテキストの表示方法を示します。
og_title: C#で画像OCRを前処理 – Aspose OCRで精度向上
tags:
- Aspose OCR
- C#
- Image preprocessing
title: C#で画像OCRを前処理 – Aspose OCRで精度向上
url: /ja/net/ocr-optimization/preprocess-image-ocr-in-c-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# preprocess image ocr in C# – Boost Accuracy with Aspose OCR

ページ上の文字を実際に読めるように **preprocess image ocr** したことがありますか？同じ悩みを抱える開発者は多いです。ノイズが多く、傾いたスキャン画像がエンジンと協調しないことが壁になります。朗報は、いくつかの賢い前処理ステップで、災害現場のような画像をきれいで読み取り可能なテキストに変えることができるということです。

このチュートリアルでは、**recognize text image** ファイルを認識し、**improve OCR accuracy** し、最終的にコンソールに **display OCR text** を表示する、完全に実行可能なサンプルを順を追って解説します。最後まで読めば、**load image OCR** アセットの読み込み方法、傾き補正やノイズ除去といったフィルタの適用方法、そして信頼できる結果の取得方法を Aspose.OCR for .NET で習得できます。

## What You’ll Learn

- `OcrEngine` インスタンスの作成と前処理フィルタの設定方法。  
- **improve OCR accuracy** において傾き補正とデノイズフィルタが重要な理由。  
- **load image ocr** ファイルを読み込んで認識を実行する正確なコード。  
- ユーザーフレンドリーに **display OCR text** を出力する方法。  
- 実務で役立つヒント、落とし穴、オプションの調整方法。

### Prerequisites

- .NET 6+（または .NET Framework 4.7+）がマシンにインストールされていること。  
- Aspose.OCR のライセンス（デモ用の無料トライアルで可）。  
- 基本的な C# の知識—高度なテクニックは不要です。  

これらに心当たりがなければ、まずは不足しているものをインストールしてください。残りの手順はすべて前提が整っていることを想定しています。

---

## preprocess image ocr – Setting Up Filters

最初に理解すべきは **why preprocessing matters** です。OCR エンジンは鮮明で正面から撮影された文字を得意としますが、実際のスキャンは回転やぼやけ、背景ノイズが付きものです。クリーンな画像をエンジンに渡すことで、正しい文字起こしの可能性が大幅に向上します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters.
        //    • SkewCorrectionFilter: straightens tilted text.
        //    • DenoiseFilter: removes speckles and grain.
        ocrEngine.Settings.PreprocessingFilters.Add(new SkewCorrectionFilter());
        ocrEngine.Settings.PreprocessingFilters.Add(new DenoiseFilter());

        // 3️⃣ (Optional) Fine‑tune filter parameters.
        // ((SkewCorrectionFilter)ocrEngine.Settings.PreprocessingFilters[0]).MaxAngle = 25;

        // 4️⃣ Load the image you want to run OCR on.
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition.
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣ Show the recognized text.
        Console.WriteLine("Corrected text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ここで何が起きているのか？**  
- **Step 1** でエンジン（Aspose OCR ライブラリの中心）を作成します。  
- **Step 2** で 2 つのフィルタを添付します。`SkewCorrectionFilter` は画像を水平に戻し、`DenoiseFilter` はピクセルレベルのノイズを平滑化します。  
- **Step 3** はオプションですが便利です。エンジンが補正しようとする最大角度を上限設定し、すでに水平なページでの過剰回転を防ぎます。  
- **Step 4** で **load image OCR** データを読み込みます。`YOUR_DIRECTORY/skewed_noisy.jpg` をテストファイルのパスに置き換えてください。  
- **Step 5** で実際に OCR を実行し、`OcrResult` を取得します。  
- **Step 6** でコンソールに **display OCR text** を出力し、即座にフィードバックを得られます。

> **Pro tip:** 出力に文字化けが残る場合は、`MaxAngle` を上げるか、デノイズ前に `ContrastFilter` を追加してみてください。

---

## recognize text image – Loading Your Files Correctly

よくある落とし穴は、**load image ocr** を誤った形式や DPI で読み込んでしまうことです。Aspose.OCR は PNG、JPEG、TIFF、BMP、さらには PDF ベースの画像もサポートします。ただし、印刷文書の場合は 300 DPI 以上がベストです。

```csharp
// Example: loading a high‑resolution PNG
string imagePath = @"C:\Images\invoice_300dpi.png";
OcrImage highRes = OcrImage.FromFile(imagePath);
```

マルチページ TIFF を扱う場合は、各フレームをループで処理できます：

```csharp
var tiff = Aspose.OCR.ImageProcessing.TiffImage.FromFile(@"multi_page.tif");
foreach (var frame in tiff.Frames)
{
    OcrResult pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

**なぜこれが improve OCR accuracy に関係するのか？** 高解像度は文字の形状を保持し、認識エンジンにより多くのデータポイントを提供します。低 DPI の画像は文字が合体したり欠けたりしやすく、エンジンが誤認識しやすくなります。

---

## improve OCR accuracy – Tweaking Filter Parameters

デフォルトのフィルタ設定は良い出発点ですが、パラメータを調整すればさらに性能を引き出せます。

| フィルター | キー プロパティ | 典型的な値 | 調整するタイミング |
|------------|----------------|------------|-------------------|
| `SkewCorrectionFilter` | `MaxAngle` | `15`（度） | 大きく傾いた画像（最大 30°） |
| `DenoiseFilter` | `Strength` | `0.5`（0‑1） | ノイズが非常に多いスキャン；`0.8` に上げる |
| `ContrastFilter` (optional) | `Level` | `1.2` | コントラストが低いスクリーンショット |

両方をカスタマイズする例：

```csharp
var skew = new SkewCorrectionFilter { MaxAngle = 25 };
var denoise = new DenoiseFilter { Strength = 0.8 };
ocrEngine.Settings.PreprocessingFilters.Clear(); // start fresh
ocrEngine.Settings.PreprocessingFilters.Add(skew);
ocrEngine.Settings.PreprocessingFilters.Add(denoise);
```

**エッジケース:** 画像に手書きメモと印刷文字が混在している場合は、デノイズ前に `BinarizationFilter` を追加して前景と背景を分離すると効果的です。

---

## display OCR text – Formatting the Output

デモではシンプルなコンソール出力で十分ですが、実運用では文字列の整形や改行、さらには JSON 形式が求められることがあります。

```csharp
// Remove extra whitespace and line breaks
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(ocrResult.Text, @"\s+", " ")
    .Trim();

Console.WriteLine("📝 Recognized Text:");
Console.WriteLine(cleaned);
```

API のレスポンスとして JSON が必要な場合：

```csharp
var payload = new {
    source = imagePath,
    text = cleaned,
    confidence = ocrResult.Confidence // overall confidence score
};
string json = System.Text.Json.JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```

これで **display OCR text** を、下流サービスが利用できる形式に整形できました。

---

## Full Working Example – Put It All Together

以下は新しいコンソールプロジェクトにコピペできる、最終的な自己完結型プログラムです。オプションフィルタ、高解像度画像の読み込み、クリーンな出力をすべて含んでいます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Text.Json;
using System.Text.RegularExpressions;

class PreprocessDemo
{
    static void Main()
    {
        // ---------- 1️⃣ Initialize OCR engine ----------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------- 2️⃣ Configure preprocessing ----------
        // Skew correction (up to 25°) + strong denoise
        var skew = new SkewCorrectionFilter { MaxAngle = 25 };
        var denoise = new DenoiseFilter { Strength = 0.8 };
        ocrEngine.Settings.PreprocessingFilters.Add(skew);
        ocrEngine.Settings.PreprocessingFilters.Add(denoise);

        // Optional: increase contrast for low‑visibility scans
        // ocrEngine.Settings.PreprocessingFilters.Add(new ContrastFilter { Level = 1.3 });

        // ---------- 3️⃣ Load the image ----------
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // ---------- 4️⃣ Run OCR ----------
        OcrResult result = ocrEngine.Recognize(inputImage);

        // ---------- 5️⃣ Clean & display ----------
        string cleaned = Regex.Replace(result.Text, @"\s+", " ").Trim();
        Console.WriteLine("✅ Corrected text:");
        Console.WriteLine(cleaned);

        // ---------- 6️⃣ JSON payload (if needed) ----------
        var payload = new {
            source = imagePath,
            text = cleaned,
            confidence = result.Confidence
        };
        string json = JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
        Console.WriteLine("\n📦 JSON output:");
        Console.WriteLine(json);
    }
}
```

**期待されるコンソール出力（例）：**

```
✅ Corrected text:
Invoice #12345 Date: 01/15/2026 Total: $1,250.00

📦 JSON output:
{
  "source": "YOUR_DIRECTORY/skewed_noisy.jpg",
  "text": "Invoice #12345 Date: 01/15/2026 Total: $1,250.00",
  "confidence": 0.97
}
```

別のファイルで実行すれば、テキストと信頼度はそれに応じて変化します。

---

## Common Questions & Answers

**Q: 画像がすでに水平な場合はどうすればいいですか？**  
A: 傾きフィルタはほぼゼロ角度を検出すると実質的に何もしないので、無効にする必要はありません。

**Q: Aspose.OCR は英語以外の言語もサポートしていますか？**  
A: はい。`ocrEngine.Settings.Language = OcrLanguage.Spanish;`（またはサポートされている任意の言語）を `Recognize` 呼び出し前に設定すれば利用できます。

**Q: マルチページ PDF はどう扱いますか？**  
A: 各ページを画像に変換します（Aspose.PDF が可能）し、同じ `OcrEngine` インスタンスに 1 ページずつ渡します。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}