---
category: general
date: 2026-02-25
description: GPU 加速 OCR を使用して画像からテキストを高速に認識します。GPU モードの設定方法、OCR 用画像の読み込み、TIFF からのテキスト抽出を学びましょう。
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: ja
og_description: GPU 加速 OCR を使用して画像からテキストを瞬時に認識します。GPU モードの設定、OCR 用画像の読み込み、TIFF からのテキスト抽出をカバーしたステップバイステップの
  C# チュートリアルです。
og_title: GPU 加速 OCR で画像からテキストを認識する – C# ガイド
tags:
- Aspose OCR
- C#
- GPU computing
title: C#でGPUアクセラレートされたOCRを使用して画像からテキストを認識する
url: /ja/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU 加速 OCR を使用した C# での画像からのテキスト認識

画像からテキストを **認識** したいのに、CPU が高解像度スキャンでボトルネックになっていませんか？ あなただけではありません。実務のプロジェクトでは、請求書のデジタル化や古い新聞のアーカイブ化など、単一の TIFF ファイルがパイプラインを数分間停止させることがあります。良いニュースは、Aspose.OCR がスイッチ一つで重い処理を GPU に任せられ、遅い操作をほぼ瞬時に変換できることです。

このチュートリアルでは、**GPU モードの設定**、**OCR 用画像の読み込み**、そして **TIFF ファイルからのテキスト抽出** の全プロセスを解説します。最後まで読むと、.NET 6 以降のプロジェクトにそのまま組み込める、自己完結型の本番向けサンプルが手に入ります。

## 前提条件

- .NET 6 SDK（またはそれ以降）がインストールされていること。
- Visual Studio 2022 またはお好みのエディタ。
- Aspose.OCR NuGet パッケージ（`Aspose.OCR`）がプロジェクトに追加されていること。
- DirectX 11 以降をサポートする GPU（ほとんどの最新 GPU が該当）。  
  *GPU がない場合でも `GpuMode.Auto` でコードを実行できます。ライブラリは自動的に CPU にフォールバックします。*

> **プロのコツ:** GPU ドライバーが最新であることを確認してください。古いドライバーは原因不明の初期化エラーを引き起こすことがあります。

## Step 1 – OCR エンジンの作成と GPU モードの設定

最初に必要なのは `OcrEngine` のインスタンスです。このオブジェクトはすべての設定を保持し、エンジンが GPU を使用するかどうかも含まれます。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**重要な理由:** GPU モードを有効にすると、計算負荷の高い画像前処理（二値化、ノイズ除去など）がグラフィックカードにオフロードされます。ミッドレンジの RTX 3060 でも、純粋な CPU 処理に比べて **3‑5 倍** の速度向上が期待できます。

## Step 2 – OCR 用画像の読み込み（TIFF の例）

Aspose.OCR は多数のフォーマットに対応していますが、TIFF はロスレス品質を保つため、スキャン文書で一般的に使用されます。`ImageStream.FromFile` を使ってファイルをメモリに読み込みます。

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**エッジケース:** TIFF ファイルの中には複数ページが含まれるものがあります。`ImageStream.FromFile` は最初のページだけを読み込みます。すべてのページを処理する必要がある場合は、`ImageInfo.Pages` をループし、各ページをエンジンに個別に渡してください。

## Step 3 – 認識の実行

エンジンの設定と画像の読み込みが完了したら、`Recognize()` を呼び出します。このメソッドはプレーンテキストの出力と追加メタデータを含む `OcrResult` オブジェクトを返します。

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**テキストが文字化けしている場合は？**  
- 画像が正しい向きであることを確認してください（必要なら回転）。  
- `ocrEngine.Config.DeskewEnabled = true;` など、前処理オプションを調整します。  
- 多言語文書の場合は `ocrEngine.Config.Language = Language.English;` など、適切な列挙体に設定してください。

## Step 4 – 出力の検証とエラーハンドリング

堅牢な実装では、null 結果のチェックと潜在的な例外（例: GPU ドライバーが見つからない）を捕捉します。

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**なぜラップするのか？** 必要なネイティブライブラリが存在しない場合、GPU 初期化で `DllNotFoundException` がスローされることがあります。catch ブロックは、優雅にフォールバックする手段を提供します。

## 完全な実行可能サンプル

以上をまとめた、すぐにコンパイルして実行できる完全なプログラムを示します。ファイルパスは実際の TIFF に置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**期待される出力**

TIFF に読み取り可能な英語テキストが含まれていれば、以下のような出力が得られます。

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

画像が空白または読めない場合、コンソールにソースファイルを確認するよう指示が表示されます。

## よくある質問とバリエーション

| Question | Answer |
|----------|--------|
| **TIFF の代わりに JPEG や PNG を処理できますか？** | もちろんです。`ImageStream.FromFile` は Aspose.OCR がサポートする任意のフォーマット（PNG、JPEG、BMP など）で動作します。 |
| **1つの TIFF に複数ページがある場合はどうすればよいですか？** | `ImageInfo.Pages` をループし、`Recognize()` を呼び出す前に各ページを `ocrEngine.Image` に割り当てます。 |
| **Aspose.OCR のライセンスは必要ですか？** | 無料評価版は最大 100 ページまで利用可能です。本番環境では評価透かしを除去するためにライセンスを購入してください。 |
| **言語モデルはどう変更しますか？** | `ocrEngine.Config.Language = Language.Spanish;` のように設定します（サポートされている列挙体なら何でも可）。 |
| **信頼度スコアを取得する方法はありますか？** | `ocrEngine.Config.EnableConfidence = true;` を有効にし、各行の `result.Confidence` を確認します。 |

## 結論

これで、C# で **GPU 加速 OCR** パイプラインを使用して **画像からテキストを認識**する方法が分かりました。**GPU モードの設定**、**OCR 用画像の読み込み**、そして **TIFF ファイルからのテキスト抽出** を行うことで、実務のワークロードに対応できる高速でスケーラブルなソリューションが構築できました。

次のステップは？このコードを PDF ジェネレータと組み合わせて検索可能な PDF を作成したり、抽出した文字列を自然言語処理パイプラインに渡したりしてみてください。また、`GpuMode.Auto` を試すことで、GPU が無い環境にも適応できるアプリにすることができます。

コーディングを楽しんで、OCR が閃光のように速く動作しますように！

![画像からテキストを認識する例](https://example.com/ocr-demo.png "GPU 加速 OCR を使用した画像からテキストを認識")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}