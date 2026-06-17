---
category: general
date: 2026-03-15
description: Aspose OCR を使用して画像からテキストを抽出し、C# で画像を JSON に変換する方法。PNG からテキストを認識し、迅速に構造化された出力を取得する方法を学びます。
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出し、C# で画像を JSON に変換する方法。このガイドでは、PNG からテキストを認識し、構造化された出力を取得する手順を解説します。
og_title: Aspose OCR を使用して画像を JSON に変換する方法
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose OCR を使用して画像を JSON に変換する方法
url: /ja/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用して画像を JSON に変換する

Aspose OCR の使い方は、開発者が画像からテキストを抽出する必要があるときによくある質問です。**画像を JSON に変換**したり、**PNG からテキストを認識**したりしたい場合、このガイドがすべてカバーします—余計な説明はなく、実用的なエンドツーエンドのソリューションです。

数分で、ライブラリのインストール、JSON 出力のエンジン設定、レシート PNG の読み込み、OCR の実行、そして最終的に結果を `.json` ファイルに書き込むまでの手順をすべて解説します。最後まで読めば、**画像からテキストを抽出**するメソッド呼び出し一つで完了し、各ステップの重要性も理解できるようになります。

> **プロのコツ:** Aspose OCR は幅広い画像フォーマット (PNG、JPEG、BMP、TIFF) に対応しています。以下の同じコードで全て処理できるので、フォーマット固有のロジックを書く必要はありません。

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）  
- 有効な Aspose.OCR NuGet パッケージ（無料トライアルまたはライセンス版）  
- 処理したい画像ファイル（例: `receipt.png`）  
- Visual Studio、VS Code、またはお好みの C# エディタ  

それだけです—余計な依存関係や外部サービスは不要です。準備はできましたか？さっそく始めましょう。

![Aspose OCR エンジンの使い方](image-placeholder.png "Aspose OCR エンジンの使い方")

## Aspose OCR の使用方法 – JSON 出力の設定

OCR 用に **Aspose の使い方** を始める際に最初に行うべきことは、`OcrEngine` インスタンスを作成し、JSON を出力するよう指示することです。この小さな設定スイッチにより、後で結果を手動でシリアライズする手間が省けます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**この設定が重要な理由:** `OutputFormat` を `Json` に設定すると、OCR エンジンはテキストをページ、行、単語の階層構造に自動で整形します。後で生の文字列を解析する必要がなくなるため、データベースへの投入などの下流処理が格段にシンプルになります。

## Aspose OCR で画像を JSON に変換する

エンジンが設定されたので、**画像を JSON に変換**する部分を詳しく見ていきます。

1. **画像を読み込む** – `Image.FromFile` はサポートされているすべてのフォーマットで動作します。ストリーム（例: アップロードされたファイル）から処理する場合は `Image.FromStream` を使用できます。  
2. **`Recognize` を実行** – このメソッドは `OcrResult` オブジェクトを返します。出力を JSON に設定しているため、`ocrResult.Text` にはすでに JSON 文字列が格納されています。  
3. **ファイルに書き込む** – `File.WriteAllText` は JSON を永続化する最もシンプルな方法です。クラウドバケットに保存したい場合は、この行を適切な SDK 呼び出しに置き換えるだけです。

### 期待される JSON 出力

典型的な JSON ペイロードは以下のようになります（簡略化）:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

この構造を任意の下流システムに渡すことができます—レポートツール、機械学習モデル、あるいは単純なログファイルでも構いません。

## Aspose OCR を使用して画像からテキストを抽出する

JSON が不要で、生の文字列だけが必要な場合は、出力形式をプレーンテキストに戻すだけです:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**プレーンテキストを選ぶタイミング**  
- 素早いデバッグやコンソール出力。  
- カスタムの後処理（例: 正規表現抽出）を適用したいシナリオ。  

ただし、**画像からテキストを抽出**する際に JSON を使用すると、位置情報が得られます—UI でテキストをハイライトしたり、フォームフィールドと位置合わせしたりするのに便利です。

## PNG ファイルからテキストを認識する

PNG はロスレス形式であり、圧縮率の高い JPEG に比べて OCR の精度が向上しやすいです。**PNG からテキストを認識**する際に最高の結果を得るための簡易チェックリストをご紹介します。

| チェック項目 | 効果の理由 |
|----------------|--------------|
| DPI を 300 以上に設定する | 高解像度はエンジンにより多くのピクセルを提供し、精度が向上します。 |
| 画像をグレースケールに保つ | ノイズが減少します。Aspose OCR は自動で変換しますが、前処理により速度が向上します。 |
| 背景の雑音を除去する | 背景がクリアだと信頼度スコアが向上します。 |

信頼度スコアが低い場合は、DPI を上げるか、シンプルな閾値フィルタを適用してから Aspose に画像を渡してみてください。

## OCR 結果をプログラムで抽出する

JSON を保存するだけでなく、特定のフィールド（例: レシートの合計金額）をプログラムで読み取りたいこともあるでしょう。JSON が階層構造を持っているので、C# オブジェクトにデシリアライズできます:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

これで `ocrData` を LINQ でクエリできます:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**この方法が機能する理由:** JSON は各単語がページ上のどこにあるかを既に示しているため、レイアウトが多少変わってもフィールドを確実に特定できます。

## エッジケースと一般的な落とし穴

- **Null 結果:** `ocrEngine.Recognize` が `null` を返す場合、画像がサポート外または破損している可能性があります。必ずチェックしてください:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **大容量ファイル:** 数メガバイト級の画像の場合、OCR 前に画像をストリーミングするかリサイズして、メモリ使用量を抑えることを検討してください。

- **ライセンス問題:** トライアル版は出力に透かしを追加します。プログラム開始時にライセンスをロードするようにしてください:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **非ラテン文字スクリプト:** Aspose OCR は多くの言語に対応していますが、`Language` プロパティを適切に設定する必要があります（例: `ocrEngine.Configuration.Language = Language.English;`）。

## 完全動作例（コピー＆ペースト可能）

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}