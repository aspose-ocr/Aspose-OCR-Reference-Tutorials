---
category: general
date: 2026-02-24
description: C#で Aspose.OCR を使用して画像を高速にバッチ OCR し、ディレクトリからファイルを読み込み、画像からテキストを認識し、画像をテキストに変換する手順を数ステップで学びましょう。
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: ja
og_description: Aspose.OCR を使用して C# で画像のバッチ OCR を実行します。このチュートリアルでは、ディレクトリからファイルを読み取り、画像からテキストを認識し、画像を効率的にテキストに変換する方法を示します。
og_title: C#で画像をバッチOCR – 完全ステップバイステップガイド
tags:
- C#
- OCR
- Aspose
title: C#で画像を一括OCR処理 – テキスト抽出の完全ガイド
url: /ja/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でバッチ OCR 画像 – テキスト抽出の完全ガイド

Ever needed to **batch OCR images** but weren’t sure where to start? You’re not alone—many developers hit the same wall when they first try to **extract text from images** en masse. The good news is that with a few lines of C# and Aspose.OCR you can turn a folder full of pictures into tidy `.txt` files in no time.

このチュートリアルでは、ディレクトリからファイルを読み取り、各画像を OCR エンジンに渡し、最後に **convert image to text** できるファイルを作成し、インデックスや検索、または下流パイプラインに供給できます。最後までに、任意の .NET ソリューションに組み込める自己完結型コンソールアプリが手に入ります。

## 必要なもの

- **.NET 6+**（サンプルは .NET 6 でコンパイルされますが、最近のバージョンならどれでも動作します）
- **Aspose.OCR** NuGet パッケージ（`Install-Package Aspose.OCR`）
- 処理したい画像ファイル（`.png`, `.jpg` など）が入ったフォルダー
- Visual Studio、Rider、またはお好みのエディタ

追加の設定ファイルや外部サービスは不要です—ローカルで実行される純粋な C# コードだけです。

## バッチ OCR 画像 – プロジェクトの設定

First, create a new console project:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

That command scaffolds a minimal project and pulls in the OCR library. After the restore finishes you’re ready to add the core logic.

### ディレクトリからファイルを読み取る

We need to tell our app where the source images live and where the resulting text files should go. Using `System.IO` makes this a breeze.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Why this step matters:** If the output directory doesn’t exist the program will throw an exception when it tries to write a `.txt` file. `CreateDirectory` is idempotent—it does nothing if the folder is already there, so it’s safe to call every run.

### 画像からテキストを認識し、画像をテキストに変換

Now we spin up the OCR engine and loop over every file we found. The loop uses `Directory.GetFiles` with a wildcard (`*.*`) so it grabs *all* files, but you can tighten the filter to `*.png` or `*.jpg` if you prefer.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**What’s happening here?**  
- `ocrEngine.RecognizeImage(imagePath)` はビットマップを読み取り、OCR アルゴリズムを実行し、`OcrResult` オブジェクトを返します。  
- `ocrResult.Text` にはエンジンが読み取れたすべてのテキストがプレーンテキストとして格納されています。  
- `File.WriteAllText` は抽出したテキストで新しいファイル（または既存ファイルを上書き）を作成します。

That’s the entire **batch OCR images** pipeline in under 30 lines of code.

## プロのコツとエッジケース

| 状況 | 推奨事項 |
|-----------|----------------|
| 画像が大きい（> 5 MB） | 認識速度を上げつつ精度を落とさないよう、幅約1500 px に事前にスケールダウンしてください。 |
| PDF をサポートする必要がある | 各 PDF ページをまず画像に変換（例：`Aspose.PDF` を使用）し、同じループに渡してください。 |
| 一部のファイルは画像ではない（例：`.txt`） | 簡単なフィルタを追加します：`if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| 多言語サポートが必要 | ループの前に `ocrEngine.Language = Language.English | Language.Spanish;` を設定してください。 |
| 進捗報告が必要 | `foreach` 内で `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` と書き出してください。 |

> **Pro tip:** Wrap the OCR call in a `try/catch`. Occasionally a corrupted image will cause `RecognizeImage` to throw; handling it prevents the whole batch from stopping.

## 期待される出力

After the program finishes, the `outputFolder` will contain a `.txt` file for each original image:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Each file holds the raw text the engine extracted, for example:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

You can now feed these files into a search index, run sentiment analysis, or simply archive them for compliance.

## よくある質問

**Q: これは Linux でも動作しますか？**  
A: もちろんです。Aspose.OCR はクロスプラットフォームで、ここで使用している `System.IO` API は OS に依存しません。フォルダー パス（`/home/user/images`）を調整するだけです。

**Q: **read files from directory** を再帰的に行う必要がある場合はどうすればいいですか？**  
A: `SearchOption.TopDirectoryOnly` を `SearchOption.AllDirectories` に変更してください。深いフォルダーでは権限の問題に注意しましょう。

**Q: OCR の精度はどの程度ですか？**  
A: 精度は画像の品質、フォント、言語に依存します。最良の結果を得るには、高解像度のスキャンとクリーンな背景を使用してください。また、`ocrEngine.Config` を調整してデスキューやノイズ除去を有効にすることもできます。

## まとめ

You’ve just learned how to **batch OCR images** in C# using Aspose.OCR, from reading files from a directory to **recognize text from image** and finally **convert image to text** files you can store or process further. The complete, runnable example above should work out‑of‑the‑box, and the tips section gives you a roadmap for scaling or customizing the solution.

Next steps? Try adding a simple UI with WinForms or WPF, integrate the output with Azure Cognitive Search, or experiment with other languages supported by Aspose.OCR. The sky’s the limit once you’ve mastered the core loop.

Happy coding, and may your OCR batches be error‑free!  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}