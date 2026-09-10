---
category: general
date: 2026-01-06
description: C#でAspose OCRのGPUアクセラレーションを使用して画像からテキストを抽出します。中国語テキストや高解像度ファイルなどに高速OCRを実現。
draft: false
keywords:
- extract text from image
- Aspose OCR
- GPU acceleration
- C# OCR tutorial
- Chinese OCR
language: ja
og_description: C#でAspose OCRのGPUアクセラレーションを使用して画像からテキストを抽出します。高解像度の中国語ページを高速かつ信頼性の高い方法でOCRする方法を学びましょう。
og_title: Aspose OCR と GPU を使用して画像からテキストを抽出する – C# ガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Aspose OCR と GPU を使用した画像からテキスト抽出 – C# ガイド
url: /ja/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR と GPU を使用した画像からテキスト抽出 – 完全 C# チュートリアル

画像から **テキストを抽出** したいけれど、ファイルが巨大で CPU がなかなか動かない…という経験はありませんか？同じ壁にぶつかる開発者は多いです。特に高解像度のスキャンや多言語ドキュメントを扱うときに顕著です。朗報です。Aspose OCR には GPU 加速パスが用意されており、遅い処理をほぼ瞬時に変えることができます。

このガイドでは、C# で Aspose OCR をセットアップし、CUDA ベースの GPU 加速を有効にして **画像からテキストを抽出** する手順を詳しく解説します。また、実際のシナリオとして、数メガバイトの TIFF に含まれる簡体字中国語テキストを認識する例も紹介するので、コードをそのままプロジェクトにコピペできます。

## 学べること

このチュートリアルを終えると、以下ができるようになります。

* Aspose.OCR NuGet パッケージをインストールし、参照する方法。  
* 大幅な速度向上を実現する **GPU 加速** に OCR エンジンを切り替える方法。  
* GPU パイプラインの恩恵を受けやすい最適な言語（例：**Chinese OCR**）を選択する方法。  
* 高解像度画像を読み込み、確実に **画像からテキストを抽出** する方法。  
* GPU デバイス選択やメモリ上限といった一般的な落とし穴への対処法。

GPU プログラミングの事前知識は不要です。基本的な C# 環境と対応 GPU があれば始められます。

## 前提条件

* .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）。  
* CUDA 対応 GPU（NVIDIA GeForce、Quadro、または Tesla）。  
* Visual Studio 2022（またはお好みのエディタ）。  
* Aspose.OCR NuGet パッケージ: `Install-Package Aspose.OCR`。  

これらが揃っていない場合は、特に GPU ドライバを先にインストールしてください。`UseGpu` フラグはドライバが認識できないと CPU にフォールバックします。

---

## 手順 1: OCR エンジンを **画像からテキストを抽出** 用に設定

まず `OcrEngine` のインスタンスを作成し、GPU モードを有効にします。必要に応じて GPU デバイスインデックス（0 が最初のカード）も指定できます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Initialize OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable CUDA‑based GPU acceleration
    UseGpu = true,

    // Optional: select a specific GPU device (0 = first GPU)
    GpuDeviceId = 0
};
```

**ポイント:** `UseGpu` を有効にすると、重い画像前処理とニューラルネットワーク推論が GPU にオフロードされ、巨大画像では CPU の 5〜10 倍の速度が期待できます。このステップを省くと結果は正確でも、大きなファイルではパフォーマンスが顕著に低下します。

> **プロのコツ:** `OcrEngine.IsGpuSupported` を出力して GPU が認識されているか確認してください。`false` が返った場合はドライババージョンを再確認しましょう。

## 手順 2: GPU 処理の恩恵を受けやすい言語を選択

Aspose OCR は多数の言語をサポートしていますが、文字セットが大きい **Chinese OCR** などは特に GPU の並列処理で効果が高いです。

```csharp
// Select Chinese Simplified for this example
ocrEngine.Language = OcrLanguage.ChineseSimplified;
```

`OcrLanguage.English` など他の言語に差し替えても構いません。その際は、使用する言語がパッケージに含まれていることを確認してください。

## 手順 3: 高解像度画像を読み込む

エンジンは `ImageStream` を介して画像を扱います。TIFF、PNG、JPEG のいずれかを指定してください。

```csharp
// Load a high‑resolution TIFF image
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\big_chinese_page.tif");
```

**エッジケース:** 画像がメモリ上で 8 KB を超える場合、古い GPU でのメモリ不足を防ぐためにダウンサンプリングを検討してください。`Bitmap` のリサイズ（DPI を維持）で精度を保ちつつ VRAM に収められます。

## 手順 4: 認識を実行し **抽出されたテキスト** を取得

`Recognize()` を呼び出します。`true` が返れば OCR 結果は `ocrEngine.Text` に格納されています。

```csharp
if (ocrEngine.Recognize())
{
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed. Check the image format and GPU settings.");
}
```

出力は認識された文字すべてを含むプレーンな Unicode 文字列です。中国語の場合は文字化けせず実際の字形が得られます—Aspose は内部で Unicode を扱っています。

### 期待される出力

ソース TIFF に簡体字中国語の段落が含まれていると仮定すると、次のような出力が得られます。

```
=== Extracted Text ===
在这个示例中，我们演示如何使用Aspose OCR与GPU加速来提取图像中的文本。
```

英語の画像であれば、同じコードで英語の文字列が返ります。

## 完全動作サンプル

以下は新規コンソールプロジェクトにそのまま貼り付けて実行できる、自己完結型のプログラムです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with GPU support
            OcrEngine ocrEngine = new OcrEngine
            {
                UseGpu = true,          // Switch pipelines to CUDA
                GpuDeviceId = 0         // Optional: select the first GPU
            };

            // Verify GPU availability (optional but helpful)
            if (!ocrEngine.IsGpuSupported)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
            }

            // 2️⃣ Choose language (Chinese Simplified for this demo)
            ocrEngine.Language = OcrLanguage.ChineseSimplified;

            // 3️⃣ Load a high‑resolution image
            string imagePath = @"C:\Images\big_chinese_page.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Perform recognition
            if (ocrEngine.Recognize())
            {
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – check the image and GPU settings.");
            }
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行するとコンソールに OCR 結果が表示されます。これで **画像からテキストを抽出** する処理が GPU 加速で完了です。

## よくある質問と落とし穴

| 質問 | 回答 |
|----------|--------|
| **CUDA 対応 GPU がない場合はどうすれば？** | `UseGpu = false` に設定すれば、エンジンは自動的に CPU パスに切り替わります。 |
| **複数画像をループで処理できるか？** | はい。同じ `OcrEngine` インスタンスを再利用し、各イテレーションで新しい `ImageStream` を割り当てれば可能です。 |
| **メモリリークはどう防止する？** | 長時間稼働するサービスでは、処理完了後に `ocrEngine.Dispose()` を必ず呼び出してください。 |
| **画像サイズに上限はあるか？** | 実質的な上限は GPU の VRAM です。4 GB 超の画像は、画像を小さなタイルに分割して処理することを検討してください。 |
| **Aspose OCR のライセンスはどこで取得？** | Aspose.com から無料トライアルを申し込み、`ocrEngine.License = new License("Aspose.OCR.lic");` と設定します。 |

## 次のステップと関連トピック

**画像からテキストを抽出** が効率的にできるようになったので、以下のテーマにも挑戦してみてください。

* **バッチ OCR パイプライン** – `Parallel.ForEach` と組み合わせて大量文書を高速処理。  
* **ポストプロセッシング** – 正規表現で一般的な OCR アーティファクトをクリーンアップ。  
* **Azure Cognitive Services との統合** – ローカル GPU OCR とクラウド OCR をコスト・精度で比較。  
* **他言語のサポート** – `OcrLanguage` を日本語、アラビア語などに変更するだけで対応可能。  

これらはすべて、ここで構築した Aspose OCR エンジンと GPU 加速をベースに拡張できます。

---

### 結論

C# で Aspose OCR の GPU 加速エンジンを使い、**画像からテキストを抽出** する方法を学びました。エンジンの初期化、CUDA の有効化、適切な言語選択、高解像度画像の読み込み、`Recognize()` の呼び出しという手順で、特に中国語のような複雑なスクリプトでも高速かつ信頼性の高い OCR 結果が得られます。

ぜひ自分のドキュメントで試し、言語や設定を変えてパフォーマンス向上を体感してください。問題が発生したら「よくある質問」表を再確認するか、コメントで質問を残してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}