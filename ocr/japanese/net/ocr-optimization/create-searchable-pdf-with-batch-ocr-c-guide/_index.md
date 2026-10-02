---
category: general
date: 2025-12-29
description: Aspose OCR バッチ処理を使用して、スキャン画像から検索可能な PDF を作成します。画像を PDF に変換し、OCR 用に画像を前処理し、スキャン文書の傾きを補正する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: ja
og_description: Aspose OCR バッチ処理を使用して、スキャン画像から検索可能な PDF を作成します。画像を PDF に変換し、OCR 用に画像を前処理し、スキャンした文書の傾きを補正する方法を学びます。
og_title: バッチOCRで検索可能なPDFを作成 – C#ガイド
tags:
- OCR
- C#
- PDF/A
- Aspose
title: バッチOCRで検索可能なPDFを作成する – C#ガイド
url: /ja/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# バッチ OCR で検索可能 PDF を作成 – C# ガイド

大量のスキャン画像から **検索可能な PDF** を作成したいけど、最初の一歩でつまずいたことはありませんか？同じ壁にぶつかる開発者は多いです。スキャンが乱雑だったり、ページが歪んでいたり、単に大量変換が必要だったりします。  

朗報です！Aspose OCR を使えば、 **バッチ OCR 処理** パイプラインを構築でき、 **画像を PDF に変換** するだけでなく、 **OCR 用に画像を前処理** したり、 **スキャン文書の傾きを自動で補正** したりできます。このチュートリアルでは、エンジンの設定から出力の仕上げまで、フォルダー内のファイルを一括で処理し、検索可能な PDF/A‑2b を生成する手順をすべて解説します。

> **得られるもの:** 画像（または PDF）のディレクトリを受け取り、各ページをクリーンアップし、OCR を実行し、ソースと同じ場所に検索可能な PDF/A‑2b ファイルを出力する、単一の実行可能な C# コンソールアプリです。断片的なコードではなく、統合されたソリューションが手に入ります。

---

## 前提条件

- .NET 6 SDK 以降（コードは .NET Core でもコンパイル可能）  
- Aspose OCR NuGet パッケージ（`Aspose.OCR`）  
- スキャン画像（TIFF、JPEG、PNG）または検索可能 PDF に変換したい PDF のフォルダー  
- （任意）本番用ライセンスキー – ライセンスが無い場合はトライアルモードで透かしが入りますが、テストには問題ありません

これらが揃ったら、さっそく始めましょう。

---

## 概要 – パイプライン全体で検索可能 PDF を作成する流れ

1. **トライアルモードを有効化**（またはライセンスをロード）  
2. **`OcrBatchProcessor` を設定** – 入力フォルダー、出力フォルダー、使用フォーマット、並列スレッド数を指定  
3. **各画像を前処理** – デスクュー、ノイズ除去、背景除去で OCR エンジンがクリーンなページを認識できるようにする  
4. **バッチを実行** – Aspose がすべてのファイルを処理し、OCR を実行して検索可能な PDF/A‑2b を書き出す  
5. **完了を通知** – コンソールにシンプルなメッセージを出すだけですが、ロガーや Webhook に差し替えることも可能  

以上がハイレベルなフローです。以下のコードは各ステップをコメント付きで実装しているので、任意の部分を自由に調整できます。

---

## 手順 1 – トライアルモードを有効化（またはライセンスをロード）

Aspose のクラスを呼び出す前に、ライセンス情報を設定する必要があります。簡易実験ならトライアルモードで十分です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **プロのコツ:** ライセンスの有効化は `Program.cs` の最上部に置きましょう。忘れると `Process()` 初回呼び出し時に例外がスローされます。

---

## 手順 2 – バッチ OCR 処理エンジンを設定

ここで **バッチ OCR 処理** オブジェクトを構築します。例では `InputFolder` と `OutputFolder` が同じですが、別々に指定しても構いません。

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### 設定が重要な理由

- **`MaxDegreeOfParallelism`**: OCR スレッドを増やしすぎると CPU が飽和します。特にミドルスペックのワークステーションでは、4 コアノートパソコンの場合 3 スレッドが最適です。  
- **`Preprocess` パイプライン**: 3 つのフィルタを組み合わせることで OCR 精度が大幅に向上します。デスクューは「傾いたスキャン」問題を解消し、ノイズ除去はランダムノイズを除去、背景除去はエンジンが黒文字・白背景だけを認識できるようにします。  
- **`SaveFormat.SearchablePdf`**: PDF/A‑2b を生成し、アーカイブ対応かつ検索可能な状態にします。多くのコンプライアンス基準で求められる形式です。

---

## 手順 3 – バッチを実行して結果を見る

バッチ実行は `Process()` を呼び出すだけです。メソッドはすべてのファイルが完了するまでブロックし、完了後に戻ります。進捗レポートが必要な場合は `ProgressChanged` イベントをフックできます（ここでは省略）。

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

コンソールに最終行が表示されたら、`C:\Scans\Processed` に各入力画像に対応した検索可能 PDF が生成されています。Adobe Reader で任意のファイルを開き、**Ctrl+F** で検索すれば、スキャンから抽出されたテキストが検索できます。

---

## 手順 4 – 完全な実行可能プログラム（コピー＆ペースト用）

以下は **完結した自己完結型** プログラムです。新しいコンソールプロジェクト（`dotnet new console`）に貼り付けて使用してください。先に Aspose.OCR NuGet パッケージを追加することを忘れずに（`dotnet add package Aspose.OCR`）。

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### 期待される出力

```
All files processed. Searchable PDFs are ready.
```

実行後、`C:\Scans\Processed` を開くと `.pdf` ファイルが並んでいます。すべて検索可能で PDF/A‑2b に準拠しています。任意のファイルを開き、元のスキャンに含まれる単語を入力すれば、テキストがハイライトされます。

---

## よくある質問とエッジケースの対処

### ソースフォルダーに既に PDF が含まれている場合は？

Aspose OCR は PDF を直接取り込めます。各ページをラスタライズし、同じ **前処理** フィルタを適用して OCR レイヤーを埋め込みます。追加コードは不要です。

### 出力形式を検索不可の普通の PDF に変更したい場合は？

`SaveFormat.SearchablePdf` を `SaveFormat.Pdf` に置き換えます。テキストレイヤーは失われますが、見た目はそのままです。

### スキャンがカラーの場合、背景除去は影響しますか？

`RemoveBackground()` は白以外の背景を除去しつつ、主要テキストは保持します。カラー画像やグラフィックを残したい場合はこのフィルタを除外できます。

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### サーバーのメモリが限られている場合、スレッド数を減らせますか？

もちろんです。`MaxDegreeOfParallelism` を `1` または `2` に設定すれば、処理時間は伸びますがメモリ使用量は抑えられます。

---

## ビジュアルサマリー（任意）

フローチャートが好きな方は、以下の流れをイメージしてください：

![検索可能な PDF を作成するワークフロー – 入力フォルダー → 前処理 → OCR → 検索可能な PDF 出力](/images/ocr-workflow.png)

*画像の代替テキスト:* **検索可能な PDF を作成するワークフロー図** – バッチ OCR 処理、変換、デスクュー処理を示しています。

---

## 結論

これで **完全な本番レベル** のソリューションが手に入り、**検索可能 PDF** を任意のスキャン画像バッチから作成できるようになりました。**バッチ OCR 処理** を活用すれば、**画像を PDF に変換**、**OCR 用に画像を前処理**、そして **スキャン文書の傾きを自動補正** する作業が数行の C# コードで完結します。

次のステップは？ カスタム命名規則を追加したり、OCR の信頼度スコアを記録するロギングフレームワークを組み込んだり、`ImageFilters` の `Sharpen()` で薄い文字を強調したりしてみてください。Aspose OCR API は柔軟性が高く、ニーズに合わせて拡張可能です。

Happy coding, and may your PDFs always be searchable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}