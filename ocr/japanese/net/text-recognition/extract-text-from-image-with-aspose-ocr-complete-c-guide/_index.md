---
category: general
date: 2026-03-04
description: C#でAspose OCRを使用して画像からテキストを抽出します。OCR用に画像を読み込む方法と、TIFFファイルからテキストを効率的に認識する方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for ocr
- recognize text from tiff
- Aspose OCR C#
- GPU OCR engine
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、OCR用に画像をロードし、GPUエンジンでTIFFファイルからテキストを認識する方法を示します。
og_title: Aspose OCRで画像からテキストを抽出する – C#チュートリアル
tags:
- OCR
- C#
- Aspose
- GPU
title: Aspose OCRで画像からテキストを抽出する – 完全なC#ガイド
url: /ja/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する – Aspose OCR 完全 C# ガイド

画像から **テキストを抽出** したいけど、速度と精度の両方を満たすライブラリがどれか分からない…という経験はありませんか？ スキャンした PDF や TIFF アーカイブを扱うとき、多くの開発者が同じ壁にぶつかります。朗報です。Aspose OCR と GPU 対応エンジンを組み合わせれば、プロセスが驚くほどスムーズになります。

このチュートリアルでは、**OCR 用に画像をロード** する方法、GPU エンジンの設定方法、そして数行のコードで **TIFF からテキストを認識** する手順をすべて解説します。最後には、抽出したテキストをコンソールに出力する実行可能なコンソールアプリが完成し、各ステップの「なぜ」も理解できるようになります。

## 学べること

- Aspose.OCR NuGet パッケージのインストールと参照方法
- GPU 加速された `GpuOcrEngine` が処理時間を劇的に短縮する理由
- `ImageInfo` を使った **OCR 用に画像をロード** する正しい方法
- 言語設定とメモリ上限の構成方法
- **TIFF からテキストを認識** し、よくある落とし穴に対処する方法

Aspose の事前知識は不要です。C# と .NET の基本が分かっていれば大丈夫です。さっそく始めましょう。

---

## Step 1: Extract Text from Image – Initialize the GPU OCR Engine

最初に必要なのは、ピクセルを実際に読み取れる OCR エンジンです。Aspose が提供する `GpuOcrEngine` は、重い処理を GPU にオフロードします。大量の高解像度 TIFF がキューに並んでいる場合に特に有効です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine.
// Setting GpuMemoryLimit helps avoid out‑of‑memory crashes on modest GPUs.
GpuOcrEngine ocrEngine = new GpuOcrEngine
{
    GpuMemoryLimit = 1024 // limit to 1024 MB
};
```

**この重要性:**  
CPU のみのエンジンはピクセルを順次走査するため、画像が大きいと非常に遅くなります。GPU メモリを制限することで、軽量に保ちつつパフォーマンス向上が得られます。

> **プロのコツ:** GPU が無いサーバーで実行する場合は `OcrEngine` にフォールバックしてください。API は同一で、クラス名を差し替えるだけです。

---

## Step 2: Load Image for OCR – Preparing the TIFF File

エンジンの準備ができたら、**OCR 用に画像をロード** します。Aspose の `ImageInfo.Load` はマルチページ TIFF を含む幅広いフォーマットに対応しています。ファイルパスを指定するだけで、残りはライブラリが処理してくれます。

```csharp
// Replace the path with the location of your TIFF file.
string imagePath = @"YOUR_DIRECTORY/english_page.tif";

// Load the image into an ImageInfo object.
// ImageInfo abstracts away format specifics, giving you a uniform API.
ImageInfo image = ImageInfo.Load(imagePath);
```

**エッジケース:**  
TIFF に複数ページが含まれる場合は、`image.Pages` を列挙して各ページを個別に処理できます。単一ページのスキャンであれば、上記の 1 行だけで十分です。

---

## Step 3: Recognize Text from TIFF – Performing the OCR

画像がメモリにロードされ、エンジンが準備できたら、いよいよ **TIFF からテキストを認識** します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、抽出された文字列、信頼度スコア、必要に応じてバウンディングボックス情報も保持します。

```csharp
// Set the language you expect in the image.
// English is the default, but you can combine languages like Language.English | Language.Spanish.
ocrEngine.Language = Language.English;

// Run the OCR process.
OcrResult ocrResult = ocrEngine.Recognize(image);
```

**言語設定が重要な理由:**  
正しい言語を指定すると、エンジンは言語固有の辞書や文字モデルを適用できるため、精度が大幅に向上します。

---

## Step 4: Output the Extracted Text

最後のステップは至ってシンプルです。結果をコンソール、ファイル、またはデータベースに書き出すだけです。ここでは画面に表示するだけにします。

```csharp
// Print the recognized text.
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**期待される出力例:**  
`english_page.tif` に印刷された段落が含まれている場合、次のような出力が得られます。

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

OCR がうまく認識できない場合は、文字化けが発生することがあります。その際は `GpuMemoryLimit` を調整したり、解像度の高い画像を使用したりすると改善します。

---

## Full Working Example

以下は、コピー＆ペーストで新規 Console App プロジェクトに貼り付けられる、完全な自己完結型プログラムです。.NET 6 以降でコンパイルできます。

```csharp
// ------------------------------------------------------------
// Complete C# program to extract text from image using Aspose OCR.
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GPU OCR engine with a memory cap.
        GpuOcrEngine ocrEngine = new GpuOcrEngine
        {
            GpuMemoryLimit = 1024 // MB
        };

        // 2️⃣ Choose the language for recognition.
        ocrEngine.Language = Language.English;

        // 3️⃣ Load the image you want to process.
        // Make sure the path points to a valid TIFF file.
        string imagePath = @"YOUR_DIRECTORY/english_page.tif";
        ImageInfo image = ImageInfo.Load(imagePath);

        // 4️⃣ Perform OCR – this returns the recognized text.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Display the result.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open when debugging.
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

ファイルを保存し、`dotnet run` を実行すれば、抽出されたコンテンツがコンソールに表示されます。シンプルですね。

---

## Common Questions & Edge Cases

**画像が TIFF ではなく PNG や JPEG の場合は？**  
`ImageInfo.Load` は事実上すべてのラスタ形式に対応しているので、拡張子を差し替えるだけでコードはそのまま動作します。追加の変更は不要です。

**OCR の結果が文字化けしている—何を確認すべき？**  
1. 画像解像度を確認（300 dpi 以上が理想）。  
2. 正しい `Language` が設定されているか確認。言語が合わないと辞書サポートが低下します。  
3. 画像が非常に大きい場合は `GpuMemoryLimit` を増やす。エンジンが自動的にスロットリングしている可能性があります。

**複数ファイルをバッチ処理したい場合は？**  
もちろん可能です。`foreach (var file in Directory.GetFiles(...))` ループでロードと認識の処理を包みます。数百ファイルを処理する場合は、各 `ImageInfo` を適切に破棄してネイティブリソースを解放してください。

**GPU が無くても動作しますか？**  
はい。対応 GPU が無い環境では `GpuOcrEngine` を通常の `OcrEngine` に置き換えるだけで動作します。API 呼び出し（`Recognize`、`Language` など）は変更不要です。

---

## Performance Tips – Getting the Most Out of GPU OCR

- **エンジンを再利用する:** 画像ごとに新しい `GpuOcrEngine` を生成するとオーバーヘッドが増えます。1 回インスタンス化したら多数のファイルで使い回しましょう。  
- **バッチ処理:** 複数画像をメモリにロードし、順次 `Recognize` を呼び出すことで GPU がウォーム状態を保ち、処理が速くなります。  
- **メモリ上限の調整:** 4 GB VRAM のマシンでは 1024 MB が安全です。ハイエンドワークステーションなら 4096 MB まで上げても問題ありません。

---

## Conclusion

これで **画像からテキストを抽出** する方法、**OCR 用に画像をロード** する正しい手順、そして **TIFF からテキストを認識** する方法を、実用的な C# コンソールアプリとして学びました。コードはそのまま実行可能で、解説は「やり方」だけでなく「なぜ」もカバーしています。これを基盤に、マルチランゲージ文書やリアルタイムカメラフィードといった、より高度な OCR シナリオにも挑戦できます。

次のステップに進みませんか？ サンプルを拡張して CSV に出力したり、`BoundingBox` データを利用して元画像に認識結果をハイライト表示したりしてみましょう。可能性は無限大ですし、GPU 加速によるパフォーマンス向上でパイプラインは常に高速です。

このガイドが役に立ったら、GitHub でスターを付けたり、チームメンバーと共有したり、コメントで独自のコツを教えてください。Happy coding!  

![extract text from image using Aspose OCR](placeholder.png){alt="Aspose OCR を使用した画像からテキストを抽出"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}