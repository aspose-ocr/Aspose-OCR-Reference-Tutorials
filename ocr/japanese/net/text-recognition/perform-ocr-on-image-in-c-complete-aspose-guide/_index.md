---
category: general
date: 2026-06-28
description: C# で Aspose.OCR を使用して画像の OCR を実行します。画像からテキストを認識し、請求書からテキストを抽出し、OCR 用に画像を読み込み、JSON
  をファイルに書き出す方法を学びます。
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: ja
og_description: C#でAspose.OCRを使用して画像のOCRを実行します。このガイドでは、画像からテキストを認識し、請求書からテキストを抽出し、JSONをファイルに書き込む方法を示します。
og_title: C#で画像のOCRを実行する – Aspose OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: C#で画像のOCRを実行する – 完全なAsposeガイド
url: /ja/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像のOCRを実行 – 完全な Aspose ガイド

画像ファイルに対して **画像でOCRを実行** したいが、どの .NET ライブラリがきれいで構造化された結果を提供してくれるか分からないことはありませんか？ あなたは一人ではありません。開発者は常に **画像からテキストを認識** する方法を尋ねており、特に請求書や領収書を扱うときにそのニーズは高まります。このチュートリアルでは、画像を **OCR用に読み込む** だけでなく、**請求書からテキストを抽出** し、**JSONを書き込む** ことで下流処理に利用できる例をハンズオンで解説します。

このガイドを最後まで読むと、次のことができるコンソールアプリが手に入ります。

* Aspose OCR エンジンをインスタンス化
* PNG（または JPG）画像を読み込み
* テキスト内容を認識
* 結果を整形された JSON にシリアライズ
* その JSON をディスクに保存

外部サービスは不要、隠されたマジックもなし――コピー＆ペーストしてすぐに実行できる純粋な C# コードだけです。

## 前提条件

作業を始める前に、以下を用意してください。

* .NET 6 SDK 以降（コードは .NET Core と .NET Framework のどちらでも動作します）
* 有効な Aspose.OCR ライセンス、または一時的な評価キー（無料トライアルでテスト可能）
* Visual Studio 2022、VS Code、またはお好みの IDE
* 画像ファイル（例: `invoice.png`）を、フルパスまたは相対パスで参照できる場所に配置

> **プロのコツ:** スキャンした請求書を扱う場合は、OCR エンジンに渡す前に画像の前処理（デスキュー、コントラスト強化）を検討してください。Aspose.OCR は多くの前処理を自動で行いますが、元画像がクリアであるほど結果は向上します。

---

## 手順 1: プロジェクトの作成と Aspose.OCR のインストール

まず、コンソールプロジェクトを新規作成し、Aspose.OCR NuGet パッケージを追加します。

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **この手順が重要な理由:** `Aspose.OCR` アセンブリは、**画像でOCRを実行** するために使用する `OcrEngine` クラスを提供します。パッケージが無いと、OCR 関連の型がコンパイラに認識されません。

---

## 手順 2: OCR 用に画像を読み込む

次に、**画像をOCR用に読み込む** コードを書きます。`OcrImage.FromFile` メソッドは絶対パスまたは相対パスを受け取り、エンジンが理解できる形式にビットマップをラップします。

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **解説:** パスを別変数に分離することでコードがすっきりし、後でロギングやデバッグ時に同じ画像参照を再利用しやすくなります。ファイルが見つからない場合、`FromFile` は `FileNotFoundException` をスローするので、キャッチしてフレンドリーなエラーメッセージを表示できます。

---

## 手順 3: 画像で OCR を実行しテキストを認識

画像が手元にあれば、`OcrEngine` インスタンスを作成し、**画像からテキストを認識** させます。このステップがチュートリアルの核心で、実際の OCR マジックが行われます。

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **`using var` を使う理由:** `OcrEngine` はアンマネージドリソース（ネイティブライブラリ）を保持します。`using` ブロックでラップすることで適切に破棄され、メモリリークを防止します――長時間稼働するサービスでは特に重要です。
>
> **取得できる情報:** `ocrResult` には生テキスト、信頼度スコア、レイアウト情報（行、単語、バウンディングボックス）が含まれます。多くの請求書処理パイプラインでは `Text` プロパティだけで十分ですが、追加メタデータは検証や可視化デバッグに役立ちます。

---

## 手順 4: 結果を整形された JSON に変換

Aspose.OCR は `OcrResult` に `ToJson` メソッドがあるため、**JSONを書き込む** のが非常に簡単です。`indent: true` を指定すれば人間が読みやすい出力が得られ、後で **請求書からテキストを抽出** する際に便利です。

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **サンプル JSON スニペット**（省略表示）:

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **エッジケース:** OCR エンジンがテキストを検出できなかった場合、`ocrResult.Text` は空文字列になりますが、JSON には画像サイズなどのメタデータが残ります。ファイルを書き込む前に空結果をチェックしてガードすると安全です。

---

## 手順 5: JSON をファイルに書き込む

いよいよ **JSONを書き込む** 作業です。`File.WriteAllText` を使えば、文字列全体が一度の原子的な操作でディスクに保存されます。

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **本番向けのヒント:** ファイル名にタイムスタンプ（例: `invoice_20260628_1500.json`）を付与して、過去の実行結果が上書きされないようにしましょう。また、書き込み処理を try/catch で囲み、権限エラーなどを優雅に処理してください。

---

## 手順 6: 完全動作サンプル

すべてのパーツを組み合わせた、すぐにコンパイルして実行できる完全プログラムを示します。`YOUR_DIRECTORY` を `invoice.png` が格納されているフォルダーに置き換えてください。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**期待される出力**（プログラム実行時）:

```
JSON saved to C:\Invoices\invoice.json
```

`invoice.json` を開くと、整形された OCR データが確認でき、下流のパースや保存にすぐ利用できます。

---

## よくある質問とエッジケース

### 画像に複数言語が含まれる場合は？

Aspose.OCR は文字セットに基づいて自動的に言語を検出します。特定の言語（例: 請求書の多くは英語）を強制したい場合は、エンジンの `Language` プロパティを設定してください。

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### ページ数の多い PDF を処理したい場合は？

まず PDF を画像に変換（PDF‑to‑image ライブラリ使用）し、各ページ画像に対して同じ **画像でOCRを実行** 手順を繰り返します。結果の JSON を配列にまとめれば、統合出力が得られます。

### JSON をファイルに書き出さずにストリームで返すことは？

はい。Web API を構築している場合は、`json` をそのままレスポンスボディとして返せます。

```csharp
return Results.Json(ocrResult);
```

### パフォーマンスは？

上記例は同期的に OCR エンジンを呼び出しています。高スループットが必要なシナリオでは、`Task.Run` でラップするか、非同期版（利用可能なら）を使用して UI の応答性を保ちつつバッチ処理を並列化してください。

---

## 結論

本稿では、**画像でOCRを実行** し、**画像からテキストを認識**、**請求書からテキストを抽出**、そして最終的に **JSONを書き込む** 完全なエンドツーエンドソリューションを Aspose.OCR と C# で実装する方法を解説しました。コードは意図的にシンプルに保たれているので、画像前処理の追加や JSON のデータベース格納、REST エンドポイントでの公開など、より複雑なワークフローへ容易に拡張できます。

次のステップに進みましょう。PNG を JPEG に差し替えてみたり、`ocrEngine.Dpi` などの設定を変えてみたり、PDF‑to‑image 変換ステップを組み込んで請求書バンドル全体を処理したりしてみてください。基本をマスターすれば、可能性は無限です。

Happy coding, and may your OCR results always be crisp and accurate!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックをベースに、さらに関連するトピックを深掘りするものです。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探索に役立ちます。

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}