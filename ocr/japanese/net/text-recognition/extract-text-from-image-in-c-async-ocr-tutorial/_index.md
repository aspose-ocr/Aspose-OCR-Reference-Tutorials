---
category: general
date: 2026-04-03
description: C#でAspose OCRを使用して画像からテキストを抽出します。スキャン画像の変換方法、C#で画像ファイルを読み込む方法、そしてTIFから非同期でテキストを認識する方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert scanned image
- how to ocr image
- load image file c#
- recognize text from tif
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出する。このガイドでは、スキャンした画像を変換し、C#で画像ファイルを読み込み、非同期呼び出しを使用してTIFからテキストを認識する方法を示します。
og_title: C#で画像からテキストを抽出する – 非同期OCRチュートリアル
tags:
- OCR
- C#
- Aspose
- Async
title: C#で画像からテキストを抽出する – 非同期OCRチュートリアル
url: /ja/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – 非同期 OCR チュートリアル

Need to **extract text from image** quickly? With Aspose OCR you can do it in C# using async calls, and the whole process finishes before you’ve even finished your coffee.  
If you’re also wondering how to **convert scanned image** files or load an image file in C# without breaking a sweat, you’re in the right place.

画像からテキストを**素早く抽出**したいですか？Aspose OCR を使えば、C# で非同期呼び出しを利用して実行でき、コーヒーがまだ飲み終わっていないうちに処理が完了します。  
また、**スキャンした画像**ファイルを変換したり、C# で画像ファイルをロードする方法が知りたい場合も、ここが正解です。

In this guide we’ll walk through every step—from pulling a TIF off disk to getting clean, searchable text back. By the end you’ll be able to **recognize text from TIF** files, understand the nuances of loading different image formats, and have a solid async pattern you can reuse in any .NET project.

このガイドでは、ディスクから TIF を取得し、クリーンで検索可能なテキストを取得するまでのすべての手順を解説します。最後まで読むと、**TIF からテキストを認識**できるようになり、さまざまな画像フォーマットのロードのコツを理解し、任意の .NET プロジェクトで再利用できる堅牢な非同期パターンを手に入れられます。

## 学習内容

* Aspose OCR エンジンを非同期で使用できるように設定する方法。  
* **load image file C#** スタイルで必要な正確なコード、欠損ファイルに対するエラーハンドリングを含む。  
* **convert scanned image** PDF や TIFF を Aspose が読み取れるビットマップに変換する方法。  
* 非同期 OCR (`RecognizeAsync`) が同期版より高速でスケーラブルである理由。  
* 期待されるコンソール出力と、抽出されたテキストが元データと一致するかを検証する方法。

> **プロのコツ:** 数十ページを処理する場合、呼び出し間で OCR エンジンを維持してください。毎回新しいインスタンスを作成すると不要なオーバーヘッドが発生します。

---

## 画像からテキストを非同期に抽出

The heart of the solution lives in an async `Main` method. Using `await` keeps the UI thread free (or, in a console app, frees up the thread pool) while the OCR engine does its heavy lifting.

このソリューションの核心は非同期 `Main` メソッドにあります。`await` を使用することで、OCR エンジンが重い処理を行っている間、UI スレッド（またはコンソール アプリの場合はスレッド プール）を解放できます。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // 1️⃣ Create an instance of the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        Image inputImage = Image.FromFile(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Run asynchronous OCR recognition (returns a Task<string>)
        string recognizedText = await ocrEngine.RecognizeAsync(inputImage);

        // 4️⃣ Display the OCR result
        Console.WriteLine("Async OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**なぜ非同期か？** OCR の処理はネットワーク I/O（エンジンがクラウドサービスを使用する場合）や集中的な CPU 作業を伴うことがあります。`RecognizeAsync` は呼び出し元スレッドを解放し、他の作業（例えば、さらにファイルを処理するなど）を継続できるようにします。

### 期待される出力

```
Async OCR result:
The quick brown fox jumps over the lazy dog.
```

If the image contains multiple lines, each line will appear separated by newline characters. You can pipe the result into a file with `File.WriteAllText("output.txt", recognizedText);` if you need persistent storage.

画像に複数行が含まれる場合、各行は改行文字で区切られて表示されます。永続的に保存したい場合は、`File.WriteAllText("output.txt", recognizedText);` を使って結果をファイルに書き込むことができます。

---

## Convert Scanned Image to a Usable Format

Sometimes you receive a scanned PDF or a multi‑page TIFF. Aspose OCR works best with a `System.Drawing.Image`, so you may need to convert first.

時にはスキャンした PDF や複数ページの TIFF を受け取ることがあります。Aspose OCR は `System.Drawing.Image` と組み合わせて使用するのが最適なため、最初に変換が必要になる場合があります。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.Drawing.Imaging;

// Load a multi‑page TIFF and pick the first frame
Image tiff = Image.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
tiff.SelectActiveFrame(FrameDimension.Page, 0); // Grab page 0

// Optionally, change DPI for better accuracy
var bitmap = new Bitmap(tiff);
bitmap.SetResolution(300, 300); // 300 DPI is a sweet spot for OCR
```

> **なぜ DPI を変更するのか？** 高解像度にすると OCR エンジンがより多くの詳細を取得でき、ぼやけたスキャンでの誤認識が減ります。ただし 600 DPI を超えないでください。ほとんどのエンジンは精度向上が得られず、メモリ使用量だけが増加します。

---

## Load Image File C# – Handling Different Formats

You might be tempted to hard‑code a `.tif` path, but a robust utility should accept **any** image type (`.png`, `.jpg`, `.bmp`). Here’s a tiny helper that abstracts the loading logic:

`.tif` パスをハードコードしたくなるかもしれませんが、堅牢なユーティリティは **任意の** 画像タイプ（`.png`、`.jpg`、`.bmp`）を受け入れるべきです。以下はロードロジックを抽象化した小さなヘルパーです：

```csharp
static Image LoadImage(string path)
{
    if (!File.Exists(path))
        throw new FileNotFoundException($"Image not found: {path}");

    // Let .NET decide the correct decoder based on file header
    using (var stream = File.OpenRead(path))
    {
        return Image.FromStream(stream);
    }
}
```

Use it like:

以下のように使用します：

```csharp
Image img = LoadImage(@"YOUR_DIRECTORY/input.tif");
string text = await ocrEngine.RecognizeAsync(img);
```

Now you’ve covered the **load image file C#** scenario without worrying about the exact extension.

これで、正確な拡張子を気にせずに **load image file C#** シナリオをカバーできました。

---

## Recognize Text from TIF – What You Need to Know

TIF files often store multiple pages or use compression that confuses some libraries. Two things help you get reliable results:

TIF ファイルは複数ページを保持したり、いくつかのライブラリを混乱させる圧縮方式を使用したりすることがよくあります。信頼できる結果を得るために役立つ二つのポイントがあります：

1. **正しいフレームを選択** – 以前に `SelectActiveFrame` で示したように。  
2. **色を正規化** – 24 ビット RGB ビットマップに変換することで、奇妙なパレットを排除できます。

```csharp
static Image PrepareTif(string tifPath, int pageIndex = 0)
{
    Image tif = Image.FromFile(tifPath);
    tif.SelectActiveFrame(FrameDimension.Page, pageIndex);
    // Convert to 24‑bit RGB to avoid palette issues
    Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
    using (Graphics g = Graphics.FromImage(rgb))
    {
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
    }
    return rgb;
}
```

Feed the returned `Image` straight into `RecognizeAsync` and you’ll reliably **recognize text from TIF** even when the source uses CCITT Group 4 compression.

返された `Image` をそのまま `RecognizeAsync` に渡せば、ソースが CCITT Group 4 圧縮を使用している場合でも、確実に **TIF からテキストを認識** できます。

---

## Full End‑to‑End Example

Putting everything together gives you a single file you can drop into a console project and run.

すべてを組み合わせると、コンソール プロジェクトにドロップして実行できる単一ファイルが得られます。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        try
        {
            // Step 1 – Initialize OCR engine (reuse if processing many files)
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2 – Load and prepare the image (handles TIF, PNG, JPG, etc.)
            Image img = PrepareImage(@"YOUR_DIRECTORY/input.tif");

            // Step 3 – Run async recognition
            string result = await ocrEngine.RecognizeAsync(img);

            // Step 4 – Output the result
            Console.WriteLine("Async OCR result:");
            Console.WriteLine(result);

            // Optional: Save to a text file
            File.WriteAllText("ocr-output.txt", result);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // Helper that decides how to load based on extension
    static Image PrepareImage(string path)
    {
        string ext = Path.GetExtension(path).ToLowerInvariant();
        return ext switch
        {
            ".tif" or ".tiff" => PrepareTif(path),
            _ => LoadImage(path)
        };
    }

    static Image LoadImage(string path)
    {
        if (!File.Exists(path))
            throw new FileNotFoundException($"Image not found: {path}");

        using var stream = File.OpenRead(path);
        return Image.FromStream(stream);
    }

    static Image PrepareTif(string tifPath, int page = 0)
    {
        Image tif = Image.FromFile(tifPath);
        tif.SelectActiveFrame(FrameDimension.Page, page);
        Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
        using var g = Graphics.FromImage(rgb);
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
        return rgb;
    }
}
```

**期待される結果:** コンソールに抽出されたテキストが表示され、実行ファイルの隣に `ocr-output.txt` という名前のファイルが作成され、同じ文字列が格納されます。

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *PDF を直接 OCR できますか？* | Aspose OCR は画像上で動作するため、まず各 PDF ページを画像に変換する必要があります（例: Aspose.PDF や `PdfRenderer` を使用）。 |
| *画像が非常に大きい場合は？* | OCR 前に幅・高さを最大 2500 px に縮小してください。Aspose は内部で自動的にリサイズしますが、メモリを節約できます。 |
| *非同期メソッドはスレッドセーフですか？* | はい。ただし、`RecognizeAsync` を同時に呼び出さない場合に限り、同じ `OcrEngine` インスタンスを再利用してください。並列処理を行う場合は、タスクごとに別々のエンジンを作成します。 |
| *ライセンスは必要ですか？* | Aspose OCR は透かし付きの無料評価版を提供しています。製品版ではライセンスを購入し、`License license = new License(); license.SetLicense("Aspose.OCR.lic");` のように設定してください。 |

---

## 結論

これで、Aspose OCR の非同期 API を使用して C# で **画像からテキストを抽出** する方法がわかりました。画像のロード、スキャン画像のオプション変換、TIF ファイルの特性に対応することで、ソリューションは堅牢かつ本番環境で使用できる状態になっています。  

From here you might:

* **Convert scanned image** PDF を OCR 前に PNG に変換して精度を向上させます。  
* Explore **how to ocr image** ストリームをウェブ API から直接処理する方法を検討し、テンポラリファイルの必要性を排除します。  
* Batch‑process dozens of files by reusing the `OcrEngine` instance inside a `Parallel.ForEach` loop. -> `Parallel.ForEach` ループ内で `OcrEngine` インスタンスを再利用して、数十ファイルをバッチ処理します。  

これらのバリエーションを試してみてください。非同期 OCR が文書中心のアプリケーションにとっていかに画期的かすぐに実感できるはずです。コーディングを楽しんで、問題があれば遠慮なくコメントを残してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}