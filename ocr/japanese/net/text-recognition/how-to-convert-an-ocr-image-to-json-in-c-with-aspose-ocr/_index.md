---
category: general
date: 2026-09-06
description: Aspose.OCR を使用した C# における OCR 画像から JSON への変換 – 画像からテキストを抽出し、JSON 出力を取得するステップバイステップガイド
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: ja
lastmod: 2026-09-06
og_description: C# と Aspose.OCR を使用した画像の OCR を JSON に変換。画像を OCR 用に読み込む方法、写真からテキストを認識する方法、そして結果を
  JSON に変換する方法を学びましょう。
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: C#でOCR画像をJSONに変換する – 完全なAspose.OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Aspose.OCR を使用して C# で OCR 画像を JSON に変換する方法
url: /ja/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.OCR を使用して OCR 画像を JSON に変換する方法

.NET アプリケーションで **ocr image to json** が必要な場合、このガイドでは Aspose.OCR を使用した手順を示します。OCR 用に画像を読み込み、写真からテキストを認識し、結果を JSON に変換して API やデータベースで利用できるようにします。

画像ファイルからテキストを抽出することは、請求書処理、領収書スキャン、アーカイブプロジェクトなどで一般的な要件です。このチュートリアルの最後までに、**convert image to text** ができ、プレーンテキストの結果を取得し、レイアウト情報を保持した構造化 JSON ペイロードを生成できるようになります。

## 前提条件

- .NET 6.0 SDK 以降がインストールされていること  
- Visual Studio 2022（または .NET をサポートする任意のエディタ）  
- プロジェクトに Aspose.OCR NuGet パッケージ（`Aspose.OCR`）が追加されていること  
- コードから参照できるフォルダーにサンプル画像（`input.jpg`）が配置されていること  

追加の OCR エンジンは必要ありません。Aspose.OCR が内部で重い処理を行います。

## 手順 1: Aspose.OCR NuGet パッケージをインストールする

プロジェクトフォルダーでターミナルを開き、以下を実行します：

```bash
dotnet add package Aspose.OCR
```

このパッケージには `Aspose.OCR.OcrEngine` クラスが含まれており、**load image for ocr**、言語選択、結果エクスポートのメソッドを提供します。

## 手順 2: 新しい C# コンソールプロジェクトを作成する

まだプロジェクトがない場合は、以下で作成します：

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

必要な `using` ディレクティブを追加します：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## 手順 3: 画像を読み込み OCR エンジンを構成する

以下のコードは **load image for ocr** の方法、言語設定、エンジンの処理準備を示しています。この例ではキリル文字を使用していますが、ソース言語に応じて `OcrLanguage.English`、`OcrLanguage.French` などに切り替えることができます。

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **重要な理由:** 正しい言語を設定することで、**recognize text from photo** 時の精度が大幅に向上します。エンジンは言語固有の辞書と文字セットを使用します。

## 手順 4: OCR プロセスを実行し結果を取得する

OCR エンジンを実行します。処理が成功すれば、**extract text from image** をプレーンテキスト、HTML、または JSON として取得できます。Aspose.OCR は構造化結果をファイルに書き出す `SaveJson` メソッドを提供します。

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### 期待される JSON 構造

典型的な `output.json` ファイルは以下のようになります（可読性のために整形）。

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

JSON ペイロードには各行のテキスト、信頼度スコア、元の写真でその行を囲む矩形が含まれます。これにより、OCR 結果を UI 要素やデータベースフィールドに簡単にマッピングできます。

## 手順 5: デモ用の完全なソースコード

以下は **ocr image to json** ワークフローを実行する、完全で実行可能なプログラムです。`Program.cs` にコピーし、`dotnet run` を実行してください。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### 例の実行方法

1. プロジェクトルートに `input.jpg` という名前の画像を配置します。  
2. `dotnet run` を実行します。  
3. コンソール出力を確認し、`output.json` を開いて構造化データを確認します。

## プロのコツと一般的な落とし穴

| 状況 | 推奨事項 |
|-----------|----------------|
| **低解像度の写真** | 処理前に DPI を上げるか、`ocrEngine.Image = ImageStream.FromFile(path, 300)` を使用して 300 DPI を強制してください。 |
| **混在言語** | `ocrEngine.Language = OcrLanguage.Multilingual` を設定し、必要に応じて `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` のように言語リストを提供します。 |
| **大容量ドキュメント** | メモリ使用量を抑えるためにページごとに処理し、エンジンはマルチページ TIFF をサポートしています。 |
| **文字の誤認識** | 正しい `OcrLanguage` が選択されているか確認してください。間違った言語を使用すると、**convert image to text** 時の精度が低下します。 |
| **JSON にフィールドが欠落** | Aspose.OCR バージョン 23.6 以降を使用していることを確認してください。古いリリースでは `SaveJson` メソッドが提供されていません。 |

## よくある質問

**Q: OCR 結果をファイルではなくバイト配列として取得できますか？**  
A: はい。`ocrEngine.SaveJson(Stream)` を使用して直接 `MemoryStream` に書き込み、`stream.ToArray()` で取得します。

**Q: エンジンは PDF 入力をサポートしていますか？**  
A: Aspose.OCR は Aspose.PDF を介して画像に変換した PDF ページを受け取れますが、OCR エンジン自体はラスタ画像で動作します。まず PDF を画像に変換し、次に **load image for ocr** を行ってください。

**Q: アラビア語など右から左へ書くスクリプトはどう扱いますか？**  
A: `ocrEngine.Language = OcrLanguage.Arabic` を設定します。JSON には正しいテキスト方向が含まれており、RTL をサポートする UI フレームワークで表示できます。

## 結論

これで C# における **ocr image to json** の完全なソリューションが手に入りました。画像を読み込み、言語を設定し、OCR エンジンを実行して結果を JSON としてエクスポートすることで、**extract text from image**、**convert image to text**、**recognize text from photo** を単一のシンプルなワークフローで実現できます。

ここからは以下を検討できます：

- `ASP.NET Core` の Web API と JSON 出力を統合する  
- MongoDB などの NoSQL データベースに結果を保存する  
- 一般的な OCR エラーを修正するポストプロセッシングを追加する  

プロジェクトの要件に合わせて、さまざまな言語、画像形式、出力オプションを自由に試してみてください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C#で画像からテキストを認識する – OCRとJSONの完全ガイド](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Aspose OCRを使用したC#で画像をテキストに変換 – ステップバイステップガイド](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Aspose.OCR for .NETを使用して画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}