---
category: general
date: 2026-05-25
description: C#でAspose OCRを使用して画像からテキストを認識します。OCR用に画像を読み込む方法、OCR言語を設定する方法、OCRエンジンを作成する方法、そしてTIFFからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを認識します。このチュートリアルでは、OCRエンジンの作成、OCR用画像の読み込み、OCR言語の設定、そしてTIFFからテキストを抽出する方法を示します。
og_title: Aspose OCRで画像からテキストを認識する – 完全C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Aspose OCRで画像からテキストを認識する – 完全なC#ガイド
url: /ja/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCRで画像からテキストを認識する – 完全なC#ガイド

画像からテキストを**認識**したいけれど、速度と精度の両方を満たすライブラリがどれか分からないことはありませんか？請求書処理やアーカイブプロジェクトでは、TIFF ファイルからクリーンで検索可能なテキストを取得することが最大の課題です。

実は、Aspose OCR for .NET を使えば、その一連のパイプラインがとても簡単になります。このガイドでは、パッケージのインストール、**OCR エンジンの作成**、TIFF の読み込み、OCR 言語の設定、そして最終的に**TIFF からテキストを抽出**するまでの手順をすべて解説します。最後まで読めば、画像ファイルからテキストを瞬時に**認識**できるコンソールアプリが完成します。

## 前提条件

- .NET 6.0 以降（コードは .NET Core と .NET Framework でも動作します）
- Visual Studio 2022（またはお好みの IDE）
- Aspose.OCR NuGet パッケージ（GPU サポートには `Aspose.OCR.Gpu` アドオンが必要）
- 追加速度が欲しい場合は CUDA 対応 GPU（任意ですが推奨）

> **プロのコツ:** GPU が無い場合は `GpuDevice` 行を省略すれば、エンジンは自動的に CPU にフォールバックします。

## 手順 1: Aspose OCR のインストールと OCR エンジンの作成

まず、NuGet で必要なパッケージを追加します。

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

これで**OCR エンジンを作成**できます。このオブジェクトがプロセスの中心で、実行デバイスやメモリ制限などの設定を保持します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**重要ポイント:** エンジンを GPU にバインドすると、特に高解像度の TIFF を大量に処理する場合、**画像からテキストを認識**する時間が大幅に短縮されます。

## 手順 2: OCR 用に画像を読み込む

次に**OCR 用に画像を読み込む**必要があります。Aspose.OCR は `System.Drawing.Image` を使用するため、GDI+ がサポートする形式（マルチページ TIFF を含む）であれば問題ありません。

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

マルチページ TIFF を扱う場合は `image.SelectActiveFrame` でページをループできますが、ほとんどのシナリオでは単一呼び出しで十分です。

## 手順 3: OCR 言語を設定する

エンジンは自動で言語を判別しません。**OCR 言語を設定**してから認識を実行しないと、文字化けした出力が得られます。

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **豆知識:** 実行時に言語を切り替えるコストは低く、ページごとにこのプロパティを変更すれば混在言語の文書も処理できます。

## 手順 4: 認識を実行 – 画像からテキストを認識する

さあ、本番です。実際に**画像からテキストを認識**します。`Recognize` メソッドは検出された文字列をプレーンテキストで返します。

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

信頼度スコアやバウンディングボックスが必要な場合は、`OcrResult` オブジェクトを返すオーバーロードを使用できますが、ほとんどの抽出タスクではプレーン文字列で十分です。

## 手順 5: TIFF からテキストを抽出（マルチページファイルの処理）

ソースが複数ページの TIFF の場合、ステップ 2‑4 を各フレームで繰り返す必要があります。以下はページごとに**TIFF からテキストを抽出**する簡易ループです。

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

上記コードは各ページの抽出テキストを出力するので、結果をデータベースや検索インデックスにパイプするのがとても簡単です。

## 手順 6: 抽出テキストを表示または永続化する

最後に**抽出テキストを表示**し、必要に応じてファイルに書き出して後で処理できるようにします。

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

プログラムを実行すると、認識された文字がコンソールに表示され、ソース TIFF と同じディレクトリに `extracted_text.txt` が作成されます。

---

## よくある質問とエッジケース

- **GPU が検出されない場合は？**  
  `GpuDevice` 行を削除すれば、エンジンは自動的に CPU モードに切り替わります。速度は遅くなりますが、結果の精度は変わりません。

- **PNG や JPEG も処理できますか？**  
  もちろんです。`Image.FromFile` は System.Drawing がサポートするすべての形式に対応しているので、拡張子に関係なく**OCR 用に画像を読み込む**ことができます。

- **低解像度のスキャンはどう扱うべき？**  
  `ocrEngine.PreprocessOptions.Dpi` を `Recognize` 呼び出し前に上げてください。DPI を高くするとエンジンが利用できるピクセル数が増え、精度が向上します。

- **TIFF のサイズに上限はありますか？**  
  `GpuMemoryLimit` プロパティで GPU 使用量を制限できます。上限に達した場合、エンジンは残りのページを CPU にフォールバックします。

---

## 結論

これで、Aspose OCR を使って C# で**画像からテキストを認識**するための、実運用可能な完全コードが手に入りました。チュートリアルでは**OCR エンジンの作成**、**OCR 用に画像を読み込む**、**OCR 言語の設定**、そして**TIFF からテキストを抽出**する方法を解説し、GPU 加速による高速化も実現しました。

ここからは次のようなことに挑戦できます：

- 異なる言語 (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified` など) を試す
- 出力を検索可能な ElasticSearch インデックスに統合する
- 後処理（スペルチェック、正規表現によるクリーンアップ）を追加してデータ品質を向上させる

自分の請求書バッチで試してみて、メモリ制限を調整しながら OCR パフォーマンスの向上を体感してください。Happy coding!

## 関連チュートリアル

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}