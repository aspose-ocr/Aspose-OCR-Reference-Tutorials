---
category: general
date: 2026-05-28
description: C# を使用して画像上で OCR を実行し、画像からテキストを読み取り、レシートのテキストを高速に抽出します。GPU のオプションとロード技術を学びましょう。
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: ja
og_description: C#で画像のOCRを実行する。このチュートリアルでは、画像からテキストを読み取る方法、レシートからテキストを抽出する方法、そしてGPU使用率を最適化する方法を示します。
og_title: 画像でOCRを実行する – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: 画像でOCRを実行する – 完全なC#ガイド
url: /ja/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行 – 完全 C# ガイド

画像ファイルに **OCR を実行** したいけど、どこから始めればいいか分からないことはありませんか？ 初めて画像データからテキストを読み取ろうとする開発者の多くが同じ壁にぶつかります。朗報は、数行の C# コードでレシートのスキャンや PDF、任意の写真からテキストを抽出できることです。このガイドでは、**OCR 用に画像をロード** し、GPU 加速を活用し、メモリ使用量を安全に制限する方法も示した、すぐに実行できる完全なサンプルを順を追って解説します。

このチュートリアルを終えると、以下ができるようになります。

* C# で OCR エンジンを初期化する  
* ディスクまたはストリームから **OCR 用に画像をロード** する  
* 任意で GPU サポートを利用し **画像からテキストを読み取る**  
* **レシートからテキストを抽出** し、コンソールに出力する  

外部サービスは不要です。ローカルのライブラリとサンプルレシート画像だけで完結します。

---

## 必要なもの

| 前提条件 | 理由 |
|--------------|--------|
| .NET 6.0 SDK 以降 | 最新ランタイムで、最新の言語機能をサポート |
| `OcrEngine` クラスを提供する OCR ライブラリ（例: IronOCR、Tesseract .NET ラッパー） | 本稿で使用する `Configuration` と `Recognize` メソッドを提供 |
| CUDA 対応 GPU（任意） | `EnableGpu` フラグで高速処理が可能 |
| サンプルレシート画像（`receipt.jpg`） | **レシートからテキストを抽出** のステップを実演 |
| 任意の C# IDE（Visual Studio、Rider、VS Code） | コンパイルとデバッグを迅速に行うため |

GPU がなくても、コードは自動的に CPU モードにフォールバックしますので安心してください。

---

![画像で OCR を実行 のサンプルコンソール出力](https://example.com/ocr-output.png "画像で OCR を実行 – サンプルコンソール出力")

*Alt text: 画像で OCR を実行 のサンプルコンソール出力（認識されたレシートテキストを表示）*

---

## 手順 1: 画像で OCR を実行 – エンジンの設定

まず最初に OCR エンジンのインスタンスを作成します。このオブジェクトがプロセスの中心で、すべての設定情報を保持し、重い処理を実行します。

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*重要ポイント:* `OcrEngine` クラスはネイティブ OCR エンジン（Tesseract、IronOCR など）をラップしています。一度インスタンス化して複数画像で再利用することでオーバーヘッドを削減し、設定変更も一箇所で行えます。

---

## 手順 2: OCR 用に画像をロード

エンジンが何かを読む前に、画像を供給する必要があります。ライブラリの `Image` プロパティは実装に応じてストリームまたはファイルパスを受け取ります。

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*ヒント:* ユーザーアップロードを扱う場合は `try/catch` でラップし、先にファイルタイプを検証してください。未対応フォーマットは例外がスローされ、適切にハンドリングできます。

---

## 手順 3: GPU 加速を有効化（任意）

マシンに対応する CUDA または OpenCL ランタイムがある場合、GPU モードをオンにすると認識ごとに数秒の短縮が期待できます。

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*プロのコツ:* すべての GPU が同等ではありません。古いカードではドライバのオーバーヘッドにより若干遅くなることがあります。`EnableGpu = true/false` の両方でベンチマークし、ハードウェアに最適な方を選びましょう。

---

## 手順 4: GPU メモリ使用量を制限（任意）

GPU を他のワークロード（例: ディープラーニング推論）と共有している場合、OCR がすべての GPU メモリを食いつぶさないようにしたいことがあります。

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*使用シーン:* 多数の画像を同時に処理する Web サービスを運用している場合、メモリ上限を設定することで OOM クラッシュを防げます。

---

## 手順 5: テキストを認識し、画像からテキストを読み取る

エンジンの準備が整ったので、いよいよ OCR パイプラインを走らせます。`Recognize()` を呼び出すと抽出された文字列が返ります。

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*核心:* この一行で二値化や傾き補正といった前処理、そして文字分類までが内部で実行されます。返される `recognizedText` はプレーンな Unicode 文字列で、後続の処理にすぐ使えます。

---

## 手順 6: レシートからテキストを抽出 – 出力

最後に結果をコンソールに書き出すか、必要な場所に保存します。レシートの場合は、後で行項目や合計、日付などをパースすることが想定されます。

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**期待されるコンソール出力（抜粋）:**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

OCR が特定のレシートレイアウトでうまく認識できない場合は、前処理オプション（例: `ocrEngine.Configuration.Deskew = true`）を調整したり、解像度の高い画像を使用したりしてください。

---

## よくあるエッジケースと対処法

| 状況 | 推奨対策 |
|-----------|----------------|
| **画像が null** – `ocrEngine.Image` が `null` | 代入前にファイルパスを検証し、欠損時は明確な `ArgumentException` をスロー |
| **GPU が利用不可** – `EnableGpu = true` が `PlatformNotSupportedException` をスロー | GPU 有効化呼び出しを `try/catch` でラップし、例外時は CPU モードにフォールバック |
| **大容量レシート（> 10 MB）** がメモリ圧迫を引き起こす | `GpuMemoryLimit` を使用するか、画像をタイル単位で処理（`ocrEngine.Configuration.TileSize`） |
| **言語検出が誤っている** – 出力が文字化け | `ocrEngine.Configuration.Language = "eng"`（または該当 ISO コード）で言語を強制指定 |

---

## 本番向け OCR のプロティップス

1. **バッチ処理:** 画像バッチ全体で単一の `OcrEngine` インスタンスを再利用すると、言語モデルがキャッシュされレイテンシが低減します。  
2. **前処理:** エンジンに渡す前に簡易的なグレースケール変換とコントラスト強化を行うと精度が向上します。多くのライブラリは `Preprocess` メソッドを提供しています。  
3. **エラーロギング:** 各 `Recognize()` 呼び出し後に `ocrEngine.LastError`（利用可能な場合）を取得し、サービスをクラッシュさせずに失敗原因を記録します。  
4. **スレッド安全性:** 大半の OCR エンジンは **スレッドセーフではありません**。並列処理が必要な場合はスレッドごとに別インスタンスを作成するか、キューで順次処理します。

---

## 結論

ここまでで、C# における **画像で OCR を実行** のフルワークフローを体験しました。エンジンの作成、**OCR 用に画像をロード**、GPU 加速の切り替え、そして最終的に **レシートからテキストを抽出** するまでの流れをマスターしたので、より高度な文書処理パイプラインの構築に自信を持って取り組めます。

次のステップ例:

* 正規表現や自然言語処理ライブラリを使ってレシートテキストを構造化 JSON に変換（**画像からテキストを読み取る** 自動化に最適）  
* ASP .NET Core API に OCR ステップを組み込み、ユーザーが HTTP 経由でレシートをアップロードできるようにする  
* Tesseract と商用 SDK（例: IronOCR）を比較し、精度と速度のベンチマークを取る  

さまざまなレシートレイアウトで試し、設定を微調整すれば、ぼやけた写真でもすぐに活用可能なデータに変換できます。コーディングを楽しんで、画像が常に鮮明であることを願っています！

## 関連チュートリアル

- [Aspose.OCR を使用した言語選択付き画像テキスト抽出 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose.OCR for .NET による OCR 最適化 – 画像からテキスト抽出](/ocr/english/net/ocr-optimization/)
- [OCR で矩形領域を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}