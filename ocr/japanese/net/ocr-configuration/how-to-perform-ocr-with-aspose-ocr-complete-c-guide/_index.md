---
category: general
date: 2026-07-05
description: Aspose.OCR を使用して C# で OCR を実行し、言語を設定し、画像を読み込んで OCR を行い、PNG を JSON に変換する方法を、簡単な手順で学びましょう。
draft: false
keywords:
- how to perform OCR
- how to set language
- convert png to json
- load image ocr
- set ocr language
language: ja
og_description: C#でAspose.OCRを使用してOCRを実行し、OCR言語を設定し、画像を読み込んでOCRし、PNGをJSONに変換する方法—すべてを一つの簡潔なチュートリアルで。
og_title: Aspose.OCRでOCRを実行する方法 – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  headline: How to Perform OCR with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  name: How to Perform OCR with Aspose.OCR – Complete C# Guide
  steps:
  - name: – Install the Aspose.OCR NuGet Package
    text: 'Before you can even think about **how to perform OCR**, the library has
      to be on your machine. Open a terminal in your project folder and run:'
  - name: – Load the Image for OCR (load image OCR)
    text: 'Now that the package is ready, you need to **load image OCR**. The engine
      expects an `ImageStream`, which you can create from a file path, a `MemoryStream`,
      or even a byte array. Here’s the simplest approach using a PNG file on disk:'
  - name: – Set the OCR Language (how to set language / set OCR language)
    text: Aspose.OCR supports over 60 languages, but it defaults to English. If your
      document is in another language, you must tell the engine which one to use.
      That’s where **how to set language** and **set OCR language** come into play.
  - name: – Perform OCR and Convert PNG to JSON
    text: 'With the image loaded and the language set, the final piece is to run the
      OCR engine and **convert PNG to JSON**. Aspose.OCR makes this a one‑liner:'
  - name: Full Working Example (All Steps Combined)
    text: 'Putting everything together, here’s a compact program you can compile and
      run instantly:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Aspose.OCRでOCRを実行する方法 – 完全なC#ガイド
url: /ja/net/ocr-configuration/how-to-perform-ocr-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCRでOCRを実行する方法 – 完全なC#ガイド

大量の定型コードを書かずに、スキャンした請求書で **OCRを実行する方法** を知りたくありませんか？ あなたは一人ではありません。画像からテキストを抽出する必要があるとき、多くの開発者が壁にぶつかります。特に、下流のフォーマットがJSONである必要がある場合はなおさらです。

このチュートリアルでは、Aspose.OCR ライブラリを使用した **OCRを実行する方法** を正確に示し、**言語の設定方法** を学び、**画像OCRのロード** の最適な方法を発見し、**PNGをJSONに変換** するすぐに実行できるスニペットを提供します。最後まで読むと、任意の .NET プロジェクトに組み込める堅牢な本番環境向けソリューションが手に入ります。

![Aspose.OCR を使用した C# での OCR 実行方法を示す図](ocr-flow.png "OCR の実行方法")

## 学べること

- Aspose.OCR を実行するための最小限の前提条件。
- ステップバイステップのコードで、**画像 OCR をロード**し、正しい言語を選択し、**PNG を JSON に変換**します。
- 正しい OCR 言語を設定する重要性と安全な設定方法。
- 一般的な落とし穴（大きなファイル、サポートされていない言語）とその回避方法。
- すぐにコピー＆ペーストできる完全な実行可能サンプル。

## C# で Aspose.OCR を使用して OCR を実行する方法

### 手順 1 – Aspose.OCR NuGet パッケージをインストールする

**OCR を実行する方法** を考える前に、まずライブラリをマシンにインストールする必要があります。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

この1行で最新の安定版（2026年7月時点、バージョン 23.10）が取得されます。余計な DLL や手動設定は不要で、クリーンなパッケージ参照だけです。

### 手順 2 – OCR 用に画像をロードする (load image OCR)

パッケージの準備ができたら、**画像 OCR をロード**する必要があります。エンジンは `ImageStream` を期待しており、ファイルパス、`MemoryStream`、またはバイト配列から作成できます。以下はディスク上の PNG ファイルを使用した最もシンプルな方法です。

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

// Create an OCR engine instance
var engine = new OcrEngine();

// Load the image you want to process
engine.Image = ImageStream.FromFile(@"C:\Invoices\invoice.png");

// Optional: verify that the image was loaded
if (engine.Image == null)
{
    throw new InvalidOperationException("Failed to load the image. Check the file path.");
}
```

> **重要性:** 画像を正しくロードすることは、すべての OCR パイプラインの基礎です。画像がロードされていないと、エンジンは暗号的な `NullReferenceException` をスローし、デバッグが悪夢になります。

### 手順 3 – OCR 言語を設定する (how to set language / set OCR language)

Aspose.OCR は 60 以上の言語をサポートしていますが、デフォルトは英語です。文書が別の言語の場合、エンジンに使用する言語を指示する必要があります。ここで **言語の設定方法** と **OCR 言語の設定** が重要になります。

```csharp
// Specify the language of the text in the image
engine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish, etc.

// You can also set multiple languages if needed
// engine.Language = OcrLanguage.English | OcrLanguage.French;
```

> **ヒント:** 言語は常に明示的に設定してください。テキストが英語でも、`OcrLanguage.English` を明示的に割り当てることで、エンジンが言語検出ステップを省略し、精度が向上することがあります。

### 手順 4 – OCR を実行し PNG を JSON に変換する

画像がロードされ、言語が設定されたら、最後のステップは OCR エンジンを実行し **PNG を JSON に変換**することです。Aspose.OCR ではこれがワンライナーで実現できます。

```csharp
// Perform OCR and save the recognized text as JSON
engine.Save(@"C:\Invoices\invoice.json", OcrOutputFormat.Json);
```

生成される JSON は以下のようになります。

```json
{
  "Pages": [
    {
      "Text": "Invoice #12345\nDate: 2026-07-01\nTotal: $1,250.00\n..."
    }
  ]
}
```

この構造は、下流の API、データベースへの挿入、または簡易 UI プレビューに最適です。

### 完全な動作例（すべての手順を統合）

すべてをまとめると、すぐにコンパイルして実行できるコンパクトなプログラムがこちらです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var engine = new OcrEngine();

        // 2️⃣ Load the PNG image (load image OCR)
        string inputPath = @"C:\Invoices\invoice.png";
        engine.Image = ImageStream.FromFile(inputPath);
        if (engine.Image == null)
        {
            Console.WriteLine($"Unable to load image from {inputPath}");
            return;
        }

        // 3️⃣ Set the language (how to set language / set OCR language)
        engine.Language = OcrLanguage.English; // Adjust as needed

        // 4️⃣ Run OCR and write JSON (convert PNG to JSON)
        string outputPath = @"C:\Invoices\invoice.json";
        engine.Save(outputPath, OcrOutputFormat.Json);

        Console.WriteLine($"OCR complete! JSON saved to {outputPath}");
    }
}
```

**コンソールに期待される出力:**

```
OCR complete! JSON saved to C:\Invoices\invoice.json
```

JSON ファイルを開くと、抽出されたテキストが次の処理にすぐ使える状態で表示されます。

## よくあるエッジケースと対処方法

| 状況 | 注意点 | 推奨修正 |
|-----------|-------------------|-----------------|
| **大きな PNG (>10 MB)** | メモリ使用量の急増、処理速度の低下 | まず `engine.Image = ImageStream.FromFile(...).Resize(1024, 0)` を使用して画像を縮小します |
| **サポートされていない言語** | `engine.Language` 設定時に `ArgumentException` が発生 | `OcrLanguage.GetSupportedLanguages()` で言語列挙体を確認します |
| **破損した画像ファイル** | ロード時に `InvalidOperationException` がスロー | `try/catch` でロード呼び出しを囲み、`File.Exists` でファイルを検証します |
| **JSON の代わりにプレーンテキストが必要** | 出力形式が間違っている | `engine.Save(outputPath, OcrOutputFormat.PlainText)` を使用します |

## 精度向上のプロティップス

1. **画像の前処理** – エンジンに渡す前にコントラストを上げたりグレースケールに変換したりします。Aspose.OCR では `engine.Image = engine.Image.AdjustContrast(1.2f)` を使って手軽に調整できます。
2. **回転したスキャンの傾き補正** – 文書が完全に整列していない場合は `engine.Image = engine.Image.Deskew()` を使用します。
3. **バッチ処理** – 数十枚の請求書を処理する際は同じ `OcrEngine` インスタンスを再利用します。言語モデルをキャッシュし、以降の呼び出しを高速化します。
4. **JSON の検証** – 保存後に簡易スキーマチェックを実行し、出力が下流の契約と合致していることを確認します。

## まとめ：OCR をエンドツーエンドで実行する方法

- NuGet で Aspose.OCR をインストールする。  
- **画像 OCR をロード** は `ImageStream.FromFile` を使用。  
- `engine.Language` を使用して **OCR 言語を設定**（または **言語の設定方法**）。  
- `engine.Save(..., OcrOutputFormat.Json)` を呼び出して **PNG を JSON に変換**。

これが **OCR を実行する方法** の全体的なワークフローで、クリーンかつ保守しやすい形になっています。

## 次にやることは？

- **set OCR language** を使って多言語請求書（例：英語 | スペイン語）を試す。  
- 生の文字列だけが必要な場合は `OcrOutputFormat.Json` を `OcrOutputFormat.PlainText` に置き換える。  
- JSON 出力を Azure Function や AWS Lambda に統合し、サーバーレス処理を実現する。

例を自由に調整したり、エラーロギングを追加したり、再利用可能なサービスクラスにラップしたりしてください。Aspose.OCR で **OCR を実行する方法** の基本を習得すれば、可能性は無限です。

コーディングを楽しんで、テキスト抽出が常に正確でありますように！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [画像認識で JSON 結果を取得するための Aspose OCR の使用方法](/ocr/english/net/text-recognition/get-result-as-json/)
- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [.NET 用 Aspose.OCR で画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}