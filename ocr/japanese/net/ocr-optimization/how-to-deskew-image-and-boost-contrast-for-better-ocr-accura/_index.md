---
category: general
date: 2025-12-30
description: 画像の傾きを素早く補正し、画像からテキストを抽出しながらコントラストを強化してOCR精度を向上させる方法。
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: ja
og_description: 画像の傾きを素早く補正し、画像からテキストを抽出しながらコントラストを強化して OCR の精度を向上させる方法
og_title: 画像の傾き補正とコントラスト強化でOCR精度を向上させる方法
tags:
- OCR
- C#
- Image Processing
title: 画像の傾きを補正し、コントラストを強化してOCR精度を向上させる方法
url: /ja/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾きを補正し、コントラストを上げて OCR 精度を向上させる方法

スキャナーやスマートフォンで取得した画像の **画像の傾きを補正する方法** でお悩みですか？  
同じような問題に直面している開発者は多く、画像が少し傾いていたりノイズが多いと、OCR の出力が文字化けしてしまいます。  

良いニュースは、数行の C# コードで画像をまっすぐにし、背景をクリーンにし、さらにコントラストを上げるだけで、エンジンがテキストをプロのように読み取れるようになることです。このガイドでは、Aspose.OCR を使って **画像からテキストを抽出する** 方法と **画像内テキストを認識する** 方法も紹介し、常に **OCR 精度の向上** を意識します。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.7+ でもコンパイル可能）  
- **Aspose.OCR** NuGet パッケージ（バージョン 23.12 以上） – `dotnet add package Aspose.OCR` でインストール  
- 回転とノイズが入ったサンプル画像（例: `noisy_rotated.jpg`）  
- Visual Studio、VS Code、またはお好みの IDE  

以上だけです。追加のネイティブライブラリや重い OpenCV バインディングは不要です。純粋なマネージドコードだけで完結します。

---

## 手順 1: プロジェクトを作成し名前空間をインポート

まず新しいコンソール アプリを作成し、必要な名前空間をスコープに持ち込みます。このステップが以降のすべての基盤となります。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**重要なポイント:**  
`Aspose.OCR` が `OcrEngine` クラスを提供し、`Aspose.OCR.Filters` が `DeskewFilter` や `ContrastBoostFilter` といった便利な前処理フィルタを提供します。最初にインポートしておくことでコードがすっきりし、コンパイラにも使用意図が明確になります。

---

## 手順 2: OCR エンジンを初期化し Deskew フィルタを追加

ここで実際に **画像の傾きを補正する方法** を実装します。`DeskewFilter` は回転角度（最大角度を設定可能）を自動検出し、ビットマップを水平に戻します。

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**内部で何が起きているか:**  
フィルタは画像内の最長水平テキストラインをスキャンし、傾きを推定して逆回転を適用します。`MaxAngle` を 15° に制限することで、すでにまっすぐな画像が過度に補正されるのを防ぎます。

> **プロのコツ:** ソース画像が逆さまになる可能性がある場合は `MaxAngle` を 180° に設定してください。フィルタは正しい向きを検出します。

---

## 手順 3: Denoise フィルタでノイズを低減

ノイズの多いスキャンは、どんなに賢い OCR エンジンでも誤認識します。`DenoiseFilter` を追加すると、細部を失わずに斑点を平滑化できます。

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**必要な理由:**  
ノイズは偽のエッジを生成し、OCR アルゴリズムが文字として解釈してしまいます。`Strength` を `0.7` に設定すると、ほとんどのスキャン文書でバランスが取れます。極端にきれいな画像や非常に汚い画像では調整してください。

---

## 手順 4: コントラストを上げる – 「**コントラストを上げる方法**」の実装

ここで二次キーワード **コントラストを上げる方法** に答えます。`ContrastBoostFilter` は暗い文字と明るい背景の差を増幅し、文字を際立たせます。

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**理屈:**  
コントラストが高いほど、薄い筆跡が見逃される可能性が減ります。`Level` を `1.3` にすると、一般的な黒文字・白背景の文書でうまく機能します。カラー写真の場合は `1.5` 以上が必要になることがあります。

---

## 手順 5: OCR を実行しテキストを抽出

画像の前処理が完了したら、`Recognize` メソッドで **画像からテキストを抽出** します。メソッドは `OcrResult` オブジェクトを返し、生の文字列と信頼度スコアが含まれます。

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**取得できるもの:**  
`ocrResult.Text` にはエンジンが読み取れたプレーンテキストが格納されています。単語レベルの信頼度が必要な場合は `ocrResult.Regions` を調べてください。各領域には `Confidence` プロパティがあります。

---

## 完全動作サンプル（コピペ即使用）

以下は `Program.cs` に貼り付け可能な完全プログラムです。画像パスは実際に存在するファイルに置き換えてください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**期待される出力例:**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

結果が文字化けしている場合は、画像品質を再確認し、`Strength` や `Level` を調整するか、`MaxAngle` を上げてより積極的に傾きを補正してください。

---

## よくある質問とエッジケース

### 画像が逆さまの場合は？

`DeskewFilter` の `MaxAngle = 180` を設定してください。フィルタは 180° の回転を検出し、正しく反転します。

### カラー文書（例: 青いハイライトが入ったスキャンフォーム）  

コントラストブーストの前に `ColorFilter` を追加するか、手動でグレースケールに変換してみてください。

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### 多数のファイルをバッチ処理したい  

ディレクトリを走査する `foreach` ループで OCR ロジックをラップします。

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### OCR の信頼度はどうやって確認する？

`ocrResult.Regions` をチェックします。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

信頼度が 100% に近いほど、前処理がうまく機能したことを示します。

---

## OCR 精度を最大化するためのヒント

| ヒント | 効果の理由 |
|-----|--------------|
| **ロスレス画像形式を使用** (PNG, TIFF) | JPEG の圧縮はエッジをぼかし、認識精度を低下させます。 |
| **DPI を 300 以上に保つ** | 文字あたりのピクセル数が増えることで、エンジンが取得できる情報が増えます。 |
| **不要な余白をトリミング** | ノイズが減り、処理速度も向上します。 |
| **コントラストブースト後に二値化** (黒/白) を適用 | 文字と背景が2色になることで、ほとんどの OCR エンジンが好むシンプルな画像になります。 |
| **まず小サンプルでテスト** | `Strength` や `Level` を本格導入前に微調整でき、失敗リスクを減らせます。 |

---

## 結論

本稿では **画像の傾きを補正する方法**、**コントラストを上げる方法**、そして Aspose.OCR を用いた **画像からテキストを抽出する** 完全パイプラインを解説しました。`DeskewFilter`、`DenoiseFilter`、`ContrastBoostFilter` を順に適用し、`Recognize` を呼び出すだけで、実務で扱う多くのスキャン画像において **OCR 精度の向上** が実感できるはずです。

コードを実行し、フィルタパラメータを自分の文書に合わせて調整すれば、最も乱雑な写真からでもクリーンなテキストが取得できます。さらに踏み込むなら、言語固有の辞書を追加したり、出力をスペルチェッカーに通すことでポストプロセスを強化できます。

楽しいコーディングを！OCR の結果がいつでもクリアになることを願っています。

--- 

![画像の傾きを補正する例](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}