---
category: general
date: 2026-05-25
description: C#でOCRを使用して画像ファイルからテキストを抽出する方法。Aspose.OCRを使ってJPGから中国語文字を認識する簡単な手順をご紹介します。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: ja
og_description: C#でOCRを使用して画像ファイルからテキストを抽出する方法。このガイドでは、Aspose.OCRを使ってJPGから中国語文字を認識する手順を示します。
og_title: C#でOCRを使用する方法 – JPGから中国語テキストを認識する
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でOCRを使用する方法 – JPGから中国語テキストを認識する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – JPG から中国語テキストを認識する

スマートフォンで撮影した画像から文字を取り出す **how to use OCR** について考えたことはありませんか？ あなたは一人ではありません。レシートスキャナー、翻訳アプリ、または自動データ入力など、実際のプロジェクトでは **extract text from image** ファイルを迅速かつ確実に取得する必要があります。

このチュートリアルでは、**recognizes text from JPG** ファイルを認識し、さらに **recognize Chinese characters** の難しいケースを **OCR Chinese Simplified** 言語パックを使用して処理する、完全で実行可能な例を順に解説します。最後まで実行すれば、検出された文字列をコンソールに出力する自己完結型のコンソールアプリが手に入り、追加の手動ダウンロードは不要です。

> **Quick note:** このコードは Aspose.OCR ≥ 23.7 で動作し、初回使用時に言語リソースを自動的に取得します。古いバージョンを使用している場合は、言語を手動で追加する必要があります。

## 前提条件

始める前に、以下が揃っていることを確認してください：

- .NET 6.0 SDK 以降（この例は .NET 6 を対象としていますが、.NET 5 でも動作します）
- Visual Studio 2022 または C# 拡張機能がインストールされた VS Code の最新バージョン
- 最初の言語ダウンロードのためのインターネット接続
- 簡体字中国語テキストを含む JPG 画像（ここでは `chinese_sign.jpg` と呼びます）

以上です—重厚な OCR エンジンやネイティブ DLL の操作は不要です。NuGet コマンドを数回実行し、数行のコードを書くだけです。

## 手順 1: NuGet で Aspose.OCR をインストールする

まず最初に、OCR ライブラリが必要です。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の UI が好きな場合は、**Dependencies → Manage NuGet Packages** を右クリックし、“Aspose.OCR” を検索して **Install** をクリックします。

> **Pro tip:** パッケージは常に最新の状態に保ちましょう。新しい言語パックやパフォーマンス向上がマイナーバージョンごとに追加されます。

## 手順 2: 新しいコンソールプロジェクトを作成する（まだ作成していない場合）

ゼロから始める場合は、新しいコンソールアプリを作成します：

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

これで OCR コードを記述できる `Program.cs` ファイルが用意できました。

## 手順 3: OCR コードを書く – JPG から簡体字中国語を認識する

`Program.cs` を開き、内容を以下に置き換えます。各行に注釈が付いているので、*何を* しているかだけでなく、*なぜ* それを行うのかが分かります。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 背後で何が起きているか？

- **`OcrEngine.Language`** は Aspose にどの辞書を使用するかを指示します。`ChineseSimplified` を選択することで、エンジンは簡体字中国語の言語パックを使用するよう指示します。
- **First‑time download**: `Recognize` が実行されると、SDK は Aspose の CDN にアクセスし、約 6 MB の言語ファイルを取得してローカルにキャッシュし、その後 OCR を実行します。以降の呼び出しは瞬時に完了します。
- **`Image.FromFile`** は .NET がデコードできる任意のラスタ形式（JPG、PNG、BMP など）で動作するため、**extract text from image** ファイルを多数のタイプから取得できます。JPG に限りません。

## 手順 4: アプリケーションを実行し、出力を確認する

ビルドして実行します：

```bash
dotnet run
```

以下のような出力が表示されるはずです：

```
=== Recognized Text ===
欢迎光临
```

コンソールに文字化けや空文字列が表示された場合は、次の点を再確認してください：

1. 画像に実際に鮮明で高コントラストな中国語文字が含まれていること。
2. ファイルパスが正しいこと（余分なスペースや拡張子の欠落がないか）。
3. マシンが言語パック取得のために `https://download.aspose.com` にアクセスできること。

## 手順 5: エッジケースと一般的な落とし穴の対処

### 5.1 低品質画像への対処

ソース画像がぼやけていたり、ノイズが多かったり、照明が悪いと OCR の精度は低下します。簡単な対策として画像を前処理します：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 ヘッドレス環境での実行

GUI のない Linux コンテナにデプロイする場合は、`System.Drawing` に必要な `libgdiplus` ライブラリがインストールされていることを確認してください：

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 言語パックを手動でキャッシュする

言語ファイルを一度ダウンロードし、`License` API を介して Aspose に指定すれば、1 回限りのネットワーク呼び出しを省くことができます。オフライン環境で便利です。

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## 完全動作例（オールインワン）

以下は `Program.cs` にコピー＆ペーストできる *完全* なプログラムです。隠し要素や外部スクリプトはありません。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 期待される出力

JPG にフレーズ “欢迎光临” が含まれている場合、コンソールは次のように出力します：

```
=== Recognized Text ===
欢迎光临
```

画像は他の簡体字中国語の看板、道路名、商品ラベルなどに自由に置き換えて構いません—エンジンは最善を尽くします。

## 結論

本稿では C# で **how to use OCR** を用いて **extract text from image** ファイルを処理し、特に **recognize Chinese characters** を **JPG** で実現する方法を取り上げました。Aspose.OCR のオンザフライ言語ダウンロードを活用すれば、軽量なデプロイを保ちつつ、**OCR Chinese Simplified** をすぐに利用できます。

次は何をすべきか？以下のアイデアを試してみてください：

- **Batch processing**: 画像フォルダーをループし、各結果を CSV に書き出す。
- **Combine with translation APIs**: 認識した文字列を Azure Translator に渡してリアルタイム多言語アプリを実現する。
- **Explore other languages**: `OcrLanguage.ChineseSimplified` を `Japanese` や `Arabic` に置き換えて、同じコードがどのように動作するか確認する。

パフォーマンスチューニング、ライセンス、または OCR を Web サービスに統合することについて質問がありますか？以下にコメントを残してください—楽しいコーディングを！

---

![C# で OCR を使用して JPG 画像から中国語テキストを認識する方法を示すコンソール出力のスクリーンショット](ocr-chinese-demo.png "OCR コンソール出力の使用方法")

## 関連チュートリアル

- [Aspose.OCR を使用した言語選択による画像テキスト抽出（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [複数言語対応の Aspose OCR で画像テキストを認識する](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}