---
category: general
date: 2026-07-18
description: C#でAspose OCRを使用してPNGからテキストを抽出します。画像をテキストに変換し、画像上でOCRを実行してキリル文字テキストを迅速に認識する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from png
- convert image to text
- perform ocr on image
- recognize cyrillic text
- ocr cyrillic image
language: ja
lastmod: 2026-07-18
og_description: Aspose OCRでPNGからテキストを抽出します。このガイドでは、画像をテキストに変換し、画像上でOCRを実行し、C#の数行でキリル文字テキストを認識する方法を示します。
og_image_alt: Screenshot showing C# console output after extracting text from a PNG
  image
og_title: Aspose OCRでPNGからテキストを抽出 – 完全C#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  headline: Extract Text from PNG with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  name: Extract Text from PNG with Aspose OCR – Complete C# Guide
  steps:
  - name: Why Each Piece Matters
    text: '* **`var ocrEngine = new OcrEngine();`** – This creates the engine object
      that holds all OCR settings. Think of it as the “brain” that will analyze the
      pixels. * **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – By explicitly setting
      the language, you tell the engine which character set to expect. '
  - name: 4.1 Dealing with Low‑Resolution PNGs
    text: 'OCR accuracy drops when the source image is under 300 dpi. You can pre‑process
      the image using `System.Drawing` or `ImageSharp` to upscale it:'
  - name: 4.2 Recognizing Multiple Languages
    text: 'If you need to **perform OCR on image** files that contain both Latin and
      Cyrillic characters, set a composite language:'
  - name: 4.3 Saving the Result to a File
    text: 'Instead of printing to the console, you might want a persistent text file:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Aspose OCRでPNGからテキストを抽出する – 完全なC#ガイド
url: /ja/net/text-recognition/extract-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した PNG からのテキスト抽出 – 完全 C# ガイド

PNG から **テキストを抽出** したいと思ったことはありますか、しかし、Cyrillic（キリル文字）をすぐに扱えるライブラリがどれか分からなかった…？ あなただけではありません。多くのプロジェクト—例えば自動レシート処理や多言語文書アーカイブ—では、**画像をテキストに変換** できることが日常的な課題です。  

良いニュースです。Aspose.OCR を使えば、数行のコードで **画像に対して OCR を実行** でき、必要な言語モジュールは自動的にダウンロードされます。以下では、PNG で **Cyrillic テキストを認識** し、さらに処理できるクリーンな文字列を取得する方法を示します。

## このチュートリアルでカバーする内容

必要な手順をすべて解説します：

* Aspose.OCR NuGet パッケージのインストール  
* C# で OCR エンジンを初期化  
* **Cyrillic** 言語モデルの選択（**Cyrillic テキストを認識** できるように）  
* PNG ファイルをエンジンに渡し、**画像に対して OCR を自動実行** させる  
* 結果をコンソールまたはファイルに出力  

外部ツールや手動での言語ファイルのダウンロードは不要です—任意の .NET プロジェクトに貼り付けられる純粋な C# コードだけです。

---

![OCR ワークフローの図 – PNG からテキストを抽出](/images/ocr-workflow.png "Aspose OCR を使用して PNG 画像が処理されテキストに変換される様子を示す図")

*Image alt text: “Aspose OCR を使用して C# で PNG からテキストを抽出するプロセスを示す図”。*

## 前提条件

始める前に、以下が揃っていることを確認してください：

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 SDK or later (the code also works on .NET Framework 4.7.2+) | 最新のランタイムは最新の言語機能を提供します。 |
| Visual Studio 2022 (or any editor you prefer) | NuGet パッケージの追加やコンソール アプリの実行が簡単になります。 |
| A PNG image that contains Cyrillic characters (e.g., `sample_cyrillic.png`) | OCR エンジンに渡すファイルです。 |
| Internet connection (the first run will download the Cyrillic language module) | Aspose.OCR は必要に応じて言語パックを取得します。 |

以上です—追加の DLL や外部サービスは不要です。準備はいいですか？始めましょう。

## ステップ 1: NuGet で Aspose.OCR をインストール

整理のために、新しいコンソール プロジェクトを作成し、OCR ライブラリを追加します。

```bash
dotnet new console -n OcrCyrillicDemo
cd OcrCyrillicDemo
dotnet add package Aspose.OCR
```

`dotnet add package` コマンドを実行すると、NuGet から Aspose.OCR の最新安定版が取得されます。これにはコア OCR エンジンが含まれますが、言語パックは **含まれません**。言語を設定すると自動的に取得されます。

> **プロのコツ:** .NET Framework を対象にする場合は、Visual Studio の NuGet パッケージ マネージャーを開き “Aspose.OCR” を検索してください。同じパッケージがすべてのランタイムで動作します。

## ステップ 2: 最小限の C# プログラムを作成

`Program.cs` を開き、以下の完全なサンプルに内容を置き換えます。このスニペットはすべてを行います：エンジンの初期化、Cyrillic モデルの選択、PNG の読み込み、認識されたテキストの出力。

```csharp
using System;
using Aspose.OCR;

namespace OcrCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------------------------------------------------------
            // Step 2.1: Instantiate the OCR engine – the heart of the process
            // ---------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------
            // Step 2.2: Choose the Cyrillic language model.
            // Aspose will download the necessary module on first use.
            // ---------------------------------------------------------
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // ---------------------------------------------------------
            // Step 2.3: Define the path to the PNG you want to convert.
            // You can also accept this as a command‑line argument.
            // ---------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";

            // ---------------------------------------------------------
            // Step 2.4: Perform OCR on the image.
            // RecognizeImage returns a string with the extracted text.
            // ---------------------------------------------------------
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // ---------------------------------------------------------
            // Step 2.5: Output the result – you could write to a file instead.
            // ---------------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 各要素が重要な理由

* **`var ocrEngine = new OcrEngine();`** – すべての OCR 設定を保持するエンジン オブジェクトを作成します。ピクセルを解析する “脳” と考えてください。  
* **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – 言語を明示的に設定することで、エンジンに期待する文字セットを指示します。これにより Cyrillic スクリプトの精度が大幅に向上し、言語パックの自動ダウンロードがトリガーされます（手動操作は不要）。  
* **`RecognizeImage(imagePath)`** – このメソッドは PNG ファイルを読み込み、OCR アルゴリズムを実行し、プレーンテキスト文字列を返します。これはコアな **画像をテキストに変換** 操作です。  
* **`Console.WriteLine`** – 抽出が成功したかを確認するシンプルな方法です。実際のアプリでは文字列をデータベースに保存したり、翻訳サービスに渡したりすることが多いでしょう。  

## ステップ 3: アプリケーションを実行

ターミナルから以下を実行します：

```bash
dotnet run
```

最初の実行時には、Aspose が Cyrillic 言語モジュールをダウンロードしている間、短いプログレスバーが表示されます（通常数 MB）。その後、次のような出力が表示されます：

```
=== Extracted Text ===
Пример текста на кириллице.
```

出力が文字化けしている場合は、画像に明瞭な Cyrillic 文字が含まれているか、ファイルパスが正しいかを再確認してください。

## ステップ 4: 一般的なエッジケースの処理

### 4.1 低解像度 PNG の対処

ソース画像が 300 dpi 未満の場合、OCR の精度が低下します。`System.Drawing` や `ImageSharp` を使用して画像を前処理し、拡大することができます：

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;

// Load, upscale, and save a temporary higher‑resolution copy.
using (var original = new Bitmap(imagePath))
{
    var upscale = new Bitmap(original.Width * 2, original.Height * 2);
    using (var g = Graphics.FromImage(upscale))
    {
        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
        g.DrawImage(original, 0, 0, upscale.Width, upscale.Height);
    }
    upscale.Save("temp_upscaled.png", ImageFormat.Png);
    recognizedText = ocrEngine.RecognizeImage("temp_upscaled.png");
}
```

### 4.2 複数言語の認識

Latin と Cyrillic の両方の文字が含まれる **画像に対して OCR を実行** する必要がある場合は、複合言語を設定します：

```csharp
ocrEngine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

エンジンは各スクリプトを自動的に検出しようとします。

### 4.3 結果をファイルに保存

コンソールに出力する代わりに、永続的なテキストファイルが欲しい場合は次のようにします：

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognizedText);
Console.WriteLine("Text saved to extracted_text.txt");
```

## ステップ 5: 本番環境向け OCR のヒント

* **言語モジュールをキャッシュ** – 最初のダウンロード後、ファイルはユーザーの一時フォルダーに保存されます。サーバー環境では、永続的な場所にコピーし、`OcrEngine.LanguageFolder` をその場所に設定してください。  
* **`ocrEngine.Config` を設定** – スキャン文書の精度向上のために、ノイズ除去、二値化、回転検出などを調整できます。  
* **バッチ処理** – `foreach` ループで認識呼び出しをラップし、数十枚の PNG を処理します。同じ `OcrEngine` インスタンスを再利用して、モジュールの再読み込みを防ぐことを忘れないでください。  

---

## 結論

これで、Aspose OCR を使用して C# で PNG ファイルから **テキストを抽出** する動作するエンドツーエンドの例が手に入りました。上記の手順に従うことで、**画像をテキストに変換**、**画像に対して OCR を実行**、そして確実に **Cyrillic テキストを認識** でき、ライブラリが言語モジュールを管理してくれます。  

ここからは、ソリューションを拡張することを検討してください：PDF 出力の追加、サーバーレス処理のための Azure Functions との統合、または再利用可能なクラス ライブラリとしてコードをパッケージ化するなど。可能性は遭遇するスクリプトと同様に広がります。  

他の文字体系の扱い、パフォーマンス調整、UI との統合について質問がありますか？コメントを残してください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースは、ステップバイステップの解説と完全な動作コード例を含み、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [画像をテキストに変換 – URL から画像に対して OCR を実行](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}