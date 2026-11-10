---
category: general
date: 2026-05-28
description: C# で Aspose を使用した韓国語 OCR チュートリアル。ストリームから画像を読み込み、プレーンテキストを抽出し、画像を PDF
  に変換し、検索可能な PDF をエクスポートする方法を学びます。
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: ja
og_description: Aspose を使用した C# の韓国語 OCR。ストリームから画像を読み込み、プレーンテキストを抽出し、画像を PDF に変換し、検索可能な
  PDF としてエクスポートするステップバイステップガイド。
og_title: 韓国語 OCR – 画像をPDFに変換してテキストを抽出 (C# ガイド)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: Asposeによる韓国語OCR：画像をPDFに変換し、C#でテキストを抽出
url: /ja/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose を使用した韓国語 OCR: 画像を PDF に変換し C# でテキストを抽出

クラウドに何も送らずに画像上で **Korean Language OCR** を実行できたらと思ったことはありませんか？ あなただけではありません。道路標識のデジタル化、レシートの処理、あるいは多言語検索インデックスの構築など、ローカルで韓国語文字を認識できることは、時間・コスト・プライバシーの面で大きなメリットになります。

このチュートリアルでは、**load image from stream**、**extract plain text**、**convert image to PDF**、そして最終的に **export searchable PDF** を行う、完全に実行可能なサンプルを順を追って解説します。使用するのは Aspose.OCR と数行の C# コードだけです。外部サービスは不要、隠されたマジックもありません。任意のコンソールアプリに貼り付けてすぐに動かせる純粋な .NET コードです。

## 本チュートリアルで得られるもの

- ファイルストリームを介して JPEG ファイルを読み込む動作するコンソールプログラム。  
- 韓国語テキストがプレーンな Unicode 文字列として抽出されます。  
- デバッグや分析用の OCR 実行結果を詳細に記録した JSON レポート。  
- 任意の PDF リーダーで開き、韓国語の単語を選択できる検索可能な PDF。  

**前提条件**  
- .NET 6.0 以降（コードは .NET Framework 4.7 以降でも動作します）。  
- Aspose.OCR for .NET の NuGet パッケージがインストールされていること（`Install-Package Aspose.OCR`）。  
- `korean_sign.jpg` を含むフォルダーと、出力ファイルを書き込める場所。  

これらが揃っているなら、さあ始めましょう。

## ステップ 1: 韓国語 OCR 用に OCR エンジンを初期化する

`OcrEngine` インスタンスが最初に必要です。GPU（お持ちの場合）を有効にすると認識速度が劇的に向上し、`AutomaticResourceDownload` をオフにすることで、ライブラリが提供したオフライン言語パックのみを使用するよう強制できます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **なぜ重要か:**  
> *GPU 加速* により、大量バッチの処理時間が秒単位からミリ秒単位に短縮されます。`AutomaticResourceDownload` を `false` に設定すると、デモがオフラインでも動作するようになり、企業環境での重要な要件を満たします。

## ステップ 2: ストリームから画像を読み込む

ストリーム経由で画像を読み込むことで柔軟性が得られます。ディスク、ネットワーク共有、あるいはメモリキャッシュされた BLOB からでも取得可能です。ここではローカルの JPEG ファイルを開きますが、同じパターンは任意の `Stream` でも機能します。

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **プロのコツ:** Web API 経由でアップロードされた画像を処理する場合は、`File.OpenRead` を受信した `IFormFile.OpenReadStream()` に置き換えるだけで、残りは同じです。

## ステップ 3: 韓国語を選択し前処理フィルタを適用する

Aspose.OCR は認識前に画像をクリーンアップするいくつかの前処理ステップをサポートしています。韓国語の標識の場合、デスキューとデノイズだけで十分なことが多いです。

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **内部で何が起きているか:**  
> `Deskew` フィルタは回転したテキストを水平に補正し、`Denoise` は文字分類器を混乱させる粒子ノイズを除去します。これらのステップを省くと、特に低解像度の写真で文字化けが起こりやすくなります。

## ステップ 4: 非同期でプレーンテキストを抽出する

いよいよ本番です—エンジンに文字認識を指示し、クリーンな文字列を取得します。`RecognizeAsync` を使用すれば、デスクトップや Web アプリに組み込んだ場合でも UI が応答し続けます。

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

プログラムを実行すると、以下のような出力が得られるはずです。

```
OCR complete. Extracted text:
서울시청
```

> **なぜ非同期か？**  
> OCR は CPU に負荷がかかります。非同期実行によりスレッドのブロックを防げるため、スレッド枯渇が問題になる ASP.NET Core では特に便利です。

## ステップ 5: 詳細な認識結果を取得し JSON として保存する

単なる文字列だけでなく、信頼度スコアやバウンディングボックス、元画像データなどが必要になることがあります。`RecognizeDetailed` メソッドは `RecognitionResult` オブジェクトを返し、後で分析できるよう JSON にシリアライズできます。

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

`korean_ocr.json` を開くと、以下のような構造が確認できます。

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **いつ使うべきか:**  
> 検索インデックスを構築する場合、信頼度の値で低品質な結果を除外できます。UI でテキストをハイライトしたい場合は、バウンディングボックスが位置情報として役立ちます。

## ステップ 6: 画像を PDF に変換し検索可能 PDF をエクスポートする

Aspose はラスタ画像からベクタへ変換する作業をシームレスに行います。`OutputFormat` を `SearchablePdf` に設定すると、ライブラリは元画像を埋め込み、OCR 結果を含む見えないテキスト層を重ねます。生成された PDF は検索、コピー、インデックス付けが可能で、通常の PDF と同様に扱えます。

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

`korean_searchable.pdf` を Adobe Reader などの PDF ビューアで開き、**Ctrl+F** で韓国語の単語を入力すると、ページ上の正確な位置にジャンプします。これが検索可能 PDF の威力です。

> **余分なヒント:** 隠しテキスト層が不要でビジュアル PDF だけが必要な場合は、`OutputFormat` を `Pdf` に変更してください。

## 完全な動作例

以下が完全なプログラムです。コピーして貼り付け、`YOUR_DIRECTORY` を実際のパスに置き換えて **F5** を押してください。

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### 期待されるコンソール出力

```
OCR complete. Extracted text:
서울시청
```

ソース画像の隣に次の 3 つの新しいファイルが作成されます。

- `korean_ocr.json` – 完全な認識データ。  
- `korean_searchable.pdf` – 検索可能な PDF。  
- (任意) 追加した中間ログ。

## よくある質問とエッジケース

**GPU がない場合はどうすれば？**  
`EnableGpu = false` に設定すれば、CPU フォールバックで小規模バッチでも問題なく動作します。

**1 回の実行で複数画像を処理できますか？**  
もちろん可能です。コアロジックを `foreach (var file in Directory.GetFiles(...))` ループで囲み、各イテレーションで `ocrEngine.Image` を再割り当てしてください。

**韓国語以外の言語も同時に扱うには？**  
Aspose.OCR では `Language = Language.AutoDetect` を設定するか、ビット単位の OR 演算子で言語を組み合わせられます（例: `Language.Korean | Language.English`）。

**OCR の信頼度が低い場合は？**  
`detailedResult.Pages[0].Words` を確認し、`Confidence < 0.7` のエントリを除外します。また、前処理フィルタを調整してみてください—`PreprocessFilter.ContrastEnhancement` を追加すると効果的です。

## まとめ

これで **Korean Language OCR** をエンドツーエンドで実行する方法、すなわち **loading image from stream** → **extract plain text** → **convert image to PDF** → **export searchable PDF** の流れが分かりました。この手法はモジュール化されているため、画像ソースを差し替えたり、出力形式を変更したり、JSON を任意の下流パイプラインに組み込んだりできます。

次は何をすべきか

## 関連チュートリアル

- [Aspose.OCR を使用した言語選択付き画像テキスト抽出 (C#)](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [複数言語対応の Aspose OCR で画像テキストを認識](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [.NET 用 Aspose.OCR の OCR 最適化 – 画像からテキスト抽出](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}