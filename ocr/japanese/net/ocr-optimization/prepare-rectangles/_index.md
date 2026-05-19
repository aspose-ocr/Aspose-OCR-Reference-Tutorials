---
date: 2026-02-25
description: Aspose.OCR for .NET を使用して画像からテキストを抽出する方法を学びましょう。このガイドでは、OCR 画像認識用の矩形を準備し、精度を向上させる手順を案内します。
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCRで矩形を設定して画像からテキストを抽出する方法
url: /ja/net/ocr-optimization/prepare-rectangles/
weight: 11
---

< blocks/products/products-backtop-button >}}

Make sure to keep markdown formatting, code block placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR画像認識で矩形を準備する

## Introduction

光学文字認識（OCR）は、視覚的コンテンツを検索可能で編集可能なテキストに変換するために不可欠です。このチュートリアルでは、OCRエンジンを特定の領域に集中させるカスタム矩形を準備することで、**画像からテキストを抽出**します。Aspose.OCR for .NET を使用して、プロジェクトの設定から認識されたテキストの取得までのすべての手順を解説しますので、.NET アプリケーションに強力な画像からテキストへの機能を統合できます。

## Quick Answers
- **“画像からテキストを抽出”とは何ですか？** 画像内の視覚的文字を機械が読み取れる文字列に変換することを意味します。  
- **.NET でこれを支援するライブラリはどれですか？** Aspose.OCR for .NET。  
- **開発にライセンスは必要ですか？** テストには無料トライアルで動作しますが、本番環境ではライセンスが必要です。  
- **特定の領域を対象にできますか？** はい、OCR の範囲を制限する矩形を定義することで可能です。  
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。

## What is “extract text from image” with rectangles?

画像上に矩形領域を定義すると、OCR エンジンはその領域のみを処理します。これにより精度が向上し、処理時間が短縮され、ノイズの多い背景や不要な部分を無視できます。

## Why prepare rectangles before OCR?

- **関連コンテンツに集中:** ヘッダー、フッター、装飾的なグラフィックをスキップします。  
- **パフォーマンス向上:** 小さな領域は認識が速くなります。  
- **精度向上:** 視覚的ノイズが減少し、結果がクリーンになります。

## Why this matters for real‑world projects

領収書、請求書、身分証明書など多くのビジネス文書はレイアウトが混在しており、価値のあるテキストは特定の部分にしかありません。矩形を使用することで、必要なフィールドだけを抽出でき、後処理作業を大幅に削減し、オートメーションパイプライン全体の信頼性を向上させます。

## Common use cases

- **データ入力の自動化:** スキャンしたフォームから特定のフィールドを抽出します。  
- **コンプライアンスチェック:** 法的テキストブロックを分離して検証します。  
- **コンテンツインデックス作成:** 画像の見出しやキャプションのみを検索エンジン用にインデックスします。  

## Prerequisites

- C# と .NET 開発の知識があること。  
- Aspose.OCR for .NET ライブラリがインストールされていること – **[here](https://releases.aspose.com/ocr/net/)** からダウンロードできます。  
- 抽出したいテキストを含むサンプル画像（例: `sample.png`）。

## Import Namespaces

First, bring the required namespaces into scope:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Specify where your image files live and create an instance of the OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## How to extract text from image using multiple rectangles

### Step 2: Recognize Image with Multiple Rectangles

#### 2.1 Define the rectangles

Create a list of `Rectangle` objects that outline the areas you want the OCR engine to scan.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Perform OCR recognition

Pass the image path and the rectangle list to `RecognizeImage`. The method returns a collection of strings—each entry corresponds to one rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Step 3: Recognize Image with Recognition Settings (Alternative Approach)

If you prefer using `RecognitionSettings`, you can achieve the same result with a slightly different API call.

#### 3.1 Define recognition settings

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Display recognized text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Common Issues & Tips

- **矩形座標が正しくない:** `X`、`Y`、`Width`、`Height` の値が目的の領域に正しく対応していることを確認してください。  
- **画像品質:** 低解像度の画像は OCR 結果が悪くなる可能性があります。前処理（例: 二値化）を検討してください。  
- **結果が空:** 矩形が実際にテキストを含んでいるか確認してください。含まれていない場合、エンジンは空文字列を返します。

## Troubleshooting and Best Practices

| Symptom | Likely Cause | Remedy |
|---------|--------------|--------|
| 出力なしまたは空文字列 | 矩形が画像の範囲外 | 画像サイズと矩形座標を再確認する |
| 文字化け | コントラストが低い、またはノイズが多い | OCR 前に画像クリーニング（グレースケール、閾値処理）を適用する |
| 大きなファイルでパフォーマンスが低下 | 矩形が多すぎる、または画像が非常に大きい | 画像を分割するか、可能な限り矩形数を減らす |

## Conclusion

これで、Aspose.OCR for .NET を使用してカスタム矩形を準備し、**画像からテキストを抽出**する方法を学びました。この手法により OCR 処理を細かく制御でき、アプリケーションに高速で高精度なテキスト抽出機能を構築できます。

## Frequently Asked Questions

**Q:** Aspose.OCR for .NET は他の .NET フレームワークでも使用できますか？  
**A:** はい、Aspose.OCR for .NET はさまざまな .NET フレームワークと互換性があります。

**Q:** Aspose.OCR for .NET の無料トライアルはありますか？  
**A:** もちろんです！無料トライアルは **[here](https://releases.aspose.com/)** から利用できます。

**Q:** Aspose.OCR for .NET のサポートはどこで受けられますか？  
**A:** 専用サポートは **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** をご覧ください。

**Q:** テスト目的で一時ライセンスを取得できますか？  
**A:** はい、**[here](https://purchase.aspose.com/temporary-license/)** から取得できます。

**Q:** Aspose.OCR for .NET のドキュメントはどこにありますか？  
**A:** ドキュメントは **[here](https://reference.aspose.com/ocr/net/)** にあります。

---

**Last Updated:** 2026-02-25  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}