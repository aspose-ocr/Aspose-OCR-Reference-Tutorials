---
category: general
date: 2026-05-06
description: Aspose OCR と GPU サポートを使用して画像からテキストを抽出します。セットアップ、コード、ベストプラクティスを網羅した C#
  OCR チュートリアルで、テキストを迅速に抽出する方法を学びましょう。
draft: false
keywords:
- extract text from image
- how to extract text
- c# ocr tutorial
- Aspose OCR GPU
- C# image processing
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、GPUアクセラレーションを活用した高速なテキスト抽出方法と、ステップバイステップでテキストを抽出する手順を解説します。
og_title: C#で画像からテキストを抽出する – 完全OCRチュートリアル
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを抽出する – 完全OCRチュートリアル
url: /ja/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像からテキストを抽出 – 完全OCRチュートリアル

画像から **画像からテキストを抽出** する必要があったことはありますか、しかしどのライブラリが速度 *と* 精度の両方を提供するか分からなかったことはありませんか？ あなたは一人ではありません—多くの開発者が文書デジタル化パイプラインを構築する際にこの壁にぶつかります。良いニュースは、Aspose OCR を使用すれば、事実上すべてのビットマップからテキストを取得でき、数行のコードで GPU 加速がバックグラウンドで動作します。

この **C# OCR チュートリアル** では、必要なすべてを順に解説します：NuGet パッケージのインストール、GPU モードの設定、マルチページ TIFF の処理まで。最後まで読めば、古典的な「テキスト抽出方法」への質問に自信を持って答えられ、任意の .NET プロジェクトに組み込める実行可能なサンプルが手に入ります。

## 学べること

- Aspose OCR を使用して画像ファイルから **テキスト抽出方法** の正確な手順。
- 大幅なパフォーマンス向上のために GPU 加速を有効にする方法。
- 一般的な落とし穴（例：CUDA ドライバーが見つからない）と迅速な対処法。
- バッチ処理や異なる画像フォーマット向けにソリューションを拡張する方法。

> **プロチップ:** 専用 GPU がない開発マシンでも、コードを CPU モードで実行できます—`UseGpu = false` に設定するだけです。チュートリアルの残りの部分は同じです。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.7.2+) | Aspose OCR は最新のランタイムを対象としています。 |
| Visual Studio 2022 (or any IDE you prefer) | デバッグや NuGet 統合に便利です。 |
| NVIDIA GPU with CUDA 11+ (optional but recommended) | `UseGpu = true` 設定に必要です。 |
| Aspose.OCR NuGet package (`Aspose.OCR` and `Aspose.OCR.Gpu`) | OCR エンジンと GPU サポートを提供します。 |

これらのいずれかが欠けていると、コンパイル時エラーや実行時例外が発生します—慌てないでください、チュートリアルで復旧方法を説明します。

## 手順 1: Aspose OCR パッケージのインストール

ターミナルでプロジェクトフォルダーを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

これら 2 つのパッケージは、コア OCR 機能とオプションの GPU 加速レイヤーを提供します。インストール後、`.csproj` にアセンブリが参照されているのが確認できます。

## 手順 2: GPU 用 OCR 設定の構成

ここで `OcrEngineSettings` オブジェクトを作成し、エンジンに GPU 使用を指示します。これが **画像からテキストを抽出** のパフォーマンス向上の魔法です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

// Configure OCR to run on the first available GPU (device ID 0)
var ocrSettings = new OcrEngineSettings
{
    UseGpu = true,          // Turn on GPU acceleration
    GpuDeviceId = 0         // Optional: specify which GPU to use
};
```

> **なぜ重要か:** GPU を有効にすると、重い処理（ピクセル前処理、ニューラル推論）が CPU からグラフィックカードへ移り、処理時間が秒単位からミリ秒単位に短縮されることが多いです。

互換性のある GPU がない場合は、`UseGpu = false` に設定すれば、エンジンはコード変更なしで CPU モードにフォールバックします。

## 手順 3: OCR エンジンの初期化

設定が整ったら、`OcrEngine` をインスタンス化します。このオブジェクトは構成を保持し、処理する各画像で再利用されます。

```csharp
// Create the OCR engine with the previously defined settings
var ocrEngine = new OcrEngine(ocrSettings);
```

設定とエンジンを分離する理由が気になるかもしれません。答えは柔軟性です—`ocrSettings` を差し替えることで、同じ `ocrEngine` インスタンスを複数のファイルで再利用でき、必要に応じて GPU と CPU をリアルタイムに切り替えられます。

## 手順 4: 画像からテキストを認識

これが **テキスト抽出方法** の核心です。`RecognizeImage` を呼び出し、解析したいファイルのパスを渡します。このメソッドは抽出された文字列と信頼度スコアを含む `OcrResult` を返します。

```csharp
// Replace with the actual path to your image file
string imagePath = @"C:\Images\sample_multi_page.tif";

// Perform OCR – this will extract text from the image
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

**エッジケース:** 画像がマルチページ TIFF の場合、Aspose OCR は自動的に各ページを処理し結果を連結します。ページごとの出力が必要な場合は `ocrResult.PageResults` を確認してください。

## 手順 5: 抽出したテキストの表示または保存

最後に、結果をコンソールに出力したり、ファイルに書き込んだり、別のシステムに渡したりします。このチュートリアルでは単にコンソールに出力します。

```csharp
// Show the extracted text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、以下のような出力が表示されます：

```
=== OCR Output ===
Invoice #12345
Date: 04/30/2026
Total: $1,250.00
...
```

これで Aspose OCR を使用して **画像からテキストを抽出** に成功した瞬間です。

## 完全動作例

以下は、すべての要素を組み合わせた完全な実行可能コンソールアプリケーションです。新しい `Program.cs` ファイルに貼り付けて **F5** を押してください。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure OCR settings (GPU enabled)
            var ocrSettings = new OcrEngineSettings
            {
                UseGpu = true,          // Turn on GPU acceleration
                GpuDeviceId = 0         // Optional: specify which GPU to use
            };

            // 2️⃣ Initialize the OCR engine with those settings
            var ocrEngine = new OcrEngine(ocrSettings);

            // 3️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY\sample_multi_page.tif";

            // 4️⃣ Perform OCR – this extracts the text
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Output the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 期待される出力

鮮明な印刷済み請求書に対してプログラムを実行すると、請求書項目のプレーンテキスト表現が得られます。画像がぼやけている、または言語がサポートされていない場合、`ocrResult.Text` に文字化けが含まれることがあります。その場合は画像前処理（例：二値化）を調整するか、別の言語モデルに切り替えて精度を向上させてください。

## よくある質問とトラブルシューティング

**Q: アプリが “CUDA driver not found” でクラッシュします。**  
A: CUDA 11+ がインストールされており、GPU ドライバーが CUDA バージョンと一致していることを確認してください。コマンドプロンプトで `nvidia-smi` を実行すれば、ドライバーが認識されているか確認できます。

**Q: 画像フォルダー全体を処理するにはどうすればよいですか？**  
A: `RecognizeImage` 呼び出しを `foreach (var file in Directory.GetFiles(folder, "*.tif"))` ループで囲みます。効率のために同じ `ocrEngine` インスタンスを再利用することを忘れないでください。

**Q: PDF からテキストを抽出できますか？**  
A: Aspose OCR では直接はできませんが、まず PDF ページを画像に変換（Aspose.PDF や他のライブラリを使用）し、その画像を OCR パイプラインに渡すことができます。

**Q: 英語以外の言語でテキストを抽出したい場合は？**  
A: `RecognizeImage` を呼び出す前に `ocrEngine.Language = OcrLanguage.Spanish`（またはサポートされている任意の言語）を設定してください。

## チュートリアルの拡張

- **バッチ処理:** GPU が利用できない場合、`Parallel.ForEach` と組み合わせてマルチコア処理を行います。
- **ポストプロセッシング:** 正規表現を使用して電話番号、日付、金額などをクリーンアップします。
- **統合:** 抽出した文字列をデータベースや Azure Cognitive Search インデックスに投入し、検索可能なドキュメントにします。

## 結論

これで、画像から **テキスト抽出方法** を正確に示し、GPU 加速を活用し、マルチページファイルもスムーズに処理できる堅実な **C# OCR チュートリアル** が手に入りました。上記の手順に従えば、Aspose OCR を任意の .NET プロジェクトに統合し、画像をすぐに検索可能で編集可能なテキストに変換できます。

次のチャレンジに挑みますか？ GPU フラグをオフにして性能差を確認したり、PNG や JPEG など異なる画像フォーマットで実験してみてください。可能性は無限です—ハッピーコーディング！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}