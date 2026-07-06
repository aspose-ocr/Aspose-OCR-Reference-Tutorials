---
category: general
date: 2026-02-14
description: 画像ファイルを読み込み、Aspose OCR GPUエンジンを使用してレシートからテキストを抽出します。最大GPUメモリの設定方法、GPUメモリの構成方法、そして画像上でOCRを効率的に実行する方法を学びます。
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: ja
og_description: 画像ファイルを読み込み、Aspose OCR GPUエンジンを使用してレシートからテキストを抽出します。このガイドでは、GPU の最大メモリを設定し、C#
  で画像に対して OCR を実行する方法を示します。
og_title: C#で画像ファイルを読み込み、GPU OCRで領収書テキストを抽出
tags:
- C#
- OCR
- Aspose
- GPU
title: C#で画像ファイルを読み込み、GPU OCRで領収書テキストを抽出
url: /ja/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU OCR を使用した C# での画像ファイルの読み込みとレシートテキスト抽出

画像ファイルを **load image file** してレシートから正確なテキストを取得したいと思ったことはありませんか？OCR の段階で行き詰まった方は他にもいます。実際のアプリケーション—経費トラッカー、在庫管理システム、あるいはシンプルなレシートスキャンボット—では、レシート画像をすばやく読み取る能力がゲームチェンジャーになることがあります。  

良いニュースです。Aspose.OCR の GPU 加速エンジンを使えば、**load image file**、**set max GPU memory**、そして **run OCR on image** を数行の C# で実行できます。以下では、GPU の設定から抽出されたプレーンテキストの出力まで、全工程を順に解説します。

## 学べること

* **Load image file** を Aspose の `ImageStream` でディスクから読み込む。
* **Configure GPU memory** を設定し、エンジンが許可された以上の RAM を使用しないようにする。
* **Run OCR on image** を実行し、レシート上のすべての文字を抽出する。
* Out‑of‑memory エラーやぼやけたスキャンなど、一般的な落とし穴に対処する。
* 出力を検証し、精度向上のために設定を調整する。

外部サービスや特殊なテクニックは不要です。純粋な C# コードだけで、任意の .NET 6+ プロジェクトに組み込むことができます。

---

## 前提条件

始める前に、以下が揃っていることを確認してください。

* .NET 6 SDK またはそれ以降がインストールされていること。
* 有効な Aspose.OCR ライセンス（または無料評価モード）を持っていること。
* プロジェクトに `Aspose.OCR` と `Aspose.OCR.Gpu` NuGet パッケージが追加されていること。
* サンプルのレシート画像（`receipt.png`）がディスク上に用意されていること。

これらのいずれかが不明な場合は、一度止めてパッケージをインストールしてください：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

以上です。GPU サポートは NuGet パッケージに組み込まれているため、追加のネイティブライブラリは不要です。

---

## 画像ファイルの読み込みと GPU エンジンの準備

最初に行うべきことは、**load image file** を `ImageStream` に読み込むことです。このオブジェクトはファイルシステムの詳細を抽象化し、OCR エンジンにクリーンなインメモリ表現を提供します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Why this matters:**  
`ImageStream.FromFile` を使用した *Loading the image file* は、エンジンが正確なピクセルデータを取得し、DPI とカラーデプスを保持することを保証します。このステップを省略したり、破損したストリームを渡すと、OCR が文字を見逃したり例外が発生したりします。

> **Pro tip:** ユーザーがアップロードしたファイルを扱う場合は、`FromFile` 呼び出しを try‑catch ブロックでラップし、まずファイルサイズを検証してください。大きな画像は、**configured GPU memory** を適切に設定していないと GPU メモリを圧迫します。

---

## 最適なパフォーマンスのための Max GPU Memory の設定

GPU リソースは貴重です。特に共有サーバーや VRAM が限られたラップトップではなおさらです。`MaxDeviceMemory` プロパティは、Aspose に対して GPU メモリのうちどれだけ安全に割り当てられるかを指示します。

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

**set max GPU memory** を設定すると、要求に応えられない場合はエンジンが自動的に CPU 処理にフォールバックし、クラッシュを防止します。これはデバイス固有の上限をハードコーディングせずに **configure GPU memory** を行う最も安全な方法です。

**When to adjust:**  

- `OutOfMemoryException` が大量バッチ処理中に発生した場合は、上限を下げてください。
- レシートが高解像度（300 DPI 以上）の場合は、速度を保つために 2 GB に上げてください。

---

## 画像で OCR を実行してレシートからテキストを抽出する

さあ楽しいパートです—実際に **run OCR on image** を実行し、レシートのテキストを取得します。`Recognize` メソッドは、プレーンテキスト出力を持つ `Text` プロパティを含む `OcrResult` オブジェクトを返します。

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

コンソールには次のような出力が表示されます：

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Why this works:**  
GPU エンジンはさまざまな文書レイアウトでトレーニングされたディープラーニングモデルを実行します。クリーンで正しく読み込まれた画像を提供することで、モデルは **extract text from receipt** を正確に行う最良の機会を得ます。

---

## 出力の検証と一般的な落とし穴

強力なエンジンでも、OCR は魔法ではありません。注意すべき点をいくつか挙げます：

| 問題 | 原因 | 対策 |
|------|------|------|
| 文字化け | コントラストが低い、または画像がぼやけている | Aspose の `ImageProcessor` で前処理し、コントラストを上げる |
| 行が欠落 | 画像が切りすぎている | レシートが画像の境界内に完全に収まっていることを確認する |
| メモリ不足エラー | `MaxDeviceMemory` が画像サイズに対して低すぎる | `MaxDeviceMemory` を増やすか、先に画像を縮小する |
| 言語が間違っている | レシートに英語以外のテキストが含まれている | `gpuEngine.Language = OcrLanguage.Spanish;` など適切な言語を設定する |

これらの問題に直面した場合の簡単な回避策は、画像の長辺を 2000 px 未満にリサイズすることです。これにより、ほとんどのレシートで可読性を損なうことなく GPU の負荷が大幅に減ります。

---

## 完全な動作例（コピー＆ペースト可能）

以下はコンパイル可能な完全なプログラムです。ファイルパスを自分のレシートの場所に置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected console output**（もちろんレシートによって出力は異なります）：

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

`dotnet run` でプログラムを実行してください。テキストが表示されれば、**load image file**、**set max GPU memory**、そして **run OCR on image** を使って **extract text from receipt** に成功したことになります。おめでとうございます。

---

## よくある質問

**Q: Does this work on machines without a dedicated GPU?**  
A: はい。Aspose.OCR は互換性のある GPU が検出されない場合、CPU モードに優雅にフォールバックします。**load image file** と **run OCR on image** は引き続き可能ですが、少し遅くなります。

**Q: Can I process multiple receipts in a batch?**  
A: もちろんです。認識コードを `foreach` ループで囲みますが、同じ `GpuEngine` インスタンスを再利用することを忘れないでください。これにより、各ファイルごとに GPU リソースを再初期化する必要がなくなります。

**Q: What if my receipt is in a language other than English?**  
A: 認識を呼び出す前に言語を設定してください：

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## 次のステップと関連トピック

基本をマスターしたので、以下の項目を検討してください：

* **Fine‑tuning OCR accuracy** – `gpuEngine.RecognitionOptions` の `EnableDeskew` や `ContrastEnhancement` などを試してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}