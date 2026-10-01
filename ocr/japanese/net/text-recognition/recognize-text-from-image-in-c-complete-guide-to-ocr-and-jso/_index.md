---
category: general
date: 2026-01-10
description: C#でAspose OCRを使用して画像からテキストを認識し、テキスト座標を抽出し、領収書をJSONに変換する方法を学びましょう。ステップバイステップのチュートリアルです。
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: ja
og_description: Aspose OCR を使用して C# で画像からテキストを認識します。このガイドでは、テキストの抽出方法、座標の取得方法、領収書を
  JSON に変換する方法を示します。
og_title: 画像からテキストを認識する – 完全なC# OCRチュートリアル
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを認識する – OCRとJSONの完全ガイド
url: /ja/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する – 完全な C# OCR チュートリアル

画像からテキストを認識したいが、どのライブラリを選べばよいか分からなかったことはありませんか？ あなたは一人ではありません。実際のアプリ（費用トラッカー、レシートスキャナー、ドキュメントアーカイバーなど）では、テキストを確実に抽出することが最初のハードルです。

このチュートリアルでは、**テキストの抽出方法**、バウンディングボックスの取得、そして最終的に Aspose.OCR for .NET を使用して **レシートを JSON に変換** する手順を解説します。最後まで実行すれば、レシートの写真を入力として、信頼度スコアと座標を含む整然とした JSON ファイルを出力する、自己完結型の C# プロジェクトが手に入ります。

## 必要なもの

始める前に、以下がマシンにインストールされていることを確認してください：

- **.NET 6.0 SDK**（またはそれ以降のバージョン）。古いフレームワークでも動作しますが、.NET 6 は最新ライブラリに最適です。
- **Visual Studio 2022** または C# 拡張機能がインストールされた VS Code。
- **Aspose.OCR for .NET** NuGet パッケージ（`Aspose.OCR` と `Aspose.OCR.Output`）。Package Manager Console からインストールできます：

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- サンプルのレシート画像（例：`receipt.jpg`）を、後で参照するフォルダーに配置します。

以上です—追加の SDK やネイティブバイナリは不要で、純粋なマネージドコードだけです。

## 手順 1: 新しいコンソールプロジェクトを作成する

まずはコンソールアプリを作成します。UI のオーバーヘッドがなく、OCR をテストする最速の方法です。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **プロのコツ:** プロジェクトフォルダーを整理整頓しましょう。`Resources` というサブフォルダーを作成し、そこに `receipt.jpg` を置きます。パス処理が楽になります。

## 手順 2: レシート画像を読み込む

ここで実際に **画像からテキストを認識** します。最初のステップは OCR エンジンにファイルを指定することです。

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

なぜロード時に簡単な存在チェックを行うのでしょうか？ 本番環境では、ユーザーがアップロードしたファイルが欠損や破損していることがよくあります。早期に問題を検出することで、後で意味不明な例外に悩まされることを防げます。

## 手順 3: OCR を実行する – **画像からテキストを認識**

画像がメモリ上にある状態で、Aspose に **画像からテキストを認識** させます。この操作は同期的で、豊富な結果セットが返されます。

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

内部では、Aspose が何百万もの文字で学習したニューラルネットワークを実行しています。エンジンは `ocrEngine.Text`、`ocrEngine.RecognitionResult`、そして座標を保持する `OcrRegion` オブジェクトのコレクションを生成します。これが次のステップで必要になる情報です。

## 手順 4: **テキストの抽出方法** – 生文字列の取得

プレーンテキストだけが必要な場合（例えば簡易検索用）、エンジンから直接取得できます：

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

OCR が段落の境界を検出した場所で改行が入っていることに気付くでしょう。レシートスキャンの多くのシナリオでは、生文字列だけで合計金額や日付、ベンダー名をシンプルな正規表現で抽出できます。

## 手順 5: **テキスト座標の抽出** – 各単語のバウンディングボックス

画像上で特定のテキストがどこにあるか（例：UI で合計金額をハイライトする）を知りたくなることがよくあります。Aspose は `OcrRegion` オブジェクトを通じてその情報を提供します。

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

ここでは認識されたすべてのセグメントに対して **テキスト座標の抽出** をループしています。座標は元画像に対して相対的なので、グラフィックキャンバスや HTML の `<canvas>` 要素に重ねて表示できます。

## 手順 6: **レシートを JSON に変換** – 詳細結果の保存

ここで全体を結びつけるパートです。テキスト、信頼度スコア、バウンディングボックスを含む機械可読な構造が欲しいです。Aspose には `JsonSaveOptions` が用意されており、これを簡単に実現できます。

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

生成されたファイルは以下のようになります（簡略化しています）：

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

これで **レシートを JSON に変換** した成果物ができました。これを下流のサービス（例：経費レポート API、分析パイプライン、あるいは各単語に矩形を描画するシンプルな UI）に渡すことができます。

## 完全な動作例

すべてのパーツを組み合わせた完全な `Program.cs` を以下に示します。プロジェクトにコピー＆ペーストして使用できます：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

プログラムを実行（`dotnet run`）し、コンソール出力を確認してください。`Resources/receipt.json` を開いて構造を検証しましょう。

## よくある質問とエッジケース

- **画像がぼやけている場合は？**  
  Aspose OCR は 300 dpi 以上で最適に動作します。信頼度スコアが低い場合は、エンジンに画像を渡す前にシャープ化フィルタを適用することを検討してください。

- **複数言語を認識できますか？**  
  はい。`Recognize()` を呼び出す前に `ocrEngine.Language = Language.English | Language.Spanish;` と設定します。

- **出力を数字（例：合計金額）のみに限定するには？**  
  プレーンテキストを取得した後、`ocrEngine.Text` に対して `\d+\.\d{2}` のような正規表現を実行します。座標情報が既にあるので、マッチした文字列を対応する領域にマッピングして視覚的にハイライトできます。

- **JSON フォーマットはカスタマイズ可能ですか？**  
  `JsonSaveOptions` クラスは複数のフラグを提供しています。完全に独自のスキーマが必要な場合は、`ocrEngine.RecognitionResult.Regions` を走査し、`System.Text.Json` を使って自分でオブジェクトをシリアライズできます。

## 結論

ここでは、C# で Aspose.OCR を使用して **画像からテキストを認識** し、**テキストを抽出**、**テキスト座標を取得**、そして最終的に **レシートを JSON に変換** する方法を示しました。全体のフローは単一の実行しやすいコンソールアプリに収められており、プロトタイプや大規模システムの構成要素として最適です。

次のステップは？ JSON をバウンディングボックスを描画するフロントエンドに渡す、あるいは経費レポートサービスに組み込んでみてください。また、異なる画像フォーマット（PNG、TIFF）を試したり、レシートフォルダーをバッチ処理したりすることもできます。

OCR、Aspose、JSON の取り扱いについてさらに質問がありますか？以下にコメントを残してください。コーディングを楽しんで！

![画像からテキストを認識するためのレシート画像例](receipt.jpg "レシート画像例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}