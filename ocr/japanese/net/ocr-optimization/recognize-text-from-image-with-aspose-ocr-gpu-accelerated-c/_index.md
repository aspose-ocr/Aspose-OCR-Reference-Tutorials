---
category: general
date: 2026-01-13
description: Aspose OCR を使用して画像からテキストを認識し、レシートからテキストを迅速に抽出する方法を学びます。OCR 用に画像をロードし、GPU
  デバイス ID を設定する手順が含まれています。
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: ja
og_description: Aspose OCRで画像からテキストを即座に認識しましょう。OCR用に画像を読み込み、GPUデバイスIDを設定し、レシートからテキストを抽出する手順をご覧ください。
og_title: 画像からテキストを認識 – 完全GPUアクセラレートC#ガイド
tags:
- Aspose OCR
- C#
- GPU computing
title: Aspose OCRで画像からテキストを認識する – GPUアクセラレートされたC#チュートリアル
url: /ja/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識 – 完全GPUアクセラレートC#ガイド

画像からテキストを**認識**したいけれど、CPU版が非常に遅いと感じたことはありませんか？レシートの**テキスト抽出**を試みていて、遅延がユーザー体験を損なっているかもしれません。良いニュースは、遅いパフォーマンスに妥協する必要はないということです—Aspose OCR の GPU パッケージを使えば処理が高速化され、コードは数行だけです。

このチュートリアルでは、**OCR 用に画像をロード**し、**GPU デバイス ID を設定**し、最終的にプレーンテキスト結果を取得するまでの、完全に実行可能なサンプルを順に解説します。最後まで読めば、サポートされている NVIDIA カードが搭載された最新の Windows または Linux マシンで動作する、すぐに使えるスニペットが手に入ります。

---

## 必要な環境

- **.NET 6+**（または .NET Framework 4.7.2+） – API は両方に対応しています。  
- **Aspose.OCR** NuGet パッケージ **＋** **Aspose.OCR.Gpu** アドオン。  
- 最低 2 GB VRAM を搭載した NVIDIA GPU（デモは 1 GB まで使用します）。  
- サンプル画像、例：スキャンしたレシート (`receipt.jpg`)。

既にプロジェクトがある場合は、`dotnet add package Aspose.OCR` と `dotnet add package Aspose.OCR.Gpu` を実行するだけです。追加のネイティブライブラリは不要で、SDK が必要な CUDA バイナリを同梱しています。

---

## ステップバイステップ実装

### ## Aspose OCR と GPU を使用して画像からテキストを認識する方法

以下は **完全な単体実行プログラム** です。新しいコンソールプロジェクトに貼り付けて `Ctrl+F5` で実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **プロのコツ:** マシンに複数の GPU がある場合は、`DeviceId` を `1`、`2` などに変更して、負荷の少ないカードを選択してください。ID が範囲外の場合、SDK は明確な `GpuDeviceNotFoundException` をスローします。

### ### ステップ 1: OCR 用に画像をロード

`OcrImage.FromFile` は単にビットマップを読み込むだけでなく、内部ヒューリスティックに基づいて画像を前処理（デスキュー、二値化）します。これが **OCR 用に画像をロード** が別ステップとなる理由です。画像がデータベースに保存されている場合は、`MemoryStream` に差し替えることも可能です。

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

メモリ上にある画像から **画像からテキストを認識** したい場合は次のようにします：

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### ステップ 2: GPU デバイス ID とメモリ上限を設定

GPU リソースは有限です。`DeviceId` と `MaxMemoryMb` を公開することで、Aspose は **GPU デバイス ID を設定** でき、1 つのプロセスがカード全体を占有するのを防ぎます。

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

メモリ上限を超えると、エンジンは自動的にシステム RAM にスワップします。これは遅くなりますが、クラッシュを防止します。

### ### ステップ 3: レシートからテキストを抽出（画像からテキストを認識）

`Recognize` メソッドが本格的な処理を行います。Aspose OCR がサポートする任意の言語を指定できます。レシートの場合、英語がほとんどの場合で機能しますが、`OcrLanguage.Spanish` やカスタム言語パックを追加することも可能です。

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**期待される出力**（サンプル）：

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## よくあるバリエーションとエッジケース

| シチュエーション | 変更点 | 理由 |
|-------------------|--------|------|
| **1 枚の画像に複数のレシートがある** | `ocrEngine.Recognize` を各切り抜き領域（`OcrImage.Crop` 使用）で呼び出す | エンジンが小さくクリーンな領域を処理するため、精度が向上します。 |
| **低解像度スキャン (<150 dpi)** | 認識前に `receiptImage.Resize(2.0)` でアップスケール | ピクセル密度が高くなると、GPU が扱えるデータが増えます。 |
| **英語以外のレシート** | `OcrLanguage.French`（またはカスタム `.traineddata`）を渡す | 言語固有のモデルが誤検出を減らします。 |
| **GPU が利用できない** | `try‑catch` 内で `OcrEngine`（CPU）にフォールバック | ヘッドレスサーバーでもアプリが動作し続けます。 |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## 本番向け OCR のヒント

- **バッチ処理:** 認識ループを `Parallel.ForEach` でラップするが、GPU ストリーム数（通常 1‑2）に合わせて並列度を制限する。  
- **メモリ管理:** `OcrImage` オブジェクトは速やかに破棄（`receiptImage.Dispose()`）する。特に数千枚のレシートを処理する場合は必須です。  
- **ロギング:** 各行の `ocrResult.Confidence` を取得し、低信頼度は手動レビューに回す。  
- **セキュリティ:** 機密レシートを扱う際は、画像ファイルを暗号化された一時フォルダーに保存し、処理後に削除する。

---

## 結論

これで **画像からテキストを認識** するための **完全な実行可能サンプル** が完成しました。Aspose OCR の GPU 加速を利用して **OCR 用に画像をロード**、**GPU デバイス ID を設定**、そして **レシートからテキストを抽出** する手順を数行で実装できます。コードはコピー＆ペースト可能で、マルチ言語・マルチ GPU・高スループットシナリオへの適応に必要な説明も含まれています。

次のチャレンジに挑みますか？`GpuOcrEngine` にライブビデオストリームを流し込みリアルタイムレシートスキャンを実装したり、結果を会計 API に統合したりしてみてください。高速 GPU OCR と洗練された C# 設計を組み合わせれば、可能性は無限です。

*Happy coding, and may your OCR be ever swift!*

![画像からテキストを認識するデモスクリーンショット](placeholder-image.png "画像からテキストを認識する例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}