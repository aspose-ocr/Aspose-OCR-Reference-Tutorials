---
category: general
date: 2026-03-18
description: スキャンしたファイルの画像を傾き補正し、ノイズを除去する方法。ファイルから画像を読み込み、TIFF からテキストを抽出し、Aspose OCR
  で画像からテキストを認識する方法を学びます。
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: ja
og_description: Aspose OCR を使用して画像を素早くデスケューする方法。このガイドでは、ノイズの除去、ファイルからの画像読み込み、C# での
  TIFF からのテキスト抽出方法を示します。
og_title: 画像の傾き補正方法 – 完全なC# OCRチュートリアル
tags:
- OCR
- C#
- Image Processing
title: 画像の傾き補正とスキャンのクリーニング方法 – 完全C#ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像のデスキュー方法 – 完全な C# OCR チュートリアル

スキャナーが揺れて撮影したような **画像のデスキュー** 方法に興味がありますか？ あなたは一人ではありません。ソースの TIFF が少し歪んでいると、ほとんどの開発者がこの問題に直面し、OCR の結果がめちゃくちゃになります。朗報です！数行の C# コードで画像を真っ直ぐにし、ざらざらした背景を除去し、ファイルからクリーンで検索可能なテキストを直接抽出できます。

このガイドでは **ノイズの低減方法**、**ファイルから画像を読み込む方法**、そして最終的に **画像からテキストを認識する方法** を Aspose OCR を使って解説します。最後まで読めば、**TIFF からテキストを抽出** できるようになります。

> **プロのヒント:** すでに他のプロジェクトで Aspose OCR を使用している場合、追加のライセンス問題なくこのフィルタをそのまま組み込めます。

---

## 必要なもの

- .NET 6 以上（コードは .NET Core でも動作します）  
- Aspose.OCR NuGet パッケージ (`Install-Package Aspose.OCR`)  
- 少し回転またはノイズがあるスキャン済み TIFF（例として `skewed_scanned_doc.tif` を使用）  
- テキストエディタまたは IDE（Visual Studio、VS Code、Rider などお好みで）

追加のライブラリは不要です。使用するフィルタはすべて Aspose OCR に組み込まれています。

---

## Step 1 – OCR エンジンの作成（画像のデスキュー方法）

最初に `OcrEngine` を作成します。これは後で文字を読み取る「脳」のようなものです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

なぜ事前にエンジンを作成するのか？ 前処理フィルタ、言語パック、出力オプションを一箇所にまとめて設定できるからです。`OcrEngine.Recognize` を直接呼び出すと、画像を先にクリーンアップする機会を失い、デスキューができなくなります。

---

## Step 2 – デスキューとノイズ低減フィルタの追加（ノイズの低減方法）

次に 2 つのフィルタを添付します。

| フィルタ | 機能 | 重要な理由 |
|--------|------|------------|
| `AutoDeskewFilter` | 回転を検出し補正 | テキスト行をまっすぐにし、OCR エンジンが正しく読み取れるようにする |
| `NoiseReductionFilterV2` | 斑点や背景の粒子を除去 | ピクセルがクリーンになるほど誤認識が減少する |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

`NoiseReductionFilterV2` を古いバージョンに置き換えることも可能ですが、v2 アルゴリズムは最新のスキャナーに最適化されています。文書がすでに完全に平坦であれば、デスキューフィルタは画像をそのまま通過させるだけで、影響はありません。

---

## Step 3 – ファイルから画像を読み込む（Load Image from File）

Aspose には TIFF、JPEG、PNG、BMP など様々な形式を読み込める便利な `ImageStream.FromFile` ヘルパーがあります。以下のコードでファイルをメモリに取り込みます。

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

`YOUR_DIRECTORY` を実際のパスに置き換えてください。相対パスを使用する場合は、実行ファイルと同じディレクトリにファイルがあるか、作業ディレクトリを適切に設定してください。

---

## Step 4 – 前処理済み画像で OCR を実行（Recognize Text from Image）

フィルタを設定し画像を読み込んだら、いよいよ Aspose に文字認識を依頼します。

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

内部ではエンジンがデスキューアルゴリズムを実行し、ノイズを平滑化した後、ニューラルネットワークベースの認識器が走ります。結果は `OcrResult` オブジェクトにラップされ、テキスト本体、信頼度スコア、必要に応じてバウンディングボックスも取得できます。

---

## Step 5 – 抽出したテキストの表示または保存（Extract Text from TIFF）

デモとしてコンソールにテキストを出力しますが、ファイルやデータベースに書き込んだり、後続のワークフローに渡したりすることも可能です。

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力**（サンプル、実際の文書により異なります）:

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

出力に文字化けが残る場合は、元の TIFF が解像度不足（最低 300 dpi 推奨）でないか、`ocrEngine.Settings.Language` が正しく設定されているかを再確認してください。

---

## 完全動作サンプル（すべての手順を一つにまとめた例）

以下は新しいコンソールプロジェクトにコピペしてすぐに実行できる完全プログラムです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すれば、クリーンアップされたテキストが端末に表示されます。

---

## FAQ とエッジケース

### TIFF に複数ページがある場合は？
Aspose OCR は `image.GetPages()`（または `image.Pages`）でマルチページ画像をループ処理できます。各ページは個別の `OcrResult` を返すので、必要に応じて `StringBuilder` で結合してください。

### 大きく回転した画像でもデスキューフィルタは機能するか？
±15° 程度までの回転に対応しています。それ以上の場合は、`System.Drawing` や `SkiaSharp` などのグラフィックライブラリで事前に回転させてから Aspose に渡す必要があります。

### 非英語テキストの精度を上げるには？
言語を明示的に設定します:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

組み込みの言語パックに含まれない文字種がある場合は、カスタム言語パックをロードすることも可能です。

### Linux で実行できるか？
もちろんです。Aspose OCR はクロスプラットフォーム対応です。純粋な .NET バージョンでは通常追加のネイティブ依存関係は不要です。`dotnet publish -r linux-x64` で自己完結型バイナリを作成してください。

---

## ボーナス：デスキュー後の画像を可視化

OCR 前に補正後の画像を確認したい場合は、ディスクに保存できます。

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![how to deskew image example](https://example.com/deskew-demo.png "how to deskew image example")

*画像の代替テキスト:* **how to deskew image example** – AutoDeskewFilter によって回転した TIFF が補正された前後の比較を示しています。

---

## 結論

**画像のデスキュー方法**、**ノイズの低減方法**、そして **画像からテキストを認識**、**ファイルから画像を読み込む**、**TIFF からテキストを抽出** まで、Aspose OCR と C# を使った一連のパイプラインを網羅しました。要点は、2 つの前処理フィルタを追加するだけで、揺れた粒子の多いスキャンでも鮮明で検索可能な文書に変換できるということです。

次のステップに挑戦してみませんか？ 文書が逆さまの場合は `AutoDeskewFilter` を `AutoRotateFilter` に置き換えるか、薄く印刷されたものには `ContrastEnhancementFilter` を試してみてください。同じパターン（エンジン → フィルタ → 読み込み → 認識）はすべての Aspose OCR シナリオで有効なので、PDF、PNG、カメラ写真にもこの雛形を再利用できます。

Happy coding, and may your OCR be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}