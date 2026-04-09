---
category: general
date: 2026-04-08
description: C#でAspose OCRを使用して画像からテキストを抽出します。OCRのための画像前処理方法と、精度を向上させる画像前処理方法を学びましょう。
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、OCR用の画像前処理方法と、最適な結果を得るための画像前処理方法を示します。
og_title: Aspose OCRで画像からテキストを抽出する – 完全C#ガイド
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Aspose OCRで画像からテキストを抽出する – 完全なC#ガイド
url: /ja/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR で画像からテキストを抽出 – 完全 C# ガイド

画像から **テキストを抽出** したいのに、結果がエラーだらけだったことはありませんか？ 開発者の多くが、画像が傾いていたり、ノイズが多かったり、コントラストが低いときに同じ壁にぶつかります。 良いニュースは、短い前処理ルーチンを加えるだけで、揺らいだスナップショットを OCR 用のクリーンなソースに変換でき、Aspose OCR ならその全工程がとても簡単になるということです。

このチュートリアルでは、Aspose OCR の組み込みフィルタを使って **画像を OCR 用に前処理する方法** を実例で解説し、数行の C# で **画像からテキストを抽出** する手順を示します。 最後まで実行可能なプログラムが手に入り、各フィルタの重要性が理解でき、独自のケースに合わせてパイプラインを調整できるようになります。

## 必要な環境

- .NET 6.0 以上（コードは .NET Framework 4.7+ でも動作します）
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）
- 傾いている、ノイズが多い、またはコントラストが低いサンプル画像（例: `skewed_noisy.jpg`）
- お好みの IDE（Visual Studio、Rider、VS Code など）

追加のネイティブライブラリや Web サービスは不要です。純粋な C# だけで完結します。

## Step 1: OCR エンジンの設定 – テキスト抽出の出発点

まずは `OcrEngine` インスタンスを作成し、認識対象の言語を指定します。 英語がデフォルトですが、 `"en"` を `"fr"`、`"de"` などに置き換えることができます。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**ポイント:** エンジンは内部辞書と各言語固有のヒューリスティックを保持しています。 言語設定を省略すると Aspose はデフォルトで英語を使用しますが、明示的に指定しておくと後でロケールを変更したときの予期せぬ挙動を防げます。

## Step 2: 前処理パイプラインの構築 – 最高の結果を得るための画像前処理

次にフィルタを追加します。 これらは OCR 前に自動で実行されるミニ写真編集スイートと考えてください。 以下の 3 つのフィルタが最も一般的な問題をカバーします。

| フィルタ | 修正対象 | 使用シーン |
|--------|---------------|----------------|
| `DeskewFilter` | 画像を水平に回転させる | 斜めに撮影された画像 |
| `DenoiseFilter` | ランダムな斑点や粒子を除去 | 低照度の写真やスキャン文書 |
| `ContrastStretchFilter` | コントラストを上げ、暗い文字を際立たせる | 薄れた印刷物や色あせたスクリーンショット |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**プロのコツ:** 順序が重要です。 まず Deskew、次に Denoise、最後に ContrastStretch の順に適用します。 順序を逆にすると、ノイズが除去されずに増幅されてしまうことがあります。

## Step 3: OCR の実行 – ついに画像からテキストを抽出

パイプラインが整ったら、エンジンに画像パスを渡します。 Aspose が自動でフィルタを適用し、認識アルゴリズムを実行します。

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

ファイルが見つからない場合は `FileNotFoundException` がスローされます。 開発中は絶対パスを使用し、運用時は相対パスや設定値に切り替えることを推奨します。

## Step 4: 結果の表示 – 取得したテキストを確認

`OcrResult` オブジェクトには生テキスト、信頼度スコア、各単語のバウンディングボックスが含まれます。 デモとしてコンソールにテキストだけを出力します。

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行すると、次のような出力が得られます。

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

出力が文字化けしている場合は、画像品質を再確認するか、追加フィルタ（例: バイナリ画像用の `BinarizationFilter`）を試してください。

## 完全動作サンプル – コピー＆ペーストで実行

以下は単体で動作する完全プログラムです。 `YOUR_DIRECTORY/skewed_noisy.jpg` を実際のテスト画像パスに置き換えてください。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力** – コンソールに画像内のプレーンテキストがそのまま表示されます。 たとえば画像に「OpenAI」というサインが写っていれば、余計な記号なしでその単語だけが出力されます。

## エッジケースとパイプラインの調整方法

### 1️⃣ 極暗画像

コントラストフィルタだけでは足りない場合は、`BrightnessCorrectionFilter` を先頭に追加します。

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ 多言語文書

`Language = "en+fr"`（カンマ区切りの言語コードをサポート）と設定し、エンジンに自動検出させたい場合は `LanguageDetectionFilter` を追加します。

### 3️⃣ 大容量 PDF を画像に変換して処理

千ページ規模の PDF を 1 枚ずつ処理すると遅くなります。 `Parallel.ForEach` を使って複数画像を同時に OCR できますが、`OcrEngine` はスレッドセーフでないため、スレッドごとに別インスタンスを作成してください。

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ バウンディングボックスの取得

各単語の位置情報が必要な場合は `ocrResult.Regions` を調べます。 各リージョンは `Rectangle` 座標を持ち、UI のオーバーレイに利用できます。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## よくある落とし穴（回避策付き）

- **Deskew を省略** – 2 度の傾きでも信頼度が 20 % 低下します。 ソースが完全に水平でない限り必ず `DeskewFilter` を追加してください。
- **高圧縮 JPEG の使用** – 圧縮アーティファクトがノイズと見なされます。 PNG や TIFF に切り替えると OCR 精度が向上します。
- **パスのハードコーディング** – ローカルでは相対パスが便利ですが、CI/CD パイプラインでは設定ファイルや環境変数から画像パスを取得するようにしましょう。

## セットアップのテスト手順

1. 高コントラストでクリーンな画像でプログラムを実行し、ほぼ完璧なテキストが得られることを確認します。  
2. ノイズが多く傾いた写真に差し替えて、3 つのフィルタを追加した後の出力が改善されているか検証します。  
3. フィルタを 1 つずつ除外して実行し、各ステップが結果に与える影響を体感します。これにより **なぜ** そのステップが必要かが理解できます。

## 結論

本稿では Aspose OCR を用いた **画像からテキストを抽出** の方法と、実務で役立つ **画像を OCR 用に前処理する** 手順を実演しました。 `DeskewFilter`、`DenoiseFilter`、`ContrastStretchFilter` を順に適用することで、エンジンに対してクリーンなキャンバスを提供し、認識精度が大幅に向上します。

ここからは、さらに高度なフィルタを試したり、マルチページ文書に対応したり、OCR 結果を検索インデックスに統合したりできます。 基本パターン（初期化 → 前処理 → 認識 → 結果利用）は変わりません。

レベルアップしたい方は、白黒スキャン向けの `BinarizationFilter` を試すか、結果をデータベースに保存して検索可能な PDF を作成してみてください。 コーディングを楽しみながら、Aspose が返すクリアで読みやすいテキストをぜひ体感してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}