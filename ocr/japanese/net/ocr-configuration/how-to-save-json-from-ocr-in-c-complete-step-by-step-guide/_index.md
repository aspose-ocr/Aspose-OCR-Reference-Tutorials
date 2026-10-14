---
category: general
date: 2026-03-02
description: Aspose OCR を使用して画像からテキストを抽出しながら JSON を保存する方法を学びます。JSON ファイルの書き込みコード、ビットマップ画像の読み込みヒント、完全な
  C# サンプルが含まれています。
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: ja
og_description: Aspose OCRで画像からテキストを抽出しながらJSONを保存する方法を発見しましょう。完全なC#コード、JSONファイルの書き込み手順、実用的なヒントをご紹介します。
og_title: C#でOCRからJSONを保存する方法 – 完全プログラミングチュートリアル
tags:
- C#
- OCR
- Aspose
- JSON
title: C#でOCRからJSONを保存する方法 – 完全ステップバイステップガイド
url: /ja/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRからJSONを保存する方法 – 完全ステップバイステップガイド

画像から取得したテキストを含む **JSONを保存する方法** を考えたことがありますか？ あなただけではありません。多くの開発者が *画像からテキストを抽出* して、その情報をきれいに整形されたJSONファイルとして永続化する際に壁にぶつかります。良いニュースは、適切な要素が揃えば解決策はかなりシンプルだということです。

このチュートリアルでは、実際のシナリオとして Aspose.OCR を使用して **画像からテキストを抽出** し、次に **JSONファイルを書き出す** 出力を行い、最終的にディスクに **JSONを保存する方法** を示します。途中で **ビットマップ画像をロード** する方法も正しく示し、遭遇しうるいくつかのエッジケースもカバーします。最後までに、画像のロードから使用可能なJSONドキュメントの生成までをすべて行う、自己完結型の C# コンソールアプリが手に入ります。

## 必要なもの

- .NET 6.0 以降（コードは .NET Core および .NET Framework でも動作します）
- Aspose.OCR for .NET（無料トライアルの NuGet パッケージを取得できます）
- 英文が含まれるサンプル PNG または JPG 画像
- Visual Studio、VS Code、または任意の C# 対応 IDE

追加のライブラリは必要ありません—ビットマップ処理には標準の `System.Drawing` 名前空間、シリアライズには `System.Text.Json` を使用します。

---

## ステップ 1 – ビットマップ画像をロードする（“load bitmap image” 部分）

OCR を実行する前に、画像を `Bitmap` としてメモリに読み込む必要があります。これは、ページを読む前に本を開くことに例えられます。

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **プロのコツ:** 画像が大きい場合は、まずリサイズしてパフォーマンスを向上させることを検討してください。OCR エンジンは 2 MB 未満の画像でより高速に動作します。

---

## ステップ 2 – Aspose OCR エンジンを構成する

ビットマップが準備できたので、`OcrEngine` が必要です。このオブジェクトは **画像からテキストを抽出** する方法を知っており、オプションでバウンディングボックスなどのジオメトリデータも提供できます。

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

`ExportBoundingBoxes` を有効にする理由は何ですか？ UI で単語をハイライトする必要がある場合、これらの座標は非常に有用です。不要な場合はフラグを `false` に設定すれば、JSON がややコンパクトになります。

---

## ステップ 3 – OCR を実行し、構造化された結果を取得する

エンジンが構成されたら、次のステップは実際の **テキスト抽出方法** の操作です。`RecognizeToOcrResult` メソッドは、認識されたテキスト、信頼度スコア、オプションのレイアウトデータを含むリッチなオブジェクトを返します。

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

`ocrResult` 変数には必要な情報がすべて格納されています。デバッガで確認すると、`Page`、`Paragraph`、`Line`、`Word` オブジェクトの階層が表示され、各オブジェクトは `Text` プロパティを持っています。

---

## ステップ 4 – 結果を整形された JSON 文字列にシリアライズする

ここが **JSONを保存する方法** の魔法が本格的に始まるところです。`System.Text.Json` を使用します。これは組み込みで高速、かつデフォルトで整形出力（pretty printing）をサポートしています。

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

別の命名規則（例: camelCase）が必要な場合は、オプションに `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` を追加するだけです。

---

## ステップ 5 – JSON をディスクに書き込む（“write json file” ステップ）

最後に、実際に **JSONファイルを書き込む** ことでファイルシステムに保存します。これが C# 環境で **JSONを保存する方法** に対する具体的な回答です。

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

この行が実行されると、元の画像の隣にインデントされた `sample-page.json` が作成されます。任意のテキストエディタで開くか、別のサービスに渡すことができます—OCR データが今やポータブルです。

---

## ステップ 6 – 出力を検証する（何が表示されるべきか）

プログラムを実行すると、コンソールに簡単な確認メッセージが表示されます：

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

生成された JSON ファイルを開くと、以下のような内容が見られます：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

`ExportBoundingBoxes` フラグが true の場合、各単語には `Rectangle` 座標も含まれます。これは下流の UI 作業に便利です。

---

## よくある質問とエッジケース

### 画像パスが無効な場合は？

`Bitmap` のロードを `try/catch` ブロックで囲み、明確なエラーを表示します：

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### 英語以外の言語を扱うには？

`Language` プロパティを変更するだけです：

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose は 50 以上の言語をサポートしているので、ソース素材に合った言語を選択してください。

### `Bitmap` オブジェクトを破棄する必要がありますか？

はい。`Bitmap` は `IDisposable` を実装しているため、`using` 文で囲んでネイティブリソースを速やかに解放してください。

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### インデントなしのコンパクトな JSON が欲しい場合は？

`JsonSerializerOptions` を入れ替えます：

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

これによりファイルサイズが削減され、帯域幅が制限されたシナリオで有用です。

---

## 完全動作例（コピー＆ペースト可能）

以下は、上記のすべてのステップ、エラーハンドリング、ベストプラクティスのヒントを組み込んだ完全なプログラムです。`Program.cs` として保存し、コマンドラインまたは IDE から実行してください。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**このプログラムの動作:**  
1. 画像が存在するか確認します。  
2. `using` ブロックで安全にロードします。  
3. OCR を実行して **画像からテキストを抽出** します。  
4. 結果を整形された JSON 文字列にシリアライズします。  
5. その文字列をディスクに保存し、核心的な質問 **JSONを保存する方法** に答えます。

`dotnet run` を実行する（または Visual Studio で F5 を押す）と、ファイルが書き込まれた際に確認メッセージが表示されます。

---

## 結論

これで、OCR に基づくテキスト抽出から生成された **JSONを保存する方法** の完全なプロダクション向けレシピが手に入りました。ビットマップ画像のロードからクリーンな JSON ファイルの書き込みまで、各ステップはコードの背後にある “なぜ” を交えて説明しているので、独自のプロジェクトに合わせてソリューションを適応できます。

次のステップに興味があるなら、以下を検討してください：

- まず各ページを画像に変換して **PDF からテキストを抽出** する方法。  
- バウンディングボックスデータを使用して WPF または WinForms UI で単語をハイライトする。  
- JSON をファイルに書き込む代わりに直接 Web API にストリーミングする（`HttpClient` を使用）。

ぜひ試してみて、オプションを調整し、OCR データを構築中のアプリケーションに活用してください。質問があればコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}