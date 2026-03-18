---
category: general
date: 2026-03-18
description: Aspose OCRでGPUデバイスを設定し、画像からテキストを迅速に抽出します。OCR用に画像を読み込む方法、領収書画像を認識する方法、そして正確な結果を得る方法を学びましょう。
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: ja
og_description: Aspose OCRでGPUデバイスを設定し、画像からテキストを高速に抽出します。このステップバイステップガイドに従って、OCR用に画像を読み込み、レシート画像を認識してください。
og_title: C#でOCR用GPUデバイスを設定する – 完全プログラミングガイド
tags:
- OCR
- C#
- GPU
- Aspose
title: C#でOCR用GPUデバイスを設定する – 完全プログラミングガイド
url: /ja/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR の GPU デバイスを設定する – 完全プログラミングガイド

高速な OCR 処理のために **set GPU device** が必要ですか？このガイドでは Aspose OCR を使用して GPU デバイスを設定する方法をステップバイステップで解説し、レシート画像から数行のコードだけでテキストを抽出する方法をご紹介します。  

画像の **load image for OCR** に苦労したことがある方や、高解像度スキャンから *how to extract text* したいと考えている方は、ここが最適です。最後まで読めば、レシート画像を認識しプレーンテキストを出力、GPU が利用できない場合は自動的にフォールバックする実行可能なプログラムが手に入ります。

## このチュートリアルでカバーする内容

以下を網羅します：

* Aspose OCR NuGet パッケージのインストール（唯一の外部依存）。  
* GPU デバイスの設定（`set GPU device`）と、必要に応じて別の GPU インデックスを選択する方法。  
* OCR 用の画像ファイルの読み込み – 多くの初心者がつまずく「load image for OCR」ステップも含みます。  
* 認識エンジンを実行して **recognize receipt image** の内容を取得。  
* 結果の文字列を抽出し、**extract text from image** してアプリで利用できる形にする方法。  

マジックや隠しドキュメントリンクはありません。Visual Studio にコピペしてすぐに実行できる、完全に自己完結したソリューションです。

## 前提条件

* .NET 6.0 以上（コードは .NET Core と .NET Framework でも動作）。  
* 適切なドライバーがインストールされた GPU 対応マシン – これがない場合、ライブラリは自動的に CPU モードに切り替わります。  
* サンプルのレシート画像（例：`receipt_highres.png`）をフルパスで参照できる場所に配置。  

以上です。NuGet パッケージが無い場合は、プロジェクトフォルダーで `dotnet add package Aspose.OCR` を実行してください。

---

## Step 1 – Set GPU Device in Aspose OCR

最初に行うべきことは OCR エンジンで **set GPU device** を行うことです。これにより、CPU ではなくグラフィックカードに重い処理をオフロードさせます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Why this matters:**  
エンジンが `ProcessingMode.Gpu` で動作すると、内部の CUDA カーネルが文字分割やニューラルネットワーク推論を劇的に高速化します。RTX 3080 のような最新 GPU では、高解像度レシートの OCR 時間が数秒からサブ秒へと短縮されます。

> **Pro tip:** どの GPU インデックスを使用すべきか分からない場合は、`OcrEngine.GetAvailableGpuDevices()`（新しいバージョンで利用可能）を呼び出し、最も空きメモリが多いデバイスを選びましょう。

---

## Step 2 – Load Image for OCR

エンジンの設定が完了したら、**load image for OCR** を行います。Aspose は `ImageStream` ラッパーを提供しており、ファイル I/O を抽象化し、メモリ・ネットワーク・ディスクからのストリームをサポートします。

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**What could go wrong?**  
ファイルパスが間違っている、または画像が破損している場合、`FromFile` は `FileNotFoundException` をスローします。`File.Exists(imagePath)` で事前にチェックすれば、クラッシュを防げます。

---

## Step 3 – Recognize Receipt Image

画像が用意できたら `Recognize` を呼び出します。これが実際に **recognize receipt image** の内容を GPU 加速パイプラインで認識するステップです。

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Behind the scenes:**  
エンジンはまず画像を正規化されたグレースケールビットマップに変換し、続いて文字確率を予測するディープラーニングモデルを実行します。GPU 上で動作するため、ビットマップ全体を並列処理でき、大きなレシートでも高速に完了します。

---

## Step 4 – Extract Text from Image and Verify Output

最後に `OcrResult` からプレーンテキストを取得し、コンソールに出力します。ここで **extract text from image** が完了し、下流ロジック（例：項目のパース）に渡すことができます。

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Expected output:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

テキストが乱れている場合は、画像が高解像度であること、GPU ドライバーが最新であることを再確認してください。また、`ocrEngine.Settings.PreprocessMode` を切り替えて、光量が不足したレシートのコントラストを改善することもできます。

---

## Step 5 – Fallback to CPU (Edge Case Handling)

対象マシンに対応 GPU が無い場合はどうするか？クラッシュさせるのではなく、状況を検出して CPU 処理に切り替えることができます。

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Why include this?**  
CI パイプラインやクラウドコンテナでは、GPU の無いヘッドレスサーバーで実行されることが多々あります。優雅なデグレードを実装すれば、同一コードがどこでも動作します。

---

## Common Pitfalls and Practical Tips

| 落とし穴 | 回避方法 |
|---------|--------------|
| `ProcessingMode` を画像読み込み前に設定し忘れる | 常にエンジンを最初に構成する（Step 1）。 |
| 間違った GPU インデックス（`GpuDeviceId`）を使用する | 利用可能デバイスを問い合わせるか、デフォルトの `0` を使用する。 |
| 低解像度画像を読み込むと OCR 精度が低下する | レシートは最低でも 300 DPI を目指す。 |
| `ImageStream` を破棄しない – ファイルロックが残る | `using` ブロックでラップするか、手動で `Dispose()` を呼ぶ。 |
| CUDA が無いマシンで `IsGpuAvailable` フラグを無視する | Step 5 のフォールバックロジックを追加する。 |

---

## Full Working Example (Copy‑Paste Ready)

以下がコンパイル可能な完全プログラムです。`Program.cs` として保存し、Aspose OCR NuGet パッケージを追加して実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

プログラムを実行すると、先ほど示した通りに抽出されたレシートテキストがコンソールに表示されます。この文字列をパーサーやデータベース、その他任意のビジネスロジックに流し込むことができます。

---

## Conclusion

本稿では Aspose OCR で **set GPU device** を行い、**load image for OCR**、**recognize receipt image**、そして **extract text from image** を高速に実現する方法を示しました。完全に実行可能なサンプルは「やり方」と「理由」の両方を提供し、GPU 加速が必要な C# OCR プロジェクトの堅実な基盤となります。

次のステップに挑戦してみませんか？

* `Parallel.ForEach` を使って複数画像を並列処理。  
* `ocrEngine.Settings.PreprocessMode` を調整し、低コントラストスキャンの結果を改善。  
* OCR 出力を JSON にエクスポートして下流分析に活用。  

質問や問題があればコメントで教えてください。ハッピーコーディング！

![GPU デバイスを設定して OCR 処理を行う方法を示す図](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}