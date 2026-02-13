---
category: general
date: 2026-02-13
description: C#でAspose OCRを使用して画像からテキストを抽出します。JPGからテキストを読み取り、画像に対してOCRを実行する方法を、完全な実行可能サンプルで学びましょう。
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、jpg からテキストを読み取り、画像に対して OCR
  を実行する方法を、完全なコードサンプルとともに示します。
og_title: Aspose OCR を使用して画像からテキストを抽出する – C# クイックスタート
tags:
- C#
- OCR
- Aspose
title: Aspose OCRで画像からテキストを抽出 – C# クイックスタート
url: /ja/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト抽出 – C# クイックスタート

画像から **テキストを抽出** したいことはありませんか？どのライブラリを選べばよいか迷うことも多いでしょう。特に非ラテン文字のコンテンツを jpg ファイルから読み取る場合、開発者は常に頭を悩ませています。朗報です！Aspose OCR を使えば、数行の C# コードで画像ファイルに OCR を実行でき、必要に応じて言語パックを自動でダウンロードしてくれます。

このチュートリアルでは、Aspose OCR を使用して **画像からテキストを抽出** し、認識言語をロシア語に限定し、結果をコンソールに出力する完全なエンドツーエンドのサンプルを順を追って解説します。最後まで読めば、jpg ファイルからテキストを読み取り、任意のサイズの画像に OCR を実行し、最小限の変更で他言語にも対応できるようになります。

> **学べること**
> * .NET プロジェクトへの Aspose OCR のインストールと参照方法。  
> * **画像からテキストを抽出** する正確な手順 ― エンジンの初期化、言語の選択、`RecognizeImage` の呼び出し。  
> * エンジンを単一言語パックにロックする理由（速度・精度向上）。  
> * ファイルが見つからない、未対応フォーマットなどの一般的な落とし穴と、優雅なエラーハンドリング方法。  

## 前提条件

作業を始める前に、以下がマシンに揃っていることを確認してください。

| 必要条件 | 理由 |
|-------------|--------|
| .NET 6.0 SDK 以上 | Aspose OCR は .NET Standard 2.0+ を対象としているため、.NET 6 で最新ランタイム機能が利用できます。 |
| Visual Studio 2022（またはお好みの IDE） | デバッグに便利ですが、必須ではありません。 |
| Cyrillic テキストを含む画像ファイル（`cyrillic_sample.jpg`） | **jpg からテキストを読む** デモに使用します。 |
| インターネット接続（初回実行時のみ） | Aspose OCR が必要に応じて言語パックをダウンロードします。 |

上記が不足している場合は、今すぐ入手してください。SDK をインストールした後に再起動する必要はありません。

## 手順 1: Aspose OCR NuGet パッケージのインストール

まずは Aspose OCR ライブラリを入手します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版（2026 年 2 月時点で 23.12）を取得し、`.csproj` に追加します。パッケージにはコア OCR エンジンと軽量な言語パックダウンローダが含まれているため、アプリに巨大なファイルを同梱する必要はありません。

> **プロのコツ:** 社内プロキシ環境下で作業している場合は、コマンド実行前に `http_proxy` 環境変数を設定してダウンロードエラーを回避してください。

## 手順 2: コンソール アプリケーションの雛形作成

OCR ロジックをホストする最小限のコンソール アプリを作成します。`Program.cs`（または新規ファイル）を開き、以下の雛形を貼り付けてください。先頭の `using` ディレクティブは Aspose OCR の名前空間をインポートします。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

この時点でプロジェクトはビルドできますが、まだ何も実行されません。次のセクションで **画像で OCR を実行** するワークフローを具体化します。

## 手順 3: OCR エンジンの初期化（画像からテキストを抽出）

**画像からテキストを抽出** するには、まず `OcrEngine` インスタンスを作成します。Aspose OCR は初回使用時に言語リソースを遅延ダウンロードするため、バイナリサイズが小さく抑えられます。

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

なぜここで初期化し、静的フィールドにしないのか？`Main` 内で初期化すれば、ネイティブ依存関係が欠如している場合などの例外が早期に表面化し、デバッグが容易になります。

## 手順 4: 認識言語を限定する（JPG からテキストを読む）

スキャン対象のテキスト言語が分かっている場合（例: ロシア語）、`Language` プロパティを設定することで速度と精度の両方を向上させられます。特に **JPG からテキストを読む** ファイルがキリル文字を含む場合に有効です。

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

内部的には、最初にこの行が実行されたときにロシア語パックがダウンロードされます。以降の実行ではキャッシュされたパックが再利用されるため、ネットワーク負荷は初回以外発生しません。

> **言語をロックする理由**  
> * **パフォーマンス:** 選択したアルファベットに含まれない文字のスキャンをスキップします。  
> * **精度:** 言語固有のヒューリスティック（頻出単語頻度など）が適用され、誤認識が減少します。  

複数言語に対応したい場合は、カンマ区切りで列挙できます。例: `OcrLanguage.English | OcrLanguage.Russian`.

## 手順 5: 対象 JPG で OCR を実行（画像で OCR を実行）

いよいよ **画像で OCR を実行** します。JPG ファイルへのフルパスを指定してください。Aspose OCR は多数のフォーマット（`.png`, `.bmp`, `.tif` など）をサポートしていますが、ここではデモ用に `.jpg` に絞ります。

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

ファイルが見つからない場合、`RecognizeImage` は `FileNotFoundException` をスローします。チュートリアルを堅牢にするため、以下のように try‑catch でラップしましょう。

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

`RecognizeImage` メソッドは `OcrResult` オブジェクトを返し、その `Text` プロパティに抽出されたプレーンテキストが格納されます。レイアウト情報が必要な場合は `Boxes` でバウンディングボックスデータにもアクセスできます。

## 手順 6: 出力結果の確認

プログラムを実行（`dotnet run`）すると、次のような出力が得られるはずです。

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

出力が文字化けしている場合は、画像が鮮明かつ正しい言語が選択されているかを再確認してください。ぼやけた画像やコントラストが低い画像は、OCR 精度低下の最も一般的な原因です。

### エッジケースとよくある質問

| 状況 | 対処方法 |
|-----------|------------|
| **画像に複数言語が混在** | `ocrEngine.Language` に `OcrLanguage.English | OcrLanguage.Russian` のように組み合わせて設定します。 |
| **大量の画像を一括処理** | 同一の `OcrEngine` インスタンスを使い回すことで、言語データがキャッシュされ効率的に処理できます。 |
| **ヘッドレスサーバで実行** | UI は不要です。Aspose OCR は Docker や Azure Functions 上でも問題なく動作します。 |
| **精度を上げたい** | `ocrEngine.Options` を調整します（例: `ocrEngine.Options.Denoise = true`）。 |
| **未対応フォーマット** | `RecognizeImage` を呼び出す前に、画像を PNG か JPG などサポート形式に変換してください。 |

## 完全動作サンプル

以下は、上記手順をすべて組み込んだコピー＆ペースト可能なプログラムです。`Program.cs` として保存し、コマンドラインから実行してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**期待されるコンソール出力**（サンプル画像に「Пример текста на кириллице」というフレーズが含まれている場合）:

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

画像を英語の写真に差し替えて `ocrEngine.Language = OcrLanguage.English;` に変更すれば、同じコードで **JPG からテキストを読む** 英語版が動作します。

## ボーナス: 複数ファイルに対する OCR 実行

画像コレクションに対して **画像で OCR を実行** したいことが多いでしょう。以下はフォルダー内のファイルをループ処理する簡易スニペットです。

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

エンジンは既にダウンロード済みの言語パックを再利用するため、バッチ処理でも効率的に動作します。

## 結論

これで Aspose OCR を用いた **画像からテキストを抽出** するための、実務レベルのパターンが手に入りました。NuGet パッケージのインストールからエラーハンドリング、複数ファイルへのスケーリングまで網羅しています。**JPG からテキストを読む** アセットの処理はもちろん、PDF のスキャンやドキュメント自動化パイプラインにも同様の手法が適用できます。言語パックを差し替えるか OCR オプションを微調整すれば、さまざまなシナリオに対応可能です。

次のステップに挑戦してみましょう:

* 他言語（例: `OcrLanguage.ChineseSimplified`）で実験する。  
* `recognizedResult.Boxes` を使ってレイアウト情報を取得する。  
* OCR フローを ASP.NET Core API に統合し、他サービスからテキスト抽出をオンデマンドで呼び出せるようにする。

コーディングを楽しんで、画像が常に鮮明で完璧な OCR が得られるよう願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}