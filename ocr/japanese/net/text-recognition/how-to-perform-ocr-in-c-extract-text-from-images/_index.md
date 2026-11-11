---
category: general
date: 2026-10-08
description: C# で Aspose.OCR を使用して画像ファイルからテキストを抽出する OCR の実行方法を学びます。このガイドでは、画像をテキストに変換し、JPEG
  からテキストを認識する方法を示します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: ja
lastmod: 2026-10-08
og_description: Aspose.OCR を使用した C# での OCR の実行方法。画像ファイルからテキストを抽出し、画像をテキストに変換し、JPEG
  からテキストを認識するステップバイステップのガイドをご覧ください。
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: C#でOCRを実行する方法 – 画像からテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: C#でOCRを実行する方法 – 画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を実行する方法 – 画像からテキストを抽出する

.NET アプリケーションで **OCR の実行方法** が必要な場合、このチュートリアルは完全に動作するソリューションを提供します。Aspose.OCR を使用すれば、**画像からテキストを抽出**、**画像をテキストに変換**、そして **JPEG からテキストを認識** するコードを数行書くだけで実現できます。

ライブラリのインストールから認識結果の出力までの全工程を示すので、例を自分のプロジェクトにコピーしてすぐに画像処理を開始できます。

## 学べること

* OCR タスク用に C# プロジェクトを設定する方法。  
* JPEG（またはサポートされている任意の画像）を読み込み、認識を実行する方法。  
* 取得したテキストをアプリケーションで利用する方法。  

前提条件は、最新の .NET SDK（≥ .NET 6）と、最初の言語モデルダウンロードのためのインターネット接続だけです。

## 手順 1: プロジェクトを作成し Aspose.OCR をインストール

1. 新しいコンソールプロジェクトを作成します：

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. Aspose.OCR NuGet パッケージを追加します：

   ```bash
   dotnet add package Aspose.OCR
   ```

   このパッケージには、**画像をテキストに変換**するために必要な OCR エンジン、言語モデル、画像処理ユーティリティが含まれています。

> **プロのコツ:** 複数の画像で OCR を実行する予定がある場合は、共有ライブラリにパッケージを追加して同じエンジンインスタンスを再利用できるようにすると便利です。

## 手順 2: C# OCR サンプルコードを書く

`Program.cs` を作成または置き換えて、以下のコードを貼り付けます。これは Aspose.OCR がサポートする任意の画像形式（JPEG、PNG、BMP など）で動作する **C# OCR サンプル** です。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### 各行の意味

* **`OcrEngine ocrEngine = new OcrEngine();`** – OCR パイプライン全体を統括するエンジンをインスタンス化します。  
* **`ocrEngine.Language = Language.Cyrillic;`** – 言語モデルを選択します。正しい言語を指定することで、**画像からテキストを抽出**する際の非ラテン文字の認識精度が大幅に向上します。  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – ソース JPEG（または他のサポート画像）を読み込みます。このステップは **JPEG からテキストを認識** するために必須です。  
* **`ocrEngine.Recognize();`** – コア OCR アルゴリズムを実行します。エンジンが処理を完了するまでメソッドはブロックされます。  
* **`ocrEngine.Text;`** – プレーンテキストの結果を取得します。取得したテキストは、以降の **画像をテキストに変換** ロジックで使用できます。

## 手順 3: プログラムを実行し出力を確認

コンパイルして実行します：

```bash
dotnet run
```

画像 `sample_cyrillic.jpg` にキリル文字のフレーズ “Привет мир” が含まれている場合、コンソールには次のように表示されます：

```
=== Recognized Text ===
Привет мир
```

この出力は、**OCR の実行方法** と **画像からテキストを抽出** できたことを示しています。

## 手順 4: よくあるバリエーションとエッジケース

### 4.1 英語または多言語テキストの認識

言語割り当てを適切な enum に置き換えます：

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 ファイルではなくストリームから画像を処理する

画像が HTTP 応答やデータベース BLOB として取得される場合は、`MemoryStream` を使用します：

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 大きな画像や低解像度画像の取り扱い

大きな画像はメモリ使用量が増加します。OCR 前にダウンサンプリングすると効果的です：

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 エラーハンドリング

認識呼び出しを try‑catch ブロックでラップし、ネットワークやファイルアクセスエラーを捕捉します：

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## 手順 5: 次のステップ – OCR ワークフローの拡張

* **バッチ処理:** ディレクトリ内のファイルをループし、各 JPEG に対して **画像をテキストに変換** します。  
* **ポストプロセッシング:** 正規表現を適用して認識文字列をクリーンアップ。フォームや請求書の **画像からテキストを抽出** する際に便利です。  
* **Azure Cognitive Services との統合:** 複雑なレイアウトに対しては、クラウドベース OCR と Aspose.OCR の結果を比較して精度を向上させます。  
* **結果の保存:** 抽出したテキストを SQL データベースや ElasticSearch インデックスに格納し、検索可能なドキュメントとして活用します。

---

## 結論

Aspose.OCR を使って C# で **OCR の実行方法** をインストールから認識文字列の表示までマスターしました。この完全な **C# OCR サンプル** により、数行のコードで **画像からテキストを抽出**、**画像をテキストに変換**、そして **JPEG からテキストを認識** できるようになります。さまざまな言語モデル、画像ソース、ポストプロセッシング手法を試して、特定のユースケースに合わせて最適化してください。

---


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Use OCR in C# – Extract Text from Image Files](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Perform OCR in C# – Extract Text and Write JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}