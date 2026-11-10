---
category: general
date: 2026-02-19
description: Aspose OCR ライブラリを使用して、画像からテキストを抽出し、JPG からテキストを認識し、画像をテキストに変換する方法を示す C#
  OCR チュートリアル。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpg
- convert image to text
- extract text from jpg
language: ja
og_description: c# OCRチュートリアルで、画像からテキストを抽出し、JPGからテキストを認識し、Aspose OCRを使用して画像をテキストに変換する方法を案内します。
og_title: C# OCRチュートリアル – Aspose OCRで画像からテキストを抽出
tags:
- OCR
- C#
- Aspose
title: C# OCRチュートリアル – Aspose OCRを使用して画像からテキストを抽出する
url: /ja/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – Aspose OCR で画像からテキストを抽出する

髪をむしることなく、画像ファイルから **テキストを抽出** する方法を考えたことはありませんか？実際のアプリケーションでは、スキャンした請求書を読み取ったり、写真からシリアル番号を取得したり、単に JPG を検索可能なテキストに変換したりする必要があります。この **c# ocr tutorial** では、Aspose OCR ライブラリを使用してその方法を具体的に示し、*recognize text from jpg* と *convert image to text* の微妙な違いも解説します。

このガイドでは、Aspose OCR NuGet パッケージの設定方法、画像を読み込む小さなコンソールプログラムの作成方法、そして一般的な落とし穴（サポートされていない画像形式や言語設定など）の対処方法を学びます。最後まで読むと、任意の .NET プロジェクトに貼り付けて数秒で **extracting text from jpg** ファイルの抽出を開始できる動作するコードスニペットが手に入ります。

## 必要なもの

本題に入る前に、以下のものが準備できていることを確認してください：

| 前提条件 | 重要な理由 |
|--------------|----------------|
| .NET 6 SDK (or later) | 最新の C# 機能とパフォーマンス向上 |
| Visual Studio 2022 or VS Code | 快適な編集体験 |
| `sample.jpg` など、処理したい画像ファイル | OCR エンジンの実際の入力ソース |
| Aspose.OCR NuGet パッケージを取得するためのインターネット接続 | このライブラリは標準搭載されていないため、ダウンロードが必要です |

これらに馴染みがなくてもパニックになる必要はありません。以下の手順で各項目を順に説明しますし、コードはプレーンテキストエディタと `dotnet` CLI だけでも動作します。

## 手順 1: Aspose.OCR NuGet パッケージのインストール

まず最初に、OCR エンジンをプロジェクトに導入します。プロジェクトフォルダーでターミナルを開き、以下を実行してください：

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio を使用している場合は、プロジェクトを右クリック → *Manage NuGet Packages* → “Aspose.OCR” を検索し、*Install* をクリックすることもできます。

このコマンドは最新の安定版（2026年2月時点で 23.3）を取得し、`.csproj` に参照を追加します。追加で DLL をコピーする必要はなく、すべて .NET ランタイムが処理します。

## 手順 2: シンプルなコンソールアプリの雛形を作成

それでは、OCR ロジックをホストする最小限のコンソールアプリケーションの雛形を作成しましょう。`Program.cs` というファイルを作成（または既存のものを置き換え）し、以下のスケルトンを貼り付けてください：

```csharp
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the OCR routine from here.
            Console.WriteLine("Starting c# OCR tutorial...");
        }
    }
}
```

先頭にある `using System;` に注目してください。コンソール出力や後で発生し得る例外処理に必要です。

## 手順 3: OCR エンジンの初期化と言語設定

Aspose OCR は多数の言語をサポートしていますが、デモの多くは英語で十分です。エンジンは軽量なので、`Main` 内で直接インスタンス化できます。以下のコードを導入文の `Console.WriteLine` **の後** に追加してください：

```csharp
using Aspose.OCR;   // <-- add this using directive at the top of the file

// ...

// Step 3: Create an OCR engine and configure it for English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // you can switch to Language.Spanish, etc.
};
```

言語を明示的に設定する理由は何ですか？ 基礎となる認識アルゴリズムは言語固有の辞書を使用して精度を向上させるためです。この手順を省略しても動作する場合がありますが、英語以外のテキストでは結果が乱れることが多くなります。

## 手順 4: JPG 画像からテキストを認識

本チュートリアルの核心です – 画像ファイルをエンジンに渡し、テキスト結果を取得します。エンジン初期化直後に以下のコードを挿入してください：

```csharp
// Step 4: Define the path to the image you want to process
string imagePath = @"YOUR_DIRECTORY/sample.jpg";   // <-- replace with your actual path

try
{
    // Recognize the image. This method returns an OcrResult object.
    OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

    // Display the raw OCR output in the console
    Console.WriteLine("\n--- OCR Output ---");
    Console.WriteLine(ocrResult.Text);
}
catch (Exception ex)
{
    // If something goes wrong (file not found, unsupported format, etc.)
    Console.Error.WriteLine($"Error during OCR: {ex.Message}");
}
```

いくつかのポイントに注意してください：

* **`RecognizeImage`** は JPEG、PNG、BMP、TIFF などの一般的なラスタ形式に対応しています。そのため、このチュートリアルは余分な変換ステップなしで *recognize text from jpg* が可能です。
* このメソッドは `OcrResult` オブジェクトを返し、`Text`、`Confidence`、さらに必要に応じて位置情報の `BoundingBoxes` も含まれます。
* 呼び出しを `try/catch` でラップすることで、プログラムの堅牢性が向上し、ファイルが見つからなくてもアプリ全体がクラッシュしなくなります。

## 手順 5: アプリケーションを実行し出力を確認

ファイルを保存し、ターミナルに戻って以下を実行してください：

```bash
dotnet run
```

以下のような出力が表示されるはずです：

```
Starting c# OCR tutorial...

--- OCR Output ---
Hello, world!
This is a sample image containing text.
```

`sample.jpg` に表示されているテキストがコンソールに正確に出力されれば、成功です！数行の C# で **converted image to text** を実現できました。

### 出力が変な場合は？

* **Low confidence:** 画像解像度を上げるか、前処理（例: シャープ化、二値化）を適用してみてください。Aspose OCR には `PreprocessImage` メソッドがありますので、試してみる価値があります。
* **Wrong language:** `ocrEngine.Language` が画像の言語と一致しているか再確認してください。
* **Unsupported format:** ファイル拡張子が本当に JPEG であることを確認してください。`.jpg` 拡張子で保存された PNG などはパーサーを混乱させることがあります。

## 手順 6: 再利用可能な完全例のパッケージ化

以下は **完全で実行可能なプログラム** です。任意の新しいコンソールプロジェクトにコピー＆ペーストでき、必要な `using` 文、例外処理、各行を説明するコメントがすべて含まれています。

```csharp
// Program.cs
using System;
using Aspose.OCR;   // Aspose OCR library

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("=== c# OCR Tutorial – Extract Text from Image ===");

            // 1️⃣ Create OCR engine and set language (English by default)
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY/sample.jpg"; // <-- update this

            try
            {
                // 3️⃣ Perform OCR – this both *recognizes text from jpg* and *extracts text from image*
                OcrResult result = ocrEngine.RecognizeImage(imagePath);

                // 4️⃣ Output the recognized string – you’ve now *converted image to text*
                Console.WriteLine("\n--- OCR Result ---");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Friendly error message – helps when the file is missing or corrupted
                Console.Error.WriteLine($"Oops! Something went wrong: {ex.Message}");
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すれば、**extract text from jpg** の実演がライブで確認できます。

## ボーナス: フォルダー内の複数画像からテキストを抽出

スキャンした画像が多数あるディレクトリを一括処理したいことがよくあります。以下はフォルダー内のすべての `.jpg` ファイルをループし、OCR を実行して結果を同名の `.txt` ファイルに書き出す簡易拡張です。

```csharp
using System.IO;

// ...

string folderPath = @"YOUR_DIRECTORY"; // folder containing many jpg files

foreach (string file in Directory.GetFiles(folderPath, "*.jpg"))
{
    try
    {
        OcrResult batchResult = ocrEngine.RecognizeImage(file);
        string txtPath = Path.ChangeExtension(file, ".txt");
        File.WriteAllText(txtPath, batchResult.Text);
        Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {Path.GetFileName(file)}: {ex.Message}");
    }
}
```

このスニペットは、ドキュメント管理システムでよく求められる、*extract text from image* ファイルを大量に処理する実践的なシナリオを示しています。

## 画像イラスト（オプション）

記事に視覚的なヒントを入れたい場合は、コンソール出力のスクリーンショットを埋め込むことができます：

![c# OCR チュートリアル コンソール出力（抽出されたテキスト）](/images/ocr-console.png)

*Alt text には SEO 対策のための主要キーワードが含まれています。*

## よくある質問とエッジケース

**Q: PDF でも動作しますか？**  
**A:** 直接はできません。まず各 PDF ページを画像にラスタライズ（例: Aspose.PDF を使用）し、その画像を OCR エンジンに渡す必要があります。

**Q: 手書き文字はどうですか？**  
**A:** Aspose OCR は印刷文字に焦点を当てています。筆記体や手書きのメモについては、専用のモデル（例: Azure Cognitive Services や Google Vision）を使用する必要があります。

**Q: 出力エンコーディングを変更できますか？**  
**A:** `OcrResult.Text` は .NET の `string` で、デフォルトは UTF‑16 です。そのため、`File.WriteAllText(path, text, Encoding.UTF8)` のように好きなエンコーディングでファイルに書き出すことができます。

**Q: ライブラリは無料ですか？**  
**A:** Aspose には透かし付きのフル機能評価モードがあります。本番環境で使用するにはライセンスが必要ですが、API の使い方は変わりません。

## 結論

これで **c# OCR tutorial** は完了です。Aspose OCR のインストール、エンジンの初期化、そして JPEG を含む **extract text from image** ファイルの **extracting text from image** 手順を学び、*convert

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}