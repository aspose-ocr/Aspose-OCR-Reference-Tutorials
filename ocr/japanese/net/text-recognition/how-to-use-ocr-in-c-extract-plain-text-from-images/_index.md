---
category: general
date: 2026-04-06
description: C#でOCRを使用してJPG画像（キリル文字を含む）からプレーンテキストを抽出する方法。画像のOCRへの読み込み、JPGのテキスト認識、信頼できる結果の取得を学びましょう。
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: ja
og_description: C#でOCRを使用してJPGファイルからプレーンテキストを抽出する方法。このガイドでは、OCR用に画像を読み込む方法、JPGのテキストを認識する方法、そしてキリル文字を扱う方法を示します。
og_title: C#でOCRを使用する方法 – 画像からプレーンテキストを抽出する
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#でOCRを使用する方法 – 画像からプレーンテキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – 画像からプレーンテキストを抽出する

.NET プロジェクトで **OCR の使い方** に悩んだことはありませんか？スキャンした領収書が入ったフォルダーや、キリル文字のキャプションが付いたスクリーンショットが数枚、あるいは JPEG からテキストをすぐに取り出したいだけかもしれません。朗報です。Aspose OCR を使えば、この一連の作業がとても簡単になります。

このチュートリアルでは、JPEG 画像から **プレーンテキストを抽出** する **OCR の使い方** を示す、完全に実行可能なサンプルをステップバイステップで解説します。**画像を OCR 用に読み込む** 方法や、ソース言語がラテン文字でない場合に **キリル文字テキストを抽出** する方法も紹介します。最後には、認識結果をコンソールに直接出力する小さなコンソールアプリが完成します—余計なファイルや不明な副作用はありません。

> **得られるもの**  
> * Visual Studio にコピペできるステップバイステップガイド。  
> * 各行が *何をするか* だけでなく *なぜ必要か* を解説。  
> * 大きな画像、複数言語、一般的な落とし穴への対処法。

## 前提条件

始める前に以下を用意してください。

* .NET 6 SDK 以降（コードは .NET Core や .NET Framework でも動作します）。  
* Visual Studio 2022（またはお好みのエディタ）。  
* 初回実行時にインターネット接続が必要です—Aspose OCR は必要に応じて言語パックをダウンロードします。

Aspose OCR の NuGet パッケージがまだない場合は、最初の手順でインストール方法を説明します。

## 手順 1 – NuGet で Aspose OCR をインストール（なぜ重要か）

**画像を OCR 用に読み込む** 前にライブラリが必要です。NuGet を使うことで、最新かつセキュリティパッチが適用されたバイナリが取得でき、必要な依存関係も自動で追加されます。

```bash
dotnet add package Aspose.OCR
```

*重要ポイント*: Aspose OCR は非常に小さなコア DLL と、要求されたときにだけ言語データを取得する仕組みです。これによりアプリは軽量に保たれ、未使用の言語ファイルが数メガバイトもバンドルされることを防げます。

## 手順 2 – OCR エンジンを初期化（**OCR の使い方** の核心）

`OcrEngine` インスタンスを作成することが、**OCR の使い方** における最初の実装行になります。エンジンはデフォルトで「オンデマンド」モードになっており、特定の言語を初めて要求したときに言語パックをダウンロードします。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **プロのコツ**: 社内プロキシ環境下で実行する場合は、最初の認識呼び出しの前に `OcrEngine.Proxy` を設定しておくとダウンロードが成功します。

## 手順 3 – 言語を選択 – 必要に応じて **キリル文字テキストを抽出**

Aspose OCR は多数のスクリプトに対応しています。**キリル文字テキストを抽出** したいときは、`Language` プロパティを `OcrLanguage.Cyrillic` に設定します。この行が初めて実行されると、キリル文字モジュール（約 5 MB）が Aspose の CDN から取得されます。

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

画像がラテン文字だけの場合は、`Cyrillic` を `English` に置き換えて構いません。サポートされている言語であれば同じパターンが使えます。

## 手順 4 – **画像を OCR 用に読み込む** – ディスクまたはストリームから

ここで実際に **画像を OCR 用に読み込む** 作業を行います。`System.Drawing.Image` クラスは JPG、PNG、BMP などの一般的なフォーマットを扱えます。非 Windows 環境の場合は `ImageSharp` の使用を検討してください。ただし本チュートリアルでは組み込み型で十分です。

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **なぜ重要か**: `using` ブロック内で画像を読み込むことで、アンマネージドな GDI+ リソースが速やかに解放され、長時間稼働するサービスでのメモリリークを防げます。

## 手順 5 – **JPG テキストを認識** – OCR プロセスを実行

エンジンの設定と画像の読み込みが完了したら、いよいよ **JPG テキストを認識** します。`Recognize` メソッドは `OcrResult` を返し、プレーン文字列、信頼度スコア、必要に応じてバウンディングボックスも含まれます。

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

精度を微調整したい場合は `ocrEngine.Config` を変更できます（例: `AutoRotate` を有効にしたり `TextOrientation` を設定したり）。多くのシンプルなシナリオではデフォルト設定で十分に高精度です。

## 手順 6 – **プレーンテキストを抽出** – 結果を表示

**OCR の使い方** の最終ステップは、`ocrResult` から認識された文字列を取り出し、何らかの形で利用することです。ここではコンソールに出力するだけにしていますが、同時に **プレーンテキストを抽出** する方法も示しています。

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### 期待される出力

`cyrillic_sample.jpg` に「Привет мир」（Hello world）というフレーズが含まれている場合、次のように表示されます。

```
=== Recognized Text ===
Привет мир
```

画像がぼやけている、または文字が小さすぎる場合はエラーが含まれることがあります。その際は `ocrResult.Confidence` を確認し、より高解像度の画像で再試行するか判断してください。

## 完全版・実行可能サンプル

以下が全コードです。新規コンソールアプリプロジェクト（`dotnet new console`）に貼り付けて実行してください。画像ファイルへのパス以外に追加ファイルは不要です。

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **注意**: `YOUR_DIRECTORY\cyrillic_sample.jpg` を実際の JPEG ファイルパスに置き換えてください。

## よくある質問とエッジケース

### ストリームから **JPG テキストを認識** したい場合は？

`MemoryStream` を直接渡すことができます。

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### 同一画像内で複数言語を扱うには？

`ocrEngine.Language` を `OcrLanguage.Multilingual` に設定します。エンジンが各スクリプトを自動検出し、英語とキリル文字が混在した領収書などに便利です。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 画像が非常に大きい（5 MP 超）場合はどうなる？

大きな画像はメモリ使用量が増え、認識速度が低下します。事前にリサイズすると効果的です。

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### 行ごとの信頼度スコアを取得できるか？

はい。`ocrResult.Lines` には各行の `Confidence` が含まれます。ループで走査すれば低信頼度の結果を除外できます。

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## 本番環境向け OCR のプロティップ

* **言語パックをキャッシュ** – 初回ダウンロードは数秒かかります。取得したファイルを既知のフォルダーに保存し、`ocrEngine.LanguageDataPath` で再利用してください。  
* **バッチ処理** – 多数の画像を処理する場合は、`OcrEngine` インスタンスを使い回すことでオーバーヘッドを削減できます。  
* **エラーハンドリング** – `Recognize` 呼び出しは `try/catch` で囲みましょう。画像が破損している、または未対応フォーマットの場合は `OcrException` がスローされます。  
* **ロギング** – `ocrResult.Confidence` を記録しておくと、後で手動レビューが必要なページを特定できます。

## 結論

本稿では C# で **OCR の使い方** を学び、JPEG から **プレーンテキストを抽出** する方法、**画像を OCR 用に読み込む** 手順、**JPG テキストを認識** する流れ、そして画像から **キリル文字テキスト** を取り出す方法を実演しました。サンプルは単一の NuGet パッケージだけで動作し、マルチランゲージ文書やバッチジョブ、リアルタイムスキャンシナリオへも容易に拡張可能です。

次のステップに挑戦してみませんか？キリル語の代わりにアラビア語を指定したり、`AutoRotate` フラグを試したり、認識結果を検索インデックスに統合したり。可能性は無限です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}