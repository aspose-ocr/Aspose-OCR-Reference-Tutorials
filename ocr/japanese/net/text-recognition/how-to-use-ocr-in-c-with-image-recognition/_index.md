---
category: general
date: 2026-11-20
description: C#でOCRを使用して画像からテキストを認識する方法。画像OCRの読み込み、OCR言語の設定、JPEGファイルからのテキスト抽出を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: ja
lastmod: 2026-11-20
og_description: C#でOCRを使用して画像からテキストを抽出する方法。このガイドでは、画像の読み込み、OCR言語の設定、JPEGファイルからのテキスト認識を示します。
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: C#でOCRを使用する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: C#で画像認識を利用したOCRの使い方
url: /ja/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用して画像認識を行う方法

C# アプリケーションで **OCR の使い方** が必要な場合、このガイドは全工程を案内します。スキャンした契約書をデジタル化する場合でも、写真から情報を抽出する場合でも、**テキスト画像** ファイルを迅速かつ確実に **認識** する方法を学べます。

このチュートリアルでは画像の読み込み、OCR エンジンの設定、JPEG ファイルから認識されたテキストの取得について解説します。最後までで、任意の .NET プロジェクトに組み込める自己完結型の実行可能サンプルが手に入ります。

## 前提条件

* .NET 6.0（またはそれ以降）がインストールされていること。
* `OcrEngine`、`ImageStream`、言語モジュールを提供する OCR ライブラリへのアクセス（例: **Leadtools**、**Aspose.OCR**、または互換パッケージ）。
* 既知のディレクトリに `sample.jpg` という名前のサンプル画像があること。

追加の外部サービスは不要です。OCR エンジンが不足している言語パックを自動的にダウンロードします。

## 手順 1: OCR 用に画像を読み込む

画像の読み込みはすべての OCR ワークフローの最初のステップです。以下のコードはディスク上の JPEG ファイルから `ImageStream` を作成します。

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*Why this matters:* `ImageStream` オブジェクトはファイル処理を抽象化し、OCR エンジンが使用するピクセルデータを提供します。ファイルが見つからない場合、`FromFile` は明確な例外をスローし、デバッグが容易になります。

## 手順 2: OCR エンジンインスタンスを作成する（自動解放）

`using` ブロックを使用することで、OCR の処理が完了した時点でアンマネージドリソースが確実に解放されます。

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*Pro tip:* `using` 文は手動の `Dispose()` 呼び出しより推奨されます。ネイティブメモリの解放忘れによる長時間稼働サービスでのメモリリークを防げます。

## 手順 3: OCR 言語を設定する（任意だが推奨）

元文書の言語が分かっている場合、設定することで精度が向上し、処理速度も速くなります。例では言語をキリル文字に設定していますが、任意のサポートされている言語列挙体に置き換えられます。

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*Why set the language?* OCR エンジンは言語固有の文字モデルを持っています。正しいものを選択することで、誤検出を減らし、不要な文字置換を防げます。

## 手順 4: 読み込んだ画像で OCR を実行する

これでエンジンがビットマップを処理し、認識されたテキストを文字列として返します。

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*Edge case:* 画像が低解像度または高圧縮の場合、エンジンは部分的な結果を返すことがあります。より良い結果を得るために前処理（例: 二値化）を検討してください。

## 手順 5: 認識されたテキストを出力する

最後に、抽出したテキストをコンソールに表示するか、別のコンポーネントへ渡します。

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**期待される出力**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

正確な内容は元画像に依存しますが、コンソールには OCR エンジンが検出した全文が表示されます。

## 完全な実行可能サンプル

すべての手順を組み合わせると、すぐにコンパイルして実行できるコンパクトなプログラムが得られます。

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

コードを新しいコンソールプロジェクトに貼り付け、`YOUR_DIRECTORY` を画像へのパスに置き換えて `dotnet run` を実行してください。プログラムは認識されたテキストをコンソールに出力します。

## よくある質問とトラブルシューティング

| Question | Answer |
|----------|--------|
| **言語パックがダウンロードされていない場合はどうしますか？** | OCR ライブラリは自動的に取得しようとします。マシンがインターネットに接続されていることを確認するか、ライブラリのドキュメントに従って言語パックを事前にインストールしてください。 |
| **PNG や BMP ファイルからテキストを認識できますか？** | はい。`ImageStream.FromFile` は基盤となる画像ライブラリがサポートする任意の形式で動作します。ファイル拡張子を変更するだけです。 |
| **ノイズの多いスキャンで精度を向上させるには？** | `Recognize` に渡す前に画像を前処理（コントラスト調整、ノイズ除去）してください。多くのライブラリはこの目的のために `ImageProcessor` クラスを提供しています。 |
| **ユーザーがアップロードしたファイルで OCR を実行しても安全ですか？** | ファイルサイズとタイプを検証し、サンドボックス化された環境で OCR を実行して悪意あるペイロードを防止してください。 |

## 結論

これで C# で **OCR の使い方** を理解し、**テキスト画像** ファイルを **認識** し、**画像 OCR を読み込む**、**OCR 言語を設定する**、そして **JPEG のテキストを認識** する方法を確実に実装できます。完全なサンプルは、クリーンで使い捨て可能なワークフローを示しており、追加の前処理や多言語サポート、あるいは大規模な文書処理パイプラインへの統合に拡張できます。

### 次のステップ

* JPEG ディレクトリをループしてバッチ処理を検討する。  
* OCR と自然言語処理 (NLP) を組み合わせて構造化データを抽出する。  
* `OcrLanguage.English` や `OcrLanguage.Arabic` など、他の言語モジュールを試す。  

コードをご自身のユースケースに合わせて自由に調整し、楽しいコーディングを！

## 次に学ぶべきことは？

以下のチュートリアルは本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説とともに完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C# で Windows.Media.Ocr を使用してテキスト画像を認識する – 完全 OCR ガイド](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [C# で OCR を使用する方法 – 画像からテキストを非同期で抽出](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [C# で OCR を使用する方法 – Aspose OCR で画像からテキストを抽出](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}