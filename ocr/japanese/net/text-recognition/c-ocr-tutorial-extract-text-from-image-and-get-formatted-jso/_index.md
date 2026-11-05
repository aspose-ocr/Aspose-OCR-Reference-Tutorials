---
category: general
date: 2026-01-13
description: C# OCRチュートリアル：画像からテキストを抽出し、OCR用に画像を読み込み、Aspose OCRを使用してJSON出力をフォーマットする方法を示します。オブジェクトをJSONにシリアライズする方法を学びましょう。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: ja
og_description: 画像からテキストを抽出し、OCR用に画像を読み込み、Aspose OCRでJSON出力をフォーマットする手順を示すC# OCRチュートリアル。
og_title: C# OCRチュートリアル – テキスト抽出とJSONフォーマット
tags:
- OCR
- C#
- JSON
title: c# OCRチュートリアル – 画像からテキストを抽出し、フォーマットされたJSONを取得
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 画像からテキストを抽出し JSON 出力を整形

C# プロジェクトで低レベルのピクセル処理に悩むことなく、**extract text from image** ファイルを行う方法を考えたことはありますか？ それがこの *c# ocr tutorial* が解決する課題です。数分で **load image for ocr** の方法、Aspose OCR の実行、そして **format json output** の手順を確認でき、データを API やデータベースに直接渡すことができます。

コードを一行ずつ解説し、各部分がなぜ重要かを説明し、期待される正確な JSON 例も示します。最後には、請求書 PNG をきれいにインデントされた JSON に変換するコンソール アプリが完成します。余計な説明は省き、実践的なソリューションだけを提供します。

## What This c# ocr tutorial Covers

- Aspose.OCR NuGet パッケージのインストール  
- OCR 処理用の画像ファイルの読み込み  
- 英語テキスト（またはサポートされている任意の言語）の認識  
- **Serializing the OCR result to JSON** を整形して出力  
- コンソールへの JSON 表示と、必要に応じた保存  

C# の基本的な知識と最近の .NET SDK があれば十分です。請求書、領収書、スキャンしたフォームなどの **extract text from image** に興味がある方は、ぜひ読み進めてください。

---

## Step 1: Set Up the c# ocr tutorial Environment

コードを書く前に、必要なツールを揃えてください：

1. **.NET 6 SDK 以降** – Microsoft のサイトからダウンロードできます。  
2. **Visual Studio 2022**（Community エディションでも可）またはお好みのエディタ。  
3. **Aspose.OCR NuGet パッケージ** – プロジェクト フォルダーで `dotnet add package Aspose.OCR` を実行します。

> **Pro tip:** CI パイプラインを使用している場合は、`.csproj` にパッケージ参照を追加しておくと、ビルド時に自動で復元されます。

---

## Step 2: Load Image for OCR

チュートリアルの最初の実際のステップは、処理したい画像を取得することです。Aspose OCR は PNG、JPEG、TIFF などの一般的な形式をサポートしています。

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** 画像を `OcrImage` として読み込むことで、エンジンはビットマップ データや DPI 情報にアクセスでき、認識精度が向上します。このステップを省略したり、破損したファイルを渡すと実行時例外が発生します。

---

## Step 3: Extract Text from Image

いよいよ OCR エンジンを実行します。`Recognize` メソッドは、生テキスト、信頼度スコア、レイアウト情報を含むリッチな `OcrResult` オブジェクトを返します。

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Edge case:** 多言語文書を処理する必要がある場合は、異なる `OcrLanguage` 値で `Recognize` を2回呼び出し、結果を結合します。エンジンはスレッドセーフなので、大量バッチを並列化することも可能です。

---

## Step 4: Serialize Object to JSON – Format JSON Output

`OcrResult` オブジェクトは単なる C# クラスなので、`System.Text.Json` に渡すことができます。`WriteIndented` を有効にすると、出力が人間に読みやすい形式になります。

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **What you get:** 認識されたテキスト、信頼度、ページレイアウトを含む、見やすくインデントされた JSON 文字列が得られます。ログ出力や Web サービスへの送信、NoSQL データベースへの保存に最適です。

---

## Step 5: Display and (Optionally) Save the Formatted JSON

最後に、JSON をコンソールに出力します。必要に応じて `File.WriteAllText` を使ってファイルに書き込むこともできます。

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Expected console output (truncated for brevity):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

OCR エンジンがテキストを検出できなかった場合、`Text` フィールドは空文字列になり、`Confidence` は `0` になります。これは画像品質を再確認すべきサインです。

---

## Step 6: Complete Working Example

すべてをまとめた完全なプログラムを以下に示します。新しいコンソール アプリにコピー＆ペーストして使用してください。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

プロジェクト フォルダーで `dotnet run` を実行すると、スキャンした請求書の JSON 表現がきれいに整形されてコンソールに表示されます。

---

## Common Pitfalls & Tips (c# ocr tutorial Extras)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank `Text` field** | 画像のコントラストが低い、または回転している。 | 画像を前処理（コントラスト増加、デスキュー）するか、`OcrEngine.ImagePreprocess` を使用。 |
| **`System.DllNotFoundException`** | Aspose OCR のネイティブ バイナリが見つからない。 | NuGet パッケージが正しく復元されたか確認し、ランタイム アーキテクチャ（x64/x86）が OS と一致していることを確認。 |
| **Performance lag on large PDFs** | OCR が各ページを順次処理している。 | ページごとに別々の `OcrEngine` インスタンスを作成して並列化（エンジンはスレッドセーフ）。 |
| **JSON too large** | バウンディング ボックスなどすべての詳細をシリアライズしている。 | シリアライズ前に `Text` と `Confidence` のみを含む DTO に変換。 |

> **Remember:** このチュートリアルの目的は、クリーンでエンドツーエンドなフローを示すことです。後から JSON を削減したり、メタデータを追加したりしても構いません。

---

## Conclusion

**c# ocr tutorial** を完了し、画像を読み込み、**extract text from image** を実行し、**format json output** を **serializing object to json** で整形しました。手順はシンプルで、コードはすぐに実行可能、JSON は下流の処理に最適な形でインデントされています。

次は何をしますか？ `OcrLanguage.English` を `OcrLanguage.French` に置き換えてみる、または領収書フォルダー全体をループで処理してみる。さらに、JSON を直接 Azure Blob Storage に保存したり、機械学習モデルに渡したりすることも検討してください。

エラーが出たら、画像パスが正しいか、Aspose OCR のライセンス（所有している場合）が `Recognize` 呼び出し前にロードされているかを再確認してください。Happy coding、そして OCR 結果が常に鮮明でありますように！

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}