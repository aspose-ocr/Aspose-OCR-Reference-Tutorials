---
category: general
date: 2026-02-25
description: Aspose OCR を使用して画像からテキストを抽出します。OCR 用に画像を読み込む方法、ノイズ除去を適用する方法、前処理で OCR
  の精度を向上させる方法を学びましょう。
draft: false
keywords:
- extract text from image
- apply noise reduction
- improve ocr accuracy
- load image for ocr
- preprocess ocr image
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出します。このガイドでは、OCR 用に画像を読み込む方法、ノイズ除去を適用する方法、そして前処理で
  OCR の精度を向上させる方法を示します。
og_title: 画像からテキストを抽出 – 完全なC# OCRガイド
tags:
- OCR
- C#
- Aspose
title: 画像からテキストを抽出 – ノイズ除去付き完全C# OCRガイド
url: /ja/net/ocr-optimization/extract-text-from-image-complete-c-ocr-guide-with-noise-redu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – 完全な C# OCR ガイド

画像から**テキストを抽出**したいと思ったことはありませんか？しかし結果がミスだらけだった… たとえば写真が少し揺れていたり、背景がノイズだらけだったり、文字が少し傾いていたりすると、OCR の結果は大きく低下します。実際、これらの小さな不完全さが OCR 精度低下の最大の原因です。良いニュースは、**ノイズ除去**や**デスクュー**といった前処理を数ステップ加えるだけで、認識コードを一切変更せずに**OCR 精度を大幅に向上**させられることです。

このチュートリアルでは、**OCR 用に画像をロード**し、**前処理 OCR 画像**パイプラインをチェーンし、最終的に Aspose.OCR for .NET を使ってクリーンなテキストを抽出する実践的な例を順を追って解説します。最後まで読めば、ノイズが多く傾いた画像でも快適に処理できる C# コンソールアプリがすぐに実行可能な状態になります。

## 学べること

- Aspose.OCR ライブラリのインストールと参照方法。
- ディスクから **load image for OCR** するために必要な正確なコード。
- 単一のフルエントフィルタで **apply noise reduction**、適応的閾値処理、デスクューを行う方法。
- **improving OCR accuracy** のために各前処理ステップが重要な理由。
- 期待されるコンソール出力と結果をすばやく検証する方法。

> **Tip:** Aspose が初めての方へ、ライブラリは .NET 6+、.NET Framework 4.6+、さらには .NET Core でも動作します。余分なネイティブ依存は不要で、NuGet パッケージだけで完結します。

---

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or later) | 最新の言語機能とパフォーマンス向上のため。 |
| Visual Studio 2022 (or VS Code) | デバッグと IntelliSense が便利。 |
| Aspose.OCR for .NET NuGet package | `OcrEngine`、`PreprocessFilter`、および関連型を提供。 |
| A sample image (`noisy_skewed.jpg`) | 前処理の効果を示すため。 |

既にプロジェクトがある場合は、`dotnet add package Aspose.OCR` を実行してライブラリを取得してください。

---

## Step 1 – 新しいコンソールプロジェクトの作成

まずは例をすっきり保つために、フレッシュなコンソールアプリを作成します。

```bash
dotnet new console -n AsposeOcrDemo
cd AsposeOcrDemo
dotnet add package Aspose.OCR
```

このコマンドで `Program.cs` が作成され、OCR パッケージが追加されます。お好みのエディタでプロジェクトを開き、生成された `Main` メソッドをより説明的なバージョンに置き換えます。

---

## Step 2 – OCR 用に画像をロード

認識を行う前に、エンジンは画像ストリームを必要とします。`ImageStream.FromFile` メソッドは JPG、PNG、BMP などの一般的なフォーマットを自動で処理します。`using` ブロックでラップして、ファイルハンドルが自動的に解放されるようにしましょう。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 👉 Step 2: Load the raw image we want to process.
        // Replace the path with the location of your own test picture.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // The rest of the pipeline follows…
        RunOcrPipeline(rawImage);
    }

    static void RunOcrPipeline(ImageStream rawImage)
    {
        // Placeholder – we’ll fill this in next.
    }
}
```

> **Why this matters:** 画像を正しくロードすることが基盤です。ファイルパスが間違っていると `FileNotFoundException` がスローされ、前処理段階に到達できません。

---

## Step 3 – 前処理フィルタの構築（ノイズ除去など）

いよいよ魔法の時間です。**preprocess OCR image** フィルタを使うと、複数の操作をフルエントにチェーンできます。各ステップが重要な理由は次の通りです。

1. **Adaptive Threshold** – ローカルコントラストに基づき画像を白黒に変換し、OCR エンジンが背景と文字を区別しやすくします。  
2. **Deskew** – 回転を検出・補正し、テキスト行が水平になるようにします。傾いた文字は認識漏れの原因になります。  
3. **Noise Reduction** – 斑点やほこり、圧縮アーティファクトなどの不要なピクセルを除去します。

```csharp
static void RunOcrPipeline(ImageStream rawImage)
{
    // 👉 Step 3: Build a preprocessing filter that applies three operations.
    PreprocessFilter preprocessFilter = new PreprocessFilter()
        .ApplyAdaptiveThreshold()   // Enhance contrast for better binarization
        .ApplyDeskew()              // Correct any rotation in the image
        .ApplyNoiseReduction();     // Remove speckles and background noise

    // Execute the filter and get a cleaned image stream.
    ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

    // Pass the cleaned image to the OCR engine.
    PerformRecognition(cleanedImage);
}
```

> **Pro tip:** 呼び出し順序は変更可能ですが、上記の順序（threshold → deskew → noise reduction）が最も効果的です。まず前景と背景を分離し、次にテキストを整列、最後に残存アーティファクトを除去します。

---

## Step 4 – OCR を実行し、認識結果を表示

前処理済みの画像が用意できたら、`OcrEngine` が本格的に処理を行います。エンジンはデフォルトで英語モデルを自動選択しますが、別の言語を指定しない限りは英語が使用されます。

```csharp
static void PerformRecognition(ImageStream image)
{
    // 👉 Step 4: Create the OCR engine and assign the cleaned image.
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = image
    };

    // Run the recognition process.
    OcrResult result = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(result.Text);
}
```

プログラムを実行すると（`dotnet run`）次のような出力が得られるはずです。

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

元の画像がノイズが多い場合でも、未処理のまま OCR を走らせたときに比べて意味不明な文字が大幅に減少していることが確認できます。

---

## Step 5 – 完全な実行可能サンプル

すべての要素を組み合わせた **complete code** を以下に示します。`Program.cs` にそのまま貼り付けてください。欠けている部分や隠れた依存関係はありません。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Load the image you want to OCR.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // Build and execute the preprocessing pipeline.
        PreprocessFilter preprocessFilter = new PreprocessFilter()
            .ApplyAdaptiveThreshold()
            .ApplyDeskew()
            .ApplyNoiseReduction();

        ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

        // Run OCR on the cleaned image.
        OcrEngine ocrEngine = new OcrEngine
        {
            Image = cleanedImage
        };

        OcrResult result = ocrEngine.Recognize();

        // Show the extracted text.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(result.Text);
    }
}
```

### 期待される出力

元画像に文 *“The quick brown fox jumps over the lazy dog.”* が含まれていれば、余計な記号や欠落文字なしでそのまま一行が出力されます。これが **improved OCR accuracy** を実現した証です。

---

## よくある質問とエッジケース

### 画像が別の形式（例：PNG）の場合は？

`ImageStream.FromFile` がファイルタイプを自動検出するので、コードを変更せずに `.png` や `.bmp` を指定できます。

### マルチページ PDF の処理方法は？

Aspose.OCR は各ページを個別に処理できます。`PdfDocument.Pages` をループし、各ページを画像ストリームに変換して同じ前処理パイプラインに渡します。

### 言語モデルを変更できますか？

はい。`ocrEngine.Language = OcrLanguage.Spanish;`（またはサポートされている任意の言語）を `Recognize()` 呼び出し前に設定してください。

### 画像がすでにきれいな場合は？

不要なステップはスキップできます。完璧にスキャンされた文書であれば `ApplyAdaptiveThreshold()` だけ呼び出すか、フィルタ自体を省略しても OCR は動作しますが、微細な改善は得られない可能性があります。

---

## 本番環境向け OCR のプロティップス

- **Batch Processing:** 何十枚もの画像を処理する際はパイプラインを `Parallel.ForEach` でラップし、マルチコア CPU を活用します。  
- **Memory Management:** 使用後は `ImageStream` オブジェクトを必ず `Dispose()`（例: `rawImage.Dispose();`）して、ネイティブリソースを速やかに解放します。  
- **Logging:** 監査用に `ocrResult.Text` と元ファイル名を同時に記録します。  
- **Error Handling:** 全体を `try/catch` で囲み、`OcrException` の詳細をログに残します。例外メッセージには未対応画像形式に関する手がかりが含まれることが多いです。

---

## 結論

今回、Aspose.OCR を使用して **画像からテキストを抽出** し、**OCR 用に画像をロード** する方法を示しました。また、**ノイズ除去**（閾値処理とデスクューを含む）を適用することが **OCR 精度向上** の秘訣であることを実証しました。全体のソリューションは 1 ファイルの C# コードに収まり、明日から任意の .NET プロジェクトに組み込めます。

次のステップに進みませんか？別言語に切り替えてみたり、カスタムフィルタで実験したり、スキャンした請求書のバッチを同じパイプラインに流し込んでみましょう。学んだ概念（前処理、クリーンな画像ストリーム、堅牢なエラーハンドリング）はすべての OCR シナリオに応用できます。

質問や奇妙なエッジケースを見つけたらコメントを残してください。ワークフローの微調整を喜んでお手伝いします。コーディングを楽しんで、OCR が常にクリアになることを願っています！

![Diagram showing the OCR preprocessing pipeline – extract text from image after noise reduction, adaptive threshold, and deskew](extract-text-from-image-ocr-pipeline.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}