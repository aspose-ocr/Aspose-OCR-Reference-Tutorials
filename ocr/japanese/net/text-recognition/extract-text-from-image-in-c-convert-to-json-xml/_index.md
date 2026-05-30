---
category: general
date: 2026-04-26
description: Aspose.OCR を使用して C# で画像からテキストを抽出し、数分で画像を JSON および XML 形式に変換する方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: ja
og_description: Aspose.OCR を使用して C# で画像からテキストを抽出します。結果を JSON や XML に即座に変換する方法をステップバイステップで学びましょう。
og_title: C#で画像からテキストを抽出 – JSONとXMLに変換
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: C#で画像からテキストを抽出 – JSONとXMLに変換
url: /ja/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – JSON と XML に変換

.NET プロジェクトで **画像からテキストを抽出** したいと思ったことはありませんか？しかし「実際にデータを取得するにはどうすればいいのか？」で行き詰まっていませんか？あなたは一人ではありません。請求書処理、レシートスキャン、バッジ認証など、実際のアプリケーションでは画像から生の文字を取り出すことが最初で重要なステップです。  

良いニュースがあります。Aspose.OCR を使えば、数行のコードで実現でき、さらに下流システム向けに **画像を JSON に変換** したり **画像を XML に変換** したりできます。このガイドでは、完全に実行可能なコードを順に解説し、各部分が重要な理由を説明し、一般的な落とし穴を回避するコツをいくつか紹介します。

---

## 必要なもの

- **.NET 6+**（最新の SDK が使用可能です；サンプルは .NET 6 を対象）
- **Aspose.OCR for .NET** NuGet パッケージ  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 印刷可能なテキストを含む画像ファイル（PNG、JPG など）。例として `invoice.png` を使用します。
- コードエディタ（Visual Studio、VS Code、Rider のいずれでも構いません）。

それだけです。追加の OCR エンジンや外部サービスは不要で、単一の NuGet パッケージだけです。

---

## ステップ 1: OCR エンジンのセットアップ – 画像からテキストを抽出する方法

まず `OcrEngine` インスタンスを作成し、画像ファイルを指定します。このステップが基礎となり、画像が正しく読み込まれていなければエンジンは何も認識できません。

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Why this matters:**  
- `OcrEngine` は、二値化やデスケーリングなどの低レベル画像前処理をすべてカプセル化します。  
- `ImageStream.FromFile` で画像を読み込むことで、エンジンは正確なバイト列を取得し、DPI とカラーデプスを保持します。これらは認識精度に影響します。  

> **Pro tip:** ソース画像がストリーム（例: Web API でアップロードされたもの）にある場合は、`FromFile` の代わりに `ImageStream.FromStream(yourStream)` を使用してください。

---

## ステップ 2: エンジンに期待する言語を指定 – 画像からテキストを正確に抽出

Aspose.OCR は多数のアルファベットをサポートしています。正しい言語を指定することで文字セットが絞られ、精度が向上します。

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Why:**  
`Language.Latin` を設定すると、OCR エンジンはキリル文字やアジア文字を無視し、誤検出が減少します。後で多言語文書を扱う必要がある場合は、`Language.Multilingual` に切り替えるか、複数の言語を組み合わせることができます。

---

## ステップ 3: 認識プロセスを実行 – 画像からテキストを一括抽出

いよいよテキストを認識します。`Recognize` メソッドは `RecognitionResult` オブジェクトを返し、そこに生テキスト、信頼度スコア、レイアウトデータが格納されます。

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Why:**  
`Recognize` を一度呼び出すだけで、エンジン内部で前処理、セグメンテーション、文字分類が行われます。`Text` プロパティはプレーン文字列を提供し、ログ出力や簡易検証に最適です。

---

## ステップ 4: 結果を JSON に変換 – 画像を簡単に JSON に変換

多くのモダンサービスは JSON ペイロードを好みます。Aspose.OCR は `ToJson` メソッドを提供しており、`RecognitionResult` 全体（信頼度やバウンディングボックスを含む）をシリアライズできます。

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Why you might want JSON:**  
- **Interoperability:** フロントエンドアプリ（React、Angular など）は JSON を直接利用できます。  
- **Debugging:** JSON には文字ごとの信頼度が含まれ、信頼度の低い単語を手動レビューの対象としてフラグ付けできます。  

> **Edge case:** 下流システムがプレーンテキストだけを必要とする場合は、`recognitionResult.Text` を抽出し、独自の JSON オブジェクトにラップすれば、Aspose のフルペイロードを使用しなくても済みます。

---

## ステップ 5: 結果を XML に変換 – レガシーシステム向けに画像を XML に変換

一部の企業ではデータ交換に XML スキーマを使用し続けています。`ToXml` メソッドは `ToJson` と同様の情報を XML 形式で出力します。

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Why XML:**  
- **Schema validation:** Aspose が生成する構造に合わせた XSD を定義でき、契約遵守を保証できます。  
- **Integration:** 古い ERP や文書管理システムは、XML をそのまま解析できることが多いです。

---

## 完全動作サンプル – ワンストップコード

以下はすべてを結びつけた完全なプログラムです。`dotnet new console` で新しいコンソールプロジェクトを作成し、貼り付けて実行してください。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Expected output (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

JSON と XML ファイルには、たとえば次のようなリッチな構造が含まれます。

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## よくある質問とエッジケース

### 画像がぼやけている、または回転している場合は？
Aspose.OCR はほとんどの画像を自動でデスケーリングしますが、極端なケースでは `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` で前処理すると良いでしょう。コントラストを少し上げる（`ImageProcessor.AdjustContrast`）ことで信頼度スコアが向上することもあります。

### PDF からテキストを抽出できるか？
はい。まず各 PDF ページを画像に変換します（例: Aspose.PDF や無料ライブラリの PDFium を使用）。その画像を同じ OCR フローに渡せば抽出できます。

### 1 文書内で複数言語を扱うには？
`ocrEngine.Language = Language.Multilingual;` または特定の言語を組み合わせて設定します：

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

言語セットを広げすぎると認識精度が低下する可能性があることに注意してください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}