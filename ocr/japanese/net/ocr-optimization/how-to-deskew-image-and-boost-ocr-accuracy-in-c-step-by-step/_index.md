---
category: general
date: 2026-04-17
description: Aspose.OCR を使用して画像を素早くデスケューする方法 – 画像 OCR の読み込み、画像 OCR の前処理、そして高精度でテキスト画像を認識する方法を学びましょう。
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: ja
og_description: C#で画像の傾き補正を行い、OCR精度を向上させる方法。Aspose.OCRを使用して画像を読み込み、前処理し、テキストを認識する手順を学びます。
og_title: 画像の傾き補正方法 – 完全なC# OCRチュートリアル
tags:
- Aspose.OCR
- C#
- Image Processing
title: C#で画像の傾き補正とOCR精度向上を行う方法 – ステップバイステップガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正と OCR 精度向上（C#）

**画像の傾き補正** は、写真からテキストを抽出する際に、画像が完全に整列していない場合に頻繁に直面する課題です。このガイドでは、画像の読み込み、前処理、そして最終的に **テキスト画像認識** を Aspose.OCR の強力なフィルタチェーンで実行する手順を解説します。

レシートや看板、スキャンしたフォームなどをスマートフォンで撮影し、文字が歪んで読めない経験がある方は、そのフラストレーションをご存知でしょう。朗報は、数行の C# コードで画像をまっすぐにし、ノイズを除去し、実際に利用できるクリーンな文字列を取得できることです。また、前処理手順を調整することで **OCR 精度の向上** も可能です。

## 必要なもの

- .NET 6.0 以降（.NET Core でも動作します）  
- **Aspose.OCR** のライセンスまたは評価版（NuGet で入手可能）  
- 多少回転している、またはノイズがある画像ファイル（例: `skewed_photo.png`）  

サードパーティのツールは不要です。Aspose.OCR ライブラリと少しの C# 知識があれば始められます。

![画像の傾き補正例](/images/deskew-demo.png "画像の傾き補正 – 元画像 vs 補正後")

---

## 手順 1 – 画像 OCR の読み込み: ソースファイルの準備

画像をまっすぐにする前に、まずメモリに読み込む必要があります。`OcrImage.FromFile` メソッドがこれを行います。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **ポイント:** 画像を `OcrImage` として読み込むことで、OCR エンジンがピクセルデータに直接アクセスでき、後続の **画像前処理 OCR** 手順が正しく機能します。ファイルパスが間違っていると `FileNotFoundException` が発生するので、パスを必ず確認してください。

## 手順 2 – 画像前処理 OCR: 傾き補正フィルタチェーンの構築

ここからが **画像の傾き補正** の核心です。Aspose.OCR には任意の順序で積み重ねられるフィルタが多数用意されています。実際の写真では次の順序が一般的です。

1. **Deskew** – 回転を補正  
2. **Denoise** – 塩胡椒ノイズを除去  
3. **ContrastEnhance** – 薄い文字を際立たせる  

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **プロのコツ:** 画像がすでに十分に露出されている場合は `ContrastEnhanceFilter` を省略できます。処理が減るほど実行速度が速くなります。

### エッジケース

- **極端な回転 (>45°):** `DeskewFilter` は約 30° までが最適です。より大きな角度の場合は、まず手動で回転させてから (`filteredImage.Rotate(…)`) 使用してください。  
- **カラー背景:** デノイズ前にグレースケールに変換すると効果的です（`filteredImage = filteredImage.ToGrayscale();`）。

## 手順 3 – テキスト画像認識: OCR エンジンの実行

クリーンでまっすぐになったビットマップが用意できたら、文字抽出を行います。

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **内部で何が起きているか？** `OcrEngine` はニューラルネットワークベースの認識器で、ほぼ垂直で高コントラストな画像を前提としています。そのため、前述の **画像前処理 OCR** 手順が **OCR 精度の向上** に不可欠です。

### 期待される出力

元の写真に「Invoice #12345 – Total $89.99」という行が含まれていた場合、コンソールには次のように表示されます。

```
Invoice #12345 – Total $89.99
```

文字化けが見られる場合は、フィルタチェーンを見直してください。追加のシャープ化（`new SharpenFilter()`）が必要なことがあります。

## 手順 4 – OCR 精度向上のための微調整

傾き補正だけでなく、フォントや低解像度スキャンに対して OCR が失敗することがあります。以下の簡単な調整を試してみてください。

| 問題 | 対策 |
|------|------|
| 小さなフォントサイズ (<10 pt) | 画像を拡大する (`filteredImage = filteredImage.Resize(2.0);`) |
| 薄いグレー文字が白背景にある | コントラストをさらに上げる (`new ContrastEnhanceFilter(1.5)`) |
| 複数言語が混在 | `ocrEngine.Language = OcrLanguage.Multilingual;` を設定 |

これらの調整により、コード構造を変えることなく **OCR 精度の向上** が期待できます。

## 完全動作サンプル

以下は、上記手順をすべて組み込んだ、すぐに実行可能なプログラムです。新しいコンソールプロジェクトに貼り付けて **F5** キーで実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行すると、クリーンで傾き補正されたテキストがコンソールに表示されます。

## よくある質問と回答

**Q: PDF でも動作しますか？**  
A: はい。`Aspose.PDF` などで各 PDF ページを画像に変換し、同じフィルタチェーンに渡すだけです。

**Q: 画像がすでに完全に整列している場合はどうすれば？**  
A: `DeskewFilter` はほぼゼロの角度を検出すると何も変更せずにそのまま通過させます。問題ありません。

**Q: 複数画像を一括処理できますか？**  
A: もちろんです。`foreach (var path in Directory.GetFiles(...))` ループでコードを包み、各 `ocrResult.Text` をリストやファイルに保存すれば完了です。

---

## 結論

本稿では **画像の傾き補正** をプログラムで実現し、**画像 OCR の読み込み** 手順、堅牢な **画像前処理 OCR** パイプラインの適用、そして最終的な **テキスト画像認識** を Aspose.OCR で行う方法を示しました。フィルタを微調整したり、拡大やシャープ化を加えることで、さまざまな実務シーンで **OCR 精度の向上** が可能です。

次のステップに挑戦したいですか？このパイプラインを Web API に組み込んだり、`new BinarizationFilter()` を傾き補正前に追加して手書きノート認識に挑戦してみてください。可能性は無限大です—楽しいコーディングを！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}