---
category: general
date: 2026-03-29
description: C#でOCRを実行し、PNGファイルからテキストを読み取る方法。ロシア語テキストの抽出、PNGからのテキスト読み取り、そしてAspose
  OCRを使用したテキスト抽出方法を学びます。
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: ja
og_description: Aspose OCR を使用して C# で OCR を実行する方法。このガイドでは、png からテキストを読み取り、ロシア語テキストを抽出し、完全な
  C# OCR ソリューションを実装する方法を示します。
og_title: C#でOCRを実行する方法 – PNGテキスト抽出の完全ガイド
tags:
- OCR
- C#
- Aspose
title: C#でPNG画像にOCRを実行する方法 – ステップバイステップガイド
url: /ja/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG画像に対するOCRをC#で実行する方法 – 完全チュートリアル

スクリーンショットやスキャンした文書で **OCR を実行** したいが、C# でどこから始めればよいか分からないことはありませんか？ あなただけではありません。開発者は常に「外部サービスに送らずに PNG ファイルからテキストを読むにはどうすればいいのか？」と質問します。良いニュースは、Aspose.OCR を使えば **ロシア語テキストを抽出** でき、**png からテキストを読む**ことができ、数行のコードでクリーンな文字列を取得できるということです。

このチュートリアルでは、必要なすべての手順を解説します：ライブラリの設定、適切な言語モデルの選択、認識の実行、一般的な落とし穴の対処。最後まで読むと、英語、ロシア語、または Aspose がサポートする 70 以上の言語のいずれであっても、任意の PNG 画像から **テキストを抽出する方法** が分かります。余計な説明は省き、すぐにコンソールアプリに組み込める実用的で実行可能なサンプルを提供します。

---

## 学習内容

- Aspose.OCR NuGet パッケージをインストールし、参照する。
- OCR エンジンをデフォルトの自動ダウンロードモードで初期化する。
- Cyrillic 言語モデルを使用してエンジンを **ロシア語テキストを抽出** するよう構成する。
- ローカルの PNG ファイルで OCR を実行し、結果を表示する。
- 言語ファイルが見つからない場合のトラブルシューティングや精度向上のヒント。

**前提条件**: .NET 6+（または .NET Framework 4.7.2+）、Visual Studio 2022 または VS Code、そして初回実行時にインターネット接続が必要です（言語モデルは自動的にダウンロードされます）。

## ステップ 1 – Aspose.OCR パッケージのインストール

始めるには、プロジェクトに Aspose.OCR ライブラリを追加します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

あるいは、Visual Studio の UI を使用したい場合は、**Dependencies → Manage NuGet Packages** を右クリックし、**Aspose.OCR** を検索して **Install** をクリックします。

> **プロのコツ**: パッケージは数メガバイトしかなく、言語モデルは必要に応じて取得されるため、不要なファイルでアプリが肥大化することはありません。

## ステップ 2 – OCR エンジンの初期化（主要キーワードの実装）

エンジンの作成は簡単です。コンストラクタは自動的に *auto‑download mode* を有効にし、ローカルに存在しない言語を初めて要求した際に Aspose が自動で取得します。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **なぜ重要か**: デフォルトの auto‑download mode を使用することで手動でファイルを扱う必要がなくなります。後で別の言語で **png からテキストを読む** 必要がある場合は、`Language.RussianCyrillic` を適切な enum 値に変更するだけです。

## ステップ 3 – PNG 画像の準備

処理したい画像が実行時にアクセス可能であることを確認してください。`sample_russian.png` をコンパイルされた `.exe` と同じフォルダーに配置するか、絶対パスを使用してください。画像は鮮明なスキャンまたはスクリーンショットである必要があります。ぼやけた画像や過度に圧縮された PNG では OCR の精度が大幅に低下します。

**一般的なエッジケース**: PNG に�数の言語が含まれている場合、`ocrEngine.Language = Language.Multilingual;` を設定すると、エンジンが各ブロックを自動的に検出します。

## ステップ 4 – アプリケーションの実行と出力の確認

プログラムをコンパイルして実行します：

```bash
dotnet run
```

コンソールに抽出されたロシア語テキストが表示されます。例としては次のようになります：

```
Привет, мир! Это пример текста на русском языке.
```

空文字列が返された場合は、以下を再確認してください：

1. ファイルパスが正しいか。
2. 画像が全白または全黒でないか。
3. 言語モデルが正常にダウンロードされたか（ユーザープロファイル下に `Aspose.OCR` フォルダーがあるか）を確認してください。

## ステップ 5 – 精度向上のための高度な調整

デフォルト設定は多くの場合で機能しますが、エンジンを微調整したい場合があります：

| Setting | What it does | When to use it |
|---------|---------------|----------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | わずかな回転を補正する | 完全に揃っていないスキャン文書 |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | 背景の斑点を除去する | モバイルカメラからの低品質 PNG |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | 文字を数字に限定する | 請求書から数字を抽出する |

`RecognizeImage` を呼び出す前にこれらを追加してください：

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

## ステップ 6 – 結果をファイルへエクスポート（オプション）

後で処理するために **テキストを抽出する方法** をファイルに保存する必要がある場合は、結果をディスクに書き込むだけです：

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

これで、データベース、検索インデックス、または翻訳エンジンに投入できる永続的なコピーが得られます。

## よくある質問

**Q: JPEG や BMP など他の画像形式でも動作しますか？**  
A: もちろんです。`RecognizeImage` は .NET の `System.Drawing` ライブラリがサポートするすべての形式（JPEG、BMP、TIFF など）を受け付けます。

**Q: 同じ実行で英語テキストを抽出したい場合は？**  
A: `Language.English` を使用して 2 番目の `OcrEngine` インスタンスを作成するか、呼び出し間で言語プロパティを切り替えてください。

**Q: メインスレッドをブロックせずに Web API で OCR を実行できますか？**  
A: はい。認識呼び出しを `Task.Run` でラップするか、非同期オーバーロードの `RecognizeImageAsync`（新しい Aspose バージョンで利用可能）を使用してください。

**Q: PNG のサイズに制限はありますか？**  
A: ライブラリは大きな画像も処理できますが、解像度が上がるとメモリ使用量も増加します。`OutOfMemoryException` が発生した場合は、まず画像を縮小することを検討してください。

## 完全動作例（コピー＆ペースト可能）

以下は、NuGet パッケージをインストールした後すぐに実行できる、新しいコンソールプロジェクト（`dotnet new console`）に貼り付けられる完全なプログラムです。

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**期待されるコンソール出力**（サンプルに “Привет, мир!” というフレーズが含まれていると仮定）：

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

## 結論

C# を使用して PNG 画像に対する **OCR の実行方法** を、Aspose.OCR のインストールから前処理オプションのカスタマイズ、結果のエクスポートまでカバーしました。これで、**png からテキストを読む方法**、異なる言語で **テキストを抽出する方法**、そして特に **ロシア語テキストを抽出する方法** を最小限のコードで実装できるようになりました。

次の課題に挑戦する準備はできましたか？ OCR の出力を言語検出ライブラリに渡したり、Azure Cognitive Services と組み合わせて翻訳に利用したりしてみてください。信頼できる OCR エンジンと C# の強力なエコシステムを組み合わせれば、可能性は無限です。

この **c# ocr チュートリアル** が役立ったと思ったら、スターを付けたり、チームメンバーと共有したり、あなたのヒントをコメントで残したりしてください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}