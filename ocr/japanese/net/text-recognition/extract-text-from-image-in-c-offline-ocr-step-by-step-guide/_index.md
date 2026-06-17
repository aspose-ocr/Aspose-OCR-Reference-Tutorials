---
category: general
date: 2026-02-28
description: インターネットを使用せずに Aspose.OCR で画像からテキストを抽出します。png からテキストを認識する方法、スキャンからテキストを読み取る方法、画像をテキストに変換する方法、OCR
  用に画像を読み込む方法を学びましょう。
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from scan
- convert image to text
- load image for OCR
language: ja
og_description: Aspose.OCR を使用してオフラインで画像からテキストを抽出します。このチュートリアルでは、png からテキストを認識し、スキャンからテキストを読み取り、画像をテキストに変換し、OCR
  用に画像をロードする方法を示します。
og_title: C#で画像からテキストを抽出 – オフラインOCRガイド
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#で画像からテキストを抽出する – オフラインOCRステップバイステップガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-offline-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – オフライン OCR ステップバイステップ ガイド

インターネット接続に依存できないアプリで、**画像からテキストを抽出**したいことはありませんか？サンドボックス化されたデバイス上で動作するセキュアなスキャナを構築しているか、単に遅延のスパイクを回避したいだけかもしれません。いずれの場合も、Aspose.OCR を使用すれば **png からテキストを認識** できることをオフラインで実現できます。  

このチュートリアルでは、Aspose.OCR ライブラリを使用して **スキャンからテキストを読み取る**、**画像をテキストに変換する**、そして **OCR 用に画像をロードする** 方法を示す、完全な実行可能サンプルを順に解説します。最後まで実行すれば、抽出したテキストをコンソールに出力する自己完結型のコンソールアプリが手に入ります—クラウドサービスは不要です。

## 必要なもの

- **.NET 6.0**（または最近の .NET バージョン）。示した構文は .NET 6 以降で動作しますが、同じ概念は .NET Framework 4.7 以降にも適用できます。
- **Aspose.OCR for .NET** NuGet パッケージ。`dotnet add package Aspose.OCR` でインストールします。
- 明瞭で読みやすいテキストが含まれる画像ファイル（png、jpg、bmp など）。このガイドでは `offline_test.png` と呼び、`YOUR_DIRECTORY` フォルダーに配置するとします。
- お好みの IDE（Visual Studio、VS Code、Rider など）

> **プロ・チップ:** 必要な言語パック（例では英語）をアプリと同じマシンに置いておくと、真のオフライン動作が保証されます。

## ステップ 1 – プロジェクトのセットアップと Aspose.OCR のインストール

新しいコンソールプロジェクトを作成し、OCR ライブラリを取り込みます。

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
dotnet add package Aspose.OCR
```

> **重要な理由:** NuGet パッケージを追加すると必要な DLL がすべて復元されるため、コンパイル時に “missing reference” エラーが発生しません。

## ステップ 2 – オフライン使用のために OCR エンジンを設定する

このソリューションの中心は `OcrEngine` クラスです。`OfflineMode` を `true` に設定することで、エンジンがネットワーク呼び出しを行わないことを保証します。また、ローカルにある言語パックを指定します。

```csharp
using Aspose.OCR;
using System.Drawing;   // For Image.Load

// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    OfflineMode = true,               // Prevent any network calls
    Language = OcrLanguage.English    // Use the locally‑installed English pack
};
```

> **説明:** `OfflineMode` は安全装置です。設定し忘れると、Aspose がバックグラウンドでクラウドサービスに接続し、欠落した言語データをダウンロードしようとする可能性があり、オフラインスキャナの目的が失われます。

## ステップ 3 – 処理したい画像をロードする

画像のロードはシンプルですが、`using var` を使用してビットマップが自動的に破棄されることに留意してください。

```csharp
// Adjust the path to point at your image file
using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

// Quick sanity check – you can inspect image.Width / image.Height if needed
Console.WriteLine($"Loaded image with dimensions: {image.Width}x{image.Height}");
```

> **エッジケース:** ファイルが見つからない場合、`Image.Load` は `FileNotFoundException` をスローします。本番コードでは try‑catch ブロックで呼び出しをラップしてください。

## ステップ 4 – OCR を実行してテキストを取得する

いよいよ認識を実行します。`Recognize` メソッドは抽出された文字列と信頼度スコアを含む `OcrResult` オブジェクトを返します。

```csharp
// Perform OCR
var ocrResult = ocrEngine.Recognize(image);

// The Text property holds the plain‑text extraction
string extractedText = ocrResult.Text;

// Show the result
Console.WriteLine("\n--- OCR Output ---");
Console.WriteLine(extractedText);
```

> **表示内容:** `ocrResult.Text` はすでにクリーンな文字列です—下流のロジックで改行を除去する必要がなければ、そのままで構いません。

## ステップ 5 – 完全な動作例

すべてをまとめると、プロジェクトにコピー＆ペーストできる完全な `Program.cs` がこちらです。そのままコンパイル・実行できます（画像パスを置き換えるだけです）。

```csharp
using Aspose.OCR;
using System.Drawing;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true,               // Prevent any network calls
            Language = OcrLanguage.English    // Use a locally‑available language pack
        };

        // Step 2: Load the image you want to process
        using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

        // Step 3: Run OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Display the extracted text
        System.Console.WriteLine("\n--- Extracted Text ---");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 期待される出力

`offline_test.png` に “Hello, world!” という文が含まれている場合、コンソールに次のように出力されます:

```
--- Extracted Text ---
Hello, world!
```

長文の場合、OCR エンジンが解釈した通りに段落全体、改行、句読点が保持された形で出力されます。

## よくある質問と注意点

### 1. *カラー背景の png ファイルからテキストを認識できますか？*  
はい。Aspose.OCR は自動的にコントラストを正規化する前処理を適用します。背景がノイズが多すぎる場合は、まず画像をグレースケールに変換することを検討してください:

```csharp
image = image.ConvertToGrayscale();
```

### 2. *PNG ではなくスキャンした PDF からテキストを読み取る必要がある場合は？*  
PDF ライブラリ（例: Aspose.PDF）を使用して各ページを画像として抽出し、同じ OCR パイプラインに渡します。ビットマップを取得した後は、ワークフローは同一です。

### 3. *低信頼度の結果はどう処理すればよいですか？*  
`OcrResult` には文字ごとの `Confidence` プロパティが含まれます。`ocrResult.Characters` を走査し、信頼度が 0.75 未満の文字を手動レビュー用にフラグ付けできます。

### 4. *英語の言語パックだけがオフラインで動作しますか？*  
いいえ。ローカルにインストールした任意の言語パック（例: `OcrLanguage.Spanish`）が同様に機能します—`Language = OcrLanguage.Spanish` と設定すればよいだけです。

### 5. *画像フォルダーをバッチ処理できますか？*  
もちろん可能です。ロードと認識ロジックを `foreach (var file in Directory.GetFiles(folder, "*.png"))` ループで囲みます。処理後は各画像を破棄することを忘れないでください。

## パフォーマンスのヒント

- **`OcrEngine` インスタンスを再利用** して複数画像を処理します。ファイルごとに新しいエンジンを作成するとオーバーヘッドが増えます。
- **大きな画像はリサイズ** して、長辺を最大 2000 px に抑えます。サイズが大きくても精度は向上せず、処理が遅くなるだけです。
- **マルチスレッドを有効化** して多数の画像を処理する場合は、各スレッドが独自の `OcrEngine` を持つか、共有インスタンスをロックで保護してください。

## ビジュアル概要

![オフライン OCR フローを示す図 – 画像からテキストを抽出 → OCR 用に画像をロード → png からテキストを認識 → テキストを出力](https://example.com/ocr-flow.png "画像からテキストを抽出するワークフロー")

*この図は本ガイドで取り上げた4つの主要ステップを強調しています。*

## 結論

これで、Aspose.OCR を使用して画像ファイルからテキストを完全にオフラインで **抽出**する方法が分かりました。このチュートリアルでは、プロジェクトのセットアップ、エンジンのオフラインモード設定、画像のロード、そして最終的に **png からテキストを認識** し **スキャンからテキストを読み取る** ドキュメントまでを網羅しました。完全なソースコードが手元にあるので、**画像をテキストに変換**するバッチジョブへの適用、デスクトップユーティリティへの統合、またはオンプレミスで動作するサーバーサイドサービスへの組み込みがすぐに行えます。

次は何をすべきでしょうか？英語の言語パックを別の言語に差し替えてみたり、画像前処理（しきい値処理、デスキュー）を試したり、OCR の出力を自然言語処理パイプラインに渡して感情分析を行ったりしてみてください。オフライン OCR と最新の .NET ツールを組み合わせれば、可能性は無限です。

コーディングを楽しんで、スキャンが常にクリアでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}