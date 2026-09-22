---
category: general
date: 2026-02-09
description: Aspose OCR を使用して画像 OCR の前処理方法とテキスト画像の認識方法を学びましょう。画像のノイズを低減し、フィルターを追加し、数分でプレーンテキストを抽出できます。
draft: false
keywords:
- preprocess image OCR
- recognize text image
- extract plain text
- reduce image noise
- how to add filters
language: ja
og_description: 画像のOCRを迅速に前処理します。このガイドでは、フィルタを追加し、画像ノイズを低減し、任意の画像からプレーンテキストを抽出する方法を示します。
og_title: C#で画像OCRを前処理する – ステップバイステップチュートリアル
tags:
- OCR
- C#
- Image Processing
title: C#で画像OCRを前処理する – フィルタ付き完全ガイド
url: /ja/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-with-filters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像 OCR を前処理する – フィルタ付き完全ガイド

スキャンが歪んでいたり、粒子が多かったり、読みにくい画像で **画像 OCR の前処理** に苦労したことはありませんか？ あなただけではありません。実務では、レシートのブレた写真やノイズが多いスキャン画像が原因で、OCR エンジンが意味不明な文字列を出力してしまうことがよくあります。  

良いニュースは、エンジンに渡す前に画像をきれいにすれば、 **テキスト画像の認識** 精度が劇的に向上するということです。このチュートリアルでは、 **フィルタの追加方法**、ノイズ除去、そして最終的に **プレーンテキストの抽出** を Aspose.OCR for C# で行う手順を詳しく解説します。

ライブラリのインストールからコード実行、出力の検証まで、すべて網羅しているので、すぐに動くソリューションをコピーペーストできます。

---

## 必要なもの

- **.NET 6+**（または最近の .NET ランタイム；API の使い方は同じです）
- **Aspose.OCR for .NET** NuGet パッケージ  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 回転・ノイズ・コントラスト低下があるサンプル画像（例：`skewed_noisy.jpg`）
- お好みの IDE またはエディタ（Visual Studio、VS Code、Rider など）

以上です。追加のネイティブライブラリや重い画像処理フレームワークは不要です。Aspose に必要なフィルタがすべて含まれています。

---

## 手順 1 – OCR エンジン インスタンスの作成  

最初に `OcrEngine` を作成します。これは、画像をクリーンアップした後に文字を読み取る「脳」のようなものです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class FilterExample
{
    static void Main()
    {
        // Initialize the OCR engine – this object will hold our filters and settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **ポイント:** エンジンは **前処理パイプライン** を保持しています。後からフィルタを追加すると、`Recognize` を呼び出すたびに自動的に適用されます。

---

## 手順 2 – 画像ノイズを減らし可読性を向上させるフィルタを追加  

ここで **フィルタを追加** します。各フィルタは特定の欠点に対処します。

| フィルタ | 修正対象 | 典型的な設定値 |
|--------|----------|----------------|
| `DeskewFilter` | 傾いたテキスト（スキュー） | `MaxAngle = 12`（度） |
| `DenoiseFilter` | ランダムな斑点・粒子 | `Strength = 0.6`（0‑1） |
| `ContrastBoostFilter` | 薄くなった文字 | `Level = 1.3`（1‑2） |
| `BinarizeAdaptiveFilter` | 不均一な照明 | デフォルトで十分 |

```csharp
        // Step 2: Add preprocessing filters to improve image quality
        //   • Deskew to correct rotation (max 12°)
        //   • Denoise to reduce noise (strength 0.6)
        //   • Contrast boost to enhance visibility (level 1.3)
        //   • Adaptive binarization for better binarization
        ocrEngine.Preprocessing.Add(new DeskewFilter { MaxAngle = 12 });
        ocrEngine.Preprocessing.Add(new DenoiseFilter { Strength = 0.6 });
        ocrEngine.Preprocessing.Add(new ContrastBoostFilter { Level = 1.3 });
        ocrEngine.Preprocessing.Add(new BinarizeAdaptiveFilter());
```

> **プロのコツ:** 画像がすでに正立している場合はデスクュー処理を省略できます。不要なフィルタを削除すると処理速度が上がります。

---

## 手順 3 – 処理対象の画像を読み込む  

次に、エンジンにクリーンアップ対象の画像を指示します。`ImageStream.FromFile` はファイルを OCR エンジンが理解できる形式に変換します。

```csharp
        // Step 3: Load the image that needs OCR processing
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **エッジケース:** Web API からストリームで受け取る場合は、`FromFile` を `FromStream` に置き換えてファイルシステムへのアクセスを回避してください。

---

## 手順 4 – OCR エンジンを実行しテキスト画像を認識  

いよいよ魔法の瞬間です。エンジンは追加したすべてのフィルタを適用し、文字認識を行います。

```csharp
        // Step 4: Run the OCR engine on the prepared image
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **なぜ効果があるか:** 前処理パイプラインにより、認識器に渡される画像が可能な限りクリーンになるため、 **テキスト画像の認識** 精度が直接向上します。

---

## 手順 5 – プレーンテキストを抽出して表示  

最後に、プレーンテキスト結果を取得しコンソールに出力します。これがワークフローの **プレーンテキスト抽出** 部分です。

```csharp
        // Step 5: Output the recognized plain text
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

### 期待される出力

`skewed_noisy.jpg` にシンプルな請求書行 `Total: $123.45` が含まれている場合、次のように表示されます。

```
Total: $123.45
```

たとえ元ファイルが 10° 回転し、斑点があり、コントラストが低くても、フィルタが十分に画像をクリーンにし、OCR エンジンが正しく読み取れるはずです。

---

## ビジュアル概要  

以下は前処理パイプラインの簡易図です。コード実行に必須ではありませんが、フローをイメージしやすくなります。

![画像 OCR 前処理パイプライン](https://example.com/ocr-pipeline.png "画像 OCR 前処理パイプライン")

*Alt テキスト: 画像 OCR 前処理パイプラインは、デスクュー、デノイズ、コントラストブースト、適応二値化のステップを示しています。*

---

## よくある質問と落とし穴  

- **OCR 結果がまだ乱れている場合は？**  
  `DenoiseFilter.Strength` を `0.8` に上げるか、`ContrastBoostFilter.Level` を `1.1` に下げてみてください。コントラストを過度に上げるとハローが発生し、認識器が混乱することがあります。

- **独自のカスタムフィルタは追加できる？**  
  できます。Aspose.OCR では `IFilter` を実装し、`ocrEngine.Preprocessing` に注入できます。高度なトピックですが、ドメイン固有の前処理が必要なときに有用です。

- **PDF でも使えるか？**  
  各 PDF ページを画像に変換した後（例: Aspose.PDF を使用）であれば、同じフィルタチェーンを適用できます。

- **ライブラリはスレッドセーフか？**  
  `OcrEngine` インスタンスは **スレッドセーフではありません**。スレッドごとに別インスタンスを作成するか、呼び出しをロックで保護してください。

---

## サンプルの拡張例  

ベースができたので、次のステップを検討してください。

1. **バッチ処理** – フォルダ内の画像をループで処理し、各結果を `.txt` ファイルに書き出す。  
2. **言語パック** – フランス語やドイツ語を認識したい場合は、`ocrEngine.Language = "fra"`（または `"deu"`）で対応言語データをロード。  
3. **領域指定 (ROI)** – `ocrEngine.Recognize(image, new Rectangle(x, y, width, height))` を使って特定領域だけを認識させれば、大きなスキャンでも高速化できます。

---

## 結論  

本ガイドでは、組み込みフィルタを順に追加して **画像 OCR の前処理** を行い、 **テキスト画像の認識** と **プレーンテキストの抽出** を実現しました。完全な実行可能コードは上部に示していますので、任意の C# プロジェクトに組み込んで信頼性の高い OCR 結果を得られます。  

優れた OCR の鍵は、強力なエンジンだけでなく「きれいな入力」にあります。画像ノイズを減らし、テキストを正しく整列させることで、認識器に最高のチャンスを与えましょう。  

フィルタ値をいじってみたり、別フォーマットの画像で試したり、他の Aspose ライブラリと組み合わせたりして自由に実験してください。問題があればコメントを残すか、Aspose の公式ドキュメントで各フィルタクラスの詳細を確認してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}