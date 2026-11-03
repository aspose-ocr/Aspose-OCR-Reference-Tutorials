---
category: general
date: 2026-03-26
description: C#でAspose OCRのGPUサポートを使用して画像のOCRを実行します。OCR用に画像をロードし、GPUデバイスIDを設定し、画像からテキストを高速に抽出する方法を学びましょう。
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: ja
og_description: C#でAspose OCR GPUを使用して画像のOCRを実行します。このガイドでは、OCR用に画像を読み込む方法、GPUデバイスIDを設定する方法、そして画像からテキストを効率的に抽出する方法を示します。
og_title: C#でGPUを使用した画像のOCR実行 – 完全ガイド
tags:
- C#
- OCR
- GPU
- Aspose
title: C#でGPUを使用して画像のOCRを実行する – 完全プログラミングガイド
url: /ja/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で GPU を使用した画像 OCR の実行 – 完全プログラミングガイド

画像ファイルで **run OCR on image** を実行したいが、CPU バージョンが非常に遅いと感じたことはありませんか？ あなたは一人ではありません。実際のアプリケーション、たとえば請求書スキャナーや大規模な文書アーカイブなどでは、ボトルネックは OCR エンジンそのものです。  

このチュートリアルでは、**complete, runnable example** を通じて、**load image for OCR** の方法、オプションで **set GPU device ID**、そして最終的に Aspose OCR の GPU 加速 API を使用して **extract text from image** を行う方法を説明します。最後まで読むと、純粋な CPU アプローチに比べてごく短時間で **recognize text from document** 画像を認識できるようになります。

## 学習できること

- Aspose.OCR と Aspose.OCR.Gpu パッケージのインストールと参照方法。  
- GPU 加速で **run OCR on image** を実行する正確な手順。  
- マルチ GPU マシンで適切な **GPU device ID** を選択する重要性。  
- 大きなファイルの処理、フォールバック戦略、一般的な落とし穴に関するヒント。  

### 前提条件

| 要件 | 理由 |
|------|------|
| .NET 6.0 以降 | 最新の言語機能とパフォーマンス向上 |
| Visual Studio 2022（または任意の C# IDE） | プロジェクト設定が簡単 |
| CUDA 対応 NVIDIA GPU（オプション） | GPU 加速が必要な場合のみ必須 |
| Aspose.OCR & Aspose.OCR.Gpu NuGet パッケージ | `GpuOcrEngine` クラスを提供 |

GPU がなくても心配はいりません。コードは自動的に CPU エンジンにフォールバックします。これについては後ほど説明します。

---

## 手順 1: Aspose OCR パッケージのインストール

**run OCR on image** を実行する前に、ライブラリが必要です。ターミナル（または Package Manager Console）を開き、以下を実行してください：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

これら 2 つのパッケージはコア OCR エンジンと GPU 固有の拡張機能を提供します。インストール後、`.csproj` に次の参照が追加されているはずです：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **プロのコツ:** パッケージのバージョンを同期させてください。バージョンが不一致だと実行時エラーの原因になります。

---

## 手順 2: GPU 対応 OCR エンジンの作成

ライブラリが揃ったので、GPU を使用して **run OCR on image** を行いましょう。`GpuOcrEngine` クラスが加速処理のエントリーポイントです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**GPU を使用する理由**  
GPU コアは並列ピクセル処理に優れており、高解像度スキャンの OCR に最適です。`DeviceId` を設定することで、どの物理カードを使用するかライブラリに指示できます。複数 GPU を搭載したワークステーションで便利です。

---

## 手順 3: OCR 用画像のロード

認識を行う前に、**load image for OCR** が必要です。Aspose は多数のフォーマット（JPEG、PNG、TIFF など）に対応した便利な静的ファクトリーメソッドを提供しています。

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **エッジケース:** 画像が 10 MB を超える場合、GPU メモリ不足を防ぐためにまずダウンサンプリングを検討してください。認識前に `ocrImage.Resize(width, height)` でサイズ変更できます。

---

## 手順 4: 文書からテキストを認識

エンジンが準備でき、画像がロードされたら、**recognize text from document** を実行する時です。`Recognize` メソッドはプレーンテキスト出力と追加メタデータを含む `OcrResult` オブジェクトを返します。

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**内部で何が起きているか**  
GPU エンジンはピクセルデータを CUDA カーネルにストリーミングし、二値化、文字分割、ニューラルネットワーク推論をすべて並列で実行します。そのため、CPU では数秒かかる **run OCR on image** ファイルを短時間で処理できるのです。

---

## 手順 5: 画像からテキストを抽出して出力

最後に、**extract text from image** を行い、結果を表示します。結果をファイルやデータベースに書き込んだり、下流の NLP パイプラインに渡すことも可能です。

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**期待される出力**（簡略化）:

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

プログラムを実行して上記のようなブロックが表示されたら、GPU 加速で **run OCR on image** に成功したことになります。おめでとうございます！

---

## GPU がない環境での対処（フォールバック）

デプロイ先のマシンに対応 GPU が無い場合はどうすればよいでしょうか？`GpuOcrEngine` のコンストラクタは `GpuNotSupportedException` をスローします。初期化を try‑catch でラップし、以下のように `OcrEngine`（CPU）にフォールバックしてください：

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

このパターンにより、ハードウェアに関係なくアプリが機能し続けるため、クラウド展開時の重要な考慮点となります。

---

## 完全動作例（コピー＆ペースト可能）

以下は **entire program** です。欠けている部分はなく、ファイルパスを自分の環境に合わせて置き換えるだけです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **注:** 上記コードは自動的に **extract text from image** を行い、`ocr_result.txt` に書き込みます。必要に応じてパスを調整してください。

---

## よくある質問とヒント

| 質問 | 回答 |
|------|------|
| *特定の NVIDIA ドライバーが必要ですか？* | はい。CUDA 11.x 以降が推奨されます。正確な互換性は Aspose のリリースノートをご確認ください。 |
| *複数の画像を同時に処理できますか？* | 可能です。OCR 呼び出しを `Parallel.ForEach` ループでラップしてください。ただし GPU メモリの上限に注意してください。 |
| *OCR 結果に文字化けが含まれる場合は？* | 画像前処理を調整してみてください。認識前に `ocrImage.Binarize()` や `ocrImage.Deskew()` を使用します。 |
| *言語モデルを限定する方法はありますか？* | 英語のみが必要な場合は `gpuEngine.Language = OcrLanguage.English;` を設定して処理を高速化できます。 |

---

## 結論

これで、**complete, end‑to‑end solution** を使って **run OCR on image** ができるようになりました。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}