---
category: general
date: 2026-06-03
description: Aspose OCR C# の例で、GPU メモリ制限の設定方法、OCR 用画像の読み込み、TIF ファイルからのテキスト認識をフルコードとヒント付きで示しています。
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: ja
og_description: 完全なAspose OCR C#サンプルを学びましょう：GPUを有効にし、GPUメモリ上限を設定し、OCR用に画像を読み込み、TIFファイルからテキストを認識します。フルコードが含まれています。
og_title: Aspose OCR C# サンプル – GPU 加速、メモリ制限、TIF 処理
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Aspose OCR C# サンプル – GPU を有効化、メモリ制限を設定、TIF 画像を処理
url: /ja/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# Example – GPU を有効化、メモリ制限を設定、TIF 画像を処理

大量の TIFF スキャンを扱うとき、**Aspose OCR C# example** のコードから最大のパフォーマンスを引き出す方法を考えたことはありますか？ 多くの実務プロジェクト—例えばアーカイブのデジタル化や高解像度レシートからのデータ抽出—では、ボトルネックは OCR アルゴリズムそのものではなく、ハードウェアの活用方法にあります。

ポイントは次のとおりです。Aspose OCR は GPU アクセラレーションをサポートしていますが、使用できるメモリ量を明示的に指定し、適切な画像タイプをロードし、最終的に .tif ファイルから認識テキストを取得する必要があります。このチュートリアルでは、SDK のインストールから GPU 設定の調整まで、すべての手順を詳しく解説します。GPU の RAM を使い果たすことなく、超高速 OCR を実現できるようになります。

さらに、マルチページ TIFF の扱い方や GPU が存在しない環境で CPU にフォールバックする方法など、いくつかの「もしも」シナリオも紹介します。これにより、単なるワンショットのコードではなく、堅牢なソリューションが手に入ります。

## 必要なもの

作業を始める前に、以下の項目がマシンに揃っていることを確認してください。

| 前提条件 | 重要な理由 |
|--------------|----------------|
| **.NET 6 SDK**（またはそれ以降） | Aspose OCR は .NET Standard 2.0+ を対象としているため、最近の .NET バージョンであれば動作します。 |
| **Aspose.OCR NuGet パッケージ** (`Install-Package Aspose.OCR`) | `OcrEngine`、`GpuSettings` などのコアライブラリです。 |
| **CUDA 11+**（NVIDIA） **または ROCm 5+**（AMD） | GPU アクセラレーションに必須です。SDK は実行時に互換性のあるドライバーをチェックします。 |
| **最低 2 GB VRAM を搭載した GPU**（ここでは 2048 MB に上限を設定） | メモリが不足するとエンジンは自動的に CPU にフォールバックします。 |
| **処理したい高解像度 TIFF 画像** | Aspose OCR は事実上すべてのラスタ形式を読み取れますが、スキャン画像では TIF が一般的です。 |
| Visual Studio 2022（またはお好みのエディタ） | C# プロジェクトのビルドとデバッグに使用します。 |

これらのいずれかが欠けていてもコードはコンパイルできますが、期待するパフォーマンス向上は得られません。

## Step 1: Aspose OCR C# Example エンジンの作成

すべての **Aspose OCR C# example** の最初のステップは OCR エンジンのインスタンス化です。`OcrEngine` は映画の監督のようなものです—画像の読み込みからテキスト抽出まで全てを調整します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **プロのコツ:** 連続して多数の画像を処理する場合は、`OcrEngine` を 1 つだけ保持してください。画像ごとにエンジンを再生成すると、OCR 時間をはるかに上回るオーバーヘッドが発生します。

## Step 2: GPU メモリ制限の設定（およびアクセラレーションの有効化）

ここで多くの人が躓くポイント、**GPU メモリ制限の設定** です。デフォルトでは Aspose OCR は利用可能な VRAM をすべて使おうとしますが、共有ワークステーションでは他のアプリケーションがメモリ不足になる恐れがあります。`GpuSettings` オブジェクトを使って割り当て上限を設定できます。

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### なぜメモリ制限を設定するのか？

- **安定性:** 巨大画像を処理中のメモリ不足クラッシュを防止します。  
- **共存性:** TensorFlow など GPU を多用する他アプリと同時に動作させられます。  
- **予測可能性:** GPU がスワップしなくなるため、パフォーマンス測定が再現性を持ちます。

`MemoryLimitMb` を省略すると、Aspose は必要と判断した分だけメモリを確保します。専用の推論サーバーでは問題ありませんが、開発用ノート PC ではリスクがあります。

## Step 3: OCR 用画像のロード

正しいファイル形式のロードは次に重要なステップです。`OcrImage.FromFile` は自動で画像タイプを判別しますが、ファイルの存在確認と、サポートされている TIFF バリアント（例: LZW 圧縮、CCITT‑G4）であることの検証は行っておくべきです。

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### マルチページ TIFF の扱い方

TIFF に複数ページが含まれている場合、Aspose OCR はデフォルトで最初のページしか読み取りません。すべてのページを処理したいときは、`image.Pages`（新しい SDK バージョンで利用可能）をループし、各ページをエンジンに個別に渡します。

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

上記スニペットは、シングルページでもマルチページでも機能する **load image for OCR** パターンを示しています。

## Step 4: TIF（または任意のラスタ画像）からテキストを認識

画像がメモリ上にロードされたら、Aspose に魔法をかけてもらいます。`Recognize` メソッドは `OcrResult` を返し、プレーンテキスト、信頼度スコア、必要に応じてバウンディングボックス情報も取得できます。

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### TIF でうまく動作する理由

- **ロスレス圧縮:** TIFF は生のピクセルデータを保持することが多く、OCR エンジンに最高の忠実度を提供します。  
- **多彩なカラースペース:** Aspose はグレースケール、RGB、さらには CMYK TIFF も追加の変換コードなしで処理できます。

言語パック（例: フランス語や日本語）を使用したい場合は、`ocrEngine.Settings.Language = "fr"` のように `Recognize` 呼び出し前に設定してください。

## Step 5: 認識結果テキストの表示

最後に、テキストをコンソールへ出力します。実際のアプリケーションでは、データベースや JSON ファイルへの書き込み、あるいは下流の NLP パイプラインへの入力として利用することが多いでしょう。

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 期待される出力例

300 dpi の鮮明な印刷ページを処理した場合、次のような結果が得られます。

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

画像がぼやけていたり、GPU メモリ制限が低すぎると、文字化けや結果の切れ端が見られることがあります。画像のフットプリント（6000×8000 ピクセルの TIFF で約 1 GB 程度）より `MemoryLimitMb` を下回ると、エンジンは自動的に CPU にフォールバックします。

## 完全動作サンプル

以下はそのまま実行可能なプログラムです。新しいコンソール アプリ プロジェクトに貼り付け、`YOUR_DIRECTORY/large_photo.tif` を自分の TIFF パスに置き換えて **F5** を押してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 確認チェックリスト

- ✅ **Aspose OCR C# example** がエラーなくコンパイルできる。  
- ✅ **GPU が有効**（`Enable = true`）。  
- ✅ **GPU メモリ制限** が 2048 MB に設定されている。  
- ✅ **画像が TIF ファイル** からロードされている。  
- ✅ **テキストが認識され、コンソールに出力** される。

## よくある落とし穴と回避策

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| `System.DllNotFoundException: cudart64_110.dll` | CUDA ランタイムが未インストール、またはバージョン不一致。 | ドライバーに合わせた CUDA 11.x（または 12.x）をインストール。 |
| OCR が空文字列を返す | 画像が暗すぎる、または DPI が 150 未満。 | `image.AdjustContrast()` でコントラスト調整、または 300 dpi にリサンプリング。 |
| GPU でメモリ不足クラッシュ | `MemoryLimitMb` が画像に対して低すぎる。 | 上限を引き上げるか、`image.Crop` でタイルに分割。 |
| `Unsupported image format` エラー | TIFF が JPEG‑2000 など特殊圧縮を使用。 | ImageMagick などでサポートされている形式に変換してから OCR にかける。 |

## デモの拡張例

堅実な **aspose ocr c# example** が手に入ったので、次のような拡張に挑戦できます。

- **バッチ処理:** フォルダ内の TIF を順に走査し、各結果を `.txt` ファイルに書き出す。  
- **言語パック:** `ocrEngine.Settings.Language = "es"` でスペイン語、またはカスタム辞書をロード。  
- **バウンディングボックス:** `ocrResult.Regions` を利用して単語ごとの座標を取得—赤字消去ツールに便利。  
- **CPU フォールバック:** GPU ブロックを try/catch で囲み、失敗時に `ocrEngine.Settings.Gpu.Enable = false` に切り替えて再実行。

これらの拡張はコアパターンを保ちつつ、特定のユースケースに合わせた価値を追加します。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした、関連性の高いトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれているので、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりする際に役立ちます。

- [画像からテキストを抽出する Aspose.OCR .NET の使い方](/ocr/english/net/image-and-drawing-recognition/)
- [画像からテキストを抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)
- [言語選択付き C# で画像テキスト抽出 – Aspose.OCR の使用例](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}