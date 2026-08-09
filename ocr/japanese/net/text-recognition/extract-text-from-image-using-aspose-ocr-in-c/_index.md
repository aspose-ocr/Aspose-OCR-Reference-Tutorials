---
category: general
date: 2026-08-09
description: C# で Aspose OCR を使用して画像からテキストを抽出する。OCR 用に画像を読み込む方法、OCR 言語を設定する方法、画像の
  OCR を実行する方法、そして画像を効率的にテキストに変換する方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: ja
lastmod: 2026-08-09
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、OCR用に画像を読み込む方法、OCR言語を設定する方法、画像のOCRを処理する方法、そして数行のコードで画像をテキストに変換する方法を示します。
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Aspose OCRで画像からテキストを抽出する – C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でAspose OCRを使用して画像からテキストを抽出する
url: /ja/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使用して画像からテキストを抽出する

.NET アプリケーションで **画像からテキストを抽出** する必要がある場合、このガイドでは完全で実行可能なソリューションをステップバイステップで紹介します。**OCR 用に画像をロード** し、適切な言語モジュールを選択し、OCR エンジンを実行し、最後に数行の C# で **画像をテキストに変換** する方法が分かります。

このチュートリアルでは、Aspose.OCR で信頼できる結果を得るために必要なすべてをカバーします。サポートされていない画像形式や言語固有のニュアンスといった一般的な落とし穴も含まれます。最後まで読むと、認識されたテキストをコンソールに出力する自己完結型プログラムが手に入ります。

## 期待できる成果

* Aspose OCR エンジンに画像ファイルをロードする。  
* **OCR 言語を設定**（例ではキリル文字ですが、サポートされている任意の言語が使用可能）。  
* **画像 OCR を処理**し、テキスト表現を取得する。  
* **画像をテキストに変換**し、表示する。これにより、さらなる処理や保存が可能になる。  

**前提条件**

* .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）。  
* Visual Studio 2022（または C# をサポートする任意の IDE）。  
* Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）。  

---

## 画像からテキストを抽出 – 完全コード解説

以下は完全な実行可能プログラムです。新しいコンソールプロジェクトにコピーし、`YOUR_DIRECTORY/sample_cyrillic.jpg` をご自身の画像へのパスに置き換えてください。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### 各ステップの重要性

1. **OCR エンジン インスタンスを作成** – `OcrEngine` はすべての OCR 機能をカプセル化します。速やかに破棄することでネイティブリソースが解放され、長時間稼働するサービスにとって重要です。  
2. **OCR 言語を設定** – 正しい言語モジュールを選択すると精度が大幅に向上します。Aspose は 30 以上の言語パックを提供しており、デフォルトは英語です。例ではキリル文字を使用し、ラテン文字以外のスクリプトを示しています。  
3. **OCR 用に画像をロード** – エンジンは `ImageStream` と連携します。高解像度画像（≥300 dpi）を提供すると、特に複雑なスクリプトでの誤認識が減少します。  
4. **画像 OCR を処理** – ここで本格的な処理が行われます。このメソッドは抽出されたテキスト、信頼度スコア、オプションのレイアウトデータを含む `OcrResult` を返します。  
5. **画像をテキストに変換** – `result.Text` は単純な `string` です。ファイルに書き出したり、検索インデックスに投入したり、下流の NLP パイプラインに渡したりできます。  

---

## OCR 用に画像をロード

`ImageStream.FromFile` メソッドは一般的なラスタ形式をサポートします。画像がバイト配列（例：Web API から）として受け取られる場合は、代わりに `ImageStream.FromBytes(byte[])` を使用してください：

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**プロのコツ:** エンジンに渡す前に画像が破損していないか必ず確認してください。簡単な `try { Image.FromFile(...); } catch { ... }` ガードで実行時例外を防げます。

---

## OCR 言語を設定

Aspose.OCR にはランタイムで有効化できる言語パックが同梱されています。利用可能なすべての言語を一覧表示するには次のようにします。

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

同一文書で複数言語を認識する必要がある場合は、ビット単位の OR 演算子で組み合わせます：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**エッジケース:** 右から左へ（RTL）書く言語（例：アラビア語）と左から右へ書くスクリプトを混在させる場合、追加のレイアウト処理が必要になることがあります。Aspose は自動的に方向を検出しますが、`engine.PageSegmentationMode` で微調整できます。

---

## 画像 OCR を処理

`Process` 呼び出しは同期的で、エンジンが完了するまでブロックします。大量バッチや UI アプリケーションの場合は、非同期オーバーロードの使用を検討してください：

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**一般的な落とし穴:** `Process` を呼び出す前に `engine.Image` を設定し忘れると `InvalidOperationException` がスローされます。必ず先に画像を割り当ててください。

---

## 画像をテキストに変換

抽出された文字列は他の .NET `string` と同様に操作できます。例として、出力をファイルに書き込む方法は以下の通りです。

```csharp
File.WriteAllText("output.txt", result.Text);
```

画像中の改行をそのまま保持したい場合は `result.Text` を直接使用します。後処理（例：余分な空白の除去）には標準の文字列メソッドを適用してください。

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## 完全な例のまとめ

すべてを組み合わせると、プログラムは次のようになります：

1. `OcrEngine` をインスタンス化する。  
2. **OCR 言語を設定** してキリル文字（または選択した任意の言語）にする。  
3. **OCR 用に画像をロード** してディスクから読み込む。  
4. **画像 OCR を処理** してテキスト結果を取得する。  
5. **画像をテキストに変換** し、コンソールに出力する。  

鮮明なキリル文字画像でサンプルを実行すると、以下のような出力が得られます：

```
=== Recognized Text ===
Пример текста на кириллице
```

画像に英語テキストが含まれる場合は、`engine.Language = OcrLanguage.English;` に変更すれば、同じコードで **画像からテキストを抽出** できます。

---

## 結論

これで C# で Aspose OCR を使用して **画像からテキストを抽出** する方法が分かりました。チュートリアルでは画像のロード、適切な言語の選択、OCR プロセスの実行、そして下流での利用のために **画像をテキストに変換** する手順をカバーしました。  
ここからは次のことができます：

* 他の言語で実験する（`load image for OCR` → `set OCR language` → `process image OCR`）。  
* OCR ステップをより大きなパイプラインに統合する（例：文書取り込み、検索可能な PDF）。  
* 画像をバッチ処理したり非同期 API を使用したりしてパフォーマンスを最適化する。  

カスタム辞書、ページ分割モード、OCR 精度調整などの高度な機能については、Aspose.OCR のドキュメントをぜひご覧ください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [画像からテキスト抽出 – .NET 用 Aspose.OCR の OCR 最適化](/ocr/english/net/ocr-optimization/)
- [Aspose OCR を使用したストリームからの画像テキスト抽出方法](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}