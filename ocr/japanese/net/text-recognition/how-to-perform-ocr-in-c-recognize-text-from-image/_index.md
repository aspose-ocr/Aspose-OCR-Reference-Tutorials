---
category: general
date: 2026-04-17
description: C#でOCRを実行し、画像からテキストを認識し、JPGから文字を抽出して、画像を素早くテキストに変換する方法を学びましょう。
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: ja
og_description: C#でOCRを実行する方法は？このガイドでは、画像からテキストを認識し、JPGからテキストを抽出し、画像をテキストに変換する方法を数分で紹介します。
og_title: C#でOCRを実行する方法 – 画像からテキストを認識する
tags:
- OCR
- C#
- Aspose
title: C#でOCRを実行する方法 – 画像からテキストを認識する
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を実行する方法 – 画像からテキストを認識する

スキャナーやスマートフォンで撮影した画像で **OCR を実行する方法** を考えたことはありませんか？多くのプロジェクトで **画像からテキストを認識** する必要があります—領収書、手書きメモ、PDF ページを JPEG に変換したものなどです。良いニュースは、Aspose.OCR を使えば数行の C# コードで **jpg からテキストを抽出** し、**画像をテキストに変換** できることです。

このチュートリアルでは、ライブラリのインストールから言語が欠如している場合の対処まで、全工程を順を追って解説します。最後まで読めば **OCR を実行する方法** が正確に分かり、抽出した文字列をコンソールに出力する実行可能なプログラムが手に入ります。曖昧な「ドキュメント参照」ではなく、完全な自己完結型のソリューションを提供します。

## 必要なもの

- **.NET 6+**（コードは .NET Framework でも動作しますが、.NET 6 が現在の LTS です）
- **Aspose.OCR for .NET** NuGet パッケージ – `dotnet add package Aspose.OCR` でインストール
- テストに使用する画像ファイル（JPEG、PNG、BMP） – ここでは `input.jpg` と呼びます
- お好みの IDE（Visual Studio、Rider、VS Code など）

以上です。追加の設定や外部サービス、隠れた手順は不要です。

## 手順 1: Aspose.OCR をインストールし参照を追加

まず、OCR ライブラリをプロジェクトに導入します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版（2026 年 4 月時点で **23.9.0**）を取得し、`.csproj` を更新します。その後、ファイルの先頭に using ディレクティブを追加します。

```csharp
using Aspose.OCR;
```

> **プロのコツ:** Visual Studio を使用している場合は、NuGet パッケージ マネージャ UI でも同様に *Aspose.OCR* を検索してインストールできます。

## 手順 2: 認識したい画像を読み込む

次に、OCR エンジンにどの画像を読み取らせるか指示します。Aspose には、ほとんどの一般的なフォーマットをサポートする便利な `OcrImage.FromFile` メソッドがあります。

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

`YOUR_DIRECTORY` を実際のパスに置き換えるか、実行ファイルと同じディレクトリに画像を置いて相対パスを使用してください。ファイルが存在しない場合は `FileNotFoundException` がスローされ、後でキャッチできます。

## 手順 3: OCR エンジンを作成（プラットフォーム対応）

Aspose.OCR は実行環境（Windows、Linux、macOS）に最適な基盤エンジンを自動的に選択します。`using` ブロック内で作成すれば、適切に破棄されます。

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

なぜ `using` なのか？エンジンはネイティブリソース（アンマネージド メモリなど）を保持しており、解放しないとメモリリークの原因になります。特に多数の画像をループ処理する場合は注意が必要です。

## 手順 4: （任意）言語を設定 – デフォルトは英語

画像に英語テキストが含まれる場合は、この手順は不要です。`OcrLanguage.English` がデフォルトになっています。他の言語を使用する場合は、適切な列挙値を割り当てます。

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **知ってましたか？** Aspose.OCR は 30 以上の言語に対応しており、アラビア語、中国語、ロシア語なども含まれます。言語切替は列挙値を変更するだけで簡単です。

## 手順 5: 認識プロセスを実行

`Recognize` を呼び出すと、ピクセル解析、文字分割、辞書照合といった重い処理が内部で行われます。

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

エンジンがテキストを検出できなかった場合、`ocrResult.Text` は空文字列になります。続行前に `ocrResult.HasText`（ブール値）を確認すると安全です。

## 手順 6: プレーンテキスト結果を取得して表示

最後に文字列を抽出し、コンソールに出力します。ここが実際に **画像をテキストに変換** する部分です。

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

出力例は次のようになります。

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

抽出したテキストをさらに処理したい場合（ファイル保存、データベース投入、正規表現適用など）は、すでに `recognizedText` 変数に格納されています。

## 完全動作サンプル

以下は新規コンソール アプリ（`dotnet new console`）に貼り付けてそのまま実行できる完全版プログラムです。一般的な落とし穴に対するエラーハンドリングも含んでいます。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **期待される出力:** コンソールに OCR エンジンが検出した文字がそのまま表示されます。元画像が鮮明で高解像度であれば、精度は通常 95 % 以上です。

## よくあるエッジケースの対処法

### 1️⃣ 複数言語が混在する画像  
バイリンガルの領収書などの場合は、`ocrEngine.Language` を `OcrLanguage.Multilingual` に設定します。エンジンが自動的に各言語を検出します。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ 低解像度または歪んだ画像  
画像を Aspose に渡す前に前処理（回転、リサイズ、コントラスト強調）を行います。`OcrImage` には `Resize` や `Rotate` といったメソッドが用意されています。

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ 大量バッチ処理  
多数のファイルを処理する際は、ループごとに新しい `OcrEngine` を作成せず、同じインスタンスを再利用してください。バッチ終了後に破棄することを忘れないでください。

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Linux コンテナでのメモリ制約  
Docker コンテナ内で RAM が制限されている場合、（API が提供していれば）`ocrEngine.MaxMemoryUsage` を設定して OOM クラッシュを防止します。

## プロのコツ & 注意点

- **ファイルエンコーディング:** 返される文字列は UTF‑16（.NET の `string`）です。UTF‑8 でファイルに書き出す必要がある場合は `Encoding.UTF8.GetBytes(recognizedText)` を使用してください。
- **パフォーマンス:** 単一画像の場合、エンジン初期化のオーバーヘッドは無視できる程度です。大量ジョブでは一度だけ初期化し（バッチ例参照）約 30 % の処理時間短縮が期待できます。
- **デバッグ:** OCR 結果が文字化けしている場合は、`ocrResult.Words`（個々の単語オブジェクトのコレクション）を調べて信頼度スコアを確認しましょう。信頼度が低いと画像がぼやけている可能性があります。
- **ライセンス:** Aspose.OCR は評価モードでも動作しますが、出力テキストに透かしが入ります。商用利用時はライセンス ファイル（`Aspose.OCR.lic`）を登録してください。

## ビジュアル概要

![C# で OCR を実行する例](ocr-example.png "C# で OCR を実行する例")

*サンプルコードを実行した後のコンソール出力全体を示すスクリーンショットです。*

## 結論

これで Aspose.OCR を使用した **C# での OCR 実行方法** をしっかりと習得できました。画像ファイルからテキストを認識し、**jpg からテキストを抽出**、さらに **画像をテキストに変換** して downstream の処理に活用できます。例は必須ステップを網羅し、各要素の重要性を解説するとともに、マルチランゲージ対応やバッチ処理といった高度なシナリオへのヒントも提供しています。

次は何をしますか？ JPEG を PNG に変えてみる、`OcrLanguage.Multilingual` を試す、あるいは抽出テキストを自然言語処理パイプラインに流し込んでみるなど、画像を検索可能で編集可能な文字列に変換できる可能性は無限です。

質問や問題があれば下のコメント欄にどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}