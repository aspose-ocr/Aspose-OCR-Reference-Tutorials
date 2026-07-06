---
category: general
date: 2026-03-17
description: C#でOCR結果のJSONを解析する方法を学びましょう。このチュートリアルでは、テキストの抽出、OCR用画像の読み込み、OCR認識の実行、そしてOCRエンジンをC#で効率的に使用する方法をカバーしています。
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: ja
og_description: C#でOCR出力からJSONを解析する方法。テキスト抽出、OCR用画像の読み込み、OCR認識の実行、OCRエンジンの使用方法をご案内します。
og_title: OCRエンジンC#でJSONを解析する方法 – 完全チュートリアル
tags:
- C#
- OCR
- JSON
- Image Processing
title: OCRエンジン（C#）でJSONを解析する方法 – 完全ステップバイステップガイド
url: /ja/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRエンジン C# で JSON を解析する方法 – 完全ステップ‑バイ‑ステップガイド

OCRエンジンから直接出力されるJSONを**how to parse json**したことがありますか？ あなたは一人ではありません。ほとんどの開発者が同じ壁にぶつかります—生のJSONを取得し、信頼度スコアや実際のテキストなどの有用な情報を抽出する最適な方法を見つけることです。このガイドでは、OCR用に画像をロードし、OCR認識を実行し、最後に**how to parse json**をクリーンで保守しやすい方法で行う手順を説明します。

チュートリアルの最後までに、以下ができるようになります：

* 数行のコードだけで OCR 用画像をロードできる。  
* C# OCR エンジンを使用して OCR 認識を実行できる。  
* **How to extract text** と JSON ペイロードからのその他のメタデータを取得できる。  
* クラッシュせずに一般的なエッジケース（欠損フィールド、予期しない形式）を処理できる。

外部ドキュメントは不要です—必要なものはすべてここにあります。

## 前提条件

始める前に、以下が揃っていることを確認してください：

* .NET 6.0 以降（コードは .NET Framework 4.7+ でもコンパイル可能）。  
* 使用している OCR ライブラリへの参照（例では仮想の `OcrEngine` クラスを使用）。  
* JSON 処理のための `Newtonsoft.Json` NuGet パッケージ（`Install-Package Newtonsoft.Json`）。  
* アプリが読み取れる場所に配置された画像ファイル（例：`passport.png`）。

> **Pro tip:** 商用 OCR SDK を使用している場合は、JSON 出力形式が有効になっているか確認してください—ほとんどのベンダーは `ocrEngine.Config.OutputFormat` のような構成プロパティでこれを公開しています。

## ステップ 1 – OCR エンジンの作成と構成（アクション内の主要キーワード）

最初に行うべきことは、OCR エンジンをインスタンス化し、JSON を返すように設定することです。ここでコード中に **how to parse json** というフレーズが初めて登場します。エンジンは後で解析する JSON 文字列を返します。

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Why this matters:** `OutputFormat` を `Json` に設定すると、認識されたテキスト **and** 信頼度スコアなどの有用なメタデータがレスポンスに含まれます。このステップを忘れるとプレーンテキストが返され、**how to parse json** が無意味になります。

## ステップ 2 – OCR 用画像のロード

次に、解析したい画像をロードします。ここが二次キーワード **load image for OCR** が光るポイントです。

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **What if the file isn’t there?** 呼び出しを `try/catch` でラップし、フレンドリーなメッセージを表示させましょう—アプリはクラッシュせず、ユーザーは何が問題だったか分かります。

## ステップ 3 – OCR 認識の実行

エンジンの準備ができ、画像もロードされたので、次は実際に認識プロセスを実行します。これが二次キーワード **run OCR recognition** に該当します。

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

`ocrResult.Text` プロパティには JSON 文字列が入ります。コンソールに出力すると次のようになります：

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## ステップ 4 – JSON からテキスト（および他のフィールド）を抽出する方法

チュートリアルの核心です：**how to parse json** と **how to extract text** を OCR ペイロードから行います。柔軟性のために `Newtonsoft.Json.Linq.JObject` を使用します。

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Why use `JObject`?** 完全な C# モデルクラスを定義せずに JSON ツリーを安全にナビゲートできます。`?.` 演算子は OCR エンジンがフィールドを省略した場合でも `NullReferenceException` を防ぎます。

### エッジケースの処理

* **Missing fields:** `?.Value<T>() ?? default` パターンで妥当なフォールバックを返します。  
* **Multiple pages:** 複数ページがある場合は `jsonObject["Pages"]` をループ処理します。  
* **Non‑numeric confidence:** SDK が文字列で返すことがある場合は `double.TryParse` を使用します。

## ステップ 5 – 再利用可能なメソッドにまとめる

同じボイラープレートをコピー＆ペーストしないように、フロー全体をヘルパーメソッドにカプセル化します。これにより **use OCR engine C#** をクリーンで再利用可能な形で示すことができます。

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

これで `RunOcrAndParseJson(@"C:\Images\passport.png");` を `Main` から、あるいはアプリケーションの任意の場所から呼び出せます。

## 完全動作例

以下は新しい `.csproj` にコピー＆ペーストできる、自己完結型のコンソールプログラムです。ここまで説明したすべての要素と、簡単なエラーハンドリングが含まれています。

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Expected output**（OCR が成功した場合）：

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

画像が読み取れない場合、SDK が例外をスローし、`Main` で捕捉してフレンドリーなエラーメッセージを出力するため、クラッシュしません。

## よくある質問 (FAQs)

**Q: OCR エンジンがページの配列を返す場合はどうすればいいですか？**  
A: `json["Pages"]` をループし、各 `["Text"]` 値を連結するか、ユースケースに応じて個別に処理してください。

**Q: JSON を型付き C# クラスにデシリアライズできますか？**  
A: もちろんです。JSON スキーマに合わせたクラス構造を定義し、`JsonConvert.DeserializeObject<YourRootClass>(result.Text)` を使用します。これによりコンパイル時の安全性が得られますが、モデルを SDK の出力と同期させておく必要があります。

**Q: 非同期 OCR API でも動作しますか？**  
A: はい。`engine.Recognize()` を `await engine.RecognizeAsync()` に置き換え、`RunOcrAndParseJson` を `async Task` にすれば OK です。JSON 解析部分は同じままです。

**Q: 後で分析できるように JSON をファイルに保存するには？**  
A: `result.Text` を取得した後、`File.WriteAllText(@"output.json", result.Text);` を呼び出します。その後 `JObject.Parse(File.ReadAllText(...))` で再読み込みできます。

## 次のステップ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}