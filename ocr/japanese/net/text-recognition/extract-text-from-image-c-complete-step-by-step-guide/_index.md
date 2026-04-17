---
category: general
date: 2026-03-29
description: Aspose OCR を使用して C# で画像からテキストを抽出します。信頼度値を含む JSON の取得方法、エッジケースの処理、数分で結果を保存する方法を学びましょう。
draft: false
keywords:
- extract text from image c#
- c# ocr library
- aspose ocr c#
- image to text c#
- json output c#
language: ja
og_description: Aspose OCR を使用して C# で画像からテキストを抽出します。このガイドでは、テキストの認識方法、信頼度スコアの含め方、JSON
  出力の保存方法を示します。
og_title: C#で画像からテキストを抽出 – 完全プログラミングチュートリアル
tags:
- C#
- OCR
- Aspose
- JSON
title: 画像からテキストを抽出する C# – 完全ステップバイステップガイド
url: /ja/net/text-recognition/extract-text-from-image-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する C# – 完全ステップバイステップガイド

低レベルのピクセル処理に悩むことなく、**画像からテキストを抽出する C#** ができるか気になったことはありませんか？ あなただけではありません。多くのプロジェクト—請求書のスキャン、領収書のデジタル化、あるいはスクリーンショットを検索可能なテキストに変換するだけでも—画像から単語を抽出できることは必須スキルです。

このチュートリアルでは、Aspose.OCR ライブラリを使用した実用的なソリューションを順を追って解説します。最後まで実行すれば、画像を読み込み、すべての単語とその信頼度スコアを取得し、任意の下流システムに渡せる整然とした JSON ファイルを書き出すコンソール アプリが完成します。曖昧な説明は一切なく、コピー＆ペースト可能な完全な例です。

## 学べること

* **C# OCR** NuGet パッケージのインストール方法。
* 正しい言語で OCR エンジンを初期化する重要性。
* **画像からテキストを認識** し JSON としてエクスポートするための正確なコード。
* ファイルが見つからない場合や画像形式が異なる場合、信頼度閾値の扱い方のヒント。
* 出力を検証し、より大きなワークフローに統合する方法。

**Prerequisites** – .NET 6 以降、Visual Studio 2022（またはお好みのエディタ）、処理したい画像ファイルが必要です。OCR の事前知識は不要です。

![画像からテキストを抽出する C# の例](https://example.com/placeholder.png "画像からテキストを抽出する C# スクリーンショット")

## 手順 1: Aspose.OCR NuGet パッケージをインストールする

コードを書く前に、まず Aspose OCR ライブラリをプロジェクトに追加します。このパッケージはすべてのネイティブモデルをバンドルし、クリーンな C# API を提供します。

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* Visual Studio を使用している場合は、プロジェクトを右クリック → **Manage NuGet Packages** → “Aspose.OCR” を検索して **Install** をクリックすることもできます。これにより、最新の安定版（現在は 23.12）を取得できます。

## 手順 2: OCR エンジンを初期化する

エンジンの作成はシンプルですが、**why** が重要です。`Language` プロパティを設定すると、エンジンが期待する文字セットを認識し、精度が大幅に向上します。

```csharp
using Aspose.OCR;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine and tell it we’re processing English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // English works for most Latin‑based documents
        };
```

フランス語やドイツ語で処理したい場合は、`Language.English` を `Language.French` または `Language.German` に置き換えるだけです。ライブラリは 40 以上の言語を標準でサポートしています。

## 手順 3: 画像からテキストを認識する

ここでエンジンにファイルパスを渡します。`RecognizeImage` メソッドはビットマップを読み込み、ニューラルネットワークを実行し、各単語・バウンディングボックス・信頼度 (0‑100) を保持する `OcrResult` オブジェクトを返します。

```csharp
        // Path to the image you want to process – adjust as needed
        string inputPath = "YOUR_DIRECTORY/input.png";

        // Make sure the file exists before we try to read it
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Error: Cannot find {inputPath}");
            return;
        }

        // Perform the OCR operation
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**Edge case:** 画像が大きすぎる（>5 MB）とメモリ制限に達することがあります。その場合は、まず画像をリサイズする（例: `System.Drawing` を使用）か、ファイルパスの代わりに `Stream` を渡してください。

## 手順 4: OCR 結果を信頼度付き JSON に変換する

ライブラリは便利な `ToJson` メソッドを提供します。`includeConfidence: true` を指定すると、以下のような詳細ペイロードが得られます。

```json
{
  "Text": "Hello World",
  "Words": [
    { "Text": "Hello", "Confidence": 98.5 },
    { "Text": "World", "Confidence": 96.2 }
  ]
}
```

JSON 文字列を生成しディスクに書き込むコードは次のとおりです。

```csharp
        // Serialize the result, including per‑word confidence
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // Destination file – feel free to change the name or folder
        string outputPath = "YOUR_DIRECTORY/output.json";

        // Write the JSON to a file (overwrites if it already exists)
        File.WriteAllText(outputPath, jsonResult);
```

*Why keep confidence?* 後でテキストをデータベースに格納する場合、信頼度が低い単語（例: `< 80%`）を除外して下流の品質を向上させることができます。

## 手順 5: JSON を保存して出力を検証する

最終ステップは、処理が正常に完了したことをユーザーに通知し、必要に応じて JSON の最初の数行を表示して結果を目視で確認できるようにするだけです。

```csharp
        // Let the user know we’re done
        Console.WriteLine("JSON saved with confidence values.");
        Console.WriteLine($"Output file: {outputPath}");

        // Optional: print a short preview (first 200 chars)
        Console.WriteLine("Preview:");
        Console.WriteLine(jsonResult.Substring(0, Math.Min(200, jsonResult.Length)) + "...");
    }
}
```

プログラムを実行すると（`dotnet run`）、次のような出力が表示されます。

```
JSON saved with confidence values.
Output file: YOUR_DIRECTORY/output.json
Preview:
{
  "Text":"Hello World",
  "Words":[
    {"Text":"Hello","Confidence":98.5},
    {"Text":"World","Confidence":96.2}
  ]
}...
```

任意のエディタで `output.json` を開くと、抽出されたテキストの機械可読表現が確認でき、さらに処理を進める準備が整います。

## よくある質問と落とし穴

| Question | Answer |
|----------|--------|
| **Can I process PDFs directly?** | Aspose.OCR はラスタ画像で動作します。PDF ページを PNG/JPEG に変換してから（例: Aspose.PDF を使用）OCR エンジンに渡してください。 |
| **What if I need multi‑language support?** | `ocrEngine.Language = Language.Multilingual` と設定するか、画像ごとに言語を切り替えてください。 |
| **How do I handle a corrupted image?** | `RecognizeImage` を `try/catch` で囲み、`ImageCorruptedException` を捕捉してデフォルト画像にフォールバックするかエラーをログに記録してください。 |
| **Is the JSON format fixed?** | はい、固定です。ただし、好みでカスタム C# クラスにデシリアライズして強く型付けされたモデルとして扱うことも可能です。 |

## 本番向け OCR のプロチップ

* **Batch processing:** 画像ディレクトリをループし、各 JSON 結果をマスターファイルに追記します。  
* **Confidence filtering:** `ocrResult.Words.Where(w => w.Confidence < 80).ToList()` で信頼度が低い単語を抽出できます。  
* **Parallelism:** 大量バッチでは `Parallel.ForEach` を使用しますが、CPU の過負荷を防ぐために同時実行数は制限してください。  
* **Logging:** `Serilog` や `NLog` と統合して OCR の処理時間やエラー率を記録します。  

## 次のステップ

**画像からテキストを抽出する C#** ができるようになったので、以下を検討してください。

* **SQL データベースに結果を保存** – 各単語とその信頼度をテーブルにマッピングして分析に活用。  
* **Azure Cognitive Services と統合** して言語検出や翻訳を実装。  
* **シンプルな API を構築**（ASP.NET Core）し、アップロードされた画像を受け取りリアルタイムで JSON を返す。

これらの拡張はすべて、本チュートリアルで扱ったコア概念を基盤としており、信頼性の高い OCR パイプラインの堅実な土台から恩恵を受けます。

---

*Happy coding! If you hit any snags, drop a comment below or check the Aspose.OCR documentation for advanced configuration options.*  
*ハッピーコーディング！問題が発生したら下にコメントを残すか、Aspose.OCR のドキュメントで高度な設定オプションを確認してください。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}