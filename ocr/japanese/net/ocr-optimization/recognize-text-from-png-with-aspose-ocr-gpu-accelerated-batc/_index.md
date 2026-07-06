---
category: general
date: 2026-04-01
description: Aspose OCRでGPUデバイスIDを設定し、GPUアクセラレーションを有効にして、pngファイルからテキストを迅速に認識する方法を学びましょう。ステップバイステップのC#ガイド。
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: ja
og_description: GPUデバイスIDを設定してPNGファイルからテキストを高速に認識します。Aspose OCRでGPUアクセラレーションを有効にする完全なC#ガイドをご覧ください。
og_title: PNGからテキストを認識する – GPUアクセラレートされたAspose OCRチュートリアル
tags:
- C#
- OCR
- GPU
- Aspose
title: Aspose OCRでPNGからテキストを認識 – GPU加速バッチデモ
url: /ja/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを認識 – 完全なC# GPUアクセラレートバッチチュートリアル

PNG画像から**テキストを認識**したいけれど、処理が非常に遅いと感じたことはありませんか？ あなたは一人ではありません。多くの開発者はシンプルな OCR 呼び出しから始め、フォルダーに数十枚のスクリーンショットがあるとコンソールがカタツムリのように進むのを見つめます。

朗報です。Aspose OCR は重い処理をグラフィックカードにオフロードでき、数行のコードで**GPU デバイス ID を設定**すれば、使用したい GPU を正確に指定できます。このガイドでは、フォルダー内のすべての PNG を取得し、GPU 加速を有効にし、最初の GPU を選択し、各ファイルの文字数を出力する、完全に実行可能なサンプルを順に解説します。

最後まで読むと、任意の .NET プロジェクトに貼り付けられる自己完結型プログラムが手に入り、GPU を有効にする意義、エッジケースの処理方法、さらなるパフォーマンス向上のための調整ポイントが理解できるようになります。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Core でもコンパイル可能）  
- **Aspose.OCR** NuGet パッケージ – `dotnet add package Aspose.OCR` でインストール  
- CUDA 対応 GPU（一般的には NVIDIA）と適切なドライバーを備えたマシン  
- 処理したい **PNG** 画像が入ったフォルダー  

これらに心当たりがなくても慌てないでください。以下の手順に正確なコマンドが記載されており、GPU が無い場合の対処法も説明します。

## 手順 1: OCR エンジンを初期化し GPU 加速を有効化

まず `OcrEngine` インスタンスを作成し、GPU サポートをオンにします。このフラグにより Aspose は内部でネイティブ CUDA ライブラリを使用します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**重要ポイント:** `UseGpuAcceleration` を設定しないと、各画像は CPU で処理されます。特に高解像度 PNG の場合、処理速度は桁違いに遅くなります。このフラグを有効にすると、後で特定の GPU デバイスを指定できるようになります。

## 手順 2: GPU デバイス ID を設定（任意だが推奨）

ワークステーションに複数の GPU が搭載されている場合、使用する GPU を選択できます。デバイス ID は **0** から始まり、`0` が最初の GPU、`1` が二番目の GPU です。

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**プロのコツ:** 共有サーバー上で実行する場合、GPU デバイス ID を明示的に設定すると、他プロセスからリソースを奪うことを防げます。この行を省略すると、Aspose はデフォルトデバイスを自動選択しますが、単一 GPU 環境では通常問題ありません。

## 手順 3: バッチフォルダー内のすべての PNG ファイルを取得

次に OCR を実行したい PNG をすべて探します。`Directory.GetFiles` メソッドがその役割を担います。

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**エッジケース:** フォルダーが空の場合、`imageFiles` は空配列になります。後ほどフレンドリーなメッセージで対処します。

## 手順 4: 各画像を処理し、認識された文字数を出力

ここがメインループです。各 PNG に対して `Recognize` を呼び出し、ファイル名と抽出テキストの長さを表示します。

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**出力例:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

画像にテキストが含まれていなければ、カウントは `0` になります。これは、純粋にグラフィックだけのスクリーンショットでは普通の結果です。

## 手順 5: プログラムを実行し GPU 使用状況を確認

ファイルをコンパイル（`dotnet build`）し、実行（`dotnet run`）します。コンソールがスクロールしている間に、GPU 監視ツール（例: NVIDIA Smi）を開き、各画像処理時に GPU 使用率が一瞬上がるのを確認してください。何も表示されない場合は以下を再確認してください。

1. CUDA ドライバーがインストールされているか  
2. `UseGpuAcceleration` が `true` に設定されているか  
3. 正しい `GpuDeviceId` が実際の GPU と一致しているか  

GPU が利用できない場合、Aspose は自動的に CPU にフォールバックしますが、速度優位は失われます。

## よくあるバリエーションとヒント  

| シチュエーション | 変更点 |
|-----------|----------------|
| **別の画像形式**（例: JPEG） | 検索パターンを `*.jpg` または `*.*` に変更すれば、Aspose は依然としてテキストを認識します。 |
| **バッチサイズが非常に大きい**（数千ファイル） | メモリ圧迫を防ぐためにチャンク処理を行う：`imageFiles` を小さな配列に分割します。 |
| **文字列そのものが必要** | `WriteLine` 内の `ocrResult.Text.Length` を `ocrResult.Text` に置き換えます。 |
| **ヘッドレスサーバーで実行** | サーバーに GPU ドライバーが無い場合は `UseGpuAcceleration = false` に設定し、不要なエラーを回避します。 |
| **複数 GPU を使い負荷を分散** | `foreach` 内で `ocrEngine.GpuDeviceId = i % gpuCount` としてデバイスをローテーションします。 |

## 期待される出力と検証  

すべてが正しく動作すれば、コンソールは各ファイル名と文字数を先ほどの例のように表示します。実際の OCR 結果を確認したい場合は、一時的にテキストを出力してみてください。

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

大量バッチではこの行を削除またはコメントアウトしてください。数千行の出力はターミナルを埋め尽くしてしまいます。

## 完全動作サンプル（コピー＆ペースト用）

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

このコードを `GpuBatchDemo.cs` として保存し、`dotnet add package Aspose.OCR`、続いて `dotnet run` を実行します。GPU 加速のおかげで、各 PNG の文字数がほぼ瞬時に表示されるはずです。

## まとめ  

これで **PNG からテキストを認識** する際に GPU 加速を有効にし、Aspose OCR で **GPU デバイス ID を設定** する方法がマスターできました。フォルダー探索、エッジケースチェック、OCR パフォーマンスの即時フィードバックをすべて網羅した、コピー＆ペースト可能なプログラムが完成です。

次のステップは？`Recognize` 呼び出しを `ocrEngine.RecognizeAsync` に置き換えて非同期処理にしたり、Aspose が提供する画像前処理オプション（例: 二値化）を試したりしてください。また、OCR 結果をデータベースや検索インデックスに流し込めば、全文検索ソリューションが構築できます。

マルチページ PDF の取り扱いや、Tesseract との性能比較に関する質問があればコメントを残すか、**バッチ OCR C#**、**OCR パフォーマンスのコツ**、**GPU 主導の画像処理** といった他のチュートリアルもぜひご覧ください。Happy coding!  

![Console output showing recognised character counts for PNG files – recognize text from png using GPU acceleration](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}