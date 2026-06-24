---
category: general
date: 2026-06-19
description: C# で Aspose OCR を使用して画像からテキストを認識する：画像をテキストに変換し、JPG ファイルからテキストを抽出するステップバイステップガイド
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを認識します。OCR言語の設定方法、jpgからテキストを抽出する方法、画像をテキストに変換する方法を数分で学びましょう。
og_title: C#で画像からテキストを認識する – 画像をテキストに変換
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを認識 – 画像をテキストに変換
url: /ja/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像からテキストを認識 – 画像をテキストに変換

画像からテキストを **認識したい** が、高額なライセンス料がかからないライブラリがどれか分からない、ということはありませんか？ あなたは一人ではありません。このチュートリアルでは、Aspose OCR の無料 Community モードを使って **画像をテキストに変換** し、jpg ファイルからテキストを抽出し、さらに **OCR 言語を設定** して多言語シナリオに対応する方法を解説します。

NuGet パッケージのインストールから、マルチページ PDF や低解像度画像といったエッジケースの処理まで網羅します。最後には、画像ファイルに対して **OCR を実行** できるコンソール アプリがすぐに動作するようになります。

## 必要なもの

- .NET 6 SDK 以上（コードは .NET Core 3.1+ でも動作します）  
- Visual Studio 2022 またはお好みのエディタ  
- 読み取れるテキストが含まれた画像ファイル（JPG、PNG、BMP など）  
- `Aspose.OCR` NuGet パッケージを取得できるインターネット接続  

以上です — 余計な DLL や外部サービスは不要、純粋に C# だけです。

![画像からテキストを認識する例](https://example.com/ocr-screenshot.png "画像からテキストを認識する例")

*(このスクリーンショットは、サンプル JPG を認識した後のコンソール出力を示しています。)*

## 手順 1: NuGetで Aspose OCR をインストール

まず、プロジェクトに Aspose OCR ライブラリを追加します。プロジェクト フォルダでターミナルを開き、以下を実行してください。

```bash
dotnet add package Aspose.OCR
```

このパッケージは **Community モード** を備えており、1 回の実行で最大 100 ページまで処理が制限されます。小規模な実験には最適です。もし上限を超える必要が出た場合は、後から有料ライセンスにアップグレードすればコードの変更は不要です。

## 手順 2: OCRエンジンの設定（OCR言語の設定）

**画像に対して OCR を実行** する前に、エンジンに期待する言語を伝える必要があります。デフォルトは英語ですが、1 行のコードでスペイン語、フランス語、さらには中国語に切り替えることができます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

言語が重要な理由は何でしょうか？ OCR モデルは文字セットごとに学習されており、英語モデルにフランス語文書を渡すとアクセントや合字が認識されません。正しい言語を設定することで精度が劇的に向上します。

## 手順 3: OCRエンジンを作成し画像を認識

設定が完了したら、`using` ブロック内でエンジンをインスタンス化し、リソースが自動的に解放されるようにします。その後、`RecognizeImage` に JPG（またはサポートされている任意の形式）のパスを渡して呼び出します。

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

注意すべき点は以下の通りです：

- **スレッド安全性:** `OcrEngine` インスタンスはスレッドセーフではありません。多数の画像を同時に処理する場合は、スレッドごとに別々のエンジンを作成してください。  
- **サポート形式:** JPG だけでなく、PNG、BMP、TIFF、さらには PDF も扱えます。同じメソッドで **jpg からテキストを抽出** したり、他のラスタ画像からテキストを取得したりできます。

## 手順 4: 認識結果の出力（画像をテキストに変換）

OCR エンジンが処理を終えると、結果は `OcrResult` オブジェクトに格納されます。その `Text` プロパティには、エンジンが読み取れたすべてのテキストがプレーンテキストとして保持されています。

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

クリアなレシートのスクリーンショットでプログラムを実行すると、次のような出力が得られます：

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

これが **画像をテキストに変換** の本質です — 画像が文字列となり、保存・検索・他システムへの入力が可能になります。

## 手順 5: 一般的なエッジケースの処理

### 5.1 低解像度画像

100 dpi 未満になると OCR の精度は急激に低下します。文字化けが見られる場合は、画像を前処理（コントラスト上げ、リサイズ、シャープフィルタ適用など）してから Aspose OCR に渡してみてください。

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 複数ページ文書

Community モードは 100 ページで上限がかかりますが、PDF やマルチページ TIFF も処理可能です。エンジンはテキストを連結して返し、ページ区切りは `\f` で保持されます。

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 英語以外の言語

`Language` 列挙体を別のサポート対象に変更します：

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

デフォルトセット以外の言語を使用する場合は、対応する言語パックをインストールしてください。Aspose はそれらを別個の NuGet パッケージとして提供しています。

## 手順 6: 完全な動作例

すべてを組み合わせた、コピー＆ペーストで動作するコンソール アプリの完全コードを示します。このコードは **画像からテキストを認識** し、**jpg からテキストを抽出** し、必要に応じて **OCR 言語を設定** できます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力**（サンプル画像に「Hello World!」というテキストが含まれていると仮定）：

```
=== OCR Output ===
Hello World!
```

`dotnet run` でプログラムを実行すると、コンソールに抽出された文字列が表示されます。

## プロのコツと一般的な落とし穴

- **プロのコツ:** OCR 呼び出しを `try/catch` で囲み、破損したファイルを優雅に処理できるようにしましょう。  
- **注意点:** 透かしや強い背景ノイズがある画像はエンジンを混乱させやすいです。  
- **ヒント:** バッチ処理が必要な場合はディレクトリ内のファイルをループし、同じ `OcrEngine` インスタンスを再利用できます。ただし、画像ごとの設定はリセットすることを忘れずに。  
- **覚えておくべきこと:** Community モードの 100 ページ上限は「実行」ごとの制限であり、ファイル単位の制限ではありません。大きな PDF は分割して処理してください。

## 結論

これで、Aspose OCR を使って C# で **画像からテキストを認識** するための、実務でも使えるコード スニペットが完成しました。NuGet パッケージのインストールから **OCR 言語の設定**、低解像度画像への対応、そして **画像をテキストに変換** まで、すべてのステップを網羅しています。言語を変えてみたり、PNG を試したり、出力を検索インデックスに流し込んだりして、自由に実験してください。

次のステップとしては、**jpg からテキストを抽出** をスケールさせるために Azure Function に組み込んだり、レイアウト解析や手書き認識といった Aspose OCR の高度な機能を掘り下げたりすると良いでしょう。可能性は無限大です。今日構築した基盤が、今後の拡張をスムーズにします。

Happy coding, and may your images always be legible!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、別の実装アプローチを探求したりするのに役立ちます。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}