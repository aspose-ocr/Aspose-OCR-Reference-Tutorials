---
date: 2025-12-22
description: Aspose.OCR for .NET を使用して画像からテキストを抽出する方法を学びましょう。このガイドでは、OCR 画像認識のための矩形の準備と精度向上の手順を案内します。
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCRで矩形を設定して画像からテキストを抽出する方法
url: /ja/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR画像認識で矩形を準備する

## はじめに

Optical Character Recognition (OCR) は、視覚的コンテンツを検索可能で編集可能なテキストに変換するために不可欠です。このチュートリアルでは、**画像からテキストを抽出**するために、OCR エンジンが特定の領域に焦点を当てるカスタム矩形を準備します。Aspose.OCR for .NET を使用し、プロジェクトの設定から認識されたテキストの取得まで、すべての手順を詳しく解説しますので、.NET アプリケーションに強力な画像‑テキスト変換機能を組み込むことができます。

## クイック回答
- **「画像からテキストを抽出する」とは何ですか？** 画像内の視覚的文字を機械が読み取れる文字列に変換することです。  
- **.NET でこれを支援するライブラリはどれですか？** Aspose.OCR for .NET。  
- **開発用にライセンスは必要ですか？** 無料トライアルでテスト可能です。商用利用にはライセンスが必要です。  
- **特定の領域だけを対象にできますか？** はい、矩形を定義して OCR の範囲を限定できます。  
- **サポートされている .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。

## 矩形を使用した「画像からテキストを抽出する」とは何ですか？
画像上に矩形領域を定義すると、OCR エンジンはその領域のみを処理します。これにより精度が向上し、処理時間が短縮され、ノイズの多い背景や不要な部分を無視できます。

## OCR の前に矩形を準備する理由
- **関連コンテンツに集中:** ヘッダー、フッター、装飾的なグラフィックをスキップ。  
- **パフォーマンス向上:** 小さな領域ほど認識が高速。  
- **精度改善:** ビジュアルノイズが減少し、結果がクリアに。

## 前提条件

- C# と .NET 開発の基本的な知識。  
- Aspose.OCR for .NET ライブラリがインストール済み – **[こちら](https://releases.aspose.com/ocr/net/)** からダウンロード可能。  
- テキスト抽出対象のサンプル画像（例: `sample.png`）。

## 名前空間のインポート

まず、必要な名前空間をスコープに持ち込みます。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ステップ1: ドキュメントディレクトリの設定

画像ファイルが格納されている場所を指定し、OCR エンジンのインスタンスを作成します。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 複数の矩形を使用して画像からテキストを抽出する方法

### ステップ2: 複数の矩形で画像を認識する

#### 2.1 矩形の定義

OCR エンジンに走査させたい領域を表す `Rectangle` オブジェクトのリストを作成します。

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR 認識の実行

画像パスと矩形リストを `RecognizeImage` に渡します。このメソッドは文字列のコレクションを返し、各エントリは 1 つの矩形に対応します。

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### ステップ3: 認識設定を使用して画像を認識する（代替アプローチ）

`RecognitionSettings` を使用したい場合、少し異なる API 呼び出しで同様の結果が得られます。

#### 3.1 認識設定の定義

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 認識されたテキストの表示

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 一般的な問題とヒント

- **矩形座標が正しくない:** `X`, `Y`, `Width`, `Height` の値が対象領域に正しくマッピングされていることを確認してください。  
- **画像品質:** 低解像度の画像は OCR 結果が悪くなる可能性があります。前処理（例: 二値化）を検討してください。  
- **結果が空:** 矩形内にテキストが含まれているか確認してください。含まれていなければ空文字列が返ります。

## 結論

Aspose.OCR for .NET を使用して、カスタム矩形を準備することで **画像からテキストを抽出**する方法を学びました。この手法により OCR 処理を細かく制御でき、アプリケーションに高速で高精度なテキスト抽出機能を組み込むことができます。

## よくある質問

**Q:** Aspose.OCR for .NET は他の .NET フレームワークでも使用できますか？  
**A:** はい、Aspose.OCR for .NET はさまざまな .NET フレームワークと互換性があります。

**Q:** Aspose.OCR for .NET の無料トライアルはありますか？  
**A:** もちろんです！無料トライアルは **[こちら](https://releases.aspose.com/)** から入手できます。

**Q:** Aspose.OCR for .NET のサポートはどこで受けられますか？  
**A:** 専用サポートは **[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)** でご利用ください。

**Q:** テスト目的の一時ライセンスは取得できますか？  
**A:** はい、**[こちら](https://purchase.aspose.com/temporary-license/)** から一時ライセンスを取得できます。

**Q:** Aspose.OCR for .NET のドキュメントはどこにありますか？  
**A:** ドキュメントは **[こちら](https://reference.aspose.com/ocr/net/)** にあります。

---

**最終更新日:** 2025-12-22  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}