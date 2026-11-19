---
category: general
date: 2026-04-04
description: Aspose OCRでGPUをすばやく有効にする方法。画像からテキストを抽出し、OCR用に画像を読み込み、C#でテキストを認識する方法を学びましょう。
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: ja
og_description: Aspose OCRでGPUをすばやく有効にする方法。このチュートリアルに従って画像からテキストを抽出し、OCR用に画像を読み込み、C#でテキストを認識します。
og_title: C#でOCRにGPUを有効にする方法 – 完全ガイド
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C#でOCR用GPUを有効にする方法 – ステップバイステップガイド
url: /ja/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR の gpu を有効にする方法 – 完全ガイド

Aspose OCR を使用する際に **gpu を有効にする方法** を考えたことはありますか？何百枚ものレシートを処理していてパフォーマンスの壁にぶつかり、CPU が追いつかないことがあるかもしれません。良いニュースは、GPU アクセラレーションをオンにするのはとても簡単で、オンにすれば OCR エンジンが画像を高速に処理するのが実感できるでしょう。

このチュートリアルでは GPU スイッチを切り替えるだけでなく、**load image for OCR**、**recognize text**、そして最終的に **extract text from image** をクリーンな C# の例で示します。最後まで読むと、外部サービスを必要とせずに任意のサポート画像からプレーンテキストを抽出できる、すぐに実行可能なプログラムが手に入ります。

## 必要なもの

- .NET 6+（または .NET Framework 4.7.2 以降）。  
- Aspose.OCR for .NET、バージョン 24.2.0 以上（このリリースで GPU フラグが追加されました）。  
- 適切なドライバーがインストールされた GPU 対応マシン（NVIDIA CUDA 11+ が推奨）。  
- 処理したい画像ファイル（スキャンしたレシート、撮影した請求書、手書きメモなど）。

これらが揃っていれば、準備完了です—さっそく始めましょう。

## 手順 1: gpu を有効にする – OCR エンジンの設定

最初に行うべきことは、Aspose OCR に GPU の使用を指示することです。これは `OcrEngine` インスタンスの `UseGpu` プロパティを設定することで行います。このプロパティはデフォルトで `false` になっているので、明示的にオンにします。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Why this matters:** `UseGpu` が `true` の場合、ライブラリは重い行列計算をグラフィックプロセッサにオフロードします。RTX 3060 などの標準的な GPU でも、画像ごとのレイテンシが数秒から数百ミリ秒にまで低減することが実感できるでしょう。

> **Pro tip:** ヘッドレス CI 環境で実行する場合は、GPU ドライバーがインストールされており、サービスアカウントにデバイスへのアクセス権があることを確認してください。そうでないとエンジンは静かに CPU モードにフォールバックします。

## 手順 2: Load Image for OCR – エンジンにファイルを指定

次に **load image for OCR** が必要です。Aspose OCR は System.Drawing がサポートするすべての画像形式（PNG、JPEG、BMP、TIFF など）を受け付けます。`ImageStream.FromFile` ヘルパーはファイルを必要なストリームオブジェクトにラップします。

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

`byte[]` からロードしたい場合（例：画像がデータベースに格納されている場合）は、代わりに `ImageStream.FromBytes(byteArray)` を使用できます。結果は同じですが、ソースが異なるだけです。

## 手順 3: How to recognize text – OCR プロセスの実行

エンジンの設定と画像のロードが完了したので、**recognize text** を実行する時です。`Recognize` メソッドがすべての処理を行い、プレーンテキスト、信頼度スコア、必要に応じてバウンディングボックスまで含む `OcrResult` オブジェクトを返します。

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` を呼び出す前に `ocrEngine.Language = OcrLanguage.French;` のように設定すれば言語を変更できます。GPU アクセラレーションはロードする言語パックに関係なく機能します。

## 手順 4: How to extract text from image – 結果の出力

最後に結果オブジェクトの `Text` プロパティを読み取ることで **extract text from image** を行います。デモではコンソールに出力しますが、ファイルやデータベースに書き込んだり、別のサービスに渡したりすることも可能です。

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Expected output**（実際のテキストは画像に応じて異なります）:

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

生の信頼度値が必要な場合は `ocrResult.Regions` をイテレートし、各 `Region.Confidence` を確認できます。

## 完全動作例 – 1 ファイルで実行可能

以下に完全なプログラムを示します。新しいコンソールプロジェクトにコピー＆ペーストし、Aspose.OCR の NuGet パッケージを復元して **F5** を押してください。

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note:** `YOUR_DIRECTORY/receipt.jpg` を実際の画像パスに置き換えてください。プログラムが `FileNotFoundException` をスローした場合は、パスとファイル権限を再確認してください。

## よくある質問とエッジケース

### GPU が検出されない場合は？

Aspose OCR は自動的に CPU モードに切り替え、警告をログに出します。どのモードが有効か確認するには、構築後に `ocrEngine.IsGpuEnabled` をチェックしてください。GPU ドライバーが正常にロードされた場合にのみ `true` を返します。

### 複数画像をループで処理できますか？

もちろん可能です。`ocrEngine.Image = …` の行を `foreach (var file in files)` ループ内に移動すれば OK です。同じ `OcrEngine` インスタンスを使い回すことで、GPU リソースの再割り当てオーバーヘッドを回避できます。

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### 非英語言語を扱うには？

`Recognize()` を呼び出す前に言語を設定します：

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

GPU アクセラレーションの動作は同じで、言語モデルだけが変わります。

### 大きく高解像度の写真はどうですか？

メモリ不足エラーが発生した場合は、まず画像を縮小してください。Aspose OCR には `ImageHelper.Resize` があり、詳細をあまり失わずに手早く縮小できます。

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## 結論

ここまでで Aspose OCR の **how to enable gpu**、**load image for OCR**、**how to recognize text**、そして **how to extract text from image** を簡潔で本番環境向けの C# プログラムを使って解説しました。`UseGpu` フラグを切り替えるだけで、特にレシートや請求書など大量の文書をバッチ処理する際に顕著な速度向上が得られます。

次のステップに進みませんか？この OCR パイプラインをデータベースと連携させて抽出したレシートを保存したり、プレーンテキストを自然言語処理モデルに渡して費用のカテゴリ分けに利用したりできます。また、`OcrResult.Regions` コレクションを調べてバウンディングボックス座標を取得し、元画像上で単語をハイライトする UI を構築することも可能です。

コーディングを楽しんで、GPU アクセラレーションがもたらす OCR ワークロードの余分なパワーを活用してください！

---

![how to enable gpu illustration](gpu-ocr-diagram.png "how to enable gpu illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}