---
title: OCR画像認識で複数ページの結果をドキュメントとして保存
linktitle: OCR画像認識で複数ページの結果をドキュメントとして保存
second_title: Aspose.OCR .NET API
description: Aspose.OCR for .NET の可能性を解き放ちます。この包括的なステップバイステップ ガイドを使用すると、複数ページの OCR 結果をドキュメントとして簡単に保存できます。
type: docs
weight: 14
url: /ja/net/ocr-optimization/save-multipage-result-as-document/
---
## 導入

Aspose.OCR for .NET を使用した光学式文字認識 (OCR) の魅力的な世界へようこそ!このチュートリアルでは、Aspose.OCR の機能を利用して、複数ページの OCR 結果をドキュメントとして保存する方法を検討します。経験豊富な開発者でも、OCR を始めたばかりでも、このガイドでは各ステップを順を追って説明し、この強力なツールを最大限に活用できるようにします。

## 前提条件

チュートリアルに入る前に、すべての設定が完了していることを確認してください。

1.  Aspose.OCR for .NET をインストールする: まず、Aspose.OCR for .NET をダウンロードしてインストールします。必要なファイルが見つかります[ここ](https://releases.aspose.com/ocr/net/).

2. 無料トライアルまたはライセンスを取得する: まだ取得していない場合は、無料トライアルを取得できます。[ここ](https://releases.aspose.com/)またはライセンスを購入する[ここ](https://purchase.aspose.com/buy).

3. ドキュメントを参照してください:[ドキュメンテーション](https://reference.aspose.com/ocr/net/)Aspose.OCR for .NET の場合。詳細な情報を得るには、頼りになるリソースです。

4. サポート フォーラムにアクセスする: 問題が発生したり、質問がある場合は、[サポートフォーラム](https://forum.aspose.com/c/ocr/16)は貴重なコミュニティリソースです。

これですべての準備が整ったので、ステップバイステップのガイドに進みましょう。

## 名前空間のインポート

必要な名前空間をインポートしてプロジェクトを開始します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## ステップ 1: ドキュメント ディレクトリを設定する

```csharp
//ドキュメントディレクトリへのパス。
string dataDir = "Your Document Directory";
```

必ず交換してください`"Your Document Directory"`ドキュメントディレクトリへの実際のパスを置き換えます。

## ステップ 2: Aspose.OCR を初期化する

```csharp
// AsposeOcr のインスタンスを初期化する
AsposeOcr api = new AsposeOcr();
```

のインスタンスを作成します`AsposeOcr`OCR 機能にアクセスします。

## ステップ 3: 画像を認識する

```csharp
//画像を認識する
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Aspose.OCR を利用して、複数の画像からテキストを認識します。画像ファイルに応じてファイルパスを調整します。

## ステップ 4: 結果を好みの形式で保存する

```csharp
//結果を好みの形式で保存します
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

希望の形式 (Docx、Text、Pdf、または Xlsx) を選択し、OCR 結果を複数ページのドキュメントとして保存します。

## 結論

おめでとう！ Aspose.OCR for .NET を使用して、複数ページの OCR 結果をドキュメントとして保存する方法を学習しました。この多用途ツールは、プロジェクトにおけるテキスト認識の可能性の世界を開きます。

## よくある質問

### Q1: 一時ライセンスはテスト目的で利用できますか?

 A1: はい、一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/) Aspose.OCR のテスト用。

### Q2: 異なる形式の画像からテキストを認識できますか?

A2：もちろんです！ Aspose.OCR はさまざまな画像形式をサポートし、OCR タスクの柔軟性を確保します。

### Q3: 認識する画像の数に制限はありますか?

A3: 処理できる画像の数はライセンスによって異なります。詳細についてはドキュメントを確認してください。

### Q4: OCR 認識中のエラーはどのように処理すればよいですか?

A4: エラー処理のベスト プラクティスについてはドキュメントを参照するか、サポート フォーラムで支援を求めてください。

### Q5: Aspose.OCR は英語以外の言語をサポートしていますか?

A5: はい、Aspose.OCR は複数の言語をサポートしています。言語サポートの詳細については、ドキュメントを参照してください。