---
category: general
date: 2026-06-06
description: C# OCR を使用してテキスト画像を認識する – スキャンからテキストを抽出し、数分でスキャンをテキストに変換するステップバイステップの
  C# OCR 例。
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: ja
og_description: C# OCRで画像内のテキストを認識。スキャンからテキストを抽出し、スキャンをテキストに変換し、実際の画像を処理する実用的なC# OCR例を学びましょう。
og_title: C#でテキスト画像を認識する – 完全OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: C#でテキスト画像を認識する – 完全OCRガイド
url: /ja/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でテキスト画像を認識する – 完全 OCR チュートリアル

スキャンした写真から **テキスト画像を認識** したいと思ったことはありませんか？ あなただけではありません。古いレシートをデジタル化したり、名刺からデータを抽出したり、低解像度のスキャンを編集可能なテキストに変換したりする際に、画像からテキストを抽出できることは、すべての開発者がツールボックスに持っておくべき便利な技です。

このガイドでは、画像を読み込み、光学文字認識を実行し、結果をコンソールに出力する **c# ocr example** を順を追って解説します。最後まで読めば、**テキストスキャンを抽出** でき、**スキャンをテキストに変換** でき、ノイズが多い画像向けに調整する方法も習得できます。サードパーティの高価なサービスは不要です—組み込みの Windows.Media.Ocr API（または互換性のある OcrEngine）と数行のコードだけで完結します。

## 学べること

* C# プロジェクトで OCR を設定する方法
* **テキスト画像を認識** するために必要な正確なコード
* 低解像度スキャンや複数ページ文書の取り扱いのコツ
* サンプルを自分のアプリ用に再利用可能なライブラリへ拡張する方法

### 前提条件

* .NET 6.0 以上（API は .NET 5+ でも動作します）
* Visual Studio 2022（Community エディションで可）またはお好みの IDE
* `lowres_scan.jpg` のようなサンプル画像を参照できるフォルダーに配置
* async/await の基本的な知識—Windows API の OCR 呼び出しは非同期です

> **Pro tip:** 非 Windows 環境の場合は `Windows.Media.Ocr` 名前空間を TesseractSharp などのクロスプラットフォームライブラリに置き換えてください。ロジック自体は同じです。

---

## 手順 1: OCR エンジンで **テキスト画像を認識** する準備

まず OCR エンジンのインスタンスが必要です。`OcrEngine` クラスは **画像からテキストへの C#** 操作のエントリーポイントです。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**ポイント:** エンジンはパターン認識という重い処理を抽象化します。明示的にインスタンス化することで言語設定を制御でき、後で他言語の **テキストスキャンを抽出** したい場合に必須です。

## 手順 2: 画像ファイルを読み込む – **スキャンをテキストに変換** の核心

次にディスク上の画像を読み込み、OCR エンジンが期待する `SoftwareBitmap` に変換します。

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**理由:** 生のファイルストリームを直接 OCR に渡すと、特に低解像度スキャンでは結果が悪くなります。`SoftwareBitmap` に変換することで DPI や色深度を調整したり、認識前にフィルタを適用したりできます。

## 手順 3: **テキスト画像を認識** する操作を実行

いよいよエンジンの `RecognizeAsync` メソッドを呼び出します。ここが魔法の瞬間です。

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**期待される出力:** `lowres_scan.jpg` に「Hello World」というフレーズが含まれていれば、コンソールに次のように表示されます。

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

これが **c# ocr example** の全体像です—4 つの論理ステップだけで、ファイル読み込みから最終出力まで網羅しています。

## 手順 4: エッジケースの処理 – スキャンが完璧でないとき

実際の画像は必ずしも鮮明とは限りません。プログラム全体を書き直さずにできる調整をいくつか紹介します。

| 問題 | 簡単な対策 |
|-------|-----------|
| **非常に低 DPI（≤ 72）** | 認識前に `BitmapTransform` でビットマップを拡大 |
| **文字が傾いている** | `SoftwareBitmap.Rotate` で回転変換を適用し、ページを水平に |
| **複数言語** | `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` を作成し、`engine.Language` に設定 |
| **大容量ファイル** | 画像をタイルに分割して `engine.RecognizeAsync(tileBitmap)` で処理し、結果を結合 |

これらの調整により、ノイズの多いレシートや斜めに撮影した写真でも **テキストスキャンを抽出** する信頼性が保たれます。

## 手順 5: 再利用可能なヘルパーへ変換（任意）

アプリケーションの複数箇所で **スキャンをテキストに変換** したい場合は、ロジックを小さなユーティリティクラスにまとめましょう。

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

これで次のように呼び出すだけです。

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**メリット:** ヘルパーが OCR の配管部分を隠蔽するので、ビジネスロジックに集中できます。プロジェクト間で再利用できる **c# ocr example** に最適です。

---

![recognize text image example](https://example.com/ocr-demo.png "OCR コンソール出力のスクリーンショット – recognize text image の結果を表示")

*Alt text:* **recognize text image** の結果を示す C# OCR コンソールアプリケーションの出力例。

---

## よくある質問

**Q: Linux 上の .NET Core でも動作しますか？**  
A: `Windows.Media.Ocr` 名前空間は Windows 専用です。Linux や macOS では TesseractSharp や IronOcr に置き換えれば、同様の `Engine.Recognize` メソッドが提供されるため、周辺コードはほぼそのまま使えます。

**Q: 手書きメモの認識精度はどれくらいですか？**  
A: 手書き認識はまだ実験的です。高精度が必要な場合は、印刷フォントを使用するか、Azure Cognitive Services などのクラウドサービスを検討してください。

**Q: PDF を直接処理できますか？**  
A: 標準では対応していません。`PdfSharp` や `Ghostscript` で各ページを画像に変換してから OCR エンジンに渡す必要があります。

---

## 結論

これで **c# ocr example** が完成し、**テキスト画像を認識** ファイルの処理、**テキストスキャンを抽出**、そして **スキャンをテキストに変換** が数行のコードで実現できました。エンジン作成、画像読み込み、非同期認識、結果処理という流れを理解すれば、画像を検索可能な文字列に変換する必要がある任意の C# プロジェクトにパターンを適用できます。

次のステップに進みませんか？ WinForms や WPF でシンプルな UI を作成したり、言語を変えてみたり、出力をデータベースに保存して検索アーカイブにしたり。**画像からテキストへの C#** 技術をマスターすれば、可能性は無限です。

Happy coding, and may your scans always be crisp!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能や代替実装アプローチを自分のプロジェクトでマスターするのに役立ちます。

- [Aspose.OCR を使った言語選択付き画像テキスト抽出 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [URL から画像を取得して OCR を実行する – Image to Text](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [OCR で矩形領域を指定して画像テキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}