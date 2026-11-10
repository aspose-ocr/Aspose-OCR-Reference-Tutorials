---
category: general
date: 2026-03-21
description: Aspose OCR を使用して画像ファイルのデスキュー（傾き補正）とテキスト画像の認識方法を学びましょう。数行の C# コードで JPG
  をテキストに変換し、画像の回転を補正します。
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: ja
og_description: Aspose OCR を使用して画像の傾きを補正し、JPEG からテキストを抽出する方法。画像の回転を修正しながら JPG をテキストに変換するステップバイステップのガイドをご覧ください。
og_title: C#で画像の傾き補正を行う方法 – 簡単なAspose OCRチュートリアル
tags:
- OCR
- C#
- Aspose
title: C#で画像の傾き補正を行う方法 – Aspose OCRを使用した完全ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像の傾き補正を行う方法 – Aspose OCRを使用した完全ガイド

スキャナーから斜めに出力された画像ファイルの **how to deskew image**（傾き補正）について考えたことはありますか？ あなた一人ではありません—レシート、請求書、手書きメモからテキストを抽出しようとする多くの開発者がこの問題に直面しています。 良いニュースは、Aspose OCR を使えば画像の回転を補正し、数行のコードでクリーンで検索可能なテキストを取得できることです。

このチュートリアルでは、ライブラリのインストールから自動傾き補正の有効化、テキスト画像の認識、最終的に JPG をテキストに変換するまでの全プロセスを順に解説します。最後まで読むと、手動で回転させることなく **recognize text jpg** ファイルを処理できる、すぐに実行可能なコンソールアプリが手に入ります。

## 必要なもの

- **.NET 6.0** またはそれ以降（コードは .NET Core と .NET Framework の両方で動作します）  
- **Aspose.OCR for .NET** NuGet パッケージ – バージョン 23.12 以上を推奨  
- サンプルの **skewed JPEG**（例: `skewed_receipt.jpg`）をアプリが読み取れる場所に配置  
- Visual Studio、VS Code、またはお好みの C# エディタ  

他のサードパーティツールは必要ありません。ライブラリは内部で傾き補正、OCR、さらには言語検出まで処理します。

![画像の傾き補正例](/images/deskew-example.png "Aspose OCR を使用した画像の傾き補正")

## 手順 1: プロジェクトのセットアップと Aspose.OCR のインストール

整理のために、新しいコンソールプロジェクトを作成します：

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` 行は **Aspose.OCR** のバイナリとすべてのネイティブ依存関係を取得します。Windows の場合はネイティブ DLL が自動的に取得されますが、Linux/macOS では `libgdiplus` パッケージが必要になることがあります。ただし、これは一度だけのインストールです。

## 手順 2: 自動傾き補正の有効化（画像の回転補正）

`Program.cs` を開き、以下のコードに内容を置き換えます。ここで重要な行は `ocrEngine.Settings.Deskew = true;` です – これがエンジンに **how to deskew image** を自動的に行わせるフラグです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### なぜ傾き補正を有効にするのか？

スキャナーがページを斜めに供給すると、テキストのベースラインが傾きます。従来の OCR エンジンは各文字を傾いた状態で読み取るため、精度が大幅に低下します。`Deskew = true` を設定すると、Aspose OCR は内部で高速な Hough 変換を実行し、ビットマップを水平に回転させてから認識を行います。その結果は、Photoshop で手動で画像を回転させたのと同じですが、はるかに速く、完全に自動化されています。

## 手順 3: テキスト画像の認識と JPG のテキスト変換

`Recognize` 呼び出しは同時に二つのことを行います：

1. **Deskews** 画像（フラグをオンにしたため）。  
2. **Extracts** テキストコンテンツを抽出し、`OcrResult` オブジェクトとして返します。

`ocrResult.Text` をプレーンな文字列として扱い、ファイルに書き出したり、下流の処理パイプラインに渡したりできます。単語ごとの生の信頼度スコアが必要な場合は、`ocrResult.Words` が `Confidence` 値を含むコレクションを提供します。

### 出力例

`skewed_receipt.jpg` にシンプルなレシートが含まれていると仮定すると、以下のような出力が得られるかもしれません：

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

元の画像が約 7° 回転しているにもかかわらず、数字がきれいに揃っていることに注目してください。これはライブラリに組み込まれた **correct image rotation** の魔法です。

## 手順 4: サンプルの実行と結果の検証

コンパイルして実行します：

```bash
dotnet run
```

すべて正しく設定されていれば、抽出されたテキストがコンソールに表示されます。`FileNotFoundException` のような例外が発生した場合は、JPEG のパスを再確認し、ファイルが読み取り可能であることを確認してください。

### よくある落とし穴とプロのコツ

- **Large Images** – OCR のメモリ使用量は画像サイズに比例して増加します。エンジンに渡す前に、過大なファイル（例: 幅 > 3000 px）をリサイズしてください。  
- **Non‑Latin Scripts** – デフォルトではエンジンは英語を想定しています。別の文字体系で **recognize text image** が必要な場合は、`ocrEngine.Settings.Language = OcrLanguage.French;`（またはサポートされている任意の言語）を設定してください。  
- **Batch Processing** – 多数のファイルを処理する場合は同じ `OcrEngine` インスタンスを再利用してください。ファイルごとに新しいエンジンを作成すると不要なオーバーヘッドが発生します。  
- **Quality Check** – 傾き補正後、`ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` で補正されたビットマップをエクスポートし、回転修正を視覚的に確認できます。

## 完全動作例（すべてまとめて）

以下は `Program.cs` にコピー＆ペーストできる、完全で自己完結型のプログラムです。コメント、エラーハンドリング、そしてオプションで傾き補正した画像を保存する手順が含まれています。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

プログラムを実行すると **recognize text jpg** ファイルを処理し、傾きを自動的に補正して、クリーンで検索可能なテキストをコンソールに出力します。

## まとめ

これで、Aspose OCR を使用して **how to deskew image** ファイルを傾き補正し、内容を抽出する、実用的で本番環境向けのコードスニペットが手に入りました。この手法はレシート、請求書、スキャンした契約書、またはテキストが完全に水平でない任意の JPEG に対して機能します。

次に検討できるステップ：

- **Batch processing**: JPEG フォルダ内のファイルを一括処理し、各結果を `.txt` ファイルに書き出す（*convert jpg to text* に関連）。  
- OCR ステップを ASP.NET Core API に統合し、クライアントが画像をアップロードして JSON 形式のテキストを受け取れるようにする。  
- `ocrEngine.Settings.Language` や `ocrEngine.Settings.RecognitionMode` など、さまざまな OCR 設定を試して、英語以外の文書の精度を向上させる。

ぜひ試してみて、設定を調整し、エンジンに重い処理を任せてください。いつでも問題が発生したり、便利な最適化があれば下のコメントで共有してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}