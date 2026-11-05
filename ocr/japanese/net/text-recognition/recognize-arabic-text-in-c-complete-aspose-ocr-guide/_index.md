---
category: general
date: 2026-06-19
description: C# で Aspose.OCR を使用して画像からアラビア語テキストを認識します。画像からテキストを抽出し、アラビア語の OCR 画像を処理し、右から左へのテキストを効率的に読み取る方法を学びます。
draft: false
keywords:
- recognize arabic text
- extract text from image
- ocr arabic image
- read right-to-left text
language: ja
og_description: C#で画像からアラビア語テキストを認識します。このガイドでは、画像からテキストを抽出し、OCRでアラビア語画像を処理し、右から左へ読むテキストを扱う方法を示します。
og_title: C#でアラビア語テキストを認識 – Aspose.OCRステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize Arabic text from images in C# using Aspose.OCR. Learn to
    extract text from image, handle OCR Arabic image, and read right-to-left text
    efficiently.
  headline: Recognize Arabic Text in C# – Complete Aspose.OCR Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- Arabic
title: C#でアラビア文字を認識する – 完全なAspose.OCRガイド
url: /ja/net/text-recognition/recognize-arabic-text-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でアラビア文字を認識する – 完全な Aspose.OCR ガイド

写真の中のアラビア文字を手動で入力せずに **認識** できるか、考えたことはありませんか？ あなただけではありません—請求書スキャナーや多言語チャットボット、アーカイブツールを構築する開発者は常にこの壁に直面しています。 良いニュースは、Aspose.OCR を使えば数行のコードで **画像からテキストを抽出** でき、ライブラリは右から左 (RTL) の特殊処理も自動で行ってくれます。

このチュートリアルでは、実際の例を通して **ocr arabic image** ファイルの処理方法、Unicode の順序を保持する方法、そして最終的にコンソールアプリで **右から左のテキストを読む** 方法を解説します。最後まで読むと、任意の .NET プロジェクトに組み込める実行可能なプログラムが手に入ります。

## 前提条件 – 開始前に必要なもの

- **.NET 6.0 以降**（コードは .NET Framework 4.7+ でも動作します）
- **Aspose.OCR for .NET** NuGet パッケージ（`Aspose.OCR`）
- アラビア語またはウルドゥー語の文字を含むサンプル画像（例：`arabic_invoice.png`）
- 開発環境（Visual Studio、Rider、または VS Code）

まだ NuGet パッケージを追加していない場合は、プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

以上です—ネイティブ DLL や外部バイナリは不要です。Aspose がすべてを処理し、アラビア語用言語パックの自動リソースダウンロードも行います。

## 手順 1: アラビア語（およびウルドゥー語）用に OCR エンジンを設定 – 基本設定

最初に行うべきことは、OCR エンジンに期待する言語を指定することです。アラビア語は **右から左** のスクリプトで、ライブラリにはウルドゥー語文字もカバーする専用の言語モデルが同梱されています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Step 1: Set up OCR configuration for Arabic
var ocrConfig = new OcrEngineConfig
{
    Language = Language.Arabic,          // Enables Arabic & Urdu support
    AutoDownloadResources = true        // Downloads language data on first run
};
```

> **なぜ重要か:**  
> `Language.Arabic` を明示的に設定することで、エンジンは正しい文字セットとレイアウト規則を適用します。`AutoDownloadResources` フラグにより、サーバーに言語ファイルを手動で配置する手間が省け、コードを初めて実行したときに Aspose が自動で取得します。

## 手順 2: 設定を使用して OCR エンジンをインスタンス化

設定オブジェクトの準備ができたら、実際の OCR エンジンを作成します。`using` ステートメントを使用することで、アンマネージドリソースの適切な破棄が保証されます。

```csharp
// Step 2: Create the OCR engine with the Arabic configuration
using var ocrEngine = new OcrEngine(ocrConfig);
```

> **プロのコツ:**  
> バッチで多数の画像を処理する場合、画像ごとに再作成するのではなく、バッチ全体で `OcrEngine` を保持してください。これによりオーバーヘッドが減り、処理速度が向上します。

## 手順 3: 右から左の画像からテキストを認識

エンジンが用意できたら、`RecognizeImage` を呼び出し、対象ファイルを指定します。このメソッドは認識された Unicode 文字列を含む `OcrResult` オブジェクトを返します。

```csharp
// Step 3: Perform OCR on an Arabic image file
var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/arabic_invoice.png");
```

> **エッジケースの注意:**  
> 画像パスが間違っている、またはファイルにアクセスできない場合、`RecognizeImage` は例外をスローします。本番コードでは `try/catch` ブロックで呼び出しをラップしてください。

## 手順 4: 認識された Unicode テキストを出力 – RTL 方向を保持

最後に、抽出したテキストをコンソール（または他の出力先）に書き込みます。OCR エンジンはすでに正しい論理順序でテキストを返すため、追加の文字列操作は不要です。

```csharp
// Step 4: Print the recognized text – RTL direction is preserved
System.Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、次のような表示が出るはずです：

```
فاتورة رقم 12345
التاريخ: 01/09/2023
المبلغ: ٥٠٠٠ ريال
```

これが求めていた **右から左のテキストの読み取り** です—追加のレイアウト処理は不要です。

### 完全な動作例

以下は、コピーして新しいコンソールプロジェクトに貼り付けられる、完全で自己完結型のプログラムです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

class RtlDemo
{
    static void Main()
    {
        // Configure OCR for Arabic (includes Urdu) and enable auto‑download
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.Arabic,
            AutoDownloadResources = true
        };

        // Create OCR engine with the configuration
        using var ocrEngine = new OcrEngine(ocrConfig);

        // Recognize text from the Arabic image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/arabic_invoice.png");

        // Output the recognized Unicode text (preserves RTL direction)
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **期待される出力:** コンソールは、元画像に表示されている通りのアラビア語テキストを、数字・句読点・改行を保持したまま出力します。

## PNG 以外の画像ファイルからテキストを抽出する方法

Aspose.OCR は PNG に限定されません。JPEG、BMP、TIFF、あるいは PDF ページも直接入力できます：

```csharp
// Recognize a JPEG image
var jpegResult = ocrEngine.RecognizeImage("sample.jpg");

// Recognize a TIFF (multi‑page) – choose the first page
var tiffResult = ocrEngine.RecognizeImage("multi_page.tiff", pageIndex: 0);
```

**画像からテキストを抽出** するストリームが必要な場合（例：Web API でのアップロード時）、`byte[]` または `Stream` を受け取るオーバーロードを使用してください：

```csharp
using var stream = File.OpenRead("upload.png");
var streamResult = ocrEngine.RecognizeImage(stream);
```

## OCR アラビア語画像ファイルを扱う際の一般的な落とし穴

| 問題 | 発生理由 | 簡単な対策 |
|-------|----------------|-----------|
| 文字化け | 画像解像度が低い、または圧縮アーティファクトがあるため | より高解像度のソースを使用する（≥300 dpi） |
| ダイアクリティックが欠落 | 言語モデルがロードされていないため | `AutoDownloadResources = true` を設定するか、リソースフォルダーにアラビア語モデルを手動で配置してください |
| テキストが左から右に表示される | UI の出力レンダリングが LTR を強制しているため | Unicode 対応コントロール（`RichTextBox`、Unity の `TextMeshPro` など）を使用するか、WPF/WinForms で `FlowDirection = RightToLeft` を設定してください |
| 初回実行が遅い | 言語パックのダウンロードが原因 | インターネット接続があるマシンで一度実行するか、言語ファイルを事前にダウンロードしてください |

これらに早めに対処することで、後で謎のバグを追いかける手間を省けます。

## ボーナス: 認識されたテキストをファイルに保存

OCR 結果を印刷せずに保存したい場合は、シンプルな `File.WriteAllText` 呼び出しで実現できます：

```csharp
string outputPath = "extracted_arabic.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
System.Console.WriteLine($"Text saved to {outputPath}");
```

出力ファイルは UTF‑8 エンコードを保持するため、アラビア文字が正しく保存されます。

## 結論 – 達成したこと

ここでは、Aspose.OCR を使用して **アラビア語テキストを認識** し、**画像からテキストを抽出** し、.NET コンソールアプリで正しく **右から左のテキストを読む** 方法を示しました。設定、インスタンス化、認識、出力の 4 ステップのフローは、アラビア語、ウルドゥー語、ヘブライ語など、あらゆる RTL 言語で再利用できる基本パターンです。

次のチャレンジに備えましたか？ OCR エンジンに請求書のバッチを入力し、結果を翻訳サービスに渡す、あるいはコードを ASP .NET Core API に統合して JSON エンコードされたアラビア語文字列を返すなど、可能性は無限です。共通する原則は同じで、適切な言語設定、リソース管理、Unicode 対応の出力です。

マルチページ PDF の扱い方や信頼度閾値の調整について質問がありますか？以下にコメントを残してください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.OCR を使用した言語選択付き C# 画像テキスト抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [複数言語対応の Aspose OCR で画像テキストを認識](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Aspose.OCR for .NET を使用した画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}