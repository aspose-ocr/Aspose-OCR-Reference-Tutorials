---
category: general
date: 2026-05-06
description: Aspose OCR を使用して画像の傾きを補正し、画像からテキストを抽出する方法を学びましょう – OCR の精度を向上させ、画像のノイズ除去を行うステップバイステップガイド。
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: ja
og_description: Aspose OCR を使用して画像の傾きを補正し、画像からテキストを抽出する方法を学びましょう。このチュートリアルでは、画像のノイズ除去と
  OCR 精度の向上方法を示します。
og_title: C#で画像の傾き補正を行う方法 – 完全OCRガイド
tags:
- OCR
- C#
- Image Processing
title: C#で画像の傾き補正を行う方法 – 完全OCRガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像の傾きを補正する方法 – 完全 OCR ガイド

OCR を実行する前に **画像の傾きを補正する方法** が必要だったことはありませんか？どのフィルタを適用すべきか分からないこともあるでしょう。あなたは一人ではありません—ソース写真が少し歪んでいたりノイズが多いと、多くの開発者が同じ問題に直面します。良いニュースは、C# と Aspose.OCR の数行のコードで、画像を真っ直ぐにし、クリーンにし、最終的にテキストを高精度で抽出できるということです。

このチュートリアルでは、必要なすべての手順を解説します：傾いた画像の読み込み、傾き補正とノイズ除去フィルタの適用、コントラストの強化、そして最終的にテキストを抽出します。最後まで読むと、**OCR の使い方** が理解でき、**OCR の精度を向上させる方法** が分かり、任意の .NET プロジェクトにすぐに組み込める実行可能なコードサンプルが手に入ります。

## 必要なもの

- .NET 6 以降（API は .NET Core と .NET Framework でも動作します）
- Aspose.OCR for .NET（無料トライアルまたはライセンス版）– NuGet で `Install-Package Aspose.OCR` を使用して取得できます
- 傾いていて少しノイズのあるサンプル画像（例：`skewed_noisy.jpg`）
- Visual Studio、VS Code、またはお好みのエディタ

追加のネイティブライブラリは不要です；Aspose がすべて内部で処理します。

## 手順 1: プロジェクトのセットアップと Aspose.OCR のインストール

### 新しいコンソール アプリを作成

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### Aspose.OCR パッケージを追加

```bash
dotnet add package Aspose.OCR
```

これで完了です—プロジェクトは OCR エンジンと必要な組み込みフィルタを参照するようになりました。

## 手順 2: 処理したい画像を読み込む

`OcrEngine` インスタンスを作成し、クリーンアップしたいファイルを指定することから始めます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **重要な理由:** 画像の読み込みは、以降のすべてのフィルタの最初のフックです。パスが間違っていると、パイプライン全体が黙って失敗してしまうので、場所を再確認してください。

## 手順 3: 処理パイプラインの構築 – 傾き補正、ノイズ除去、そしてコントラスト強化

ここが魔法の場所です。最高の OCR 結果を得るために、正確な順序で 3 つのフィルタを追加します：

1. **DeskewFilter** – 画像を真っ直ぐにします。
2. **MedianDenoiseFilter** – エッジをぼかさずにランダムな斑点を除去します。
3. **ContrastStretchFilter** – テキストと背景の差を強調します。

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **プロのコツ:** 順序は極めて重要です。まず傾き補正を行います。傾いた画像はノイズ除去フィルタを混乱させる可能性があります。画像が正立した後にメディアンフィルタで粒状ノイズを除去し、最後にコントラストストレッチで文字を際立たせます。

## 手順 4: OCR 認識を実行

ここで Aspose に重い処理を任せます。`Recognize` メソッドは抽出された文字列といくつかの信頼度指標を含む `OcrResult` オブジェクトを返します。

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **OCR の使い方:** `Recognize` 呼び出しは内部で追加したすべてのフィルタを適用し、OCR エンジンを実行します。各フィルタを手動で呼び出す必要はなく、パイプラインが自動で処理します。

## 手順 5: 認識結果のテキストを出力

最後に、テキストをコンソールに出力します。実際のアプリケーションでは、ファイルやデータベースに書き込んだり、別のサービスに渡したりすることが多いでしょう。

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 完全な実行可能サンプル

すべてをまとめると、`Program.cs` にコピー＆ペーストできる完全なプログラムは以下の通りです：

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

以下のコマンドで実行します：

```bash
dotnet run
```

実行すると、信頼度スコアと、元の写真に写っていたテキストのプレーンテキスト版が表示されます。

## 結果の検証 – 期待される出力

例えば、ソース画像に印刷された請求書の行が含まれている場合：

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

パイプライン実行後、コンソールには次のような出力が表示されます：

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

高い信頼度（通常は 90% 以上）は、**画像の傾きを補正する方法** と **画像のノイズを除去する方法** のステップが OCR エンジンに文字をはっきり認識させたことを示します。

## よくある質問とエッジケース

### 画像が 45 度以上回転している場合は？

`DeskewFilter` は ±45° までの角度を自動検出します。より大きな回転の場合は、傾き補正の前に `ocrEngine.Filters.Add(new RotateFilter(angle))` を使用して画像を事前に回転させてください。

### 信頼度が低い—他に何ができる？

- **BinarizationFilter** を追加して白黒変換を強制する。
- **MedianDenoiseFilter** の半径を増やす：`new MedianDenoiseFilter(3)`。
- 高解像度のソース画像を使用する（300 dpi 以上）。

### ループで複数の画像を処理できますか？

もちろん可能です。エンジンの作成をループの外に移動し、各ファイルに対して `SetImage` を呼び出し、同じフィルタコレクションを再利用してください。

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### PDF でも動作しますか？

Aspose.OCR は PDF ページを画像として読み取れますが、各ページをビットマップとして抽出するには Aspose.PDF ライブラリが必要です。

## OCR 精度を最大化するためのヒント

1. **不要な余白を切り取る** – 余分な空白は OCR エンジンを混乱させることがあります。
2. **均一な背景を使用する** – 真っ白または薄いグレーが最適です。
3. **極端な照明を避ける** – 影は偽のエッジを作り、ノイズ除去フィルタが完全に除去できないことがあります。
4. **実際のサンプルでテストする** – 合成データはきれいに見えますが、実運用の画像はしばしばアーティファクトを含みます。

## 結論

ここでは **画像の傾きを補正する方法**、**画像のノイズを除去する方法**、そして Aspose を使用した **OCR の使い方** の全体フローをカバーし、**画像からテキストを抽出する** と同時に **OCR の精度を向上させる** 方法を紹介しました。サンプルコードは完全で実行可能であり、バッチ処理、UI 統合、またはクラウドサービスへの適用がすぐに行えます。

次のステップは？`MedianDenoiseFilter` を `GaussianDenoiseFilter` に置き換えて信頼度スコアを比較したり、抽出したテキストを自然言語パーサに渡して自動的にフォームに入力させたりしてみてください。前処理パイプラインをマスターすれば、可能性は無限です。

コーディングを楽しんで、OCR の結果がクリアになることを願っています！

--- 

![how to deskew image example](/images/deskew-example.png "how to deskew image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}