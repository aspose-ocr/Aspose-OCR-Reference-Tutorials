---
category: general
date: 2026-01-13
description: C#で画像の傾きを補正し、ノイズを除去する方法 – 画像のコントラストを上げ、OCRの前処理を行い、複数の画像フィルタを適用する方法を学ぶ。
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: ja
og_description: C#で画像の傾きを補正しノイズを除去する方法 – 画像のコントラストを上げ、OCRの前処理を行い、複数の画像フィルタを適用する方法を学ぶ。
og_title: 画像の傾き補正方法 – OCR向け完全C#前処理ガイド
tags:
- OCR
- C#
- Image Processing
title: 画像の傾き補正方法 – OCRのための完全なC#前処理ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 – OCR のための完全な C# 前処理ガイド

OCR エンジンに渡す前に **画像の傾き補正方法** を考えたことはありますか？ あなただけではありません。実際のシナリオ—スキャンした契約書、領収書、古いコピー—では、テキストがわずかに傾いていたり、画像がざらざらしたり、コントラストが不均一だったりします。良いニュースは、数行の C# コードで傾きを直し、画像ノイズを除去し、コントラストを向上させ、OCR の土台をしっかり作れるということです。

このチュートリアルでは、**完全で実行可能なサンプル** を通して、画像の傾き補正、画像ノイズ除去、コントラスト向上、そして Aspose.OCR を使った OCR 実行の手順を詳しく解説します。最後まで読めば、**複数の画像フィルタ** を 1 つの流暢な呼び出しで適用できる再利用可能なパイプラインが手に入ります—推測は不要です。

## 必要なもの

- **.NET 6+**（または最近の .NET バージョン；API の挙動は同じです）
- **Aspose.OCR for .NET** NuGet パッケージ（`Aspose.OCR` と `Aspose.OCR.Filters`）
- 歪み・ノイズ・低コントラストがあるサンプルスキャン画像（例：`skewed_noisy.png`）
- お好みの IDE（Visual Studio、Rider、VS Code など）

プロジェクトがすでにある場合は、NuGet 参照を追加するだけです：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **プロのコツ:** Aspose はページ数制限付きの無料トライアルを提供しています—以下のコードを試すのに最適です。

## Step 1: OCR エンジン インスタンスの作成

最初に `OcrEngine` を起動します。これは後でテキストを読み取る「脳」と考えてください。特別なことはありませんが、以降のすべての処理の基盤となります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **重要ポイント:** エンジンを一度初期化して再利用すれば、画像ごとに言語データを読み込むオーバーヘッドを回避できます。

## Step 2: 生スキャン画像の読み込み

次にディスクから画像を取得します。`OcrImage.FromFile` メソッドはファイルを Aspose が操作できる形式に読み込みます。

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **エッジケース:** 画像が TIFF や BMP などの非標準形式の場合でも Aspose は処理できますが、整合性のために PNG に変換しておくと良いでしょう。

## Step 3: 前処理パイプラインの構築（Deskew → Denoise → Contrast）

ここで **画像の傾き補正方法** に加えて **画像ノイズ除去** と **画像コントラスト向上** を実現します。Aspose の流暢な API によりフィルタをチェーンでき、コードが文章のように読めます。

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### 各フィルタの役割

| Filter | Purpose | Typical Impact |
|--------|---------|----------------|
| **DeskewFilter** | テキスト行の角度を検出し、画像を水平に回転させます。 | OCR を混乱させる傾きを除去し、エラー率を 30‑50 % 程度低減します。 |
| **DenoiseFilter** | エッジを保持しつつランダムノイズを除去する平滑化アルゴリズムを適用します。 | スキャンした領収書や暗所撮影の写真の文字をクリアにします。 |
| **ContrastFilter** | ヒストグラムを伸張し、暗部はさらに暗く、明部はさらに明るくします。 | テキストと背景の区別を強化し、特に色あせた文書で有効です。 |

> **なぜチェーンするのか？** まず傾き補正を行うことで、デノイズ処理が正しい向きの画像に対して実行されます。最後にコントラストを上げることで、クリーンになったテキストが OCR エンジンにとって見やすくなります。

## Step 4: 前処理済み画像で OCR を実行

画像がまっすぐでクリーン、かつ高コントラストになったら OCR エンジンに渡します。ここでは英語の言語データを使用しますが、Aspose は 150 以上の言語に対応しています。

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

別の言語が必要な場合は、`OcrLanguage.English` を該当する列挙値（例：`OcrLanguage.Spanish`）に置き換えるだけです。

## Step 5: 認識結果の出力

最後にコンソールへ結果を表示します。実際のアプリケーションではファイルやデータベースに書き込んだり、下流の NLP パイプラインにテキストを渡したりすることもあります。

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 期待される出力

典型的な傾いた領収書に対してプログラムを実行すると、以下のような出力が得られます：

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

出力が文字化けしている場合は、元画像を再確認してください。過度のぼやけや極端な暗さは、追加の前処理（例：`SharpenFilter`）が必要になることがあります。

![画像の傾き補正例](images/deskewed_example.png "画像の傾き補正 – 前後の処理")

*上の画像は左側が元の傾いたスキャン、右側が補正・ノイズ除去・高コントラスト化された結果を示しています。*

## Additional Tips & Common Pitfalls

### 1. 傾き角度が極端な場合

文書が 30° 以上傾いていると `DeskewFilter` がうまく機能しないことがあります。その場合は手動で事前に回転させます：

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. カラー画像の取り扱い

フィルタは内部でグレースケールに変換して動作しますが、明示的に変換を強制できます：

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. デノイズ強度の調整

`DenoiseFilter` はオプションの `strength` パラメータ（0‑100）を受け取ります。数値が大きいほどノイズ除去が強くなりますが、細部がぼやける可能性があります。

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. 基本以外の複数フィルタ活用

Aspose には `SharpenFilter`、`BinarizeFilter`、`ResizeFilter` など多数のフィルタが用意されています。組み合わせて独自のパイプラインを作成し、対象文書に最適化できます。

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Full Working Example (Copy‑Paste Ready)

以下はコンソールプロジェクトにそのまま貼り付け可能な完全プログラムです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

`dotnet run` でプログラムを実行してください。設定が正しければ、コンソールに元の傾いたノイズ画像から抽出されたクリーンで読みやすいテキストが表示されます。

## Conclusion

本稿では C# で **画像の傾き補正方法** を実装しながら、**画像ノイズ除去**、**画像コントラスト向上**、そして **複数画像フィルタ** のチェーンによる OCR 前処理を網羅しました。重要なポイントは、順序立てた前処理パイプラインが OCR 精度を劇的に向上させ、ほとんど読めないスキャンを完全に判読可能なテキストへと変換できることです。

次のステップに進みませんか？ `ContrastFilter` を `BinarizeFilter` に置き換えて二値化が結果に与える影響を確認したり、`ResizeFilter` で高解像度画像をエンジンに供給したりしてみてください。どのフィルタを選んでも同じパターンが適用できるので、今後の OCR プロジェクト全般に柔軟に活用できる基盤が手に入ります。

PDF の取り扱い、マルチランゲージ OCR、ASP.NET API への統合などについて質問があれば、下のコメント欄にどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}