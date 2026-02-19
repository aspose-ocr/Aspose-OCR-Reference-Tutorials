---
category: general
date: 2026-02-19
description: Aspose OCR を使用してスキャン画像からテキストを抽出し、OCR の精度を向上させるために画像を前処理する方法を学びましょう。ステップバイステップの
  C# チュートリアルです。
draft: false
keywords:
- extract text from scan
- preprocess image for ocr
language: ja
og_description: スキャンからテキストを素早く抽出します。このガイドでは、OCR 用に画像を前処理し、C# の Aspose OCR で信頼性の高い結果を得る方法を紹介します。
og_title: スキャンからテキストを抽出 – 完全な C# Aspose OCR チュートリアル
tags:
- OCR
- C#
- Aspose
title: C#でスキャン画像からテキストを抽出 – 完全なAspose OCRガイド
url: /ja/net/ocr-optimization/extract-text-from-scan-in-c-complete-aspose-ocr-guide/
---

"What’s Next?" heading.

Also final line.

Also closing shortcodes.

Also backtop button shortcode.

We must keep URLs unchanged.

Now let's produce the translated content.

Be careful to preserve markdown formatting exactly.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャンからテキストを抽出 – 完全な Aspose OCR ガイド

スキャンされたファイルから **スキャンからテキストを抽出** したいのに、文字化けした出力ばかりになっていませんか？ あなただけではありません。請求書のデジタル化や古文書のアーカイブ化など、実務でスキャン画像からきれいなテキストを取得することは最初のハードルです。朗報です！数行の C# と Aspose OCR さえあれば、ノイズの多い JPEG を読みやすい文字列に変換でき、ちょっとした前処理で「まあまあ」から「すごい」へと差がつきます。

このチュートリアルでは、OCR エンジンの設定、**OCR 用に画像を前処理** して品質を向上させる方法、認識の実行、そして抽出したテキストの出力まで、全工程を順に解説します。最後まで読めば、任意のスキャン画像から確実にテキストを取得できるコンソール アプリが完成します。

## 必要なもの

作業を始める前に、以下が揃っていることを確認してください。

- **.NET 6+**（または .NET Framework 4.7.2+）がインストール済み – API はどちらでも動作します。
- **Aspose.OCR** NuGet パッケージ (`Install-Package Aspose.OCR`) – これだけが外部依存です。
- サンプルのスキャン画像（例: `skewed_scan.jpg`）を参照できるフォルダーに配置。
- コード エディタまたは IDE – Visual Studio、Rider、VS Code などお好きなものを使用してください。

他にライブラリは不要です。今回使用する前処理オプションはすべて Aspose OCR に組み込まれています。

## Step 1: 新しいコンソール プロジェクトを作成

まず、クリーンなサンドボックスとして新しいコンソール アプリを作成します。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

これでプロジェクトに OCR ライブラリが参照されました。`Program.cs` を開き、デフォルトの `Hello World` 行を削除して、これから自分のコードを記述します。

## Step 2: OCR エンジンの初期化 – 抽出のコア

**スキャンからテキストを抽出** するには `OcrEngine` インスタンスが必要です。言語は英語が最も一般的ですが、Aspose は多数の言語に対応しています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Preprocessing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };
```

なぜ最初にエンジンをインスタンス化するのか？ エンジンは言語設定、前処理、内部キャッシュなどすべての構成情報を保持するため、最初に作成しておくことで以降の呼び出しが同一設定を共有します。

## Step 3: OCR 用に画像を前処理 – 抽出前の精度向上

スキャンはほとんど完璧ではありません。回転していたり、ノイズが多かったり、コントラストが低かったりします。Aspose OCR には結果を劇的に改善する 3 つの便利な前処理オプションがあります。

- **Deskew** – 回転したページを自動で真っ直ぐにします。
- **Denoise** – 斑点や粒子ノイズを除去します。
- **Contrast** – 薄い文字を明るくします。

```csharp
        // 2️⃣ Turn on preprocessing to clean up the image
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = DeskewAdvanced.Enable(),      // corrects rotation
            Denoise = DenoiseWavelet.Enable(),    // reduces noise
            Contrast = ContrastBoost.Enable()     // enhances contrast
        };
```

このステップは、スキャナーで撮った写真を OCR エンジンに渡す前に「磨き上げる」作業と考えてください。省略すると、汚れたはがきの文字を読もうとするような、可能だがイライラする結果になります。

## Step 4: テキスト認識 – 実際の抽出

次に、前処理した画像をエンジンに渡します。`YOUR_DIRECTORY` を実際に `skewed_scan.jpg` が置かれているパスに置き換えてください。

```csharp
        // 3️⃣ Run OCR on the preprocessed image
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/skewed_scan.jpg");
```

`RecognizeImage` メソッドは `OcrResult` オブジェクトを返し、そこに生テキスト、信頼度スコア、必要に応じてバウンディング ボックスが格納されます。

## Step 5: 抽出したテキストの表示（または保存）

最後に、取得した内容を確認します。実際のプロジェクトではデータベースやファイルに書き込むことが多いですが、ここではコンソールに出力するだけにします。

```csharp
        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行 (`dotnet run`) すると、次のような出力が得られるはずです。

```
=== Extracted Text ===
Invoice #12345
Date: 01/02/2026
Total: $1,234.56
Thank you for your business!
```

出力が文字化けしている場合は、画像パスが正しいか、前処理オプションが有効かを再確認してください。微妙な回転や強いノイズが原因であることが多いです。

![extract text from scan example](/images/ocr-example.png)

*Alt text: Aspose OCR を使用して C# でスキャンからテキストを抽出する様子を示すスクリーンショット*

## Common Pitfalls and How to Avoid Them

- **パスが間違っている** – 相対パスはプロジェクトのルートを基準にします。バイナリ フォルダーではありません。自信がなければ絶対パスを使用してください。
- **サポート外の画像形式** – Aspose OCR は JPEG、PNG、BMP、TIFF に対応しています。PDF がある場合はまず画像に変換してください。
- **言語データが不足** – 英語以外を使用する場合は、Aspose のサイトから追加の言語パックをダウンロードする必要があります。
- **過剰な前処理** – すでにきれいな画像に対して denoise と contrast の両方を適用すると、文字が薄くなりすぎることがあります。各オプションを有無でテストしてください。

プロのコツ: 多くのスキャンは回転だけなので、deskew のみを使用すれば数ミリ秒の処理時間を節約できます。

## Extending the Solution – What If I Need More?

### 複数スキャンからテキストを抽出

フォルダー内のすべての画像を対象に認識コードを `foreach` ループで回します。

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### 信頼度スコアの取得

低信頼度の結果を除外したい場合は次のようにします。

```csharp
if (ocrResult.Confidence < 0.75)
{
    Console.WriteLine("Warning: Low confidence, consider manual review.");
}
```

### Web API で OCR を利用

抽出ロジックを ASP.NET Core エンドポイントとして公開します。コアコードはそのままで、エンジンをシングルトン サービスとして注入すれば完了です。

## Recap

Aspose OCR と C# を使って **スキャンからテキストを抽出** するために必要な手順をすべて網羅しました。プロジェクト作成から以下を実施しました。

1. 英語言語で OCR エンジンを初期化。
2. **OCR 用に画像を前処理** として deskew、denoise、contrast を適用。
3. サンプル JPEG で認識を実行。
4. コンソールにクリーンなテキストを出力。

これらのブロックを組み合わせれば、請求書処理システムや文書アーカイバ、紙媒体を検索可能データに変換したいあらゆるアプリに OCR を組み込めます。

## What’s Next?

- `Binarize` など他の前処理コンビネーションを試す（白黒文書向け）。
- 別言語や多言語検出に挑戦。
- OCR 出力を自然言語処理と組み合わせて、キー フィールドを自動抽出。

質問や工夫があればコメントで教えてください。コーディングを楽しみながら、スキャンが常にクリアになることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}