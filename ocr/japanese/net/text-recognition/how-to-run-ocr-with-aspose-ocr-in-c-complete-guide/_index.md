---
category: general
date: 2026-02-28
description: Aspose OCR を使用して C# で OCR を実行する方法 – 画像からテキストを抽出し、画像を JSON または XML に変換する方法を数ステップで学びましょう。
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: ja
og_description: Aspose OCR を使用した C# での OCR 実行方法 – 画像からテキストを抽出し、画像を JSON または XML に変換する方法を、すぐに実行できるサンプルでご紹介します。
og_title: C#でAspose OCRを使ってOCRを実行する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でAspose OCRを使ってOCRを実行する方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使用して OCR を実行する方法 – 完全ガイド

レシート画像から **OCR を実行** したいとお考えですか？このチュートリアルでは **画像からテキストを抽出** し、さらに Aspose OCR を使って **画像を JSON に変換** または **画像を XML に変換** する方法を、単一の自己完結型プログラムで解説します。

例えば、経費管理アプリを作成していて、撮影したレシートから項目を取得したいとします。手動で入力するのは面倒ですよね？本ガイドの最後まで読むと、任意の画像を読み取り、構造化テキストを返し、JSON と XML の両方の表現を取得できる再利用可能なコードスニペットが手に入ります。

## 前提条件

始める前に以下を用意してください。

- .NET 6.0 SDK 以降（コードは .NET Framework 4.8 でも動作します）
- Visual Studio 2022（またはお好みのエディタ）
- 有効な **Aspose.OCR** NuGet パッケージ (`Install-Package Aspose.OCR`)
- 参照できるフォルダーに配置したサンプル画像（例: `receipt.png`）

追加の設定は不要です。ライブラリには必要な OCR モデルがすべて同梱されています。

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *Alt text: Receipt image for OCR processing – how to run OCR*

## 手順別実装

以下では解決策を論理的なチャンクに分けて説明します。各ステップでは **なぜ** それを行うのか、そして **何を** 行うのかを解説します。

### 1️⃣ OCR エンジンの初期化 – **how to run OCR** の基盤

`OcrEngine` クラスがエントリーポイントです。インスタンス化すると内部の言語モデルがロードされ、認識の準備が整います。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **プロのコツ:** 同じ `OcrEngine` を複数画像で再利用するとメモリの消費が抑えられ、バッチ処理が高速化します。

### 2️⃣ 画像の読み込み – **extract text from image** のコア

Aspose OCR は独自の `Image` ラッパーを使用します。`using` 文で囲むことでファイルハンドルが速やかに解放されます。

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

画像が BMP、TIFF、PDF など別の形式でも、同じ `Load` メソッドで対応可能です。追加の変換は不要です。

### 3️⃣ OCR 認識の実行 – **how to run OCR** の中心

`Recognize` を呼び出すと、レイアウト解析、文字分割、言語別分類といった重い処理が実行されます。

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

返される `OcrResult` には生テキスト、信頼度スコア、詳細なレイアウトツリーが含まれ、シリアライズ可能です。

### 4️⃣ 画像を JSON に変換 – **convert image to json** のシンプルな方法

JSON は Web API や NoSQL ストアに最適です。`ToJson` メソッドは整形された文字列を返すので、デバッグが楽になります。

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

典型的な JSON 出力例（省略表示）:

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

この JSON をそのまま REST エンドポイントに送信したり、Azure Cosmos DB に保存したりできます。

### 5️⃣ 画像を XML に変換 – **convert image to xml** が必要なとき

レガシーシステムの中には XML を要求するものがあります。Aspose はスキーマ互換なクリーンな XML を生成する `ToXml` を提供しています。

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

サンプル XML スニペット:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

両形式とも同じ階層データを保持しているので、パイプラインに合う方を選択してください。

## よくある落とし穴とテキスト抽出を安定させるコツ

堅牢なライブラリでも、実際の画像は様々な問題を投げかけます。ここでは遭遇しやすい 3 つの課題と対策を紹介します。

### 📏 低解像度画像

**影響:** 小さなフォントが結合され、信頼度が低下します。  
**対策:** 画像を前処理し、`Image.Resize` で拡大するか、シャープフィルタを適用してから `Recognize` に渡します。

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 コントラスト不足

**影響:** 暗い背景に薄い文字があると、文字分割アルゴリズムが混乱します。  
**対策:** `Image.AdjustBrightnessContrast` で色を反転したり、明暗・コントラストを調整します。

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 多言語文書

**影響:** デフォルトは英語モデルなので、混在言語は文字化けしやすいです。  
**対策:** 認識前に `ocrEngine.Language = OcrLanguage.Multilingual;` を設定します。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

これらのケースに対応すれば、**any image からテキストを抽出** する手順が信頼できるものになります。

## 完全動作サンプル（コピー＆ペースト可能）

以下はコンパイルしてすぐに実行できる完全プログラムです。`YOUR_DIRECTORY` を画像のパスに置き換えて F5 を押すだけです。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**期待されるコンソール出力**（可読性のため整形）には、抽出されたテキストとバウンディングボックスを含む JSON と XML の構造が表示されます。

## まとめ – 本稿で学んだこと

- Aspose OCR を使った **how to run OCR**（C#）  
- **extract text from image** のステップバイステップ手順  
- 2 つのシリアライズ方法：**convert image to json** と **convert image to xml**  
- 低解像度、低コントラスト、多言語シナリオへの対処法  
- 任意の .NET プロジェクトに貼り付けられる完成コードサンプル  

## 次のステップは？

テキスト抽出と構造化データ取得ができたら、以下のような活用を検討してください。

- JSON を Azure Function に渡し、レシートを Cosmos DB に保存する。  
- XML 出力を既存の SOAP ベース会計システムに取り込む。  
- Aspose OCR と機械学習モデルを組み合わせて、費用項目を自動分類する。

`receipt.png` を請求書、名刺、手書きメモなどに差し替えて実験してみましょう。同じパターンがあらゆる画像で機能します。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}