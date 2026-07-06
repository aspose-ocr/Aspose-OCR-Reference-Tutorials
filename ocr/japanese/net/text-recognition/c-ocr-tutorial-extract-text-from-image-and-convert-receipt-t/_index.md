---
category: general
date: 2026-02-14
description: C# OCRチュートリアル：画像からテキストを抽出し、信頼度スコアを含め、Aspose OCRを使用して領収書をJSONに変換する方法を学びます。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- how to include confidence
- convert receipt to json
- Aspose OCR C#
language: ja
og_description: c# OCRチュートリアル：画像からテキストを抽出し、信頼度スコアを含め、領収書をAspose OCRでJSONに変換するステップバイステップガイド。
og_title: C# OCRチュートリアル – 画像からテキストを抽出し、領収書をJSONに変換
tags:
- OCR
- C#
- Aspose
title: C# OCRチュートリアル – 画像からテキストを抽出し、領収書をJSONに変換
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-convert-receipt-t/
---

answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – レシート画像を構造化 JSON に変換

C#で低レベルのピクセル計算に苦労せずに **画像からテキストを抽出** する方法を考えたことはありませんか？もしかしたら、簿記アプリを作っていてスキャンしたレシートから項目を取得する必要があるかもしれません。良いニュースは、車輪の再発明をする必要はなく、Aspose OCR が重い作業を代わりにやってくれるということです。

この **c# OCR チュートリアル** では、レシート画像の読み込み、エンジンに **信頼度を含める** 設定、そして最終的に **レシートを JSON に変換** して、下流のロジックが通常のオブジェクトのように扱えるようにする手順をすべて解説します。最後まで実行すれば、整然とした JSON 文字列を出力するコンソールプログラムがすぐに動作します。

## 必要なもの

- **.NET 6.0** 以上 (コードは .NET Framework でも動作しますが、最新の SDK は暗黙的 using を提供します)。  
- 有効な **Aspose.OCR** NuGet パッケージ (`dotnet add package Aspose.OCR`)。  
- レシート画像 (JPEG、PNG、BMP など、ライブラリがサポートする形式)。  
- 好きな IDE (Visual Studio、Rider、または VS Code)。  

以上です。追加のネイティブライブラリや OCR の学習データは不要で、特別な設定もありません。さあ、始めましょう。

## c# OCR チュートリアル: ステップバイステップ実装

以下は完全に実行可能なプログラムです。新しいコンソールプロジェクトにコピー＆ペーストして **F5** を押すだけで動作します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Create the OCR engine.
            // The Engine class is the entry point; it holds all the settings.
            var ocrEngine = new Engine();

            // Step 2 – Load the receipt image from disk.
            // ImageStream.FromFile reads the file into a format the engine understands.
            var receiptImage = ImageStream.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

            // Step 3 – Tell the engine what we want in the JSON output.
            // IncludeBoundingBoxes gives us the location of each word,
            // IncludeConfidence adds a confidence score (0‑100),
            // IncludeWords makes the JSON human‑readable.
            var jsonOutputOptions = new JsonOutputOptions
            {
                IncludeBoundingBoxes = true,
                IncludeConfidence = true,
                IncludeWords = true
            };

            // Step 4 – Run OCR and receive a JSON string.
            // RecognizeToJson does the recognition and serialises the result.
            string jsonResult = ocrEngine.RecognizeToJson(receiptImage, jsonOutputOptions);

            // Step 5 – Show the JSON result on the console.
            // In a real app you might write this to a file or a database.
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **Pro tip:** `YOUR_DIRECTORY/receipt.jpg` をテスト用レシートの絶対パスに置き換えてください。相対パスを使用する場合は、コンソールアプリの作業ディレクトリが画像を含むフォルダーを指していることを確認してください。

### 各ステップの重要性

| ステップ | 目的 | どのように役立つか |
|------|---------|------------------|
| **OCR エンジンの作成** | コア処理オブジェクトをインスタンス化します。 | 必要に応じて言語、DPI、またはカスタム辞書を後から調整できます。 |
| **レシート画像の読み込み** | ファイルを Aspose が読み取れる `ImageStream` に変換します。 | エンジンが解析したい正確なピクセルを確実に取得します。 |
| **JSON 出力オプションの定義** | 結果の形状を設定します。 | `IncludeConfidence` は下流の検証に重要で、信頼度の低い単語を除外できます。 |
| **JSON への認識** | OCR を実行し、データを一度にシリアライズします。 | 手動パーサーを書く手間が省け、クリーンで構造化された文字列が得られます。 |
| **JSON の表示** | すべてが正常に動作したかをすぐに視覚的に確認できます。 | データ統合前にフォーマットの問題を早期に発見できます。 |

## OCR 結果に信頼度スコアを含める方法

OCR を試したことがあるなら、常に完璧ではないことをご存知でしょう。**信頼度を含める方法** は一般的な質問で、開発者は単語を信頼するかユーザーに確認させるかを判断する必要があります。

上記コードの以下の行は、まさにそれを実現します。結果の JSON には、認識された各単語に対して `confidence` フィールドが含まれ、通常 `0`（信頼度なし）から `100`（完全一致）までの範囲です。出力例の抜粋は次の通りです：

```json
{
  "pages": [
    {
      "words": [
        {
          "text": "Total",
          "boundingBox": { "x": 45, "y": 320, "width": 50, "height": 20 },
          "confidence": 98
        },
        {
          "text": "$12.34",
          "boundingBox": { "x": 110, "y": 320, "width": 60, "height": 20 },
          "confidence": 95
        }
      ]
    }
  ]
}
```

これで次のようなロジックを書けます：

```csharp
if (word.confidence < 80) { /* flag for manual review */ }
```

このシンプルなチェックにより、下流の会計ワークフローの信頼性が大幅に向上します。

## Aspose OCR を使用した画像からのテキスト抽出 – クイックテスト

JSON パイプライン全体を組む前に、プレーンテキスト抽出が機能するか確認すると便利です。一時的に `IncludeWords = true` に設定し、他のフラグをオフにできます：

```csharp
var jsonOutputOptions = new JsonOutputOptions
{
    IncludeBoundingBoxes = false,
    IncludeConfidence = false,
    IncludeWords = true
};
```

プログラムを実行すると、`text` フィールドだけを含むコンパクトな JSON が出力されます。例：

```json
{
  "pages": [
    {
      "words": [
        { "text": "Item" },
        { "text": "Qty" },
        { "text": "Price" }
        // …
      ]
    }
  ]
}
```

期待通りの単語が表示されれば、OCR エンジンがレシート画像を正しく読み取れることが分かります。その後、信頼度とバウンディングボックスのオプションを再度有効にして、よりリッチな出力を得られます。

## レシートを JSON に変換 – 構造の意味

**レシートを JSON に変換** ステップは、テキストを文字列化するだけではありません。Aspose OCR が生成する JSON は階層モデルに従います：

- **pages** – 配列（ほとんどのレシートは単一ページですが、形式はマルチページ PDF も扱えます）。
- **words** – 各単語オブジェクトは以下を保持します：
  - `text` – 認識された文字列。
  - `boundingBox` – 元画像上で単語をハイライトするための座標。
  - `confidence` – 前述したスコア。

なぜこれが有用なのでしょうか？スキャンしたレシートと抽出データを並べて表示する UI を構築していると想像してください。`boundingBox` の値で矩形を描画し、`confidence` に基づいて色分けすれば、エンジンが不確かだった部分をユーザーに視覚的に示すことができます。

フラットな構造（例: 行項目のリストだけ）が必要な場合は、LINQ で JSON を後処理できます：

```csharp
var receipt = JsonSerializer.Deserialize<ReceiptRoot>(jsonResult);
var lineItems = receipt.Pages
    .SelectMany(p => p.Words)
    .Where(w => w.Confidence > 80) // filter low‑confidence words
    .Select(w => w.Text)
    .ToList();
```

## 完全動作例 – すべてのパーツを統合

以下は **全体** のソースファイルで、コンパイル可能です。JSON 構造を反映した小さなヘルパークラスが含まれており、デシリアライズが簡単になります。

```csharp
using System;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    // Helper POCOs matching the JSON schema
    public class ReceiptRoot
    {
        public Page[] Pages { get; set; }
    }

    public class Page
    {
        public Word[] Words { get; set; }
    }

    public class Word
    {
        public string Text { get; set; }
        public BoundingBox BoundingBox { get; set; }
        public int Confidence { get; set; }
    }

    public class BoundingBox
    {
        public int X { get; set; }
        public int Y { get; set; }
        public int Width { get; set; }
        public int Height { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var engine = new Engine();

            // 2️⃣ Load receipt image (adjust the path!)
            var image = ImageStream.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

            // 3️⃣ Configure JSON output – we want everything.
            var options = new JsonOutputOptions
            {
                IncludeBoundingBoxes = true,
                IncludeConfidence = true,
                IncludeWords = true
            };

            // 4️⃣ Perform OCR and get JSON string
            string json = engine.RecognizeToJson(image, options);

            // 5️⃣ Show raw JSON (great for debugging)
            Console.WriteLine("--- Raw JSON Output ---");
            Console.WriteLine(json);

            // 6️⃣ Optional: deserialize to C# objects for further processing
            var receipt = JsonSerializer.Deserialize<ReceiptRoot>(json);
            Console.WriteLine("\n--- High‑confidence words (>90) ---");
            foreach (var word in receipt.Pages[0].Words)
            {
                if (word.Confidence > 90)
                    Console.WriteLine($"{word.Text} (confidence: {word.Confidence}%)");
            }
        }
    }
}
```

**期待されるコンソール出力**（簡略化）:

```
--- Raw JSON Output ---
{
  "pages":[
    {
      "words":[
        {"text":"Subtotal","boundingBox":{"x":30,"y":250,"width":80,"height":20},"confidence":97},
        {"text":"$45.00","boundingBox":{"x":120,"y":250,"width":50,"height":20},"confidence":95},
        ...
      ]
    }
  ]
}

--- High‑confidence words (>90) ---
Subtotal (
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}