---
category: general
date: 2026-09-22
description: C#でAspose.OCRを使用して画像からテキストを抽出します。画像をテキストに変換する方法、OCR用に画像を読み込む方法、そしてキリル文字を効率的に認識する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for OCR
- recognize text image
- recognize Cyrillic text
language: ja
lastmod: 2026-09-22
og_description: C# で Aspose.OCR を使用して画像からテキストを抽出します。このチュートリアルでは、画像をテキストに変換し、OCR 用に画像を読み込み、数行のコードでキリル文字テキストを認識する方法を示します。
og_image_alt: Diagram showing extract text from image workflow using Aspose.OCR
og_title: Aspose.OCRで画像からテキストを抽出する – ステップバイステップ C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  headline: How to extract text from image using Aspose.OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  name: How to extract text from image using Aspose.OCR in C#
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your solution folder and run:'
  - name: Create the OCR engine instance
    text: '```csharp using Aspose.OCR; using System.Drawing; // Required for Image
      handling'
  - name: Choose the language to recognize
    text: '```csharp // Step 3: Select Cyrillic as the target language engine.Language
      = OcrLanguage.Cyrillic; ```'
  - name: Load image for OCR
    text: '```csharp // Step 4: Load the image that contains the text engine.Image
      = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png"); ```'
  - name: Perform the recognition and get the result
    text: '```csharp // Step 5: Run the recognition process string recognizedText
      = engine.Recognize(); ```'
  - name: Output the extracted text
    text: '```csharp // Step 6: Display the extracted text Console.WriteLine("Recognized
      text:"); Console.WriteLine(recognizedText); ```'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image processing
title: C#でAspose.OCRを使用して画像からテキストを抽出する方法
url: /ja/net/text-recognition/how-to-extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.OCR を使用して画像からテキストを抽出する方法

.NET アプリケーションで **画像からテキストを抽出** したい場合、本ガイドは完全に実行可能なソリューションをステップバイステップで案内します。**画像をテキストに変換** する方法、OCR 用に画像を読み込む方法、そして追加設定なしでキリル文字を扱う方法が分かります。

このチュートリアルでは、必要な NuGet パッケージ、完全なコードサンプル、各手順の解説、よくある落とし穴への対策まで網羅しています。最後には数行のコードをプロジェクトに貼り付けるだけで、すぐにテキスト認識を開始できます。

## 必要な環境

開始する前に以下を用意してください。

- .NET 6.0 SDK 以降（.NET Framework 4.7+ でも動作します）
- Visual Studio 2022 または C# に対応した任意の IDE
- プロジェクトにインストール済みの Aspose.OCR NuGet パッケージ（`Aspose.OCR`）
- キリル文字を含むサンプル画像（例: `sample_cyrillic.png`）

> **プロのコツ:** バンドルされていない言語を初めて要求すると、Aspose.OCR が自動的に必要なモジュールをダウンロードします。この動作によりシームレスに **キリル文字を認識** できるようになります。

## Aspose.OCR で画像からテキストを抽出する

ソリューションの中心は `OcrEngine` の作成、言語設定、画像の読み込み、そして `Recognize()` の呼び出しです。以下のセクションで各手順を詳しく解説します。

### 手順 1: Aspose.OCR パッケージをインストール

ソリューションフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

このコマンドは Aspose.OCR の最新安定版をプロジェクトファイルに追加し、実行時に OCR エンジンと各言語モジュールが利用できるようにします。

### 手順 2: OCR エンジンのインスタンスを作成

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image handling

// ...

// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

`OcrEngine` はすべての OCR 操作のエントリーポイントです。インスタンス化することで画像解析に必要な内部リソースが確保されます。

### 手順 3: 認識する言語を選択

```csharp
// Step 3: Select Cyrillic as the target language
engine.Language = OcrLanguage.Cyrillic;
```

`engine.Language` に設定することで、Aspose.OCR が対象とする文字セットを指定します。**キリル文字を認識** すると、マシンにパックが存在しない場合は自動的にキリル語パックがダウンロードされます。

### 手順 4: OCR 用に画像を読み込む

```csharp
// Step 4: Load the image that contains the text
engine.Image = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png");
```

この行は `System.Drawing.Image` を使用して **画像を OCR 用に読み込み** ます。`YOUR_DIRECTORY` を実際の PNG または JPEG ファイルのパスに置き換えてください。エンジンは解析可能なビットマップを保持します。

### 手順 5: 認識を実行し結果を取得

```csharp
// Step 5: Run the recognition process
string recognizedText = engine.Recognize();
```

`Recognize()` はビットマップを走査し、言語固有のモデルを適用して抽出された文字列を返します。画像が鮮明で言語設定が正しければ、高精度な結果が得られます。

### 手順 6: 抽出したテキストを出力

```csharp
// Step 6: Display the extracted text
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

コンソールに結果を出力することで、**画像からテキストを抽出** が期待通りに動作することを確認できます。テキストをファイルやデータベースに書き込んだり、別の **サービス** に渡したりすることも可能です。

## 完全実行可能なサンプル

以下は上記手順をすべて含んだ単体プログラムです。新しいコンソールプロジェクト（`dotnet new console`）にコードを貼り付けて実行してください。

```csharp
using System;
using System.Drawing;          // Provides Image class
using Aspose.OCR;              // Aspose OCR namespace

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            OcrEngine engine = new OcrEngine();

            // Select the language – Cyrillic triggers module download if needed
            engine.Language = OcrLanguage.Cyrillic;

            // Load the image file (adjust the path to your environment)
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";
            engine.Image = Image.FromFile(imagePath);

            // Perform recognition
            string recognizedText = engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**期待される出力**

```
Recognized text:
Пример текста на кириллице
```

サンプル画像にフレーズ “Пример текста на кириллице” が含まれている場合、コンソールはそのまま表示します。フォントやサイズ、ノイズの違いにより精度が変わることがありますが、Aspose.OCR の組み込み前処理機能が多くのケースで対応します。

## 一般的なエッジケースの対処

| シナリオ | 対策 | 重要な理由 |
|----------|------|------------|
| 画像が見つからない | `Image.FromFile` を `try / catch (FileNotFoundException)` で囲み、分かりやすいメッセージを表示する | アプリケーションのクラッシュを防ぎ、ユーザーが正しいファイルを特定できるようにする |
| コントラストが低い画像 | `engine.ImagePreprocessingOptions` を `ImagePreprocessingOptions.Auto` に設定するか、認識前に明るさ/コントラストを手動調整する | 画像が薄い場合でも OCR の精度が向上する |
| 複数言語を認識したい | `engine.Language = OcrLanguage.Multilingual;` とし、必要に応じて `engine.AdditionalLanguages.Add(OcrLanguage.English);` を追加する | キリル文字とラテン文字が混在した文書など、混合スクリプトの検出が可能になる |
| 大量の画像をバッチ処理 | 1つの `OcrEngine` インスタンスを再利用し、ループ内で `engine.Recognize()` を呼び出す。処理後はエンジンを破棄する | メモリ割り当てを削減し、処理速度を向上させる |

## 信頼性の高い OCR のベストプラクティス

- **ロスレス画像形式**（PNG または TIFF）を可能な限り使用する。JPEG の圧縮は認識器を混乱させるアーティファクトを生むことがあります。
- **画像解像度は 300 dpi 以上** を推奨。印刷されたテキストの場合、解像度が低いと小さな文字が抜け落ちる可能性があります。
- **不要な余白はトリミング** してから読み込む。余分な空白は処理時間を増やすだけで価値を提供しません。
- **出力結果を検証** する。空文字列や予期しない文字がないかチェックし、特にノイズが多いスキャン文書では注意が必要です。

## 次のステップ

**画像からテキストを抽出** できるようになったので、以下のように機能を拡張してみてください。

- **大量画像の一括変換**: ディレクトリ内の画像を順に読み込み、各ファイルを処理して CSV に結果を書き出す。
- **クラウドストレージとの統合**: Azure Blob Storage や Amazon S3 から画像を取得し OCR を実行、抽出テキストをクラウドに保存する。
- **翻訳 API と組み合わせる**: キリル文字を認識した後、Azure Translator や Google Cloud Translation を呼び出して英語に翻訳する。
- **高度なレイアウト解析**: Aspose.OCR の `OcrPage` オブジェクトを利用してテキスト座標を取得し、PDF の再構築や検索可能ドキュメントの作成に活用する。

本チュートリアルの手順に従えば、**画像をテキストに変換** したり、**テキスト画像を認識** したりするあらゆるプロジェクトの堅実な基盤が手に入ります。

---


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image with Aspose OCR – C# Quickstart](/ocr/english/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}