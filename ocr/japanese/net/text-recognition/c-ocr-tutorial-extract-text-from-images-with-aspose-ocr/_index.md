---
category: general
date: 2026-02-24
description: Aspose OCR を使用して画像からテキストを抽出する方法を示す C# OCR チュートリアル – .NET 開発者向けの完全なステップバイステップガイド。
draft: false
keywords:
- c# ocr tutorial
- how to extract text from image
- Aspose OCR C#
- OCR region of interest
- image text extraction C#
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出する方法を示す C# OCR チュートリアル – .NET 開発者向けの完全なステップバイステップガイド。
og_title: C# OCRチュートリアル：Aspose OCRで画像からテキストを抽出
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C# OCRチュートリアル：Aspose OCRで画像からテキストを抽出する
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – Aspose OCR を使用して画像からテキストを抽出する

C# アプリケーションで画像ファイルからテキストを抽出する方法を考えたことがありますか？ あなただけではありません。実際のプロジェクトでは、パスポートスキャナ、請求書処理、あるいはシンプルなレシートリーダーなど、信頼できる OCR 結果を得ることが日々の課題です。  

この **c# OCR チュートリアル** は、Aspose OCR を使用した実用的なソリューションをステップバイステップで解説し、**画像からテキストを抽出する方法**、スキャン範囲を関心領域に限定する方法、結果の表示方法を、数行のコードで実現します。  

必要なものはすべてカバーします：NuGet パッケージ、必要な `using` 文、ROI の設定、オプション構成、そして出力の簡易チェックです。最後まで読めば、パスポートスキャン（または任意の画像）から名前を取得できる実行可能なコンソールアプリが手に入ります。余計な説明は省き、コピー＆ペーストしてすぐに実行できる明確で完全な解答を提供します。

## 前提条件

- .NET 6+ SDK（または、古いランタイムが好みなら .NET Framework 4.7+）
- Visual Studio 2022 または C# をサポートするエディタ
- **Aspose.OCR** NuGet パッケージを取得するためのインターネット接続
- 読み取り可能なテキストを含む画像ファイル（例：`passport_scan.png`）

> **プロのコツ:** ローカルで試す場合は、プロジェクト内に `Images` フォルダーを作り、そこに小さな PNG または JPEG を入れてください。パスが短くなり、コードがすっきりします。

## 手順 1: Aspose OCR をインストールし、名前空間を追加する

まず最初に、OCR ライブラリが必要です。ターミナル（または Package Manager Console）を開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.OCR
```

パッケージがインストールされたら、`Program.cs` の先頭に必要な `using` ディレクティブを追加します：

```csharp
using Aspose.OCR;          // Core OCR engine
using System.Drawing;     // Rectangle struct for ROI
```

この 2 行で、`OcrEngine`、`OcrOptions`、およびスキャン領域を限定するために使用する `Rectangle` 型が利用可能になります。

## 手順 2: OCR エンジン インスタンスの作成

エンジンはプロセスの中心です。ピクセルを読み取り文字に変換する“脳”と考えてください。初期化はシンプルです：

```csharp
// Step 2: Instantiate the OCR engine – this object does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

> **なぜ重要か:** `OcrEngine` を 1 つだけ作成すれば、複数の画像で再利用でき、メモリ節約とライセンスチェックの繰り返しを防げます。

## 手順 3: 関心領域 (ROI) の定義

高解像度の画像全体をスキャンすると無駄になることがあります。特にテキストがどこにあるか正確に分かっている場合（例：パスポートの名前欄）には、**関心領域** を指定することで、エンジンに矩形外の領域を無視させることができます。

```csharp
// Step 3: Set the ROI – adjust X, Y, Width, Height to match your image layout.
Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);
```

- **X** と **Y** は矩形の左上隅を表します。
- **Width** と **Height** はボックスのサイズを定義します。

正確な数値が分からない場合は、任意の画像エディタ（例：Paint.NET）で簡単に視覚的にテストし、座標を特定すると良いでしょう。

## 手順 4: OCR オプションの設定と ROI の適用

ここで ROI を `OcrOptions` オブジェクトに結び付けます。このオブジェクトは言語や検出速度などの調整も可能ですが、このチュートリアルでは最小限に抑えます。

```csharp
// Step 4: Prepare OCR options and assign the ROI we just defined.
OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };
```

> **エッジケース:** ROI を省略すると、Aspose OCR は画像全体をスキャンし、処理時間が増加し、結果に余計なノイズが混入する可能性があります。

## 手順 5: 画像で OCR エンジンを実行する

すべて設定できたので、実際にテキスト認識を行います。画像へのパスと先ほど作成したオプションを指定してください。

```csharp
// Step 5: Perform OCR on the target image using the configured options.
OcrResult ocrResult = ocrEngine.RecognizeImage(
    "Images/passport_scan.png", // Adjust this path to your file location
    ocrOptions);
```

このメソッドは `OcrResult` オブジェクトを返し、抽出された文字列、信頼度スコア、さらに各単語のバウンディングボックス（後で必要な場合）を含みます。

## 手順 6: 抽出されたテキストの出力

最後に結果を表示します。実際のアプリケーションではデータベースに保存することもありますが、このチュートリアルではシンプルなコンソール出力で十分です。

```csharp
// Step 6: Show the extracted text in the console.
Console.WriteLine("Extracted name: " + ocrResult.Text);
```

プログラムを実行すると、以下のような出力が得られるはずです：

```
Extracted name: JOHN DOE
```

出力が空だったり文字化けした場合は、ROI の座標を再確認し、元画像がはっきりしているか（高コントラスト、ぼやけが少ない）を確認してください。

## 完全な動作例

以下はコンパイル可能な完全な `Program.cs` ファイルです。コンソールプロジェクトに保存し、画像を `Images` フォルダーに置いて **F5** を押してください。

```csharp
using Aspose.OCR;
using System.Drawing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Define the region of interest (ROI) where the text is expected
            // (x, y, width, height) – adjust these values for your own image
            Rectangle regionOfInterest = new Rectangle(150, 300, 800, 200);

            // Step 3: Prepare OCR options and assign the ROI
            OcrOptions ocrOptions = new OcrOptions { Roi = regionOfInterest };

            // Step 4: Perform OCR on the target image using the configured options
            OcrResult ocrResult = ocrEngine.RecognizeImage(
                "Images/passport_scan.png",
                ocrOptions);

            // Step 5: Display the extracted text
            Console.WriteLine("Extracted name: " + ocrResult.Text);
        }
    }
}
```

> **期待される出力:**  
> `Extracted name: JOHN DOE`（または ROI に含まれる任意のテキスト）

## よくある質問とエッジケース

### 画像が別の形式の場合は？

Aspose OCR は PNG、JPEG、BMP、TIFF、さらには PDF もサポートしています。パスの拡張子を変更すれば、エンジンが自動的に形式を検出します。

### ループで複数画像を処理できますか？

もちろんです。`OcrEngine` は再利用できます：

```csharp
foreach (var file in Directory.GetFiles("Images", "*.png"))
{
    var result = ocrEngine.RecognizeImage(file, ocrOptions);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

### ラテン文字以外のスクリプトの精度を上げるには？

`OcrOptions` の language プロパティを設定します：

```csharp
ocrOptions.Language = Language.English; // or Language.Russian, Language.ChineseSimplified, etc.
```

### ROI が間違っていてテキストが抜けた場合は？

矩形を拡大するか、ROI を完全に省略してエンジンに画像全体をスキャンさせることができます。ただし、全画像をスキャンすると処理時間が増えることを覚えておいてください。

## スムーズに使うためのプロのコツ

- **エンジンをキャッシュ:** 各画像ごとに新しい `OcrEngine` を作成するとオーバーヘッドが増えます。アプリが動作している間は単一インスタンスを保持しましょう。
- **画像の前処理:** グレースケール変換やコントラスト向上といった簡単な処理で、認識率が大幅に向上します。
- **null 結果の処理:** `ocrResult?.Text` を使用する前に必ずチェックし、`NullReferenceException` を防ぎます。
- **ライセンスの重要性:** 無料版は最初の 200 文字以降に透かしを挿入します。本番環境で使用する場合は、トライアルまたは商用ライセンスを取得してください。

## 次のステップ

これで **c# OCR チュートリアル** の基本をマスターしたので、以下のトピックを検討してみてください：

- **画像からテキストを一括抽出**（バッチ処理）
- **Aspose OCR** を使用したテーブルや構造化データの検出
- OCR 結果をデータベースや Web API と統合する
- `OpenCvSharp` のような **画像前処理** ライブラリと OCR を組み合わせる

これらのトピックはすべて、作成した基盤の上に構築され、生のスキャンを検索可能で実用的なデータに変換できます。

---

*本番環境で使う準備はできましたか？ GitHub リポジトリから完全なソースを取得し、独自のドキュメントに合わせて ROI を調整すれば、テキストが魔法のように現れます。*  

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}