---
category: general
date: 2026-10-11
description: Aspose.OCR を使用して C# で画像の OCR を実行する方法を学びます。System.Drawing.Common のインストールや
  JPG ファイルからのテキスト抽出も含まれます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: ja
lastmod: 2026-10-11
og_description: Aspose.OCR を使用して C# で画像の OCR を実行します。このガイドでは、System.Drawing.Common
  のインストール方法、OCR 用に画像を読み込む方法、JPG からテキストを抽出する方法を示します。
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: C#で画像のOCRを実行する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: C#でAspose.OCRを使用して画像のOCRを実行する方法
url: /ja/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.OCR を使用して画像の OCR を実行する方法

.NET アプリケーションで画像ファイルの **perform OCR on image** を行う必要がある場合、このガイドでは完全なソリューションを示します。Aspose.OCR を使用すると、JPG などの **recognize text from picture** ファイルからテキストをすばやく認識し、コンソールウィンドウに結果を表示できます。

以下を学びます:

* **install System.Drawing.Common package** – `Image` クラスを提供するライブラリ、  
* **load image for OCR** – JPEG または PNG をメモリに読み込む、  
* 言語モデルを構成する、  
* **perform OCR on image** を実行し、最後に、  
* **extract text from JPG** を抽出して出力する。

手順は .NET 6+ 用に記述されていますが、.NET Framework 4.6.1 以降でも動作します。

---

## 前提条件

| 要件 | 重要な理由 |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | C# コンソールアプリのランタイムを提供します。 |
| Visual Studio 2022 (or any IDE) | NuGet パッケージの追加やプログラムの実行が簡単になります。 |
| Internet connection (first run only) | Aspose.OCR が言語モジュールを自動的にダウンロードします。 |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | **extract text from JPG** をデモンストレーションするために使用します。 |

---

## 手順 1: Install System.Drawing.Common パッケージのインストール

`System.Drawing.Common` NuGet パッケージは、**load image for OCR** に使用する `Image` クラスを提供します。Package Manager Console を開き、次のコマンドを実行します：

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Linux/macOS でプラットフォーム固有の警告が出た場合は、`net6.0-windows` をターゲットにするか、プロジェクトファイルに `<UseWindowsForms>true</UseWindowsForms>` を追加してください。

---

## 手順 2: Aspose.OCR NuGet パッケージの追加

Aspose.OCR には OCR エンジンと語彙モデルが含まれています。以下のコマンドでインストールします：

```powershell
Install-Package Aspose.OCR
```

このパッケージは軽量で、必要な言語データ（例: Cyrillic）は `OcrEngine.Language` を初めて設定したときにダウンロードされます。

---

## 手順 3: OCR 用に画像をロードする方法

画像をロードすることは、**perform OCR on image** を行う前の最初の具体的なステップです。`Image.FromFile` メソッドは、JPG、PNG、BMP、TIFF など GDI+ がサポートするすべての形式を読み取ります。

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*ファイルが存在しない場合、`FileNotFoundException` がスローされます – 本番コードでは try/catch ブロックで呼び出しをラップしてください。*

---

## 手順 4: エンジンの構成と **perform OCR on image** の実行

`OcrEngine` インスタンスを作成し、言語モデルを選択し、ロードした画像を割り当て、`Recognize()` を呼び出します。

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` メソッドは、抽出されたテキスト、信頼度スコア、バウンディングボックスを保持する `OcrResult` オブジェクトを返します。言語モジュールは初回使用時に自動的にダウンロードされるため、追加のファイルは不要です。

---

## 手順 5: **Extract text from JPG** の抽出と表示

これで **recognize text from picture** が可能になり、結果を出力できます。`OcrResult` の `Text` プロパティにはプレーン文字列が含まれています。

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### 期待されるコンソール出力

```
Recognized text:
Пример текста на кириллице
```

ソース画像に英語テキストが含まれている場合、出力は画像内に配置した英語の文になります。

---

## エッジケースとベストプラクティスのヒント

| 状況 | 推奨事項 |
|-----------|----------------|
| **Large images ( > 5 MB )** | OCR 前に画像の長辺を ≤ 2000 px にリサイズして、メモリ使用量を減らし速度を向上させます。 |
| **Multiple languages in one picture** | `ocrEngine.AddLanguage(OcrLanguage.English)` を Cyrillic に加えて呼び出し、`ocrEngine.Language = OcrLanguage.Multilingual` を設定します。 |
| **Low‑contrast scans** | ビットマップをエンジンに渡す前に `System.Drawing.Graphics` でコントラストを上げます。 |
| **Running on Linux/macOS** | `libgdiplus` のネイティブ依存関係がインストールされていることを確認します（`sudo apt-get install -y libgdiplus`）。 |
| **Repeated OCR calls** | 同じ `OcrEngine` インスタンスを再利用し、`ocrEngine.Image` だけを差し替えてモジュールの再読み込みを防ぎます。 |

---

## 完全な実行可能プログラム

以下は、これまでのすべての手順を組み込んだ完全なコンソールアプリケーションです。コードを新しい C# コンソールプロジェクトにコピーし、画像パスを置き換えて実行してください。

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** は認識された文字列をコンソールに出力し、**performed OCR on image** と **extract text from JPG** に成功したことを確認します。

---

## 結論

これで、C# で Aspose.OCR を使用して **perform OCR on image** ファイルを処理する方法が分かりました。必要な **System.Drawing.Common package** のインストールから **load image for OCR**、適切な言語の選択、最終的な **extract text from JPG** までを網羅しています。このエンドツーエンドの例は、画像フォルダーのバッチ処理や OCR を Web API に統合するなど、より高度なドキュメント処理パイプラインを構築するための確固たる基盤を提供します。

### 次にやることは？

- PDF で **recognize text from picture** を試すには、まず各ページを画像に変換します。  
- `OcrEngine` のプロパティ `Resolution`、`Threshold`、`MaxProcessingTime` を実験的に調整し、ノイズの多いスキャンの精度を微調整します。  
- OCR の出力を自然言語処理ライブラリと組み合わせて、抽出されたコンテンツを自動的に分類します。

他の画像形式に合わせてコードを適応したり、エラーハンドリングを追加したり、より大きなアプリケーションに統合したりして構いません。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}