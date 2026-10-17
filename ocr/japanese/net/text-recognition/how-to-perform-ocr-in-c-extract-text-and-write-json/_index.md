---
category: general
date: 2026-02-09
description: C#でOCRを実行し、画像からテキストを抽出し、PNGから文字を認識し、JSONファイルを書き出す方法を素早く学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: ja
og_description: C#でOCRを実行する方法は？このステップバイステップガイドに従って画像からテキストを抽出し、PNGから文字を認識し、C#で効率的にJSONファイルを書き出しましょう。
og_title: C#でOCRを実行する方法 – テキストを抽出してJSONを書き込む
tags:
- OCR
- C#
- Aspose
- JSON
title: C#でOCRを実行する方法 – テキスト抽出とJSON書き込み
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 完全ガイド

C#でOCRを実行することは、**画像からテキストを抽出**する必要があるときによくあるハードルです。このガイドでは、PNGからテキストを認識し、詳細な結果をJSON文字列にエクスポートし、最後に**C#スタイルでJSONファイルを書き込む**方法を順に説明します。スキャンしたフォームを見て、あの乱線を検索可能なテキストに変える方法を考えたことはありませんか？あなたは一人ではありません。多くの開発者が初期段階でこの問題に直面します。

Aspose.OCR ライブラリを使用します。このライブラリはシンボルごとの信頼度を標準で提供し、.NET 6+ プロジェクトと相性が良いからです。このチュートリアルの最後までに、PNG を読み込み、すべての文字を抽出し、データベースや AI モデルに渡せる整った JSON ファイルを保存する、すぐに実行できるコンソールアプリが手に入ります。「ドキュメントを参照」的な不明瞭な手順はありません—自己完結型のソリューションです。

## 必要なもの

- **.NET 6 SDK** (またはそれ以降) – 執筆時点での最新 LTS バージョンです。
- **Aspose.OCR for .NET** NuGet パッケージ – `Install-Package Aspose.OCR`.
- スキャンしたい PNG 画像（例: `form.png`）。  
- 好みの IDE またはエディタ – Visual Studio、VS Code、Rider など。

以上です。これらが揃っていれば、すぐに始められます。

![C# コンソールアプリが PNG を処理する様子を示す OCR 実行イラスト](ocr-example.png "C#でOCRを実行する方法")

*画像の代替テキスト: C# コンソールアプリが PNG を処理する様子を示す OCR 実行イラスト*

## ステップ 1: プロジェクトのセットアップと依存関係の追加

まず、新しいコンソールプロジェクトを作成し、Aspose OCR ライブラリを導入します。

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **プロのコツ:** ターゲットフレームワークを明示的に固定したい場合は `--framework net6.0` フラグを使用してください。

このステップが重要な理由: NuGet パッケージには、私たちが使用する `OcrEngine`、`ImageStream`、`JsonExporter` クラスが含まれています。これがなければ、コンパイラは “OCR” が何であるかさえ理解できません。

## ステップ 2: コア OCR ロジックの実装

`Program.cs` を開く（または新しいファイルを作成）し、内容を以下に置き換えます。各セクションにはコメントが付いているので、なぜそこにあるのかが分かります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### 各要素が重要な理由

- **OcrEngine**: 操作の「脳」と考えてください。言語モデルを読み込み、推論パイプラインを設定します。
- **ImageStream.FromFile**: PNG、JPEG、BMP などあらゆる形式を処理します。ファイル I/O の細かな違いを抽象化します。
- **RecognitionResult**: 生テキストと信頼度スコアを保持します。下流の検証に必要な詳細データがここにあります。
- **JsonExporter**: 豊富な `RecognitionResult` をクリーンな JSON ペイロードに変換し、API に最適です。
- **File.WriteAllText**: 余計な依存関係なしで **C#でJSONファイルを書き込む** ためのシンプルな .NET 方法です。

## ステップ 3: アプリケーションの実行と出力の確認

プログラムをコンパイルして実行します:

```bash
dotnet run
```

以下のようなコンソールメッセージが表示されるはずです:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

`form.json` を開くと、次のような内容が見つかります:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

**画像からテキストを抽出** ステップが成功し、すべての文字の機械可読な JSON 表現が手に入りました。

## ステップ 4: 一般的なエッジケースの処理

### ファイルが見つからない、または破損している場合

PNG のパスが間違っていると、`ImageStream.FromFile` は `FileNotFoundException` をスローします。ロードコードを try‑catch ブロックでラップしてください:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### 低信頼度スコアの場合

ノイズの多いスキャンでは OCR が低い信頼度を返すことがあります。エクスポート前にシンボルをフィルタリングできます:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

これにより、JSON には信頼できる文字だけが含まれ、下流の検証パイプラインにデータを渡す際に便利です。

### 大きなファイルとメモリ

数メガバイトの PNG を処理するとメモリ使用量が急増することがあります。画像をチャンクでストリーミングするか、`OcrEngine.RecognizeAsync`（新しい Aspose バージョンで利用可能）を使用して UI の応答性を保ちましょう。

## ステップ 5: ソリューションの拡張（オプション）

- **バッチ処理**: PNG が入ったディレクトリをループし、ファイルごとに対応する JSON を生成します。
- **データベース保存**: JSON を SQL の `NVARCHAR(MAX)` カラムに挿入し、後で分析に利用します。
- **言語選択**: 英語以外が必要な場合は `ocrEngine.Language = OcrLanguage.Spanish;` のように設定します。

これらすべての拡張は、私たちが確立した **OCR の実行方法** パターン—初期化、認識、エクスポート、永続化—に従っています。

## よくある質問

**Q: JPG や TIFF でも動作しますか？**  
A: もちろんです。`ImageStream.FromFile` はフォーマットを自動検出するので、PNG を任意のサポートされたラスタ画像に置き換えられます。

**Q: PDF からテキストを抽出したい場合は？**  
A: まず各 PDF ページを画像に変換します（例: `Aspose.PDF` を使用）。その後、ここで説明した OCR フローに PNG を渡します。

**Q: OCR 結果を JSON ではなく XML で取得できますか？**  
A: はい。Aspose.OCR には `XmlExporter` も用意されています。`JsonExporter` を `XmlExporter` に置き換え、ファイル拡張子を調整してください。

## 結論

C# で **OCR を実行する方法** を最初から最後まで順に解説し、**画像からテキストを抽出**、**PNG からテキストを認識**、そして **C#でJSONファイルを書き込む** 方法を問題なく示しました。完全な実行可能サンプルは上記のコードスニペットにあり、各ステップの背後にある理由—エンジンの初期化、エッジケースの処理、結果の永続化—が理解できたはずです。

次のステップとして、バッチ OCR パイプラインの検討、JSON 出力を Azure Cognitive Search と統合、あるいはカスタム言語モデルで実験することが考えられます。C# における OCR の基本を習得すれば、可能性は無限です。

もし問題に直面したり、さらなる拡張アイデアがあれば、下にコメントを残してください。コーディングを楽しんで、ピクセル化されたスキャンをクリーンで検索可能なデータに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}