---
category: general
date: 2026-02-11
description: Aspose OCR を使用して C# でマルチページ TIFF の OCR を実行する方法を学びましょう。TIFF をテキストに変換し、TIFF
  からテキストを抽出し、画像からテキストを素早く認識します。
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: ja
og_description: C#でAspose OCRを使用してマルチページTIFFにOCRを実行する方法。TIFFをテキストに変換し、TIFFからテキストを抽出し、画像からテキストを認識するステップバイステップガイド。
og_title: マルチページTIFF画像でOCRを実行する方法 – 完全C#チュートリアル
tags:
- OCR
- C#
- Aspose
- TIFF
title: Aspose OCRでマルチページTIFF画像にOCRを実行する方法 – C#ガイド
url: /ja/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

The heading "# How to Run OCR on Multi‑Page TIFF Images with Aspose OCR" should be translated to Japanese, but maybe keep the title in English? The rule says translate all text content naturally to Japanese. So translate heading.

Thus "# Aspose OCR を使用したマルチページ TIFF 画像の OCR 実行方法"

Similarly subheadings.

Proceed.

Let's produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用したマルチページ TIFF 画像の OCR 実行方法

スキャンした TIFF に複数ページが含まれている場合、**OCR を実行する方法** を知りたくありませんか？同じ問題に直面している開発者は多く、古い文書から検索可能なテキストを抽出したいときに壁にぶつかります。朗報です！Aspose OCR を使えば、C# の数行のコードで画像ファイルからテキストを認識でき、インデックス作成やさらなる処理に使える平文の連結テキストが手に入ります。

このチュートリアルでは、Aspose OCR パッケージのインストールから、マルチページ TIFF の読み込み、TIFF からテキストへの変換、抽出したコンテンツの表示まで、ワークフロー全体を順を追って解説します。最後まで読めば、**TIFF からテキストを抽出** し、**画像からテキストを認識** し、バッチジョブで数十ファイルを自動処理する方法が身につきます。魔法はありません、実践的な手順だけです。

## 学べること

- 英語認識用に Aspose OCR エンジンを設定する方法。  
- `OcrEngine` クラスを使って **TIFF をテキストに変換** する正確なコード。  
- マルチページ画像を扱い、各ページを正しく分離するコツ。  
- よくある落とし穴（ネイティブ依存関係の欠如など）と回避策。  

**前提条件** – .NET 6 以上、Visual Studio（または任意の C# エディタ）、自動リソースダウンロード機能のためのインターネット接続が必要です。これだけで完了です。追加のネイティブライブラリを用意する必要はありません。

---

## Step 1 – Install Aspose OCR NuGet Package

画像ファイルに対して **OCR を実行** する前に、ライブラリをプロジェクトに追加する必要があります。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio を使用している場合は、プロジェクトを右クリック → *Manage NuGet Packages* → “Aspose.OCR” を検索して *Install* をクリックすることもできます。

このパッケージには必要なものがすべて含まれており、`AutomaticResourceDownload = true` を設定すればエンジンが言語パックを自動で取得します。

---

## Step 2 – Initialize the OCR Engine (How to Run OCR)

パッケージが導入できたら、`OcrEngine` インスタンスを作成し設定します。これが **OCR の実行方法** の中心です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**重要ポイント:** `Language` を設定するとエンジンが期待する文字セットを認識し、`AutomaticResourceDownload` によりサーバーに言語ファイルを手動で配置する手間が省けます。`OutputFormat` を `Text` にすれば、**TIFF をテキストに変換** パイプラインに最適なシンプルな文字列が得られます。

---

## Step 3 – Load the Multi‑Page TIFF (Recognize Text from Image)

TIFF は複数のフレーム（ページ）を保持できます。`System.Drawing.Image` クラスがそれを抽象化します。

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **ファイルが同じフォルダにない場合は？** 絶対パスを指定するか、`Path.Combine` と `AppContext.BaseDirectory` を組み合わせて使用してください。  
> **メモリ使用量は？** `using` 文で画像を処理後に破棄するため、リークを防げます。大量の大きな TIFF をバッチ処理する際に重要です。

`Recognize` 呼び出しは TIFF 内のすべてのページを自動的に走査し、結果を改行で連結します。そのため、`ocrResult.Text` を出力すると各ページが区切られて表示されます。

---

## Step 4 – Full Working Example (All Steps in One File)

以下はコンソールアプリケーションとしてそのまま実行できる完全版です。新しい .NET コンソールプロジェクトに貼り付けて **F5** を押すだけです。

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**期待される出力**（抜粋）:

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

各ページが改行で区切られているのは `OcrOutputFormat.Text` がフレーム間に改行を挿入するためです。別の区切り文字が必要な場合は、`result.Text` に対して `String.Replace` で後処理できます。

---

## Step 5 – Handling Common Edge Cases

### 5.1 Large TIFF Files  
ギガバイト級の TIFF を扱う場合、ファイル全体をメモリに読み込むと問題が生じます。回避策として、フレームごとに個別に処理します。

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Non‑English Documents  
スペイン語やフランス語など、**画像からテキストを認識** したい場合は `Language` プロパティを変更するだけです。

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose が自動的に該当言語のリソースをダウンロードします。

### 5. Saving the Output  
**TIFF をテキストに変換** した結果を `.txt` ファイルに保存したいケースが多いでしょう。

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

`String.Split(Environment.NewLine)` を使ってページ単位に分割し、各スライスを別ファイルに書き出すことも可能です。

---

## Pro Tips & Gotchas

- **AutomaticResourceDownload** はアプリを初めて実行したときにのみオンラインで動作し、以降はオフラインで利用できます。  
- 文字化けが発生したら、まず `Language` 設定を確認してください。言語パックが合っていないと認識精度が低下します。  
- TIFF にラスタライズされた PDF を処理する場合は、`ocrEngine.Dpi`（既定は 300）を上げると精度が向上します。  
- `Image.FromFile` は必ず `using` ブロックで囲み、処理後にファイルがロックされて削除や移動ができなくなるのを防ぎましょう。

---

## Frequently Asked Questions

**Q: 単一ページの TIFF でも動作しますか？**  
A: はい。エンジンは単一フレーム TIFF も同様に扱い、1 行のテキストが返ります。

**Q: PNG や JPEG でも同じ手順で処理できますか？**  
A: 可能です。拡張子を変更すれば OK。`Recognize` メソッドは任意の `System.Drawing.Image` フォーマットを受け付けます。

**Q: OCR 結果をプレーンテキストではなく PDF にしたい場合は？**  
A: `OutputFormat = OcrOutputFormat.Pdf` と設定すれば、`ocrResult` に PDF のバイト配列が格納され、ディスクに書き出せます。

---

## Conclusion

これで Aspose OCR を使ったマルチページ TIFF ファイルの **OCR 実行方法** が完璧にマスターできました。エンジンの設定、画像の読み込み、`Recognize` の呼び出しだけで、**TIFF からテキストを抽出**、**TIFF をテキストに変換**、そして **画像からテキストを認識** できるようになります。言語や出力形式、フレーム単位の処理を調整すれば、バッチ処理にも柔軟に対応できます。

次のステップに進みませんか？フォルダー監視サービスと組み合わせて、ドロップフォルダーに入った画像に自動で **OCR を実行** したり、検索インデックスに出力を組み込んで即時全文検索を実現したりできます。可能性は無限大です。今回示したコードは堅実な土台となります。

実装中に問題があればコメントを残すか、GitHub で ping してください。楽しいコーディングを！頑張って、頑固な TIFF を検索可能なテキストに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}