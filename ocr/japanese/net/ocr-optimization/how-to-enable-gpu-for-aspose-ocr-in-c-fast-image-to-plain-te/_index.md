---
category: general
date: 2026-02-24
description: Aspose OCR C# の例で GPU を有効にする方法 – 画像をすばやくプレーンテキストに変換します。GPU デバイス ID の設定と画像テキストの読み取り
  C# ガイドを含む。
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: ja
og_description: Aspose OCR C# のサンプルで GPU を有効にする方法。GPU デバイス ID の設定方法と、C# で画像テキストを効率的に読み取る方法を学びましょう。
og_title: C#でAspose OCRのGPUを有効にする方法 – 画像をテキストに素早く変換
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C#でAspose OCRのGPUを有効にする方法 – 画像からプレーンテキストへの高速変換
url: /ja/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR の GPU を C# で有効にする方法 – 画像からプレーンテキストへ高速変換

Aspose OCR を使って画像を編集可能なテキストに変換する際に **GPU を有効にする方法** を疑問に思ったことはありませんか？ あなた一人ではありません—多くの開発者が大量の請求書やスキャンした契約書を処理する際にパフォーマンスの壁にぶつかります。 良いニュースは、グラフィックカードを活用すれば、画像をプレーンテキストに変換する速度が光速のように速くなるということです。

このガイドでは、**Aspose OCR のサンプル** を通して、GPU の有効化方法、GPU デバイス ID の設定方法、そして **C# で画像テキストを読み取る** 方法を詳しく解説します。 最後まで読めば、CPU のみで実行する場合と比べて格段に短い時間で、サポートされている任意の画像からテキストを抽出できる実行可能なプログラムが手に入ります。

## 必要なもの

- .NET 6.0 以降（API は .NET Core と .NET Framework の両方で動作します）
- 最新ドライバーがインストールされた CUDA 対応 GPU
- Aspose.OCR for .NET のライセンス（または開発用に利用できる無料トライアル）
- Visual Studio 2022（またはお好みの C# エディタ）

`Aspose.OCR` 以外の NuGet パッケージは不要です—ライブラリ自体だけで完結します。

---

## Step 1 – Install the Aspose OCR NuGet Package

まずは公式の Aspose OCR ライブラリをプロジェクトに追加します。Package Manager Console を開き、次のコマンドを実行してください。

```powershell
Install-Package Aspose.OCR
```

これで `Aspose.OCR.dll` とそのすべての依存関係が取得されます。GUI が好きな方は、プロジェクトを右クリック → **Manage NuGet Packages** → *Aspose.OCR* を検索して **Install** をクリックしてください。  

*Pro tip:* インストール後、Solution Explorer の **Dependencies** 配下に `Aspose.OCR` フォルダーが表示されていることを確認しましょう。

---

## Step 2 – Create a Simple Console App Skeleton

OCR の全体フローを示す小さなコンソールアプリを作ります。新しいプロジェクトを作成してください。

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

生成された `Program.cs` を後述の完全コードに置き換えます。このスケルトンはクリーンなエントリーポイントを提供し、OCR ロジックに集中できるようにします。

---

## Step 3 – How to Enable GPU and Set GPU Device ID

ここが本題です：**Aspose OCR で GPU を有効にする方法**。ライブラリは `OcrSettings` オブジェクトを通じて `UseGpu` を切り替え、必要に応じて `GpuDeviceId` で特定の CUDA デバイスを指定できます。以下のコードスニペットをプログラムに組み込みます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Why Enable GPU?

GPU を有効にすると、ピクセル前処理、文字分割、ニューラルネットワーク推論といった重い処理がグラフィックカードにオフロードされます。たとえば GTX 1650 でも、CPU のみモードと比べて **2‑3 倍の速度向上** が期待でき、特に高解像度の文書で顕著です。

### Choosing a Device ID

マシンに複数の GPU が搭載されている場合、`GpuDeviceId` で対象を指定できます。`0` が最初のデバイス、`1` が2番目…という具合です。利用可能な ID は NVIDIA の `nvidia-smi` ツールや Aspose の `GpuInfo` クラス（ここでは省略）で確認できます。

---

## Step 4 – Full Working Example (Copy‑Paste Ready)

以下はそのまま実行可能な完全プログラムです。`Program.cs` に貼り付け、画像パスを実際のファイルに置き換えて **F5** を押してください。

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Expected Output

画像に *“Invoice #12345 – Total $1,250.00”* という行が含まれている場合、コンソールは次のように出力します。

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

結果はプレーンテキストとなり、データベースへの投入や自然言語パーサへの入力など、後続処理にすぐ利用できます。

---

## Step 5 – Verify GPU Utilisation (Optional)

GPU が実際に使用されているか確認するには、プログラム実行中に **NVIDIA‑Smi** や **GPU‑Z** といった GPU 監視ツールを開きます。選択したデバイスの Compute 使用率がスパイクしているはずです。CPU のみが動いているように見える場合は、以下を再確認してください。

- GPU ドライバーが最新であること
- `UseGpu` フラグが `true` に設定されていること
- 画像形式がサポート対象（PNG、JPEG、TIFF など）であること

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU not detected** | ドライバーが古い、または CUDA ランタイムが欠如している | 最新の NVIDIA ドライバーと CUDA ツールキットをインストール |
| **`Aspose.OCR` throws “GPU not supported”** | CUDA 非対応 GPU（例：古い AMD）で実行している | `UseGpu = false` に設定するか、対応 GPU に切り替える |
| **Incorrect image path** | 相対パスが誤ったフォルダーを指している | 絶対パスを使用するか、コマンドライン引数でパスを渡す |
| **License not applied** | 評価モードでは GPU 使用が制限される可能性がある | `License license = new License(); license.SetLicense("Aspose.OCR.lic");` でライセンスを登録 |

---

## Extending the Example: Batch Processing with GPU

多数の請求書を処理する必要がある場合は、認識呼び出しをループで囲みます。GPU が温まった状態を保てるため、以降の画像は **ウォームアップキャッシュ** の恩恵を受け、さらに数ミリ秒の高速化が期待できます。

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

同じ `OcrEngine` インスタンスを使い続けることを忘れずに—ファイルごとに新しいエンジンを作成すると GPU コンテキストが再初期化され、パフォーマンスが低下します。

---

## Conclusion

これで **Aspose OCR のサンプル** が完成し、**GPU の有効化方法**、**GPU デバイス ID の設定方法**、そして **C# で画像テキストを読み取る方法** がすべて網羅できました。`UseGpu` をオンにし、適切なデバイスを指定すれば、遅い CPU 限定の OCR 作業が高スループットなパイプラインに変わり、大量の請求書や領収書、スキャン文書を快適に処理できます。

ぜひ色々試してみてください：画像形式を変えてみる、マルチ GPU 環境で `GpuDeviceId` を調整する、あるいは他の Aspose ライブラリと組み合わせて PDF 生成などを行うなど、GPU が活躍すれば可能性は無限です。

<img src="gpu-ocr.png" alt="Aspose OCR で GPU を有効にして C# で画像をプレーンテキストに高速変換する方法">

*楽しいコーディングを！問題が発生したら下のコメント欄に書き込むか、Aspose の公式フォーラムで詳しい情報をチェックしてください。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}