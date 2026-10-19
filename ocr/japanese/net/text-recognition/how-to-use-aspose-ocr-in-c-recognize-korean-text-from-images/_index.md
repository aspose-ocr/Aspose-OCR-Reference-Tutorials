---
category: general
date: 2025-12-29
description: Aspose OCR を使用して画像テキストを変換し、韓国語テキストを抽出する方法。C# でテキスト画像を抽出し、韓国語テキストを認識するステップバイステップガイド。
draft: false
keywords:
- how to use aspose
- convert image text
- extract text image
- extract korean text
- recognize korean text
language: ja
og_description: Aspose OCR の使い方を学び、画像テキストを変換し、韓国語テキストを抽出し、写真から韓国語テキストを認識する方法を、完全な
  C# サンプルでご紹介します。
og_title: Aspose OCR の使い方 – C#で韓国語テキストを認識する
tags:
- Aspose
- OCR
- C#
- Image Processing
title: C#でAspose OCRを使用する方法 – 画像から韓国語テキストを認識する
url: /ja/net/text-recognition/how-to-use-aspose-ocr-in-c-recognize-korean-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でAspose OCRを使用する方法 – 画像から韓国語テキストを認識する

写真から韓国語の文字を抽出する方法を **Asposeの使い方** で使うことに興味がありますか？通りの看板のスクリーンショットや、スキャンしたレシート、検索可能なテキストに変換したいミームがあるかもしれません。良いニュースは、Aspose OCR を使えばこれがとても簡単で、低レベルの画像処理テクニックに悩む必要がないということです。

このチュートリアルでは、**完全で実行可能なサンプル**を通して、Aspose OCR ライブラリを使用して **画像テキストを変換**、**テキスト画像を抽出**、そして特に **韓国語テキストを抽出** する方法を示します。最後までに、認識された韓国語文字列を出力するコンソールアプリが完成し、各行がなぜ重要かが理解できるようになります。

## 必要なもの

- **.NET 6+**（最新の .NET SDK が使用可能 – Visual Studio、Rider、または `dotnet` CLI）
- **Aspose.OCR for .NET** NuGet パッケージ  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 韓国語文字を含む画像ファイル（例: `korean_sign.jpg`）。
- C# の基本的な知識 – 「Hello World」を書いたことがあれば問題ありません。

> **Pro tip:** Aspose OCR は標準で50以上の言語をサポートしています。ここでは韓国語に焦点を当てます。Hangul スクリプトは一般的な OCR エンジンでうまく認識できないことが多いためです。

## ステップ 1 – Aspose OCR のインストールと参照

まず、ライブラリをプロジェクトに追加します。上記の NuGet コマンドが主要な作業を行いますが、UI が好みの場合は NuGet パッケージマネージャで *Aspose.OCR* を検索してください。

```csharp
// No code needed here – the package reference is enough.
// The using directives below will bring the types into scope.
using Aspose.OCR;
using Aspose.OCR.Models;
```

> **Why this matters:** `using` 文により `OcrEngine`、`Language`、`Image` ヘルパークラスにアクセスできるようになります。これらが無いとコンパイラは不明な型についてエラーを出します。

## ステップ 2 – 処理したい画像をロードする

Aspose OCR は独自の `Image` ラッパーを使用し、JPEG、PNG、BMP など多数のフォーマットを読み取れます。韓国語テキストが入ったファイルを指定してください。

```csharp
// Step 2: Load the image containing Korean characters
var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
var image = Image.Load(imagePath);
```

ファイルが実行ファイルと同じフォルダーにない場合は、パスを適宜調整してください。`Image.Load` 呼び出しは **画像テキストを変換** し、OCR エンジンが理解できる内部表現にします。

![Aspose OCR の使用例](/images/aspose-ocr-korean.png "Aspose OCR を使用して韓国語テキストを認識する方法")

*画像代替テキスト: “韓国の街頭看板を示す Aspose OCR の使用例”。*

## ステップ 3 – 韓国語用に OCR エンジンを設定する

エンジンは対象言語を認識する必要があります。指定しない場合はデフォルトで英語となり、Hangul 文字を見逃します。

```csharp
// Step 3: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Tell Aspose we want to recognize Korean (Hangul)
    Language = Language.Korean
};
```

> **Why this matters:** `Language = Language.Korean` を設定すると、エンジンは韓国語パックをロードし、Hangul グリフの精度が大幅に向上します。このステップを省くと、文字化けした出力になることが多いです。

## ステップ 4 – 認識プロセスを実行する

いよいよ Aspose に画像の読み取りを指示します。`Recognize` メソッドは抽出された文字列と信頼度スコアを含む `OcrResult` オブジェクトを返します。

```csharp
// Step 4: Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(image);
```

大きな写真（例: 複数の UI 要素があるスクリーンショット）から **テキスト画像を抽出** したい場合は、`Recognize` を呼び出す前に `image.Crop(...)` で関心領域を切り取ることができます。特定の部分だけが必要なときに便利なテクニックです。

## ステップ 5 – 認識された韓国語テキストを出力する

最後に結果を表示します。実際のアプリではデータベースに保存したり翻訳 API に渡したりするかもしれませんが、このチュートリアルではコンソール出力でシンプルにします。

```csharp
// Step 5: Print the recognized Korean text
Console.WriteLine("Recognized Korean text:");
Console.WriteLine(ocrResult.Text);
```

### 期待される出力

```
Recognized Korean text:
서울특별시 강남구 테헤란로 123
```

実際の出力はもちろん、`korean_sign.jpg` に含まれる韓国語文字に応じたものになります。

## 完全な動作例

以下は **完全なプログラム** で、新しいコンソールプロジェクト（`dotnet new console`）にコピー＆ペーストできます。画像ファイルがコンパイルされた `.exe` の隣にあることを確認するか、パスを調整してください。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet before running this code.

        // 2️⃣ Load the image that contains Korean text.
        var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
        var image = Image.Load(imagePath);

        // 3️⃣ Create the OCR engine and set it to recognize Korean.
        var ocrEngine = new OcrEngine
        {
            Language = Language.Korean   // 👈 This enables Hangul support.
        };

        // 4️⃣ Run the OCR process.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted Korean string.
        Console.WriteLine("Recognized Korean text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

`dotnet run` でプログラムを実行し、コンソールに韓国語文字が表示されるのを確認してください。

## よくある質問とエッジケース

### OCR が文字化けした場合は？

- **言語設定を確認**してください。`Language.Korean` を忘れるのが最も一般的なミスです。
- **画像品質を向上**させます。鮮明な画像、高 DPI、適切な照明が精度を高めます。
- **画像を前処理**します。Aspose OCR には組み込みフィルタ（`image.Binarize()`, `image.Deskew()`）があり、ノイズの多いスキャンをクリーンアップできます。

### **画像テキストを一括変換**できますか？

もちろんです。上記の手順を画像フォルダーを走査する `foreach` ループで囲みます。以下は簡単なコード例です：

```csharp
foreach (var file in Directory.GetFiles(@"C:\KoreanImages", "*.jpg"))
{
    var img = Image.Load(file);
    var result = ocrEngine.Recognize(img);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

このスクリプトはすべてのファイルから **テキスト画像を抽出** し、隣に `.txt` ファイルを書き出します。

### 同一画像内の複数言語をどう扱うか？

Aspose OCR は `Language = Language.Auto` と設定すれば言語を自動検出できます。ただし、自動検出は速度が遅く、正確さが若干低下することがあります。画像に韓国語と英語の両方が含まれることが分かっている場合は、`Language.Korean` で一度、次に `Language.English` で二回実行し、結果を結合することができます。

## 本番環境向け OCR のヒント

- **OcrEngine をキャッシュ**します。リクエストごとに新しいエンジンを作成するとオーバーヘッドが増えます。多数の画像を処理する場合はシングルトンを保持してください。
- **画像サイズを制限**します。大きな画像はメモリを消費するため、エンジンに渡す前に幅約1500 px に縮小してください。
- **例外処理**を行います。`Recognize` 呼び出しを try/catch で囲み、破損したファイルに対処できるようにします。

## 結論

ここでは **Aspose の使い方** を通じて **画像テキストを変換**、**テキスト画像を抽出**、そして特に **韓国語テキストを抽出** する方法を数行の C# コードで説明しました。手順はシンプルです：

1. Aspose OCR をインストールする。  
2. 画像をロードする。  
3. エンジンを韓国語用に設定する。  
4. `Recognize` を実行する。  
5. 結果を出力する。

このスニペットをバッチ処理、文書アーカイブ、あるいはリアルタイム翻訳アプリなど、より大きなワークフローに組み込むことができます。さらに進めたい場合は、Aspose の `Image.Preprocess()` メソッドを追加したり、他言語で実験したり、出力を Azure Cognitive Services の翻訳機能と統合したりしてみてください。

**韓国語テキストの認識** や他の Aspose 機能について質問があれば、コメントを残してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}