---
category: general
date: 2026-02-16
description: C#でOCRを素早く実行する方法 – Aspose OCRライブラリを使用して画像からテキストを抽出する簡単な手順を学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- Aspose OCR C#
- OCR JSON output
- image text extraction
language: ja
og_description: C#でOCRを実行する方法は？Aspose OCRを使用して画像からテキストを抽出し、JSON結果を取得するステップバイステップのチュートリアルをご覧ください。
og_title: C#でOCRを実行する方法 – クイックガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でOCRを実行する方法 – Aspose OCRを使用して画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – Aspose OCRを使用した画像からテキスト抽出

C#で**OCRを実行する方法**に頭を抱えていませんか？ あなたは一人ではありません。スキャンしたフォームや領収書、手書きのメモからテキストを抽出する必要があるとき、多くの開発者が壁にぶつかります。良いニュースは、Aspose OCRを使えば、数行のコードで**画像からテキストを抽出**できるということです。

このチュートリアルでは、言語モデルのロード、画像の入力、認識エンジンの実行、結果のJSONシリアライズまでを示す、完全に実行可能なサンプルを順を追って解説します。最後には、任意の.NETプロジェクトに組み込める再利用可能なコードスニペットと、実務で役立つヒントを提供します。

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework でも動作しますが、.NET 6+ が推奨されます）
- 有効な Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）
- テキストが含まれる画像ファイル（JPEG、PNG、BMP など）
- 基本的な C# 開発環境（Visual Studio、Rider、または VS Code）

これだけで完了です—余分なOCRエンジンやネイティブDLLは不要、クリーンなマネージドライブラリだけです。

## ステップ 1: OCR エンジン インスタンスの作成 – OCR を実行する方法

最初に必要なのは `OcrEngine` オブジェクトです。これは重い処理を担う頭脳と考えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **このステップが重要な理由:** `OcrEngine` はすべての構成オプションをカプセル化します。これがなければ、どの言語を使用するか、画像の場所をライブラリに指示できません。

## ステップ 2: 言語モデルのロード – 画像からテキストを抽出

Aspose OCR には複数の言語パックが同梱されています。ほとんどの英語文書では組み込みの英語モデルをロードします。

```csharp
// Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **プロのコツ:** フランス語、ドイツ語、またはカスタム言語を認識する必要がある場合は、`LanguageModel.English` を適切な enum 値に置き換えるか、カスタムモデルファイルをロードしてください。

## ステップ 3: 処理対象画像の提供 – OCR を実行する方法

次に、エンジンに読み取るファイルを指示します。`ImageStream.FromFile` ヘルパーは画像を OCR エンジンが理解できる形式に読み込みます。

```csharp
// Supply the image (replace the path with your own file location)
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");
```

> **エッジケース:** 大きな画像（5 MB 超）は処理が遅くなる可能性があります。エンジンに渡す前にリサイズや圧縮を検討してください。

## ステップ 4: 認識の実行 – 画像からテキストを抽出

すべての準備が整ったら、いよいよ OCR 操作を実行します。`Recognize` メソッドはテキスト、バウンディングボックス、信頼度スコアを含む `OcrResult` オブジェクトを返します。

```csharp
// Perform OCR and capture the result
OcrResult ocrResult = ocrEngine.Recognize();
```

> **内部で何が起きているか？** エンジンは何百万もの文字で訓練されたニューラルネットワークを実行し、検出された各グリフを Unicode テキストにマッピングします。

## ステップ 5: 結果を JSON に変換 – OCR を実行する方法

最新の API の多くは JSON を期待します。結果をシリアライズしましょう。`ToJson` 拡張メソッドは整形された文字列を返します。

```csharp
// Serialize the OCR result to JSON
string jsonResult = ocrResult.ToJson();
```

典型的な JSON ペイロードは以下のようになります（簡略化）:

```json
{
  "Text": "Invoice #12345\nDate: 01/02/2026\nTotal: $250.00",
  "Words": [
    {
      "Value": "Invoice",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 80, "Height": 20 },
      "Confidence": 0.98
    },
    // ... more words ...
  ]
}
```

> **なぜ JSON？** 言語に依存せず、ログが取りやすく、Elasticsearch や REST API などの下流サービスへ送信するのに最適です。

## ステップ 6: JSON の出力 – 画像からテキストを抽出

最後に、JSON をコンソール（またはファイル、データベースなど）に書き出します。

```csharp
// Print the JSON result to the console
Console.WriteLine(jsonResult);
```

プログラムを実行すると完全な JSON 構造が表示され、**画像からテキストを抽出**できたことが確認できます。

## 完全な動作例

以下は新しいコンソールプロジェクトにコピー＆ペーストできる完全なコードです。抜けはありません—必要なものはすべてここにあります。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Load the English language model for recognition
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Provide the image to be processed
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");

            // Step 4: Perform OCR on the image
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 5: Convert the recognition result to JSON (includes text, bounding boxes, confidence scores)
            string jsonResult = ocrResult.ToJson();

            // Step 6: Output the JSON result
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **期待される出力:** 認識されたテキスト、各単語のバウンディングボックス、信頼度値を含む JSON 文字列です。画像が鮮明で言語モデルが一致すれば、信頼度スコアは通常 0.90 以上になります。

## よくある質問と落とし穴

- **画像が回転している場合は？**  
  Aspose OCR は自動で向きを検出できますが、最高の結果を得るには `System.Drawing` や `ImageSharp` を使って事前に回転させてからエンジンに渡すと良いでしょう。

- **PDF を直接処理できるか？**  
  標準機能では対応していません。各 PDF ページを画像に変換（例: Aspose.PDF を使用）し、その画像を OCR エンジンに渡してください。

- **マルチページのフォームはどう扱うか？**  
  各ページ画像をループで処理し、同じ手順を実行して JSON 結果を単一のコレクションに集約します。

- **出力をプレーンテキストのみに限定できるか？**  
  はい、連結された文字列だけが必要な場合は `ToJson()` の代わりに `ocrResult.Text` プロパティを使用してください。

## 本番環境向け OCR のプロティップス

1. **言語モデルをキャッシュ** – モデルのロードは軽いですが、1 秒間に数百枚の画像を処理する場合は、毎回新しく作らずに単一の `OcrEngine` インスタンスを維持してください。  
2. **信頼度閾値を調整** – `Confidence < 0.80` の単語を除外してノイズを減らします。  
3. **バッチ処理** – 大量の処理が必要なときは、画像パスをキューイングし、`Task.Run` で非同期に処理することを検討してください。  
4. **ロギング** – 生の JSON を元画像と共に保存して監査証跡を残すと、認識ミスのデバッグに非常に役立ちます。

## 結論

これで **C#でOCRを実行する方法** と **画像からテキストを抽出** するための、Aspose OCR ライブラリを使用したエンドツーエンドの解決策が手に入りました。サンプルはエンジン作成、言語ロード、画像入力、認識、JSON シリアライズ、出力までを一つの実行可能プログラムで示しています。

次は何をしますか？ 英語モデルを別の言語に置き換えてみる、異なる画像形式で実験する、あるいは JSON ペイロードを検索インデックスに統合するなど、可能性は無限です。この構成要素があれば、どんなテキスト抽出課題にも挑む準備が整いました。

Happy coding, and may your OCR results be ever accurate! 

![Aspose OCR ライブラリを使用した C# での OCR 実行を示す図](https://example.com/ocr-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}