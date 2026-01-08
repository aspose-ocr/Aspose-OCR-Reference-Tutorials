---
category: general
date: 2026-01-07
description: C#でAspose OCRを使用して画像からテキストを抽出します。写真からテキストを認識する方法、OCR精度を向上させる方法、OCR用に画像を読み込む方法、OCR言語を設定する方法を学びましょう。
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出します。このガイドでは、写真からテキストを認識する方法、OCR の精度を向上させる方法、OCR
  用に画像を読み込む方法、OCR 言語を設定する方法を示します。
og_title: Aspose OCRで画像からテキストを抽出 – C#チュートリアル
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCRで画像からテキストを抽出する – 完全C#ガイド
url: /ja/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – Aspose OCR を使用した完全な C# 実装

画像からテキストを**抽出**したいと思ったことはありませんか？どのライブラリが信頼できる結果を提供するか分からないこともあるでしょう。実際のアプリケーション—レシートスキャナー、ID 検証、あるいは簡単なメモ取りツール—では、**写真からテキストを認識**できることが必須機能です。

このチュートリアルでは、**OCR 用に画像をロード**し、エンジンに**OCR 言語を設定**し、**OCR 精度を向上**させるいくつかの前処理テクニックを適用する、完全に実行可能なサンプルを順を追って解説します。最後まで実行すれば、抽出されたテキストをコンソールに出力する単一の C# ファイルが手に入り、各設定がなぜ重要なのかが理解できるようになります。

> **Tip:** このコードは Aspose.OCR ≥ 23.5、.NET 6+、および .NET Core を実行できる Windows、Linux、macOS 環境で動作します。

## 前提条件

- .NET 6 SDK（またはそれ以降）をインストール済み  
- Visual Studio 2022、VS Code、またはお好みのエディタ  
- NuGet パッケージ `Aspose.OCR`（`dotnet add package Aspose.OCR` でインストール）  
- 明瞭な印刷またはタイプされたテキストを含む画像ファイル（JPEG/PNG）  

これらが揃ったら、さっそく始めましょう。

![画像からテキストを抽出する例](/images/ocr-example.png "画像からテキスト抽出 – Aspose OCR 出力")

## 手順 1: OCR エンジンの作成と破棄 – 「画像からテキストを抽出」コア

最初に必要なのは `OcrEngine` のインスタンスです。`using` ブロックでラップすることで、ネイティブリソースの適切な破棄が保証されます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**なぜ重要か:** `OcrEngine` はネイティブ OCR DLL のアンマネージド メモリを保持します。速やかに破棄することで、特にバッチで多数の画像を処理する際のメモリリークを防げます。

## 手順 2: 認識設定の定義 – OCR 精度の向上

次に `RecognitionSettings` オブジェクトを作成します。ここで **OCR 言語を設定**し、文字化けした文字列ときれいな出力の差を生む前処理フィルタを追加します。

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**なぜこれらのフィルタか:**  
- **Deskew** は、スマートフォンで撮影した写真が数度ずれているという一般的な問題を修正します。  
- **Denoise** は、文字として誤認識される可能性のある斑点を除去します。  
- **ContrastEnhance** は薄いインクを際立たせ、**OCR 精度の向上**に不可欠です。

## 手順 3: 画像の読み込み – OCR 用画像の効率的なロード

Aspose は `ImageStream.FromFile` を提供しており、迅速にロードできます。画像が Web リクエストやデータベースから来る場合は `MemoryStream` を使用することも可能です。

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**一般的な落とし穴:** Windows でスラッシュ区切りのパスを指定しても動作しますが、クロスプラットフォームプロジェクトでは `Path.Combine` を使用する方が安全です。

## 手順 4: 認識の実行 – 写真からテキストを認識

ここで `Recognize` を呼び出し、画像ストリームと設定の両方を渡します。メソッドは抽出されたテキストを含むプレーン文字列を返します。

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

画像に複数のテキストブロックが含まれる場合、Aspose は可能な限り元のレイアウトを保持しつつ改行で結合します。

## 手順 5: 結果の出力 – 抽出結果の検証

最後に結果をコンソールに書き出します。実際のアプリケーションではデータベースに保存したり、別サービスへ送信したり、UI に表示したりすることが考えられます。

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### 期待されるコンソール出力

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

文字化けした文字が表示された場合は、画像が鮮明か、言語がテキストに合っているか、前処理フィルタが適切かを再確認してください。

## 手順 6: オプションの調整 – エッジケース向けの微調整

### a. 言語の切替え

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. カスタムフィルタの追加

Aspose には `PreprocessFilter.Sharpen` や `PreprocessFilter.Binarize` も用意されています。デフォルトの 3 つのフィルタで足りない場合は、これらを試してみてください。

### c. 大きな画像の処理

非常に高解像度の写真の場合は、メモリ使用量を抑えるために先に縮小してください。

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## よくある質問

**Q: 手書きメモでも動作しますか？**  
A: Aspose OCR は印刷テキスト向けに調整されています。手書き認識には別のエンジン（例: Aspose.OCR for Handwriting や機械学習モデル）が必要です。

**Q: ループ内で複数画像を処理できますか？**  
A: もちろん可能です。`using (var ocrEngine = new OcrEngine())` ブロックをループの外に出し、エンジンを再利用すればパフォーマンスが向上します。

**Q: 画像が PDF ページだった場合は？**  
A: まず PDF ページを画像に変換します（Aspose.PDF でページを PNG/JPEG にレンダリング可能）。その後 OCR エンジンに渡してください。

## まとめ – 達成したこと

- **画像からテキストを抽出**する単一の自己完結型 C# プログラムを作成しました。  
- 前処理を組み合わせて **OCR 精度を向上**させながら、**写真からテキストを認識**する方法を実演しました。  
- 多言語シナリオに対応するための **OCR 用画像のロード** と **OCR 言語の設定** の正しい手順を示しました。  

## 次のステップと関連トピック

- **バッチ処理:** このスニペットを `Directory.GetFiles` と組み合わせて、フォルダー全体を OCR できます。  
- **後処理:** 正規表現を使って抽出後に日付、金額、ID などをクリーンアップします。  
- **統合:** 抽出したテキストを Azure Cognitive Search や Elastic に流し込み、検索可能なドキュメントを作成します。  

さまざまなフィルタ組み合わせ、言語、画像ソースで自由に実験してみてください。基本パターンは変わりません：エンジンを作成し、設定を構成し、画像をロードし、認識し、結果を出力する。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}