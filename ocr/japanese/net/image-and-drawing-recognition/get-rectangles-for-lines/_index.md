---
date: 2026-02-22
description: Aspose.OCR for .NET を使用して、画像内のテキスト行を認識し、行の矩形を抽出することで、レイアウト分析 OCR の実行方法を学びます。
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: レイアウト解析 OCR – 画像から行の矩形を取得
url: /ja/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# レイアウト分析 OCR – 画像から行の矩形を取得

## Introduction

このチュートリアルでは、Aspose.OCR for .NET を使用して **OCR 行矩形を取得する方法** を学びます。ガイドの最後までに、**画像内のテキスト行を認識**し、検出された各行の **行座標を抽出** できるようになります。これは、**レイアウト分析 OCR**、データ抽出、カスタムレンダリングなどの下流処理に最適です。

## Quick Answers
- **「OCR 行矩形を取得する」 とは何ですか？** 画像内で検出された各テキスト行のバウンディングボックスを返します。  
- **使用される API メソッドはどれですか？** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`。  
- **ライセンスは必要ですか？** 開発には無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **サポートされている画像形式は？** PNG、JPEG、BMP、TIFF など。  
- **.NET Core で実行できますか？** はい、Aspose.OCR は .NET Core および .NET 5/6 を完全にサポートしています。

## Prerequisites

チュートリアルに入る前に、以下の前提条件が揃っていることを確認してください：

- C# と .NET 開発の基本的な知識。  
- Visual Studio などの統合開発環境 (IDE)。  
- Aspose.OCR for .NET ライブラリがインストールされていること。ダウンロードは [here](https://releases.aspose.com/ocr/net/) から。  
- OCR 認識用のテキストを含むサンプル画像。

## Import Namespaces

プロジェクトに必要な名前空間がインポートされていることを確認してください。C# ファイルの先頭に以下の行を追加します：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

次に、OCR 画像認識で行の矩形を取得するプロセスを、簡単に追えるステップに分解します。

## layout analysis ocr – Step‑by‑Step Guide

### Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

「Your Document Directory」を、サンプル画像が格納されているフォルダーへの実際のパスに置き換えてください。

### Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

`AsposeOcr` クラスのインスタンスを作成して、OCR 機能にアクセスします。

### Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR を実行したい画像へのフルパスを定義します。

### Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` メソッドは `Rectangle` オブジェクトのリストを返し、各オブジェクトは検出されたテキスト行の座標を表します。これは **OCR 行矩形を取得する** の核心であり、**レイアウト分析 OCR** を可能にします。

### Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

検出された領域の座標をコンソールに出力します。後で **行座標を抽出** してカスタム処理に使用できる値が表示されます。

## Why Use Aspose.OCR for Line Rectangles?

- **高精度** – 高度なアルゴリズムにより、ノイズが多い画像や歪んだ画像でも行を検出します。  
- **クロスプラットフォーム** – .NET Framework、.NET Core、.NET 5/6 で動作します。  
- **外部依存なし** – 純粋な .NET ライブラリで、ネイティブ DLL を配布する必要がありません。  
- **豊富な出力** – 行矩形に加えて、単語、文字、信頼度スコアも取得できます。

## Common Issues and Solutions

| 問題 | 解決策 |
|-------|----------|
| **矩形が返されません** | 画像に明瞭で水平なテキストが含まれていること、かつ `AreasType.LINES` が指定されていることを確認してください。 |
| **座標が正しくありません** | 画像の DPI を確認してください。低解像度の画像は境界が不正確になる可能性があります。 |
| **大きな画像でのパフォーマンスボトルネック** | `GetRectangles` を呼び出す前に、画像を適切な解像度にリサイズしてください。 |
| **ライセンス例外** | テストにはトライアルライセンスを使用し、本番環境では評価制限を回避するためにフルライセンスを適用してください。 |

## Frequently Asked Questions

**Q: 行全体ではなく個々の単語を抽出できますか？**  
A: はい、同じ `GetRectangles` メソッドで `AreasType.WORDS` を使用すると、単語レベルのバウンディングボックスが取得できます。

**Q: API はマルチページ PDF をサポートしていますか？**  
A: まず各 PDF ページを画像に変換し、各画像に対して `GetRectangles` を呼び出してください。

**Q: 回転したテキストを処理するには？**  
A: OCR 設定で自動回転オプションを有効にするか、処理前に画像を事前に回転させてください。

**Q: 各行の信頼度スコアを取得する方法はありますか？**  
A: 矩形を取得した後、`api.RecognizeImage(...).Lines` を呼び出すと、信頼度値を含む行オブジェクトにアクセスできます。

**Q: どの .NET バージョンに対応していますか？**  
A: ライブラリは .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 に対応しています。

## Real‑World Use Cases

- **ドキュメントレイアウト分析 OCR** – 行矩形をレイアウトエンジンに入力して、カラム構造を再構築します。  
- **自動データ抽出** – 座標を使用して個々の行を切り抜き、下流の NLP パイプラインに渡します。  
- **カスタムレンダリング** – 元画像にバウンディングボックスをオーバーレイして、視覚的検証や UI オーバーレイに利用します。  

## Conclusion

おめでとうございます！Aspose.OCR for .NET を使用して画像から **OCR 行矩形を取得** できました。バウンディングボックスが手に入ったので、カスタムレンダリング、データ抽出、または **レイアウト分析 OCR** などの下流ワークフローに行座標を組み込むことができます。

---

**最終更新日:** 2026-02-22  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作成者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}