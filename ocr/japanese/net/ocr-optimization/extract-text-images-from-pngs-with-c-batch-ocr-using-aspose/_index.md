---
category: general
date: 2026-02-09
description: C#でバッチOCRの最大並列度を設定し、テキスト画像を高速に抽出する – スキャンしたページの変換、複数画像のOCR処理、PNGテキストの効率的な読み取り方法を学ぼう。
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: ja
og_description: C#で最大並列度を設定してテキスト画像を抽出します。このチュートリアルでは、スキャンしたページを変換し、複数の画像OCRを実行し、Aspose
  OCRでPNGテキストを読み取る方法を示します。
og_title: C#でPNGからテキスト画像を抽出 – 完全バッチOCRガイド
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: C#でPNGからテキスト画像を抽出 – Aspose OCRを使用したバッチOCR
url: /ja/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキスト画像を抽出する C# – Aspose OCR を使用したバッチ OCR

スキャンした PNG のフォルダから **extract text images** をしたいと思ったことはありませんか？しかし「どうやって高速化するか？」という疑問で行き詰まっていませんか？あなたは一人ではありません。実際のプロジェクトでは、開発者は **set max parallelism** をして、数十ページを数秒で処理できるようにしなければなりません。  

このガイドでは、**converts scanned pages**し、**multiple image OCR** を実行し、最終的に **reads png text** する完全な実行可能サンプルを順に解説します。曖昧な「see the docs」リンクはありません—コピー＆ペーストできるコード、各行が重要な理由の説明、そして一般的な落とし穴を回避するためのヒントだけを提供します。

> **Pro tip:** すでに他の場所で Aspose OCR を使用している場合、同じ `OcrEngine` クラスが現れることに気付くでしょう、しかし本稿では真の並列処理のために設定を調整します。

## 必要なもの

- **.NET 6+** (または .NET Framework 4.6+)。API は同じですが、最新のランタイムはスレッド処理が改善されています。  
- **Aspose.OCR for .NET** – NuGet でインストール: `Install-Package Aspose.OCR`。  
- PNG スキャンが数枚入ったフォルダ（`page1.png`、`page2.png`、…）。  
- お好みの IDE またはエディタ（Visual Studio、Rider、VS Code など）。

以上です。余分なサービスやクラウドキーは不要で、純粋にローカルで処理します。

## extract text images – バッチ OCR の Max Parallelism 設定

複数のファイルに対して OCR を実行すると、エンジンはデフォルトで単一スレッドを使用します。安全ですが非常に遅いです。`MaxDegreeOfParallelism` を設定することで、エンジンが同時に起動できるスレッド数を指定できます。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Why 4?**  
4 は多くの最新ラップトップでの最適ポイントです—CPU を忙しくさせるのに十分なコア数ですが、他のプロセスを圧迫しすぎません。サーバーで 16 コアの場合は、12 か 14 に増やすと顕著な速度向上が期待できます。

## Convert scanned pages – Image Stream コレクションの構築

Aspose は各画像を `ImageStream` として受け取ります。`FromFile` ヘルパーはファイルを読み込み、メモリに保持し、OCR エンジンに渡します。画像がデータベースや HTTP 応答から来る場合は、`MemoryStream` を使用することもできます。

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Edge case:** ファイルが欠損または破損している場合、`FromFile` は `FileNotFoundException` をスローします。入力が信頼できない可能性がある場合は、`try/catch` で構築をラップしてください。

## multiple image ocr – バッチ OCR の実行

ここで本格的な処理が行われます。`RecognizeBatch` は先ほど設定したスレッド数までスレッドを生成し、各画像を処理し、`OcrResult` オブジェクトのリストを返します。

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

内部では、各スレッドが画像を読み込み、ニューラルネットワークを実行し、プレーンテキストを抽出します。結果の順序は入力リストの順序と一致するため、ページ 1 → 結果 0 のように安全にマッピングできます。

## read png text – 抽出されたコンテンツの表示

最後に結果をループし、プレーンテキストをコンソールに出力します。ここで出力をファイルやデータベース、あるいは下流の NLP サービスにパイプすることも可能です。

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### 期待されるコンソール出力

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

空白のセクションが表示された場合、PNG が純白画像でないか確認してください—OCR にはコントラストが必要です。

## 実践的なヒントと一般的な落とし穴

| 状況 | 対策 |
|-----------|------------|
| **Memory pressure** on large batches | 画像を 10‑20 ファイルずつのチャンクで処理し、スパイクが見られたら `GC.Collect()` を呼び出す。 |
| **Incorrect language detection** | `ocrEngine.Configuration.Language = OcrLanguage.English;`（または対象言語）を `RecognizeBatch` を呼び出す前に設定する。 |
| **Slow performance despite parallelism** | SSD が I/O をスロットリングしていないか確認し、すべてのファイルを先にメモリに読み込む（`ImageStream.FromFile` のように）。 |
| **Missing characters** | 高解像度処理のために `ocrEngine.Configuration.DPI = 300;` を増やす。 |

## Extending the Example – PNG から PDF または DOCX へ

最終的に **convert scanned pages** を検索可能な PDF に変換する必要がある場合は、同じ `ocrResults[i].PlainText` を PDF ライブラリ（例: Aspose.PDF）に渡し、テキストを不可視レイヤーとしてオーバーレイすれば完了です。同じ並列処理のテクニックはそこでも有効です。

## 完全なソースコード（コピー＆ペースト可能）

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

`BatchExample.cs` として保存し、`dotnet run` を実行すると、コンソールに PNG スキャン内に隠れていたテキストが表示されます。

## ビジュアルサマリー

![テキスト画像抽出例](images/ocr-batch.png){alt="テキスト画像抽出例"}

この図はフローを示しています: **PNG ファイル → ImageStream コレクション → OcrEngine（max parallelism） → OCR 結果 → コンソール / 下流ストレージ**。

## 結論

これで、C# で **extract text images** しながら **setting max parallelism**、**converting scanned pages**、**multiple image OCR** を処理し、**reading png text** を効率的に行う完全なエンドツーエンドのレシピが手に入りました。コードは自己完結型で、解説は「やり方」だけでなく「なぜ」もカバーし、ヒントは一般的な頭痛の種を回避させてくれます。

次は何をすべきでしょうか？PNG のリストを動的な `Directory.GetFiles` ループに置き換えてみたり、スレッド数を変えて実験したり、出力を検索可能な PDF に流し込んでください。同じパターンは数百ページにもほぼコードを増やさずにスケールします。

質問や厄介なエッジケースがありますか？下にコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}