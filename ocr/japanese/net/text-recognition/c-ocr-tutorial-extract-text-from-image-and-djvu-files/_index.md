---
category: general
date: 2026-01-09
description: c# OCRチュートリアルでは、画像ファイルからテキストを抽出し、Aspose.OCRを使用してDJVUをテキストに変換する方法を示します。数分でステップバイステップの抽出を学びましょう。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: ja
og_description: c# OCRチュートリアル：画像ファイルからテキストを抽出し、Aspose.OCRを使用してDJVUをテキストに変換する方法を迅速に紹介します。実用的な解決策を得るためにガイドに従ってください。
og_title: c# OCRチュートリアル – 画像とDJVUからテキストを抽出
tags:
- OCR
- C#
- Aspose
title: c# OCRチュートリアル：画像とDJVUファイルからテキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – 画像と DJVU ファイルからテキストを抽出する

画像ファイルからテキストを抽出したいけど、どうすればいいか分からずに悩んだことはありませんか？この **c# OCR チュートリアル** では、通常の画像 *と* DJVU ドキュメントの両方からテキストを取り出す、実行可能なサンプルを一から解説します。

**DJVU をテキストに変換** したい方にも最適です—余計なコンバータは不要、純粋な C# コードだけで完結します。

## 学べること

- .NET プロジェクトに Aspose.OCR ライブラリを設定する方法  
- 画像ファイルから **テキストを抽出** するための正確なコード  
- **DJVU からテキストを抽出** する簡潔な手法（同じエンジンで可能）  
- 大容量ファイル、フォント欠如、ライセンス問題などの一般的な落とし穴と回避策  

必要なのは最新の .NET SDK と NuGet パッケージを取得できるインターネット環境だけ。OCR の事前知識は不要です。

## 前提条件

作業を始める前に以下を用意してください。

| 必要条件 | 理由 |
|-------------|----------------|
| .NET 6.0 以上 | Aspose.OCR は .NET Standard 2.0 を対象としているため、.NET 6+ で最高のパフォーマンスが得られます。 |
| Visual Studio 2022（または VS Code） | IDE がパッケージ管理を楽にしますが、任意のエディタでも構いません。 |
| NuGet パッケージ **Aspose.OCR** | 実際に OCR 処理を行うエンジンです。 |
| サンプル画像 (`sample.png`) と DJVU ファイル (`sample.djvu`) | 両方の抽出シナリオをデモするために使用します。 |

パッケージは以下のコマンドでインストールできます。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** CI サーバー上でビルドする場合は、`--no-restore` をビルドステップに追加し、最初の一回だけ `restore` することで速度を向上させられます。

## Step 1: OCR エンジンの初期化 – c# OCR チュートリアルの核

最初に `OcrEngine` のインスタンスを作成します。ソフトウェアでスキャナをオンにするイメージです。

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

なぜ毎回新しいエンジンを作るのか？ エンジンは設定（言語、検出モード等）を保持しているため、毎回クリーンな状態で開始することで前回の設定が流出するのを防げます。

## Step 2: 画像を読み込み認識 – 画像からテキストを抽出する方法

次に通常のビットマップ（PNG、JPEG、BMP…）をエンジンに渡します。`RecognizeImage` メソッドは検出された文字列を返します。

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

留意点は以下の通りです：

* **ファイルの存在** – パスが間違っていると `FileNotFoundException` がスローされます。ユーザー入力のパスを受け取る場合は `try/catch` で囲んでください。  
* **画像の品質** – OCR は 300 dpi 以上で最適に動作します。低解像度のスキャンは文字化けしやすくなります。  
* **言語サポート** – デフォルトでは Aspose.OCR は英語を想定しています。別言語に変更するには、`ocrEngine.Language = Language.Spanish;` を `RecognizeImage` の前に設定します。

## Step 3: DJVU ドキュメントからテキストを認識 – DJVU をテキストに変換

DJVU は複数ページを保持できるコンテナ形式です。Aspose.OCR は直接処理できるので、ファイルを指すだけで OK です。

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

内部では、エンジンが各ページを画像として抽出し、同じ認識パイプラインを実行します。そのため、別途「DJVU をテキストに変換」するステップは不要で、OCR エンジンが自動的に処理してくれます。

### マルチページ DJVU の取り扱い

DJVU に複数ページがある場合、`RecognizeImage` は順番に結合して返します。ページごとに個別の文字列が必要なときは、`List<string>` を返すオーバーロードを使用できます。

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## Step 4: エンジンを微調整して精度向上 – 重要性のポイント

デフォルトの結果でもまずまずですが、いくつかの設定を調整するだけで精度を大幅に向上させられます。

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

これらのフラグは、**DJVU に変換されたスキャン PDF からテキストを抽出** する際に特に有用です。向き検出を有効にすれば、画像を手動で回転させる手間が省けます。

## Step 5: ライセンスと実行時エラーへの対処

Aspose.OCR には無料トライアルが付属しており、数ページを超えると出力に「Demo」透かしが入ります。透かしを除去するにはライセンスファイルを追加してください。

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

この手順を忘れるとエンジンは動作しますが、結果に「Demo」という文字が含まれます。また、巨大な DJVU ファイルを処理する際は `OutOfMemoryException` に注意し、前述のページ単位処理を検討してください。

## 完全な実行可能サンプル

以下はすべてをまとめたコンソールアプリのコードです。コピーして貼り付け、ファイルパスを調整したら **Run** してください。

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**期待される出力**（ファイルに「Hello World」というフレーズが含まれている場合）：

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

ソースに複数行がある場合は、元のドキュメントと同じ順序で表示されます。

## よくある質問 & エッジケースの対処

* **画像が白黒の場合は？**  
  OCR は問題なく動作しますが、`ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;` でコントラストを上げると精度が向上します。  

* **数字だけ抽出したい場合は？**  
  `ocrEngine.CharWhitelist = "0123456789";` を `RecognizeImage` の前に設定すれば数字のみ取得できます。  

* **ファイルサイズに上限はあるか？**  
  エンジンはファイル全体をメモリに読み込みます。約 100 MB を超える場合は、ページ単位で処理する（Step 3 のリストオーバーロード参照）ことを推奨します。  

* **Tesseract と何が違うのか？**  
  Aspose.OCR は商用ライブラリで、DJVU 直接サポートやネイティブ依存が不要です。一方 Tesseract はネイティブバイナリと別途 DJVU 変換ツールが必要です。  

## 結論

これで **c# OCR チュートリアル** は完了です。Aspose.OCR を使って **画像からテキストを抽出** し、シームレスに **DJVU をテキストに変換** する方法を学びました。パッケージのインストールからライセンス設定、単ページ画像抽出からマルチページ DJVU の取り扱い、精度向上のコツまで網羅しています。

次のステップとしては、PDF からテキストを抽出する方法を調べたり、OCR 処理を Web API に組み込んだり、マルチリンガル文書向けに言語パックを試したりすると良いでしょう。要点はシンプルです：エンジンを設定し、ファイルを渡し、文字列を取得するだけです。

質問があればコメントで教えてください。自分のドキュメントでコードを試し、楽しいコーディングを！ 

![c# OCR tutorial screenshot showing console output](/images/csharp-ocr-tutorial.png "c# OCR tutorial – console output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}