---
category: general
date: 2026-06-16
description: C#でAspose OCRを使用して画像をOCR用に前処理します。スキャン画像のコントラストを強化し、ノイズを除去して、正確なテキスト抽出を実現する方法を学びましょう。
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: ja
og_description: Aspose OCRでOCR用に画像を前処理します。画像のコントラストを強化し、スキャン画像のノイズを除去することで精度を向上させます。
og_title: C#でOCR用画像前処理 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: C#でOCR用画像前処理 – 完全ガイド
url: /ja/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCR用画像の前処理 – 完全ガイド

ソース写真はかなりはっきりしているのに、OCR の結果が文字化けしたように見えることはありませんか？実際、ほとんどの OCR エンジン（Aspose OCR を含む）は、きれいで整列された画像を期待しています。**Preprocess image for OCR** は、揺れた低コントラストのスキャンを鮮明で機械が読めるテキストに変える最初のステップです。

このチュートリアルでは、実用的なエンドツーエンドの例を通して、**preprocess image for OCR** だけでなく、Aspose の組み込みフィルタを使用して **enhance image contrast** と **remove noise from scanned image** の方法も示します。最後まで実行すれば、信頼性の高い認識結果を提供する C# コンソール アプリがすぐに動作するようになります。

---

## 必要なもの

- **.NET 6.0 以降**（コードは .NET Framework 4.6+ でも動作します）  
- **Aspose.OCR for .NET** – NuGet パッケージ `Aspose.OCR` を取得できます  
- ノイズ、歪み、コントラストが低いサンプル画像（デモでは `skewed-photo.jpg` を使用します）  
- 好きな IDE で構いません – Visual Studio、Rider、または VS Code が利用可能です  

追加のネイティブライブラリや複雑なインストールは不要です。すべて Aspose パッケージ内に収められています。

---

## ## OCR 用画像前処理 – ステップバイステップ実装

以下はコンパイルする完全なソースファイルです。新しいコンソール プロジェクトにコピー＆ペーストして **F5** を押すだけです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### 各フィルタが重要な理由

| Filter | 機能 | OCR に役立つ理由 |
|--------|------|-----------------|
| **DenoiseFilter** | 低照度スキャンでよく現れるランダムなピクセルノイズを除去します。 | ノイズが文字の一部と誤認識され、文字形状を損なう可能性があります。 |
| **DeskewFilter** | 主要なテキスト行の角度を検出し、画像を 0° に回転させます。 | 歪んだベースラインは OCR エンジンに文字が斜めだと認識させ、誤認識を引き起こします。 |
| **ContrastEnhanceFilter** | 暗い文字と明るい背景の差を拡大します。 | 高いコントラストは多くの OCR パイプライン内の二値化閾値処理を改善します。 |
| **RotateFilter** (optional) | 指定した手動回転を適用します。 | 自動デスクューが不十分な場合、例えば少し角度がついた写真などに便利です。 |

> **プロのコツ:** ソースがスキャンした PDF の場合、まずページを画像としてエクスポート（例: `PdfRenderer` を使用）し、同じフィルタチェーンに渡してください。同じ前処理ロジックが適用されます。

---

## ## OCR 前の画像コントラスト強化 – ビジュアル確認

フィルタを追加するだけでも効果はありますが、実際に効果を見ることは別です。以下はシンプルなビフォーアフターのイラストです（テスト時に自分のスクリーンショットに置き換えてください）。

![OCR 用画像前処理パイプラインの図](image.png){alt="OCR 用画像前処理パイプラインの図"}

左側は生のノイズが多いスキャンを示し、右側は **enhance image contrast**、**remove noise from scanned image**、そしてデスクュー後の同じ画像です。文字が鮮明かつ分離されていることに注目してください—まさに OCR エンジンが必要とする状態です。

---

## ## スキャン画像からノイズ除去 – エッジケースとヒント

すべての文書が同じ種類のノイズに悩んでいるわけではありません。以下は遭遇しうるシナリオとパイプラインの調整方法です。

1. **Heavy Salt‑and‑Pepper Noise** – カスタム `DenoiseOptions` オブジェクト（例: `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`）を渡すことで `DenoiseFilter` の強度を上げます。  
2. **Faded Ink on Yellow Paper** – コントラストを上げる前に背景色調を持ち上げるため、`ContrastEnhanceFilter` と `BrightnessAdjustFilter` を組み合わせます。  
3. **Colored Text** – 画像をまずグレースケールに変換します（`new GrayscaleFilter()`）。これは、Aspose を含むほとんどの OCR エンジンが単一チャンネルデータで最もうまく動作するためです。  

フィルタの順序を試すことも重要です。実務では、`DenoiseFilter` を `DeskewFilter` **より前に** 配置しています。クリーンな画像の方がデスクューアルゴリズムにとって信頼性の高いエッジデータを提供するからです。

---

## ## デモの実行と出力の検証

1. コンソール プロジェクトを **Build**（`dotnet build`）します。  
2. **Run**（`dotnet run`）します。以下のような出力が表示されるはずです：

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

出力にまだ文字化けが含まれる場合は、画像パスが正しいか、元ファイルがすでに解像度が低すぎないか（ほとんどの OCR タスクでは最低 300 dpi が推奨）を再確認してください。

---

## 結論

これで C# における **preprocess image for OCR** の堅牢で本番環境向けのパターンが手に入りました。Aspose の `DenoiseFilter`、`DeskewFilter`、`ContrastEnhanceFilter` を連結し（必要に応じて `RotateFilter` も）ことで、**enhance image contrast**、**remove noise from scanned image** が実現でき、以降のテキスト抽出の精度が大幅に向上します。

次は何をすべきか？クリーン化した画像をスペルチェックや言語検出などの後処理ステップに渡したり、生テキストを自然言語処理パイプラインに投入したりしてみてください。また、バイナリ専用ワークフロー向けに Aspose の `BinarizationFilter` を試したり、同じ前処理チェーンを使い回しながら別の OCR エンジン（Tesseract、Microsoft OCR）に切り替えることもできます。

まだ扱いにくい画像がありますか？コメントを残してください。一緒にトラブルシューティングします。コーディングを楽しんで、OCR の結果が常にクリアになることを願っています！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースは、ステップバイステップの解説と完全な動作コード例を含み、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [AspOCR の使い方: .NET 用画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [画像からテキスト抽出 – Aspose.OCR for .NET を使用した OCR 最適化](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET を使用した画像からテキスト抽出方法](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}