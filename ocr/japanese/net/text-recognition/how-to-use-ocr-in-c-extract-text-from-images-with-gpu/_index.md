---
category: general
date: 2026-02-13
description: C#でOCRを使用して画像ファイルからテキストを抽出し、GPU処理を有効にし、スキャンを迅速にテキストに変換する方法を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: ja
og_description: C#でOCRを使用する方法は？このガイドでは、画像ファイルからテキストを抽出し、GPU処理を有効にし、スキャンをテキストに変換する方法を示します。
og_title: C#でOCRを使用する方法 – GPUで画像からテキストを抽出
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: C#でOCRを使用する方法 – GPUで画像からテキストを抽出
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – GPUで画像からテキストを抽出

スキャンした文書からテキストを楽に抽出する方法、**OCRの使い方**を考えたことはありませんか？ あなただけではありません—開発者は常に「画像ファイルから効率的にテキストを抽出するにはどうすればいいか？」と質問します。 良いニュースは、Aspose.OCR を使えばまさにそれが可能で、サポートされているハードウェア上で目に見える速度向上を得るために **GPU処理を有効に** することもできます。

このチュートリアルでは、**OCRの使い方**、**画像からテキストを抽出する方法**、**スキャンをテキストに変換する方法**、そしてGPUが利用できない場合の対処方法を示す、完全なエンドツーエンドの例を順に解説します。最後まで実行すれば、認識されたテキストを出力し、GPUが実際に使用されたかどうかを表示する、すぐに実行可能なC#コンソールアプリが手に入ります。

## 必要なもの

- .NET 6 SDK 以上（コードは .NET Core でも動作します）  
- Visual Studio 2022 またはお好みのエディタ  
- Aspose.OCR for .NET パッケージ（NuGet 経由で入手可能）  
- テスト用の高解像度画像ファイル（例：`highres_scan.tif`）  

特別なセットアップは不要です—数行の NuGet コマンドを実行すればすぐに始められます。

## 手順 1: Aspose.OCR をインストールし、プロジェクトを準備する

まず最初に、OCR ライブラリをプロジェクトに導入します。ソリューションフォルダでターミナルを開き、以下を実行してください。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

これにより **OcrDemo** という新しいコンソールプロジェクトが作成され、`Aspose.OCR` NuGet パッケージが追加されます。このライブラリには、使用する `OcrEngine` クラスが含まれています。

> **プロのコツ:** 専用 GPU を搭載したマシンを使用している場合は、最新のグラフィックドライバがインストールされていることを確認してください。そうでなければ、ライブラリは自動的に CPU モードにフォールバックします。

## 手順 2: 完全な OCR コードを書く

次に `Program.cs` を開き、その内容を以下に置き換えてください。すべての行にコメントが付いているので、*なぜ* そのように書いているかが分かります。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### これが機能する理由

- **ProcessingMode = Gpu** はエンジンにまず GPU を試すよう指示します。ライブラリは低レベルの CUDA/OpenCL 呼び出しを抽象化しているため、デバイスコンテキストを自分で管理する必要はありません。  
- **IsGpuEnabled** は GPU パスが成功したかどうかを示すブール値です。`false` が表示された場合、エンジンは自動的に CPU にフォールバックしています—慌てる必要はありません。  
- **RecognizeImage** はすべての重い処理を行います：画像を読み込み、OCR モデルを実行し、プレーンテキストの結果を返します。特別な要件（例：デスキュー）がない限り、ビットマップを手動で前処理する必要はありません。

## 手順 3: アプリケーションを実行し、出力を確認する

コンパイルして実行：

```bash
dotnet run
```

すべてが正しく設定されていれば、以下のような出力が表示されます：

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

GPU が利用できない場合、最初の行は `GPU used: False` と表示されますが、抽出されたテキストは依然として表示されます—優雅なフォールバックのおかげです。

> **よくある質問:** *画像が TIFF ではなく JPEG の場合はどうすればいいですか？*  
> `RecognizeImage` メソッドは .NET の `System.Drawing` がサポートする任意の形式（JPEG、PNG、BMP など）を受け付けます。`imagePath` の拡張子を変更するだけです。

## 手順 4: オプション – 精度向上のために設定を調整する

Aspose.OCR には調整できる設定がいくつか用意されています：

| Setting | What it Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Language` | 特定の言語を強制します（例：`OcrLanguage.English`） | 文書の言語が分かっている場合 |
| `ocrEngine.PageSegMode` | エンジンがページをブロックに分割する方法を制御します | 複数列レイアウトの場合 |
| `ocrEngine.DetectOrientation` | 正しくない向きのテキストを自動回転させます | 逆さまにスキャンされた可能性がある場合 |

`RecognizeImage` を呼び出す前にこれらのプロパティを設定できます。例：

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## 手順 5: フローを可視化する（代替テキスト付き画像）

以下は、オプションの GPU 加速を伴う **OCRの使い方** を示すシンプルな図です。コードの実行に必須ではありませんが、全体像を把握するのに役立ちます。

![GPU処理を伴うOCRの使い方を示す図](/images/ocr-gpu-flow.png)

*代替テキスト:* *GPU処理を伴うOCRの使い方を示す図で、必要に応じてCPUにフォールバックすることがハイライトされています。*

## エッジケースとトラブルシューティング

1. **Out‑of‑Memory on GPU** – 非常に大きな画像は GPU メモリを超える可能性があります。その場合、ライブラリは自動的に CPU に切り替わります。メモリ使用量を抑えるために画像を事前に縮小できます。  
2. **Unsupported Image Format** – `RecognizeImage` が *NotSupportedException* をスローした場合、ファイル拡張子を確認し、画像が破損していないか確認してください。PNG に変換すると解決することが多いです。  
3. **Low Confidence Scores** – OCR 結果に読めない文字が多数含まれる場合、前処理（二値化、ノイズ除去）を検討するか、より高解像度のスキャンに切り替えてください。  

## まとめ: 達成したこと

今回のチュートリアルでは、C# コンソールアプリで **OCRの使い方** を取り上げ、**画像からテキストを抽出する方法** を実演し、**GPU処理を有効に** して高速化する方法を示しました。これで **スキャンをテキストに変換** する方法、GPU が実際に使用されたかどうかの確認方法、エッジケースシナリオ向けにいくつかの設定を調整する方法が分かります。

### 次のステップ

- 出力を **検索インデックス**（例：Elasticsearch）に投入し、スキャンした PDF を検索可能にしてみましょう。  
- **バッチ処理** を試してみてください—画像フォルダをループし、各結果を `.txt` ファイルに書き出します。  
- OCR と **翻訳 API** を組み合わせて、スキャンした外国語文書を自動的に翻訳します。  

質問があればコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}