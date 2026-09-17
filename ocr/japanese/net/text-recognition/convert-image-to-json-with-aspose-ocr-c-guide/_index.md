---
category: general
date: 2026-01-15
description: C#で Aspose OCR を使用して画像を JSON に変換します。画像からテキストを抽出し、JSON のバウンディングボックスを取得し、レシート画像を認識する方法を学びましょう。
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: ja
og_description: C#でAspose OCRを使用して画像をJSONに変換する。画像からテキストを抽出し、レシート画像を認識し、JSONのバウンディングボックスを取得するステップバイステップガイド。
og_title: Aspose OCR C# ガイドで画像をJSONに変換
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Aspose OCR C# ガイドで画像をJSONに変換する
url: /ja/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Image to JSON with Aspose OCR C# Guide

画像を **JSON に変換** したいと思ったことはありませんか？しかし、テキストの生データと正確な単語座標の両方を取得できるライブラリがどれか分からないことも多いでしょう。あなたは一人ではありません。多くの開発者が画像ファイル（特にレシート）からテキストを抽出しつつ、下流処理用の機械可読な JSON ペイロードが必要になる壁にぶつかります。

このチュートリアルでは、**Aspose OCR C# のサンプル** を通して、画像からテキストを抽出し、レシート画像を認識し、各単語の **JSON バウンディングボックス** を出力する方法を解説します。最後まで実行すれば、任意の API、データベース、または分析パイプラインに投入できる、整形された JSON 文字列をコンソールに出力する実行可能なコンソールアプリが手に入ります。

> **What you’ll walk away with**  
> • **画像を JSON に変換** する完全に機能する C# プロジェクト  
> • `IncludeBoundingBoxes` を有効にする理由（`json bounding boxes` の鍵）  
> • さまざまな画像形式や言語を扱う際のヒント  

さあ、始めましょう。

---

## What You’ll Need

コードに入る前に、以下の前提条件がインストールされていることを確認してください。

- **.NET 6.0 SDK**（またはそれ以降のバージョン） – コードは .NET 6 を対象としていますが、.NET Framework 4.7+ でも動作します。  
- **Aspose.OCR for .NET** NuGet パッケージ – `dotnet add package Aspose.OCR` で取得できます。  
- プロジェクトから参照できるフォルダーに配置したサンプルレシート画像（`receipt.jpg`）。  
- Visual Studio 2022、VS Code、またはお好みの IDE。

他に外部サービスは不要です。すべてローカルで実行できます。

---

## Convert Image to JSON – Overview

基本的な考え方はシンプルです。画像を読み込み、Aspose OCR に英語（またはサポートされている任意の言語）で認識させ、バウンディングボックスを含めるよう指示し、最終的に **JSON** 形式で結果を取得します。ライブラリが OCR、レイアウト解析、JSON シリアライズの重い処理をすべて担当します。

以下はフローのハイレベル図です（小さなイメージを想像してください）：

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

この小さな図が、実装する全パイプラインを表しています。

---

## Step 1: Set Up the Project and Install Aspose OCR

まず、新しいコンソールプロジェクトを作成し、Aspose OCR パッケージを追加します。

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio を使用している場合は、プロジェクトを右クリック → *Manage NuGet Packages* → **Aspose.OCR** を検索して最新の安定版（現在は 23.12）をインストールしてください。

---

## Step 2: Load the Image You Want to Recognize

`OcrImage.FromFile` メソッドを使ってレシート画像を読み込みます。パスが実際のファイルを指していることを確認しないと、`FileNotFoundException` が発生します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

画像が `.csproj` と同じフォルダーにある場合は、単に `"receipt.jpg"` を使用できます。

---

## Step 3: Configure OCR Options for JSON Bounding Boxes

`OutputFormat = OutputFormat.Json` **と** `IncludeBoundingBoxes = true` を有効にしたときに魔法が起きます。前者は Aspose に結果を JSON としてシリアライズさせ、後者は各単語に `x`, `y`, `width`, `height` を付加します――これが **json bounding boxes** に必要な情報です。

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

解像度を上げたい場合や別言語が必要な場合は、`ocrOptions.Dpi` や `ocrOptions.Language` を調整してください。

---

## Step 4: Perform the Recognition – Extract Text from Image

いよいよ `Recognize` を呼び出します。このメソッドは `OcrResult` オブジェクトを返し、JSON 文字列や生テキストなどが格納されています。

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

他言語を扱う場合は、`Language.English` を `Language.Spanish`、`Language.French` などに置き換えてください。Aspose は 30 以上の言語を標準でサポートしています。

---

## Step 5: Output the Result – Your JSON Payload

最後に、JSON をコンソールに出力します。実際のアプリではファイルに書き出したり、サービスへ送信したりすることが多いでしょう。

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

プログラムを実行すると、以下のような JSON ドキュメントが生成されます。

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

各単語に **JSON バウンディングボックス** が付与されていることに注目してください――UI のオーバーレイや下流パーサーへの入力に最適です。

---

## Full Working Example

以下がコピー＆ペーストでそのまま使える完全版プログラムです。隠し部分や外部呼び出しはなく、純粋な C# だけです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Watch out for:**  
> • **ファイルパスエラー** – 画像の場所を必ず確認してください。  
> • **NuGet パッケージの未取得** – `Aspose.OCR` が参照に含まれているか確認。  
> • **サポート外の画像形式** – ベストな結果を得るには JPEG、PNG、BMP、TIFF を使用してください。

---

## Common Questions & Edge Cases

### Can I convert a **PDF page** to JSON instead of a JPEG?

はい。まず PDF ページを画像に変換（例: `Aspose.PDF` を使用）し、その画像を同じ OCR パイプラインに渡します。JSON 出力は同一です。OCR ステップはラスターデータのみを扱うためです。

### What if the receipt is blurry?

`ocrOptions` の DPI を上げます。例:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

DPI を上げるとメモリ使用量が増えるので、品質とパフォーマンスのバランスを考慮してください。

### I need **multiple languages** on the same receipt (e.g., English + Spanish).

言語の配列を渡すことができます:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

指定した順序で Aspose が各言語の認識を試みます。

### How do I write the JSON to a file?

`Console.WriteLine` 行を次のように置き換えます:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

これで永続的なファイルが生成され、他のサービスへ送信できるようになります。

---

## Visual Summary

![convert image to json example](convert-image-to-json.png "convert image to json example")

*このスクリーンショットは、デモ実行後のコンソール出力として表示される JSON ペイロードを示しています。*

---

## Conclusion

ここまでで、Aspose OCR を使って **画像を JSON に変換** する方法を示しました。`OutputFormat` と `IncludeBoundingBoxes` を設定するだけで、**画像からテキストを抽出** し、**レシート画像を認識** し、各単語の正確な **JSON バウンディングボックス** を取得できます。完全に実行可能なコードは上記スニペットにあるので、すぐに任意の .NET プロジェクトに組み込めます。

次のステップは？取得した JSON をフロントエンドビューアに渡して単語をハイライトしたり、レシートの項目を分類する機械学習モデルに投入したりしてみてください。言語や DPI 設定の変更、複数画像のバッチ処理にも挑戦できます。

ファイルパス、DPI、言語配列に関する注意点を覚えておけば、ほとんどの障壁はクリアできます。コメントや GitHub リポジトリでの Issue で質問を受け付けていますので、ぜひフィードバックをお寄せください。コーディングを楽しみながら、画像を構造化された JSON に変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}