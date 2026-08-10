---
category: general
date: 2026-02-11
description: C#で画像の傾きを補正し、テキスト抽出前にノイズを除去する方法。ファイルから画像を読み込み、数分でOCR用に画像を前処理する方法を学びましょう。
draft: false
keywords:
- how to deskew image
- remove noise from image
- extract text from image
- preprocess image for ocr
- load image from file
language: ja
og_description: C#で画像の傾きを補正し、テキスト抽出前にノイズを除去する方法。OCRのために画像を前処理するステップバイステップガイドをご覧ください。
og_title: C#で画像の傾き補正を行う方法 – 完全OCR前処理ガイド
tags:
- C#
- OCR
- Image Processing
title: C#で画像の傾き補正を行う方法 – 完全OCR前処理ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-in-c-full-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像の傾きを補正する方法 – 完全 OCR 前処理ガイド

揺れるカメラで撮影したかのように見える画像の**傾き補正**方法を考えたことはありませんか？歪んだスキャンを OCR エンジンに渡して、文字化けした出力が得られたことがあるかもしれません。これは特に、画像が傾いていて*かつ*ノイズが多い場合に頻繁に起こる問題です。

このチュートリアルでは、ファイルから画像を読み込み、傾きを直し、斑点を除去し、最後に Aspose.OCR を使って画像からテキストを抽出する手順を順に解説します。最後まで実行すれば、重い処理をすべて行ってくれる C# コンソールアプリがすぐに動作します。謎はなく、明快なコードと各ステップの意味が分かります。

---

## 必要なもの

- **.NET 6+**（または最近の .NET ランタイム）  
- **Aspose.OCR for .NET** NuGet パッケージ（無料トライアルはデモに使用可能）  
- 傾いていてノイズの多いサンプル画像（例: `skewed_noisy.jpg`）  
- Visual Studio、VS Code、またはお好みの IDE  

以上です。すでに .NET プロジェクトがある場合は、Aspose.OCR パッケージを追加するだけです：

```bash
dotnet add package Aspose.OCR
```

---

![画像の傾き補正例](/images/deskew-example.png "画像の傾き補正")

*Alt text: 画像の傾き補正 – 前後の処理比較*

---

## ステップ 1 – ファイルから画像を読み込む

マジックをかける前に、画像をメモリに読み込む必要があります。`System.Drawing.Image.FromFile` はシンプルですが、`Image` オブジェクトを破棄するまでファイルがロックされたままになるため、`using` ブロックでラップします。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source file – this satisfies the “load image from file” requirement.
using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
{
    // The rest of the pipeline will go here.
}
```

> **プロのコツ:** テスト中は絶対パスを使用し、実運用では相対パスまたは設定項目に切り替えてください。

---

## ステップ 2 – OCR エンジンの初期化（自動リソースダウンロードの有効化）

Aspose.OCR は実行時に言語データを取得できます。`AutomaticResourceDownload` を有効にすれば、言語パックを手動でコピーする手間が省けます。

```csharp
// Step 2: Set up the OCR engine.
OcrEngine ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true,
    Language = OcrLanguage.English // you can change this to French, Spanish, etc.
};
```

言語を明示的に設定するのはなぜ？ エンジンは言語固有の辞書を利用して精度を向上させます。特に句読点や特殊文字が含まれる画像では効果的です。

---

## ステップ 3 – 画像の傾き補正（How to Deskew Image）

傾いたスキャンは文字がベースラインに揃わないため、ほとんどの OCR アルゴリズムを混乱させます。`OcrPreprocessor.Deskew` はテキスト行を解析し、角度を算出してビットマップを水平に回転させます。

```csharp
// Step 3: Correct orientation – this is the core “how to deskew image” operation.
Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);
```

> **画像がすでに真っ直ぐだったら？** メソッドはほぼゼロの角度を検出するとコピーを返すので、無条件に呼び出しても安全です。

---

## ステップ 4 – 画像からノイズを除去する

古い文書のスキャンには斑点、圧縮アーティファクト、薄い背景パターンが含まれることが多いです。これらの小さな点が OCR エンジンの文字認識を誤らせます。`OcrPreprocessor.Denoise` はエッジを保持しつつ孤立したピクセルを除去するメディアンフィルタを適用します。

```csharp
// Step 4: Clean up the deskewed picture – this fulfills “remove noise from image”.
Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);
```

さらに aggressive なクリーニングが必要な場合は、`GaussianBlur` や `ContrastAdjustment` といった追加フィルタが Aspose で利用可能です。ほとんどのシナリオではデフォルトのデノイズで十分です。

---

## ステップ 5 – OCR を実行し画像からテキストを抽出する

画像が真っ直ぐで静かになったら、OCR エンジンに渡します。`Recognize` メソッドはプレーンテキスト、信頼度スコア、必要に応じてバウンディングボックスを含む `OcrResult` オブジェクトを返します。

```csharp
// Step 5: Run OCR – this is where we “extract text from image”.
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

中間画像を破棄しなければならないか気になるかもしれません。**必ず** 各画像を個別の `using` ブロックでラップするか、手動で `Dispose()` を呼び出してください。この簡潔な例では `sourceImage` の外側 `using` に任せ、残りは GC に任せていますが、本番コードでは明示的に破棄する習慣が推奨されます。

---

## ステップ 6 – 認識結果のテキストを表示する

最後にコンソールへ結果を出力します。実際のアプリではファイルやデータベースに書き込んだり、下流の NLP パイプラインに渡したりできます。

```csharp
// Step 6: Output the recognized text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**期待される出力**（サンプル画像に “Hello World” が含まれていると仮定）：

```
=== OCR Output ===
Hello World
```

テキストが文字化けしている場合は、前のステップを見直してください。ノイズ除去を強めるか、言語設定を変える必要があるかもしれません。

---

## 完全動作サンプル

すべてをまとめた、すぐに実行できるプログラムは以下の通りです：

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with automatic resource download.
        OcrEngine ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // Load the source image from file.
        using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
        {
            // Deskew – core “how to deskew image” step.
            Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);

            // Denoise – fulfills “remove noise from image”.
            Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);

            // Perform OCR – “extract text from image”.
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Show the result.
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

ファイル名を `Program.cs` として保存し、`dotnet run` を実行すれば OCR の出力が表示されます。シンプルですよね？

---

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| **画像が PDF ページの場合はどうすればよいですか？** | まず PDF を画像に変換します（例: `Aspose.PDF` を使用）。そのビットマップを同じパイプラインに渡します。 |
| **ループで複数ページを処理できますか？** | もちろん可能です。全体のブロックを `foreach (var path in imagePaths)` ループで囲み、結果をリストに収集してください。 |
| **大量バッチのパフォーマンスはどうですか？** | `OcrEngine` インスタンスを1つだけ再利用します。言語データがキャッシュされ、初期化時間が大幅に短縮されます。 |
| **テキストにラテン文字以外が含まれています – それでも動作しますか？** | `ocrEngine.Language` を適切な `OcrLanguage` 列挙値（例: `OcrLanguage.ChineseSimplified`）に設定してください。 |
| **出力にまだ余計な文字が残ります – 何かコツはありますか？** | デノイズ強度を上げてみてください（`OcrPreprocessor.Denoise(sourceImage, strength: 2)`）または二値化フィルタ（`OcrPreprocessor.Binarize`）を適用します。 |

---

## 次のステップ

**画像の傾き補正** と **画像からノイズ除去** をマスターした今、以下のことに挑戦できます：

- **バッチ処理** – フォルダー内のスキャン文書を読み込み、結合テキストファイルとして出力。  
- **バウンディングボックス抽出** – `ocrResult.Regions` を使って各単語の位置を取得。PDF の赤字処理に便利です。  
- **言語検出** – Aspose.OCR と言語判別ライブラリを組み合わせ、実行時に `ocrEngine.Language` を自動切替。

これらはすべて、**OCR 用画像前処理** の基盤の上に直接構築できます。

---

## TL;DR

C# で **画像の傾き補正**、**画像からノイズ除去**、**ファイルから画像を読み込む**、そして最終的に **画像からテキストを抽出** する完全なソリューションを紹介しました。コードは自己完結型でコメント付き、各操作の「なぜ」を解説しているため、SEO にもフレンドリーで AI アシスタントの引用にも適しています。

ぜひ試してみて、フィルタを調整しながら OCR エンジンに重い処理を任せてください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}