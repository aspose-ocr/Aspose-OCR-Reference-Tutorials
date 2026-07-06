---
category: general
date: 2026-04-03
description: C#でAspose OCRを使用して画像の傾きを補正する方法 – OCRのための画像前処理を学び、画像からテキストを認識し、数分でOCR精度を向上させる。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: ja
og_description: C#でAspose OCRを使用して画像の傾きを補正する方法。このガイドでは、OCRのための画像前処理、画像からのテキスト認識、そして精度向上の方法を示します。
og_title: Aspose OCRで画像の傾きを補正する方法 – 完全C#ガイド
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Aspose OCRで画像の傾き補正を行う方法 – 完全C#ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR で画像の傾き補正を行う方法 – 完全な C# ガイド

OCR エンジンに渡す前に **画像の傾き補正** が必要か疑問に思ったことはありませんか？ あなただけではありません—傾いたスキャン、斜めに撮影した写真、あるいは少し歪んだ PDF でも、テキスト認識ライブラリの精度を低下させる可能性があります。

このステップバイステップのチュートリアルでは、画像の読み込みから、**OCR 用画像前処理**（傾き補正、ノイズ除去、コントラスト強化、オートローテート）を経て、Aspose OCR で **画像からテキストを認識** し、最後に **OCR 精度を向上させる** ヒントをいくつか紹介します。最後までに、ノイズが多く傾いた PNG をプロのように処理できる、すぐに実行可能な C# コンソールアプリが完成します。

## 必要なもの

- **.NET 6+**（または .NET Framework 4.7.2 – API は同じように動作します）
- **Aspose.OCR for .NET** NuGet パッケージ (`Install-Package Aspose.OCR`)
- **傾いた** かつ **ノイズが多い** サンプル画像（例: `skewed_noisy.png`）
- Visual Studio、Rider、または好きなエディタ – 特別なツールは不要です

> **Pro tip:** 傾いたサンプルがない場合は、クリーンなスクリーンショットを Paint で 10‑15° 回転させ、画像エディタで少量の「塩胡椒」ノイズを加えるだけです。コードは同じように動作します。

それでは、始めましょう。

## 画像の傾き補正と OCR 精度向上の方法

最初に行うべきことは、Aspose の `OcrEngine` に受信したビットマップを **傾き補正** させることです。このエンジンには組み込みの `ImagePreprocessingOptions` クラスがあり、複数の品質向上機能を一度に切り替えることができます。

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### これが機能する理由

- **Deskew = true** はエンジンにテキストのベースラインを検出させ、ベースラインが水平になるまで画像を回転させます。これが無いと、たとえ 5° の傾きでも精度が 15‑20 % 低下することがあります。
- **Denoise** は低解像度の文書をスキャンした際にしばしば現れるランダムな斑点を除去します。
- **ContrastBoost** は前景（テキスト）と背景（紙）の差を増幅し、**OCR 精度を向上させる** ために不可欠です。
- **AutoRotate** は縦向きと横向きの向きを自動的に判別し、手動での確認作業を省きます。

上記のコードは **完全な実行可能サンプル** です—`YOUR_DIRECTORY` をファイルのパスに置き換えて F5 を押すだけです。

## OCR 用画像前処理 – ノイズ除去とコントラスト強化

ノイズ除去とコントラスト強化の両方が本当に必要か疑問に思うかもしれません。簡潔な答えは **はい、ほとんどの実務ケースで必要です**。以下に簡単にまとめます：

| Feature | What it does | When it matters |
|---------|--------------|-----------------|
| **Deskew** | 傾いたテキスト行を水平に補正 | スキャンしたフォーム、スマートフォンカメラで撮影した画像 |
| **Denoise** | 孤立したピクセルを除去 | 低照度スキャン、低価格スキャナ |
| **ContrastBoost** | 暗いテキストを明るくし、背景を暗くする | 色あせた文書、色あせたインク |
| **AutoRotate** | 縦向きと横向きを検出 | 向きが混在したマルチページ PDF |

完璧に整列したスキャンを処理している場合はフラグをオフにしても構いませんが、**OCR 用画像前処理** はほとんどの場合で安全なデフォルトであり、ほとんど影響はありません。

## 画像からテキストを認識 – Aspose OCR の使用

前処理パイプラインが完了すると、エンジンはクリーンなビットマップを内部の認識器に渡します。`Recognize` メソッドは改行が保持されたプレーンな `string` を返します。必要に応じて結果をさらに後処理（例: 空白のトリム、スペルチェック実行）できます。

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### 期待される出力

`skewed_noisy.png` にフレーズ “Hello World!” が含まれている場合、コンソールには次のように出力されます：

```
--- OCR RESULT ---
Hello World!
```

中程度のノイズがあっても、設定した前処理ステップのおかげで **95 %以上の精度** が得られるはずです。

## OCR 用画像の読み込み – ファイル処理のヒント

`Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` は **OCR 用画像を読み込む** 最も簡単な方法ですが、いくつか留意すべき細かい点があります：

1. **File locks** – `FromFile` は `Image` が破棄されるまでファイルハンドルを開いたままにします。後でファイルを削除または移動する予定がある場合は、`using` ブロックでラップしてください。
2. **Supported formats** – Aspose OCR は BMP、JPEG、PNG、TIFF、GIF をサポートします。PDF がある場合は、まず各ページを画像として抽出してください（Aspose.PDF が役立ちます）。
3. **Memory usage** – 大きな画像（5 MP 超）は大量の RAM を消費する可能性があります。`OutOfMemoryException` が発生した場合は、エンジンに渡す前に `Bitmap` で縮小することを検討してください。

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## OCR 精度向上 – 実践的なヒント

自動前処理を行っても、いくつかのエッジケースは OCR エンジンを混乱させます。以下は実戦で検証された、パイプラインに組み込める戦略です：

- **Binarize the image** (`opts.Binarization = true`) 背景が不均一な場合に使用します。
- **Set language** (`ocrEngine.Language = Language.English`) で文字セットを限定します。
- **Increase DPI**: スキャンプロセスを管理できる場合、少なくとも 300 dpi を目指してください。
- **Crop margins**: 大きな白い余白を除去します。余白は行検出を混乱させることがあります。
- **Validate output**: 正規表現を使って日付、数字、既知のパターンをチェックし、信頼度の低い行を手動レビュー用にフラグ付けします。

> **Remember:** 目的は単に **画像からテキストを認識** することだけでなく、さまざまな文書品質でも確実に実行できることです。

## 完全動作例 – すべての手順を1つのファイルにまとめて

以下は最終的な、自己完結型プログラムです。新しいコンソールプロジェクトにコピー＆ペーストして使用できます。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

プログラムを実行すると、クリーンで傾き補正されたテキストがコンソールに表示されます。`skewed_noisy.png` をクリーンで真っ直ぐなスキャンに差し替えても、出力は同じですが、エンジンが傾き補正ステップをスキップするため、わずかなパフォーマンス向上が得られます。

## 結論

本稿では Aspose OCR を使用した **画像の傾き補正**、**OCR 用画像前処理**、**OCR 用画像の読み込み** の正しい方法、そして **画像からテキストを認識** しつつ **OCR 精度を向上させる** 方法を紹介しました。完全なコードスニペットは任意の .NET プロジェクトにすぐに組み込めますし、追加のヒントはより難しい入力を処理するためのロードマップとなります。

次の課題に挑みますか？ 複数の画像を連結してマルチページ OCR ワークフローを作成したり、非英語文書用のカスタム言語パックを試したりしてみてください。同じ前処理の原則が適用されます—傾き補正、ノイズ除去、コントラスト強化、そして Aspose に重い処理を任せます。

特定のファイルタイプについて質問がある、または `ContrastBoost` の値調整が必要ですか？ 以下にコメントを残すか、Aspose フォーラムで質問してください。コーディングを楽しんで、OCR が常に正確でありますように！  

![左側に元の傾いた画像、右側に傾き補正・クリーンアップされた結果を示す図](deskew-diagram.png "元の傾いた画像と傾き補正結果を示す図 – 画像の傾き補正例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}