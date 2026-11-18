---
category: general
date: 2026-06-19
description: C#でAspose OCRを使用して画像からテキストを抽出し、画像にOCRを実行し、スキャンからテキストを認識する方法 – ステップバイステップガイド.
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出し、画像にOCRを実行し、スキャンからテキストを認識する方法 – 完全ガイド
og_title: C#でAspose OCRを使用する方法 – 画像からテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: C#でAspose OCRを使用する方法 – 画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使用する方法 – 画像からテキストを抽出する

ドキュメントの写真から文字を取り出す **Aspose の使い方** を知りたくありませんか？ 同じ疑問を抱いたことがある人はたくさんいます。このチュートリアルでは、画像からテキストを抽出し、バッチで OCR を実行し、数行の C# だけでスキャン画像の文字を認識する実践的なエンドツーエンド例を順を追って解説します。

まず Aspose OCR エンジンをセットアップし、JPEG ファイルのリストを渡し、最後に各結果をコンソールに出力します。これで、どの .NET プロジェクトにも貼り付けられる再利用可能なスニペットが完成します—不明な手順や不足している参照はありません。

## 必要なもの

始める前に、以下を用意してください。

* .NET 6.0 SDK 以降（コードは .NET Core と .NET Framework のどちらでも動作します）  
* 有効な **Aspose.OCR** NuGet パッケージ（Aspose のウェブサイトから無料トライアルキーを取得できます）  
* テキストが含まれるスキャン画像または写真が入ったフォルダー（JPEG または PNG が OK）  
* お好きな IDE—Visual Studio、Rider、あるいは VS Code でも構いません。

以上です。重い OCR ライブラリや外部コマンドラインツールは不要です。Aspose と数行のコードだけで完結します。

## 手順 1: Aspose.OCR NuGet パッケージをインストール

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新バージョン（2026 年 6 月時点で 22.9）を取得し、`.csproj` に参照を追加します。Visual Studio の UI を使う場合は **Dependencies → Manage NuGet Packages** を右クリックし、 “Aspose.OCR” を検索してください。

> **プロのコツ:** ライセンスの有効期限に注意しましょう。無料トライアルは 30 日間有効で、その後は商用キーが必要です。

## 手順 2: OCR エンジンを構成 – “Aspose の使い方” はここから

パッケージが導入できたら、OCR エンジンを作成し、認識対象の言語を指定します。多くの場合英語で十分ですが、Aspose は 70 以上の言語に対応しています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

`OcrEngine` を `using` 文でラップするのはなぜでしょうか？ それは `IDisposable` を実装しているからです。`Dispose` すると、OCR エンジンが内部で確保したネイティブリソース（アンマネージドメモリなど）が解放されます—これは、1 分間に数十ファイルを処理する本番サービスでは必須です。

## 手順 3: 画像パスのリストを作成 – **画像で OCR を実行** の準備

次に、処理したいすべての画像を指す `List<string>` を用意します。以下のように手動で作成するか、 `Directory.GetFiles` で動的に生成できます。

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

実行ファイルからの相対サブフォルダーに画像がある場合は、 `Path.Combine` を使ってパスを組み立ててください。重要なのはリストの順序が保持されることです—Aspose は同じ順序で結果を返すため、入力と出力の対応が簡単になります。

## 手順 4: **画像で OCR を実行** を一括処理

多数のファイルを一度に処理したいとき、Aspose OCR は特に威力を発揮します。`ProcessBatch` メソッドは先ほど作成したリストを受け取り、`IList<OcrResult>` を返します。各要素には認識テキスト、信頼度スコア、必要に応じてバウンディングボックスが含まれます。

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

内部では、Aspose がネイティブスレッドを生成して処理を高速化するため、CPU コア数にほぼ比例したスケーリングが期待できます。大規模なワークロードの場合は `OcrEngineConfig.ThreadCount` プロパティでスレッド数を調整できますが、デフォルトの自動検出でほとんどのデスクトップシナリオは問題ありません。

## 手順 5: **スキャンから認識したテキスト** を表示 – 出力を検証

最後に、結果を走査して各テキストブロックをコンソールに出力します。元のファイル名も併せて表示するので、どの出力がどのスキャンに対応しているかが一目で分かります。

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

プログラムを実行すると、コンソールに次のような出力が表示されます。

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

これが **Aspose の使い方** で、スキャンした PDF や JPEG の山を検索可能で編集可能なテキストに変換する甘美な瞬間です。

![Aspose OCR の使用例出力](image-placeholder.png "Aspose OCR の使用例出力")

*画像代替テキスト: 「Aspose OCR の使用例出力 – スキャンから認識されたテキストを示す」*

## オプション: 精度調整 – **画像からテキストを抽出** したいときのブースト

文字が抜けていたり文字化けしている場合は、次の設定を試してみてください。

| 設定 | 機能 | 使用シーン |
|------|------|------------|
| `ocrConfig.DetectOrientation = true` | 画像が横向きの場合に自動回転 | 縦書きのスキャン本など |
| `ocrConfig.Preprocess = true` | コントラスト強化とノイズ除去を適用 | スマホで撮影した低品質写真 |
| `ocrConfig.CharacterWhitelist = "0123456789"` | 認識対象を数字のみに限定 | 請求書の合計金額やシリアル番号抽出 |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | ページ全体を 1 つのテキストブロックとして扱う | レイアウトがシンプルで高速化したいとき |

`ocrResults[i].Confidence` で取得できる信頼度が 0.9 以上になるまでフラグを調整してください。元画像が良好であるほど OCR 結果も向上します—Photoshop や ImageMagick で少し前処理を行うだけで、デバッグ時間を大幅に削減できます。

## 完全動作サンプル – コピペで使えるコード

以下はそのままコンパイルして実行できる完全版プログラムです。ファイルパスだけ自分の環境に合わせて置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

`dotnet run` でビルドし、コンソールにクリーンで検索可能なテキストが流れ込む様子をご確認ください。これが **Aspose の使い方** 全体を 50 行未満のコードで実現したフローです。

## よくある落とし穴と対策

* **`ocrResults[i]` で NullReferenceException** – エンジンがファイルを開けなかったことが原因です（パスが間違っている、サポート外フォーマット）。拡張子とアクセス権を再確認してください。  
* **文字化け（“�”）** – 画像が非 UTF‑8 エンコーディングで保存されている可能性があります。ロスレス PNG に変換するか、 `ocrConfig.Preprocess` を有効にしてください。  
* **パフォーマンス低下** – 100 枚以上のバッチの場合は `Parallel.ForEach` とスレッドごとに別々の `OcrEngine` インスタンスを使って並列処理を検討してください。各スレッドが自分専用のエンジンを持てば、Aspose はスレッドセーフです。

## 次のステップ – さらに深掘り

**Aspose の使い方** で OCR の基本をマスターしたら、次のテーマにも挑戦してみましょう。

* **検索可能 PDF へのエクスポート** – `Aspose.Pdf` を使って認識テキストを PDF に埋め込み、スキャン文書を本格的に検索可能にします。  
* **Azure Functions との統合** – 新しい画像が Azure Blob にアップロードされたときに自動で OCR をトリガーします。  
* **AI 言語モデルとの連携** – 抽出したテキストを ChatGPT や Claude に渡して要約、エンティティ抽出、翻訳などを実行します。

これらのトピックでも、**画像からテキストを抽出**、**画像で OCR を実行**、**スキャンから認識したテキスト** といったキーワードが自然に出てくるので、パターンを覚えながらスキルを広げられます。

## 結論

本稿では、**Aspose の使い方** で画像からテキストを抽出し、バルクで OCR を実行し、最小限のコードでスキャンから文字を認識する完全なプロダクション向けサンプルを紹介しました。エンジンの設定、ファイルパスリストの作成、バッチ処理、結果出力までの流れを習得すれば、あらゆる文書自動化プロジェクトの土台が手に入ります。

ぜひ試して設定を微調整し、紙の山を検索可能なデジタル資産に変換してみてください。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全動作コードが含まれているので、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/ocr-operation-with-folder/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}