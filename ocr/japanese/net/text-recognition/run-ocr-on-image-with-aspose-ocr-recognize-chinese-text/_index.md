---
category: general
date: 2026-03-04
description: C#で Aspose OCR を使用して画像の OCR を実行します。中国語テキストの認識、画像からのテキスト抽出、OCR 用の画像の読み込みを数ステップで学びましょう。
draft: false
keywords:
- run OCR on image
- recognize chinese text
- extract text from image
- load image for OCR
- recognize simplified chinese
language: ja
og_description: C#でAspose OCRを使用して画像のOCRを実行します。このガイドでは、中国語テキストの認識、画像からのテキスト抽出、そしてOCRのための画像を効率的に読み込む方法を示します。
og_title: Aspose OCRで画像のOCRを実行 – 簡単な中国語テキスト認識
tags:
- Aspose OCR
- C#
- Chinese OCR
title: Aspose OCRで画像のOCRを実行 – 中国語テキストを認識
url: /ja/net/text-recognition/run-ocr-on-image-with-aspose-ocr-recognize-chinese-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行する – 中国語テキスト向け完全 C# ガイド

画像で **OCR を実行** する必要があったものの、簡体字中国語に対応できるライブラリがどれか分からず悩んだことはありませんか？ あなたは一人ではありません。多くの開発者が **中国語テキストを認識** しようとして壁にぶつかり、エンコーディングの問題で頭を抱えています。  

このチュートリアルでは、ノイズを取り除き、ステップバイステップで Aspose OCR を使用して **画像で OCR を実行** する方法、必要な言語モデルを一度だけダウンロードする方法、そして簡体字中国語文字を含む **画像からテキストを抽出** する方法を示します。最後には、認識されたテキストをコンソールに出力する、すぐに実行できるコンソールアプリが手に入ります。

> **得られるもの:** 完全でコンパイル可能な C# プログラム、各行が重要な理由の説明、リソースが見つからない、画像形式が間違っているといった一般的な落とし穴への対処法のヒント。

## 必要なもの

本格的に始める前に、開発マシンに以下の前提条件がインストールされていることを確認してください。

| 前提条件 | 重要な理由 |
|--------------|----------------|
| .NET 6.0 SDK or later | C# プロジェクトのランタイムとコンパイラを提供します。 |
| Visual Studio 2022 (or VS Code with C# extension) | IntelliSense と簡単なデバッグが利用できます。 |
| Aspose.OCR NuGet package | OCR 機能を支えるコアライブラリです。 |
| An image containing Simplified Chinese characters (e.g., `chinese_sample.png`) | **OCR 用に画像をロード** するソースです。 |

NuGet パッケージは次のコマンドで取得できます：

```bash
dotnet add package Aspose.OCR
```

前提条件が整ったので、エンジンを起動しましょう。

## ステップ 1 – 言語モデルの選択（簡体字中国語を認識）

Aspose OCR は言語データをコアエンジンから分離しているため、必要なモデルを SDK に指示する必要があります。中国本土の文字を扱うので、**Simplified Chinese**（簡体字中国語）モデルを選択します。

```csharp
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

// Select the Simplified Chinese language model
LanguageModel languageModel = LanguageModel.ChineseSimplified;
```

*重要な理由:* OCR エンジンは言語固有の辞書と文字形状を使用します。正しいモデルを選択することで、特に中国語のような文字が密集したスクリプトの精度が大幅に向上します。

## ステップ 2 – モデルを一度だけダウンロード（画像からテキストを抽出）

コードを初めて実行する際、Aspose のサーバーからモデルファイルを取得する必要があります。`ResourceDownloader` がこれを処理します。本番アプリでは非同期にすることが多いですが、チュートリアルの明快さのために `.Wait()` でブロックします。

```csharp
// Initialise the downloader and fetch the model (runs once)
ResourceDownloader resourceDownloader = new ResourceDownloader();
resourceDownloader.DownloadModelAsync(languageModel).Wait();
```

> **プロのコツ:** ダウンロードしたリソースをプロジェクトの一部であるフォルダー（例: `OcrResources`）に保存します。これにより、以降の実行ではネットワーク呼び出しが省かれ、処理が高速化します。

## ステップ 3 – エンジンにローカルリソースを指定（OCR 用に画像をロード）

ここで OCR エンジンを作成し、モデルファイルの所在を指定します。`LocalResourceProvider` はディスクからファイルを読み込み、以降のネットワークトラフィックを排除します。

```csharp
// Create the OCR engine and link it to the local resources folder
OcrEngine ocrEngine = new OcrEngine
{
    ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
};
```

`YOUR_DIRECTORY` を、モデルファイルを保存した場所を指す絶対パスまたは相対パスに置き換えてください。  

*重要な理由:* エンジンが言語リソースを見つけられない場合、`FileNotFoundException` がスローされ、**画像で OCR を実行** できなくなります。

## ステップ 4 – 認識用言語の設定（中国語テキストを認識）

簡体字中国語モデルをダウンロードしたとはいえ、認識時にエンジンに使用する言語を通知する必要があります。

```csharp
// Tell the engine to use Simplified Chinese for this session
ocrEngine.Language = Language.ChineseSimplified;
```

実行時に言語を切り替える必要がある場合（例: 中国語から英語へ）、`Recognize` を呼び出す前にこのプロパティを変更すれば簡単です。

## ステップ 5 – 画像をロードして OCR を実行（画像で OCR を実行）

チュートリアルの核心です：画像ファイルをロードし、そのテキスト内容を抽出します。`ImageInfo.Load` メソッドは、OCR エンジンが理解できる形式でファイルを読み込みます。

```csharp
// Load the image that contains Chinese characters
var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

// Perform OCR – this is where we actually run OCR on image
OcrResult ocrResult = ocrEngine.Recognize(imageInfo);
```

画像が大きい、またはノイズが多い場合は、この手順の前に前処理（例: 二値化）を検討してください。Aspose OCR にはフィルタもありますが、初心者向けガイドの範囲を超えます。

## ステップ 6 – 認識結果の出力（画像からテキストを抽出）

最後に、抽出した文字列をコンソールに出力します。実際のシナリオでは、データベースやファイルに書き込んだり、別のサービスに渡したりすることもあります。

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、以下のような出力が表示されます：

```
=== Recognized Text ===
你好，世界！这是一个测试。
```

これで完了です—初めての **画像で OCR を実行** が **中国語テキストを認識** しました。

## 完全な、すぐに実行できるサンプル

以下は、`dotnet new console` で作成した新しいコンソールプロジェクトにコピー＆ペーストできる完全なプログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えることを忘れないでください。

```csharp
// ------------------------------------------------------------
// Complete C# example: Run OCR on Image and Recognize Simplified Chinese
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

class Program
{
    static void Main()
    {
        // 1️⃣ Choose the language model (Simplified Chinese)
        LanguageModel languageModel = LanguageModel.ChineseSimplified;

        // 2️⃣ Download the model (only the first time)
        var downloader = new ResourceDownloader();
        downloader.DownloadModelAsync(languageModel).Wait();   // Blocking for tutorial simplicity

        // 3️⃣ Initialise OCR engine with local resources folder
        var ocrEngine = new OcrEngine
        {
            ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
        };

        // 4️⃣ Set the language for this session
        ocrEngine.Language = Language.ChineseSimplified;

        // 5️⃣ Load the image that contains Chinese text
        var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

        // 6️⃣ Run OCR on the image and capture the result
        OcrResult result = ocrEngine.Recognize(imageInfo);

        // 7️⃣ Output the extracted text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

> **期待される出力:** コンソールは `chinese_sample.png` に見つかった中国語文字を出力します。画像が鮮明であれば、精度はしばしば 95 % を超えます。

## よくある落とし穴と回避方法

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| `FileNotFoundException` が起動時に発生 | リソースフォルダーのパスが間違っている | `LocalResourceProvider` のパスを再確認してください。クロスプラットフォームの安全性のために `Path.Combine` を使用します。 |
| 出力が空 (`ocrResult.Text` が空) | 画像がノイズが多すぎる、またはサポート外の形式 | 画像を高コントラストの PNG に変換するか、`Recognize` の前に `ocrEngine.PreprocessImage(imageInfo)` を使用してください。 |
| 例外: `Unsupported language` | 言語モデルがダウンロードされていない | ダウンローダー手順を再実行するか、破損したフォルダーを削除して再度ダウンロードさせてください。 |
| 最初の実行が遅い | 遅い接続でモデルをダウンロードしている | モデルを共有ネットワーク場所にキャッシュするか、インストーラーに事前にバンドルしてください。 |

## ソリューションの拡張（次のステップ）

- **バッチ処理:** 画像ディレクトリをループし、各ファイルに同じ `Recognize` メソッドを呼び出します。これにより、手作業なしで **画像からテキストを抽出** したコレクションを処理できます。  
- **ポストプロセッシング:** 正規表現を使用して OCR のアーティファクト（例: 余分な句読点）をクリーンアップします。  
- **言語検出:** 多言語ドキュメントを扱う必要がある場合、`ocrResult.DetectedLanguage`（新しい Aspose リリースで利用可能）を確認し、`ocrEngine.Language` を適切に切り替えます。  

## 結論

C# で Aspose OCR を使用して **画像で OCR を実行** するために必要なすべてを解説しました。正しい **簡体字中国語を認識** モデルの選択、リソースのダウンロード、エンジンの構成、そして最終的に **画像からテキストを抽出** するまで、チュートリアルは自己完結型のコピー＆ペーストソリューションを提供します。  

これで、エンジンに投げ込む任意の PNG や JPEG で自信を持って **中国語テキストを認識** でき、バッチジョブや多言語サポート、下流の分析パイプラインとの統合へ拡張するための堅固な基盤が手に入ります。  

OCR 設定の調整や他のスクリプトの取り扱いについて質問がありますか？ コメントを残してください。ハッピーコーディング！ 

![画像で OCR を実行する例](image.png "画像で OCR を実行する例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}