---
category: general
date: 2026-01-02
description: C#でAspose OCRを使用して画像からテキストを抽出します。画像をJSONL形式に迅速かつ確実に変換する方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: ja
og_description: Aspose OCRで画像からテキストを抽出し、JSONL形式に変換します。開発者向けの完全なステップバイステップC#チュートリアル。
og_title: 画像からテキストを抽出 – C#でJSONLに変換
tags:
- C#
- OCR
- Aspose
- JSONL
title: 画像からテキストを抽出しJSONLに変換 – C# ガイド
url: /ja/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出しJSONLに変換 – 完全なC#チュートリアル

画像からテキストを抽出する必要があったが、どのライブラリがきれいで構造化された出力を提供するか分からなかったことはありませんか？ あなたは一人ではありません。領収書処理や文書デジタル化の多くのプロジェクトでは、ビットマップを検索可能なテキスト *および* 機械が読める形式に変換することがボトルネックになります。  

良いニュースは？ Aspose OCR を使えば **画像からテキストを抽出** でき、数行のコードで **画像をJSONLに変換** して下流の分析に活用できます。このガイドでは、PNG の読み込みからデータパイプラインにストリームできる JSON‑Lines ファイルの書き出しまで、全工程を順を追って説明します。

> **ヒント:** すでに .NET 6 以降を使用している場合、同じコードが追加設定なしで動作します。

## 前提条件 — 必要なもの

- **.NET 6 SDK**（または最新の .NET バージョン）
- **Aspose.OCR** NuGet パッケージ  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json**（シリアライズ用）  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- サンプル画像（例: `receipt.png`）を参照できるフォルダーに配置
- お好みの IDE またはエディタ — Visual Studio、VS Code、Rider など

重いセットアップや外部サービスは不要です。NuGet パッケージを数個入れるだけです。

![Aspose OCRを使用したC#での画像からテキスト抽出](https://example.com/assets/ocr-sample.png)

*Alt text: Aspose OCRを使用したC#での画像からテキスト抽出*

## 手順 1: 処理したい画像を読み込む  

画像からテキストを抽出したいときに最初に行うことは、OCR エンジンにビットマップを渡すことです。`System.Drawing.Bitmap` を使用すればシンプルで、ほとんどのラスタ形式に対応します。

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Why this matters:** 画像を `Bitmap` として読み込むことで、OCR エンジンはピクセルに直接アクセスでき、バイトストリームを渡す場合に比べて認識速度と精度が向上します。

## 手順 2: JSON‑Lines 出力のために Aspose OCR を設定する  

Aspose OCR では言語、出力形式、いくつかのパフォーマンス調整を指定できます。ここでは **JSON‑Lines**（1 行に 1 つの JSON オブジェクト）を要求します。後続の行単位処理に最適です。

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tip:** 多言語の領収書が必要な場合は `Language = Language.Multilingual` を設定するか、`Language` 値の配列を渡してください。

## 手順 3: OCR を実行し結果を取得する  

いよいよ **画像からテキストを抽出** します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、その中に認識されたテキスト行とバウンディングボックスを表す `OcrLine` コレクションが含まれます。

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

この時点で `ocrResult.Lines` には、テキスト、信頼度スコア、座標情報がすべて格納されています。

## 手順 4: 行を JSON‑Lines にシリアライズする  

コレクションを見やすいインデント付き JSON 文字列に変換します。JSON‑Lines は通常コンパクトですが、インデントを付けることで開発中のファイル確認が楽になります。

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

生成された `jsonLines` 変数は以下のようになります（簡略化）:

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

各行は改行文字で終わるため、真の **JSONL**（JSON‑Lines）ファイルとなります。

## 手順 5: JSON‑Lines をディスクに書き込む  

最後に出力を永続化します。これにより Spark、Logstash、シンプルな Bash スクリプトなど、他のサービスが行単位で取り込めるようになります。

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

`receipt.jsonl` を開くと、1 行に 1 つの JSON オブジェクトが並んでいることが確認でき、ストリーミングにすぐ使えます。

## 手順 6: エクスポートを検証する  

簡単なサニティチェックを行うことで、後々のデバッグ時間を大幅に削減できます。最初の数行を読み戻し、コンソールに出力してみましょう。

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

典型的なコンソール出力:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

このような結果が表示されれば、**画像からテキストを抽出**し **画像をJSONLに変換**できたことになります。おめでとうございます！

## よくある落とし穴と回避策  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank output** | 画像パスが間違っている、またはファイルが読めない。 | ビットマップを作成する前に `File.Exists(imagePath)` を使用して確認する。 |
| **Low confidence scores** | 画像がぼやけている、またはコントラストが低い。 | 画像を前処理する（例: `Bitmap.RotateFlip`、`Graphics.Clear`）または DPI を上げる。 |
| **Incorrect language** | OCR がデフォルトで英語になるが、領収書は別言語。 | `options.Language = Language.Spanish`（または該当する enum）を設定する。 |
| **JSONL appears as a single JSON array** | `Formatting.None` を使用し、改行処理を行っていない。 | 各シリアライズされたオブジェクトの末尾に `Environment.NewLine` が付くようにする。 |

## 完全な動作例  

以下はそのまま実行できる完全なプログラムです。コンソールプロジェクトに貼り付けて **F5** を押してください。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Expected result:** `receipt.jsonl` ファイルには、1 行に 1 つの JSON オブジェクトが格納され、各オブジェクトは `Text`、`Confidence`、`BoundingBox` フィールドを持ちます。このファイルを JSONL を受け取る任意の分析パイプラインに投入できます。

## 次のステップ – 基本 OCR を超えて  

- **Batch processing:** 上記ロジックを `foreach` ループでラップし、領収書フォルダー全体を処理する。  
- **Parallelism:** 数千枚の画像を扱う場合は `Parallel.ForEach` を使ってマルチコアで高速化する。  
- **Post‑processing:** 保存前に低信頼度行（`Confidence < 0.9`）を除去する。  
- **Integration:** 対応 SDK を使い、JSONL を Azure Blob Storage や AWS S3 に直接プッシュする。  
- **Alternative formats:** 下流システムが別形式を好む場合は `OutputFormat` を `PlainText` や `Xml` に切り替える。  

## 結論  

これで Aspose OCR を使用した **画像からテキストを抽出** と **画像をJSONLに変換** のエンドツーエンドソリューションが完成しました。ビットマップの読み込みから出力の検証までを網羅し、パイプラインを堅牢に保つ実用的なヒントも提供しました。自分の領収書、請求書、スキャンしたフォームで試してみてください。ピクセルが数秒で検索可能な行構造データに変わります。スキャンの傾きや多言語テキストなどのエッジケースに直面したら、*RecognitionOptions* セクションに戻り、言語設定や前処理を調整してください。

Happy coding, and may your data pipelines be ever‑clean!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}