---
category: general
date: 2026-02-17
description: Aspose OCR を使用して C# で複数の PDF と画像をバッチ OCR する方法。PDF からテキストを抽出し、PDF をテキストに変換し、画像からテキストを認識する方法を学びます。
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: ja
og_description: Aspose OCR を使用して C# で複数のドキュメントをバッチ OCR する方法。PDF からテキストを抽出し、PDF をテキストに変換し、画像からテキストを認識するステップバイステップのコードを入手できます。
og_title: C#でOCRファイルを一括処理する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: C#でOCRファイルを一括処理する方法 – 完全コード例
url: /ja/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でファイルをバッチ OCR する方法 – 完全ガイド

PDF や画像スキャンの山を **バッチ OCR** したいと考えたことはありませんか？ 各ファイルごとに別々のループを書かなければならない壁にぶつかる開発者は多いです。朗報です。Aspose OCR を使えば、ファイルのコレクションを 1 つのエンジンに渡すだけで、重い処理を任せられます。  

このチュートリアルでは、**pdf からテキストを抽出**、**pdf をテキストに変換**、そして **画像からテキストを認識** する実用的なバッチ処理の解決策をステップバイステップで解説します。最後には、各ページの OCR 結果をコンソールに出力する実行可能なコンソール アプリが完成し、各ステップの背景を理解できるので自分のプロジェクトに応用できます。

## 前提条件 – 開始前に必要なもの

- **.NET 6.0 以降**（コードは .NET Framework でも動作しますが、.NET 6+ 推奨）
- **Aspose.OCR NuGet パッケージ** – `dotnet add package Aspose.OCR` でインストール
- サンプル ファイル数点：マルチページ PDF（`doc1.pdf`）とスキャンした TIFF（`doc2.tif`）。`C:\OCRSamples` など参照できるフォルダーに配置してください。
- 基本的な C# の知識 – `using` 文やコレクションに慣れていること

> プロのコツ: ライセンスがない場合は、Aspose が提供する無料の一時キーを使用すれば、開発中の 100 ページ制限を解除できます。

## 手順 1: プロジェクトの作成と名前空間のインポート

まず、コンソール プロジェクトを新規作成（または既存プロジェクトに追加）し、必要な名前空間をインポートします。

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **なぜ重要か:** `Aspose.OCR.Image` をインポートすると、PDF ページを自動的に個別の画像ストリームに分割する便利な `ImageStream.FromFile` メソッドが利用可能になります。これがバッチ処理を楽にする秘密のソースです。

## 手順 2: OCR エンジンの初期化

エンジンは基盤となる OCR エンジンとやり取りする作業馬です。バッチ全体でインスタンスは 1 つだけで構いません。

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **解説:** 同じ `OcrEngine` を再利用すると、メモリの churn が減り、ページ間でネイティブ ライブラリが保持されるため処理速度が向上します。

## 手順 3: 画像ストリームのリスト作成

ここで処理対象のすべてのドキュメントを集めます。`ImageStream.FromFile` は PDF を個別ページに分割できるので、3 ページの PDF は裏側で 3 つのストリームに変換されます。

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **エッジケース:** PDF、TIFF、JPEG、PNG が混在していても同じリストに追加すれば OK – Aspose が自動でフォーマット検出を行います。

## 手順 4: バッチ OCR の実行

リストをエンジンに渡します。`RecognizeBatch` はページごとに 1 つずつ `OcrResult` オブジェクトのコレクションを返します。

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **なぜバッチか？** 手動ループでページ単位に OCR を実行するとエンジンが毎回再初期化され、処理時間が倍増します。`RecognizeBatch` はエンジンを温めたままにし、結果が出次第ストリームで返します。

## 手順 5: 認識テキストの出力

最後に結果をループで回し、各ページのテキストをコンソールに書き出します。ここで `Console.WriteLine` をファイル書き込みや DB 挿入、その他の下流処理に置き換えることが可能です。

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### 期待されるコンソール出力

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

サンプル ファイルでプログラムを実行すると、各ページごとにテキストのブロックが表示され、**extract text scanned pdf** が 1 回のパスで成功したことが確認できます。

## よくある落とし穴の対処法

| 問題 | 発生理由 | 簡単な対策 |
|------|----------|------------|
| **メモリ不足エラー** | 大容量 PDF が多数の高解像度画像を生成するため | PDF 読み込み時に DPI を制限: `ocrEngine.Settings.ImageDpi = 200;` |
| **文字化け** | 元スキャンが低品質または未対応言語の場合 | 言語を明示的に設定: `ocrEngine.Language = Language.English;` |
| **結果が途中で途切れる** | バッチリストに破損ファイルが混在している | `RecognizeBatch` を try/catch で囲み、問題ファイルの `e.Message` をログに残す |
| **パフォーマンス低下** | マルチコア環境でシングルスレッド実行している | スレッドごとに別々の `OcrEngine` インスタンスを持つ `Parallel.ForEach` を使用（上級者向け） |

## ボーナス: OCR 結果をテキスト ファイルに保存

ページごとに個別の `.txt` ファイルを作成したい場合は、ループ内に小さな書き込みブロックを追加するだけです。

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

これで **convert pdf to text** がプレーンテキスト ファイルの整然としたフォルダーに変換され、後続のインデックス作成や検索に最適です。

## 完全動作サンプル

以下はそのままコピー＆ペーストできる完全版プログラムです。隠れた依存関係や外部スクリプトは一切ありません。

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

プロジェクト フォルダーで `dotnet run` を実行すれば、抽出されたテキストがコンソールに流れ込みます。これが **how to batch OCR** を数行の C# で実現する方法です。

## 本記事のまとめ – クイックリキャップ

- .NET コンソール アプリをセットアップし、Aspose.OCR をインストール  
- 処理効率を高めるために単一の `OcrEngine` インスタンスを作成  
- PDF を自動でページ分割する `ImageStream` オブジェクトのリストを構築  
- `RecognizeBatch` を実行して **extract text from pdf** と他の画像形式を一括取得  
- 結果をコンソールに出力し、必要に応じて個別 `.txt` ファイルに保存して **convert pdf to text** ワークフローを完了  

## 次のステップと関連トピック

- **スケールアップ**: `Parallel.ForEach` と `OcrEngine` プールを組み合わせ、数百ファイルを同時処理  
- **言語パック**: `Language.English` を `Language.French` に置き換える、またはカスタム辞書をロードして **recognize text from images** を他言語でも実現  
- **ポストプロセッシング**: OCR 出力をスペルチェッカーや自然言語パーサーに通し、スキャンされた契約書の精度を向上  
- **代替ライブラリ**: オープンソースを求めるなら Tesseract.NET と比較検討—どちらも **extract text scanned pdf** が可能ですが、ライセンス形態と初期精度に違いがあります  

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}