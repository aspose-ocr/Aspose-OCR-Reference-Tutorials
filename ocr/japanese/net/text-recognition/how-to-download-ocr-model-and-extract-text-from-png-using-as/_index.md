---
category: general
date: 2026-09-16
description: OCRモデルをダウンロードし、Aspose.OCRでPNGからテキストを抽出します。画像をテキストに変換し、C#で画像からテキストを読み取る方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR model
- extract text from PNG
- convert image to text
- recognize text from image
- read text from image
language: ja
lastmod: 2026-09-16
og_description: C#でOCRモデルをダウンロードし、PNGからテキストを抽出します。このステップバイステップのチュートリアルでは、画像をテキストに変換し、Aspose.OCRを使用して画像からテキストを読み取る方法を示します。
og_image_alt: Diagram showing OCR engine loading a model, processing a PNG, and outputting
  recognized text
og_title: Aspose.OCRでOCRモデルをダウンロードし、PNGからテキストを抽出する – C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: download OCR model and extract text from PNG with Aspose.OCR. Learn
    to convert image to text and read text from image in C#.
  headline: How to download OCR model and extract text from PNG using Aspose.OCR in
    C#
  type: TechArticle
tags:
- OCR
- Aspose.OCR
- C#
- image-processing
title: C#でAspose.OCRを使用してOCRモデルをダウンロードし、PNGからテキストを抽出する方法
url: /ja/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用して C# で OCR モデルをダウンロードし、PNG からテキストを抽出する方法

## 必要なもの

| 前提条件 | 理由 |
|--------------|--------|
| .NET 6.0 SDK またはそれ以降 | コンソール アプリのランタイムを提供します |
| Visual Studio 2022（または任意の IDE） | 編集とデバッグが簡単になります |
| Aspose.OCR for .NET NuGet パッケージ | OCR エンジンと語彙モデルを提供します |
| テキストを含む画像ファイル（`input.png`） | **画像をテキストに変換** する元となるファイルです |

NuGet コンソールから Aspose.OCR パッケージを追加できます:

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** `Language` プロパティを初めて設定すると、Aspose.OCR は自動的に OCR モデル ファイルをユーザーのローカルキャッシュに **ダウンロード** します。手動でダウンロードする必要はありません。

## Aspose.OCR 用の OCR モデルをダウンロードする方法

OCR エンジンはライブラリを軽量に保つため、言語データを同梱していません。言語（例: Cyrillic）を割り当てると、SDK はキャッシュを確認し、モデルが存在しない場合は Aspose の CDN からダウンロードします。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;   // contains Language enum
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Select the required language model.
        // This triggers a download if the model is not present locally.
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic is ready.");
```

`Console.WriteLine` は **OCR モデルのダウンロード** 手順が正常に完了したことを確認します。ダウンロードはマシンごとに一度だけ行われ、その後はキャッシュされたモデルが再利用されます。

### 自動ダウンロードが重要な理由

* **バンドルサイズの削減** – 言語パックは必要に応じて取得されるため、アプリケーションは小さく保たれます。  
* **常に最新の精度** – Aspose はモデルを定期的に更新し、常に最新バージョンが取得されます。  
* **デプロイの簡素化** – 大きな `.dat` ファイルをインストーラに同梱する必要はありません。

## C# で PNG からテキストを抽出する方法

言語モデルが準備できたら、次は処理したい PNG ファイルを読み込みます。PNG はロスレス形式で、文字エッジの品質が保たれ、認識精度が向上します。

```csharp
        // Step 3: Load the image that contains the text.
        // ImageStream.FromFile reads the file into a stream compatible with Aspose.OCR.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("Image loaded successfully.");
```

> **エッジケース:** PNG がインデックスカラー パレットを使用している場合、OCR エンジンに渡す前に 24 ビット RGB に変換して誤認識を防いでください。

## 画像をテキストに変換: 画像からテキストを認識する

いよいよ OCR プロセスを実行します。`Recognize` メソッドが前処理、セグメンテーション、文字分類、後処理といった重い処理をすべて行います。

```csharp
        // Step 4: Run the OCR process.
        // Recognize returns an OcrResult object that holds the recognized text and confidence scores.
        OcrResult result = ocrEngine.Recognize();

        // Verify that the engine actually found text.
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text was recognized. Check image quality or language settings.");
            return;
        }
```

`result` オブジェクトには生の文字列だけでなく、`ResultPage`（マルチページ画像用）や `Confidence`（全体の信頼度スコア）といったオプションプロパティも含まれます。これらは高度な検証や UI フィードバックに利用できます。

## 画像からテキストを読み取り、結果を処理する

最後に認識された文字列を表示または保存します。これが **画像からテキストを読み取る** 手順で、変換パイプラインが完了します。

```csharp
        // Step 5: Retrieve and display the recognized text.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Optional: Write the output to a .txt file for later processing.
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Text saved to output.txt");
    }
}
```

**期待される出力**（「Hello World」を含むシンプルな画像の例）:

```
=== Recognized Text ===
Hello World
Text saved to output.txt
```

### 一般的なバリエーション

| バリエーション | 使用タイミング | コードの調整 |
|-----------|-------------|------------|
| **English language** | ほとんどの西洋文書 | `ocrEngine.Language = Language.English;` |
| **Multiple languages** | 混在言語ページ | `ocrEngine.Language = Language.English | Language.Russian;` |
| **Custom DPI scaling** | 低解像度スキャン | `ocrEngine.Image = ImageStream.FromFile(...).Resize(2.0);` |
| **PDF input** | ソースが PDF ページの場合 | PDF を画像に変換してからビットマップを `ocrEngine.Image` に渡します。 |

## 完全な実行可能サンプル

以下はコピー＆ペーストして実行できる完全なプログラムです。`YOUR_DIRECTORY` を `input.png` が格納されているパスに置き換えてください。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;
using System;

class Program
{
    static void Main()
    {
        // Create OCR engine instance (downloads model if needed)
        var ocrEngine = new OcrEngine();

        // Choose language – this triggers the automatic model download
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic downloaded (if not cached).");

        // Load the PNG image containing the text
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("PNG image loaded.");

        // Perform OCR
        OcrResult result = ocrEngine.Recognize();

        // Validate result
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text recognized. Verify image quality or language settings.");
            return;
        }

        // Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Save to a file for further processing
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Recognized text saved to output.txt");
    }
}
```

プログラムは次のコマンドで実行します:

```bash
dotnet run
```

すべて正しく設定されていれば、コンソールに `input.png` から抽出されたテキストが表示され、`output.txt` に書き込まれます。

## ベストプラクティスとトラブルシューティング

* **画像品質** – 少なくとも 300 dpi を目指してください。ぼやけた画像やノイズの多い画像は信頼度スコアを下げます。  
* **言語選択** – 常にソーステキストの言語と一致させてください。言語が合わないと文字化けが発生します。  
* **キャッシュ場所** – デフォルトでは Aspose はモデルを `%USERPROFILE%\.Aspose\Aspose.OCR` に保存します。新しいダウンロードを強制したい場合のみフォルダーをクリアしてください。  
* **パフォーマンス** – バッチ処理の場合、画像ごとに新しいインスタンスを作成するのではなく、単一の `OcrEngine` インスタンスを再利用してください。  
* **エラーハンドリング** – モデルダウンロード中のネットワークエラーを捕捉するため、OCR 呼び出しを try‑catch ブロックでラップしてください。

## 結論

これで Aspose.OCR を使用して C# で **OCR モデルをダウンロード**、**PNG からテキストを抽出**、**画像をテキストに変換**、**画像からテキストを認識**、そして **画像からテキストを読み取る** 方法が分かりました。完全なサンプルは、PDF 変換やマルチページ処理、下流のテキスト分析パイプラインへの統合など、実運用向けのフローを示しています。

### 次のステップ

* **手書き文字認識** を試すには `Language.EnglishHandwritten` に切り替えてください。  
* OCR を **Aspose.PDF** と組み合わせて、抽出したテキストを検索可能な PDF に埋め込みます。  
* **画像前処理**（デスキュー、コントラスト強化）を試して、低品質スキャンの精度を向上させます。

コードを自由に自分のプロジェクトに合わせて調整し、楽しいコーディングを！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自の実装アプローチを探求したりするのに役立ちます。

- [C# で画像からテキストを抽出 – Aspose を使用したオフライン OCR（ステップバイステップガイド）](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [.NET 用 Aspose.OCR で画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}