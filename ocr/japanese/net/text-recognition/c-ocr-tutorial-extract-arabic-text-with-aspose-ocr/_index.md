---
category: general
date: 2026-04-01
description: c# OCRチュートリアル：アラビア語テキストの抽出方法、OCR用画像の前処理、Aspose OCRを使用した画像からのテキスト認識をステップバイステップで解説。
draft: false
keywords:
- c# ocr tutorial
- extract arabic text
- preprocess image for ocr
- recognize text from image
- aspose ocr c# example
language: ja
og_description: C# OCRチュートリアルで、アラビア語テキストの抽出、画像の前処理、そして Aspose OCR を使用した画像からのテキスト認識をステップバイステップで解説します。
og_title: c# OCR チュートリアル – Aspose OCRでアラビア語テキストを抽出
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# OCRチュートリアル – Aspose OCRでアラビア語テキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-arabic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr チュートリアル – Aspose OCR でアラビア語テキストを抽出する

実際に写真からアラビア語のサインを抜き取れる **c# ocr tutorial** が必要だったことはありませんか？ 頭を抱える必要はありません。多くのプロジェクトで最大の障壁はライブラリではなく、エンジンが右から左のスクリプトを読めるように画像を十分にきれいにすることです。このガイドでは、すぐに実行できるソリューションを提供し、各設定がなぜ重要かを説明し、**extract arabic text** を確実に行う方法を示します。

このチュートリアルでは、Aspose OCR パッケージのインストール、精度向上のための画像前処理、そして最終的に **recognize text from image** ファイルを実行する手順を順に解説します。最後まで実行すれば、コンソールにアラビア文字を出力する自己完結型プログラムが完成し、各オプションのトレードオフも理解できるようになります。外部ドキュメントは不要です—必要な情報はすべてここにあります。

## 必要なもの

- **.NET 6.0**（または NuGet をサポートする任意の .NET Core / .NET Framework バージョン）
- Visual Studio 2022 または C# 拡張機能付き VS Code
- アラビア語テキストを含む画像（例: `arabic_sign.jpg`）
- 有効な Aspose OCR ライセンス（開発用の無料トライアルでも可）

これらが揃っていれば、すぐにコードに取り掛かれます。

## ステップ 1 – .NET 用 Aspose OCR のインストール

最初に NuGet からライブラリを取得します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の UI が好きな場合は、**Dependencies → Manage NuGet Packages** を右クリックし、**Aspose.OCR** を検索して **Install** をクリックします。これにより `Aspose.OCR` アセンブリとすべてのトランジティブ依存関係がプロジェクトに追加されます。

> **Pro tip:** 最新の安定版（2026年4月時点で 23.9）を使用してください。新しいリリースにはアラビア語向けの言語固有改善が含まれることが多いです。

## ステップ 2 – OCR 用画像の前処理

アラビア文字は傾きやノイズに敏感です。画像をきれいにするだけで認識率が 70 % から 95 % 以上に向上します。Aspose OCR には `PreprocessOptions` オブジェクトが用意されており、auto‑deskew と denoising を切り替えることができます。

```csharp
using Aspose.OCR;
using System;

class ArabicDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with Arabic
        OcrEngine ocrEngine = new OcrEngine { Language = Language.Arabic };

        // 2️⃣ Turn on preprocessing – auto‑deskew + low‑level denoise
        ocrEngine.PreprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,                // Straightens rotated text
            DenoiseLevel = DenoiseLevel.Low   // Removes speckles without blurring characters
        };
```

**Why this matters:**  
- **AutoDeskew**: 多くのカメラ撮影は数度の軸外れがあります。アルゴリズムはテキストのベースラインを検出しビットマップを回転させ、OCR が文字をスラッシュやドットとして誤読するのを防ぎます。  
- **Low Denoise**: アラビア文字は点が多く、過度のノイズ除去はそれらを消してしまい “ب” が “ن” に変わることがあります。`Low` 設定はバランスの取れたレベルです。

特にノイズが多いスキャンの場合は、`DenoiseLevel` を `Medium` または `High` に上げてみてください。ただし出力を確認し、過剰なフィルタリングでダイアクリティックが消えていないか注意しましょう。

## ステップ 3 – 画像からアラビア語テキストを認識する

前処理した画像をエンジンに渡します。`Recognize` メソッドは抽出された文字列と信頼度スコアを保持する `OcrResult` を返します。

```csharp
        // 3️⃣ Run OCR on the target image file
        // Replace the path with the actual location of your Arabic sign picture
        string imagePath = @"YOUR_DIRECTORY/arabic_sign.jpg";
        OcrResult ocrResult = ocrEngine.Recognize(imagePath);
```

注意すべき点は以下の通りです：

| 状況 | 対応策 |
|-----------|------------|
| 画像が **グレースケール** なのに暗く見える | `Recognize` を呼び出す前に `ocrEngine.ImageProcessingOptions.IsGrayScale = true` を設定します。 |
| テキストが **15° 超** で回転している | まずビットマップを手動で回転させてください。auto‑deskew は約 10° 未満で最も効果的です。 |
| 行ごとの **confidence** が必要 | `ocrResult.Regions` コレクションを使用します。各領域には `Confidence` プロパティがあります。 |

## ステップ 4 – 抽出されたアラビア語テキストの表示と検証

最後に結果を出力します。デモではコンソール出力で問題ありませんが、実運用ではデータベースに保存したり翻訳サービスに渡したりすることが考えられます。

```csharp
        // 4️⃣ Show the recognized Arabic text in the console
        Console.WriteLine("Detected Arabic text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Expected Output

`arabic_sign.jpg` にフレーズ “مكتبة المدينة” が含まれている場合、コンソールには次のように表示されます：

```
Detected Arabic text:
مكتبة المدينة
```

右から左への順序が保持されていることに注意してください—Aspose OCR は双方向スクリプトを自動的に処理します。

## よくある落とし穴とヒント  

### 1. フォントの互換性  
一部の OCR エンジンは装飾的なアラビア語フォントに苦戦します。ベストな結果を得るには **Tahoma**、**Arial**、または **Traditional Arabic** といった一般的なフォントを使用してください。画像を自前で生成できる場合は、クリーンでコントラストの高いフォントを選びましょう。

### 2. 画像解像度  
**300 dpi** 以上の解像度が推奨されます。これ未満だとエンジンがダイアクリティックを誤認識することがあります。低解像度画像は `System.Drawing` を使ってアップスケールしてから Aspose に渡すことができます：

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

Bitmap Upscale(Bitmap src, int scaleFactor = 2)
{
    int newWidth = src.Width * scaleFactor;
    int newHeight = src.Height * scaleFactor;
    Bitmap bmp = new Bitmap(newWidth, newHeight);
    using (Graphics g = Graphics.FromImage(bmp))
    {
        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
        g.DrawImage(src, 0, 0, newWidth, newHeight);
    }
    return bmp;
}
```

### 3. ライセンスの配置  
トライアル版を使用している場合、出力に **watermark** 行が含まれます。ライセンスファイル (`Aspose.Total.lic`) を実行ファイルのフォルダーに置くか、`License license = new License(); license.SetLicense("Aspose.Total.lic");` を `OcrEngine` を作成する前に組み込んでください。

### 4. 多言語ドキュメント  
ページにアラビア語と英語が混在している場合は `ocrEngine.Language = Language.Multilingual;` を設定し、必要に応じて言語ヒントリストを提供します。エンジンは各ブロックを自動検出します。

## 完全動作サンプル  

以下は新しいコンソールプロジェクト（`dotnet new console`）にコピー＆ペーストできる完全なプログラムです。`YOUR_DIRECTORY/arabic_sign.jpg` を実際の画像パスに置き換えてください。

```csharp
using Aspose.OCR;
using System;

class ArabicDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine for Arabic
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.Arabic
        };

        // -------------------------------------------------
        // 2️⃣ Enable preprocessing (auto‑deskew + low denoise)
        // -------------------------------------------------
        ocrEngine.PreprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Low
        };

        // -------------------------------------------------
        // 3️⃣ Recognize the image
        // -------------------------------------------------
        string imagePath = @"YOUR_DIRECTORY/arabic_sign.jpg";
        OcrResult ocrResult = ocrEngine.Recognize(imagePath);

        // -------------------------------------------------
        // 4️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("Detected Arabic text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

`dotnet run` で実行すると、ターミナルにアラビア語文字列が表示されます。

## デモの拡張  

- **バッチ処理** – フォルダーをループし、結果を CSV に集計。  
- **Azure Blob Storage との統合** – クラウドから画像を取得し OCR を実行、テキストを再び保存。  
- **後処理** – `System.Globalization.StringInfo` を使用してアラビア語の合字を正規化したり、不要な Unicode 制御文字を除去したりします。

これらはすべて、**c# ocr tutorial** と **aspose ocr c# example** の基本をマスターした後の自然な次ステップです。

## 結論  

これで **c# ocr tutorial** として、画像を前処理し **preprocess image for ocr**、その後 **recognize text from image** を Aspose OCR ライブラリで実行して **extract arabic text** を行う完全な手順が手に入りました。コードは完結しており、各設定の背景も説明済みです。さらに、一般的な落とし穴を回避する実用的なヒントも紹介しました。

ぜひ色々試してみてください：異なる denoise レベル、ハイ解像度スキャン、あるいは翻訳 API と組み合わせるなど。初期化、前処理、認識、表示というパターンは言語やソースに関係なく共通です。

混合スクリプト文書の取り扱いやライセンスに関する質問があれば、下のコメント欄にどうぞ。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}