---
category: general
date: 2025-12-29
description: Aspose OCR を使用して画像の傾き補正、背景除去、テキスト抽出を学びましょう。OCR 用に画像を前処理し、画像からテキストを認識するステップバイステップの
  C# コードです。
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: ja
og_description: 画像の傾きを補正し、OCR精度を向上させる方法。このガイドに従って背景を除去し、OCR用に画像を前処理し、Aspose を使用して画像からテキストを認識します。
og_title: 画像の傾き補正方法 – C# OCR 前処理チュートリアル
tags:
- Aspose OCR
- C#
- Image preprocessing
title: 画像の傾き補正方法 – OCR前処理の完全C#ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 – OCR 前処理の完全 C# ガイド

スキャナーから出力された画像が、まるで斜めのはがきのように見えることに **画像の傾き補正方法** で悩んだことはありませんか？ あなただけではありません。実務では、元画像が傾いていたり、ノイズが多かったり、背景がごちゃごちゃしていたりして、OCR がうまく機能しないことが頻繁にあります。

このチュートリアルでは、**画像の傾き補正方法** だけでなく、**背景除去方法**、**テキスト抽出方法**、そして最終的に **画像からテキストを認識する方法** を Aspose OCR for .NET を使って実装する実践的な解決策を順を追って解説します。最後まで読めば、画像を OCR 用に前処理し、クリーンで検索可能なテキストを取得できる C# プログラムが完成します。

## 必要な環境

- .NET 6 SDK 以上（コードは .NET Core と .NET Framework のどちらでも動作します）  
- Visual Studio 2022（またはお好みのエディタ）  
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）  
- 傾きがありノイズが入ったサンプル画像（例：`skewed_noisy.jpg`）  

以上だけです。追加のネイティブライブラリや面倒なコマンドラインツールは不要です。さっそく始めましょう。

## Step 1 – 入力画像の読み込み（画像の傾き補正はここから）

最初にやるべきことは、画像をメモリに読み込むことです。Aspose OCR の `Image.Load` メソッドはファイルパスを受け取り、操作可能な `Image` オブジェクトを返します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **ポイント:** 画像をロードすることで、傾き補正や背景除去といった後続のすべての変換を適用できるハンドルが手に入ります。

## Step 2 – 画像の傾き補正（実際の画像の傾き補正）

Aspose OCR には、傾き角度を自動検出し、設定可能な閾値まで補正する便利な `Deskew` フィルタが用意されています。ここでは **5°** まで許容しています。多くのスキャン文書はこの範囲に収まります。

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **プロのコツ:** 文書が 5° を超えて回転している場合は、`angleThreshold` を 10 や 15 に上げてください。角度が大きくてもアルゴリズムは高速です。

## Step 3 – 傾き補正後の画像のノイズ除去

ノイズは OCR 精度を下げる最大の要因です。シンプルなノイズ除去パスを通すことで、文字自体をぼやけさせずに斑点を除去できます。

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **内部処理:** このフィルタはエッジ（文字）を保持しつつ、孤立したピクセルを抑えるメディアンブラーを適用します。

## Step 4 – 背景除去（効果的な背景除去方法）

薄い背景やパターンがあると OCR エンジンが混乱します。Aspose OCR の `RemoveBackground` メソッドは前景テキストを分離します。

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **背景除去の理由:** テキストと背景のコントラストが上がることで、エンジンは文字をより確実に識別でき、**テキスト抽出方法** の結果が直接向上します。

## Step 5 – OCR エンジンの初期化

画像がまっすぐでクリーン、かつ高コントラストになったので、OCR エンジンをインスタンス化します。基本的なラテン文字の場合は追加設定は不要ですが、必要に応じて言語を切り替えられます。

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **備考:** Aspose OCR は 100 以上の言語をサポートしています。多言語対応が必要な場合は、認識前に `ocrEngine.Language = OcrLanguage.YourLanguage;` を設定してください。

## Step 6 – 画像からテキストを認識（テキスト抽出方法）

エンジンが準備できたら、前処理済み画像を渡します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、そこに生テキストと信頼度スコアが格納されます。

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **結果のポイント:** `ocrResult.Text` にプレーン文字列が、`ocrResult.Confidence`（取得すれば）に各行の信頼度が格納されています。

## Step 7 – 認識結果の出力

最後に、抽出したテキストをコンソールに表示するか、ファイルやデータベースに書き出すか、ワークフローに合わせて出力します。

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

これでプログラムは実行可能です。ビルドして実行すれば、元画像が傾いていてノイズが多くても、クリーンで読みやすいテキストが得られるはずです。

![画像の傾き補正例](/images/deskew-demo.png "Aspose OCR を使用した画像の傾き補正デモ")

*上のスクリーンショットは、傾き補正前後の画像を比較したもので、前処理パイプラインの効果を示しています。*

## エッジケースとよくある質問

### 画像が 5° 以上回転している場合は？
`Deskew` 呼び出し時の `angleThreshold` を増やしてください。検索ウィンドウが広がるだけで、アルゴリズムは正しい角度を自動検出します。

### 文書にカラー文字が含まれる場合、`RemoveBackground` で色が失われませんか？
`RemoveBackground` は輝度情報で動作するため、カラー文字はグレースケールに変換されてから処理されます。カラー情報を保持したまま後続処理したい場合は、このステップを省き、ノイズ除去だけを行ってください。

### マルチページ PDF はどう扱う？
各 PDF ページを画像に変換（例：Aspose.PDF を使用）し、同じパイプラインに通します。ページごとにループして `ocrResult.Text` を連結すれば完了です。

### 手書きノートの精度を上げるには？
`ocrEngine.Options.UseNeuralNetwork = true;`（新しい Aspose バージョンで利用可能）を有効にし、処理前に画像解像度を最低 300 dpi に上げると効果的です。

## 完全動作サンプル（コピペ用）

以下は、必要な `using` ディレクティブとコメントをすべて含んだソースコード全体です。新しいコンソールプロジェクトに貼り付けて **F5** キーで実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**期待される出力例**（シンプルな請求書の場合）:

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

出力が文字化けしている場合は、元画像が十分に鮮明か、設定した傾き閾値が画像の実際の傾きより小さくないかを確認してください。

## 結論

本稿では **画像の傾き補正方法** を段階的に解説し、**背景除去方法**、**テキスト抽出方法** を前処理で実現、そして Aspose OCR を用いて **画像からテキストを認識する方法** を示しました。全工程はコンパクトな C# プログラムに収められており、バッチ処理や PDF 変換、ドキュメント管理システムへの統合など、さまざまなシナリオに拡張可能です。

次のステップに挑戦してみませんか？ スキャンした PDF フォルダ全体をこのパイプラインに流し込んだり、ノイズ除去設定を変えて信頼度スコアへの影響を観察したりしてみましょう。パラメータをいろいろ試すほど、速度と精度のトレードオフが見えてきます。

質問や「この画像だけはうまくいかない」などのケースがあれば、下のコメント欄で教えてください。一緒にトラブルシュートしましょう。コーディングを楽しんで、OCR の結果が常にクリアになることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}