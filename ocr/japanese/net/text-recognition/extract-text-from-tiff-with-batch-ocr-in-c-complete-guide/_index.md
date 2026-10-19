---
category: general
date: 2026-04-11
description: C#で Aspose OCR のバッチ処理を使用して TIFF ファイルからテキストを抽出します。バッチ OCR を効率的に処理し、リアルタイムの進捗フィードバックを取得する方法を学びましょう。
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: ja
og_description: C#でAspose OCRのバッチ処理を使用してTIFFファイルからテキストを抽出します。このチュートリアルでは、バッチOCRの処理方法と進捗の取得方法をステップバイステップで示します。
og_title: C#でバッチOCRを使用してTIFFからテキストを抽出する – 完全ガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でバッチOCRを使用してTIFFからテキストを抽出する完全ガイド
url: /ja/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF からテキストを抽出 – バッチ OCR 完全ガイド

TIFF ファイルから **テキストを抽出** したいと思ったことはありますか、しかしバッチ処理の部分で行き詰まってしまったことはありませんか？ あなただけではありません。多くのドキュメント自動化プロジェクトでは、数十枚の高解像度 TIF 画像を扱うことがすぐにボトルネックになり得ます—特に進捗のリアルタイムフィードバックが欲しい場合はなおさらです。  

良いニュースです。Aspose OCR を使えば、数行のコードで **process batch OCR** を実行し、リアルタイムの進捗イベントを取得し、各画像の認識テキストを出力できます。このチュートリアルでは、すぐに実行できる C# コンソールアプリを使ってその手順を詳しく解説します。

必要なパッケージ、各行が重要な理由、ファイルが欠損している場合などのエッジケース、結果の検証方法など、知っておくべきすべてをカバーします。最後まで読めば、サンプルを自分のソリューションに組み込んで、すぐに TIFF 画像からテキストを抽出できるようになります。

## 必要なもの

- **.NET 6 以降**（コードは .NET Core でもコンパイル可能）  
- **Aspose.OCR for .NET** NuGet パッケージ – `Install-Package Aspose.OCR`  
- 読み取りたい **TIFF** 画像が数枚入ったフォルダー（デモでは `img1.tif`, `img2.tif`, `img3.tif` を使用）  
- 好きな IDE で構いません – Visual Studio、Rider、または VS Code で OK です  

追加設定は不要です。ライブラリには独自の OCR エンジンが同梱されているため、外部のネイティブバイナリをインストールする必要はありません。

---

## ステップ 1 – OCR エンジン インスタンスの作成  

最初に行うのは `OcrEngine` を起動することです。各ピクセルを解析して文字に変換する脳のようなものと考えてください。

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **なぜ重要か:**  
> エンジンは内部の言語モデルや設定（例：DPI、言語）を保持しています。エンジンを一度作成してバッチで再利用する方が、画像ごとに新しいエンジンをインスタンス化するよりはるかに効率的です。

---

## ステップ 2 – リアルタイム進捗イベントの設定  

数十枚の TIFF ファイルを処理する場合、進捗インジケーターがアプリが停止しているかどうかの疑問を解消してくれます。

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

`ProgressChanged` イベントは各画像の処理が完了した後に発火し、`Current`、`Total`、`Percentage` を提供します。これは多くの開発者が実装し忘れがちな **process batch OCR** フィードバックループです。

---

## ステップ 3 – Image Stream のリスト構築  

Aspose.OCR は `ImageStream` オブジェクトを使用します。最も簡単な方法は、ディスクから各 TIFF を読み込むことです。

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **ヒント:**  
> 動的なフォルダーがある場合は、ハードコーディングされたリストを `Directory.GetFiles(path, "*.tif")` と `Select(ImageStream.FromFile)` に置き換えてください。これにより、手動で更新することなく本当に **process batch OCR** が実行できます。

---

## ステップ 4 – バッチ OCR プロセスの実行  

ここで本格的な処理が行われます。`ProcessBatch` は読み取り専用の `OcrResult` オブジェクトのリストを返し、各オブジェクトには抽出されたテキストと信頼度スコアが含まれます。

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **なぜ効率的か:**  
> エンジンはすべての画像で同じ言語モデルを再利用するため、単一画像呼び出しと比較してメモリの消費が大幅に減少します。

---

## ステップ 5 – 認識テキストの表示または保存  

最後に、結果を反復処理します。実際のプロジェクトではデータベースや JSON ファイルに書き込むこともありますが、このデモではコンソールに出力するだけです。

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**期待されるコンソール出力**（簡略化）:

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

画像が失敗した場合、`result.Text` は空文字列になり、`ProgressChanged` イベントは依然としてその項目が処理されたと報告します—したがって失敗は別途ログに記録できます。

---

## 進捗イベントハンドラ（完全コード）

`BatchDemo` クラス内の任意の場所にこのメソッドを配置してください—できれば `Main` の後が望ましいです。

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **プロのヒント:**  
> デスクトップアプリを作成する場合は、この出力を UI のプログレスバーにリダイレクトしてください。同じイベントは WinForms、WPF、さらには ASP.NET Core SignalR の通知でも機能します。

---

## 完全な実行可能サンプル  

すべてをまとめると、以下が新しいコンソールプロジェクトにコピー＆ペーストできる完全なプログラムです。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

`Program.cs` として保存し、`dotnet add package Aspose.OCR` を実行し、`YOUR_DIRECTORY` を実際のパスに置き換えて **Ctrl+F5** を押してください。各 TIFF の抽出テキストとともに進捗数値が表示されるはずです。

---

## 一般的なエッジケースの処理  

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **欠損または破損した TIFF** | `ImageStream.FromFile` が `FileNotFoundException` または `ArgumentException` をスローします。 | リスト作成を `try/catch` で囲み、無効なファイルをスキップし、問題をログに記録します。 |
| **非常に大きな画像（ >10 MP ）** | OCR が大量の RAM を消費し、処理が遅くなる可能性があります。 | 処理前に DPI を下げます: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **英語以外のテキスト** | デフォルトの言語モデルは英語です。 | `ocrEngine.Language = Language.Spanish;` を設定します（またはサポートされている任意の言語）。 |
| **結果を保存する必要がある** | コンソール出力は永続的ではありません。 | `result.Text` を `File.WriteAllText` を使って `.txt` ファイルに書き込みます。 |

これらのシナリオに対処することで、ソリューションは堅牢になり、ハッピーパス以外も考慮したことが示せます。

---

## 次のステップと関連トピック  

- **PDF からテキストを抽出** – 同様の API で、`ImageStream` を `PdfDocument` に置き換えるだけです。  
- **並列バッチ OCR** – 大規模なワークロードの場合、別スレッドで複数の `OcrEngine` インスタンスを起動します。ライセンス制限に注意してください。  
- **ポストプロセッシング** – OCR 出力をスペルチェッカーや正規表現で処理し、一般的な OCR アーティファクトをクリーンアップします。  

これらすべての拡張は、**process batch OCR** というコアコンセプトに基づいており、段階的に追加できます。

---

## 結論  

ここでは、Aspose OCR を使用した C# における **process batch OCR** によって、**TIFF からテキストを抽出** する効率的な方法を実演しました。サンプルは単一のエンジンを作成し、進捗イベントを購読し、Image Stream のリストをロードし、バッチを実行して各結果を出力します。  

ここからは、出力をデータベースに統合したり、検索可能な PDF を生成したり、テキストを下流の NLP パイプラインに渡したりできます。可能性は無限です—言語設定や DPI の調整、並列実行を試して、特定のワークロードに合わせて最適化してください。  

質問がある、またはバッチのカスタマイズ方法を共有したい方は、下にコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}