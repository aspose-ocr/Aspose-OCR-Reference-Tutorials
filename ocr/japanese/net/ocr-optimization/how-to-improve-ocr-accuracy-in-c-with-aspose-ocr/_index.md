---
category: general
date: 2026-04-11
description: Aspose OCR を使用して、JPG からテキストを認識し、画像の傾きを補正し、ノイズを除去することで、C# における OCR を改善する方法を学びましょう。
draft: false
keywords:
- how to improve OCR
- recognize text from jpg
- extract text from image
- how to deskew image
- how to remove noise
language: ja
og_description: JPGからテキストを認識し、画像の傾きを補正し、ノイズを除去することでOCRを向上させる方法を発見—完全なC#ガイド。
og_title: Aspose OCR を使用した C# での OCR 精度向上方法
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Aspose OCR を使用した C# で OCR 精度を向上させる方法
url: /ja/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使用して OCR 精度を向上させる方法

スキャン画像が抽象画のように読めないテキストに見えるとき、**OCR の精度を向上させる方法** を考えたことはありませんか？ あなただけではありません。実務で扱う請求書、レシート、手書きメモなどの画像は、傾いていたり、粒状だったり、ノイズが多かったりします。朗報です！ Aspose OCR には、そうした画像をきれいな機械可読文字に変換するための前処理ノブが用意されています。このチュートリアルでは、**JPG からテキストを認識し**、画像をデスクューし、不要なノイズを除去する **OCR 精度を向上させる方法** を示す、完全に実行可能なサンプルを順に解説します。

> *プロのコツ:* 前処理を省くと、暗号パズルのように読めない出力になることが多いです。これを防ぎましょう。

![How to improve OCR with Aspose OCR preprocessing](https://example.com/ocr-preprocess.png "how to improve OCR with Aspose OCR")

## 学べること

この数分で以下が学べます：

1. Aspose OCR エンジンを最適な精度で設定する方法。  
2. **JPG ファイルからテキストを認識** するために必要な正確なコード。  
3. *AutoDeskew* と *RemoveNoise* を有効にする意義と調整方法。  
4. カスタムフィルタを書かずに **画像からテキストを抽出** する方法。  
5. よくある落とし穴（ファイルが見つからない、未対応フォーマット）と即時の対処法。

最後には、任意の JPG をクリーンアップし、抽出した文字列を出力できる単一の C# コンソール アプリが完成します。これを下流処理や保存にすぐ利用できます。

## 前提条件

- .NET 6.0 SDK 以降（サンプルは簡潔さのためトップレベルステートメントを使用）。  
- Aspose.OCR NuGet パッケージ (`dotnet add package Aspose.OCR`)。  
- 実行ファイルと同じフォルダーに配置したサンプル JPG 画像（`input.jpg`）。  
- C# の基本的な知識（高度な概念は不要）。

既にプロジェクトがある場合はコードを貼り付けるだけです。新規に作成する場合はコンソール アプリを作成してください：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

それではコードを見ていきましょう。

## OCR 精度を向上させる: 前処理設定の概要

**OCR の精度を向上させる方法** の核心は `PreprocessSettings` オブジェクトです。文字認識エンジンが起動する前に実行されるミニ画像エディタと考えてください。以下は最も効果的なフラグの概要です：

| Setting                | What it does                                            | Typical use case |
|------------------------|---------------------------------------------------------|------------------|
| `AutoDeskew`           | 深層学習ベースのデスキューアルゴリズムを適用します。   | わずかに傾いたスキャンページ |
| `AdaptiveThreshold`    | 低照度や色あせた画像のコントラストを向上させます。   | インクが薄れた古いレシート |
| `RemoveNoise`          | ガウシアンブラーで斑点を抑制します。                   | スマートフォンのフラッシュ撮影 |
| `NoiseRemovalStrength`| 侵略度を制御します (1 = 低, 3 = 高)。                 | ソースの粒状度に合わせて微調整 |

これらのオプションを有効にすることが、**OCR の精度を向上させる方法** における「秘訣」です。

## Aspose OCR で JPG からテキストを認識する

以下はそのまま実行可能な完全プログラムです。各行にコメントを付けて、*何を* するだけでなく *なぜ* そうするのかが分かるようにしています。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessDemo
{
    static void Main()
    {
        // ------------------------------------------------------------
        // Step 1: Create an OCR engine instance.
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ------------------------------------------------------------
        // Step 2: Fine‑tune preprocessing to improve accuracy.
        // ------------------------------------------------------------
        ocrEngine.Settings.Preprocess = new PreprocessSettings
        {
            AutoDeskew = true,               // How to deskew image automatically.
            AdaptiveThreshold = true,        // Improves contrast for better recognition.
            RemoveNoise = true,              // How to remove noise before OCR.
            NoiseRemovalStrength = 2         // Medium strength; adjust 1‑3 as needed.
        };

        // ------------------------------------------------------------
        // Step 3: Load the JPG image you want to process.
        // ------------------------------------------------------------
        // If the file is missing, Aspose will throw a FileNotFoundException.
        // Wrap it in a try/catch if you need graceful fallback.
        ImageStream image;
        try
        {
            image = ImageStream.FromFile("input.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading image: {ex.Message}");
            return;
        }

        // ------------------------------------------------------------
        // Step 4: Run the OCR engine on the preprocessed image.
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ------------------------------------------------------------
        // Step 5: Display the extracted text.
        // ------------------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 期待される出力

`input.jpg` に「Invoice #12345 – Total: $256.78」という文言が含まれている場合、コンソールは次のように表示します：

```
=== Extracted Text ===
Invoice #12345 – Total: $256.78
```

ダッシュやドル記号がそのまま保持されていることに注目してください。これは **画像からテキストを抽出** した際に期待される結果です。

## 前処理設定で画像をデスクューする方法

デスクューが重要な理由は何でしょうか？ 2 度程度の傾きでも文字分割段階で混乱を招き、文字が誤認識されやすくなります。`AutoDeskew` フラグは内部で畳み込みニューラルネットワークを使用し、支配的な角度を検出して画像を基準に戻します。

より細かく制御したい場合は、角度を手動で設定できます：

```csharp
ocrEngine.Settings.Preprocess = new PreprocessSettings
{
    AutoDeskew = false,          // Turn off automatic detection.
    // Manually specify a rotation angle (in degrees):
    DeskewAngle = -1.8           // Positive = clockwise, negative = counter‑clockwise.
};
```

> **手動デスクューを使うタイミング:** カメラが常に一定角度で傾けて撮影する（例: 固定設置スキャナ）場合、角度をハードコードすると処理時間が僅かに短縮されます。

## ノイズ除去で抽出精度を向上させる方法

ノイズは特に低照度撮影でランダムな斑点や粒状として現れます。`RemoveNoise` フラグは背景を平滑化しつつエッジ（文字）を保持するバイラテラルフィルタを適用します。`NoiseRemovalStrength` プロパティで侵略度を調整できます：

| Strength | Effect |
|----------|--------|
| 1        | 軽い平滑化—やや粒状の画像に最適 |
| 2        | バランス良好—ほとんどのスマホ撮影に適合 |
| 3        | 強い平滑化—極端にノイズが多い画像向き。ただし細い筆跡がぼやける可能性あり |

細字が読めなくなる場合は、強度を下げるかフィルタ自体を無効にしてください。

## 画像からテキストを抽出: JPG 以外にも対応

デモは JPG に焦点を当てていますが、Aspose OCR は PNG、BMP、TIFF、さらには PDF ページもサポートしています。**画像からテキストを抽出** したいフォーマットが JPG でない場合は、`ImageStream.FromFile` の拡張子を変更するだけです。マルチページ TIFF では各ページをループ処理できます：

```csharp
for (int i = 0; i < tiffPageCount; i++)
{
    ImageStream page = ImageStream.FromFile($"input_{i}.tiff");
    OcrResult result = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

このスニペットは、**OCR の精度を向上させる方法** をバッチ処理に拡張する例です。

## よくある落とし穴と対処法

| Symptom | Likely Cause | Quick Fix |
|---------|--------------|-----------|
| 空の出力 | 前処理でしきい値が強すぎて画像が真っ白になる | `NoiseRemovalStrength` を下げるか `AdaptiveThreshold = false` に設定 |
| 文字化け | 言語モデルが間違っている（デフォルトは英語） | `ocrEngine.Settings.Language = Language.English;` で正しい言語を設定、またはカスタム言語パックをロード |
| 大容量ファイルでクラッシュ | 高解像度画像によるメモリ不足 | 認識前に `ocrEngine.Settings.ImageResizeFactor = 0.5;` で縮小 |
| 回転したスキャンで出力なし | `AutoDeskew` が無効化されている | `AutoDeskew = true` にするか、正しい `DeskewAngle` を指定 |

これらを意識すれば、**OCR の精度を向上させる方法** を本番パイプラインで実装する際のデバッグ時間を大幅に削減できます。

## ボーナス: 速度 vs. 精度の調整

1 日に数千枚のレシートを処理する場合は速度を優先します。`AdaptiveThreshold` をオフにし、`NoiseRemovalStrength = 1` に設定してください。逆に、1 文字の見落としが致命的になる法的文書の場合は、すべてのフラグをオンにし、`NoiseRemovalStrength` を 3 に上げることを検討してください。

## まとめ

C# で Aspose OCR を使用した **OCR の精度を向上させる方法** を、エンジン作成、前処理設定（*画像をデスクューする方法* と *ノイズを除去する方法* の要）、JPG の読み込み、テキスト認識、エッジケース処理まで一通り解説しました。コードは自己完結型で、すぐに実行でき、**JPG からテキストを認識** し **画像からテキストを抽出** するために必要な手順をすべて示しています。

### 次のステップは？

- 他の画像フォーマット（PNG、TIFF）でも同じ設定がどのように動作するか試してみる。  
- OCR 出力をデータベースや

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}