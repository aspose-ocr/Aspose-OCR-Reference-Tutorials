---
category: general
date: 2026-11-26
description: Aspose.OCR を使用して PNG ファイルの OCR を実行し、PNG をテキストに変換し、キリル文字テキストを抽出する方法を学びましょう
  – 開発者向けのステップバイステップガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: ja
lastmod: 2026-11-26
og_description: C#でAspose.OCRを使用してPNGファイルのOCRを実行し、キリル文字テキストを抽出する方法。PNGをテキストに変換する完全なチュートリアルをご覧ください。
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Aspose.OCRでPNG画像のOCRを実行する方法 – C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: C#でAspose.OCRを使用してPNG画像のOCRを実行する方法
url: /ja/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG画像に対してAspose.OCRを使用したOCRの実行方法（C#）

PNGファイルに対して **OCRの実行方法** が必要な場合、本ガイドでは Aspose.OCR を使用して PNG をテキストに変換する正確な手順を示します。スキャンした文書からキリル文字テキストを抽出する場合でも、PNG スクリーンショットからテキストを認識するだけの場合でも、ソリューションはすぐに使用でき、C# の数行のコードだけで実行できます。

このチュートリアルで学べること:

* ローカルフォルダーから **OCR用に画像を読み込む** 方法
* エンジンを **キリル文字テキストを抽出** するように設定する方法
* **PNGからテキストを認識** し、クリーンな文字列を取得する方法
* 言語モジュールの欠如や大きな画像など、一般的な落とし穴への対処方法

Aspose.OCR の事前経験は不要です。必要なのは .NET 開発環境と、処理したい PNG 画像だけです。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* .NET 6.0（またはそれ以降）
* **Aspose.OCR for .NET** のライセンス版またはトライアル版。Aspose のウェブサイトから無料トライアルを取得できます。
* Visual Studio 2022（または .NET をサポートする任意の IDE）
* テキスト抽出対象の PNG ファイル（例では `sample_image.png` を使用）

## 手順 1: Aspose.OCR NuGet パッケージをインストール

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

このパッケージにはコア OCR エンジンとすべての言語モジュールが含まれます。ローカルに存在しない言語を要求した場合、Aspose.OCR が自動的に必要なモジュールをダウンロードします。

## 手順 2: OCR エンジン インスタンスを作成（OCRの実行方法）

OCR ワークフローの最初の実行可能ステップはエンジンのインスタンス化です。このオブジェクトは画像の読み込みや認識など、以降のすべての操作を管理します。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**重要ポイント:** `OcrEngine` クラスは OCR パイプラインをカプセル化します。単一インスタンスを作成し、複数画像で再利用することでメモリ使用量を削減し、パフォーマンスが向上します。

## 手順 3: OCR 用に画像を読み込む – ソース PNG ファイルを指定

画像の読み込みは **OCR用に画像を読み込む** 重要なポイントです。Aspose.OCR は複数の入力タイプを受け付けますが、最もシンプルなのは `ImageStream.FromFile` です。

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **プロのコツ:** 絶対パスまたは `Path.Combine` を使用して、環境が異なる場合でも実行時エラーを回避しましょう。

### 大きな画像の取り扱い

PNG が 2 MB を超える場合、認識前に縮小すると処理速度が向上します。

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## 手順 4: 言語を設定 – キリル文字テキストを抽出

デフォルトでは Aspose.OCR は英語を想定しています。**キリル文字テキストを抽出** するには、`Language` プロパティを `Language.Cyrillic` に設定します。必要なモジュールはコード実行時に自動的にダウンロードされます。

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

複数言語（例: 英語とキリル文字）を同時に認識したい場合は、次のように組み合わせられます。

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

#### エッジケース: 言語モジュールが見つからない

ダウンロードが失敗した場合（例: オフライン環境）、エンジンは `OcrException` をスローします。例外を捕捉して、優雅にフォールバックさせましょう。

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## 手順 5: 認識処理を実行（PNGからテキストを認識）

画像と使用言語が設定されたら、**PNGからテキストを認識** できます。`Recognize` メソッドは OCR パイプラインを同期的に実行します。

```csharp
// Run OCR
ocrEngine.Recognize();
```

**仕組み:** 内部的に Aspose.OCR は前処理（二値化、ノイズ除去）を行い、選択された言語に最適化されたニューラルネットワークベースの認識器に画像を渡します。

## 手順 6: 認識結果の取得と表示（PNGをテキストに変換）

認識が完了すると、抽出された文字列は `Text` プロパティから取得できます。これが **PNGをテキストに変換** の最終ステップです。

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### 期待される出力

`sample_image.png` にキリル文字フレーズ「Привет мир」が含まれている場合、コンソールは次のように表示します。

```
=== OCR Result ===
Привет мир
```

出力には画像に表示されている改行や句読点がそのまま含まれます。必要に応じて `String.Trim()`、`Regex`、その他のテキストクリーンアップユーティリティで後処理できます。

## 手順 7: オプション – 結果をファイルに保存

OCR 結果を保存すれば、インデックス作成や翻訳などの下流処理に利用できます。以下は UTF‑8 ファイルにテキストを書き込む簡単な方法です。

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## よくある落とし穴と回避策

| 問題 | 症状 | 対策 |
|------|------|------|
| **言語モジュールが欠如** | `Language = Language.Cyrillic` で `OcrException` が発生 | 初回実行時にインターネット接続を確保するか、Aspose のオフラインパッケージで事前にモジュールをダウンロード |
| **画像がぼやけている／コントラストが低い** | 精度低下、`?` が多数出力 | 前処理でコントラストを上げ、シャープ化、またはグレースケール変換を行ってからエンジンに渡す |
| **非常に大きな PNG** | 処理時間が長く、`OutOfMemoryException` が発生する可能性 | 手順 3 のように縮小するか、マルチページ画像をタイルに分割 |
| **非 UTF‑8 文字** | 出力が文字化け | コンソールやファイルライターが UTF‑8 エンコーディング (`Encoding.UTF8`) を使用していることを確認 |

## 完全な実行可能サンプル

以下は上記手順すべてを組み込んだ完全なプログラムです。新しいコンソールプロジェクトにコピーし、ファイルパスを調整した上で実行してください。

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### 動作概要

1. **エンジン作成** – OCR パイプラインを準備  
2. **画像読み込み** – パフォーマンス向上のため、必要に応じて縮小版 PNG をサポート  
3. **言語選択** – **キリル文字テキストを抽出** し、モジュール欠如時の例外処理を実装  
4. **認識** – コアの **PNGからテキストを認識** 呼び出し  
5. **結果処理** – **PNGをテキストに変換** し、コンソール出力とファイル保存を実演  

`dotnet run` でプログラムを実行します。正しく設定されていれば、認識されたテキストがコンソールに表示され、`ocr_output.txt` に保存されます。

## 結論

本チュートリアルでは、Aspose.OCR for .NET を使用して PNG ファイルに対して **OCRの実行方法** を学びました。**OCR用に画像を読み込む**、**キリル文字テキストを抽出**、**PNGをテキストに変換** までの標準的なワークフローと、一般的なエッジケースや実用的なヒントを網羅しました。

**次のステップ**

* `Language` フラグを組み合わせて、**PNGからテキストを認識** できる言語を追加（アラビア語、中国語など）  
* OCR 結果を Azure Cognitive Search と統合し、検索可能な文書アーカイブを構築  
* `OcrEngine` の `Resolution` などの設定を試して、認識精度や速度をカスタマイズ  

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自プロジェクトで試したりするのに役立ちます。

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}