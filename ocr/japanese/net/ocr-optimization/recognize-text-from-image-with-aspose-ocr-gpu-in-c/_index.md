---
category: general
date: 2026-03-29
description: Aspose OCR GPUエンジンを使用して画像からテキストを認識し、TIFFファイルからテキストを高速かつ効率的に抽出します。
draft: false
keywords:
- recognize text from image
- extract text from tiff
language: ja
og_description: C# で Aspose OCR GPU を使用して画像からテキストを瞬時に認識しましょう。TIFF ファイルからテキストを抽出する方法、デバイスの設定、よくある落とし穴の回避方法を学べます。
og_title: Aspose OCR GPUで画像からテキストを認識する – 完全ガイド
tags:
- OCR
- C#
- Aspose
- GPU
title: C#でAspose OCR GPUを使用して画像からテキストを認識する
url: /ja/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する Aspose OCR GPU – 完全ガイド

大容量の高解像度TIFFファイルから **画像からテキストを認識** したことがありますか？ あなたは一人ではありません。実務でアーカイブをスキャンしたり請求書を処理したりすると、普通のOCRライブラリでは処理しきれない巨大な .tif ファイルができあがります。  

幸い、Aspose OCR の GPU エンジンを使えば **画像からテキストを認識** でき、必要に応じて言語パックを自動ダウンロードしてくれます。このチュートリアルでは、メモリ予算を圧迫せずに **tiff からテキストを抽出** する方法も併せて紹介します。

## 必要な環境

- .NET 6（または最近の .NET ランタイム） – コードは .NET Core でも動作します。  
- Aspose.OCR for .NET NuGet パッケージ（バージョン 23.10 以降）。  
- 最低 2 GB VRAM を搭載した GPU – 任意ですが、大きなスキャンには強く推奨します。  

GPU が無くても CPU エンジンは動作します。その場合は `GpuOcrEngine` を `OcrEngine` に置き換えてください。  

## Aspose OCR for .NET のインストール

まず、ライブラリをプロジェクトに追加します。

```bash
dotnet add package Aspose.OCR
```

このコマンドでコア OCR クラスとオプションの GPU 名前空間の両方が取得されます。

## ステップ 1: GPU OCR エンジンの初期化

GPU 上で **画像からテキストを認識** するには `GpuOcrEngine` インスタンスを作成します。このオブジェクトはグラフィックドライバと直接通信するため、大きなラスターファイルでも大幅に高速化できます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

// Create a GPU‑accelerated OCR engine
var ocrEngine = new GpuOcrEngine();
```

> **なぜ重要か:** GPU エンジンは重い行列計算をグラフィックカードにオフロードします。特に 3000 × 4000 px 以上の高解像度TIFF（例: 3000 × 4000 px 以上）を扱うときに威力を発揮します。

## ステップ 2: (任意) GPU デバイスの選択とメモリ上限の設定

マシンに複数の GPU がある場合は `DeviceId` で選択できます。また、エンジンが確保できる VRAM を上限設定できるので、共有サーバーで便利です。

```csharp
// Choose the first GPU (ID 0) – change if you have more than one
ocrEngine.DeviceId = 0;

// Reserve at most 2 GB of VRAM for this OCR session
ocrEngine.MaxMemoryInMb = 2048;
```

> **プロのコツ:** バッチで数十ページを処理する場合、`MaxMemoryInMb` をカードの総メモリより少し低めに設定しておくと、メモリ不足によるクラッシュを防げます。

## ステップ 3: 言語の選択（必要に応じて自動ダウンロード）

Aspose OCR はデフォルトで英語を搭載していますが、任意の言語をリクエストできます。ローカルに言語ファイルが無い場合、エンジンが自動的に Aspose の CDN から取得します。

```csharp
// Set the recognition language – English in this example
ocrEngine.Language = Language.English;
```

> **エッジケース:** 日本語やアラビア語を認識したい場合は `Language.Japanese` や `Language.Arabic` を設定してください。初回呼び出し時にパックをダウンロードするため、数秒かかることがあります。

## ステップ 4: TIFF 画像からテキストを認識

いよいよ **tiff からテキストを抽出** します。`RecognizeImage` メソッドはプレーンテキスト、信頼度スコア、バウンディングボックスを含む `OcrResult` を返します。

```csharp
// Path to your high‑resolution TIFF file
string imagePath = @"C:\Scans\high_res_scan.tif";

// Perform OCR – this is where the GPU shines
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

> **なぜフルパスか:** 相対パスでも動作しますが、作業ディレクトリが異なる環境（例: VS Code と Visual Studio）で「ファイルが見つからない」エラーを防ぐために絶対パスを推奨します。

## ステップ 5: 認識結果の出力

最後にテキストをコンソールに出力するか、ファイルに書き込みます。`Text` プロパティには画像上の改行がそのまま保持されています。

```csharp
// Print the OCR output to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(result.Text);
```

**期待される出力**（簡略化）:

```
=== OCR RESULT ===
Invoice #12345
Date: 2026‑03‑01
Total: $1,274.56
Thank you for your business!
```

画像が複数ページの場合は、ページごとにループして結果を結合できます。

## 完全動作サンプル

すべてをまとめた、コピー＆ペーストで新しいコンソールプロジェクトに貼り付けられる自己完結型プログラムです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create the GPU OCR engine
        var ocrEngine = new GpuOcrEngine();

        // 2️⃣ (Optional) Pick GPU device & limit VRAM usage
        ocrEngine.DeviceId = 0;            // first GPU
        ocrEngine.MaxMemoryInMb = 2048;    // cap at 2 GB

        // 3️⃣ Choose language – English will be auto‑downloaded if missing
        ocrEngine.Language = Language.English;

        // 4️⃣ Path to the TIFF you want to process
        string tiffPath = @"YOUR_DIRECTORY/high_res_scan.tif";

        // 5️⃣ Run OCR – this returns the recognized text and metadata
        OcrResult result = ocrEngine.RecognizeImage(tiffPath);

        // 6️⃣ Show the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

ファイル名を `Program.cs` として保存し、`dotnet run` を実行すれば GPU が魔法のように働く様子が確認できます。

## TIFF からテキストを効率的に抽出 – 追加考慮点

### マルチページ TIFF の取り扱い

ソースファイルに複数ページが含まれる場合、Aspose OCR は各ページを別々の画像として扱います。以下のようにイテレートできます。

```csharp
var pages = ocrEngine.RecognizeMultipageImage(tiffPath);
foreach (var pageResult in pages)
{
    Console.WriteLine("--- Page ---");
    Console.WriteLine(pageResult.Text);
}
```

### 巨大スキャン時のメモリ管理

- **必要なときだけダウンサンプリング**: GPU エンジンは元解像度でも処理できますが、メモリ制限に達したら `ocrEngine.DownscaleFactor = 0.5;` などで縮小を検討してください。  
- **Dispose**: 終了時に `ocrEngine.Dispose();` を呼び出し、GPU リソースを速やかに解放します。

### よくある落とし穴

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| 出力が空 | `DeviceId` が間違っている、またはドライバ未初期化 | GPU ドライバを確認し、`DeviceId = 0` に設定するか省略してください。 |
| 精度が低い | 言語パックが間違っている | `ocrEngine.Language` を正しい言語に設定し、パックが完全にダウンロードされていることを確認してください。 |
| メモリ不足でクラッシュ | `MaxMemoryInMb` がカードの容量を超えている | 上限を下げるか、ページを1枚ずつ処理してください。 |

## プロのコツ & ベストプラクティス

- **バッチ処理**: GPU の VRAM が十分であれば `Parallel.ForEach` で OCR ループを並列化できますが、VRAM が足りない場合は順次処理でスロットリングを防ぎましょう。  
- **ロギング**: `ocrEngine.Logger = new ConsoleLogger();` を設定すると、詳細なタイミング情報が取得でき、パフォーマンスチューニングに役立ちます。  
- **セキュリティ**: 機密文書を扱う場合は `ocrEngine.Sanitize = true;` を有効にし、結果から隠しメタデータを除去してください。

## 結論

これで Aspose OCR の GPU エンジンを使って **画像からテキストを認識** するための、インストールからマルチページスキャン、メモリ制限まで網羅したエンドツーエンドのソリューションが完成しました。  

次のステップとして、OCR 出力の **ポストプロセッシング**（スペルチェック、正規表現による請求書番号抽出など）や、検索可能なアーカイブ用データベースへの格納を検討してみてください。JPEG や PNG など他フォーマットでも同じパイプラインが利用可能です—API はフォーマットに依存しません。

GPU の選択や言語パック、1日数百ページ規模へのスケールアップについて質問があれば、下のコメント欄でお気軽にどうぞ。Happy coding!  

![Diagram illustrating the OCR pipeline where a high‑resolution TIFF is fed into the GPU engine, producing recognized text output – recognize text from image](https://example.com/ocr-pipeline.png "Aspose OCR GPU エンジンを使用した画像からテキストを認識するパイプライン")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}