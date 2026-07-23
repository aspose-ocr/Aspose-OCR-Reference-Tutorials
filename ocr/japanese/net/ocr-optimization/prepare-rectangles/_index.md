---
date: 2026-07-23
description: Aspose.OCR for .NET を使用して画像から文字を抽出する方法を学びます。OCR の精度を向上させるために矩形を準備し、画像を効率的にテキストへ変換します。
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: OCR画像認識での矩形の準備
og_description: Aspose.OCR for .NET を使用して画像から文字を抽出する方法を学びます。OCR の精度を向上させるために矩形を準備し、画像を効率的にテキストへ変換します。
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: 矩形を使用した画像からの文字抽出 – OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: 矩形を使用した画像からの文字抽出 – OCRガイド
url: /ja/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 矩形で画像からテキストを抽出 – OCR ガイド

## はじめに

光学文字認識（OCR）を使用すると、画像ファイルから **extract text from image** を抽出でき、検索可能かつ編集可能になります。このチュートリアルでは、必要な領域にエンジンを集中させるカスタム矩形を作成することで OCR の精度を向上させる方法を示します。Aspose.OCR for .NET を使用し、プロジェクトのセットアップから認識文字列の取得までの全工程を確認でき、任意の .NET アプリケーションに信頼性の高い画像からテキストへの変換機能を組み込むことができます。

## クイック回答

- **What does “extract text from image” mean?** 画像内の視覚的文字を機械が読み取れる文字列に変換します。  
- **Which library handles this in .NET?** Aspose.OCR for .NET はフル機能の OCR エンジンを提供します。  
- **Do I need a license for production?** 開発には無料トライアルが使用できますが、デプロイには商用ライセンスが必要です。  
- **Can I limit OCR to specific zones?** はい。矩形を定義して、実際にテキストが含まれる領域のみを対象にできます。  
- **What .NET versions are supported?** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7 がサポートされています。

## 矩形を使用した “extract text from image” とは何ですか？

`extract text from image` プロセスは、定義された矩形領域内の文字を読み取り、その他の部分は無視します。OCR をこれらの領域に限定することで、精度が向上し、処理が高速化され、後処理の手間も減ります。この手法は、必要なテキストだけを抽出し、背景のグラフィックや装飾要素、OCR エンジンを混乱させる可能性のある視覚的ノイズを除去します。

## OCR の前に矩形を準備する理由

矩形を準備することで、OCR エンジンを画像の最も関連性の高い部分に集中させ、速度と精度の両方を向上させます。分析領域を絞ることで、エンジンが処理するデータ量が減り、結果が迅速になり、余計な視覚的ノイズによる誤認識が減少します。

- **Focus on relevant content:** ヘッダー、フッター、装飾的なグラフィックなど、エンジンを混乱させる要素をスキップします。  
- **Boost performance:** 小さな領域は計算量が少なく、大規模なスキャンで実行時間を最大 40 % 短縮します。  
- **Improve accuracy:** 視覚的ノイズを減らすことで、文字認識率が約 85 % から 95 %以上に向上します。

## 実務プロジェクトで重要な理由

領収書、請求書、身分証明書などのビジネス文書は、テキストとロゴやバーコードが混在しています。必要なフィールドに矩形を描くことで、価値あるデータだけを抽出し、下流のクリーニング作業を大幅に削減し、自動化ワークフローの信頼性を向上させます。このターゲット抽出により、後処理の手間が減り、データ取り扱い基準へのコンプライアンス維持にも役立ちます。

## 一般的なユースケース

- **Data entry automation:** スキャンしたフォームや経費領収書から特定のフィールドを抽出します。  
- **Compliance checks:** 法的条項や規制文言を分離して検証します。  
- **Content indexing:** 画像の見出しやキャプションだけをインデックス化し、検索エンジンでの可視性を高めます。

## 前提条件

- C# と .NET 開発の基本的な知識。  
- Aspose.OCR for .NET ライブラリをインストール – **[こちら](https://releases.aspose.com/ocr/net/)** からダウンロードするか、すべてのリリースは **[こちら](https://releases.aspose.com/)** で閲覧してください。  
- 抽出したいテキストを含むサンプル画像（例: `sample.png`）。

## 名前空間のインポート

`using` ステートメントは OCR エンジンとジオメトリクラスをスコープに取り込みます。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ステップ 1: ドキュメントディレクトリの設定

画像を格納するフォルダーを指定し、OCR エンジンのインスタンスを作成します。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 複数の矩形を使用して画像からテキストを抽出する方法

画像を一度読み込み、矩形のリストを OCR エンジンに渡します。各矩形は関心領域を定義し、エンジンは各領域ごに個別の文字列を返すため、フィールドを個別に処理し、必要に応じて結果を結合できます。

### 矩形の定義

`Rectangle` オブジェクトは、スキャンしたい各領域の X‑Y 座標とサイズを表します。

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### OCR 認識の実行

`RecognizeImage` メソッドは、提供された矩形リストを使用して画像を処理し、各領域の認識テキストを返します。

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## RecognitionSettings を使用して画像からテキストを抽出する方法（代替アプローチ）

設定ベースの呼び出しを好む場合は、`RecognitionSettings` を使用して同じ結果を得られます。このオブジェクトは矩形定義を言語、DPI、その他の OCR オプションと一緒にまとめ、シンプルな単一パラメータ API 呼び出しを提供します。

### 認識設定の定義

`RecognitionSettings` は、矩形リストと追加オプション（例: 言語、DPI）を単一のオブジェクトにまとめることができます。

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 認識テキストの表示

返された文字列を反復処理し、各領域のテキストを出力します。

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 一般的な問題とヒント

- **Incorrect rectangle coordinates:** `X`、`Y`、`Width`、`Height` が意図した領域に対応しているか確認してください。  
- **Image quality:** 低解像度や過度に圧縮された画像は OCR 結果を劣化させます。二値化などの前処理を検討してください。  
- **Empty results:** 矩形が実際に読み取れるテキストを含んでいるか確認してください。含まれていない場合、エンジンは空文字列を返します。

## トラブルシューティングとベストプラクティス

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|--------|
| 出力なしまたは空文字列 | 矩形が画像の範囲外 | 画像サイズと矩形座標を再確認してください |
| 文字化け | コントラストが低いまたはノイズが多い | OCR 前にグレースケール変換と閾値処理を適用してください |
| 大きなファイルでのパフォーマンス低下 | 矩形が多すぎる、または画像が非常に大きい | 画像を分割するか、可能な限り矩形数を減らしてください |

## 結論

これで、Aspose.OCR for .NET を使用してカスタム矩形を準備し、**extract text from image** を行う方法が分かりました。このアプローチにより OCR 処理を正確に制御でき、任意の .NET ソリューション向けに、より高速で高精度なテキスト抽出機能を提供できます。

## よくある質問

**Q:** Aspose.OCR for .NET を他の .NET フレームワークと併用できますか？  
**A:** はい、Aspose.OCR for .NET は .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7 で動作します。

**Q:** 無料トライアルは利用できますか？  
**A:** もちろんです！トライアルは **[こちら](https://releases.aspose.com/)** からダウンロードしてください。

**Q:** Aspose.OCR for .NET のサポートはどこで受けられますか？  
**A:** 専用のサポートは **[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)** でご確認ください。

**Q:** テスト用の一時ライセンスは取得できますか？  
**A:** はい、一時ライセンスは **[こちら](https://purchase.aspose.com/temporary-license/)** で入手可能です。

**Q:** 公式ドキュメントはどこにありますか？  
**A:** 完全な API リファレンスは **[こちら](https://reference.aspose.com/ocr/net/)** にあります。

---

**最終更新日:** 2026-07-23  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 関連チュートリアル

- [OCR 画像認識で段落用矩形を抽出する方法](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [OCR 画像の実行 – OCR 画像認識で画像に OCR を実行する方法](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Aspose.OCR for .NET を使用して画像からテキストを抽出する方法](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}