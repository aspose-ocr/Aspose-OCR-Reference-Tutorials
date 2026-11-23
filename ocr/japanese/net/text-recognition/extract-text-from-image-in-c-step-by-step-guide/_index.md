---
category: general
date: 2026-05-06
description: C#でAspose OCRを使用して画像からテキストを抽出します。JPGをテキストに変換する方法、OCR言語の設定、JPGから効率的にテキストを読み取る方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、JPGをテキストに変換する方法、OCR言語を設定する方法、そしてJPGからテキストを読み取る方法を示します。
og_title: C#で画像からテキストを抽出する – 完全チュートリアル
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを抽出する – ステップバイステップガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – 完全プログラミングウォークスルー

画像から **テキストを抽出** したいけど、どのライブラリを選べばいいか分からないことはありませんか？開発者はよく「クラウドにデータを送らずに JPG をテキストに変換するにはどうすればいいのか？」と質問します。良いニュースは、Aspose OCR が完全オフラインで動作し、.NET アプリ内でそのまま利用できるソリューションを提供してくれることです。

このチュートリアルでは、Aspose OCR NuGet パッケージのインストールから、ロシア語テキスト用の **OCR 言語設定**、そして **JPG からテキストを読み取る** 方法まで、必要なすべてを順を追って解説します。最後まで読めば、任意の C# プロジェクトに貼り付けてすぐに画像からテキストを抽出できる再利用可能なコードスニペットが手に入ります。

> **このチュートリアルで得られるもの**  
> • **画像からテキストを抽出** する、明確で実行可能なサンプルコード  
> • Aspose OCR エンジンを使った **JPG をテキストに変換** の方法  
> • 多言語シナリオ向けの **OCR 言語設定** のコツ  
> • 読めない画像や言語パックが欠如している場合のエッジケース対策  

## 前提条件

作業を始める前に、以下を用意してください。

| 必要項目 | 理由 |
|-------------|----------------|
| .NET 6.0 以上（最新の .NET ランタイム） | Aspose OCR は .NET Standard 2.0+ を対象としているため、最新ランタイムほどパフォーマンスが向上します。 |
| Visual Studio 2022（または C# 拡張機能付き VS Code） | 使いやすい IDE があれば OCR のフローをすばやくデバッグできます。 |
| インターネット接続 **1 回だけ**（Aspose OCR NuGet パッケージのダウンロード用） | 初回インストール後は **オフラインリソース** を有効にすれば、以降のダウンロードは不要です。 |
| ロシア語テキストを含むサンプル JPG 画像（`input.jpg`） | 本チュートリアルはロシア語の例を使用しますが、インストール済みの言語パックさえあれば任意の言語に置き換え可能です。 |

これらの項目が見慣れない場合でも慌てないでください。NuGet パッケージのインストールはコマンド一つで完了し、残りの手順は Aspose がサポートするすべての画像形式で同様に動作します。

## ソリューションの概要

全体の流れは次の通りです。

1. **Create** an `OcrEngine` with offline resources so the library won’t try to download language data at runtime.  
2. **Set** the desired language (e.g., Russian) using the `OcrLanguage` enum.  
3. **Call** `RecognizeImage` on a local JPG file.  
4. **Print** the extracted string to the console or pipe it into your own workflow.

以下の図はデータフローを簡略化したものです。

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extract text from image using Aspose OCR in C#"}

*この図は概念的なものです。実際の処理はコードが担います。*

## 画像からテキストを抽出 – 基本概念

コードを書き始める前に、開発者がつまずきやすい概念を整理しておきましょう。

- **OfflineResources** – `true` に設定すると、Aspose OCR は事前にダウンロードした言語パックを探します。これにより、本番環境での起動時に「自動ダウンロード」ステップが省かれ、起動が高速化します。  
- **OcrLanguage** – この enum には `English`, `Russian`, `Japanese` など多数の言語識別子が含まれます。適切な言語を指定することで、エンジンが言語固有のヒューリスティックを適用でき、認識精度が大幅に向上します。  
- **画像品質** – OCR は高コントラストでノイズの少ない画像で最も効果を発揮します。文字化けが発生した場合は、二値化などの前処理を検討してください。

これらのポイントを理解すれば、**OCR 言語を手動で設定**すべきタイミングと、**JPG をテキストに変換** が単なるワンライナーではない理由が見えてきます。

## Step 1: Aspose OCR NuGet パッケージのインストール

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* 初回インストール後に `-v latest` を付与すると、常に最新の安定版ビルドが取得できます。パッケージサイズは約 15 MB で、デスクトップやサーバーへの導入に支障はありません。

## Step 2: JPG をテキストに変換 – エンジンの初期化

ライブラリがローカルに配置されたので、オフラインで動作する `OcrEngine` を作成しましょう。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### なぜ重要か

- **Offline mode** は起動時間を決定論的に保ち、ロックダウンされたサーバーへデプロイした際に予期せぬネットワーク呼び出しが発生しません。  
- **Setting the language** (`OcrLanguage.Russian`) により、ロシア語文字セットが使用され、クリーンな画像では認識精度が約 70 % から >95 % に向上します。  
- メソッド `RecognizeImage` は Aspose がサポートする任意の画像形式（`.jpg`, `.png`, `.tiff`, …）を受け付けます。そのため **JPG からテキストを読み取る** ための余分な変換処理は不要です。

## Step 3: OCR 言語の設定 – 複数言語への対応

文書に混在言語（例：ロシア語と英語）が含まれるケースがあります。Aspose OCR では *フォールバック* 言語配列を指定できます。

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

プライマリ言語で文字が認識できない場合、エンジンは自動的に追加リストをチェックします。この手法は、キリル文字の会社名と英語の製品コードが混在する請求書などで特に有用です。

> **注意:** 言語パックはプロジェクトの `Resources` フォルダーに配置しておく必要があります。`FileNotFoundException` が発生したら、Aspose ポータルから不足しているパックをダウンロードし、実行ファイルと同階層に置いてください。

## Step 4: JPG からテキストを読み取る – よくある落とし穴と対策

適切な言語パックがあっても、以下のような問題に遭遇することがあります。

| 問題 | 典型的な症状 | 簡易対策 |
|-------|-----------------|-----------|
| コントラストが低い | 文字化けまたは空出力 | `System.Drawing` を使ってシンプルなコントラスト伸長フィルタを適用 |
| 画像が回転している | テキストが横向きに表示 | `ocrEngine.ImageRotation = OcrRotation.Rotate90;`（または 180/270）を `RecognizeImage` 前に設定 |
| ファイルサイズが大きい | 認識が遅い、メモリ使用量が高い | 長辺を最大 2000 px にリサイズ。OCR の品質はほぼ維持されます |

以下は、画像をリサイズ・強調してエンジンに渡すコンパクトなヘルパーです。

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

これで `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` を呼び出すだけで、よりクリーンな結果が得られます。

## 完全動作サンプル – すべての手順を 1 ファイルにまとめた例

以下は `Program.cs` にそのまま貼り付けて使用できる **完全版** プログラムです。インストール手順、言語設定、前処理、エラーハンドリングがすべて含まれています。

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}