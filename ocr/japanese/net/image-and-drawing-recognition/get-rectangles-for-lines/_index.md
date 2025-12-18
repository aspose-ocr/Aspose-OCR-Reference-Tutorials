---
date: 2025-12-17
description: Aspose.OCR for .NET を使用して画像内のテキスト行を認識し、OCR 行矩形を取得して行座標を簡単に抽出する方法を学びましょう。
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: 画像テキスト行のOCRライン矩形を取得
url: /ja/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像テキスト行の OCR ライン矩形を取得する方法

## はじめに

このチュートリアルでは **Aspose.OCR for .NET** を使用して **OCR ライン矩形を取得する方法** を学びます。ガイドの最後までに、**画像内のテキスト行を認識**し、検出された各行の **ライン座標を抽出**できるようになります。レイアウト解析、データ抽出、カスタム描画など、下流処理に最適です。

## クイック回答
- **「OCR ライン矩形を取得する」とは何ですか？** 画像内で検出された各テキスト行のバウンディングボックスを返します。  
- **使用する API メソッドは？** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`。  
- **ライセンスは必要ですか？** 開発段階は無料トライアルで動作しますが、製品版は商用ライセンスが必要です。  
- **対応画像形式は？** PNG、JPEG、BMP、TIFF など多数。  
- **.NET Core でも実行できますか？** はい、Aspose.OCR は .NET Core および .NET 5/6 をフルサポートしています。

## 前提条件

チュートリアルに入る前に、以下の前提条件が整っていることを確認してください。

- C# と .NET 開発の基本知識。  
- Visual Studio などの統合開発環境 (IDE)。  
- Aspose.OCR for .NET ライブラリがインストール済み。ダウンロードは [こちら](https://releases.aspose.com/ocr/net/)。  
- OCR 認識用のテキストが含まれるサンプル画像。

## 名前空間のインポート

プロジェクトに必要な名前空間をインポートしてください。C# ファイルの先頭に以下を追加します。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

それでは、OCR 画像認識でラインの矩形を取得する手順を分かりやすく解説します。

## 手順 1: ドキュメントディレクトリの設定

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

`"Your Document Directory"` を、サンプル画像が格納されているフォルダーの実際のパスに置き換えてください。

## 手順 2: Aspose.OCR の初期化

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

`AsposeOcr` クラスのインスタンスを作成し、OCR 機能にアクセスします。

## 手順 3: 画像パスの指定

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR を実行したい画像のフルパスを定義します。

## 手順 4: 画像を認識し矩形を取得

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` メソッドは `Rectangle` オブジェクトのリストを返し、各オブジェクトが検出されたテキスト行の座標を表します。これが **OCR ライン矩形を取得する** コア部分です。

## 手順 5: 結果の出力

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

検出された領域の座標をコンソールに出力します。後で **ライン座標を抽出** してカスタム処理に利用できます。

## Aspose.OCR をライン矩形取得に使う理由

- **高精度** – ノイズや傾きのある画像でも行を検出する高度なアルゴリズム。  
- **クロスプラットフォーム** – .NET Framework、.NET Core、.NET 5/6 で動作。  
- **外部依存なし** – 純粋な .NET ライブラリで、ネイティブ DLL の配布が不要。  
- **豊富な出力** – ライン矩形に加えて、単語、文字、信頼度スコアも取得可能。

## よくある問題と解決策

| Issue | Solution |
|-------|----------|
| **矩形が返ってこない** | 画像に明瞭な水平テキストが含まれているか、`AreasType.LINES` が指定されているか確認してください。 |
| **座標が正しくない** | 画像の DPI を確認してください。低解像度画像は境界が不正確になることがあります。 |
| **大画像でパフォーマンスが低下** | `GetRectangles` を呼び出す前に、画像を適切な解像度にリサイズしてください。 |
| **ライセンス例外** | テスト時はトライアルライセンスを使用し、本番環境ではフルライセンスを適用して評価制限を回避してください。 |

## よくある質問

**Q: 行全体ではなく個々の単語を抽出できますか？**  
A: はい、同じ `GetRectangles` メソッドに `AreasType.WORDS` を指定すれば、単語レベルのバウンディングボックスが取得できます。

**Q: API はマルチページ PDF に対応していますか？**  
A: 各 PDF ページを画像に変換してから、各画像に対して `GetRectangles` を呼び出してください。

**Q: 回転したテキストはどう処理しますか？**  
A: OCR 設定で自動回転オプションを有効にするか、事前に画像を回転させてから処理してください。

**Q: 各行の信頼度スコアを取得できますか？**  
A: 矩形取得後に `api.RecognizeImage(...).Lines` を呼び出すと、信頼度を含む行オブジェクトが取得できます。

**Q: 対応 .NET バージョンは？**  
A: .NET Framework 4.5 以降、.NET Core 3.1 以降、.NET 5/6 に対応しています。

## 結論

おめでとうございます！Aspose.OCR for .NET を使用して、画像から **OCR ライン矩形を取得**できました。取得したバウンディングボックスを活用して、カスタム描画、データ抽出、レイアウト解析などの下流ワークフローにライン座標を組み込むことが可能です。

---

**最終更新日:** 2025-12-17  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}