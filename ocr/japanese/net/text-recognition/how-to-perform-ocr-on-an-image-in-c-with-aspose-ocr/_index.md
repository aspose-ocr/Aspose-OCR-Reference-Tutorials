---
category: general
date: 2026-10-21
description: Aspose.OCR を使用して C# で JPG の OCR を実行し、画像からテキストを抽出し、OCR 用に画像を読み込む方法を学びます。ステップバイステップの完全ガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: ja
lastmod: 2026-10-21
og_description: C# と Aspose.OCR を使用して画像の OCR を実行する方法。このガイドに従って OCR 用に画像を読み込み、JPG からテキストを認識し、画像からテキストを抽出します。
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: C#で画像にOCRを実行する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: C# と Aspose.OCR を使用して画像の OCR を実行する方法
url: /ja/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.OCR で画像の OCR を実行する方法

画像で **how to perform OCR** が必要な場合、このチュートリアルでは完全な実行可能なソリューションを示します。OCR 用に画像をロードする方法、JPG ファイルからテキストを認識する方法、そして Aspose.OCR ライブラリを使用して画像からテキストを抽出する方法を学びます。

このガイドでは、NuGet パッケージのインストールから言語モデルの取り扱い、認識結果の出力までを網羅しています。最後まで読むと、OCR を任意の .NET プロジェクトに統合し、IDE を離れることなくキリル文字やその他の言語テキストを処理できるようになります。

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- Visual Studio 2022（または任意の C# エディタ）
- 初回実行時のインターネット接続（Aspose.OCR が言語モデルを自動的にダウンロードします）
- サンプル画像（例: `cyrillic_sample.jpg`）をコードから参照できるフォルダーに配置

## 手順 1: Aspose.OCR のインストール

NuGet パッケージ マネージャーを開き、プロジェクトに **Aspose.OCR** を追加します。

```bash
dotnet add package Aspose.OCR
```

このパッケージには OCR エンジン、言語モデル、画像処理に必要なヘルパークラスが含まれています。追加の DLL は不要です。

## 手順 2: OCR エンジンの作成 – how to perform OCR

**how to perform OCR** の最初の実際のタスクはエンジンのインスタンス化です。このオブジェクトは認識パイプライン全体を管理します。

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` は軽量で、�数の画像に対して同じインスタンスを再利用できるため、バッチ処理時のパフォーマンスが向上します。

## 手順 3: OCR 用に画像をロード

認識を行う前に画像データを提供する必要があります。**load image for OCR** ステップは多数のフォーマットに対応していますが、ここでは JPEG ファイルに焦点を当てます。

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` はファイルをメモリに読み込み、エンジン用に準備します。ファイルパスが無効な場合は `ArgumentException` がスローされるので、パスが正しいことを確認してください。

## 手順 4: 適切な言語を選択（任意だが推奨）

画像にキリル文字が含まれる場合、言語を `Cyrillic` に設定します。必要なモデルは初回実行時に自動的にダウンロードされます。

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

このプロパティを変更することで他の言語（例: `OcrLanguage.English`）に切り替えることができます。このライブラリは 60 以上の言語をサポートしています。

## 手順 5: JPG からテキストを認識 – how to perform OCR on a JPEG

次に `Recognize` メソッドを呼び出します。これは **how to perform OCR** の核心であり、ビットマップを Unicode テキストに変換します。

```csharp
// Perform the recognition
engine.Recognize();
```

このメソッドは OCR プロセスが完了するまでブロックします。大きな画像の場合、UI の応答性を保つためにバックグラウンド スレッドで実行すると良いでしょう。

## 手順 6: 画像からテキストを抽出

認識後、エンジンは結果を `Text` プロパティに格納します。これで **extract text from image** ステップが完了します。

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

出力には画像内で検出された正確な文字が含まれ、改行や句読点も保持されます。

## 完全な実行可能サンプル

すべての手順を組み合わせると、コピーして貼り付けて実行できる単一のプログラムが得られます。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### 期待される出力

`cyrillic_sample.jpg` にフレーズ “Привет мир”（Hello world）が含まれている場合、コンソールに次のように表示されます。

```
=== OCR Result ===
Привет мир
```

フォントや画像品質の違いにより精度が変わることがありますが、Aspose.OCR は一般的に鮮明な印刷物で 95 % 以上の認識率を達成します。

## よくある落とし穴と実用的なヒント

- **Image quality matters** – 低解像度またはノイズの多い JPEG は精度を低下させます。必要に応じて `engine.Image.AdjustContrast()` で画像を前処理（例: コントラストを上げる）してください。
- **Language model download** – 初回実行時にモデルが `%USERPROFILE%\.Aspose\OCR` にダウンロードされます。プロセスに書き込み権限があることを確認してください。
- **Batch processing** – 同じ `OcrEngine` インスタンスを再利用し、ファイル間で `engine.Image` のみを変更します。これによりモデルの再読み込みを防げます。
- **Memory usage** – 大きな画像はより多くの RAM を消費します。ループで多数のファイルを処理する場合は、各認識後に `engine.Image.Dispose()` を呼び出してください。
- **Thread safety** – `OcrEngine` はスレッドセーフではありません。並列処理する際はスレッドごとに別々のインスタンスを作成してください。

## 結論

これで、C# で Aspose.OCR を使用して JPEG に対して **how to perform OCR**、**load image for OCR**、そして **extract text from image** を行う方法が分かりました。完全なソリューションは言語設定、JPG からのテキスト認識、結果の出力を示しており、あらゆるテキスト抽出プロジェクトの確固たる基盤となります。

次に、**perform OCR on image** バッチ処理、OCR を ASP.NET Core API と統合する方法、抽出したテキストを検索可能な PDF に変換する方法など、関連トピックを探求してください。さまざまな言語や画像前処理を試して、認識品質を最大化しましょう。

## 次に学ぶべきことは？

以下のチュートリアルは本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [How to Perform OCR in C# – Convert Image to Text with Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [How to Perform OCR in C# – Recognize Text from Image](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}