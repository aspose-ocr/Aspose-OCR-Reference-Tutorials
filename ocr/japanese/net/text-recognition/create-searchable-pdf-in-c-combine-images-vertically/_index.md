---
category: general
date: 2026-02-28
description: 画像を縦に結合してC#で検索可能なPDFを作成する。画像を縦にスタックする方法と、Aspose OCRを使用してスキャンしたページのPDFを変換する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: ja
og_description: C#で画像を縦に結合して検索可能なPDFを作成します。このガイドでは、画像を縦に積み重ね、Aspose OCRを使用してスキャンしたページのPDFに変換する方法を示します。
og_title: C#で検索可能なPDFを作成 – 画像を縦に結合
tags:
- Aspose OCR
- C#
- PDF generation
title: C#で検索可能なPDFを作成 – 画像を縦に結合
url: /ja/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で検索可能な PDF を作成 – 画像を縦に結合する

数枚のスキャンした PNG から **検索可能な PDF** を作成したいけど、どこから手を付ければいいか分からないことはありませんか？ 多くの文書自動化プロジェクトで最大の課題は、画像ファイルの山をきれいに整理された検索可能な PDF に変換し、インデックス付けや共有ができるようにすることです。

このチュートリアルでは、**画像を縦にスタックする方法**、**画像を縦に結合する方法**、そして最終的に **Convert Scanned Pages PDF** を単一の検索可能なドキュメントに変換する手順を、Aspose.OCR の GPU 加速エンジンを使った実行可能なサンプルで解説します。最後まで実装すれば、任意の .NET ソリューションに組み込める自己完結型プログラムが手に入ります。

> **学べること**
> - GPU 対応の OCR エンジンを初期化する
> - 画像バッチを並列処理する
> - **画像を縦に結合**してマルチページスキャンを再現する
> - 検索可能な PDF と詳細な JSON レポートをエクスポートし、下流の分析に活用する

## 前提条件

- .NET 6+（コードは .NET 6、.NET 7、.NET 8 でコンパイル可能）
- Aspose.OCR NuGet パッケージ (`Install-Package Aspose.OCR`)
- `ProcessingMode.Gpu` 設定を使用したい場合は GPU 対応マシン（CPU フォールバックも可）
- 数枚のスキャン PNG/JPEG が入ったフォルダー（デモでは `page1.png`、`page2.png`、`page3.png` を使用）

外部サービスや隠し設定ファイルは不要です。純粋な C# だけで完結します。

## Step 1 – **Create Searchable PDF** 用に OCR エンジンを設定する

まず `OcrEngine` を作成し、GPU 加速を有効にし、言語を英語に設定し、前処理フィルタを数個追加します。これらのフィルタは、傾いたページを補正する `DeskewFilter` とノイズ除去を行う `DenoiseFilter` によって認識精度を向上させます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**重要ポイント:** OCR エンジンがテキスト認識の重い処理を担います。`ProcessingMode.Gpu` を有効にすると、最新のグラフィックカード上で認識時間が半分になることもあります。一方、フィルタはスキャン時に発生しがちなアーティファクトを除去し、文字化けを防ぎます。

## Step 2 – **Convert Scanned Pages PDF** を効率的に行うバッチプロセッサを構成する

画像を1枚ずつ処理するのは数枚であれば問題ありませんが、実務では数十〜数百ページになることが普通です。Aspose.OCR の `OcrBatchProcessor` を使えば認識を並列実行でき、**convert scanned pages pdf** のステップが劇的に高速化します。

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**プロのコツ:** CPU のみの環境の場合は `ProcessingMode = ProcessingMode.Cpu` に設定してください。バッチプロセッサは `MaxDegreeOfParallelism` を尊重するので、マシンへの負荷を抑えるよう調整できます。

## Step 3 – バッチで OCR を実行し結果を取得する

いよいよテキスト認識を行います。`Recognize` メソッドは `OcrResult` オブジェクトのリストを返し、各オブジェクトは元画像と抽出テキストの両方を保持します。

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

ここまでで **create searchable PDF** に必要なものはすべて揃いました：メモリ上に残っている画像と、対応するテキストレイヤーです。

## Step 4 – **Combine Images Vertically** して検索可能な PDF を生成する

多くのスキャン文書はマルチページ PDF になるため、個々のページ画像を1枚の縦長画像に結合し、実際の紙の束に見立てます。Aspose.OCR の `Image.CombineVertical` がまさにこの用途向けに用意されています。

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

生成されたファイル (`combined_searchable.pdf`) には、各ページ画像の下に選択・検索可能なテキストが埋め込まれています。これが **create searchable PDF** をスキャンソースから作る最終形です。

![検索可能な PDF の例](/images/create-searchable-pdf.png "検索可能な PDF の例")

*画像代替テキスト: 検索可能なテキストが埋め込まれた結合 PDF の例。*

**なぜ縦にスタックするのか？** 多くの OCR ライブラリは画像ごとに別ページとして扱います。画像を縦に結合すれば、PDF のページ順序を保ちつつ、1回の OCR パスで文書全体を処理できます。

## Step 5 – 1 ページ目の詳細 JSON をエクスポートする（下流ワークフローに便利）

PDF だけでなく、OCR データをデータベースや機械学習パイプラインに流したいこともあります。Aspose.OCR は各 `OcrResult` を JSON にシリアライズでき、バウンディングボックスや信頼度スコアなどを保持します。

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**期待される JSON スニペット（抜粋）:**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

この JSON を任意の下流システムに渡せば、Elasticsearch でのテキストインデックス作成やカスタム分析ダッシュボードへの投入が簡単に行えます。

---

## **Stack Images Vertically** の手順 – 簡単まとめ

Aspose を使わずに **how to stack images vertically** したい場合は、`System.Drawing` で新しいビットマップを作成し、各ページを順に描画することが考えられます。ただし、Aspose の `Image.CombineVertical` は DPI、ピクセルフォーマット、メモリ管理を自動で処理してくれるため、実運用コードでは圧倒的に信頼性が高いです。

### 代替案: `System.Drawing` を使う（好奇心向け）

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

手動アプローチでも動作しますが、DPI の自動処理や `RecognizeToPdf` への直接入力といった便利機能が失われます。特別な要件がない限り、`CombineVertical` を使用してください。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| **Out‑of‑memory エラー**（多数の高解像度スキャンを処理中） | 画像が PDF 書き出しまでメモリに残り続ける | `using` ブロックで `Image` オブジェクトを速やかに破棄するか、結合前に画像を縮小する |
| **OCR 後に文字化け** | 傾きや低コントラストのスキャン | `DeskewFilter` と `DenoiseFilter` を必ず使用し、必要に応じて `ContrastFilter` を追加 |
| **検索レイヤーが欠如** | `Recognize` のみ呼び出した | 結合画像に対して `ocrEngine.RecognizeToPdf` を必ず呼び出す |
| **GPU フォールバックが失敗**（ドライバ不備のマシン） | `ProcessingMode.Gpu` が例外を投げる | エンジン作成を try/catch で囲み、例外時は `ProcessingMode.Cpu` に切り替える |

## 次のステップ – ワークフローの拡張

**create searchable PDF** の方法が分かったら、以下のような拡張が考えられます。

- `Directory.GetFiles` と `foreach` ループでフォルダー全体をバッチ処理
- 結合前に各ページへ透かしを追加（Aspose.Imaging の `ImageProcessor` を使用）
- 後でページ単位の PDF が必要な場合は、検索可能 PDF を個別ページに分割（Aspose.PDF の `PdfDocument.Split`）
- Azure Blob Storage と連携し、クラウド上の画像を取得・最終 PDF をアップロード

これらすべては、OCR 設定、画像処理、PDF 出力という共通のコア概念をベースに実装できます。

---

## 結論

C# でスキャン画像のコレクションから **create searchable PDF** を作成するために必要な手順をすべて網羅しました。GPU 対応の `OcrEngine` を初期化し、`OcrBatchProcessor` で並列バッチ処理を行い、**画像を縦に結合**し、最後に `RecognizeToPdf` を呼び出すだけで、アーカイブやインデックス作成に適した整然とした検索可能ドキュメントが完成します。さらに JSON エクスポートを加えることで、OCR 結果の可視化やカスタムワークフローへの活用が容易になります。

ぜひ実装してみて、フィルタを変えてみたり、パフォーマンスを測定したりして、文書自動化パイプラインをよりスムーズにしましょう。疑問や問題があればコメントで教えてください。Happy coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}