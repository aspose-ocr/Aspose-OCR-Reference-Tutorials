---
category: general
date: 2026-03-17
description: C#でAspose OCRを使用してPNGからテキストを抽出します。画像からテキストを読み取り、レシートのOCRを処理し、GPUアクセラレーション付きのOCRエンジンを作成する方法を学びましょう。
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: ja
og_description: Aspose OCR を使用して PNG からテキストを抽出します。このガイドでは、画像からテキストを読み取る方法、レシート OCR
  を処理する方法、そして OCR エンジンを効率的に作成する方法を示します。
og_title: PNGからテキストを抽出 – OCRで画像から文字を読み取る
tags:
- OCR
- CSharp
- Aspose
title: PNGからテキストを抽出 – OCRで画像からテキストを読み取る
url: /ja/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを抽出 – 画像からテキストを読み取る（OCR）

PNGから**テキストを抽出**したいけれど、どのライブラリが信頼できる結果を出すか分からないことはありませんか？開発者はしばしば「レシートのような画像ファイルからカスタムのニューラルネットを作らずにテキストを読む方法は？」と質問します。良いニュースは、Aspose OCR が重い処理を代行してくれ、GPU を使って速度を向上させることもできる点です。

このチュートリアルでは、**レシート OCR の処理**に必要なすべてを解説します。NuGet パッケージのインストールから、PNG ファイルを理解できる OCR エンジンの作成まで。最後には、レシート画像を読み取り、認識されたテキストをコンソールに出力し、さまざまなシナリオに合わせてエンジンを調整する方法を示す、自己完結型のコンソール アプリが完成します。外部ドキュメントは不要、純粋なコードと明快な説明だけです。

## 前提条件

- .NET 6.0 SDK（または最近の .NET バージョン）  
- Visual Studio 2022 または C# 拡張機能付き VS Code  
- 最新ドライバーがインストールされた対応 NVIDIA GPU（オプション、GPU モード推奨）  
- **Aspose.OCR** NuGet パッケージ（`dotnet add package Aspose.OCR`）  

GPU がなくても CPU モードでサンプルを実行できます。その場合は GPU 設定行をスキップしてください。

## 手順 1: Aspose.OCR をインストールしプロジェクトをセットアップ

まず、コンソール プロジェクトを作成し、Aspose OCR ライブラリを導入します。

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

ポイント: `Aspose.OCR` パッケージには OCR エンジン、画像ローダー、オプションの GPU サポートがすべて含まれます。NuGet 経由で追加すれば、最新の安定版（2026 年 3 月時点で 23.10）を取得できます。

## 手順 2: 名前空間をインポートし OCR エンジンを作成

**Program.cs** を開き、必要な `using` ディレクティブを追加します。その後、エンジンのインスタンスを生成します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**プロのコツ:** GPU が無いマシンで `System.DllNotFoundException` が発生した場合は、`EngineMode` と `GpuDeviceId` を設定している 2 行をコメントアウトしてください。エンジンは自動的に CPU にフォールバックします。

## 手順 3: テキストを抽出したい PNG 画像を読み込む

Aspose OCR はファイルパス、ストリーム、バイト配列から直接画像を読み取れます。このデモではローカルのレシート画像をロードします。

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

ファイルが存在しない場合のガード処理に注目してください。実際のアプリでは、単に終了するのではなく、ユーザーに分かりやすい UI メッセージを表示するのが一般的です。

## 手順 4: OCR 認識を実行

テキスト抽出はたった 1 回のメソッド呼び出しで行われます。エンジンは生文字列、信頼度スコア、レイアウト情報を含む `OcrResult` オブジェクトを返します。

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

`ocrResult.Text` を確認する理由: 低品質の PNG では空文字列が返ることがあり、何も出力しないよりはユーザーにその旨を伝える方が親切です。

## 手順 5: 認識結果のテキストを出力

最後に、抽出した文字列をコンソールに表示します。ファイルやデータベースへの書き込み、別サービスへの送信も可能です。

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

プログラムを実行（`dotnet run`）すると、次のような出力が得られます。

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

これが **PNG ファイルからテキストを抽出**するための **完全なソリューション** であり、レシートのような画像から **テキストを読み取る** 方法を学びました。

## オプション: OCR エンジンの微調整（上級者向け）

特定のフォントやノイズの多い背景に対して精度を上げたい場合は、以下の設定を調整してください。

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

バッチ処理で **レシート OCR** を行う際、スキャン品質が一定でないケースに特に有効です。

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **GPU ドライバーが見つからない** | エンジンが CUDA をロードしようとして DLL が見つからない | 最新の NVIDIA ドライバーをインストールするか、`EngineMode.Gpu` 行を削除して CPU モードに切り替える |
| **画像パスが間違っている** | `ImageStream.FromFile` がファイル未検出で例外をスロー | パスを必ず検証する（手順 3 を参照）か、クロスプラットフォーム安全のために `Path.Combine` を使用 |
| **ぼやけたレシートで信頼度が低い** | OCR エンジンが文字を判別できない | `EnableImagePreprocessing` を有効にし、必要に応じて DPI を上げてからエンジンに渡す |
| **長時間稼働するサービスでメモリリーク** | 各 `OcrEngine` がアンマネージドリソースを保持 | 使用後にエンジンを破棄する: `using var ocrEngine = new OcrEngine();` |

## 完全動作サンプル（コピー＆ペースト）

以下は **Program.cs** に貼り付け可能な **全コード** です。オプションの調整はコメントアウトされた状態で用意しています。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

保存して `dotnet run` を実行すれば、レシートの内容がコンソールに表示されます。

![extract text from png example](receipt.png "extract text from png example")

*上の画像は、コードで処理できるサンプルのレシート PNG を示しています。*

## まとめ

Aspose OCR を使って **PNG からテキストを抽出**する方法、**画像からテキストを読み取る**手順、そして **レシート OCR** の全工程を解説しました。GPU 加速のオプションも含め、**OCR エンジンを自分で作成**することで、設定・パフォーマンス・エラーハンドリングをフルコントロールできます。

## 次に挑戦できることは？

- **バッチ処理**: PNG レシートが格納されたディレクトリを走査し、各結果を CSV に書き出す。  
- **Azure Functions との統合**: このコンソール アプリをサーバーレス エンドポイントに変換し、画像アップロードを受け付ける。  
- **多言語対応**: `Language.English` を `Language.Spanish` に差し替えるか、カスタム辞書を追加。  
- **後処理**: 正規表現を使って、認識文字列から合計金額、日付、税番号などのフィールドを抽出。

ぜひ色々試してみてください。OCR は正しいノブを回すと驚くほど柔軟なツールです。問題があればコメントを残すか、Aspose OCR API リファレンスで詳細を確認してください。

Happy coding, and enjoy turning those stubborn PNG receipts into searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}