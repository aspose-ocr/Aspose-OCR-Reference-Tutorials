---
date: 2025-12-21
description: Aspose.OCR for .NET を使用して OCR を実行し、画像からテキストを抽出する方法を学びましょう。このステップバイステップガイドでは、多言語テキスト認識と文字言語の選択方法を示します。
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Aspose.OCRで言語選択付きOCRを実行する方法
url: /ja/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR で言語選択付き OCR を実行する方法

## はじめに

画像上で **OCR を実行する方法** を必要とし、.NET アプリケーションで画像ファイルからテキストを抽出したい場合、Aspose.OCR for .NET は高速で高精度、かつ言語対応のソリューションを提供します。このチュートリアルでは、言語選択付き OCR 画像認識を実演する実践的な例を順を追って解説しますので、数行のコードで画像から多言語テキストを取得できます。

## クイック回答
- **Aspose.OCR は何をしますか？** 画像内の印刷文字および手書き文字を認識し、抽出されたテキストを返します。  
- **言語を選択できますか？** はい。English、German、Spanish、Chinese など、サポートされている任意の言語を指定できます。  
- **開発にライセンスは必要ですか？** 評価目的であれば無料トライアルで動作しますが、本番環境ではライセンスが必要です。  
- **対応している .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上です。  
- **傾き補正は自動ですか？** `AutoSkew` を有効にし、`SkewAngle` 設定で微調整できます。

## OCR タスクに Aspose.OCR を選ぶ理由

- **高精度**：さまざまなフォントや画像品質に対応します。  
- **組み込みの言語選択**：外部の言語パックが不要です。  
- **シンプルな API**：既存の C# プロジェクトにスムーズに統合できます。  
- **外部依存なし**：すべてローカルで実行され、データが安全に保たれます。

## 前提条件

コードに入る前に、以下の前提条件が整っていることを確認してください。

- Aspose.OCR for .NET: Aspose.OCR ライブラリがインストールされていることを確認してください。以下の [Aspose.OCR for .NET ダウンロードページ](https://releases.aspose.com/ocr/net/) からダウンロードできます。

- 開発環境: .NET アプリケーションの作業環境を設定してください。まだ設定していない場合は、詳細手順は [ドキュメント](https://reference.aspose.com/ocr/net/) を参照してください。

## 名前空間のインポート

.NET アプリケーションで、必要な名前空間をインポートします。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 手順 1: Aspose.OCR の初期化

まず Aspose.OCR クラスのインスタンスを初期化します。これにより、アプリケーションで OCR 機能を利用できるようになります。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 手順 2: 画像パスの指定

次に、OCR を実行したい画像へのパスを定義します。画像がアプリケーションからアクセス可能であることを確認してください。

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 手順 3: 言語選択で画像を認識する

ここからが OCR の本体です。Aspose.OCR ライブラリを使用して、指定した画像からテキストを認識します。言語選択を含む認識設定を調整します。

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## 手順 4: 結果の出力と表示

OCR 処理後、認識されたテキスト、領域、警告、JSON 表現などの結果を出力・表示します。

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## よくある問題とヒント

- **言語選択が間違っている** – 出力が文字化けしている場合は、`Language` プロパティが元画像の言語と一致しているか再確認してください。
- **傾いた画像** – 傾きがあるスキャン画像では、`AutoSkew` を有効にするか、`SkewAngle` を手動で調整して精度を向上させます。
- **大きなファイル** – 大容量画像はチャンクに分割して処理するか、`RecognizeImage` に渡す前に解像度を下げてメモリ使用量を抑えてください。

## 結論

おめでとうございます！Aspose.OCR for .NET を使用して、言語選択付き **OCR の実行方法** を学びました。このチュートリアルでは、画像ファイルからテキストを抽出し、認識設定をカスタマイズし、マルチ言語コンテンツを簡単に処理する方法を示しました。

## FAQ

### Q1: Aspose.OCR はマルチ言語テキスト認識に適していますか？

A1: はい。Aspose.OCR はさまざまな言語をサポートしており、マルチ言語 OCR タスクに柔軟に対応できます。

### Q2: 特定の画像特性に合わせて OCR 設定を微調整できますか？

A2: もちろんです！傾き角度、行認識、領域検出などのパラメータを調整して、さまざまなシナリオに最適な OCR を実現できます。

### Q3: 追加のサポートやコミュニティディスカッションはどこで見つけられますか？

A3: サポートやコミュニティとのディスカッションは、[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)をご覧ください。

### Q4: 無料トライアルは利用できますか？

A4: はい、[無料トライアル](https://releases.aspose.com/)で Aspose.OCR の機能を体験できます。

### Q5: Aspose.OCR for .NET を購入するには？

A5: 購入するには、[購入ページ](https://purchase.aspose.com/buy)をご覧ください。

---

**最終更新日:** 2025-12-21  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}