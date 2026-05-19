---
date: 2026-02-25
description: Aspose.OCR for .NET を使用して画像をテキストに変換する方法を学び、正確な OCR 認識設定で画像からテキストを抽出します。
linktitle: convert image to text – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: 画像をテキストに変換 – URLから画像のOCRを実行
url: /ja/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像をテキストに変換 – URL から画像の OCR を実行する

## Introduction

.NET アプリケーションで **画像をテキストに変換** する必要がある場合、Aspose.OCR for .NET を使用すれば、ウェブ上の任意の場所にホストされた画像からテキストを確実に抽出できます。このチュートリアルでは、公開 URL にある画像からテキストを認識し、OCR 認識設定を構成し、結果を処理する方法を数分で学びます。

## Quick Answers
- **このチュートリアルで取り上げる内容は？** Aspose.OCR for .NET を使用した、公開 URL からの画像をテキストに変換する方法。  
- **対象の主要キーワードは？** *convert image to text*  
- **ライセンスは必要ですか？** トライアルは利用可能ですが、商用利用には製品ライセンスが必要です。  
- **サポートされている .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **実装にかかる時間は？** 基本的なセットアップで通常 10 分未満です。

## What is “convert image to text”?
画像をテキストに変換するとは、文字のビジュアル表現を編集可能で検索可能な文字列に変換することです。このプロセスは **extract text from image** とも呼ばれ、文書のデジタル化、データ入力の自動化、アクセシビリティソリューションを支えます。

## Why use Aspose.OCR for .NET to convert image to text?
- **高精度**：組み込みの言語サポートとオプションの **OCR language pack** 拡張機能。  
- **細かい OCR 認識設定**：自動傾き補正、領域検出、複数行処理など。  
- **シンプルな API**：.NET Framework と .NET Core の両方で外部依存なしに動作。  
- **直接 URL 対応** – 画像を事前にダウンロードせずに **recognize text from URL** が可能です。必要に応じて **download image for OCR** してストリームから処理することもできます。

## Prerequisites

開始する前に以下を用意してください。

- Aspose.OCR for .NET がインストール済み。最新ライブラリは [release page](https://releases.aspose.com/ocr/net/) から取得できます。  
- .NET 開発環境（Visual Studio、VS Code、またはお好みの IDE）。  
- 画像を取得するためのインターネット接続。

## Import Namespaces

Aspose.OCR クラスを使用できるように、必要な名前空間を追加します。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Step‑by‑Step Guide to Convert Image to Text from a URL

### Step 1: Set Up Your Document Directory
一時ファイルや結果を保存するディレクトリを定義します。

```csharp
string dataDir = "Your Document Directory";
```

### Step 2: Provide the Image URL
公開アクセス可能な URL を指定します。画像が認証を必要とする場合は、まず **download image for OCR** してからストリームを使用します。

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Step 3: Initialize the AsposeOcr Engine
OCR エンジンのインスタンスを作成します。

```csharp
AsposeOcr api = new AsposeOcr();
```

### Step 4: Configure OCR Recognition Settings
エンジンが画像を処理する方法を細かく調整します。ここでは領域検出と自動傾き補正を有効にし、例として 2 つのカスタム矩形を指定しています（**ocr recognition settings** の例）。

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

> **Pro tip:** カスタム領域が不要な場合は `DetectAreas = false` に設定し、エンジンにテキストブロックを自動検出させてください。

### Step 5: Output the OCR Result
認識されたテキスト、検出された領域、警告、およびデバッグ用の完全な JSON ペイロードを出力します。

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Step 6: Confirm Successful Execution
例外が発生しなければ、簡単な確認メッセージで処理が完了したことを知らせます。

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Common Issues and Solutions

- **Image not publicly accessible** – ブラウザで URL が開くか確認してください。保護された画像の場合は先にダウンロードし、`RecognizeImageFromStream` を呼び出します。  
- **Recognition areas are off** – `Rectangle` の値を調整するか、`DetectAreas` を無効にしてエンジンに自動検出させます。  
- **Language not recognized** – 適切な **OCR language pack** をインストールし、`RecognitionSettings` の `Language = "eng"`（または他の ISO コード）を設定してください。  

## Frequently Asked Questions

### Q1: Is Aspose.OCR suitable for handling multiple languages?
**A:** はい。該当する **ocr language pack** を追加することで、数十言語のテキストを認識できます。

### Q2: Can I use Aspose.OCR for both single‑line and multi‑line text extraction?
**A:** もちろんです。シナリオに合わせて `RecognitionSettings` の `RecognizeSingleLine` を切り替えてください。

### Q3: Are there licensing options for commercial projects?
**A:** はい、ライセンスオプションは [Aspose store](https://purchase.aspose.com/buy) で確認・購入できます。

### Q4: Is there a free trial available?
**A:** はい、[releases page](https://releases.aspose.com/) からトライアル版をダウンロード可能です。

### Q5: Where can I find community support?
**A:** 専用の [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) で質問や議論が行えます。

## Conclusion

Aspose.OCR for .NET を使用すれば、リモート URL から画像をテキストに変換する作業はシンプルかつ高度にカスタマイズ可能です。上記の手順に従うことで、シンプルな **extract text from image** 機能から、複雑な文書向けの高度な **ocr recognition settings** まで、あらゆる .NET アプリケーションに強力な OCR 機能を組み込めます。

---

**Last Updated:** 2026-02-25  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}