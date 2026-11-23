---
category: general
date: 2026-05-02
description: C# OCRチュートリアルで、画像からテキストを抽出し PNG のテキストを認識し、JsonSerializer を使用してインデントされた
  JSON を書き出す方法を示します。開発者向けのステップバイステップガイド。
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: ja
og_description: C# OCRチュートリアル：画像からテキストを抽出し、PNGテキストを認識し、JsonSerializerを使用してインデントされたJSONを書き出す方法を示します。完全な実行可能サンプルです。
og_title: C# OCRチュートリアル – テキスト抽出とインデント付きJSONへのエクスポート
tags:
- OCR
- C#
- Aspose
- JSON
title: C# OCRチュートリアル – 画像からテキストを抽出し、インデントされたJSONとしてエクスポート
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 画像からテキストを抽出し、インデントされた JSON としてエクスポート

テキストの画像からすぐにきれいに整形された JSON ファイルへ変換する **c# ocr tutorial** が必要だったことはありませんか？ あなただけではありません。請求書のスキャン、レシートの解析、あるいはシンプルなミームテキストの抽出など、さまざまなプロジェクトで PNG ファイルができ、カスタムの文字認識器を作らずに文字を取り出す方法を悩んでいることでしょう。

このガイドでは実践的な解決策を提供します。Aspose.OCR を使って **extract text image c#** を行い、**recognize png text** を実行し、そして C# の `JsonSerializer` で **write indented json** を行います。最後まで実行すれば、任意の .NET ソリューションに組み込める自己完結型のコンソールアプリが手に入ります。「ドキュメントを参照」などの曖昧なリンクはなく、完全なコピー＆ペースト可能なサンプルが用意されています。

## What You’ll Need

- **.NET 6**（または任意の最新 .NET バージョン）。古いフレームワークでも動作しますが、ここで示す構文は .NET 6+ を対象としています。
- **Aspose.OCR for .NET** – NuGet でインストール: `dotnet add package Aspose.OCR`.
- 明瞭で機械可読なテキストを含むサンプル PNG 画像（`text.png`）。
- お好みの IDE またはエディタ – Visual Studio、VS Code、Rider など。

> **Pro tip:** 多数の画像を処理する予定がある場合は、ファイルごとに新しい `OcrEngine` を作成するのではなく、単一の `OcrEngine` インスタンスを再利用することを検討してください。オーバーヘッドが削減され、スループットが向上します。

## Step 1: Set Up a c# ocr tutorial Project

まず、コンソールプロジェクトを作成します。以下のコマンドでプロジェクトの雛形を作成し、OCR ライブラリを取得します。

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

生成された `Program.cs` を開きます。後で全体のサンプルに差し替えますが、まずはプロジェクトがビルドできることを確認してください。

```bash
dotnet build
```

エラーが出なければ、次に進めます。

## Step 2: Recognize PNG Text from an Image

任意の **c# ocr tutorial** の核心は OCR エンジンそのものです。Aspose.OCR は低レベルの詳細を抽象化し、シンプルな `OcrEngine` クラスを提供します。以下ではエンジンを作成し、PNG ファイルを指定してテキスト認識を実行します。

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Why This Works

- **`RecognizeImage`** は多数のフォーマット（PNG、JPEG、BMP）を受け付けます。PNG はロスレスな詳細を保持するため、OCR に最適であり、ここでは特に **recognize png text** を行います。
- 返される `OcrResult` にはプレーンテキストだけでなく、文字ごとの信頼度スコアが含まれます。後で低信頼度の文字を除外したい場合に便利です。

## Step 3: Write Indented JSON with JsonSerializer c#

`ocrResult` を取得したので、次の論理的なステップは **c# ocr tutorial** の一環として、そのオブジェクトを人間が読みやすい JSON に変換することです。組み込みの `System.Text.Json` シリアライザが役割を果たし、**write indented json** になるよう設定します。

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Using `JsonSerializer` Correctly

- `WriteIndented` フラグは、サードパーティのライブラリを導入せずに **write indented json** を実現する最も簡単な方法です。
- プロパティ名をキャメルケースにしたい場合は、オプションに `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` を追加します。
- `jsonOutput` 文字列は `File.WriteAllText("result.json", jsonOutput);` で保存でき、実運用のパイプラインで便利です。

## Step 4: Run and Verify the Output

プログラムをコンパイルして実行します。

```bash
dotnet run
```

`text.png` にフレーズ *“Hello, OCR World!”* が含まれていると仮定すると、以下のような出力が得られるはずです。

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

この JSON は **indented** で、ログで読みやすく、下流サービスへの受け渡しも容易です。

### Edge Cases & Tips

| Situation | What to Do |
|-----------|------------|
| **Image is blurry** | `RecognizeImage` を呼び出す前に `ocrEngine.Config.Dpi` を上げます（例: `ocrEngine.Config.Dpi = 300`）。 |
| **Non‑English language** | `ocrEngine.Config.Language = OcrLanguage.German` のように、対象言語を設定します（サポートされている任意の言語）。 |
| **Large batch of files** | ディレクトリをループし、同じ `OcrEngine` インスタンスを再利用します。各 JSON 結果はユニークなファイル名で保存します。 |
| **Need only high‑confidence text** | シリアライズ前に `ocrResult.Lines` をフィルタし、`Confidence` ≥ 0.95 のものだけを残します。 |

## Full Working Example (Copy‑Paste Ready)

以下は `Program.cs` に貼り付け可能な *全体* のプログラムです。すべての手順、エラーハンドリング、コメントが含まれており、コードが自己説明的になるようになっています。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

コードを実行し、コンソールまたは生成された `.json` ファイルを確認すると、抽出されたテキストと信頼度スコアがきれいに **indented** されて出力されているのがわかります。

## Conclusion

これで、`JsonSerializer` を使用して **extract text image c#**、**recognize png text**、**write indented json** を実現する堅実な **c# ocr tutorial** が完成しました。サンプルは完全で実行可能、実務シナリオ向けの実用的なヒントも含まれています。  

次のステップは？ Aspose.OCR を別のエンジン（例: Tesseract）に置き換えて `OcrResult` の形がどう変わるか試すか、あるいは JSON を下流の API に渡して OCR データをデータベースに保存するかです。また、**use jsonserializer c#** のオプションとして、日付フォーマットや列挙型処理用のカスタムコンバータを試すこともできます。

コーディングを楽しんで、OCR パイプラインが常に正確でありますように！  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}