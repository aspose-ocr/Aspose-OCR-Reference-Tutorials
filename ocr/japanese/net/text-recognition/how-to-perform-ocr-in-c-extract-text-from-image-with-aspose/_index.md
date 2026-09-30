---
category: general
date: 2026-01-07
description: C#でAspose OCRを使用して画像からOCRを実行し、テキストを抽出する方法。画像からテキストを読み取り、ヒンディー語テキストを認識し、完全なコード例を取得する方法を学びます。
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from image
- recognize hindi text
- how to extract text from image
language: ja
og_description: C#でOCRを実行して画像からテキストを抽出する方法。このチュートリアルでは、画像からテキストを読み取り、ヒンディー語テキストを認識し、Aspose
  OCRを使用して画像からテキストを抽出する方法を示します。
og_title: C#でOCRを実行する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを実行する方法 – Aspose OCRで画像からテキストを抽出
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – Aspose OCRで画像からテキストを抽出

スキャンした請求書や看板の写真で **OCR を実行する方法** を考えたことがありますか？ あなただけではありません。実際のプロジェクトでは、領収書、パスポートのスキャン、手書きメモなど、**画像からテキストを抽出** する必要があります。良いニュースは、Aspose.OCR を使えば数行の C# コードで実現でき、さらに **ヒンディー語テキストを認識** する方法も学べます。

このチュートリアルでは、**画像からテキストを読み取る** 完全な実行可能サンプルを順に解説し、Aspose OCR エンジンを使って **画像からテキストを抽出** する方法と、各ステップの「なぜ」を説明します。外部ドキュメントへの曖昧な参照はなく、今日すぐにコピー＆ペーストして実行できる自己完結型のソリューションです。

## 必要なもの

- .NET 6.0 以降（コードは .NET Standard 2.0 でもコンパイル可能）
- Visual Studio 2022（またはお好みの IDE）
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）
- ヒンディー語テキストを含む画像ファイル（例: `hindi_invoice.jpg`）
- Aspose に同梱されている OCR 言語リソースフォルダー（Aspose サイトからダウンロード）

> **プロのコツ:** OCR リソースフォルダーをプロジェクトの隣に置くとパス管理が簡単です。

## 手順別実装

以下では、プロセスを 6 つの論理的ステップに分割します。各ステップは独自の H2 見出しを持ち（検索エンジンや AI モデルが情報をすばやく見つけられるように）、二次キーワードを自然に含む短い H3 小見出しがあります。

### Step 1 – OCR リソースパスの設定  
**Why this matters:** Aspose.OCR は、フォント、辞書、モデルファイルなどの言語パックが格納されたフォルダーに依存します。パスが間違っていると、エンジンは `FileNotFoundException` をスローし、画像からテキストを取得できません。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Tell the OCR engine where to find language resources
OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");
```

### Step 2 – OCR エンジンインスタンスの作成  
**Why this matters:** `OcrEngine` は認識モデルをメモリに保持する重厚なオブジェクトです。`using` ブロックでラップすることで適切に破棄され、バッチで多数の画像を処理する際に特に重要です。

```csharp
// Instantiate the OCR engine inside a using block
using (var ocrEngine = new OcrEngine())
{
    // Subsequent steps go here...
}
```

### Step 3 – 認識設定の構成（ヒンディー語の選択）  
**Why this matters:** デフォルトでは Aspose が言語を自動検出しようとしますが、`Language.Hindi` を明示的に設定することでデーヴァナーガリー文字の精度が向上し、処理速度も速くなります。

```csharp
    // Configure the engine to recognize Hindi text
    var recognitionSettings = new RecognitionSettings
    {
        Language = Language.Hindi   // Recognize Hindi characters
    };
```

### Step 4 – 読み取る画像のロード  
**Why this matters:** `ImageStream.FromFile` は基盤となるビットマップ処理を抽象化し、データを効率的にストリームします。画像がウェブリクエストから来る場合は `MemoryStream` を使用することもできます。

```csharp
    // Load the target image (replace with your own path)
    var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");
```

### Step 5 – OCR プロセスの実行  
**Why this matters:** `Recognize` メソッドは前処理、セグメンテーション、文字分類、最終的なテキスト組み立てという重い処理を行います。結果はプレーンな文字列として返され、保存、表示、または後処理に利用できます。

```csharp
    // Execute OCR and capture the recognized text
    string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

### Step 6 – 抽出されたテキストの表示  
**Why this matters:** デバッグのために結果をコンソールやログファイルに書き出すことが多いです。本番環境ではデータベースに保存したり、下流のワークフローに渡したりすることがあります。

```csharp
    // Output the result to the console
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(recognizedText);
}
```

## 完全な動作例

すべてを組み合わせた完全なプログラムを以下に示します。コンソールアプリプロジェクトに貼り付けて使用できます。プレースホルダーのパスは実際のディレクトリに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Set the folder that contains language resources
        OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");

        // 2️⃣ Create the OCR engine (auto‑disposed)
        using (var ocrEngine = new OcrEngine())
        {
            // 3️⃣ Tell the engine to look for Hindi characters
            var recognitionSettings = new RecognitionSettings
            {
                Language = Language.Hindi
            };

            // 4️⃣ Load the image you want to read
            var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");

            // 5️⃣ Perform OCR
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

            // 6️⃣ Show the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }

        // Keep console open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**期待される出力**（簡略化）:

```
=== OCR Result ===
Invoice No: 12345
Date: 01/01/2024
Amount: ₹ 15,000
धन्यवाद
```

ヒンディー文字の代わりに文字化けが表示された場合は、リソースフォルダーが正しいバージョンの Hindi 言語パックを指しているか再確認してください。

## よくある落とし穴と対策

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Garbage characters** | 言語リソースが間違っている、または欠如している | `SetResourcesPath` が `Hindi.cognates` などのファイルを含むフォルダーを指していることを確認 |
| **Out‑of‑memory errors** | 大きすぎる画像をスケーリングせずに読み込んでいる | `ImageStream.FromFile(..., maxWidth: 2000)` を使用してオンザフライで縮小 |
| **Slow performance** | 自動検出モードで多数の言語をスキャンしている | `Language = Language.Hindi`（または目的の言語）を明示的に設定 |
| **No output at all** | 画像が完全に白またはぼやけている | OCR に渡す前に画像を前処理（コントラスト、二値化）する |

## ソリューションの拡張：他の言語とシナリオ

英語、スペイン語、その他の言語で **画像からテキストを読み取る** 必要がある場合は、`Language` 列挙体を変更するだけです。

```csharp
recognitionSettings.Language = Language.English;   // or Language.Spanish, etc.
```

複数の言語を組み合わせることもできます。

```csharp
recognitionSettings.Language = Language.English | Language.Hindi;
```

バッチ処理の場合は、画像フォルダーを走査する `foreach` ループの周りに `using (var ocrEngine = new OcrEngine())` ブロックを配置します。エンジンはロード済みモデルを再利用し、初期化オーバーヘッドを大幅に削減します。

## OCR 精度のテスト

1. 既知のテスト画像でプログラムを実行します（任意のグラフィックエディタでヒンディー語テキストのシンプルな PNG を作成できます）。
2. コンソール出力を元のテキストと比較します。
3. エラー率が 5 % を超える場合は、画像品質を調整（DPI を 300 dpi に上げる）や、`imageStream = imageStream.ApplyGaussianBlur(1.5)` のような前処理ステップの適用を検討してください（Aspose は基本的なフィルタを提供）。

## 結論

本稿では、Aspose.OCR を使用した C# における **OCR の実行方法** を示し、**画像からテキストを抽出** する方法と **ヒンディー語テキストを認識** する実例を解説しました。リソースパスの設定、エンジンの作成、言語設定、画像のロード、認識の実行、結果の表示という 6 つのステップに従うことで、あらゆる文書デジタル化プロジェクトに利用できる信頼性の高い構成要素が手に入りました。

次に、`Language.Hindi` を別の言語に置き換えてみたり、OCR の出力を自然言語処理パイプラインに渡して請求書を自動分類したりしてください。可能性は無限で、基本パターンは変わりません：**画像からテキストを読み取る**、そしてそのテキストをアプリケーションの必要に応じて処理します。

エッジケースやパフォーマンスチューニング、ライセンスに関する質問がありますか？以下にコメントを残してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}