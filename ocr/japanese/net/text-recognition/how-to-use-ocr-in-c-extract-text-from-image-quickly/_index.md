---
category: general
date: 2026-04-08
description: C#でOCRを使用して画像ファイルからテキストを抽出する方法。JPGからテキストを読み取り、画像からテキストへの変換を実行し、Aspose.Ocrで画像を文字列に変換する方法を学びます。
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from jpg
- image to text conversion
- convert image to string
language: ja
og_description: C#でOCRを使用して画像からテキストを抽出する方法。このチュートリアルでは、JPGからテキストを読み取る方法、画像からテキストへの変換、そして画像を文字列に変換する方法を示します。
og_title: C#でOCRを使用する方法 – 画像からテキストへの高速ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – 画像からテキストを素早く抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – 画像からテキストを素早く抽出する

画像から文字を取り出す必要があるとき、**OCR の使い方**を考えたことはありませんか？スキャンしたレシートや看板のスクリーンショット、ヒンディー語の新聞ページなど、テキストをコピー＆ペーストできない状況かもしれません。これは典型的な *画像からテキストを抽出* シナリオで、クラウドサービスやコンピュータビジョンの博士号は不要だというのが朗報です。

このガイドでは、Aspose.OCR ライブラリを使用した **OCR の使い方** を示す完全な実行可能サンプルを順に解説し、JPG からテキストを読み取り、最終的に **画像からテキストへの変換** を行って純粋な C# 文字列を取得します。最後まで読むと、**画像を文字列に変換**する方法が正確に分かり、次に取り組む OCR 関連プロジェクトのしっかりした基盤が手に入ります。

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+ – API は同じように動作します）
- **Visual Studio 2022** またはお好みのエディタ
- **Aspose.OCR** NuGet パッケージ（`Install-Package Aspose.OCR`）
- サンプル画像（`hindi_sample.jpg`）をディスク上の任意の場所に配置
- 少しの好奇心と実験する意欲

以上です—追加のサービスやインターネット呼び出しは不要です（**オフラインモード**も有効にします）。さあ始めましょう。

## OCR の使用方法：環境設定

**OCR を使用**する前に最初に行うべきことは、ライブラリをプロジェクトに導入することです。

```csharp
// Open a terminal in your solution folder and run:
dotnet add package Aspose.OCR
```

> **重要な理由:** パッケージを追加すると、言語パック、画像デコード、OCR エンジン本体に必要なすべてのネイティブバイナリが Aspose から取得されます。この手順を省略すると、実行時に `FileNotFoundException` が発生します。

パッケージをインストールしたら、`Program.cs`（または任意のクラス）を開き、必要な `using` ディレクティブを追加します：

```csharp
using Aspose.Ocr;
using System;
```

これで **JPG からテキストを読み取る** 準備が整いました。

## 画像からテキストを抽出 – ヒンディー語 JPG の認識

以下は、コアワークフローを示す **完全な、自己完結型** プログラムです。コメントに注意してください；各行の *理由* が説明されています。

```csharp
using Aspose.Ocr;
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance – this object holds all settings.
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable offline mode so the engine works without network access.
            //    Offline mode uses the language data that ships with the package.
            ocrEngine.Options.OfflineMode = true;

            // 3️⃣ Choose the language. "hi" is the ISO code for Hindi.
            //    You can replace this with "en" for English, "fr" for French, etc.
            ocrEngine.Language = "hi";

            // 4️⃣ Provide the path to the image you want to process.
            //    Make sure the file exists; otherwise you'll get an exception.
            string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";

            // 5️⃣ Run the recognition. The result object contains the extracted text.
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 期待される出力

`hindi_sample.jpg` にフレーズ “नमस्ते दुनिया”（Hello World）が含まれている場合、コンソールには次のように表示されます：

```
=== OCR Result ===
नमस्ते दुनिया
```

これが求めていた **画像からテキストへの変換** です—余計な手順はなく、保存・検索・表示できるクリーンな文字列が得られます。

## JPG からテキストを読み取る – オフラインモードの扱い方

「インターネットがないマシンでどうする？」と疑問に思うかもしれません。そのようなときに **オフラインモード** が活躍します。`ocrEngine.Options.OfflineMode = true` を設定すると、Aspose はクラウドエンドポイントにアクセスする代わりに同梱の言語パックを使用します。これにより以下が保証されます：

- **決定的なパフォーマンス** – レイテンシのスパイクがありません。
- **コンプライアンス** – データはホストマシンから外部に出ません。
- **ポータビリティ** – バイナリを隔離環境に配布できます。

最新の言語アップデートのためにオンラインモードに戻す必要がある場合は、`OfflineMode = false` に設定し、`ocrEngine.License = new License("your_license_file.lic")` で API キーを提供すれば完了です。

## 画像からテキストへの変換 – 結果を文字列として取得する

`ocrResult.Text` プロパティはすでに **画像を文字列に変換** した結果を提供しますが、いくつかの便利な処理を加えることもできます：

```csharp
string rawText = ocrResult.Text;

// Trim whitespace and normalize line endings for easier downstream processing.
string cleanedText = rawText.Trim().Replace("\r\n", "\n");

// Optional: Remove any non‑Unicode characters that the OCR might have mis‑read.
cleanedText = System.Text.RegularExpressions.Regex.Replace(cleanedText, @"[^\u0000-\uFFFF]", string.Empty);

Console.WriteLine("Cleaned OCR Output:");
Console.WriteLine(cleanedText);
```

これらの追加手順により、生の OCR 出力をデータベース保存や検索インデックスへの投入、翻訳 API への入力に適した整った文字列に変換します。

## よくある落とし穴とプロのコツ

| Issue | Why it Happens | How to Fix / Avoid |
|-------|----------------|--------------------|
| **ファイルが見つからない** | パスが間違っているか画像が存在しない。 | `Path.Combine` を使用し、`RecognizeImage` を呼び出す前に `File.Exists(imagePath)` で確認してください。 |
| **文字化け** | 解像度が低い画像または未対応の言語パック。 | 画像を前処理します：DPI を上げる、グレースケールに変換する、または `ocrEngine.Options.ImagePreprocess = true` を使用してください。 |
| **結果が空** | 必要な言語データがないオフラインモード。 | 言語コード（`ocrEngine.Language`）が同梱パックと一致していることを確認するか、Aspose からパックをダウンロードして `ocrEngine.Options.LanguageDataPath` を設定してください。 |
| **パフォーマンス低下** | エンジンを再利用せずに大量バッチ処理を行っている。 | 複数の画像に対して単一の `OcrEngine` インスタンスを再利用し、必要な場合のみ `Language` を変更してください。 |
| **ライセンス例外** | 評価期間が過ぎたトライアル版を使用している。 | `ocrEngine.License = new License("Aspose.OCR.lic");` で有効なライセンスファイルを適用してください。 |

> **プロのコツ:** 多数の画像を処理する場合は、`Parallel.ForEach` ループで OCR 呼び出しをラップし、エンジンをスレッドセーフに保ちます（`ocrEngine.IsThreadSafe = true`）。これによりマルチコアマシンで処理時間を大幅に短縮できます。

## 完全動作例（すべての手順を1ファイルにまとめたもの）

コピー＆ペーストが好きな方のために、開始から終了までの全プログラムを、オプションのクリーンアップロジックも含めて示します：

```csharp
using Aspose.Ocr;
using System;
using System.IO;
using System.Text.RegularExpressions;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Verify the image exists
            string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }

            // Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                // Work offline – no network calls
                Options = { OfflineMode = true },

                // Set language (Hindi in this case)
                Language = "hi"
            };

            // Recognize the image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // Basic output
            Console.WriteLine("=== Raw OCR Result ===");
            Console.WriteLine(ocrResult.Text);

            // Clean the text for further use
            string cleaned = ocrResult.Text
                .Trim()
                .Replace("\r\n", "\n");
            cleaned = Regex.Replace(cleaned, @"[^\u0000-\uFFFF]", string.Empty);

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
    }
}
```

プログラムを実行します（プロジェクトフォルダーで `dotnet run`）。コンソールに生の文字列とクリーンアップされた文字列の両方が表示されます。これが Aspose.OCR を使用した **画像を文字列に変換** の本質です。

## 次に探求できる関連トピック

- **バッチ OCR 処理** – JPG フォルダーをループし、各結果をテキストファイルに書き出す。
- **言語検出** – `ocrEngine.Language` を設定する前にエンジンに言語を推測させる。
- **PDF OCR** – スキャンした PDF からテキストを抽出するために、各ページを画像に変換してから処理する。
- **Azure Functions との統合** – OCR をサーバーレス API として公開し、オンデマンドで画像からテキストへの変換を提供する。

## 結論

C# で **OCR の使い方** を、ライブラリのインストールからクリーンな **画像からテキストへの変換** の実行までカバーしました。これで **画像からテキストを抽出** する方法、**JPG からテキストを読み取る** 方法、そして **画像を文字列に変換** して下流処理に利用する方法が分かり、オフラインモードのおかげでインターネットに接続せずに実行できます。

別の言語パックで試したり、解像度の高い写真で試したり、ロジックを Web サービスにラップしたりしてみてください。可能性は無限で、構築できる堅実で引用に値する基盤が手に入っています。

![how to use OCR on a sample JPG image](image-placeholder.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}