---
category: general
date: 2026-01-01
description: c# OCRチュートリアル：テキスト抽出、OCR用画像の読み込み、Aspose.OCRを使用したJSONのファイル書き込みをステップバイステップで解説。
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: ja
og_description: c# OCRチュートリアルで、画像からテキストを抽出し、OCR用に画像を読み込み、Aspose.OCRを使用してJSONをファイルに書き込む方法をステップバイステップで解説します。
og_title: c# OCR チュートリアル – テキスト抽出と JSON へのエクスポート
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR チュートリアル – 画像からテキストを抽出し、JSONにエクスポート
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – 画像からテキストを抽出し JSON にエクスポート

スキャンした請求書からテキストを抽出するのに、カスタムパーサーを書いて何時間も費やすことなくできるか、考えたことはありませんか？ あなたは一人ではありません。この **c# OCR tutorial** では、OCR 用に画像をロードし、認識エンジンを実行し、そして **write JSON to file** してデータを下流システムに渡す方法を正確にお見せします。

レシートが入ったフォルダーがあり、各ファイルが `receipt1.png`、`receipt2.png` のように命名されているとします。このレシートをすばやく検索可能な JSON レコードに変換する方法が必要です。これが本チュートリアルで解決する課題で、最後にはそれを実行できるコンソールアプリが完成します。Aspose.OCR 以外の追加依存関係は不要で、魔法のようなことはありません—明確で再現可能な手順だけです。

> **学べること**
> - Aspose.OCR を使用した **load image for OCR** の方法。
> - **how to extract text** と信頼度スコアの取得ベストプラクティス。
> - OCR 結果を整然とした **OCR image to JSON** ペイロードに変換する方法。
> - **write JSON to file** を安全に行い、出力を検証する方法。

## Prerequisites

- .NET 6 SDK 以上（コードは .NET Core でも動作します）。  
- Visual Studio 2022 またはお好みのエディタ。  
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.O`）。  
- 処理したい画像ファイル（PNG、JPG、BMP）。デモでは `invoice.png` を使用します。

これらが揃っていない場合は、Microsoft のサイトから SDK を取得し、Package Manager Console で NuGet パッケージを追加してください。

```powershell
Install-Package Aspose.OCR
```

基が整ったので、実装に入りましょう。

## Step 1: c# OCR tutorial – OCR エンジンの初期化

**load image for OCR** を行う前に、認識プロセスを駆動するエンジンのインスタンスが必要です。`OcrEngine` クラスは軽量ですが、リソースを速やかに放できるよう `using` ブロックでラップするのがベストプラクティスです。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* 多数の画像をバッチ処理する場合は、毎回新しい `OcrEngine` を作成するのではなく、同じインスタンスを再利用するとメモリの消費が抑えられ、処理速度が向上します。

## Step 2: Load image for OCR

ここで実際に **load image for OCR** を行います。Aspose.OCR はさまざまなフォーマットに対応しているため、PNG、JPEG、さらにはマルチページ TIFF でも指定できます。`OcrImage.FromFile` メッドファイルを読み込み、認識の準備をします。

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **なぜ重要か:** 画像を別途ロードしておくことで、サイズや DPI、さらには前処理（例: 二値化）をエンジンに渡す前に確認できます。画像が破損している場合、`FromFile` は明確な例外をスローし、これをキャッチしてログに記録できます。

## Step 3: How to extract text – Run the recognition

画像が用意できたら、いよいよ **how to extract text** を実行します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、プレーンテキストだけでなく各単語の位置情報や信頼度スコアも含まれます。

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* PDF に見えないテキストレイヤーが含まれていることがあります。PDF ページを画像としてレンダリングして OCR にかけても何も認識されない場合があります。そのようなケースでは、まず Aspose.PDF を使って隠れたテキストレイヤーを抽出し、必要に応じて OCR を実行してください。

## Step 4: OCR image to JSON – Convert the result

`OcrResult` クラスは便利な `ToJson()` ヘルパーを提供しており、結果全体（各単語のバウンディングボックスと信頼度を含む）を JSON 文字列にシリアライズします。これが **OCR image to JSON** を自前のシリアライザーを書かずに実現する最もクリーンな方法です。

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

独自のスキーマが必要な場合は、`ocrResult.Words` を列挙して自分でオブジェクトを組み立てても構いませんが、ほとんどのシナリオでは組み込みの JSON で十分で、すでに整然としています。

## Step 5: Write JSON to file

最後のピースは JSON ペイロードを永続化することです。`File.WriteAllText` メソッドはファイルを（存在すれば上書きして）原子的に作成します。対象ディレクトリが存在しないと `DirectoryNotFoundException` が発生するので注意してください。

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* UTF‑8 に BOM を付けたい、または別のエンコーディングが必要な場合は、`Encoding` 引数を受け取るオーバーロードを使用してください。

## Step 6: Verify the output

簡単な `Console.WriteLine` で処理が正常に完了したことを確認できます。JSON ファイルをビューアで開いて構造をチェックするのもおすすめです。

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Expected JSON snippet

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON には各単語の位置情報が含まれるため、後で UI 上でテキストをハイライトしたい場合に便利です。

## Full Working Example

以下はそのままコピー＆ペーストできる完全版プログラムです。`YOUR_DIRECTORY` を画像が格納されている実際のパスに置き換えてください。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

プロジェクトフォルダーで `dotnet run` を実行すると、元の PNG と同じ場所に `invoice.json` が生成されます。

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** when loading the image | パスのタイプミスまたはファイルが存在しない | `Path.Combine` を使用し、`File.Exists` で確認してから `FromFile` を呼び出す |
| **Low confidence scores** | 画像品質が低い、DPI が不足している | `ocrImage.AdjustContrast` で前処理するか、画像を 300 DPI に拡大する |
| **JSON file empty** | `ocrResult` が null（エンジンが失敗） | 画像フォーマットがサポート対象か、ライセンス（必要な場合）が正しく適用されているか確認 |
| **Performance bottleneck on large batches** | 各イテレーションで `OcrEngine` を再作成している | バッチ全体で単一の `OcrEngine` インスタンスを再利用し、最後にだけ破棄する |

## Next Steps

**c# OCR tutorial** をマスターした今、次のような拡張が考えられます。

- フォルダー全体を **Batch process** し、JSON ファイルを単一のデータベースに集約する。  
- 出力を Azure Cognitive Search と **Integrate** して検索可能な PDF を実現する。  
- `ocrEngine.Language = OcrLanguage.Spanish`（またはサポートされている任意の言語）で **Add language support** を追加する。  
- 正規表現を使って JSON からテーブルやキー‑バリュー ペアを抽出する **Post‑process** を行う。

これらの拡張は、画像のロード、テキスト抽出、JSON 変換、ファイル書き込みという本チュートリアルで学んだコア概念に基づいています。

### Conclusion

この **c# OCR tutorial** では、**load image for OCR**、**how to extract text**、結果を **OCR image to JSON** ペイロードに変換し、最終的に **write JSON to file** するまでのすべての手順を解説しました。完全なコード例は任意の .NET プロジェクトにそのまま組み込めますし、解説は実務シナリオへの適用に必要なコンテキストを提供します。

自分のレシートや請求書で試してみてください—画像前処理を調整したり、言語を変えてみたりすれば、JSON 出力がどんどん豊かになります。問題が発生したら、上記の落とし穴表を再確認するか、コメントで質問してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}