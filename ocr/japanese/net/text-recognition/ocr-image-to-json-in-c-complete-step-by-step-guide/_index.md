---
category: general
date: 2026-02-11
description: C#でOCR画像をJSONに変換する。画像からテキストを抽出し、C#で画像ファイルを読み取り、JSON出力を整形し、Aspose.OCRを使用してC#でJSONを整形表示する方法を学びます。
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: ja
og_description: C#でOCR画像をJSONに変換する。このガイドでは、画像からテキストを抽出し、C#で画像ファイルを読み取り、JSON出力を整形し、Aspose.OCRを使用してC#でJSONをきれいに表示する方法を示します。
og_title: C#でOCR画像をJSONに変換する – 完全ステップバイステップガイド
tags:
- OCR
- C#
- JSON
title: C#でOCR画像をJSONに変換する – 完全ステップバイステップガイド
url: /ja/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

image to json – 完全ステップバイステップガイド". But maybe keep "ocr image to json" unchanged. We'll do: "# C# で ocr image to json – 完全ステップバイステップガイド". Good.

Now translate paragraphs.

Let's craft translation.

Will keep code block placeholders unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で ocr image to json – 完全ステップバイステップガイド

**ocr image to json** が必要だったけど、どのライブラリを選べばいいか、きれいに整形された結果を得るにはどうすればいいか分からない…という方は多いでしょう。レシートのスキャン、ID の検証、シンプルな文書アーカイブなど、実際のアプリケーションでは画像からテキストを抽出し、下流サービスが利用できるクリーンな JSON ペイロードに変換したい場面が頻繁にあります。

このチュートリアルでは、画像ファイルを C# で読み込み、Aspose.OCR でテキストを抽出し、エンジンに構造化された JSON 出力を要求し、最後に人が読みやすい形に整形（pretty‑print）するまでの全パイプラインを解説します。最後まで読めば、任意の .NET プロジェクトに貼り付けられる、実運用レベルの自己完結型コードが手に入ります。

また、言語パックが不足している場合の対処法など、よくある落とし穴や簡単なバリエーション（XML 出力への切り替えやマルチページ PDF の処理）も紹介します。外部ドキュメントは不要です。必要な情報はすべてここにあります。

## 必要なもの

- **.NET 6+**（.NET Framework 4.7+ でも動作します）
- **Aspose.OCR for .NET** – NuGet でインストール (`Install-Package Aspose.OCR`)
- サンプル画像（例: `receipt.png`）を参照できる場所に配置
- C# の基本構文に慣れていること（「Hello World」程度書ければ問題なし）

> *Pro tip:* CI サーバー上で実行する場合は `AutomaticResourceDownload = true` を設定しておくと、Aspose が必要な言語データをその場で取得してくれるので、DLL を手動で配置する手間が省けます。

## Step 1: Read image file C# and create the OCR engine  

最初にディスクから画像を読み込みます。`System.Drawing.Image` を使うとコードがシンプルになり、PNG、JPEG、BMP、さらにはマルチページ TIFF（デフォルトで最初のページが使用されます）にも対応できます。

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**ポイント:**  
- `AutomaticResourceDownload` を有効にすると、ローカルに英語言語ファイルが無くても実行時エラーを防げます。  
- `OutputFormat` を `Json` に設定すると、エンジンが OCR 結果の生データを自動的に構造化オブジェクトに変換してくれるため、手動で文字列を解析する必要がなくなります。

## Step 2: Run OCR and obtain JSON output  

ロードしたビットマップをエンジンに渡します。`Recognize` メソッドは `OcrResult` を返し、その `Text` プロパティに JSON 文字列が格納されています。

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**エッジケース:** 画像が破損している、またはパスが間違っている場合、`Image.FromFile` は `FileNotFoundException` をスローします。入力が不安定になる可能性がある場合は `try/catch` で囲んでください。

## Step 3: Parse and format the JSON – pretty print JSON C#  

OCR エンジンから出力される JSON はコンパクトで読みにくいです。`System.Text.Json` を使って `JsonDocument` にデシリアライズし、インデント付きで再シリアライズすれば見やすくなります。

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**出力例:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

整形された JSON には、行単位のテキスト、バウンディングボックス、検出言語、信頼度スコアが含まれ、下流の分析や UI コンポーネントへの入力に最適です。

## Step 4: Bonus – Switching output format or language  

**format json output** を XML に変更したり、スペイン語のレシートを OCR したりしたい場合は、エンジン設定を少し変えるだけです。

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

残りのコードは同じです。デシリアライズ部分だけを `XmlDocument` に置き換えれば XML 出力が得られます。

## Full Working Example  

すべてをまとめた単一ファイルです。コンソールアプリにコピペすればすぐに動作します。

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

このプログラムを実行すると、整形された JSON ペイロードがコンソールに出力され、`C:\Temp\ocr_pretty.json` に保存されます。`try/catch` ブロックにより、画像が読めない場合でもエラーメッセージが表示され、サイレントクラッシュを防げます。

## Common Questions & Gotchas  

- **OCR が空文字列を返した場合は？**  
  画像がノイズが多すぎるか、言語が合っていない可能性があります。画像のコントラストを上げるか、`Language` を `AutoDetect` に変更してみてください。  

- **複数画像をループで処理できるか？**  
  可能です。`using (var img = Image.FromFile(...))` ブロックを `foreach (var file in Directory.GetFiles(...))` ループで囲み、各 `prettyJson` をリストに集めるか、別々のファイルに書き出すだけです。  

- **JSON スキーマは安定しているか？**  
  Aspose は `Json` 出力形式の後方互換性を保証していますが、特定の API バージョンを対象にする場合はレスポンス内の `Version` 属性を必ず確認してください。  

- **Aspose.OCR のライセンスは必要か？**  
  無料評価キーで最大 100 ページまで利用可能です。実運用ではライセンスを購入し、`License license = new License(); license.SetLicense("Aspose.OCR.lic");` のように設定してください。

## Conclusion  

これで **C# で ocr image to json を実現する完全な自己完結型ソリューション** が手に入りました。画像ファイルの読み込み、OCR エンジンの設定、JSON 出力の取得、整形という一連の流れをマスターすれば、文字抽出を任意の .NET サービスにシームレスに組み込めます。

次のステップとしては、**extract text from image** を PDF やマルチページ TIFF など他のファイル形式に拡張したり、言語を増やしたり、JSON を NoSQL ストアに流し込んで分析基盤を構築したりしてみてください。エラーハンドリングとライセンス管理さえしっかりすれば、スケールアップも安心です。

Happy coding, and may your OCR pipelines be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}