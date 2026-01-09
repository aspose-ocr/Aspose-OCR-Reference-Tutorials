---
category: general
date: 2026-01-09
description: Aspose.OCR を使用して画像を OCR し、画像テキストを抽出する方法を学びます。スキャンした文書の変換、GPU の有効化、OCR
  で画像を読み取る手順が含まれます。
draft: false
keywords:
- how to ocr image
- extract image text
- convert scanned document
- how to enable gpu
- read image with ocr
language: ja
og_description: Aspose.OCRで画像を素早くOCRする方法。ステップバイステップのチュートリアルに従って、画像のテキストを抽出し、スキャンした文書を変換し、GPUを有効にしましょう。
og_title: C#で画像をOCRする方法 – GPUアクセラレートガイド
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#で画像をOCRする方法 – GPUサポート付き完全ガイド
url: /ja/net/ocr-configuration/how-to-ocr-image-in-c-complete-guide-with-gpu-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像をOCRする方法 – GPUサポート付き完全ガイド

.NET アプリから直接 **画像を OCR する** 方法を知りたくありませんか？ 開発者は PDF、TIFF、写真などの画像からテキストを抽出する必要が頻繁にあります。特に大量のスキャン文書を扱う場合は必須です。朗報です！ Aspose.OCR を使えば、数行のコードで **画像テキストを抽出** でき、さらに **GPU** を有効にして処理速度を向上させることも可能です。

このチュートリアルでは、ライブラリのインストールから GPU フォールバック付き OCR エンジンの初期化、最終的に **OCR で画像を読み取る** 方法と結果の表示まで、必要なすべての手順を解説します。最後まで読めば、外部サービスを使わずに **スキャン文書の画像を編集可能な文字列に変換** できるようになります。

---

## 必要なもの

作業を始める前に、以下を用意してください。

- **.NET 6.0** 以上（コードは .NET Core と .NET Framework でも動作します）。
- Aspose.OCR の **ライセンス** または一時的な評価キー（無料トライアルでテスト可能）。
- 処理したい画像ファイル（できれば高解像度の TIFF または PNG）。
- （オプション）GPU が有効なマシン。速度向上を確認したい場合に使用します。GPU が無い場合はエンジンが自動的に CPU にフォールバックします。

これらの前提条件が整っていれば、後で壁にぶつかることなく OCR ワークフローに集中できます。

---

## Step 1: Install Aspose.OCR NuGet Package

まずは Aspose.OCR ライブラリをプロジェクトに追加します。ソリューションフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の NuGet UI で **Aspose.OCR** を検索し、インストールボタンをクリックするだけです。この単一コマンドで必要な DLL がすべて取得され、GPU 用のネイティブバイナリが利用可能な場合は自動的に含まれます。

> **Pro tip:** パッケージは常に最新の状態に保ちましょう。新しいリリースには言語モデルの改善や GPU サポートの向上が含まれることが多いです。

---

## Step 2: Import Required Namespaces  

パッケージをインストールしたら、必要な名前空間をインポートします。ここからが **画像を OCR する** コードの出発点です。

```csharp
// Step 2: Import required namespaces
using Aspose.OCR;
using Aspose.OCR.Settings;
```

この 2 行で `OcrEngine` クラスと、GPU 使用を切り替える設定オブジェクトにアクセスできるようになります。これが無いとコンパイラは `OcrEngine` が何か分からなくなります。

---

## Step 3: Initialize the OCR Engine and Enable GPU  

**GPU を有効にする** 方法を知りたかった方へ、ここが答えです。`OcrEngineSettings` のインスタンスを作成し、`UseGpu` フラグをオンにしてエンジンのコンストラクタに渡します。エンジンは自動的に互換性のある GPU があるか検出し、無ければ CPU にフォールバックしますので、追加のエラーハンドリングは不要です。

```csharp
// Step 3: Initialize the OCR engine with GPU support (falls back to CPU if unavailable)
var ocrSettings = new OcrEngineSettings { UseGpu = true };
var ocrEngine   = new OcrEngine(ocrSettings);
```

GPU を有効にする理由は何でしょうか？ 大きな画像、たとえばマルチページ TIFF や高解像度スキャンの場合、処理時間が数秒から数百ミリ秒に短縮されます。バッチ処理パイプラインを構築している場合、この速度向上は大きなメリットになります。

---

## Step 4: Perform OCR on Your Target Image  

ここで実際に **OCR で画像を読み取る** 作業を行います。ファイルへのパスを渡すだけで、エンジンは認識したテキストを文字列として返します。Aspose がサポートするラスタ形式（PNG、JPEG、TIFF、BMP など）すべてで動作します。

```csharp
// Step 4: Perform OCR on the target image file
string imagePath = @"C:\Images\large-document.tif";
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

**スキャン文書** のページを 1 枚ずつ変換したい場合は、ファイル名のリストをループし `RecognizeImage` を呼び出すだけです。このメソッドはスレッドセーフなので、マルチコア CPU で並列処理することも可能です。

---

## Step 5: Display or Persist the Extracted Text  

最後に結果を出力します。コンソールアプリなら `Console.WriteLine` が手軽です。実際のアプリケーションでは、データベースや JSON ファイル、検索インデックスへ書き込むことが考えられます。

```csharp
// Step 5: Display the extracted text
Console.WriteLine(recognizedText);
```

上記の行は OCR の生データをコンソールに表示します。改行や稀な誤認識、余計な文字が混ざることがありますが、これは OCR では普通のことです。必要に応じて正規表現でクリーンアップするなど、後処理を加えると良いでしょう。

> **Note:** Aspose.OCR には言語別辞書も用意されています。英語以外のテキストを処理する場合は、`ocrEngine.Settings.Language` を適切に設定してから `RecognizeImage` を呼び出してください。

---

## Full Working Example  

すべてをまとめた、コピー＆ペースト可能なコンソールプロジェクトのサンプルです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support
        var ocrSettings = new OcrEngineSettings { UseGpu = true };
        var ocrEngine   = new OcrEngine(ocrSettings);

        // Path to the image you want to process
        string imagePath = @"C:\Images\large-document.tif";

        // Perform OCR
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Output the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**期待される出力**（抜粋）:

```
=== OCR Result ===
This is a sample scanned document.
It contains several lines of text that have been
converted from image to editable characters.
...
```

プログラムを実行すると、抽出されたテキストがコンソールに表示されます。GPU が利用可能な環境では、CPU のみの場合に比べて処理時間が顕著に短くなるはずです。

---

## Common Pitfalls & How to Avoid Them  

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Garbage characters** | 低解像度の画像やノイズが多い背景。 | OCR 前に画像を前処理（DPI を上げる、二値化を適用）する。 |
| **GPU not used** | 互換性のある CUDA ドライバがインストールされていない。 | ドライバのバージョンを確認するか、`UseGpu = false` で CPU を強制。 |
| **Out‑of‑memory on large TIFFs** | ファイル全体を一度に読み込んでいる。 | `OcrEngineSettings.MaxMemoryUsage` で使用メモリ上限を設定するか、ページ単位で処理する。 |
| **Incorrect language detection** | デフォルト言語が英語になっている。 | `ocrEngine.Settings.Language = Language.YourLanguage;` を `RecognizeImage` 前に設定。 |

これらのケースに対処すれば、 **画像を OCR する** 実装はさまざまな環境でも安定して動作します。

---

## Extending the Solution  

**画像テキストを抽出** できたら、次のような拡張が考えられます。

- **スキャン文書** PDF を検索可能な PDF に変換し、OCR レイヤーを埋め込む。
- 抽出結果を **Azure Cognitive Search** インデックスに保存し、高速検索を実現。
- OCR 出力を **翻訳 API** に渡して多言語対応にする。
- **Aspose.OCR** の `GetBoundingBoxes` メソッドを使い、各単語の画像上の位置情報を取得。赤字処理ツールに便利です。

これらすべては、エンジンの初期化 → 画像投入 → テキスト取得という基本フローを拡張する形で実装できます。

---

## Conclusion  

本稿では、Aspose.OCR を用いた **C# で画像を OCR する** 完全なエンドツーエンド例を紹介しました。NuGet パッケージのインストール、適切な名前空間のインポート、GPU の有効化（または CPU フォールバック）、そして `RecognizeImage` の呼び出しという手順で、 **画像テキストの抽出**、**スキャン文書の変換**、**OCR で画像を読む** が確実に行えます。

ぜひ自分のスキャン画像で試してみてください。画像形式や GPU フラグを切り替えて、パフォーマンスの変化を体感しましょう。準備ができたら、言語辞書やバウンディングボックス抽出といった高度機能に挑戦し、OCR パイプラインをさらに賢くカスタマイズしてください。

Happy coding, and may your OCR pipelines be fast, accurate, and hassle‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}