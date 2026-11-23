---
category: general
date: 2026-10-18
description: C#で画像のOCRを高速に実行します。JPGからテキストを抽出し、画像をテキストに変換し、Aspose.OCRを使用して画像からテキストを読み取る方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: ja
lastmod: 2026-10-18
og_description: C# と Aspose.OCR を使用して画像の OCR を実行します。このチュートリアルでは、JPG からテキストを抽出し、画像をテキストに変換し、数分で画像からテキストを読み取る方法を示します。
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: C#で画像のOCRを実行する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Aspose.OCR を使用して C# で画像に OCR を実行する方法
url: /ja/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.OCR で画像の OCR を実行する方法

.NET アプリケーションで **画像の OCR を実行** する必要がある場合、このガイドでは完全で実行可能なソリューションを示します。**OCR 用に画像をロード** する方法、キリル文字の認識、そして **JPG からテキストを抽出** する方法を、低レベルの画像処理コードを書かずに学べます。

このチュートリアルで行うこと:

* Aspose.OCR NuGet パッケージをインストールします。  
* 画像ファイル (JPG、PNG、BMP など) をロードします。  
* OCR エンジンを実行して **画像をテキストに変換** します。  
* コンソールに出力された **画像からテキストを読み取る**。

この手順は任意の .NET 対応画像で動作するため、PDF、スキャンした領収書、スクリーンショットなどにも応用できます。

## Prerequisites

* .NET 6.0 SDK 以降 (コードは .NET Framework 4.7+ でも動作します)。  
* Visual Studio 2022 またはお好みの C# エディタ。  
* 初回実行時にインターネット接続が必要です – Aspose.OCR はキリル文字言語モジュールを自動的にダウンロードします。  

> **プロのコツ:** NuGet パッケージは常に最新に保ちましょう。新しいバージョンは認識精度を向上させ、言語パックを追加します。

## Step 1: Install Aspose.OCR

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します:

```bash
dotnet add package Aspose.OCR
```

このパッケージには **画像の OCR を実行** するために使用される `OcrEngine` クラスが含まれています。コマンドが完了すると、パッケージ参照が *.csproj* ファイルに追加されます。

## Step 2: Create a console program skeleton

まだコンソールプロジェクトがない場合は新規作成します:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

生成された *Program.cs* を次のセクションで示すコードに置き換えてください。スケルトンには必要な `using` ディレクティブと OCR プロセスを駆動する `Main` メソッドが含まれています。

## Step 3: Load image for OCR

最初の機能行は **画像をロード** します。Aspose.OCR は任意のストリームを受け付けるため、ディスク上のファイル、Web URL、または埋め込みリソースからロードできます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Why this matters*: `ImageStream.FromFile` を使用するとフォーマット処理が抽象化され、元のファイルタイプに関係なく OCR エンジンが一貫したビットマップを受け取ります。また、`using` 文のおかげでストリームは自動的に破棄されます。

## Step 4: Initialize the OCR engine and set language (optional)

デフォルトでは Aspose.OCR が言語を自動検出します。キリル文字の場合は `Language.Cyrillic` モジュールを明示的に指定すると、初回ダウンロードが高速化されます。

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

言語の割り当てを省略すると、`Recognize` を初めて呼び出したときに必要なモジュールがダウンロードされます。ダウンロードは HTTPS 経由で行われ、以降の実行ではローカルにキャッシュされます。

## Step 5: Perform OCR and convert image to text

ここで実際に **画像の OCR を実行** し、プレーンテキスト文字列を取得します。`Recognize` メソッドが前処理、レイアウト解析、文字分類のすべてを行います。

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

返される `recognizedText` には元のレイアウトに合わせた改行が含まれるため、後処理やデータベースへの保存が容易です。

## Step 6: Display the result – read text from image

最後に、結果をコンソールに書き出すことで **画像からテキストを読み取る** を実行します。このステップで OCR が成功したことを確認し、抽出された内容を正確に確認できます。

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

プログラムを実行すると (`dotnet run`)、以下のような出力が表示されます:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Note:** 正確な出力は元の JPG の品質に依存します。鮮明で高解像度の画像ほど優れた結果が得られます。

## Full, runnable source code

以下は *Program.cs* にコピー＆ペーストして、画像パスを除いてそのまま実行できる完全なプログラムです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

プログラムを実行すると抽出された文字がコンソールに表示され、**JPG からテキストを抽出** し、**画像をテキストに変換** できたことが証明されます。

## Handling common variations

| Scenario | Adjustment |
|----------|------------|
| **Different language** | `engine.Language = Language.English;` など、サポートされている列挙体を設定します。 |
| **Multi‑page PDF** | 各ページを画像に変換 (例: `Aspose.PDF` を使用) し、各画像に対して OCR ループを呼び出します。 |
| **Large batch** | OCR 呼び出しを `Parallel.ForEach` ループでラップし、`OcrEngine` インスタンスを単一で再利用してメモリ使用量を削減します。 |
| **Low‑resolution image** | 認識前に `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` でノイズを低減する前処理を行います。 |

これらのバリエーションにより、任意の言語・サイズ・品質の **JPG からテキストを抽出** できるようになります。

## Performance tips

* **言語モジュールをキャッシュ** – 最初のダウンロードには数秒かかることがありますが、以降の実行は瞬時です。 |
* **`OcrEngine` インスタンスを再利用** して複数の画像を処理し、初期化コストの繰り返しを防ぎます。 |
* **画像サイズを制限** – 非常に大きな写真はメモリ使用量が増加します。エンジンに渡す前に幅を最大 2000 px にリサイズしてください。 |

## Conclusion

これで C# と Aspose.OCR を使用して **画像の OCR を実行** する方法が分かりました。画像をロードし、エンジンを構成し、`Recognize` を呼び出すだけで、**JPG からテキストを抽出**、**画像をテキストに変換**、そして **画像からテキストを読み取る** が数行のコードで実現できます。

次に取り組むべきこと:

* OCR 結果をデータベースに保存し、検索可能なアーカイブを作成する。  
* アップロードされた画像を受け取る Web API にワークフローを統合する。  
* 他の言語モジュール (Arabic、Hindi など) を使用してアプリケーションの対応範囲を拡大する。

さまざまな画像形式、言語、バッチ処理戦略で自由に実験してみてください。コアパターン—**OCR 用に画像をロード → 認識 → プレーンテキスト出力を処理**—は変わらないので、テキスト抽出プロジェクトの堅実な基盤となります。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれ、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像をテキストに変換 – URL から画像の OCR を実行](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [.NET 用 Aspose.OCR で画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}