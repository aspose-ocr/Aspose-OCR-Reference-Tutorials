---
category: general
date: 2026-03-23
description: C#でAspose OCRを使用して画像のデスキュー（傾き補正）を行う方法。ノイズ除去、画像の回転補正、画像からのテキスト認識を数分で学びましょう。
draft: false
keywords:
- how to deskew image
- how to remove noise
- recognize text from image
- remove salt pepper noise
- correct image rotation
language: ja
og_description: Aspose OCRで画像の傾きを素早く補正する方法。このガイドでは、ノイズ除去、画像の回転補正、画像からのテキスト認識方法も紹介します。
og_title: C#で画像の傾き補正を行う方法 – 完全なAspose OCRチュートリアル
tags:
- OCR
- C#
- Image Preprocessing
title: C# と Aspose OCR で画像の傾き補正を行う方法 – 完全ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-in-c-with-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像の傾きを補正する方法 – 完全な Aspose OCR チュートリアル

スキャナーから取得した画像が少しだけ傾いている **how to deskew image** 方法を考えたことがありますか？ あなたは一人ではありません。多くの実務プロジェクトでは、元画像が数度傾いていたり、塩胡椒ノイズが散在していたりし、それでもプレーンテキストとして読み取る必要があります。  

良いニュースです。Aspose OCR を使えば、回転を修正し、ノイズを除去し、そして **recognize text from image** を数行のコードで実現できます。このチュートリアルでは、全体のパイプラインを順に解説し、各フィルタが重要な理由を説明し、すぐに実行できる C# プログラムを提供します。

> *Pro tip:* Aspose OCR をまだ使用したことがない場合は、Aspose のウェブサイトから無料トライアルを取得してください。API は .NET 6+ ですぐに利用できます。

## 必要なもの

- **.NET 6 SDK** (または最近の .NET バージョン) – コードは Visual Studio、Rider、または `dotnet` CLI でコンパイルできます。  
- **Aspose.OCR NuGet package** – `dotnet add package Aspose.OCR` でインストールします。  
- 少し傾いていてノイズが含まれる **sample image** (例: `skewed.png`)。  
- 基本的な C# の知識 – エキスパートである必要はなく、`using` 文とコンソール操作に慣れていれば十分です。

以上です。追加の OCR エンジンやネイティブ DLL は不要で、単一の NuGet 参照だけです。

## 画像の傾き補正 – ステップバイステップ概要

以下では、プロセスを論理的なステップに分解します。各ステップには明確な見出し、コードスニペット、そして「なぜ」その呼び出しが必要かを説明する短い段落が付いています。

![how to deskew image example](https://example.com/deskew-demo.png "how to deskew image")

### ステップ 1: OCR エンジンのセットアップ

まず `OcrEngine` のインスタンスを作成します。`using` ブロックは適切な破棄を保証し、完了次第ネイティブリソースを解放します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Step 1 – instantiate the OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the pipeline goes here...
        }
    }
}
```

*Why this matters:* `OcrEngine` は Aspose OCR の中心です。画像、フィルタチェーン、認識設定を保持します。`using` でラップすることで、特にバッチジョブで数十ページを処理する際のメモリリークを防止します。

### ステップ 2: スキャン画像の読み込み

`ImageStream.FromFile` でファイルを読み込みます。パスは絶対パスでも、実行ファイルの作業ディレクトリに対する相対パスでも構いません。

```csharp
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");
```

*Why this matters:* エンジンはメモリ内の画像ストリームで動作します。正しいパスを指定しないと `FileNotFoundException` が発生する唯一の箇所なので、実行前にフォルダ構成を確認してください。

### ステップ 3: 前処理フィルタの追加

ここで **how to remove noise** と **correct image rotation** に対処します。2 つの組み込みフィルタが主要な処理を行います：

```csharp
// DeskewFilter corrects small rotation (usually up to ±5°)
ocrEngine.Filters.Add(new DeskewFilter());

// DenoiseFilter removes salt‑and‑pepper noise
ocrEngine.Filters.Add(new DenoiseFilter());
```

*Why these filters?*  
- **DeskewFilter** はテキストのベースラインを解析し、傾斜角度を計算してビットマップを水平に戻します。これがないと OCR エンジンは文字を誤認識する可能性があります（例: “l” と “i” の区別）。  
- **DenoiseFilter** は中央値ベースのアルゴリズムを適用し、孤立した黒/白ピクセルを平滑化します。画像処理用語でいう “remove salt pepper noise” と同義で、信頼度スコアが大幅に向上します。

スキャンが大幅にぼやけている場合は、`SharpenFilter` を前に追加することもできますが、これはオプションの調整です。

### ステップ 4: OCR 認識の実行

ここで Aspose OCR に処理を依頼します。`Recognize` メソッドは成功を示すブール値を返します。

```csharp
if (ocrEngine.Recognize())
{
    // Step 5 – output the cleaned text
    Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed – check the image and filter configuration.");
}
```

*Why we check the result:* 時々エンジンがテキストを検出できないことがあります（例: 空白ページ）。`false` のケースを処理することで、後でデバッグが困難になるサイレント失敗を防げます。

### ステップ 5: 出力の検証

プログラムを実行すると、以下のような出力が表示されます：

```
Cleaned text:
The quick brown fox jumps over the lazy dog.
```

テキストがまだ乱れている場合は、以下を検討してください：

- **Increasing the deskew tolerance** – `new DeskewFilter(0.1)` はフィルタがより大きな角度を許容できるようにします。  
- **Adding a `BinarizeFilter`** をデノイズ前に追加して、画像を純粋な白黒に変換します。  
- **Checking the DPI** – 低解像度スキャン（< 150 dpi）は OCR 前に拡大が必要なことが多いです。

## ノイズ除去 – 高度なオプション

基本的な `DenoiseFilter` は一般的なスキャナの斑点には効果的ですが、古いフィルムスキャンで **remove salt pepper noise** に直面することもあります。そのような場合は：

```csharp
// Apply a stronger median filter (kernel size 3x3)
ocrEngine.Filters.Add(new DenoiseFilter { KernelSize = 3 });
```

またはデノイズ前に **GaussianBlurFilter** をチェーンします：

```csharp
ocrEngine.Filters.Add(new GaussianBlurFilter { Sigma = 0.8 });
ocrEngine.Filters.Add(new DenoiseFilter());
```

これらの調整は若干のシャープさを犠牲にして、よりクリーンな二値画像にします。通常、OCR の信頼度スコアが 5‑10 % 向上します。

## 画像からテキストを認識 – 後処理のヒント

`ocrEngine.Text` を取得したら、以下の処理を行いたくなるかもしれません：

- **Trim whitespace** – `ocrEngine.Text = ocrEngine.Text.Trim();`  
- **Normalize line endings** – `ocrEngine.Text = ocrEngine.Text.Replace("\r\n", "\n");`  
- **Run a spell‑check** は、ソース言語が英語でない場合、`System.Globalization` またはサードパーティのライブラリを使用して実行します。

これらすべての手順により、抽出された文字列は検索インデックスやデータ入力フォームへの投入など、下流処理の準備が整います。

## エッジケースと一般的な落とし穴

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| Image rotated > 10° | `DeskewFilter` がデフォルトの制限で停止する | カスタムの最大角度を渡す: `new DeskewFilter { MaxAngle = 15 }` |
| Very dark background | フィルタが背景をテキストと誤認識する可能性がある | `InvertColorsFilter` を前に追加するか、コントラストを上げる |
| Multi‑page PDF | `OcrEngine` は一度に1画像しか処理できない | 各ページをループし、イテレーションごとに新しい `OcrEngine` を作成する |
| Non‑Latin script | デフォルト言語は英語 | `ocrEngine.Language = OcrLanguage.Thai;` を設定する（またはサポートされている任意の言語） |

これらを意識しておくことで、古典的な “Why is my OCR output empty?” の悪夢を回避できます。

## 完全な動作例

以下のコードを新しいコンソールプロジェクト（`dotnet new console -n OcrDemo`）にコピーしてください。Aspose OCR パッケージを復元し、`YOUR_DIRECTORY/skewed.png` をテスト画像へのパスに置き換えて実行します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Initialize OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Load the image that may be slightly rotated
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");

            // Add preprocessing filters
            //   - DeskewFilter corrects small rotation
            //   - DenoiseFilter removes salt‑and‑pepper noise
            ocrEngine.Filters.Add(new DeskewFilter());
            ocrEngine.Filters.Add(new DenoiseFilter());

            // Perform OCR recognition
            if (ocrEngine.Recognize())
            {
                // Output the cleaned text
                Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – verify the image and filters.");
            }
        }
    }
}
```

このプログラムを実行すると、クリーンで傾きが補正されたテキストがコンソールに出力されます。これが **how to deskew image** ワークフロー全体で、コードは 50 行未満です。

## 結論

ここでは Aspose OCR を使用した **how to deskew image**、**how to remove noise**、**correct image rotation** を解説し、信頼性の高い **recognize text from image** 方法を示しました。`DeskewFilter` と `DenoiseFilter` をチェーンすることで、鮮明で水平に補正されたビットマップが得られ、OCR エンジンは高い信頼度で読み取れます。

ここからは以下を検討できます：

- 並列で数十枚のスキャンをバッチ処理する。  
- OCR 結果を PDF/A にエクスポートしてアーカイブする。  
- 多言語文書向けに言語検出を統合する。

これらのアイデアを試してみて、特定のスキャンに合わせてフィルタパラメータを自由に調整してください。コーディングを楽しんで、画像が常に完璧に真っ直ぐでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}