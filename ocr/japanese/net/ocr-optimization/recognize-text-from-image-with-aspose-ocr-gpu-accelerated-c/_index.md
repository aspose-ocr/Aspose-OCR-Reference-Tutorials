---
category: general
date: 2026-03-20
description: Aspose OCR の GPU サポートを使用して C# で画像からテキストを認識し、高解像度画像を効率的にロードする方法を学びましょう。ステップバイステップのコードが含まれています。
draft: false
keywords:
- recognize text from image
- load high resolution image
language: ja
og_description: 高解像度画像を読み込み、Aspose OCRのGPUアクセラレーションを使用して、画像からテキストを迅速に認識する方法を発見しましょう。
og_title: 画像からテキストを認識 – C#で高速GPU OCR
tags:
- C#
- OCR
- Aspose
- GPU acceleration
title: Aspose OCRで画像からテキストを認識する – GPUアクセラレート C# ガイド
url: /ja/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識 – 高速GPUアクセラレートOCR（C#）

スキャナーから取得した巨大なTIFFスキャンで、**画像からテキストを認識**したいけど処理が遅く感じたことはありませんか？ あなただけではありません。請求書のデジタル化や歴史的文書のアーカイブ化といった実務プロジェクトでは、高解像度画像を読み込んでからOCRを実行することがパフォーマンスのボトルネックになることが多いです。  

良いニュースは、Aspose OCR の GPU エンジンを使えば、重い処理をグラフィックカードにオフロードでき、数分かかる処理が数秒に短縮されます。このチュートリアルでは、**高解像度画像**ファイルの読み込み、GPU 加速の有効化、画像から認識されたテキストの取得までを、クリーンで実行可能な C# コードで順を追って解説します。

---

## 学べること

- **Aspose.OCR.Gpu** NuGet パッケージのインストール方法  
- 大容量スキャンで `UseGpu = true` を有効にする重要性  
- メモリを圧迫せずに **高解像度画像** を正しく読み込む方法  
- 処理時間の測定と出力結果の検証方法  
- マルチページ TIFF の扱い方、CPU へのフォールバック、よくある落とし穴への対処法  

外部ドキュメントへのリンクは不要です。必要な情報はすべてここにあります。

---

## 前提条件

- .NET 6.0 以降（コードは `using var` 構文を使用）  
- 最新ドライバーがインストールされた GPU 対応システム（NVIDIA CUDA 12+ が最適）  
- Aspose OCR のライセンスファイル（無料トライアルでもテスト可能）  
- `high_res_page.tif` という名前の高解像度 TIFF 画像（例：300 DPI 以上）

---

## Step 1 – Aspose.OCR.Gpu パッケージのインストール

コードを書く前に、GPU 対応 OCR ライブラリをプロジェクトに追加します。Visual Studio のパッケージ マネージャ コンソールで次のコマンドを実行してください。

```powershell
Install-Package Aspose.OCR.Gpu
```

> **プロのコツ:** .NET CLI を使用する場合は、同等のコマンドは `dotnet add package Aspose.OCR.Gpu` です。これにより、ネイティブ CUDA カーネルを含む GPU 用バイナリが取得できます。

---

## Step 2 – GPU 用 OCR エンジン オプションの設定

エンジンに互換性のある GPU を使用するよう指示します。`UseGpu = true` を設定すると、ライブラリは自動的に最適なデバイスを選択（GPU が見つからない場合は CPU にフォールバック）します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR options
var ocrOptions = new OcrEngineOptions
{
    // Let Aspose select the optimal GPU; you can also specify DeviceId if needed
    UseGpu = true
};
```

**重要ポイント:** 大容量スキャンでは、GPU が数千ピクセルを同時並列で処理できるため、`ProcessingTime` が劇的に短縮されます。

---

## Step 3 – OCR エンジンの作成と言語設定

先ほど定義したオプションでエンジンをインスタンス化します。言語を English に設定すると、ラテン文字ベースのテキストの精度が向上します。

```csharp
// Initialize the OCR engine with GPU options
using var ocrEngine = new OcrEngine(ocrOptions);
ocrEngine.Language = Language.English;
```

> **エッジケース:** 文書に複数言語が混在する場合は、`Language.English | Language.Spanish` のようにカンマ区切りで指定できます。エンジンは各ブロックを自動検出します。

---

## Step 4 – OCR 用の高解像度画像を読み込む

**高解像度画像**を効率的に読み込むことは重要です。Aspose の `Image` クラスはファイル全体をメモリに読み込みますが、ギガバイトサイズのファイルを扱う場合はストリームで読み込むことも可能です。

```csharp
// Load the image from disk – replace the path with your actual file location
var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
var image = Image.FromFile(imagePath);
```

**代替アプローチ:** 超大型 TIFF の場合は、`Image.FromStream(File.OpenRead(imagePath))` に加えて `image.SetResolution(300, 300)` を使用し、フルラスタライズせずに DPI を制御すると便利です。

---

## Step 5 – OCR を実行し結果を取得

エンジンと画像の準備ができたら、認識はワンコールです。メソッドは `OcrResult` を返し、検出テキストとパフォーマンス指標の両方が含まれます。

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(image);
```

### 期待される出力

300 DPI の標準ページでコードを実行すると、次のような結果が得られます。

```
Detected text (1245 characters) in 312 ms
```

文字数やミリ秒は画像の複雑さや GPU モデルに依存しますが、単一ページで数百ミリ秒程度の処理時間が期待できます。

---

## Step 6 – 認識結果テキストの表示（任意）

実際の OCR 出力を確認したい場合は、`ocrResult.Text` をコンソールやログファイルに書き出すだけです。

```csharp
Console.WriteLine("--- OCR Text Start ---");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("--- OCR Text End ---");
```

**この操作が有用な理由:** 生テキストを確認することで、特殊文字・改行・書式が正しく保持されているかを検証でき、後続のパース処理がスムーズになります。

---

## Step 7 – 複数ページとフォールバックシナリオの処理

### マルチページ TIFF

ソースファイルに複数ページが含まれる場合は、次のようにループします。

```csharp
var multiPage = Image.FromFile(imagePath);
foreach (var page in multiPage.GetPages())
{
    var result = ocrEngine.Recognize(page);
    Console.WriteLine($"Page {page.Index}: {result.Text.Length} chars, {result.ProcessingTime} ms");
}
```

### GPU が利用できない場合

サーバーに互換性のある GPU が無いこともあります。Aspose は自動的に CPU にフォールバックしますが、現在のモードは次のコードで検出できます。

```csharp
if (!ocrEngine.IsGpuEnabled)
{
    Console.WriteLine("GPU not detected – using CPU fallback. Consider installing CUDA drivers for better performance.");
}
```

---

## 完全動作サンプル

以下は新しいコンソール プロジェクトにコピペできるフルプログラムです。上記の手順すべてを含み、テキスト長と経過時間の両方を出力します。

```csharp
// ------------------------------------------------------------
// Full example: recognize text from image with GPU acceleration
// ------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR.Gpu via NuGet before running this code.

        // 2️⃣ Configure OCR options to enable GPU
        var ocrOptions = new OcrEngineOptions
        {
            UseGpu = true
        };

        // 3️⃣ Create the OCR engine and set language
        using var ocrEngine = new OcrEngine(ocrOptions);
        ocrEngine.Language = Language.English;

        // 4️⃣ Load a high‑resolution image (adjust the path accordingly)
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var image = Image.FromFile(imagePath);

        // 5️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ Output results
        Console.WriteLine($"Detected text ({ocrResult.Text.Length} characters) in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("--- OCR Text Start ---");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("--- OCR Text End ---");

        // 7️⃣ Optional: check if GPU was actually used
        if (!ocrEngine.IsGpuEnabled)
        {
            Console.WriteLine("Warning: GPU not enabled – falling back to CPU.");
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すれば、コンソールに処理時間が表示されます。

---

## よくある落とし穴と回避策

| 症状 | 想定原因 | 対策 |
|------|----------|------|
| **`ProcessingTime` が 2 秒以上**（300 DPI ページ） | GPU ドライバーが未インストールまたは古い | 最新の NVIDIA ドライバーと CUDA ツールキットをインストール |
| **600 DPI TIFF 読み込み時に Out‑of‑memory 例外** | 画像が RAM に対して大きすぎる | 画像をストリームで処理するか、`image.SetResolution(300,300)` でダウンサンプル |
| **出力にゴミ文字** | 言語設定が誤っている | `ocrEngine.Language` を文書の言語に合わせて設定 |
| **`IsGpuEnabled` が false** | GPU の無いヘッドレスサーバーで実行 | CPU 専用 NuGet パッケージを使用するか、仮想 GPU（例：NVIDIA GRID）を構成 |

---

## 次のステップと関連トピック

- **バッチ処理:** マルチページループと `async/await` を組み合わせ、複数ファイルを並列 OCR する  
- **ポストプロセス:** 正規表現で改行を整形したり、日付・金額などの構造化データを抽出  
- **代替ライブラリ:** コスト・ベネフィット比較のために Tesseract 4.0 や Azure Computer Vision と比較  
- **GPU チューニング:** GPU が複数ある場合は `ocrOptions.GpuDeviceId` を調整してみる  

---

## 結論

本ガイドでは、**画像からテキストを認識**する際に **高解像度画像** を読み込み、Aspose OCR の GPU 加速を活用する方法を解説しました。これで、パフォーマンス測定、マルチページ文書の処理、GPU が無い環境へのフォールバックをすべて網羅した、すぐに実行可能な C# プログラムが手に入ります。  

自分のスキャン（レシートの山や歴史的新聞のバッチなど）で試してみてください。手頃な GPU が遅い OCR 作業をほぼ瞬時に変える様子が実感できるはずです。  

このチュートリアルが役立ったら、Aspose OCR の GitHub リポジトリにスターを付けたり、チームと記事を共有したり、上記の「プロのコツ」を試してみてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}