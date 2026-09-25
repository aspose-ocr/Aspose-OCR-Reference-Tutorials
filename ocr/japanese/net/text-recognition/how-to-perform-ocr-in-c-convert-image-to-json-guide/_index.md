---
category: general
date: 2026-02-17
description: C#でOCRを実行し、画像をすばやくJSONに変換する方法。このC# OCRチュートリアルに従って画像からテキストを抽出し、レイアウトをJSONとして保存します。
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: ja
og_description: C#でOCRを実行する方法は？このガイドでは、画像をJSONに変換する方法、C#で画像からテキストを抽出する方法、OCR用に画像ファイルを読み込む方法を示します。
og_title: C#でOCRを実行する方法 – 画像をJSONに変換
tags:
- OCR
- C#
- Aspose
title: C#でOCRを実行する方法 – 画像をJSONに変換するガイド
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 画像をJSONに変換するガイド

C# を使ってレシート、請求書、または任意のスキャン文書で **OCR を実行する方法** を考えたことはありますか？ あなただけではありません。テキストを抽出し *かつ* レイアウトを保持する必要がある際に、カスタムパーサーを何時間も書くことなく壁にぶつかる開発者は多いです。  

このチュートリアルでは、**c# ocr tutorial** に相当する完全な手順を追い、OCR の実行方法、**画像を JSON に変換** する方法、そして結果を後で分析できるように保存する方法を示します。最後まで読むと、C# で画像ファイルを読み込みテキストを抽出し、座標、信頼度スコア、生のテキストを含む詳細な JSON ファイルを書き出す、すぐに実行できるコンソールアプリが手に入ります。

## 前提条件 — 必要なもの

- .NET 6 SDK 以上（コードは .NET Core でも動作します）  
- Visual Studio 2022 またはお好みのエディタ  
- Aspose OCR ライセンス（無料トライアルから開始可能）  
- サンプル画像、例: `receipt.png` を参照できるフォルダに配置  

以上です—`Aspose.OCR` 以外に追加の NuGet パッケージは不要です。これらが揃っていれば、すぐに始められます。

## OCR を実行して JSON 出力を取得する方法

Aspose を使った **OCR の実行方法** の核心はシンプルです：`OcrEngine` を作成し、画像ストリームを渡し、`Recognize` を呼び出し、最後に `OcrResult` を JSON にシリアライズします。ステップごとに分解してみましょう。

### 手順 1: Aspose OCR NuGet パッケージをインストール

プロジェクトフォルダでターミナルを開き、次を実行します：

```bash
dotnet add package Aspose.OCR
```

> **プロチップ:** `--version` フラグを使用して最新の安定版（例: `23.9.0`）に固定しましょう。これによりビルドの再現性が保たれます。

### 手順 2: コンソールプロジェクトの雛形を作成

まだプロジェクトがない場合は、次のコマンドで作成します：

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

これで `Program.cs` ファイルが用意でき、**load image file c#** のコードを書き込み、OCR プロセスを開始できる状態になります。

### 手順 3: 完全な OCR‑to‑JSON コードを書く

以下は完全で実行可能なプログラムです。`Program.cs` にコピー＆ペーストしてください。各行にコメントが付いているので、各部分が *なぜ* 必要かが分かります。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### コードの動作概要

| Step | なぜ重要か |
|------|----------------|
| **Initialize OcrEngine** | デフォルト言語（英語）を設定し、内部モデルを準備します。 |
| **Load image file** | `ImageStream.FromFile` を使用することで、Aspose が期待する形式で画像が読み込まれます。 |
| **Recognize** | 本格的な処理—ピクセル解析、文字分割、辞書参照を行います。 |
| **ToJson** | バウンディングボックス、信頼度、元テキストを含む構造化された出力を生成します。 |
| **WriteAllText** | JSON を永続化し、他のサービスと共有できるようにします。 |
| **Console.WriteLine** | 即時フィードバックを提供します—ターミナルから実行する際に便利です。 |

> **注意:** 画像が大きい場合は、速度とメモリ使用量を改善するために先にリサイズすることを検討してください。Aspose は `ImageStream` 上で呼び出せる `Resize` メソッドを提供しています。

### 手順 4: アプリケーションを実行し、出力を確認

ターミナルで次を実行します：

```bash
dotnet run
```

以下のように表示されるはずです：

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

`receipt.json` を任意のエディタで開くと、次のような内容が見られます：

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

この JSON は **extract text image c#** とレイアウトメタデータを含んでおり、下流処理に最適です。

## 画像を JSON に変換 – 基礎を超えて

これで **OCR の実行方法** が分かったので、実際のプロジェクトで必要になるかもしれないいくつかのバリエーションを見てみましょう。

### 複数ページの処理

ソースが複数ページの PDF や TIFF の場合は、各ページをループするだけです：

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### 言語と精度のカスタマイズ

Aspose は 40 以上の言語に対応しています。スペイン語に切り替えるには次を使用します：

```csharp
ocrEngine.Language = Language.Spanish;
```

`ocrEngine.Settings` を調整して **auto‑rotate**、**noise removal**、または **dictionary‑based correction** を有効にすることもできます—これらは取得する JSON の品質を向上させます。

### 整形された JSON で保存

可読性のためにインデントされた JSON が好みの場合は次を使用します：

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – よくある落とし穴とヒント

**load image file c#** を実行すると、次のような問題に直面することがあります：

- **File not found** – パスが絶対パスであることを確認するか、`Environment.CurrentDirectory` と `Path.Combine` を使用してください。  
- **Unsupported format** – Aspose は PNG、JPEG、BMP、TIFF、PDF をサポートしています。RAW 形式の場合は、先に変換してください。  
- **Large file memory pressure** – `ImageStream.FromFile(path, maxSizeInKB)` を使用して読み込み時に縮小できます。

これらの問題に早めに対処することで、OCR パイプライン後半での不明瞭な例外を防げます。

## Extract Text Image C# – 結果の検証

JSON を取得したら、プレーンテキストだけが欲しい場合があります：

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

このスニペットはレイアウト情報なしで **extract text image c#** を示します—素早い検索やログ出力に便利です。

---

![OCR ワークフロー図 – OCR の実行方法、画像を JSON に変換、テキスト画像抽出 c#](/images/ocr-workflow.png "OCR の実行ワークフロー")

*画像の代替テキスト: "OCR の実行ワークフロー図（画像を JSON に変換し、テキスト画像を抽出する様子）"*  
（この画像はプレースホルダーです。公開時には実際の図に差し替えてください。）

---

## 結論

C# での **OCR の実行方法** を最初から最後までカバーし、**画像を JSON に変換** する方法を示し、**load image file c#** と **extract text image c#** の微妙な違いも解説しました。完全なコード例は任意の .NET プロジェクトにすぐ組み込め、JSON 出力は生テキストと正確なレイアウトデータの両方を提供し、下流の分析に活用できます。

次は何をすべきでしょうか？ JSON をデータベースに投入したり、UI 上でバウンディングボックスを可視化したり、バッチ処理のために複数の OCR を連結したりしてみてください。また、手書き認識やバーコード検出といった他の Aspose 機能も試せます—どちらも同じパイプラインに自然に組み込めます。

問題が発生した場合は、「Load Image File C#」セクションのトラブルシューティングヒントを再確認するか、Aspose の豊富なドキュメントで高度な設定を調べてください。コーディングを楽しみ、画像を構造化データに変換する喜びを味わってください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}